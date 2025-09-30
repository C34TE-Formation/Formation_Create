Fichier de Formation Interne : Produits d'Éclairage et Programmation (DMX/Art-Net)
Table des Matières
Les Fondamentaux du Contrôle Lumière

1.1. DMX (Le Langage de la Fixture)

1.2. Art-Net (Le Transport Réseau)

Architecture de Notre Installation

2.1. Nos Produit : Fixtures LED

2.2. Le Node Art-Net : Passerelle et Distribution (Univers)

2.3. Le Câble Chogorie : Un Seul Câble (Power + Data)

Mise en Œuvre Physique (Pré-Resolume)

3.1. Adressage DMX avec le Writer (Détails et Modes)

3.2. Configuration IP de la Node

Programmation et Contrôle dans RESOLUME

4.1. Configuration Art-Net dans Resolume (Workflow Logiciel)

4.2. Fixture Map et Mapping Vidéo (Accès et Configuration)

4.3. Contrôle final

1. Les Fondamentaux du Contrôle Lumière
Ce chapitre couvre les deux protocoles que nous utilisons.

1.1. DMX (Le Langage de la Fixture)
Rôle : Le protocole et le seul langage que nos produits d'éclairage comprennent nativement.

Structure : Un Univers DMX est composé de 512 channels.

Contrôle : Chaque channel, réglé de 0→255, détermine un paramètre (ex: Intensité, Couleur).

1.2. Art-Net (Le Transport Réseau)
Rôle : Protocole permettant de transporter les données DMX via un réseau Ethernet standard (IP).

Concept : Art-Net = DMX dans un network.

Avantage : Permet d'acheminer des commandes sur de longues distances et de gérer un très grand nombre d'univers depuis un seul PC (où Resolume est installé).

Composant Clé : Le Node Art-Net est l'interface qui reçoit le signal Art-Net (réseau) pour le retranscrire en DMX (physique).

2. Architecture de Notre Installation
Ce chapitre relie la théorie à notre équipement spécifique.

2.1. Nos Produit 
Nature : Nos tubes LED sont des appareils DMX.

Exigences Fondamentales : Pour fonctionner, chaque tube nécessite deux éléments :

Un signal DMX (les commandes de couleur, etc.).

Une Alimentation Électrique (Power).

Configuration : Ils ont besoin d’etre adressé.

2.2. Le Node Art-Net : Passerelle et Distribution (Univers)
Double Fonction du Node :

Il agit comme Passerelle Art-Net : il reçoit les données de notre logiciel (via Ethernet).

Il agit comme Source DMX/Power : il convertit ces données en signal DMX physique et merge le power.

Distribution Des Univers : Chaque port de sortie Chogorie sur la Node Art-Net est un Univers DMX indépendant.

Par exemple : Le port 1 = Univers 1, le port 2 = Univers 2, etc.

Cette structure est essentielle pour le patching dans Resolume.

2.3. Le Câble Chogorie : Un Seul Câble (Power + Data) 
Notre Spécificité : Notre Node est conçu pour injecter l'Alimentation (Power) et le Signal DMX (Data) dans un SEUL câble de sortie vers nos tubes LED : le câble chogorie.

Bénéfice Pratique : L'installation est considérablement simplifiée sur le terrain. Un seul câble chogorie suffit pour alimenter le tube et le contrôler.

3. Mise en Œuvre Physique (Pré-Resolume)
Ce chapitre couvre les étapes obligatoires avant d'ouvrir le logiciel de contrôle.

3.1. Adressage DMX avec le Writer (Détails et Modes)
Principe Opérationnel :

En entrepôt (In) : Nos tubes sont pré-adressés et taggés (étiquettes avec code de couleur/adresse DMX). Une chart (tableau de référence) est disponible.

Sur le terrain (Live) : L'adressage n'est donc pas nécessaire en théorie, sauf en cas de remplacement d'un tube défectueux ou d'une erreur d’écriture.

Au retour (Out) : Il est OBLIGATOIRE de vérifier et de re-tagger/re-adresser chaque tube qui a été readresser sur le terrain avant l'entreposage pour garantir la qualité des opérations futures.

Outil : Nous utilisons le DMX Writer (ou Writer) pour attribuer l'adresse DMX à chaque tube et pour valider son fonctionnement.

Modes Clés : Deux modes sont essentiels pour nos produits :

DMX Adress (Mode Adressage) : Pour écrire l'adresse.

Color Test (Mode Test Couleur) : Pour vérifier.

Processus d'Adressage (Mode DMX Adress) :

IC Type : Entrez toujours CD pour les tubes (Type de puce spécifique à nos produits).

Adress Auto Offset : Détermine les channels DMX utilisés.

3 pour nos produits RGB (ex: les tubes).

4 pour nos produits RGBW.

DMX Start Adress : Entrez l'adresse de départ DMX souhaitée (selon votre chart de patching).

Validation : Appuyez sur OK and Apply pour valider et écrire l'adresse dans le tube.

Extra : Un Channel Tester est disponible pour vérifier la réponse d'un channel spécifique.

Mode Color Test :

Permet de forcer des modes de couleur prédéfinis (R, RGB, RGBW, etc.) pour confirmer rapidement que le tube est alimenté et répond correctement.

Règle : Chaque tube contrôlé de manière indépendante doit posséder une adresse de départ unique dans l'Univers DMX.

3.2. Configuration IP de la Node
Rôle de l'IP : L'adresse IP est l'identifiant unique de la Node sur le réseau.

Objectif : Resolume doit savoir à quelle IP envoyer le bon Univers DMX (Art-Net).

Action : Vérifier l'adresse IP de la Node (ex: 192.168.1.XXX) via l’écran de la node.

4. Programmation et Contrôle dans RESOLUME
Ce chapitre relie la configuration physique (Chapitre 3) à l'environnement logiciel.

4.1. Configuration Art-Net dans Resolume (Workflow Logiciel)
Étape 1 : Connexion Réseau (Préférences) :

Allez dans Preferences (Préférences) → DMX.

Sous DMX Output Device (Périphérique de Sortie DMX), sélectionnez l'interface réseau (carte Ethernet) qui est connectée directement à votre Node Art-Net. Cela établit le canal de communication.

Étape 2 : Lier l'Univers (Advanced Output) :

L'assignation de l'Univers Art-Net spécifique se fait dans la fenêtre d'Advanced Output.

Dans l'onglet DMX Fixture Map, vous devez lier chaque Univers (Subnet/Universe) utilisé à l'Univers physique de la Node (voir 2.2).

Adresse Cible : Resolume enverra automatiquement les données DMX de cet Univers à l'Adresse IP du Node configurée sur ce réseau.

4.2. Fixture Map et Mapping Vidéo (Accès et Configuration)
Accès à la Configuration : Dans Resolume, allez dans le menu Output (Sortie) puis sélectionnez Advanced (Avancé). Cela ouvrira la fenêtre d'Advanced Output.

Le Patching DMX s'effectue dans l'onglet DMX Fixture Map de cette fenêtre.

Le Fixture Map (Patching) :

Ajouter la Fixture (votre tube) avec son profil (nombre de channels).

Lui assigner l'Adresse DMX (Start Address et Univers) configurée avec le Writer et la Node.

Positionnement : Positionner virtuellement la Fixture (le tube) dans l'espace 2D de la fenêtre de sortie (Output) pour créer le Mapping.

But du Mapping : Cette disposition 2D permet à Resolume de savoir quelle couleur ou pixel de la vidéo attribuer à quel tube physique.

4.3. Contrôle final
Principe : Les Layers et les clips de Resolume (vidéos, couleurs, effets) envoient leurs informations pixel par pixel au Fixture Map.

Flux de Commande : Clip Vidéo → Fixture Map → Sortie Art-Net → IP du Node → Tube LED.

Vérification : Tester une source de couleur simple (un clip de couleur pleine) et confirmer que le tube correspondant s'allume avec la couleur attendue.
