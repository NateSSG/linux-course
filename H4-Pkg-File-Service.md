# H4 Pkg-File-Service | Nathaniel Ssendagire 13.11.2025

## Ympäristö

OS: Windows 11

Browser: Firefox 128.3.1esr (64-bit)

RAM: 16GB

Processor: AMD Ryzen 7 5700X - 6 cores used

GPU: AMD Radeon RX 9060 XT 16GB

Disk: 65 GB

Network: NAT

## Tiivistelmä

- Konfiguraationhallintajärjestelmällä, kuten Saltilla, voidaan hallita suurta määrää palveluita automaattisesti.

- Yleinen malli on pkg-file-service: asenna ohjelmisto, korvaa konfiguraatiotiedosto ja käynnistä demoni uudelleen.

- SSH-palvelimen portin muuttaminen voidaan tehdä yksinkertaisella Salt-statella.

- Masterilla luodaan state-tiedosto (sshd.sls) ja masterin kopio SSH-konfiguraatiosta (sshd_config).

State määrittelee:

- openssh-server paketin asennuksen

- /etc/ssh/sshd_config tiedoston hallinnan masterin kopion perusteella

- sshd palvelun ajon, joka valvoo konfiguraatiotiedoston muutoksia (watch)

- Kun state ajetaan minioneille, konfiguraatio korvaa paikalliset muutokset ja SSH-daemon käynnistyy uudelleen.

- Testaus onnistuu esimerkiksi yhteydellä uuteen porttiin (ssh -p 8888) tai verkon tarkistustyökaluilla (nc -vz).

- Lopputulos: pkg-file-service state toimii, ja SSH-palvelin on konfiguroitu turvallisesti ja automaattisesti.

## Minion kone

Ensiksi asensimme SSH:n minion-koneelle. Minion koneella konfiguroitiin sshd_config tiedoston, johon laitettiin port 22 ja 2222 tuki. 
<img width="381" height="41" alt="installing ssh on salt minion" src="https://github.com/user-attachments/assets/7a7b5856-243f-43ec-91d1-42749c7abf83" />

<img width="498" height="56" alt="command to edit ssh config" src="https://github.com/user-attachments/assets/b8053611-0ace-4d5d-bfaa-0c39e75d1d11" />

<img width="702" height="55" alt="adding port 2222 and 22 on minion" src="https://github.com/user-attachments/assets/d680b5df-86b7-48fd-8dd7-c9c747886d94" />

<img width="424" height="36" alt="restarting ssh" src="https://github.com/user-attachments/assets/52f4ff0c-a68d-4939-b8f6-fa2d8cf16303" />

<img width="749" height="109" alt="checking if ports are open" src="https://github.com/user-attachments/assets/47611b40-042f-4b7b-b141-519e4517ff16" />

## Master kone 

Tämän jälkeen loimme master-koneelle sshd_port-hakemiston, jonka sisällä oli init.sls-tiedosto. Tämä tiedosto määritteli, mitä muutoksia Salt teki minion-koneeseen. Loimme myös sshd_config-tiedoston master-koneelle, jotta minion saisi saman konfiguraation kuin master.

<img width="493" height="58" alt="creating new directory in master pc" src="https://github.com/user-attachments/assets/c8ea9673-35e9-4491-af84-e5fe95e99766" />

<img width="515" height="26" alt="init sls file created in sshd_port dir" src="https://github.com/user-attachments/assets/1724d058-377f-452d-b678-aef23445713d" />

<img width="623" height="341" alt="salt master config file" src="https://github.com/user-attachments/assets/20298968-359b-43e1-aeb3-ea635de494bc" />


<img width="521" height="19" alt="created sshd_config file in the sshd_port" src="https://github.com/user-attachments/assets/d8caa914-a768-4272-b7c2-f3cf67cf5ea0" />


<img width="372" height="158" alt="ssh configuration" src="https://github.com/user-attachments/assets/cdfaa82c-d754-4362-b1bf-fa8721e8d262" />







Minion-koneella vastaava sshd_config-tiedosto sijaitsi polussa /etc/ssh/sshd_config, kun taas masterilla se oli Saltin hakemistorakenteessa /srv/salt/sshd_port/sshd_config. Tiedoston asetuksissa estettiin root-käyttäjän kirjautuminen, sallittiin salasanalla kirjautuminen, otettiin käyttöön SFTP (Secure File Transfer Protocol) ja avattiin portit 22 ja 2222 SSH-yhteyksille.

## Salt tila

Saltin tila (state.apply sshd_port) päivitti minionin asetukset automaattisesti ja käynnisti SSH-palvelun uudelleen, kun muutokset havaittiin. Tämä osoitti, että file.managed ja service.watch toimivat oikein ja automaatio oli onnistunut.


<img width="724" height="37" alt="ran the command to salt minioin" src="https://github.com/user-attachments/assets/1b719bb7-8a55-45cc-b3fb-a113b991ed89" />


<img width="1428" height="986" alt="open ssh server" src="https://github.com/user-attachments/assets/2b2456d4-afe4-48d5-8f52-8be84863b845" />


<img width="710" height="425" alt="changes and success" src="https://github.com/user-attachments/assets/f90d3556-1c22-49e1-b5b7-8833f910b8a0" />

## Pikku testi jos muokkaa Minionia

Testasimme myös Saltin valvontamekanismia tekemällä pienen muutoksen minion-koneen tiedostoon esimerkiksi echo-komennolla. Kun masterin state ajettiin, Salt havaitsi muutoksen (watch-mekanismin avulla) ja korjasi minionin tiedoston palauttamalla sen masterin määrittelemän version mukaiseksi. Tämän ansiosta minionin konfiguraatio palautui automaattisesti oikeaan tilaansa, mikä havainnollistaa Saltin tarjoamaa redundanssia ja konfiguraation hallinnan luotettavuutta.



<img width="790" height="106" alt="minion test listen" src="https://github.com/user-attachments/assets/042626cc-94e0-4b65-9c41-0ff07697b742" />

<img width="892" height="447" alt="minion ssh server running" src="https://github.com/user-attachments/assets/78cee7cf-45f7-4dbb-ac0a-d7de2ed9f607" />

<img width="714" height="67" alt="test change minion pc" src="https://github.com/user-attachments/assets/8d366984-d90a-4c8c-ab31-dce2116d7a7b" />

<img width="526" height="781" alt="test change on master pc success" src="https://github.com/user-attachments/assets/12a38de1-1faa-432e-9a91-22085944ad19" />

## Lähteet
https://terokarvinen.com/2018/04/03/pkg-file-service-control-daemons-with-salt-change-ssh-server-port/?fromSearch=karvinen%20salt%20ssh,

https://terokarvinen.com/palvelinten-hallinta/#h4-pkg-file-service




