# Services Réseaux Avancés – Travaux pratiques

**Université Cheikh Anta Diop de Dakar – École Supérieure Polytechnique (ESP)**
Département Génie Informatique – L3 GLSI – Année universitaire 2026/2027

| | |
|---|---|
| **Étudiant** | Daouda CISSE |
| **Enseignant** | Dr Keba GUEYE |
| **Module** | Services Réseaux Avancés |

Ce dépôt rassemble les rapports des trois TP d'administration et de prise de contrôle à distance : **SSH**, **RDP** et **VNC / noVNC**. Chaque rapport (au format PDF) est illustré par les captures d'écran réalisées pendant les manipulations et décrit les problèmes rencontrés ainsi que leurs solutions.

## Sommaire

| TP | Sujet | Rapport (PDF) | Dossier |
|---|---|---|---|
| 1 | Mise en place du protocole SSH | [Rapport_TP_SSH.pdf](tp-ssh/Rapport_TP_SSH.pdf) | [tp-ssh](tp-ssh/) |
| 2 | Configuration et utilisation de RDP | [Rapport_TP_RDP_L3GLSI.pdf](tp-rdp/Rapport_TP_RDP_L3GLSI.pdf) | [tp-rdp](tp-rdp/) |
| 3 | Configuration et utilisation de VNC et noVNC | [Rapport_TP_VNC_noVNC.pdf](tp-vnc-novnc/Rapport_TP_VNC_noVNC.pdf) | [tp-vnc-novnc](tp-vnc-novnc/) |

## Résumé des travaux

### TP SSH
- Installation et activation du serveur OpenSSH sur une VM Ubuntu 26.04, vérification du port 22.
- Connexion depuis un client macOS par mot de passe, puis par **clés RSA** (génération, copie avec `scp`, `authorized_keys`).
- **Tunnels SSH** (redirection locale de port) vers un serveur web Apache (port 1024) et une base MariaDB (port 3307).
- Difficultés traitées : permissions des clés, service SSH inactif côté Mac, authentification du compte `root` de MariaDB.

### TP RDP
- Activation du Bureau à distance sur un serveur **Windows 11 Pro** (NLA, utilisateurs autorisés, règles du pare-feu).
- Connexion depuis un client Windows (`mstsc`) puis depuis un client Linux (**Remmina**), avec options d'affichage, de son et transfert de fichiers dans les deux sens.
- Activation du **serveur RDP de VirtualBox** pour accéder au bureau d'une VM Ubuntu.
- Difficultés traitées : pare-feu tiers (Avast), isolation des appareils par le partage de connexion mobile, identifiants du compte Microsoft.

### TP VNC / noVNC
- Serveur **TigerVNC** et bureau **XFCE** sur Ubuntu 26.04 (session Wayland), avec un utilisateur dédié `vncuser` sans droits sudo.
- Connexion avec **TigerVNC Viewer** (macOS), puis sécurisation par **tunnel SSH**, vérifiée dans le journal d'authentification.
- Accès depuis un **navigateur** avec **noVNC** et **Websockify**, également protégé par tunnel SSH.
- **Démarrage automatique** après redémarrage grâce à deux services `systemd`.
- Adaptations par rapport au sujet : display `:2` (port 5902), `xstartup` réécrit pour Wayland, options SSH (`PasswordAuthentication`, `AllowUsers`), installation de Websockify via `apt` (PEP 668).

## Environnement commun

- **Serveurs** : VM Ubuntu 26.04.1 LTS sous VirtualBox (SSH, VNC) ; PC Windows 11 Pro (RDP).
- **Clients** : MacBook sous macOS (Terminal, Safari/Chrome, TigerVNC Viewer) ; client Windows ; client Linux Remmina.
- **Réseau** : réseaux locaux 192.168.x.x, VM en accès par pont.

## Organisation du dépôt

```
services-reseaux-avances/
├── README.md
├── tp-ssh/
│   └── Rapport_TP_SSH.pdf
├── tp-rdp/
│   └── Rapport_TP_RDP_L3GLSI.pdf
└── tp-vnc-novnc/
    └── Rapport_TP_VNC_noVNC.pdf
```

## Note de sécurité

Ce dépôt ne contient aucun mot de passe, aucune clé privée ni fichier d'identifiants. Les adresses IP affichées sont des adresses privées d'un réseau de test. Les configurations d'authentification faible utilisées pour les tests (authentification RDP « Aucune », SSH par mot de passe, noVNC en HTTP) sont signalées dans les rapports et ne sont pas adaptées à un environnement de production.