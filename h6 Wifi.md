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

## Lähteet

- Airodump s.a. Airodump-ng. Luettavissa: https://www.aircrack-ng.org/doku.php?id=airodump-ng. Luettu: 24.11.2026.
- Iso-Anttila, L. s.a. Verkkoon tunkeutuminen ja tiedustelu -opintojakson esitysmateriaali Moodlessa. Haaga-Helia ammattikorkeakoulu. Luettu: 24.11.2026.




