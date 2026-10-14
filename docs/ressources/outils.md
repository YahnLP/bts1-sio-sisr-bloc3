# Outils et laboratoires

| Outil | Usage dans la formation | Accès |
|---|---|---|
| **VirtualBox** | Machines virtuelles Debian, Windows et Windows Server : l'**environnement de laboratoire** des TP de sécurité (PKI, VPN, journaux, durcissement). | Installé sur les postes de la salle |
| **OpenSSL, GnuPG** | Chiffrement, hachage, signatures, autorité de certification interne (S10 à S12). | Paquets Debian |
| **WireGuard** | Tunnel VPN site à site (S13). | Paquet Debian |
| **Wireshark** | Capture et analyse de trames : voir ce qui circule en clair et ce qui est chiffré. | Installé sur les postes de la salle |
| **Nmap** | Découverte et audit de ports et de services (S16), uniquement sur le laboratoire. | Paquet Debian |
| **Suricata, fail2ban** | Détection d'intrusion, blocage de tentatives répétées (S15). | Paquets Debian |
| **Simulateur réseau, Cisco Packet Tracer** | Comprendre la segmentation et le filtrage (S14). Ils servent à comprendre et s'entraîner. | [Simulateur du bloc 2](https://yahnlp.github.io/bts1-sio-sisr-bloc2/simulateur/simulateur-reseau.html) · compte Networking Academy pour Packet Tracer |
| **InfraLab** | Gestion de parc et tickets (bloc 1) : utile pour documenter les incidents. | [yahnlp.github.io/InfraLab](https://yahnlp.github.io/InfraLab/) |

## Règles de laboratoire

> [!WARNING]
> - Les **identifiants communs d'un TP** (par exemple `etudiant` / `Lab-2026`) sont des **identifiants de laboratoire** : ils sont identiques pour toute la classe afin que chacun fasse la même chose dans un environnement contrôlé. **Ils ne sont jamais repris** dans une réalisation, un dossier d'épreuve ou un vrai système.
> - **On n'attaque que le laboratoire.** Les outils d'audit (Nmap, scanners de vulnérabilités) ne se lancent que sur les machines virtuelles du TP, isolées du réseau de l'établissement.
> - **Une simulation ne remplace pas une réalisation.** Pour les blocs 1 et 2, une solution réduite à une simulation n'est pas acceptable à l'épreuve (annexe II.E) ; ici le laboratoire sert à **comprendre et s'entraîner**.
