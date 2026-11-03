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

## Rtl_433 asennus, ja testaus toimivuudesta

Tämän työkalun asentamisen suoritin tunnin aikana, mutta käydään tämä vielä läpi. Ensimmäiseksi käytin komentoa` sudo apt-get -y install atool wget libssl-dev libtool libusb-1.0-0-dev librtlsdr-dev rtl-sdr libsoapysdr-dev`, jolla saatiin asennettua erilaisia työkaluja sekä kirjastoja. Seuraavaksi käytin komentoa `wget https://github.com/merbanan/rtl_433/releases/download/25.02/rtl_433-soapysdr-openssl3-Linux-amd64-25.02.zip`, jolla lataamme Githubista juuri tämän version, ja lopuksi purin paketin komennolla ` aunpack rtl*.zip`.

Lopuksi testasin toimivuutta komennolla `./rtl_433' `, joka ilmoitti työkalun toimivuudesta.

<img width="721" height="75" alt="kuva" src="https://github.com/user-attachments/assets/250e1913-22c6-42f5-ad48-6e8ee6305e6a" />


# Lähteet

- Hubmartin 18.1.2019. Universal Radio Hacker SDR Tutorial on 433 MHz radio plugs. Hubmartin. Katsottavissa: https://www.youtube.com/watch?v=sbqMqb6FVMY&t=199s. Katsottu: 3.11.2026.
- Kornelius 2022. Decode 433.92 MHz weather station data. Luettavissa: https://www.onetransistor.eu/2022/01/decode-433mhz-ask-signal.html. Luettu: 3.11.2026.


