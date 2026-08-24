# GestionCommerciale — Application de bureau

Ce dossier transforme votre logiciel (`app/index.html`) en une véritable application de bureau
installable, grâce à **Electron**. Vous pouvez générer :

- 🪟 **Windows** → `setup.exe` (installateur classique avec raccourci bureau)
- 🍎 **macOS** → `GestionCommerciale.dmg`
- 🐧 **Linux** → `GestionCommerciale.AppImage` et `.deb`

Vos données restent stockées **localement sur l'ordinateur de l'utilisateur** (IndexedDB), exactement
comme dans le navigateur — aucune donnée n'est envoyée sur internet.

---

## ✅ Testé et validé

Ce projet a déjà été testé : l'installation des dépendances et la génération de l'installateur
Linux (`.AppImage`) fonctionnent sans erreur. La structure est prête pour Windows et macOS.

---

## 🚀 Méthode recommandée : construire les 3 versions automatiquement (sans rien installer)

C'est la méthode la plus simple, car Windows ne peut construire que `setup.exe`, macOS que
`.dmg`, et Linux que `.AppImage`/`.deb` — il faut donc en principe un ordinateur de chaque
type. **GitHub Actions** résout ce problème : il construit les 3 versions pour vous, gratuitement,
dans le cloud.

1. Créez un compte gratuit sur [github.com](https://github.com) si vous n'en avez pas.
2. Créez un nouveau dépôt (repository), par exemple `gestion-commerciale-desktop`.
3. Envoyez (uploadez) tout le contenu de ce dossier dans le dépôt (glisser-déposer sur le site
   GitHub fonctionne très bien, ou utilisez `git push` si vous connaissez Git).
4. Allez dans l'onglet **Actions** du dépôt : la construction démarre automatiquement.
5. Une fois terminée (environ 5 à 10 minutes), ouvrez le run terminé puis la section
   **Artifacts** en bas de page : vous y trouverez `setup.exe`, le `.dmg` et l'`.AppImage`/`.deb`,
   prêts à télécharger et à distribuer.

Le fichier `.github/workflows/build.yml` est déjà configuré pour cela — vous n'avez rien à écrire.

---

## 🛠 Méthode alternative : construire localement

### Windows (produit `setup.exe`)
Nécessite un PC Windows avec [Node.js](https://nodejs.org) installé.
```
npm install
npm run dist:win
```
Le fichier `setup.exe` apparaît dans le dossier `dist/`.

### macOS (produit `.dmg`)
Nécessite un Mac avec Node.js installé.
```
npm install
npm run dist:mac
```

### Linux (produit `.AppImage` et `.deb`)
```
npm install
npm run dist:linux
```

> ⚠️ Construire un `.exe` Windows depuis Linux/Mac (ou l'inverse) sans outil supplémentaire
> (comme Wine) échoue généralement — c'est pourquoi la méthode GitHub Actions ci-dessus est
> recommandée : chaque plateforme construit sa propre version.

---

## 🧪 Tester l'application avant de construire l'installateur

```
npm install
npm start
```
Cela ouvre directement l'application dans une fenêtre de bureau, sans créer d'installateur.

---

## 📁 Structure du projet

```
gestion-commerciale-desktop/
├── app/
│   └── index.html        ← votre logiciel (identique à la version navigateur)
├── build/
│   └── icon.png           ← icône de l'application (modifiable, 1024x1024 recommandé)
├── .github/workflows/
│   └── build.yml           ← construction automatique multiplateforme (GitHub Actions)
├── main.js                 ← démarre la fenêtre de l'application
├── preload.js
├── package.json             ← configuration Electron / electron-builder
└── README.md                 ← ce fichier
```

## 🔄 Mettre à jour l'application plus tard

Remplacez simplement le fichier `app/index.html` par la nouvelle version de votre logiciel,
puis reconstruisez (`npm run dist:win`, ou repoussez sur GitHub pour une reconstruction
automatique). Comme les données sont stockées dans le navigateur intégré (IndexedDB) et non
dans l'application elle-même, **les données des utilisateurs ne sont jamais perdues lors d'une
mise à jour**, exactement comme documenté dans la section « Mises à jour » du logiciel.

## ✏️ Personnaliser l'icône

Remplacez `build/icon.png` par votre propre image carrée (1024×1024 pixels de préférence,
fond transparent ou uni). electron-builder génère automatiquement les formats `.ico`
(Windows) et `.icns` (macOS) à partir de ce fichier unique.

---
Développé par **Ingénieur SAMINOU Mahaman Chapiou** — SAM Tech Solutions
📧 samtechsolutions08@gmail.com · ☎ +227 96 30 87 54
