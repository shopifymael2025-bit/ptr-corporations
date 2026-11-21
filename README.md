# PTR Corporations

Dashboard de jeux pour **Windows et macOS** (Electron) : scan de Steam, Epic Games et des apps installées, jaquettes via SteamGridDB, temps de jeu, jeu le plus joué, interface EN/FR.

Game library dashboard for **Windows and macOS** (Electron): Steam, Epic Games and installed-app scan, SteamGridDB covers, playtime tracking, most-played game, EN/FR interface.

Site : `https://shopifymael2025-bit.github.io/ptr-corporations/`

## Installation (développement)

```bash
npm install
npm start
```

Prérequis : Node.js 18+, Windows 10/11 ou macOS 12+.

## Build

```bash
npm run build-win    # Windows : installateur .exe
npm run build-mac    # macOS : .dmg (à lancer sur un Mac)
```

Les fichiers sont créés dans `dist/`.

## Publier une version (automatique)

```bash
git tag v1.0.0
git push --tags
```

GitHub Actions (`.github/workflows/release.yml`) compile Windows et macOS et ajoute les fichiers dans **Releases**. Le site et la page « Informations » de l'app lisent cette dernière release.

## Site (GitHub Pages)

Le dossier `docs/` est le site. Dans le dépôt : **Settings → Pages → Deploy from a branch → `main` / `/docs`**.
Remplace `shopifymael2025-bit/ptr-corporations` dans `docs/index.html` (constante `REPO`), `package.json` (`repository`, `updateUrl`) et ce README.

## Structure

```
main.js        processus principal (fenêtre, scan Windows/macOS, temps de jeu, IPC)
preload.js     pont sécurisé vers l'interface
renderer/      index.html, style.css, app.js
assets/        icon.ico (Windows), icon.png (macOS)
docs/          site GitHub Pages
```

## Ce qui est scanné

- **Windows** : bibliothèques Steam (tous les disques, via `libraryfolders.vdf`), Epic Games, raccourcis du menu Démarrer.
- **macOS** : `/Applications`, `~/Applications`, Steam.

## Configuration

- **Clé API SteamGridDB** : gratuite sur https://www.steamgriddb.com/api/v2, à coller dans Paramètres. Elle est enregistrée sur ta machine (`%APPDATA%/galaxy-dashboard` sur Windows), jamais dans le dépôt.
- **Mises à jour** : `updateUrl` dans `package.json` pointe vers l'API des releases GitHub.
