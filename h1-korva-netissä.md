# h1-korva-netissä
Tässä tehtävässä tehdään muutamia tehtäviä liittyen spektriin, radiotaajuuksiin sekä tarkastellaan tehtävien tuloksia sekä analysoidaan niitä lähteiden tukemana. Tehtäviä on yhteensä viisi kappaletta.

## Spektri: Piirrä oma sähkömagneettinen spektri. Eli jana, jossa taajuus kasvaa. Ja 3-10 itseäsi kiinnostavaa sovellusta.

<img width="1111" height="621" alt="kuva" src="https://github.com/user-attachments/assets/0992d7df-fa6c-4218-bd19-254ccb9e2c5d" />




**Kuva 1**. Tässä on piirrettynä spektrini, sekä muutamia sovelluksia. Huomaamme, että aallonpituus kasvaa oikealta vasemmalle päin sekä antennin koko. Läpäisevyys sekä kyky siirtää tietoa taas vasemmalta oikealle. (Mukaillen Nasa, 2026)




Kuten näemme kuvassa: Aallonpituus kasvaa aina oikealta vasemmalle, ja näiden välinen pituus on harjanteiden välinen ero. Lyhyimmät aallonpituudet voivat olla atomin kokoisia, kun taas suurimmat voivat olla jopa suurempia kuin planeetamme halkaisija. (Nasa 2023)

## WebSDR. Etäkäytä WebSDR-ohjelmaradiota, joka on kaukana sinusta ja kuuntele radioliikennettä
Tarkoituksena on siepata radioliikennettä siten, että se on vähintään 400 km paikasta, mistä teen tätä tehtävää. Käytän tässä tehtävässä esimerkkinä toisen maan radiolähetystä, joka on amatöörien pitämä.

<img width="1755" height="193" alt="kuva" src="https://github.com/user-attachments/assets/f1ffa301-b6fb-47f9-8e5f-857115c4f8c3" />

**Kuva 2**. Valitsin Yhdysvallat, Corinnen kaupungissa olevan radiotaajuuden, joka on sijaitsee Utahin osavaltiossa.

<img width="1448" height="482" alt="kuva" src="https://github.com/user-attachments/assets/5fe42792-80df-4612-9a5b-57b78b6fcc14" />

**Kuva 3**. Taajuuden, jolla sain yhteyden radiokanavaan oli **1658 kHz**,modulaationa oli AM sekä aallonpituus oli **AM-160-120M**. Kuvassa kyseiset kohdat ollaan huomioitu punaisilla laatikoilla, joista löytyivät tiedot. Tehtävässä sain äänen kuulumaan laittamalla **Firefox/Mozilla audio start** päälle, sekä tämän jälkeen säätämällä taajuuksia sekä vaihtamalla modulaation **AM**, jotta sain äänen kuulumaan.

###  Moduwhat? Kuuntele kanavaa, joka käyttää eri modulaatiota (AM, FM...) kuin edellisessä kohdassa käyttämäsi kanava.

Vaihdoin modulaatioksi LSB (Lower Sideband), joka toimii 40, 80 ja 120M kaistoilla. (Mdarc 2026) Edelliseen lähteeseen myös viitaten, tämä on yksi suositummista amatööriradiotaajuuksista. Taajuus oli 7162.000 Khz, ja kanavasta kuului linnun ääntä.
<img width="1346" height="403" alt="kuva" src="https://github.com/user-attachments/assets/858b1fb5-b502-4cc0-84de-3aa4e46f51d7" />

Kuvassa huomataan, että taajuus on vaihdettu sekä modulaation AM -> LSB.


Kun muutin taajuuden takaisin **1658Khz**, ja vaihdoin modulaation FM, taajuudesta ei kuulunut enää muuta kuin suhinaa. Tämä ilmeisesti johtuu siitä, että FM-taajudet ovat megahertsejä (MHz), kun taas AM-taajudet ovat kilohertsejä (kHz). (Diffen 2026)

##  ADS-B. Etsi jokin sinua kiinnnostava lentokone ADS-B Exchange -palvelusta. Kuvaile konetta ja sen lentoa. Selitä, miten tiedot on saatu.


Valitsin Naton lentokoneen, joka on rekisteröity Luxemburgiin ja tämä on sotilaskone. Lentokoneen malli on   BOEING E-3 Sentry (TF33). Kone on lähtenyt liikkeelle Saksasta Naton ilmatukikohdasta, ja on matkalla itä-eurooppaan päin.

ADS-B on vastaanotinverkko, joka tarjoaa maailmanlaajuisen sekä reaaliaikaisen näkyvyyden lentokonetoiminnasta. Tämän tarkoituksena on tarjota läpinäkyvää lentoliikennettä kaikille. ADS-B hyödyntää radiosignaaleja lentokoneiden seuraamiseen. (ADS.B Exchange 2026;Federal Aviation Administration 2026)

-ADS-B Out: Lähettää tietoja lentokoneen sijainnista, nopeudesta, maannopeudesta ja niin edelleen noin kerran sekunnissa. Lennonjohto voi saada tämän avulla tiedot välittömästi. (Federal Aviation Administration 2026)







## Lähteet

ADS-B Exchange 2026. Global Flight Tracking. Built on Accuracy. Luettavissa: https://www.adsbexchange.com/. Luettu: 21.10.2026.

Diffen 2026. AM vs. FM. Luettavissa: https://www.diffen.com/difference/AM_vs_FM. Luettu: 21.10.2026

Federal Aviation Administration 2026. Ins and Outs. Luettavissa: https://www.faa.gov/air_traffic/technology/equipadsb/capabilities/ins_outs. Luettu: 21.10.2026.

Mdarc 2026. LSB or USB? Luettavissa: https://www.mdarc.org/operating-aids/lsb-or-usb. Luettu: 21.10.2026.

Nasa 2023. Anatomy of an Electromagnetic Wave. Luettavissa: https://science.nasa.gov/ems/02_anatomy/. Luettu: 21.10.2026.

Nasa 2026. The Electromagnetic Spectrum. Luettavissa: https://www.earthdata.nasa.gov/learn/earth-observation-data-basics/electromagnetic-spectrum. Luettu: 21.10.2026.

