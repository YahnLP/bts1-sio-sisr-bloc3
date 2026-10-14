# Annexe – Résultat de scan du réseau de la société Brumaire (fictif)

*Société, adresses et résultats **inventés**. Les numéros de version et de CVE sont réels ; les scores sont ceux couramment publiés (à vérifier sur la base NVD).*

**Brumaire** est une société fictive de 40 salariés. Un audit **autorisé** a été réalisé le même jour sur la plage `10.0.20.0/24`. L'infrastructure :

| Adresse | Rôle (selon la direction) | Exposition |
|---|---|---|
| `10.0.20.5` | Serveur web du site commercial | **Publié sur Internet** (redirection du port 443) |
| `10.0.20.10` | Serveur de fichiers de la comptabilité | LAN uniquement |
| `10.0.20.15` | « Ancien serveur de sauvegarde, à supprimer » | LAN uniquement |
| `10.0.20.30` | Poste de la directrice | LAN uniquement |

## Extrait des résultats

```text
Nmap scan report for 10.0.20.5
PORT    STATE SERVICE  VERSION
22/tcp  open  ssh      OpenSSH 9.2p1 Debian
80/tcp  open  http     nginx 1.22.1 (redirection vers HTTPS)
443/tcp open  ssl/http nginx 1.22.1
| ssl-enum-ciphers:
|   TLSv1.2: ... suites AES-GCM (forte)
|   TLSv1.3: ... forte
|_  least strength: A

Nmap scan report for 10.0.20.10
PORT     STATE SERVICE      VERSION
135/tcp  open  msrpc        Microsoft Windows RPC
139/tcp  open  netbios-ssn  Microsoft Windows netbios-ssn
445/tcp  open  microsoft-ds Windows Server 2012 R2 (SMBv1 activé)
3389/tcp open  ms-wbt-server Microsoft Terminal Services
Service Info: OS: Windows Server 2012 R2

Nmap scan report for 10.0.20.15
PORT     STATE SERVICE VERSION
21/tcp   open  ftp     vsftpd 2.3.4
|_ftp-anon: Anonymous FTP login allowed (FTP code 230)
22/tcp   open  ssh     OpenSSH 5.3 (protocol 2.0)
23/tcp   open  telnet  Linux telnetd
80/tcp   open  http    Apache httpd 2.2.15 ((CentOS))
3306/tcp open  mysql   MySQL 5.1.73 (accès réseau autorisé)

Nmap scan report for 10.0.20.30
PORT    STATE SERVICE VERSION
445/tcp open  microsoft-ds Windows 10 Pro
5900/tcp open vnc    VNC (protocol 3.8)
```

## Références utiles

| Constat | Référence | Score courant (à vérifier) |
|---|---|---|
| SMBv1 sur Windows (famille « EternalBlue ») | CVE-2017-0144 | 8,1 (élevé) |
| vsftpd 2.3.4 : porte dérobée dans une version diffusée | CVE-2011-2523 | 9,8 (critique) |
| Apache 2.2 / MySQL 5.1 / OpenSSH 5.3 : versions **en fin de vie**, plusieurs vulnérabilités publiées | plusieurs | variables |
| Telnet : aucune confidentialité (mots de passe en clair) | — (mauvaise pratique) | — |
