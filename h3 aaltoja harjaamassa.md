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



- Näytteitä on ainakin yhteensä 12 kappaletta.
- Time: Näyttää milloin signaaliin ollaan havaittu.
- Model: KlikAanKlikUit-Switch, nexa security ja klikaanklikuit-Switch (nämä ovat eri laitteita, joihin ollaan saatu yhteys)
- Channel: kanava 3, jota ollaan käytetty
- id: Prove security ja klikaanklikuit-Switch on sama id-numero. **Prove-securityllä on sama id, mutta edessä on housecode id:n sijaan**
- State: näyttää off.
- Group call: 0, ei lähetä muille laitteille tietoa tästä.

Selvitin ensimmäiseksi Googlesta mitä nämä yritykset ovat, ja mitä ne tekevät.( Yritykset: Proove-security, klikaanklikuit ja Nexa-scurity). klikaanklikuit on yritys, joka tekee erilaisia älylaitteita muun muassa ip-kameroita ja kytkimiä, joilla voidaan valvoa esimerkiksi omaa kotia (esimerkissä on house code: 8785315). Proove-security valmistaa myös näitä ip-kameroita, ja monia muita erilaisia laitteita viimeiseksi Nexa-Security valmistaa ilmeisesti myös jotain pistorasioita? Mahdollisesti tässä on laitettu kytkimellä kodin neljä eri turvalaitetta pois päältä (Huomaamme, että klikaanklikuit on painettu command --> off, joten Proove-security ja Nexa-security menee tilaan off state --> off). (Home-Assistant 2026; klikaanklikuit 2026; prooveglobal 2026) 



# Lähteet
- Home Assistant 2026. KlikAanKlikUit. Luettavissa: https://www.home-assistant.io/integrations/klik_aan_klik_uit/. Luettu: 3.11.2026.
- Hubmartin 18.1.2019. Universal Radio Hacker SDR Tutorial on 433 MHz radio plugs. Hubmartin. Katsottavissa: https://www.youtube.com/watch?v=sbqMqb6FVMY&t=199s. Katsottu: 3.11.2026.
- Karvinen 2026. h3 Aaltoja harjaamassa. Luettavissa: https://terokarvinen.com/verkkoon-tunkeutuminen-ja-tiedustelu/. Luettu: 3.11.2026.
- klikaanklikuit 2026. You have a smart house right in your fingers. Luettavissa: https://klikaanklikuit.nl/over-klikaanklikuit/. Luettu: 3.11.2026.
- Kornelius 2022. Decode 433.92 MHz weather station data. Luettavissa: https://www.onetransistor.eu/2022/01/decode-433mhz-ask-signal.html. Luettu: 3.11.2026.
- prooveglobal 2026. For home and office vällehti. Luettavissa: https://prooveglobal.com/. Luettu: 3.11.2026. 


