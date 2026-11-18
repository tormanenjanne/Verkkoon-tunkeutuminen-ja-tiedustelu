
## a) Aja tunnilla esitetty ARP hyökkäys ja tutki, miten se toimii.

Mininetissä selvitin aluksi nodejen mac-osoitteet Larin ohjeistuksien mukaisesti.

<img width="550" height="49" alt="kuva" src="https://github.com/user-attachments/assets/2331e877-2779-4bf9-bb80-94d5f6de5de4" />

Kuvassa nähään h2 ja h3 koneiden mac-osoitteet. Kun sain tehtyä arp-hyökkyäksen huomasin, että h1 luuli h2 ip-osoite kuuluu myös h3-koneelle, joten tässä saadaan yhteys myös h3-koneelle.

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


Seuraavaksi ajoin tiedoston spoof_icmp.py ja pyrin lähettämään h3 koneelta pingausta h1 koneelle siten, että h1 kone luulee, että pingaus tulee h2 koneelta.

<img width="743" height="222" alt="kuva" src="https://github.com/user-attachments/assets/52f8d3c0-afb4-4f97-954a-9b8ce9084fff" />

Rehellisesti tehtävä oli haastava, koska en saanut xtermiä toimimaan, ja jouduin hieman soveltamaa tehtävää tekoälyn avustuksella, jotta sain pingaukset sekä tiedostot toimimaan.






