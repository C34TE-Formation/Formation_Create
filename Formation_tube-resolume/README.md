# Fichier de Formation Interne : Tube et Resolume

## Table des Matières
- [1. Les Fondamentaux du Contrôle Lumière](#1-les-fondamentaux-du-contrôle-lumière)  
  - [1.1. DMX (Le Langage de la Fixture)](#11-dmx-le-langage-de-la-fixture)  
  - [1.2. Art-Net (Le Transport Réseau)](#12-art-net-le-transport-réseau)  
- [2. Architecture de Notre Installation](#2-architecture-de-notre-installation)  
  - [2.1. Nos Produit : Fixtures LED](#21-nos-produit--fixtures-led)  
  - [2.2. Le Node Art-Net : Passerelle et Distribution (Univers)](#22-le-node-art-net--passerelle-et-distribution-univers)  
  - [2.3. Le Câble Chogorie : Un Seul Câble (Power--Data)](#23-le-câble-chogorie--un-seul-câble-power--data)  
- [3. Mise en Œuvre Physique (Pré-Resolume)](#3-mise-en-œuvre-physique-pré-resolume)  
  - [3.1. Adressage DMX avec le Writer (Détails et Modes)](#31-adressage-dmx-avec-le-writer-détails-et-modes)  
  - [3.2. Configuration IP de la Node](#32-configuration-ip-de-la-node)  
- [4. Programmation et Contrôle dans RESOLUME](#4-programmation-et-contrôle-dans-resolume)  
  - [4.1. Configuration Art-Net dans Resolume (Workflow Logiciel)](#41-configuration-art-net-dans-resolume-workflow-logiciel)  
  - [4.2. Fixture Map et Mapping Vidéo (Accès et Configuration)](#42-fixture-map-et-mapping-vidéo-accès-et-configuration)  
  - [4.3. Contrôle final](#43-contrôle-final)  

---

## 1. Les Fondamentaux du Contrôle Lumière
Ce chapitre couvre les deux protocoles que nous utilisons.

### 1.1. DMX (Le Langage de la Fixture)
- **Rôle** : Le protocole et le seul langage que nos produits d'éclairage comprennent nativement.  
- **Structure** : Un Univers DMX est composé de **512 channels**.  
- **Contrôle** : Chaque channel, réglé de `0 → 255`, détermine un paramètre (ex: Intensité, Couleur).  

### 1.2. Art-Net (Le Transport Réseau)
- **Rôle** : Protocole permettant de transporter les données DMX via un réseau Ethernet standard (IP).  
- **Concept** : *Art-Net = DMX dans un network.*  
- **Avantage** : Permet d'acheminer des commandes sur de longues distances et de gérer un très grand nombre d'univers depuis un seul PC (où Resolume est installé).  
- **Composant Clé** : Le **Node Art-Net** est l'interface qui reçoit le signal Art-Net (réseau) pour le retranscrire en DMX (physique).  

---

## 2. Architecture de Notre Installation
Ce chapitre relie la théorie à notre équipement spécifique.

### 2.1. Nos Produit : Fixtures LED
- **Nature** : Nos tubes LED sont des appareils DMX.  
- **Exigences Fondamentales** : Chaque tube nécessite deux éléments :  
  - Un **signal DMX** (les commandes de couleur, etc.)  
  - Une **alimentation électrique (Power)**  
- **Configuration** : Chaque fixture doit être **adressée**.  

### 2.2. Le Node Art-Net : Passerelle et Distribution (Univers)
- **Double Fonction du Node** :  
  1. Passerelle Art-Net : reçoit les données du logiciel (via Ethernet).  
  2. Source DMX/Power : convertit ces données en signal DMX physique et merge le power.  

- **Distribution Des Univers** :  
  Chaque port de sortie Chogorie de la Node Art-Net correspond à un **Univers DMX indépendant**.  
  - Port 1 = Univers 1  
  - Port 2 = Univers 2, etc.  

➡️ Cette structure est essentielle pour le patching dans Resolume.  

### 2.3. Le Câble Chogorie : Un Seul Câble (Power + Data)
- **Spécificité** : Notre Node injecte **Power + DMX** dans un seul câble → le câble **Chogorie**.  
- **Bénéfice** : Simplifie énormément l’installation → **un seul câble par tube LED**.  

---

## 3. Mise en Œuvre Physique (Pré-Resolume)
Ce chapitre couvre les étapes obligatoires avant d'ouvrir le logiciel de contrôle.

### 3.1. Adressage DMX avec le Writer (Détails et Modes)
**Principe Opérationnel** :  
- **En entrepôt (In)** : Tubes pré-adressés et taggés (étiquettes avec code/adresse DMX).  
- **Sur le terrain (Live)** : Adressage non nécessaire sauf remplacement.  
- **Au retour (Out)** : Vérification/re-tag/re-adressage OBLIGATOIRE pour standardiser l’inventaire.  

**Outil** : Le **DMX Writer** sert à :  
- Écrire l’adresse DMX.  
- Valider le fonctionnement.  

**Modes Clés** :  
- **DMX Adress (Mode Adressage)** :  
  - *IC Type* : toujours `CD` (tubes LED).  
  - *Adress Auto Offset* :  
    - 3 pour produits RGB.  
    - 4 pour produits RGBW.  
  - *DMX Start Address* : adresse de départ DMX (selon chart patching).  
  - *Validation* : `OK and Apply`.  

- **Color Test (Mode Test Couleur)** :  
  - Permet de forcer des couleurs prédéfinies (R, RGB, RGBW).  
  - Vérifie alimentation et bonne réponse.  

⚠️ **Règle** : Chaque tube = une **adresse de départ unique** dans l’Univers DMX.  

### 3.2. Configuration IP de la Node
- **Rôle** : L’adresse IP identifie la Node sur le réseau.  
- **Objectif** : Resolume doit savoir à quelle IP envoyer l’Univers DMX (Art-Net).  
- **Action** : Vérifier l’IP (ex: `192.168.1.XXX`) via l’écran de la Node.  

---

## 4. Programmation et Contrôle dans RESOLUME

### 4.1. Configuration Art-Net dans Resolume (Workflow Logiciel)
1. **Connexion Réseau (Préférences)**  
   - Menu `Preferences → DMX`  
   - Sélectionner l’interface réseau reliée à la Node.  
2. **Lier l’Univers (Advanced Output)**  
   - Dans `Advanced Output → DMX Fixture Map`, assigner chaque Univers Art-Net aux Univers physiques de la Node.  
   - Resolume envoie les données à l’**IP de la Node**.  

### 4.2. Fixture Map et Mapping Vidéo (Accès et Configuration)
- **Accès** : `Output → Advanced` → ouvre la fenêtre Advanced Output.  
- **Patching** :  
  - Ajouter la Fixture (profil = nb de channels).  
  - Assigner l’Adresse DMX (Start Address + Univers).  
  - Positionner la Fixture dans l’espace 2D de sortie.  

➡️ Le **Mapping vidéo → fixture** permet d’envoyer les pixels vidéo aux bons tubes.  

### 4.3. Contrôle final
- **Flux** : Clip Resolume → Fixture Map → Art-Net → Node IP → Tube LED.  
- **Test** : Lancer un clip couleur unie → vérifier la correspondance.  

---
