## H5 Toimiva Versio | Nathaniel Ssendagire 23.11.2025

## Ympäristö

OS: Debian GNU/Linux 13 Trixie

Browser: Firefox 128.3.1esr (64-bit)

Hardware Model: Virtualbox memory used 11 GB

Processor: AMD Ryzen 7 5700X - 6 cores used

GPU: AMD Radeon RX 9060 XT 16GB

Disk: 65 GB

Network: NAT

## Tiivistelmä

Git on versionhallintajärjestelmä, joka tallentaa projektin tilan snapshoteina (kuvina tiedostoista), ei pelkästään muutoksina tiedostoihin kuten perinteiset VCS-järjestelmät (esim. CVS tai Subversion). Tämä tekee Gitistä erittäin nopean ja paikallisesti toimivan, koska suurin osa operaatioista (historia, diffit, commitit) tapahtuu omalta koneelta ilman verkkoyhteyttä.

Git myös tarkistaa tiedostojen eheyden SHA-1-tarkistussummien avulla, mikä estää tiedon katoamisen tai vahingot siirrossa. Useimmat Git-operaatiot vain lisäävät tietoa tietokantaan, joten once commitattu snapshot on turvallisesti tallessa.

### Git-tiedostojen kolme tilaa:

- Modified (muokattu) – tiedostoa on muutettu, mutta muutokset eivät ole vielä commitattu.

- Staged (valmisteltu) – muutokset on merkitty seuraavaan commit-snapshotiin.

- Committed (commitattu) – muutokset on tallennettu paikalliseen Git-tietokantaan pysyvästi.

Näiden tilojen kautta hallitaan projektin tiedostot työpuussa (working tree), staging-alueella ja Git-hakemistossa (Git directory).

### Perustoiminnot käytännössä:

- git add . – lisää kaikki muutokset staging-alueelle.

- git commit -m "viesti" – tallentaa snapshotin Git-tietokantaan.

- git pull – hakee ja yhdistää etärepositorion muutokset.

- git push – lähettää paikalliset commitit etäpalvelimelle (esim. GitHub).


## Online

<img width="1135" height="762" alt="repo creation" src="https://github.com/user-attachments/assets/f4d3493c-6cd9-49f6-b839-861404462212" />

- Loin GitHubiin uuden repositorion nimeltä “Snow”.


## Dolly

<img width="764" height="46" alt="cloning" src="https://github.com/user-attachments/assets/1fb19995-83ca-4661-b2bb-7aaf1b3215dd" />

<img width="842" height="36" alt="email and name config" src="https://github.com/user-attachments/assets/ef00f149-8ae6-4938-bafe-61fd74d8db16" />

- Repositorio kloonattiin virtuaalikoneelle. Sen jälkeen konfiguroitiin Git-käyttäjätiedot: sähköpostiosoite ja käyttäjänimi, jotta commitit tunnistetaan oikein.

## Avain SSH:llä

<img width="752" height="548" alt="keygen creation" src="https://github.com/user-attachments/assets/e0d4c563-466f-4487-9885-e6bfcccaf532" />

<img width="999" height="64" alt="public key " src="https://github.com/user-attachments/assets/3c645805-c813-40b4-9e52-c8b749bb96d7" />

- SSH-avainpari luotiin terminaalissa komennolla:

      ssh-keygen -t ed25519 -C "sahkoposti@esimerkki.fi"
    
- Avain tallennettiin oletusnimellä id_ed25519 ilman salasanaa.

<img width="893" height="469" alt="key creation github" src="https://github.com/user-attachments/assets/f8afa927-abe2-477e-835b-1942c0292f5e" />

- Julkinen avain kopioitiin .ssh-hakemistosta ja lisättiin GitHubiin kohtaan SSH and GPG keys, nimellä “snowkey”.

<img width="828" height="71" alt="connection successfull" src="https://github.com/user-attachments/assets/aab56b0e-cb6e-4cb7-bedd-142415bf1944" />

Seuraavaksi menin takaisin snow hakemistoon ja otin ssh yhteyden github repooni. Autentikointi onnistui.

<img width="854" height="23" alt="set the url to the git file in the snow dir" src="https://github.com/user-attachments/assets/03134272-3875-48a4-a2f5-41bd3865e87c" />

- Paikallisessa Snow-hakemistossa Gitin remote URL asetettiin SSH-muotoon:

      git remote set-url origin git@github.com:NateSSG/Snow.git

- Näin kaikki tulevat push-komennot voidaan tehdä ilman salasanaa.

<img width="477" height="63" alt="checking if it works the git" src="https://github.com/user-attachments/assets/10259439-ef7a-4d71-9bc3-c9b78bb63d3f" />

<img width="824" height="352" alt="test file creation to github" src="https://github.com/user-attachments/assets/f8f92fd6-834f-49a5-92df-9f870dfef5a3" />

<img width="557" height="75" alt="gibberish added " src="https://github.com/user-attachments/assets/a737afcd-fea0-4456-be79-552a8f797b62" />

<img width="797" height="48" alt="file was added" src="https://github.com/user-attachments/assets/c007b167-af70-4e57-b0f0-bf2aff540748" />

- Luotiin testitiedosto test.txt ja kirjoitettiin siihen satunnaista tekstiä.

- Muutokset lisättiin staging-alueelle ja commitattiin:
      
      git add .
      git commit -m "Lisätty testitiedosto"

- Päivitettiin repositorio git pull -komennolla ja puskettiin muutokset.

- GitHubista tarkistettiin, että tiedosto ja commit-viesti näkyivät oikein.

## Avain HTTPS:llä

<img width="895" height="855" alt="snow token gen" src="https://github.com/user-attachments/assets/16f0723d-fa12-42f2-9e81-911a2f9ea0bd" />

<img width="694" height="245" alt="git pushing" src="https://github.com/user-attachments/assets/6e072484-259d-4f05-aa5b-0e1c4d9504c6" />

- Testattiin HTTPS-autentikointia luomalla henkilökohtainen token nimeltä “snowtoken”.

- Token rajoitettiin vain Snow-repositoriolle.

- HTTPS-pushissa Git pyysi käyttäjätunnusta ja salasanaa, ja token toimi salasanana.

- Tämä varmisti, että HTTPS-token-autentikointi toimii oikein.

## Doh!

<img width="675" height="195" alt="reverted back to normal" src="https://github.com/user-attachments/assets/bcf2d6b9-9f4a-47c0-9b2d-a2031dedcb50" />

- Testattiin virhetilanteen palautusta muokkaamalla README.md-tiedostoa ja tekemällä commit.
- Jos commit olisi virheellinen, komento:

      git reset --hard HEAD~1
  
- palauttaa projektin edelliseen pushiin, poistaen ei-toivotut muutokset ja commitin.


## Tukki

<img width="709" height="153" alt="checking all the stuff " src="https://github.com/user-attachments/assets/596ee970-61b8-4485-97ce-6095eef72bc7" />

Lokin tarkastelu:
Komennolla

      git log --oneline --graph --decorate
      
voi nähdä repositorio commitit lyhyesti, graafisesti ja merkittynä branchien kanssa. Esimerkki tulosteesta:

            * 568d704 (HEAD -> master, origin/master) Added more content to notes.txt
            * 05c3975 Add notes file

- Tässä näkyy kaksi viimeisintä commitia.

- HEAD -> master, origin/master kertoo, että paikallinen master-branch ja etärepo ovat synkassa.

- Jokainen commitissa näkyvä hash (esim. 568d704) tunnistaa commitin yksilöllisesti.

Käyttäjätietojen tarkistus:
- Komennolla:

            git config --global user.name
            git config --global user.email
  
voi varmistaa, että committeihin tallennetaan oikea nimi ja sähköposti.

## Suolattu Rakki


<img width="1255" height="583" alt="running salt " src="https://github.com/user-attachments/assets/60cb5d80-23ee-40a0-b4b0-da9f5cef2543" />

<img width="648" height="482" alt="running salt pt2" src="https://github.com/user-attachments/assets/4edf0c32-a68a-47db-95a9-c50367725aec" />

Salt-tiloja ajettiin paikallisesti Snow-hakemistosta:

    sudo salt-call --local --file-root /srv/salt state.apply
    
Salt suoritti kaikki määritellyt tilat onnistuneesti, mikä osoitti automaation ja deploymentin toimivuuden

## Lähteet

https://git-scm.com/book/en/v2/Getting-Started-What-is-Git%3F,

https://github.com/terokarvinen/suolax/,

https://github.com/terokarvinen/suolax/commits/main/,

https://terokarvinen.com/palvelinten-hallinta/#h5-toimiva-versio,

https://git-scm.com/book/en/v2




