# H2 Infraa koodina | Nathaniel Ssendagire 30.10.2025

## Ympäristö

OS: Debian GNU/Linux 13 Trixie

Browser: Firefox 128.3.1esr (64-bit)

Hardware Model: Virtualbox memory used 11 GB

Processor: AMD Ryzen 7 5700X - 6 cores used

GPU: AMD Radeon RX 9060 XT 16GB

Disk: 65 GB

Network: NAT

## Tiivistelmä

- Salt “Hello World”: Luodaan yksinkertainen infra-as-code -esimerkki, jossa Salt varmistaa, että tiedosto /tmp/hellotero on olemassa.

YAMLin perussäännöt:

- Käytetään key: value-pareja.

- Vain välilyönnit sallittuja (ei tabulaattoreita).

- Kommentit alkavat #.

Rakenteet: scalareita (arvot), listoja (alkaa -), ja sanakirjoja (sisäkkäisiä key-value -pareja).

Idempotenssi: Saltin toistettu ajaminen ei muuta järjestelmää, jos se on jo halutussa tilassa.

Tärkeimmät Saltin toiminnot: pkg, file, service, user, cmd.

Top file (top.sls):

- Määrittää, mitä konfiguraatioita (state-tiedostoja) sovelletaan millekin koneelle.

- Rakenteessa on kolme tasoa: Environment → Target → States.

- Esim. kaikki koneet, joiden nimi alkaa “web”, saavat apache-tilan.

## A)  Hei infrakoodi!

<img width="730" height="474" alt="salt sls file creation" src="https://github.com/user-attachments/assets/a7d16f4f-2927-45a5-b897-df7b5c47d1f2" />

<img width="717" height="474" alt="hellonate sls file was created" src="https://github.com/user-attachments/assets/bfa688da-1d93-49fb-92d7-89df1c85af4b" />

<img width="500" height="69" alt="printed text from the created file" src="https://github.com/user-attachments/assets/aa09db4f-c184-4fdc-854b-776c3de24276" />

Tässä loin hellonate tiedoston omalle kooneelle tmp kansioon. Tiedosto sisältää tekstin "Greetings fellow comrades, salt has created a file!!"

## B) Toppping

<img width="395" height="50" alt="topfile creation" src="https://github.com/user-attachments/assets/87017d48-b422-482b-b6b6-11e3ba689b5d" />

<img width="808" height="205" alt="topfile commands" src="https://github.com/user-attachments/assets/d5a5f0b3-05a2-4968-91de-0e41fc068de7" />
<img width="721" height="704" alt="topfile command output" src="https://github.com/user-attachments/assets/c0f5788b-313f-470f-96c2-b75437b3bfe4" />
<img width="1043" height="628" alt="topfile command output 2" src="https://github.com/user-attachments/assets/c08a8c02-7432-4089-9e16-f20df8cfbb09" />

Topping toimii siten, että luodaan top.sls-tiedosto, johon määritetään kaikki luodut hello, file, service ja user -sls-tiedostot. Kun suoritat komennon sudo salt-call --local state.apply, sinun ei tarvitse erikseen mainita tiettyä tiedostoa — Salt etsii automaattisesti top.sls-tiedoston sisältöineen /srv/salt/-kansiosta ja ajaa sen. Kaikki top.sls-tiedostossa määritetyt tilat suoritetaan, kun komento ajetaan terminaalissa.

## Viisikko tiedostossa
Loin jokaisen tiedoston erikseen, joissa on erilaiset funktiot

## hellopkg luonti
<img width="809" height="176" alt="hellopkg creation" src="https://github.com/user-attachments/assets/c50cc519-2256-4188-b20c-89dfb84b2b92" />


<img width="271" height="109" alt="hellopkg command" src="https://github.com/user-attachments/assets/27901cd4-fdfc-4f9d-9199-db23ccc973f8" />

<img width="706" height="491" alt="hellopkg command output" src="https://github.com/user-attachments/assets/10ff5811-cd18-415e-872b-6309d95c7188" />

## hellofile luonti

<img width="805" height="144" alt="hellofile creation" src="https://github.com/user-attachments/assets/3f1f4e0c-10c8-4675-93e8-08fc37cf4257" />

<img width="820" height="147" alt="hellofile command" src="https://github.com/user-attachments/assets/ffa5f865-76a5-4441-8114-fe02bb1ecd54" />

<img width="721" height="429" alt="hellofile command output" src="https://github.com/user-attachments/assets/6b3ecc1c-95de-403a-8a84-92e2136052ab" />

## helloservice luonti

<img width="828" height="156" alt="helloservice creation" src="https://github.com/user-attachments/assets/4c6e8f77-9ba3-465d-9a28-2b5e10fdcfdf" />

<img width="803" height="159" alt="helloservice command" src="https://github.com/user-attachments/assets/1c732d9c-0c60-4dd6-a134-3524346a45c0" />

<img width="770" height="364" alt="helloservice command output" src="https://github.com/user-attachments/assets/a86986d3-1d21-407d-82e6-556201f0a08a" />

## hellouser luonti

<img width="516" height="151" alt="hellouser creation" src="https://github.com/user-attachments/assets/1bc84d81-a44e-4769-bf6a-a26859917271" />

<img width="806" height="138" alt="hellouser command" src="https://github.com/user-attachments/assets/ececa82e-ee43-4bd7-9569-9ba5531c8679" />

<img width="721" height="374" alt="hellouser command output" src="https://github.com/user-attachments/assets/8aede0ba-d1fc-42cf-8ae7-5a8d641c7a04" />

## hellocmd luonti 

<img width="799" height="131" alt="hellocmd creation" src="https://github.com/user-attachments/assets/a8f74cb8-8220-4230-9e8e-e0e91f2fbc16" />

<img width="806" height="133" alt="hellocmd commands" src="https://github.com/user-attachments/assets/f1e3aebb-546d-4a6f-ab8e-f5014a579ea3" />

<img width="909" height="681" alt="hellocmd command output" src="https://github.com/user-attachments/assets/9582f568-8529-4db0-be81-d9e844fd80af" />

## kaikkien sls tiedostot mitkä olin luonut

<img width="528" height="234" alt="all the commands displayed in salt directory" src="https://github.com/user-attachments/assets/0a642c27-312d-45be-a0da-0b01c72269a6" />

## Tee sls-tiedosto

<img width="1284" height="772" alt="new salt minion commands" src="https://github.com/user-attachments/assets/26043788-593d-43eb-b146-780783a87435" />

Loin sls tiedoston nimeltä multicommands jossa oli apache2 lataus sekä käynnistys, greetings_file tiedoston luonti sekä käyttäjä Nathaniel_SSG

<img width="887" height="767" alt="1 blue 3 green" src="https://github.com/user-attachments/assets/af425f1e-e61c-4f10-81cb-352387e50adf" />
<img width="295" height="134" alt="summary of 1 blue" src="https://github.com/user-attachments/assets/5fb34ae4-6a7b-45d1-9b23-906a8536d2ad" />


Ajoin luomani tiedoston. Vastaus oli että 1 uusi muutos on tullut (sinisellä) ja 3 oli ihan ok (vihree)

<img width="995" height="762" alt="all greeeeen" src="https://github.com/user-attachments/assets/6e32ba43-ee9d-45bd-9b6e-7af43aae086c" />

<img width="304" height="140" alt="summary of greeeeeeen" src="https://github.com/user-attachments/assets/40d52de6-cc18-47f6-a1fe-f999af5cb9fd" />

Ajoin sen toisen kerran ja nyt se sanoo että kaikki on ihan ajantasalla eli idempotenttinen. 


## Testasin salt minioniä



<img width="726" height="360" alt="salt minion config" src="https://github.com/user-attachments/assets/7dfbdb85-1e8b-4da8-a5c9-2b61fb511ab6" />

<img width="956" height="368" alt="ip " src="https://github.com/user-attachments/assets/ac90c863-69fe-4198-8760-03684547d4fb" />

<img width="1277" height="373" alt="master ip address" src="https://github.com/user-attachments/assets/5e81ae18-5d81-4cae-82ec-5da5148e4af9" />

Laitoin master ip osoitteeksi tuon osoitteen mikä näkyy edellisessä kuvassa.

<img width="313" height="155" alt="unaccepted keys" src="https://github.com/user-attachments/assets/b41bfead-9bfc-4b19-87ce-26e4e0053910" />

<img width="561" height="143" alt="accepting the keys" src="https://github.com/user-attachments/assets/de1a3abf-3e72-4338-b030-d60c4435fe2a" />

<img width="298" height="48" alt="key has been accepted" src="https://github.com/user-attachments/assets/a986e00b-c449-4d17-860f-389e885a00b4" />

<img width="372" height="85" alt="sudo salt test ping " src="https://github.com/user-attachments/assets/64ea01cf-e36f-45aa-9ed7-c55c083a2a8e" />

Testattiin saltin toimivuutta pingaamalla saltia

<img width="534" height="376" alt="file created" src="https://github.com/user-attachments/assets/0dc419e0-8e69-4e9f-bfa9-4fed905cd14f" />

<img width="1174" height="283" alt="salt minion service working" src="https://github.com/user-attachments/assets/ac712fbd-f184-4504-85bf-2d4de39ba309" />

Salt palvelu on päällä.

<img width="1284" height="772" alt="new salt minion commands" src="https://github.com/user-attachments/assets/26043788-593d-43eb-b146-780783a87435" />

Loin sls tiedoston nimeltä multicommands jossa oli apache2 lataus sekä käynnistys, greetings_file tiedoston luonti sekä käyttäjä Nathaniel_SSG

<img width="438" height="169" alt="4 succeeded 3 changes" src="https://github.com/user-attachments/assets/9a65a236-4d3b-4dcf-913d-6b73b4d83ced" />


<img width="1282" height="649" alt="file and apache2 screenshot" src="https://github.com/user-attachments/assets/e198813e-fcb8-46ab-a660-900442792023" />

<img width="1279" height="641" alt="create user screenshot" src="https://github.com/user-attachments/assets/266561ff-ac9d-444b-b5af-ebd028865762" />


<img width="1109" height="705" alt="everything is green so no updates" src="https://github.com/user-attachments/assets/b2bfdcba-55d1-4d5c-88d3-b4a512dfedc1" />

Ajettiin komento uudestaan ja siinä on idempotentti eli ei tehnyt mitään muutoksia jos kaikki on ajantasalla.

<img width="632" height="214" alt="evidence that they are on the minion pc as well" src="https://github.com/user-attachments/assets/c3335c6d-1331-4051-8520-22466190d331" />

kuten huomaatte tiedostot näkyvät minion pc:llä

## Lähteet

https://terokarvinen.com/palvelinten-hallinta/#h2-infraa-koodina,

https://terokarvinen.com/2024/hello-salt-infra-as-code/, 

https://docs.saltproject.io/salt/user-guide/en/latest/topics/overview.html#rules-of-yaml, 

https://docs.saltproject.io/en/latest/ref/states/top.html, 

