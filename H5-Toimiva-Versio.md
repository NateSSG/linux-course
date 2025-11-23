## H5 Toimiva Versio | Nathaniel Ssendagire 23.11.2025

## Ympäristö

OS: Debian GNU/Linux 13 Trixie

Browser: Firefox 128.3.1esr (64-bit)

Hardware Model: Virtualbox memory used 11 GB

Processor: AMD Ryzen 7 5700X - 6 cores used

GPU: AMD Radeon RX 9060 XT 16GB

Disk: 65 GB

Network: NAT

## Online

<img width="1135" height="762" alt="repo creation" src="https://github.com/user-attachments/assets/f4d3493c-6cd9-49f6-b839-861404462212" />

Luotiin repo nimeltä "Snow". 


## Dolly

<img width="764" height="46" alt="cloning" src="https://github.com/user-attachments/assets/1fb19995-83ca-4661-b2bb-7aaf1b3215dd" />
Kloonattiin repo virtuaalikoneelle.

<img width="842" height="36" alt="email and name config" src="https://github.com/user-attachments/assets/ef00f149-8ae6-4938-bafe-61fd74d8db16" />
Konfiguroitiin sähköposti osoite sekä oma nimi.

## Avain SSH:llä

<img width="752" height="548" alt="keygen creation" src="https://github.com/user-attachments/assets/e0d4c563-466f-4487-9885-e6bfcccaf532" />

<img width="999" height="64" alt="public key " src="https://github.com/user-attachments/assets/3c645805-c813-40b4-9e52-c8b749bb96d7" />
Ensiksi generoitiin ssh-avain terminaalista. Sitten annettiin nimeksi ihan tuo perus id_ed25519 ilman mitään salasanaa. Avain oli sitten luotu .ssh hakemistoon mistä sitten nappasin sen julkisen avaimen.

<img width="893" height="469" alt="key creation github" src="https://github.com/user-attachments/assets/f8afa927-abe2-477e-835b-1942c0292f5e" />

Nimesin avaimen snowkeyksi. Laitoin saamani julkisen avaimen tuonne avain laatikkoon ja painoin add ssh key.

<img width="828" height="71" alt="connection successfull" src="https://github.com/user-attachments/assets/aab56b0e-cb6e-4cb7-bedd-142415bf1944" />

Seuraavaksi menin takaisin snow hakemistoon ja otin ssh yhteyden github repooni.

<img width="854" height="23" alt="set the url to the git file in the snow dir" src="https://github.com/user-attachments/assets/03134272-3875-48a4-a2f5-41bd3865e87c" />

Asetin yhteyden sillä tavalla että aina kun pushaan jotain niin se menee automaattisesti tuonne Snow repoon ilman sitä että tarvitsee joka kerta laittaa jotain salasanaa.

<img width="477" height="63" alt="checking if it works the git" src="https://github.com/user-attachments/assets/10259439-ef7a-4d71-9bc3-c9b78bb63d3f" />

<img width="824" height="352" alt="test file creation to github" src="https://github.com/user-attachments/assets/f8f92fd6-834f-49a5-92df-9f870dfef5a3" />

<img width="557" height="75" alt="gibberish added " src="https://github.com/user-attachments/assets/a737afcd-fea0-4456-be79-552a8f797b62" />

<img width="797" height="48" alt="file was added" src="https://github.com/user-attachments/assets/c007b167-af70-4e57-b0f0-bf2aff540748" />

Tässä tehtiin testi että toimiiko kaikki kuten pitää. Loin tiedoston nimeltä test.txt johon kirjoitin ihan jotai satunnaista tekstiä. Sit tein git add ., git commit johon kirjoitin lyhyen kuvauksen siitä mitä tein.

Seuraavaksi pullasin varmistaakseni, että kaikki ovat ajan tasalla ja sitten työnsin sen repooni. Sitten lähdin githubiin katsomaan, että oliko se oikeasti siellä. Tiedoston nimi täsmää sekä lyhyt kuvaus minkä olin kirjoittanut sinne.



## Avain HTTPS:llä

<img width="895" height="855" alt="snow token gen" src="https://github.com/user-attachments/assets/16f0723d-fa12-42f2-9e81-911a2f9ea0bd" />

<img width="694" height="245" alt="git pushing" src="https://github.com/user-attachments/assets/6e072484-259d-4f05-aa5b-0e1c4d9504c6" />

Olin vähän utelias ja halusin testata että miten tämä toimii HTTPS:llä. Avain HTTPS:llä oli mielenkiintoinen. Piti luoda token jonka nimesin snowtokeniksi. Seuraavaksi valitsin tietyn repon ja se oli tietenkin se "Snow" repo. Seuraavaksi palasin takaisin terminaaliin ja git pushasin. Sitten se kysyi käyttäjätunnusta sekä salasanaa. Tämä salasana on se git token minkä olin luonut tässä tapauksessa. 

## Doh!

<img width="675" height="195" alt="reverted back to normal" src="https://github.com/user-attachments/assets/bcf2d6b9-9f4a-47c0-9b2d-a2031dedcb50" />

Seuraavaksi lähin testaamaan sitä jos jotain meneekin pieleen ja vahingossa committaat jotain. Ensiksi tein ihan saman jutun niin kuin tiedoston luonnissa mutta tässä muutin tekstiä README.md tiedostosta. Jos jokin menee pieleen ei muuta kuin git reset --hard HEAD~1 palauttaa projektisi edelliseen pushiin. 

## Suolattu Rakki


<img width="1255" height="583" alt="running salt " src="https://github.com/user-attachments/assets/60cb5d80-23ee-40a0-b4b0-da9f5cef2543" />

<img width="648" height="482" alt="running salt pt2" src="https://github.com/user-attachments/assets/4edf0c32-a68a-47db-95a9-c50367725aec" />

Ajoin saltin paikallisesti Snow hakemistossa. Salt toimii kuten pitää.

