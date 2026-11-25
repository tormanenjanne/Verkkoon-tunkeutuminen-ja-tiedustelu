# h6 Wifi

## a) Tutustu wifi challenge lab 2.1 harjoitus ympäristöön ja käytä tarvittaessa hyväksesi jo olemassa olevia ohjeita.

### 01. What is the channel that the wifi-global Access Point is currently using

Tehtävän aloitin selvittämällä komennolla `iwconfig`, mitä eri verkkoja on saatavilla.
<img width="986" height="730" alt="kuva" src="https://github.com/user-attachments/assets/c3b02416-959c-4ed2-b1c3-248c8e4cfda1" />

Tästä jatkoin Larin luentomateriaalia noudattamalla, eli käytin komentoa alhaalla olevaa komentoa, joka laittaa wlan monitoroinnin päälle. 

```markdown
sudo airmon-ng start wlan0
```

Seuraavaksi Larin ohjeistuksien mukaan komentoa `sudo airodump-ng wlan0mon --manufacturer `, mutta en löytänyt listasta wifi-globaalia, koska tämä näyttää vain valmistajat. Lähdin googlettamaan airodumpin erilaisia komentoja, ja löysin komennon, joka näyttää kaikki taajuusalueet. Käytin loppupeleissä komentoa `sudo airodump-ng wlan0mon --band abg`. -- band abg näyttää kaikki taajuusalueet. Loppujen lopuksi löysin oikea wifi-globaalin ja sen kanavanumero oli 44. (Airodump s.a;Iso-Anttila s.a)

<img width="1007" height="495" alt="kuva" src="https://github.com/user-attachments/assets/36784df7-f367-4765-ac1a-271b82c6284f" />

### 02. What is the MAC of the wifi-IT client?

Tätä lähdin selvittämään komennolla `sudo airodump-ng wlan0mon --band abg`, ja löysin kohdasta **essid** laitteen **wifi-IT**

<img width="1005" height="477" alt="kuva" src="https://github.com/user-attachments/assets/de3d0471-3df4-4a5f-8fc9-55f642a9f4ff" />

Seuraavaksi katsoin kyseisen laitteen kanavaa, mitä käyttäjiä sieltä voisi löytyä. Käytin tässä komentoa `sudo airodump-ng wlan1mon -w scan  --manufacturer --band abg -c 11
`

Kuten huomaamme bssid kertoo ap eli access pointin mac-osoitteen, ja kohdassa **Station** näytetään käyttäjän mac-osoitetta. (Airodump-ng s.a)

<img width="855" height="437" alt="kuva" src="https://github.com/user-attachments/assets/34b124d6-7199-46bf-a094-855c14756ddc" />

### 07. Get wifi-old password

Tässä tehtävässä hyödynsin walkthroughia, joten alotin tehtävän käynnistämällä wlan monitorin päälle `sudo airmon-ng start wlan0`, ja tämän jälkeen katsoin, mikä mac-osoite kuuluu tälle kyseiselle wlanille `sudo airodump-ng wlan1mon -w scan --manufacturer`. 

<img width="932" height="358" alt="kuva" src="https://github.com/user-attachments/assets/1b7fcfc0-c23e-4a19-b53e-befc77be88b8" />

Kun löysin wifi-old mac-osoitteen, seuraavaksi käytin automaattista ohjelmaa, joka etsii salasanan suoraan tälle. Tässä käytin komentoa `airmon-ng check kill` ja `besside-ng -c 1 -b F0:9F:C2:AA:19:29 wlan2 -v`

- check kill: Komento keskyttää kaikki prosessit, jotka saattavat häiritä aircrack-ng:tä
- beside-ng: Murtaa automaattisesti kaikki WEP-verkot, ja pyrkii saamaan hyödyllisiä tietoja muun muassa salasanoja. `-c` kuuntelee kanavaa 1 `-b` kohdistaan kohteen mac-osoitteelle `-v` verbose tila, joka näyttää mahdollisimman paljon tietoja.(aircrack-ng)

Ajettua besside-ng:n, se löysi lopulta kohteen salasanan.

<img width="939" height="106" alt="kuva" src="https://github.com/user-attachments/assets/d28d36bc-fd09-488b-a3f4-79f81bbe5aaa" />

Lähdin luomaan configuraatio tiedostoa komennolla `nano wep.conf` ja lisäsin sinne nämä tiedot:

```markdown
network={
  ssid="wifi-old"
  key_mgmt=NONE
  wep_key0=11BB33CD55
  wep_tx_keyidx=0
}
```

Lopuksi yhdistin wwp-verkkoon configuraatio tiedostolla `wpa_supplicant -D nl80211 -i wlan2 -c wep.conf`, ja avasin toisen terminaalin, josta saisin DHCP-palvelimelta ip-osoitteen komennolla `dhclient wlan2 -v`. Ip-osoite löytyi, ja se oli `192.168.1.1`.

<img width="725" height="282" alt="kuva" src="https://github.com/user-attachments/assets/b377dd71-639c-4c0f-bf10-7cad177ea49c" />

Kirjoittamalla selaimeen kyseisen ip-osoitteen, löysin täältä flagin.

<img width="923" height="781" alt="kuva" src="https://github.com/user-attachments/assets/a80e4625-7e3f-4d19-b4cf-a65c75da6a28" />

Nämä vihreällä olevat tehtävät sain ratkaistua.

<img width="770" height="785" alt="kuva" src="https://github.com/user-attachments/assets/eed60f36-afdb-4f0f-869e-d552e2ac04ec" />




## b) Kirjoita raportti siitä mitä opit ja mitkä asia yllättivät sinut kun tutustuit harjoitukseen.

Harjoituksien aikana opin tunnistamaan: mitä kanavaa jotkut laitteet käyttävät sekä miten voi saada asiakkaan mac-osoitteen selville. Myös senkin, miten voi saada salasanat selville Wiresharkin avulla, ja kuinka voidaan manipuolida mac-osoitteita, jotta ne kuuluisi oikeastaan minulle, ja saisin selville arkaluontoista tietoa muun muassa salansanoja. Harjoitukissa yllätti se kuinka heikko salaus WEP ja OPN oikeastaan on, ja miten helposti näihin voidaan murtautua. Toisaalta Lari mainitsikin tunnilla näiden olevan juridisista syistä, jotta voidaan syyttää hyökkääjä tehneessä rikoksen.

## c) Miten suhtautumisesi WLanin turvallisuuteen muuttui sen jälkeen kun teit harjoitukset?

Suhtaudun jatkossa hieman kriittisemmin Wlaniin. Tunnilla kuulta näistä salauksita voidaan todeta, että nämä on yllättävän helposti purettavissa, ja saadaan selville arkaluontoisia tietoja. En ole siis ihan varma käytetäänkö näitä heikkoja salausmenetelmiä enään, mutta jatkossa en aio käyttää ilmaisia julkisia Wlaneja.





## Lähteet

- Airodump s.a. Airodump-ng. Luettavissa: https://www.aircrack-ng.org/doku.php?id=airodump-ng. Luettu: 24.11.2026.
- aircrack-ng. Besside-ng:n .Luettavissa: https://www.aircrack-ng.org/doku.php?id=besside-ng. Luettu: 25.11.2026.
- Iso-Anttila, L. s.a. Verkkoon tunkeutuminen ja tiedustelu -opintojakson esitysmateriaali Moodlessa. Haaga-Helia ammattikorkeakoulu. Luettu: 24.11.2026.
- Wifi-hacking s.a. Wifi - Challenge Labs - Complete Walkthrough . Luettavissa: https://wifi-hacking.cavementech.com/wifi-challenge-labs/wifi-challenge-labs-complete-walkthrough. Luettu: 25.11.2026.




