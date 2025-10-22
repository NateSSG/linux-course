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

## 1.pkg.installed (pakettien hallinta)

- Tarkoitus: Varmistaa, että tietty paketti on asennettuna.
  
- Esimerkki:

```
sudo salt-call --local state.single pkg.installed name=vim
```
- Tulokset: Jos Vim ei ole asennettuna, salt asentaa sen. Jos paketti on jo asennettu, mitään ei tapahdu -> idempotentti.

<img width="833" height="507" alt="pkg install" src="https://github.com/user-attachments/assets/70a6ed1f-fbda-430c-a685-83048b0cab8d" />
  
<img width="859" height="651" alt="pkg removed " src="https://github.com/user-attachments/assets/c1993b4c-c532-473e-8ff7-94c9805cb8b2" />

## 2.file.managed (tiedostojen hallinta)

- Tarkoitus: Luo tai ylläpitää tiedostoja halutulla sisällöllä ja ominaisuuksilla.

- Esimerkki SLS-tiedosto:


<img width="1047" height="83" alt="idem example command" src="https://github.com/user-attachments/assets/45a55233-7209-4bcd-ae02-53098d99bca7" />


<img width="1043" height="254" alt="idem file example code" src="https://github.com/user-attachments/assets/6be178cb-5fd8-4a05-a87d-b72439326a86" />

- Tulokset: Tiedosto /tmp/foo luodaan tai päivitetään vain, jos sisältö muuttuu. Useat ajot eivät muuta sitä, jos sisältö on sama.


<img width="868" height="556" alt="updated the foo file with my newly created one" src="https://github.com/user-attachments/assets/a25ff106-04b4-48a0-850c-261286e9bf96" />

<img width="745" height="364" alt="same command but no update" src="https://github.com/user-attachments/assets/be19453a-79b9-4bf0-b692-cacd5755c5fe" />


