# h3 aaltoja harjaamassa

## x)

### Universal Radio Hacker

- Videolla käydään läpi, kuinka Universal Radio Hacker:lla voidaan analysoidan radio signaaleja, nauhoittaa pätkä signaaleista ja analysoida nauhoitusta jälkikäteen.
-  Autodetect parameters pystyy havaitsemaan automaattisesti bitit, keskikohdan ja toleranssit.
-  Bittien tarkastamisessa varmistetaan, että bitit ovat paketissa yhtä pitkiä kun `bit length` kentässä. Error tolerancea taas käytetään, jos bittien pituuksissa on eroja.
-  Jos hexadesimaalit ovat yhtä pitkät jokaisessa paketissa, tämä on merkki siitä, että demodulatointi on onnistunut. (Hubmartin 2019. 3.19-7.40 min)

### Decode 433.92 MHz weather station data

- Artikkeli sisältää, kuinka rtl_433 ohjelmalla voidaan purkaa tietoa erinäisistä laitteista. Tässä tapauksessa selvitellään artikkelin tekijänn ostamaa sääasemaa, jota käsitellä rtl_433 ja URH:lla.
- Tässä tapauksessa saatiin selville muun muassa laitteen nimen, lämpötilan ja ilmankosteuden, akun tilan ja monia muita.
- URH:lla etsitään oikea taajuus, ja tallennetaan taajuuden tiedot. Lopuksi demodulatioidaan ja näytetään digitaalista analyysia. (Cornelius 2022)

## b) Rtl_433 asennus, ja testaus toimivuudesta

Tämän työkalun asentamisen suoritin tunnin aikana, mutta käydään tämä vielä läpi. Ensimmäiseksi käytin komentoa` sudo apt-get -y install atool wget libssl-dev libtool libusb-1.0-0-dev librtlsdr-dev rtl-sdr libsoapysdr-dev`, jolla saatiin asennettua erilaisia työkaluja sekä kirjastoja. Seuraavaksi käytin komentoa `wget https://github.com/merbanan/rtl_433/releases/download/25.02/rtl_433-soapysdr-openssl3-Linux-amd64-25.02.zip`, jolla lataamme Githubista juuri tämän version, ja lopuksi purin paketin komennolla ` aunpack rtl*.zip`.

Lopuksi testasin toimivuutta komennolla `./rtl_433' `, joka ilmoitti työkalun toimivuudesta ja versiosta. (Karvinen 2026)

<img width="721" height="75" alt="kuva" src="https://github.com/user-attachments/assets/250e1913-22c6-42f5-ad48-6e8ee6305e6a" />

## c) Automaattinen analyysi, mitä tapahtuu ja mitä tunnisteita löysin

Kävin lataamassa tiedoston Tero Karvisen sivustoilta, ja tämän tehtävänannon kohdasta c. Siirsin tämän työpöydälle, ja komennolla `rtl_433 -r Converted_433.92M_2000k.cs8` sain avattua tämän tiedoston.

<img width="937" height="339" alt="kuva" src="https://github.com/user-attachments/assets/95b0ec50-fe05-44e2-b55f-6e6701ba5dd1" />

Kuvassa näkyy kolme eri näytettä, mutta todellisuudessa tämä sama kaava toistuu neljä kertaa. Eli lopputuloksena tässä tiedostossa on yhteensä 12 näytettä.



- Näytteitä on ainakin yhteensä 12 kappaletta.
- Time: Näyttää milloin signaaliin ollaan havaittu.
- Model: KlikAanKlikUit-Switch, nexa security ja klikaanklikuit-Switch (nämä ovat eri laitteita, joihin ollaan saatu yhteys)
- Channel: kanava 3, jota ollaan käytetty
- id: Prove security ja klikaanklikuit-Switch on sama id-numero. **Prove-securityllä on sama id, mutta edessä on housecode id:n sijaan**
- State: näyttää off.
- Group call: 0, ei lähetä muille laitteille tietoa tästä.

Selvitin ensimmäiseksi Googlesta mitä nämä yritykset ovat, ja mitä ne tekevät.( Yritykset: Proove-security, klikaanklikuit ja Nexa-scurity). klikaanklikuit on yritys, joka tekee erilaisia älylaitteita muun muassa ip-kameroita ja kytkimiä, joilla voidaan valvoa esimerkiksi omaa kotia (esimerkissä on house code: 8785315). Proove-security valmistaa myös näitä ip-kameroita, ja monia muita erilaisia laitteita viimeiseksi Nexa-Security valmistaa ilmeisesti myös jotain pistorasioita? Mahdollisesti tässä on laitettu kytkimellä kodin neljä eri turvalaitetta pois päältä (Huomaamme, että klikaanklikuit on painettu command --> off, joten Proove-security ja Nexa-security menee tilaan off state --> off). (Home-Assistant 2026; klikaanklikuit 2026; prooveglobal 2026) 

## d) Too complex 16? Olet nauhoittanut näytteen 'urh' -ohjelmalla .complex16s-muodossa. Muunna näyte rtl_433-yhteensopivaan muotoon ja analysoi se.

Hyödynsin tässä tehtävässä teron ohjeita sekä Nurmisen githubia. Latasin tiedoston Teron nettisivuilta, ja muunsin tämän jälkeen komentoa `mv Recorded-HackRF-20250411_183354-433_92MHz-2MSps-2MHz.complex16s foo_433.92M_2000k.cs8`, jotta sain tiedoston nimen muuttumaan (complex16 --> cs8). Teron ohjeistuksessa oli, että radiotaajuus pitää olla oikea sekä näytteenotto taajuus myös, erottimena toimii alaviiva.


<img width="723" height="39" alt="kuva" src="https://github.com/user-attachments/assets/0d22a48e-07b7-4612-94f1-7b7923317577" />

Lopputuloksena sain näytteen auki muutettuaan urh version rtl_443 yhteensopivaan muotoon.

<img width="717" height="345" alt="kuva" src="https://github.com/user-attachments/assets/7836d228-4030-494f-82fc-5c8fef587ee4" />

Tiedosto näyttää samalta kuin edellisen tehtävän näyte, joten analysointi löytyy edellisestä kohdasta c. (Nurminen 2025 ;Karvinen 2026)

## e) Asenna URH

Tein tämän myös tunnin aikana, ja käytin tässä Teron ohjeita tämän tehtävänannon vinkeistä. Aloitin tehtävän asentemalla ensimmäiseksi Pipx, joka on paketinhallintaohjelma myöskin, mutta se toimii Python pohjaisissa ohjelmistoissa käyttäen erillistä ympäristöä. (Pipx 2026)
```markdown 
sudo apt-get -y install pipx
```
Seurvaaksi asensin Pipx pakentinhallintaohjelmalla Urh ohjelman komennolla
```markdown 
pipx install urh
```
Muistaakseni tässä tuli virheilmoitus, että path pitää vielä päivittää, joten päivitin sen vielä samalla.
```markdown 
pipx ensurepath
```
Lopuksi tuli ilmoitus että päivitys on onnistunut, ja käynnistämällä uudelleen terminaalin sekä ajamalla komennon `urh` saadaan ohjelma käyntiin.

<img width="941" height="646" alt="kuva" src="https://github.com/user-attachments/assets/6ed4dc84-4e89-4c49-9809-c8bb39f58a79" />

## f)  1-on-on-on-HackRF-20250412_113805-433_912MHz-2MSps-2MHz.complex16s näytteen analysointi urh:lla: kuinka pitkä, millä taajuudella, milloin nauhoitettu ja miltä näyttää silmämääräisesti

Avasin tämän näytteen urh:lla file --> open --> ja sitten tämä kyseinen tiedosto, jonka latasin uudelleen komennolla

```markdown 
wget https://terokarvinen.com/verkkoon-tunkeutuminen-ja-tiedustelu/samples/1-on-on-on-HackRF-20250412_113805-433_912MHz-2MSps-2MHz.complex16s
```

Ja sitten päästiin analysoimaan tätä näytettä.

Näytteen pituuden sain selville, kun painoin `info` painiketta

<img width="949" height="501" alt="kuva" src="https://github.com/user-attachments/assets/3b3b894c-effc-41e3-a43b-0c3410392df9" />


- Pituus: 5,49 sekuntia
- Nauhoitettu: 4.12.2025 11:38:05 **tässä huomioin milloin näyte on luotu ei se milloin minä olen ladannut tiedoston**
- Taajuus: 2Mhz **Päättelin tämän Teron vinkeistä tehtävän aiemassa osiossa, jossa piti muuttaa tiedosto rtl_433 yhteensopivaan muotoon, ja vinkki oli tämä "Tiedoston nimessä pitää olla oikea taajuus (center frequency) ja näytteenottotaajuus (sample rate)"**

Näytteessä näkyy selkeästi, että kaukosäätimen valon on-nappia on painettu kolmesti, ja olettaen edellisiin tehtäviin, tämä on lähettänyt tiedon muille protokollille painahduksen yhteydessä. 









# Lähteet
- Home Assistant 2026. KlikAanKlikUit. Luettavissa: https://www.home-assistant.io/integrations/klik_aan_klik_uit/. Luettu: 3.11.2026.
- Hubmartin 18.1.2019. Universal Radio Hacker SDR Tutorial on 433 MHz radio plugs. Hubmartin. Katsottavissa: https://www.youtube.com/watch?v=sbqMqb6FVMY&t=199s. Katsottu: 3.11.2026.
- Karvinen 2026. h3 Aaltoja harjaamassa. Luettavissa: https://terokarvinen.com/verkkoon-tunkeutuminen-ja-tiedustelu/. Luettu: 3.11.2026.
- klikaanklikuit 2026. You have a smart house right in your fingers. Luettavissa: https://klikaanklikuit.nl/over-klikaanklikuit/. Luettu: 3.11.2026.
- Kornelius 2022. Decode 433.92 MHz weather station data. Luettavissa: https://www.onetransistor.eu/2022/01/decode-433mhz-ask-signal.html. Luettu: 3.11.2026.
- Nurminen 2025. h3 aaltoja harjaamassa: Luettavissa: https://github.com/nurminenkasper/Verkkoon-tunkeutuminen-ja-tiedustelu/blob/main/h3/h3-Aaltoja-harjaamassa.md. Luettu: 3.11.2026.
- prooveglobal 2026. For home and office vällehti. Luettavissa: https://prooveglobal.com/. Luettu: 3.11.2026.
- Pipx 2026. Pipx. Luettavissa: https://pipx.pypa.io/stable/. Luettu: 4.11.2026.


