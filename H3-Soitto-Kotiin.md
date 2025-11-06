# H3 Soitto Kotiin | Nathaniel Ssendagire 6.11.2025

## Ympäristö

OS: Windows 11

Browser: Firefox 128.3.1esr (64-bit)

RAM: 16GB 

Processor: AMD Ryzen 7 5700X - 6 cores used

GPU: AMD Radeon RX 9060 XT 16GB

Disk: 65 GB

Network: NAT

## a) Hello Vagrant! 

Latasin vagrantin tältä sivulta: https://developer.hashicorp.com/vagrant/install, latauksessa ei ilmennyt mitään ongelmia.

<img width="354" height="68" alt="vagrant version" src="https://github.com/user-attachments/assets/0ffffb38-66c9-4692-89f8-563d5ff8b56f" />

## b) Linux Vagrant

<img width="600" height="327" alt="new vagrant ls" src="https://github.com/user-attachments/assets/59288e51-f601-45c0-bb45-09ac528f9797" />

Loin ensin hakemiston nimeltä vagrant-salt-lab, johon asensin kaikki tarvittavat Vagrant-paketit.

Tämän jälkeen suoritin komennon vagrant init luodakseni Vagrantfile-tiedoston, jota muokattiin seuraavasti:

<img width="685" height="553" alt="vagrant debian config file" src="https://github.com/user-attachments/assets/4bfc6891-0530-4d72-8041-07224a0b754e" />

<img width="1357" height="987" alt="results of running vagrant run command" src="https://github.com/user-attachments/assets/3839e7bc-1979-4a5d-b8cf-35b14d0b8701" />

<img width="773" height="164" alt="connecting to salt-master" src="https://github.com/user-attachments/assets/2af36974-7f89-473d-9164-dec4897fa793" />

<img width="777" height="168" alt="connecting to salt minion" src="https://github.com/user-attachments/assets/bbe414ac-53b4-4156-b150-2ae1ecda0a17" />


Kun asetukset oli tehty, käynnistin virtuaalikoneet komennolla vagrant up. Koneiden käynnistyttyä muodostin SSH-yhteyden sekä master- että minion-koneeseen.



## c) Kaksin kaunihimpi. Tee kahden Linux-tietokoneen verkko Vagrantilla. Osoita, että koneet voivat pingata toisiaan.

<img width="1979" height="509" alt="pinging each other" src="https://github.com/user-attachments/assets/cdbba7ba-ef89-4639-a1f5-4ead9dda1d10" />


## d) Herra-orja verkossa. 
<img width="533" height="428" alt="salt master installation" src="https://github.com/user-attachments/assets/97365c5c-5b93-4669-a532-34ff4a033aee" />

<img width="484" height="82" alt="salt minion installation" src="https://github.com/user-attachments/assets/146bd6d7-247b-4b89-a60e-d7d98e3fc07a" />


Seuraavaksi asensin salt-master-paketin master-koneelle ja salt-minion-paketin minion-koneelle, käytin apuna Teron laatimaa ohjetta saltin lataamiseen: https://terokarvinen.com/install-salt-on-debian-13-trixie/. Minionin asetustiedostoon lisättiin masterin IP-osoite, minkä jälkeen palvelut käynnistettiin uudelleen. Tunnilla esiintyi aiemmasta tutuksi tullut bugi, jossa restart-komento ei toiminut, joten jouduimme sammuttamaan ja käynnistämään koneen manuaalisesti.

Kun yhteys toimi, hyväksyimme minionin avaimen master-koneella, minkä jälkeen yhteys saatiin muodostettua onnistuneesti. Testasimme tätä komennolla sudo salt '*' test.ping, joka palautti arvon True, mikä vahvisti, että koneet pystyivät kommunikoimaan keskenään.
