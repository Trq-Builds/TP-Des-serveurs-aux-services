# 📘 TP B1-S2 : Des serveurs aux services

---

Ce dépôt regroupe les réponses et analyses du TD portant sur l'infrastructure matérielle des serveurs et la logique des services réseaux. Il couvre l'étude des facteurs de forme (Tour, Rack, Lame), la redondance matérielle, ainsi que la chaîne de services nécessaire à l'authentification d'un poste client sur un domaine.

---

## `📑`︲Sommaire (cliquez pour accéder directement à la section souhaitée)

1. [`📘`︲Activité #1 : Découverte des configurations matérielles.](#-activité-1--découverte-des-configurations-matérielles)
   * [`📐`︲Facteurs de forme (Tour, Rack, Lame) et Sockets.](#-facteurs-de-forme-des-serveurs-tour-rack-lame)
   * [`🔧`︲Précisions Techniques (Q2 à Q5).](#-précisions-techniques-q2-à-q5)
   * [`🧩`︲Architecture Serveur Lame et Châssis.](#-lecosystème-du-serveur-lame-q6)
   * [`📊`︲Tableau comparatif des serveurs Dell PowerEdge.](#-fiche-récapitulative-des-serveurs-q7)
   * [`🛡️`︲Stratégies de Redondance.](#-stratégies-de-redondance-q8)

   ---

2. [`🌐`︲Activité #2 : Chaîne de services et connexion client.](#-activité-2--chaîne-de-services-lors-de-la-connexion-dun-poste-client)
   * [`🔍`︲Identification des protocoles (DHCP, DNS, AD).](#-identification-des-services-essentiels-1-à-3)
   * [`🔄`︲Schématisation du flux d'authentification.](#-ordre-chronologique-dappel-des-services)
   * [`📂`︲Services complémentaires en réseau local.](#-services-réseaux-complémentaires-post-authentification)

---

<a id="-activité-1--découverte-des-configurations-matérielles"></a>
## `📘`︲Activité #1 : Découverte des configurations matérielles.

---

<a id="-facteurs-de-forme-des-serveurs-tour-rack-lame"></a>
## `📐`︲Facteurs de forme des serveurs (Tour, Rack, Lame)

Dans une infrastructure serveur, le **facteur de forme** définit le **format physique**, le **mode d’intégration** et les **cas d’usage** du matériel. 
À partir des annexes fournies, on distingue **trois formats majeurs** :

### `🖥️`︲Serveur **Tour (Tower)**
Le serveur **Tour** reprend une conception proche d’un PC de bureau, tout en intégrant des composants **professionnels** (CPU serveur, RAM ECC, stockage renforcé).
* 📦 Format autonome, non monté en baie
* 🔧 Installation simple, sans infrastructure dédiée
* 🎯 Adapté aux **TPE / PME** ou environnements à faible densité
📌 *Exemples : Annexes 1 et 2*

### `🗄️`︲Serveur **Rack**
Le serveur **Rack** est conçu pour être installé horizontalement dans une **baie informatique standardisée (19")**.
* 📏 Hauteur exprimée en **Unités de Rack (U)**
* 🔥 Densité élevée et refroidissement optimisé
* 🧠 Centralisation et maintenance facilitées
📌 *Exemple : Annexe 3*

### `🧩`︲Serveur **Lame (Blade)**
Le serveur **Lame** est un module compact inséré dans un **châssis commun**, qui mutualise les ressources critiques.
* ⚡ Alimentation partagée
* ❄️ Refroidissement centralisé
* 🌐 Connectivité réseau intégrée
* 📈 Très forte densité de calcul
📌 *Exemple : Annexe 4*



---

### `✅`︲Synthèse rapide

| Facteur de forme | Usage principal          | Infrastructure requise |
| ---------------- | ------------------------ | ---------------------- |
| **Tour** | Petites structures       | Aucune                 |
| **Rack** | Datacenters / PME        | Baie informatique      |
| **Lame** | Environnements critiques | Châssis dédié          |

---

<a id="-précisions-techniques-q2-à-q5"></a>
### 🔧 Précisions Techniques (Q2 à Q5)

* **Le Socket (Q2) :** Il s'agit de l'emplacement physique sur la carte mère destiné à accueillir un processeur (CPU). Le nombre de sockets détermine la capacité d'évolution du serveur : un serveur "2 sockets" peut fonctionner avec un seul CPU au départ, puis en recevoir un deuxième plus tard pour doubler sa puissance de calcul.
* **Particularité de l'alimentation (Q3) :** Contrairement à un PC client, un serveur dispose d'une **alimentation redondante** (deux blocs ou plus). Ces blocs sont **extractibles à chaud (Hot-Plug)**, permettant de remplacer une alimentation défectueuse sans éteindre le serveur.
* **Stockage des serveurs Rack (Q4) :** Pour installer des serveurs au format Rack, on utilise une **baie informatique (ou armoire 19 pouces)**. Elle permet de centraliser le matériel, d'optimiser le câblage et de garantir un flux d'air de refroidissement efficace.
* **Signification du format 1U (Q5) :** Le "U" signifie **Unité de rack**. C'est une unité de mesure standardisée pour la hauteur des équipements. **1U = 1,75 pouce (soit environ 4,445 cm)**.

---

<a id="-lecosystème-du-serveur-lame-q6"></a>
### `🧩` L'écosystème du Serveur Lame (Q6)

Le serveur Dell PowerEdge M830 (Annexe 4) est une "lame" qui ne peut pas fonctionner seule. Elle doit être insérée dans un **châssis**.

* **Rôle du Châssis (Q6.a) :** Le châssis fait office de "colonne vertébrale". Il mutualise les ressources pour toutes les lames qu'il héberge :
    * **Énergie :** Alimentations partagées de forte puissance.
    * **Refroidissement :** Ventilation commune pour tout le châssis.
    * **Connectivité :** Switches réseau et stockage intégrés à l'arrière du châssis.
    * **Gestion :** Interface d'administration centralisée pour toutes les lames.
* **Nombre d'alimentations (Q6.b) :** Sur ce type d'équipement (comme le châssis Dell PowerEdge M1000e), on trouve généralement jusqu'à **6 blocs d'alimentation** haute efficacité pour garantir une redondance totale.

---

<a id="-fiche-récapitulative-des-serveurs-q7"></a>
### `📊` Fiche récapitulative des serveurs (Q7)

| Caractéristique | Annexe 1 : T140 | Annexe 2 : T440 | Annexe 3 : R240 | Annexe 4 : M830 |
| :--- | :--- | :--- | :--- | :--- |
| **Facteur de forme** | Tour | Tour | Rack (1U) | Lame (Blade) |
| **Nb. Processeurs (max)** | 1 | 2 | 1 | 4 |
| **Mémoire (max)** | 64 Go | 1 To | 64 Go | 3 To |
| **Slots RAM** | 4 slots | 16 slots | 4 slots | 48 slots |
| **Baies de stockage** | 4 baies (3.5") | 4, 8 ou 12 baies | 4 baies (3.5") | Jusqu'à 12 baies |
| **Nb. Alimentations** | 1 (365W) | 2 (Redondantes) | 2 (Redondantes) | Via Châssis (Redon.) |

---

<a id="-stratégies-de-redondance-q8"></a>
### `🛡️` Stratégies de Redondance (Q8)

La redondance est la capacité d'un système à continuer de fonctionner malgré la défaillance d'un ou plusieurs de ses composants.

* **Alimentation :** Utilisation de deux blocs (ou plus) pour garantir la disponibilité électrique continue.
* **Disques durs (Stockage) :** Mise en place du **RAID** (ex: RAID 1, 5 ou 10). Les données sont dupliquées pour rester accessibles si un disque meurt.
* **Processeur (CPU) :** Répartition de la charge sur plusieurs processeurs physiques.
* **Mémoire (RAM) :** Utilisation de barrettes **ECC** (Error Correcting Code) qui corrigent les erreurs de données à la volée.
* **Ventilation :** Présence de ventilateurs extractibles à chaud pour maintenir le refroidissement en cas de panne de l'un d'eux.

---

<a id="-activité-2--chaîne-de-services-lors-de-la-connexion-dun-poste-client"></a>
## `🌐`︲Activité #2  Chaîne de services lors de la connexion d’un poste client

Cette activité vise à identifier et comprendre la **chaîne de services réseau** sollicitée lorsqu’un poste client démarre et qu’un utilisateur s’authentifie sur un **domaine Windows**.

---

<a id="-identification-des-services-essentiels-1-à-3"></a>
## `🔍`︲Identification des services essentiels (1 à 3)

### `1️⃣`︲DHCP  Attribution de l’identité réseau
📌 **Service :** DHCP *(Dynamic Host Configuration Protocol)*
📡 **Protocole :** UDP  Ports **67 (serveur)** / **68 (client)**
🔧 **Rôle technique :** Attribution automatique d’une adresse IP, masque, passerelle et serveur DNS.
> [!NOTE]
> **Sans DHCP** : Le poste n’existe pas sur le réseau. Aucun échange possible.

---

<a id="-ordre-chronologique-dappel-des-services"></a>
### `2️⃣`︲DNS  Localisation du domaine
📌 **Service :** DNS *(Domain Name System)*
📡 **Protocole :** UDP / TCP  Port **53**
🔧 **Rôle technique :** Traduction du nom de domaine (`DESCARTESBLEU`) vers l’adresse IP du contrôleur de domaine.
> [!NOTE]
> **Sans DNS** : Le poste ne sait pas **où se trouve le domaine**. L’authentification ne peut pas démarrer.

---

### `3️⃣`︲Active Directory  Authentification de l’utilisateur
📌 **Service :** Active Directory
📡 **Protocoles associés :** LDAP (389) / Kerberos (88)
🔧 **Rôle technique :** Vérification du couple utilisateur / mot de passe et attribution des droits.
> [!NOTE]
> **Sans Active Directory** : Pas d’authentification centralisée ni de gestion des droits.

---

## `🔄`︲Ordre chronologique d’appel des services



```mermaid
graph TD
    Client[Poste Client]
    
    subgraph "Chaîne de Services"
    Step1(1. DHCP) -->|Attribution IP| Client
    Client -->|2. Requête: Où est DESCARTESBLEU ?| Step2(2. DNS)
    Step2 -->|Réponse: IP du Contrôleur| Client
    Client -->|3. Envoi identifiants| Step3(3. Active Directory)
    Step3 -->|Validation & Ouverture Session| Client
    end
    
    style Step1 fill:#f9f,stroke:#333,stroke-width:2px
    style Step2 fill:#bbf,stroke:#333,stroke-width:2px
    style Step3 fill:#bfb,stroke:#333,stroke-width:2px

```

---

<a id="-services-réseaux-complémentaires-post-authentification"></a>
## `📂`︲Services réseaux complémentaires (post-authentification)

Une fois l’utilisateur connecté, d’autres services entrent en jeu dans un environnement LAN :

* 📁 **Serveur de fichiers (SMB/CIFS)**  Port **445**
* 🖨️ **Serveur d’impression**
* ⏱️ **Serveur de temps (NTP)**  Port **123**
* 🌐 **Proxy / filtrage web**
* 🚀 **Service de déploiement** *(WDS / FOG)*

> [!TIP]
> La connexion à un domaine repose sur une **chaîne de dépendances**.
> **DHCP → DNS → Active Directory**
> Un maillon cassé = **connexion impossible**.

---
