# Nettoyeur — appli de nettoyage Android

Android 11 ou plus récent. Écrit en Kotlin + Jetpack Compose.

## Ce que fait l'appli

**Onglet Caches** : liste les applis triées par taille de cache. Un appui ouvre la fiche de l'appli dans les paramètres (Stockage › Vider le cache). Bouton vers le gestionnaire de stockage d'Android.

**Onglet Fichiers** : analyse tout le stockage et propose, cases à cocher :
- fichiers temporaires (miniatures `.thumbnails`, `.log`, `.tmp`, téléchargements partiels, `LOST.DIR`) — cochés par défaut ;
- dossiers vides — cochés par défaut ;
- doublons (comparaison par empreinte MD5) — toutes les copies cochées sauf la plus ancienne ;
- fichiers APK — non cochés ;
- gros fichiers de 50 Mo et plus — non cochés.
Une confirmation est toujours demandée avant suppression.

**Onglet Applis** : désinstaller tes applis ; pour les applis préinstallées, accès direct au bouton « Désactiver ».

## Obtenir l'APK

### Option A — Android Studio
1. Ouvrir le dossier `Nettoyeur` dans Android Studio.
2. Attendre la synchronisation Gradle.
3. Menu **Build › Build App Bundle(s) / APK(s) › Build APK(s)**.
4. L'APK est dans `app/build/outputs/apk/debug/app-debug.apk`.

### Option B — GitHub (sans rien installer)
1. Créer un dépôt GitHub et y envoyer tout le contenu du dossier (y compris `.github`).
2. Onglet **Actions** : la compilation démarre seule (environ 5 min).
3. Télécharger l'artefact **Nettoyeur-apk** (un zip contenant l'APK).

## Installer sur le téléphone
1. Copier l'APK sur le téléphone et l'ouvrir.
2. Autoriser l'installation d'applis inconnues pour l'appli qui ouvre le fichier.
3. Au premier lancement, accorder :
   - **Accès à tous les fichiers** (onglet Fichiers) ;
   - **Accès aux données d'utilisation** (onglets Caches et Applis).

## Limites imposées par Android (sans root)
- Une appli ne peut pas vider le cache des autres depuis Android 11 : il faut passer par la fiche de chaque appli.
- `Android/data` et `Android/obb` sont inaccessibles.
- Les applis système ne peuvent qu'être désactivées. Pour les désinstaller vraiment, il faut un PC et ADB :
  `adb shell pm uninstall --user 0 nom.du.paquet` (réversible avec `adb shell cmd package install-existing nom.du.paquet`).
