# Rapport de Lab 10 : Guide d'installation de Frida

## Description
Ce rapport documente la mise en place d'un environnement d'analyse dynamique sur Android. L'objectif est d'utiliser **Frida** pour inspecter les composants système, intercepter des fonctions natives et analyser les interactions Java au sein d'une application mobile.

---

## 1. Préparation de l'Environnement

### 1.1. Installation du Client Frida
Vérification de l'installation de Frida et des outils associés sur la machine hôte.
*   **Commande :** `frida --version`

![Version de Frida](Lab%20frida/frida_version.png)

### 1.2. Configuration d'ADB (Android Debug Bridge)
Vérification de la version d'ADB et de la détection de l'appareil (émulateur).

![Version ADB et devices](Lab%20frida/adb%20version.png)

---

## 2. Déploiement sur l'Appareil Android

### 2.1. Transfert du Serveur et Permissions
Le binaire `frida-server` est poussé sur l'appareil dans un répertoire temporaire et les droits d'exécution sont attribués.

![Transfert et chmod](Lab%20frida/adb_push_chmod.png)

### 2.2. Lancement du Serveur Frida
Accès au shell Android pour exécuter le serveur en arrière-plan.

![Lancement du serveur via shell](Lab%20frida/adb_shell.png)

---

## 3. Tests d'Injection et Instrumentation

### 3.1. Validation de l'Injection (Script Hello)
Injection d'un script de test `hello.js` dans le processus cible pour confirmer que l'instrumentation fonctionne sur Android 15.

![Injection hello.js](Lab%20frida/hello%20js.png)

### 3.2. Analyse de l'Architecture
Identification de l'architecture du processus (`x64`) et localisation du module principal `app_process64`.

![Architecture et MainModule](Lab%20frida/process_arch.png)

---

## 4. Analyse Avancée des Modules et Mémoire

### 4.1. Énumération des Modules
Liste des bibliothèques chargées en mémoire pour comprendre les dépendances de l'application.

![Liste des modules](Lab%20frida/enumerate_modules.png)

### 4.2. Recherche de Bibliothèques SSL/Crypto
Identification des bibliothèques liées au chiffrement (`libssl`, `libcrypto`) pour cibler l'analyse des flux sécurisés.

![Modules SSL et Crypto](Lab%20frida/available_ssl.png)

### 4.3. Inspection de la Mémoire (Plages R-X)
Examen des zones mémoire ayant des permissions de lecture et d'exécution.

![Plages mémoire exécutables](Lab%20frida/enumerate_range.png)

---

## 5. Conclusion du Laboratoire
Ce laboratoire a permis de valider la chaîne complète d'analyse dynamique :
1.  Installation et configuration des outils.
2.  Déploiement du serveur sur la cible.
3.  Analyse des structures de bas niveau (mémoire, modules, crypto).

Ces compétences sont essentielles pour les prochaines étapes : le contournement de mécanismes de sécurité (Root detection, SSL Pinning).
