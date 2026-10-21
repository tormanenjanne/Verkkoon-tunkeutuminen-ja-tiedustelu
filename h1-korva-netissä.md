# h1-korva-netissä
Tässä tehtävässä tehdään muutamia tehtäviä liittyen spektriin, radiotaajuuteen sekä tarkastellaan tehtävien tuloksia sekä analysoidaan niitä lähteiden tukemana. Tehtäviä on yhteensä viisi kappaletta.

## Spektri: Piirrä oma sähkömagneettinen spektri. Eli jana, jossa taajuus kasvaa. Ja 3-10 itseäsi kiinnostavaa sovellusta.

<img width="1159" height="610" alt="kuva" src="https://github.com/user-attachments/assets/b1a9c709-6f72-43b0-b7ba-bb42c72d5ce4" />


**Kuva 1**. Tässä on piirrettynä spektrini, sekä kolme eri kiinnostavaa sovellusta. Huomaamme, että aallonpituus kasvaa oikelta vasemmalle päin sekä antennin koko. Läpäisevyys sekä kyky siirtää tietoa taas vasemmalta oikealle. (Mukaillen Nasa, 2026)




Kuten näemme kuvassa: Aallonpituus kasvaa aina oikealta vasemmalle, ja näiden välinen pituus on harjanteiden välinen ero. Lyhyimmät aallonpituudet voivat olla atomin kokoisia, kun taas suurimmat voivat olla jopa suurempia kuin planeetamme halkaisija. (Nasa 2023)

## WebSDR. Etäkäytä WebSDR-ohjelmaradiota, joka on kaukana sinusta ja kuuntele radioliikennettä
Tarkoituksena on siepata radioliikennettä siten, että se on vähintään 400km paikasta, mistä teen tätä tehtävää. Käytän tässä tehtävässä esimerkkinä toisen maan julkista radiolähetystä, eli yleisradiolähetystä.

<img width="1755" height="193" alt="kuva" src="https://github.com/user-attachments/assets/f1ffa301-b6fb-47f9-8e5f-857115c4f8c3" />

**Kuva 2**. Valitsin Yhdysvallat, Corine kaupungin olevan radiotaajuuden, joka on sijaitsee Utahin-osavaltiossa.

<img width="1448" height="482" alt="kuva" src="https://github.com/user-attachments/assets/5fe42792-80df-4612-9a5b-57b78b6fcc14" />

**Kuva 3**. Taajuuden, jolla sain yhteyden radiokanavaan oli **1658Khz**,modulaationa oli AM sekä aallonpituus oli **AM-160-120M**. Kuvassa kyseiset kohdat ollaan huomioitu punaisilla laatikoilla, joista löyttyi tiedot. Tehtävässä sain äänen kuulumaan laittamalla **Firefex/Mozilla audio start** päälle, sekä tämän jälkeen säätämällä taajuuksia sekä vaihtamalla modulaation **AM**, jotta sain äänen kuulumaan.

###  Moduwhat? Kuuntele kanavaa, joka käyttää eri modulaatiota (AM, FM...) kuin edellisessä kohdassa käyttämäsi kanava.

Vaihdoin modulaatioksi LSB (Lower Sideband), joka toimii 40, 80 ja 120M kaistoilla. (Mdarc 2026) Edelliseen lähteeseen myös viitataten, tämä on yksi suositummista amatööriradiotaajuuksista.

Kun muutin taajuden takaisin 1658Khz, ja vainhdoin modutaaliton FM, taajuudesta ei kuulunut enään muutakuin suhinaa. Tämä ilmeisesti johtuu siitä, että FM-taajudet ovat megahertsejä (Mhz), kun taas AM-taajudet ovat kilohertzejä (Khz). (Diffen 2026)

##  ADS-B. Etsi jokin sinua kiinnnostava lentokone ADS-B Exchange -palvelusta. Kuvaile konetta ja sen lentoa. Selitä, miten tiedot on saatu.


Valitsin Naton lentokoneen, joka on rekisteröity Luxemburgiin ja tämä on sotilaskone. Lentokoneen malli on   BOEING E-3 Sentry (TF33). Kone on lähtenyt liikkeelle Saksasta Nato:n ilmatukikohdasta, ja on matkalla itä-eurooppaan päin.

ADS-B on vastaanotinverkko, joka tarjoaa maailmanlaajuisen sekä reealiaikaisen näkyvyyden lentokonetoiminnasta. Tämän tarkoituksena on tarjota läpäinäkyvää lentoliikennettä kaikille. ADS-B hyödyntää radiosignaaleja lentokoneiden seuraamiseen. (ADS.B Exchange 2026;Federal Aviation Administration 2026)

-ADS-B Out: Lähettää tietoja lentokoneen sijainnista, nopeudesta, maannopeudesta ja niin edelleen noin kerran sekunnissa. Lennonjohto voivat saada tämän avulla tiedot välittömästi. (Federal Aviation Administration 2026)







## Lähteet

ADS-B Exchange 2026. Global Flight Tracking. Built on Accuracy. Luettavissa: https://www.adsbexchange.com/. Luettu: 21.10.2026.

Diffen 2026. AM vs. FM. Luettavissa: https://www.diffen.com/difference/AM_vs_FM. Luettu: 21.10.2026

Federal Aviation Administration 2026. Ins and Outs. Luettavissa: https://www.faa.gov/air_traffic/technology/equipadsb/capabilities/ins_outs. Luettu: 21.10.2026.

Mdarc 2026. LSB or USB? Luettavissa: https://www.mdarc.org/operating-aids/lsb-or-usb. Luettu: 21.10.2026.

Nasa 2023. Anatomy of an Electromagnetic Wave. Luettavissa: https://science.nasa.gov/ems/02_anatomy/. Luettu: 21.10.2026.

Nasa 2026. The Electromagnetic Spectrum. Luettavissa: https://www.earthdata.nasa.gov/learn/earth-observation-data-basics/electromagnetic-spectrum. Luettu: 21.10.2026.

