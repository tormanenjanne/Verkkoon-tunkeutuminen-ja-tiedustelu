# h6 Wifi

## a) Tutustu wifi challenge lab 2.1 harjoitus ympäristöön ja käytä tarvittaessa hyväksesi jo olemassa olevia ohjeita.

### 01. What is the channel that the wifi-global Access Point is currently using

Tehtävän aloitin selvittämällä komennolla `iwconfig`, mitä eri verkkoja on saatavilla.
<img width="986" height="730" alt="kuva" src="https://github.com/user-attachments/assets/c3b02416-959c-4ed2-b1c3-248c8e4cfda1" />

Tästä jatkoin Larin luentomateriaalia noudattamalla, eli käytin komentoa alhaalla olevaa komentoa, joka laittaa wlan monitoroinnin päälle. 

```markdown
sudo airmon-ng start wlan0
```

Seuraavaksi Larin ohjeistuksien mukaan komentoa `sudo airodump-ng wlan0mon --manufacturer `, mutta en löytänyt listasta wifi-globaalia. Lähdin googlettamaan airodumpin erilaisia komentoja, ja löysin komennon, joka näyttää kaikki taajuusalueet. Käytin loppupeleissä komentoa `sudo airodump-ng wlan0mon --band abg`.



