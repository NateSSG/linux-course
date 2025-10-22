# H1 Viisikko | Nathaniel Ssendagire 22.10.2025

## Ympäristö 

OS: Debian GNU/Linux 13 Trixie

Browser: Firefox 128.3.1esr (64-bit)

Hardware Model: Virtualbox memory used 11 GB

Processor: AMD Ryzen 7 5700x - 6 cores used

Disk: 65 GB

Network: NAT

## Salt Asennus.

Käytin apuna teron ohjeita saltin asentamiseen: https://terokarvinen.com/install-salt-on-debian-13-trixie/. Ne oli selitetty tosi selkeesti ja sain saltin ladattua ilman mitään ongelmia.

## Viisi tärkeintä Saltin tilafunktiota Linuxissa

## 1. pkg.installed (pakettien hallinta)

- Tarkoitus: Varmistaa, että tietty paketti on asennettuna.
  
- Esimerkki:

```
sudo salt-call --local state.single pkg.installed name=vim
```
- Tulokset: Jos Vim ei ole asennettuna, salt asentaa sen. Jos paketti on jo asennettu, mitään ei tapahdu -> idempotentti.

<img width="833" height="507" alt="pkg install" src="https://github.com/user-attachments/assets/70a6ed1f-fbda-430c-a685-83048b0cab8d" />
  
<img width="859" height="651" alt="pkg removed " src="https://github.com/user-attachments/assets/c1993b4c-c532-473e-8ff7-94c9805cb8b2" />

## 2. file.managed (tiedostojen hallinta)

- Tarkoitus: Luo tai ylläpitää tiedostoja halutulla sisällöllä ja ominaisuuksilla.

- Esimerkki SLS-tiedosto:


<img width="1047" height="83" alt="idem example command" src="https://github.com/user-attachments/assets/45a55233-7209-4bcd-ae02-53098d99bca7" />


<img width="1043" height="254" alt="idem file example code" src="https://github.com/user-attachments/assets/6be178cb-5fd8-4a05-a87d-b72439326a86" />

- Tulokset: Tiedosto /tmp/foo luodaan tai päivitetään vain, jos sisältö muuttuu. Useat ajot eivät muuta sitä, jos sisältö on sama.


<img width="868" height="556" alt="updated the foo file with my newly created one" src="https://github.com/user-attachments/assets/a25ff106-04b4-48a0-850c-261286e9bf96" />

<img width="745" height="364" alt="same command but no update" src="https://github.com/user-attachments/assets/be19453a-79b9-4bf0-b692-cacd5755c5fe" />

## 3. service.running (palveluiden hallinta)

-Tarkoitus: Varmistaa, että palvelu on käynnissä ja tarvittaessa käynnistyy automaattisesti.

<img width="734" height="481" alt="failed to run service" src="https://github.com/user-attachments/assets/e374c128-6c72-4dc6-a5c7-907ff73e68c5" />

Tässä kuvassa palvelun käynnistys epäonnistui, koska minulla ei ollut apache2 ladattuna.


<img width="739" height="484" alt="apache2 running " src="https://github.com/user-attachments/assets/7e22401d-a659-4db8-a489-793890f9405e" />
<img width="736" height="477" alt="apache2 disabled" src="https://github.com/user-attachments/assets/98479181-a4a4-4e23-8618-85fc16ebdab2" />


Ladattuani apache2, komento toimi niin kuin pitää.

Selitys:

- Salt tarkistaa, että Apache2-palvelu (apache2) on käynnissä.
- Jos palvelu ei ole käynnissä, Salt käynnistää sen.
- Jos se on jo käynnissä, Salt ei tee mitään


## 4. user.present (käyttäjien hallinta)

- Tarkoitus: Luo käyttäjän, jos sitä ei ole olemassa.

<img width="1052" height="640" alt="natedabest id created" src="https://github.com/user-attachments/assets/8de34ef8-a12b-4d20-a754-a6feb827966f" />

<img width="884" height="543" alt="removed the user natedabest" src="https://github.com/user-attachments/assets/bce0adbb-a122-449e-b736-e746870fe20e" />

## 5. cmd.run (komentojen suoritus)

- Tarkoitus: Suorittaa mielivaltaisia shell-komentoja.

Esimerkki:

```
sudo salt-call --local state.single cmd.run 'echo "Hello from Salt"'

```
Tulokset: Komento suoritetaan joka kerta. Eiu ole luonnostaan idempotentti, mutta sen voi tehdö idempotentiksi käyttämällä esim. creates, onlyif tai unless. Komento suoritetaan vain, jos ehdot eivät ole jo täyttyneet.

## Yhteenveto

- pkg, file, service, user -> kaikki idempotentteja -> järjestelmä ei muutu, jos haluttu tila on jo saavutettu.
- cmd -> ei idempotentti ilman lisäehtoja
- idempotenssi on tärkeää, koska Saltin komentoja voidaan ajaa useita kertoja ilman, että järjestelmään tehdään turhia muutoksia.
- Tämä tekee järjestelmän hallinnasta ennustettavaa ja turvallista.


  




