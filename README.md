# LabSec19 – Analyse Android : Challenge Snake.apk



---

## Contexte

Ce laboratoire est consacré à l'analyse de l'application Android **Snake.apk** dans un environnement de test pédagogique.

L'objectif du challenge consiste à comprendre le fonctionnement interne de l'application, identifier les mécanismes de protection mis en œuvre et analyser le traitement permettant de générer le résultat final du challenge.

L'application embarque plusieurs couches de protection destinées à compliquer l'analyse, notamment des mécanismes de détection d'environnement ainsi qu'une logique native implémentée dans une bibliothèque partagée.

---

## Objectifs du Laboratoire

* Identifier les mécanismes de protection présents dans l'application.
* Étudier la structure de l'APK après décompilation.
* Analyser les composants Java et Smali.
* Examiner les bibliothèques natives embarquées.
* Comprendre le rôle du fichier YAML utilisé par l'application.
* Observer le comportement de l'application lors de son exécution.
* Valider les résultats obtenus pendant l'analyse.

---

## Environnement

| Élément           | Valeur                      |
| ----------------- | --------------------------- |
| Application       | Snake.apk                   |
| Plateforme        | Android Emulator            |
| Décompilation APK | Apktool                     |
| Analyse Smali     | Apktool                     |
| Analyse native    | Bibliothèque `libsnake.so`  |
| Journalisation    | Android Logcat              |
| Type de challenge | Reverse Engineering Android |

---

## Présentation de l'Application

L'application réalise plusieurs contrôles lors de son démarrage afin de vérifier son environnement d'exécution.

Par ailleurs, le résultat final du challenge n'est pas affiché directement dans l'interface graphique. Une partie importante de la logique applicative est exécutée dans une bibliothèque native.

---

## Décompilation de l'APK

L'analyse débute par une décompilation de l'application afin d'obtenir les fichiers Smali et les ressources internes.

### Décompilation avec Apktool

![Décompilation Apktool](screens/01_apktool_decompile.png)

Cette étape fournit une vue détaillée de la structure interne de l'application Android.

---

## Analyse des Mécanismes de Protection

L'étude des fichiers Smali permet d'identifier plusieurs routines de contrôle exécutées lors du lancement de l'application.

### Recherche des Contrôles

![Recherche des protections](screens/02_root_detection_search.png)

Les vérifications observées concernent principalement :

* l'environnement d'exécution ;
* certains indicateurs système ;
* des mécanismes destinés à limiter l'analyse dynamique.

L'inspection du code permet de localiser précisément les fonctions impliquées dans ces contrôles.

---

## Analyse de la Bibliothèque Native

L'application charge une bibliothèque native :

```text
libsnake.so
```

Cette bibliothèque contient plusieurs fonctions participant au fonctionnement du challenge.

L'étude de cette partie native permet de comprendre :

* le flux d'exécution principal ;
* les vérifications réalisées côté natif ;
* la génération du résultat final.

---

## Analyse du Fichier YAML

Une partie du comportement de l'application repose sur la lecture d'un fichier YAML externe.

### Exemple de Structure YAML

![Payload YAML](screens/03_yaml_payload.png)

L'analyse du code révèle que ce fichier est utilisé comme entrée pour certaines opérations internes de l'application.

Cette étape permet de comprendre les relations entre :

* les paramètres transmis à l'application ;
* le contenu du fichier YAML ;
* les traitements réalisés côté Java et natif.

---

## Préparation de l'Environnement de Test

L'application est installée sur l'émulateur Android de laboratoire.

### Installation de l'Application

![Installation APK](screens/04_install_patched_apk.png)

Les autorisations nécessaires au fonctionnement du challenge sont ensuite configurées.

### Configuration des Permissions

![Permission stockage](screens/05_grant_storage_permission.png)

---

## Validation des Ressources Utilisées

Les ressources attendues par l'application sont positionnées dans l'environnement Android.

### Déploiement du Fichier YAML

![Envoi du fichier YAML](screens/06_push_payload.png)

Cette étape permet à l'application d'accéder aux données utilisées pendant son exécution.

---

## Observation de l'Exécution

L'application est ensuite exécutée dans l'environnement de test.

Les journaux Android permettent d'observer :

* le comportement de l'application ;
* les messages générés pendant l'exécution ;
* les informations produites par la logique native.

### Journaux Applicatifs

![Flag dans Logcat](https://github.com/user-attachments/assets/144aa686-f330-4e50-9f83-2382e845e102)

L'analyse des logs constitue une étape importante pour comprendre le comportement global du challenge.

---

## Analyse des Résultats

| Élément analysé                | Résultat |
| ------------------------------ | -------- |
| Décompilation APK              | Réussie  |
| Analyse Smali                  | Réussie  |
| Identification des protections | Réussie  |
| Analyse native                 | Réussie  |
| Étude du YAML                  | Réussie  |
| Validation de l'environnement  | Réussie  |
| Observation via Logcat         | Réussie  |

---

## Résultats

Les objectifs du laboratoire ont été atteints :

* ✅ Analyse complète de l'application.
* ✅ Étude des protections applicatives.
* ✅ Analyse des composants Smali.
* ✅ Compréhension du rôle de la bibliothèque native.
* ✅ Analyse du traitement YAML.
* ✅ Observation du comportement de l'application.
* ✅ Validation des résultats obtenus dans le challenge.

---

## Enseignements du Laboratoire

Ce challenge illustre plusieurs concepts fréquemment rencontrés lors d'une analyse Android :

* protections contre l'analyse ;
* logique métier répartie entre Java et code natif ;
* utilisation de bibliothèques partagées ;
* exploitation de journaux applicatifs ;
* importance de l'analyse statique et dynamique combinées.

L'exercice montre également qu'une application peut répartir ses mécanismes de vérification entre plusieurs couches afin de compliquer le travail d'analyse.

---

## Conclusion

Ce laboratoire a permis d'étudier une application Android intégrant plusieurs mécanismes de protection et une logique native avancée.

L'approche combinant décompilation, analyse Smali, étude des bibliothèques natives et observation dynamique fournit une vision complète du fonctionnement interne de l'application.

Cette méthodologie complète les travaux réalisés dans les laboratoires précédents consacrés à l'analyse statique Android, au reverse engineering, à Frida, Drozer, Burp Suite, Objection et Medusa.

---

