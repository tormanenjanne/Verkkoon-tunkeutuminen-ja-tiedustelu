# h2 nuuh

Koneen tiedot:
- Näytönohjain: AMD Radeon RX 6500M
- Prosessori: AMD Ryzen 5 5600H
- RAM: 8,00 Gt

## x) Lue ja vastaa lyhyesti kysymyksiin.

### WireShark

- Artikkelissa käydään Wiresharkin asennusohjeet vaiheittain, ja tärkeänä tässä asennusvaiheessa pidin itsellä sen, että pitää lisätä itsensä ryhmään, jotta voidaan nuuhkia verkkoliikennettä. Tämä tapahtuu komennolla: `sudo adduser "omakäyttäjä" wireshark`, ja tämän jälkeen buuttaa virtuaalikone.
- Wiresharkissa voidaan nähdä muun muassa protokolla hierarkiaa, listauksen päätelaitteen osoitteista sekä kaavion verkkoliikenteessä milloin paketteja liikkuu. Myös erilaisia suodattimia on, jos halutaan tarkastella tietyn protokollan liikkenne muun muassa: dns, tls, http, tcp, udp ja niin edelleen.

### Network Interface Names on Linux

- Artikkelissa avataan lukijalle, että verkkoliitäntä on tavallaan verkkokortti, mutta se ei ei ole fyysinen.
- Mistä tunnistan, mikä kuuluu verkkoliitäntä kuuluu mihinkin, voidaan päätellä esimerkiksi: "en == langallinen verkko", "wl == Wlaniin ja WiFi" ja `lo = loopback adapteri`. Näillä etuliittellä voidaan tunnistaa, millaista verkkoliitäntä haluamme kaapata esimerkkinä: `enp1s0 == langallinen verkkokortti`.
- Omat verkkoliitännät voidaan tarkistaa komennolla: `ip a` ja `ip route`

## Osoittaminen, että voin katkaista ja palauttamaan virtuaalikoneen internet-yhteyden

Avattuani virtuaalikoneen, ja pingaamalla terminaalissa `ping 8.8.8.8`, joka on Googlen nimipalvelin, huomaamme liikenteen liikkuvan. Liikenteen palauttaminen onnistuu katkaisemalla oikealta valikosta volume nappulan vierestä `Connected to the wired network`, ja täältä wired kohtaan "täppä" mustaksi. Verkkoliikenteen palauttaminen onnistuu painamalla wired kohtaa uudestaan, jotta se muuttuu siniseksi.

<img width="238" height="184" alt="kuva" src="https://github.com/user-attachments/assets/341e1560-eaf8-4179-8a7e-48bd3e65add9" />

Tässä vielä kuva, jossa verkkoliikenne toimii aluksi (wired kohta on sinisenä), liikenteen katkaisemisen jälkeen ei saada enään yhteyttä Googlen nimipalvelimeen (wired kohta on musta), ja lopuksi verkkoliikenteen palauttaminen normaaliksi (wired kohta on palautettu takaisin siniseksi).

<img width="726" height="402" alt="kuva" src="https://github.com/user-attachments/assets/78e6a06c-3848-4d7d-ba98-d23ea6474801" />

## Wireshark asennus sekä liikenteen sieppaaminen

Wiresharkin asennus suoritettiin tunnin aikana, ja tämä onnistui komennolla `sudo apt-get install wireshark`. Asentamisen aikana tuli banneri, jossa varmistettiin, että haluammeko muiden kuin superuserit sieppaamaan pakettaja, tähän vastataan `yes`. Näin saimme asennettua wiresharkin.

Huomiona on tässä aikasemmassa mainitussa (lue ja tiivistä wireshark tehtävä x), on lisätä itsensä Wireshark ryhmään, jotta pysty alkaa nuuskimaan verkkoliikennettä. Komento on siis `sudo adduser OmaKäyttäjäNimi wireshark`. Lopuksi buutataan vielä virtuaalikone, jotta päivitykset astuvat voimaan.

Liikenteen sieppaaminen onnistuu avaamalla Wireshark terminaalissa komennolla `wireshark`, joka avaa tämän ohjelman. Ohjelmasta valitsemme `enp0s3`, joka on meidän virtuaallinen langallinen verkkokortti.

<img width="816" height="411" alt="kuva" src="https://github.com/user-attachments/assets/0901ad36-3aab-4a03-8958-a500a0059aa3" />

Lopuksi vielä testasin, että saan siepattua liikennettä. Avasin Firefoxin, ja kirjoitin selaimeen `yle.fi`, ja tämän jälkeen Wiresharkissa alkoi verkkoliikenne liikkua, alhaalla vielä kuva tästä.

<img width="1105" height="233" alt="kuva" src="https://github.com/user-attachments/assets/6ab397ab-f5b0-4999-a6ae-875eebb70b81" />

## Osoita TCP/IP-mallin neljä kerrosta yhdestä siepatusta paketista

<img width="695" height="695" alt="kuva" src="https://github.com/user-attachments/assets/ad3486c8-c5d6-457d-9890-1dfe3ff31288" />


- Punainen laatikko: Tämä on TCP/IP kerroksesta Link kerros, joka lähettää ja vastaanottaa tietoa paikallisessa verkossa. tiedonsiirto toimii muun muassa Mac-osoitteilla.
- Sininen laatikko: TCP/IP kerroksen internet kerros, jossa näkyy kohde- sekä vastaanottajan ip-osoitteet. Tässä käytetään muun muassa IPv4- ja IPv6 prokollia sekä ICMP (Internet Control Message Protocol).
- Keltainen laatikko: TCP/IP kerroksen transport kerros, joka lähettää paketteja joko TCP ja UDP protokollan välityksellä. TCP on luotettavampi kuin UDP, ja tässä data saapuu järjestyksessä, ja . TCP toimii muun muassa sähköpostien lähetyksessä. UDP-protokolla voi tiputtaa paketteja, ja se ei ole niin varma kuin TCP. UDP-protokollaa käytetään muun muassa pelaamisessa tai striimaamisessa.
- Vihreä laatikko: TCP/IP kerroksen application kerros, jossa toimii muun muassa verkkoselaimet, sähköpostiohjelmat sekä tiedostojen jakamistyökalut. Protokollia tähän kuuluu muun muassa: HTTP, FTP,SMTP ja DNS.

## surfing-secure.pcap. Tutustu siihen pintapuolisesti ja kuvaile, millainen kaappaus on kyseessä. Tässä siis vain lyhyesti ja yleisellä tasolla. Voit esimerkiksi vilkaista, montako konetta näkyy, mitä protokollia pistää silmään. Määrästä voit arvioida esimerkiksi pakettien lukumäärää, kaappauksen kokoa ja kestoa.

Kaappauksessa huomataan, että käyttäjä on vieraillut muun muassa Googlessa, terokarvinen.com ja lopuksi vielä Goatcounter (tämä on avoimen lähdekoodin web-analytiikkatyökalu).

tutkimalla lisää tätä surfing-secure.pcap kaappausta, klikkaamalla ylhäältä `statistics` ja alasvetovalikosta `endpoints` näemme että mac-osoitteita on 2, ja IPv4-osoitteita 7.

<img width="836" height="168" alt="kuva" src="https://github.com/user-attachments/assets/a6af3c6a-75dd-41e6-82b6-e06430590c6d" />

Protokollia joita tässä sieppauksessa näkyy on muun muassa: DNS,QUIC,TCP,TLS ja ARP. Ylhäällä valikossa kohdassa klikkaamalla `Statistics` ja valikosta `Capture file properties` pääsemme näkemään pakettien lukumäärää, kaappauksen kokoa sekä kestoa.

<img width="913" height="765" alt="kuva" src="https://github.com/user-attachments/assets/6bf6e4fd-3eaf-4f49-9743-586a46475a11" />



**Punaisella** näkyy pakettien kokonaismäärä: 283. **Keltaisella** kestoa, joka on 7 sekuntia ja **Vihreällä** Kaappauksen koko on: 126kb

##  Minkä merkkinen verkkokortti käyttäjällä on?

Selvittämällä Wiresharkista ensimmäiseksi meidän kohde mac-osoite linkki kerroksesta. Huomaamme, että osoite saadaan selville, mutta tässä tapauksessa Wireshark ei näytä valmistajaa.

<img width="1061" height="667" alt="kuva" src="https://github.com/user-attachments/assets/0ab87db5-35c0-4d32-80a2-276fd75c8a7c" />

Mac-address lookupista löytyi tieto, joka viittaa joko Realtekin verkkokorttiin.

<img width="955" height="489" alt="kuva" src="https://github.com/user-attachments/assets/5423d8b9-61b0-4129-aa91-89358d54e1cc" />


## Millä weppipalvelimella käyttäjä on surffaillut?

Kirjottamalla filtteriin `dns` huomaamme että, käyttäjä on surffaillut muun muassa: google.com, terokarvinen.com, goathunter.com ja gc.zgo.at. Tiedot löytyivät `info` kohdasta.

<img width="1871" height="385" alt="kuva" src="https://github.com/user-attachments/assets/fa83dfe9-d5b5-4752-8de2-f4f5740ca46c" />

## Analyysi. Sieppaa pieni määrä omaa liikennettäsi. Analysoi se, eli selitä mahdollisimman perusteellisesti, mitä tapahtuu.

Pingasin terminaalissa Googlen nimipalvelimeen `ping 8.8.8.8`, ja analysoidaan tätä liikennettä.


<img width="892" height="670" alt="kuva" src="https://github.com/user-attachments/assets/891c49f3-47f6-4745-9da9-94ce697f3732" />

### Paketti 1
- Lähde ip on `10.0.2.15` ja kohde `8.8.8.8`.
- Protokolla on ICMP, joka toimii internet kerroksessa.
- Verkkokortti on `PCSSystemtec`. 
- Tässä lähetetään `ICMP echo request` pyyntö Googlen nimipalvelimeen `8.8.8.8`.
- Ensimmäinen paketti on lähtenyt `2026-10-28 11:12:35` ja viimeinen `2026-10-28 11:12:42`, kesto on ollut 7 sekuntia.
### Paketti 2
- Lähde ip on `8.8.8.8` ja kohde `10.0.2.15`.
- Sama protokolla kuin ensimmäisessä
- Tässä taas vastataan ensimmäisen paketin kyselyyn `ICMP echo reply` viestillä, että paketti on tullut perille.

## Ajankäyttö

-Käytin 27.10 1.5h raportin työstämiseen sekä 28.10 yhteensä noin 4-5h raportin työstämiseen ja tehtävien tekemiseen (Verkkokortti tehtävään meni yllättävän paljon aikaa...) 
  
## Lähteet
- Luettavissa: https://analytics-alternatives.com/goatcounter-review-2026/. Luettu 28.10.2026.
- GeekForGeeks 2026. TCP/IP Model. Luettavissa: https://www.geeksforgeeks.org/computer-networks/tcp-ip-model/. Luettu: 27.10.2026.
- Karvinen 2025. Wireshark - Getting started. Luettavissa: https://terokarvinen.com/wireshark-getting-started/. Luettu: 27.10.2026.
- Karvinen 2025. Network Interface Names on Linux: Luettavissa: https://terokarvinen.com/verkkoon-tunkeutuminen-ja-tiedustelu/#tehtavanannot. Luettu: 27.10.2026.


