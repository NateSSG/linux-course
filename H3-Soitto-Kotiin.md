# H3 Soitto Kotiin | Nathaniel Ssendagire 6.11.2025

## Ympäristö

OS: Windows 11

Browser: Firefox 128.3.1esr (64-bit)

RAM: 16GB 

Processor: AMD Ryzen 7 5700X - 6 cores used

GPU: AMD Radeon RX 9060 XT 16GB

Disk: 65 GB

Network: NAT

## Tiivistelmä

## Two Machine Virtual Network With Debian 11 Bullseye and Vagrant

Vagrant automatisoi VirtualBoxin virtuaalikoneiden luomisen ja SSH-yhteydet ilman graafista käyttöliittymää.

Vagrantfile määrittää kaksi konetta (t001 ja t002), joilla on omat IP-osoitteet (esim. 192.168.88.101 ja 192.168.88.102).

Molemmat koneet voivat kommunikoida toistensa ja internetin kanssa.

vagrant up käynnistää verkon ja vagrant ssh mahdollistaa kirjautumisen koneille.

Koneet voi helposti poistaa ja luoda uudelleen komennolla vagrant destroy ja vagrant up.

IP-virheissä Vagrantfileen määritetty verkko-osoitealue tulee tarkistaa ja korjata.

## Salt Quickstart – Salt Stack Master and Slave on Ubuntu Linux

Salt mahdollistaa satojen koneiden hallinnan yhdestä master-palvelimesta käsin.

Master asennetaan komennolla sudo apt-get install salt-master ja minion komennolla sudo apt-get install salt-minion.

Minionin asetustiedostossa määritetään masterin IP-osoite ja mahdollinen tunniste (id).

Yhteys muodostetaan hyväksymällä avain masterilla komennolla sudo salt-key -A.

Testaus onnistuu komennolla sudo salt '*' cmd.run 'whoami', joka osoittaa yhteyden toimivan.

Järjestelmällä voidaan myöhemmin hallita ohjelmistojen asennuksia, tiedostoja ja palveluita useilla koneilla yhtä aikaa.

## Salt Vagrant – Automatically Provision One Master and Two Slaves

Kolmen koneen verkko luodaan automaattisesti Vagrantilla (yksi master, kaksi minionia).

Vagrantfile asentaa ja konfiguroi Saltin automaattisesti kaikille koneille.

Master hyväksyy minionien avaimet komennolla sudo salt-key -A, ja yhteys testataan sudo salt '*' test.ping.

Komentoja voi ajaa kaikille minioneille esim. sudo salt '*' cmd.run 'hostname -I'.

Saltin idempotentit tilat varmistavat, että järjestelmä pysyy halutussa tilassa – muutoksia tehdään vain tarpeen mukaan.

Infra as Code: järjestelmän haluttu tila määritetään tekstitiedostoissa (esim. /srv/salt/hello/init.sls).

top.sls-tiedosto määrittää, mitkä tilat ajetaan millekin minionille.

Lopuksi koneet voi poistaa komennolla vagrant destroy, mikä hävittää kaiken sisällön.

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

<img width="1939" height="512" alt="ping from minion to master" src="https://github.com/user-attachments/assets/e4906b1c-142b-4e3c-a2bc-2bbba8864aba" />


## d) Herra-orja verkossa. 
<img width="533" height="428" alt="salt master installation" src="https://github.com/user-attachments/assets/97365c5c-5b93-4669-a532-34ff4a033aee" />

<img width="484" height="82" alt="salt minion installation" src="https://github.com/user-attachments/assets/146bd6d7-247b-4b89-a60e-d7d98e3fc07a" />



Seuraavaksi asensin salt-master-paketin master-koneelle ja salt-minion-paketin minion-koneelle, käytin apuna Teron laatimaa ohjetta saltin lataamiseen: https://terokarvinen.com/install-salt-on-debian-13-trixie/. 

Minionin asetustiedostoon lisättiin masterin IP-osoite, minkä jälkeen palvelut käynnistettiin uudelleen. Tunnilla esiintyi aiemmasta tutuksi tullut bugi, jossa restart-komento ei toiminut, joten jouduimme sammuttamaan ja käynnistämään koneen manuaalisesti.

<img width="466" height="198" alt="minion file config" src="https://github.com/user-attachments/assets/57170116-75b6-4b95-99ef-86071275d318" />

<img width="255" height="42" alt="master ip" src="https://github.com/user-attachments/assets/2a416abe-bfca-4bb8-8492-6fab46636e59" />

<img width="811" height="209" alt="shutting down salt minion" src="https://github.com/user-attachments/assets/783db9a4-2143-4cc6-a569-25fef23aa700" />

<img width="791" height="345" alt="starting salt minion" src="https://github.com/user-attachments/assets/52202416-66f3-4e89-8720-09b75d145629" />

Kun yhteys toimi, hyväksyimme minionin avaimen master-koneella, minkä jälkeen yhteys saatiin muodostettua onnistuneesti. Testasimme tätä komennolla sudo salt '*' test.ping, joka palautti arvon True, mikä vahvisti, että koneet pystyivät kommunikoimaan keskenään.

<img width="399" height="106" alt="listing available keys" src="https://github.com/user-attachments/assets/925672d0-82f7-4c30-b250-637f3b6aa153" />

<img width="381" height="106" alt="accepting minion key" src="https://github.com/user-attachments/assets/04f60420-9445-4bf6-942c-29967b61977a" />

<img width="406" height="64" alt="ping test to salt minion" src="https://github.com/user-attachments/assets/ade13539-d964-4dc3-b6d0-315ffe7c4fdb" />

## e) Kokeile vähintään kahta tilaa verkon yli 

Lopuksi loimme hakemiston doubletrouble, jonka sisällä oli tiedosto init.sls.
Tässä tiedostossa määritimme kaksi Salt-tilaa:

Paketin (htop) asennuksen

Tekstitiedoston (/home/vagrant/salt_message.txt) luonnin

<img width="536" height="131" alt="making a dir doubletrouble" src="https://github.com/user-attachments/assets/78aa873a-fe6d-4478-826f-980c389746fa" />

<img width="585" height="237" alt="doubletrouble config file" src="https://github.com/user-attachments/assets/49684b9e-4c8c-4093-bb99-1bc2be68e8ba" />

<img width="693" height="836" alt="output of the doubletrouble command" src="https://github.com/user-attachments/assets/8615167c-0c8f-4f81-948b-e981e490aba5" />


Ajoimme tämän tilan komennolla sudo salt '*' state.apply doubletrouble, ja tarkistimme minion-koneelta, että tiedosto oli luotu onnistuneesti.

<img width="565" height="51" alt="file is found in salt minion" src="https://github.com/user-attachments/assets/ae06337d-73d7-4425-b48d-e9d6f70dd292" />


Näin saimme aikaan toimivan Salt-järjestelmän, jossa master pystyy hallitsemaan minionia verkon yli — onnistunut ja toimiva kokonaisuus!


## Lähteet

https://terokarvinen.com/palvelinten-hallinta/#h3-soitto-kotiin,

https://terokarvinen.com/install-salt-on-debian-13-trixie/, 

https://terokarvinen.com/2021/two-machine-virtual-network-with-debian-11-bullseye-and-vagrant/, 

https://terokarvinen.com/2018/salt-quickstart-salt-stack-master-and-slave-on-ubuntu-linux/?fromSearch=salt%20quickstart%20salt%20stack%20master%20and%20slave%20on%20ubuntu%20linux, 

https://terokarvinen.com/2023/salt-vagrant/#infra-as-code---your-wishes-as-a-text-file
