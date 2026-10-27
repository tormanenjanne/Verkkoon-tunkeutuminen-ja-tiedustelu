# h2 Lempiväri: violetti

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





  
## Lähteet
- Karvinen 2025. Wireshark - Getting started. Luettavissa: https://terokarvinen.com/wireshark-getting-started/. Luettu: 27.10.2026.
- Karvinen 2025. Network Interface Names on Linux: Luettavissa: https://terokarvinen.com/verkkoon-tunkeutuminen-ja-tiedustelu/#tehtavanannot. Luettu: 27.10.2026.


