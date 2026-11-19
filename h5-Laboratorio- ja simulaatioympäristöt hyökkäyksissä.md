
## a) Aja tunnilla esitetty ARP hyökkäys ja tutki, miten se toimii.

Mininetissä selvitin aluksi nodejen mac-osoitteet Larin ohjeistuksien mukaisesti.

<img width="550" height="49" alt="kuva" src="https://github.com/user-attachments/assets/2331e877-2779-4bf9-bb80-94d5f6de5de4" />

Kuvassa nähään h2 ja h3 koneiden mac-osoitteet. Kun sain tehtyä arp-hyökkyäksen huomasin, että h1 luuli h2 ip-osoiteen sekä mac-osoitteen vastaavan h2-konetta, mutta todellisuudessa tiedot meni arp-hyökkäyksen taki h3-koneelle, koska mac-osoite osoitteh3-koneelle.

<img width="569" height="34" alt="kuva" src="https://github.com/user-attachments/assets/36c5470e-a2af-42df-9b77-44ab4b7bb43e" />

Ssh-yhteys h2-koneelle ilmoitti mahdollisesta Man-in-the-middle hyökkäyksessä, johon olen joutunut. sekä avain olisi mahdollisesti muuttunut.

<img width="518" height="184" alt="kuva" src="https://github.com/user-attachments/assets/04ea88a4-3ec6-491a-ab6c-17731091c1d0" />

lokitiedoissa nähädää se, että h1 on lähetti h2 ssh-yhteyden, mutta se yhteys siirtyi h3 koneelle. Tämä siirtyi sen takia, koska teimme aikaisemmin arp-hyökkäksen. Tässä saataisiin muun muassa toisen salasana lokitiedoista, jonka hän on syöttänyt kirjautuessaan ssh:lla toiselle koneelle.

<img width="579" height="206" alt="kuva" src="https://github.com/user-attachments/assets/9f160c8c-c853-415c-a932-ba7d7d38f92c" />

## b) Samassa hakemistossa on myös ICMP Spoofing ja TCP Session Hijacking. Aja molemmat labrat läpi ja kerro, miten molemmat tekniikat toimivat.

### ICMP Spoofing

Hyödynsin tässä tehtävässä ssam246 githubia, ja hänen ohjeistuksiaan molempien tehtävien ajamiseen. polku oli tämä `cd /home/mininet/lab/01-Network-Security-Lab/scripts/`, ja harjoituksen sai ajamalla komennon:

```markdown
sudo python hub_topo.py
```

Testasin vielä `pingall` komennolla, jotta saan yhteyden kaikkiin laitteisiin.

<img width="738" height="339" alt="kuva" src="https://github.com/user-attachments/assets/8a4d96a8-cd51-450d-a8ab-a37facf19678" />

Käynnistin h1 koneella sniff_icmp-py, ja pingasin tämän jälkeen h2 -> h1 koneelle. Paketit tulivat normaalisti.

<img width="516" height="141" alt="kuva" src="https://github.com/user-attachments/assets/7936b236-e4cd-4191-92cb-ec0c16afaa0e" />


Seuraavaksi ajoin tiedoston spoof_icmp.py h3 koneella, ja pingasin h2 koneelta h1 koneelle. Skripti ilmeisesti kuunteli, ja muodosti väärennettyjä paketteja siten, että h3 kone olisi h1 kone. Tässä on kuva, jossa lokitiedoissa nähdään pingauksen menevän perille. En varmistanut tuliko pingaus todellisuudessa h1 koneelta vai h3.

<img width="743" height="222" alt="kuva" src="https://github.com/user-attachments/assets/52f8d3c0-afb4-4f97-954a-9b8ce9084fff" />

Rehellisesti tehtävä oli haastava, koska en saanut xtermiä toimimaan, ja jouduin hieman soveltamaa tehtävää tekoälyn avustuksella, jotta sain pingaukset sekä tiedostot toimimaan.

### TCP Hijack

Lähdin tekemään tehtävän pohjaa samanlailla kuin edellisessä tehtävässä, jotta saan testiympäristön auki

- Seuraavaksi käynnistin h1 koneelle tcp_server.py
- Sitten h2 koneelle käynnistin tcp_client.py
- h3 koneelle laitoin tcp pakettien päälle sniff_tcp_session.py

Tällä sniff_tcp_session komennolla pystyin katsomaan tcp liikennettä h1 ja h2 koneiden välillä. Tässä kuva, jossa näen koneiden liikenteen

<img width="448" height="334" alt="kuva" src="https://github.com/user-attachments/assets/bdd30044-b6d8-4c24-b030-9b640d4a3bb1" />

Seuraavaksi ajoin h3 koneella tcp_hijack.py, ja lähden tutkimaan onnistuiko hyökkäys. H1-konella ei näkynyt liikennettä, jossa olisi viesti "you are hacked". Eli siis en saanut hyökkäystä onnistumaan, vaikka pystyin kuunntelemaan h1- ja h2 koneiden välistä liikennettä.

<img width="612" height="306" alt="kuva" src="https://github.com/user-attachments/assets/79598f28-ce25-49b6-afae-2df8d906783a" />


Aikaisemmin huomasin, että pystyin h3-koneella tarkastelemaan h1- ja h2-koneiden välillä, koska minulla oli tcp_sniff_session.py tässä auki. Lokitiedoissa näkyi muun muassa lähde- sekä kohde osoitteet sekä seq act numerot.

- Seq: Viestin aloittaja ilmoittaa palvelimelle oman sekvenssinumeron, ja millä numerolla hän tulee aloittamaan tämän.
- act: On kuittaus tästä, ja lähettää oman sekvenssinumeron viestin lähettäjälle, ja luo luotettavan yhteyden (GeekforGeeks 2026) 

<img width="349" height="259" alt="kuva" src="https://github.com/user-attachments/assets/936ca605-22f1-4b2a-a558-fc5e7ce5f11c" />

Kokonaisuudessaan jos ymmärsin oikein, tämän hyökkäyksen tarkoituksena oli kuunnella h1 ja h2 koneiden välistä liikennettä, sekä tämän jälkeen saada selville mahdolliset seq ja act kuittaukset, jolla voitaisiin saada yhteys näiden välille. Lopuksi en saanut kuittausta siitä, sainko lähetettyä h3 koneelta tietoa h1 koneelle, koska lokitiedoissa ei valitettavasti näkynyt mitään tähän viittaavaa tietoa. (abnormal 2026)

## c) Hakemistossa 02-SDN-DDos_Simulation tryout-kansiossa on työkalut, jotta voit ajaa TCP SYN-Flood-hyökkäyksen turvallisesti.

Aloitin tehtävän käynnistämällä verkko-ohjaimen, ja tämän jälkeen menin 2-SDN-DDos_Simulation tryou kansioon, ja käytin komentoa `python simple_tree_top.py`.

<img width="767" height="435" alt="kuva" src="https://github.com/user-attachments/assets/dd3afaf4-352d-4f40-89f3-28c8cf7a2c51" />

Käytin hyökkäksen tekemiseen hping3 työkalua, jolla pystyttiin lähettämään paketteja esimerkiksi 1000 pakettia nopeasti, ja ruuhkauttamaan vastaanottava tietokone. Tallensin liikennettä tcpdumpilla. Ja lopuksi huomaamme, että paketteja tuli aivan valtava määrä, ja jouduin keskeyttämään ajon. (sciencedirect 2025; Miessler 2026)

<img width="614" height="418" alt="kuva" src="https://github.com/user-attachments/assets/01a9d8b8-91a0-43a9-8089-b5e4a20943da" />

Komentoja minulla ei juurikaan näy tässä, koska oli hieman tässäkin haasteita saada tämä toimimaan, enkä saanut niitä poimittua jälkeenpäin. Tässä tehtävässä on hyödynnetty lähteitä sekä osittain tekoälyä auttamaan haastavissa tilaneissa.


Hyökkäys toimi tässä siten, että kyselyitä lähetettiin aivan valtava määrä, ja saatiin ruuhkautettua toinen kone. Ilmeisesti kaikki paketit ovat jääneet tcp-handshakessa vain SYN viestin eli minun lähtettämät 1000 pakettia, sekä ack viestiä ei tullut kertaakaan, joten yhteys on ruuhkautunut tämän takia.




## Lähteet

- abnormal 2026. TCP Session Hijacking: How It Works and How to Detect It. Luettavissa: https://abnormal.ai/learning/tcp-session-hijacking. Luettu: 18.11.2026.
- Geekforgeek 2026. TCP 3-Way Handshake Process. Luettavissa: https://www.geeksforgeeks.org/computer-networks/tcp-3-way-handshake-process/. Luettu: 18.11.2026.
- Miessler, D. 2026. tcpdump Examples: A Tutorial with 150 Commands. Luettavissa: https://danielmiessler.com/blog/tcpdump. Luettu: 18.11.2026
- sciencedirect 2025. SDN TCP-SYN Dataset: A dataset for TCP-SYN flood DDoS attack detection in software-defined networks. :luettavissa: https://www.sciencedirect.com/science/article/pii/S2352340925000460. Luettu: 18.11.2026.






