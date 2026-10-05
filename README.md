# Pose Sténopé

Calculateur de temps de pose pour appareil photo sténopé, en une seule page HTML sans dépendance.
Ouvrez `index.html` dans un navigateur (ordinateur ou téléphone).

## Fonctions

- **Sténopé** : diamètre du trou et focale → ouverture (f/N), avec le diamètre optimal (critère de Rayleigh).
- **Lumière**, trois façons de la renseigner :
  - *Scène* : situations types (plein soleil IL 15, couvert IL 12, intérieur…) ;
  - *Posemètre* : ouverture et vitesse lues sur un posemètre ou une appli de téléphone ;
  - *IL manuel* : indice de lumination à ISO 100.
- **Compensation** en IL (contre-jour, filtre…).
- **Film** : sensibilité et correction de l'effet Schwarzschild (défaut de réciprocité)
  - Ilford / Kentmere : formule `t corrigé = t^p` ;
  - Kodak Tri-X, T-Max, Fomapan 100 : tableaux du fabricant, interpolés en échelle log ;
  - papier photo, numérique (sans correction), ou exposant `p` personnalisé.
- **Minuteur** avec bips sur les 5 dernières secondes, signal de fin, vibration et maintien de l'écran allumé.
- **Tableau** des poses pour toutes les situations types avec le réglage courant.

Les réglages sont mémorisés dans le navigateur.

## Formules

- `N = focale / diamètre`
- `t = N² / 2^(IL100 + log2(ISO/100) − compensation)`
- diamètre optimal : `d = 1,9 × √(focale × 0,00055 mm)`

## Appli Android

Le dossier `android/` contient une appli Android (Java, sans dépendance) qui affiche la même page
dans une WebView, hors ligne. Elle ajoute la vibration native en fin de pose et garde l'écran allumé
pendant le minuteur.

### Récupérer l'APK

Chaque push lance le workflow **Appli Android** (GitHub Actions) :

1. onglet *Actions* du dépôt → dernier run « Appli Android » ;
2. section *Artifacts* → télécharger `pose-stenope-apk` (un zip contenant `pose-stenope.apk`) ;
3. copier l'APK sur le téléphone et l'ouvrir (autoriser l'installation d'applis de source inconnue).

Un tag `v1.0`, `v1.1`… publie aussi l'APK dans une release GitHub.

### Construire en local

Avec Android Studio ou le SDK Android installé (JDK 17) :

```sh
cd android
./gradlew assembleRelease
# APK : android/app/build/outputs/apk/release/app-release.apk
```

### Signature

Sans configuration, l'APK est signé avec une clé de debug générée à chaque build : il s'installe,
mais une nouvelle version demandera de désinstaller la précédente. Pour des mises à jour directes,
créez une clé et ajoutez ces secrets au dépôt (*Settings → Secrets and variables → Actions*) :

```sh
keytool -genkeypair -v -keystore pose.jks -alias pose -keyalg RSA -keysize 2048 -validity 10000
base64 -w0 pose.jks   # valeur de POSE_KEYSTORE_BASE64
```

- `POSE_KEYSTORE_BASE64`, `POSE_KEYSTORE_PASSWORD`, `POSE_KEY_ALIAS`, `POSE_KEY_PASSWORD`
