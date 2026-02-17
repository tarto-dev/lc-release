# lc-release

Script shell permettant de générer des **release notes structurées** à
partir d'un diff Git entre deux refs (branches ou tags).

Il transforme un `git log` brut en sortie propre, triée et exploitable
pour des changelogs, Merge Requests ou livraisons.

------------------------------------------------------------------------

## 🎯 Objectif

`lc-release` permet de :

-   Lister les commits entre deux refs Git
-   Ignorer les merges
-   Trier les commits par type (`feat`, `fix`, `refactor`, etc.)
-   Extraire automatiquement les tickets (`#123`, `ABC-123`, etc.)
-   Afficher l'auteur au format `@username`
-   Générer des liens GitLab cliquables (OSC8) ou Markdown
-   Produire une sortie prête à copier dans une release note

------------------------------------------------------------------------

## ⚙️ Prérequis

Le script nécessite :

-   `git`
-   `awk`
-   `sort`
-   `sed`
-   `grep`
-   `tr`

Sur macOS ou Linux standard, ces outils sont disponibles par défaut.

------------------------------------------------------------------------

## 🚀 Installation

### Option 1 --- Fonction shell

Ajoute le contenu de `lc-release.sh` dans ton `~/.zshrc` ou `~/.bashrc`,
puis :

``` bash
source ~/.zshrc
```

### Option 2 --- Commande globale

``` bash
curl -fsSL https://raw.githubusercontent.com/tarto-dev/lc-release/master/lc-release.sh -o ~/.local/bin/lc-release
chmod +x ~/.local/bin/lc-release
```

------------------------------------------------------------------------

## 🧠 Usage

### 1 argument

``` bash
lc-release develop
```

Calcule automatiquement :

    origin/main..develop

(si `origin/main` existe, sinon `origin/master`)

------------------------------------------------------------------------

### 2 arguments

``` bash
lc-release develop origin/release
```

Calcule :

    develop..origin/release

Interprétation : commits présents dans `develop` mais pas dans
`origin/release`.

------------------------------------------------------------------------

## 🔧 Variables d'environnement

### Mode de liens

``` bash
LC_RELEASE_LINK_MODE=md lc-release develop
```

Valeurs possibles : - `osc8` (liens cliquables terminal) - `md` (liens
Markdown) - `off` (désactivé)

------------------------------------------------------------------------

### Debug

``` bash
LC_RELEASE_DEBUG=1 lc-release develop
```

Affiche les informations internes (range, origin, parsing GitLab...).

------------------------------------------------------------------------

### Extraction ticket depuis branches

``` bash
LC_RELEASE_TICKET_FROM_BRANCH=1 lc-release develop
```

Active un fallback pour retrouver un ticket depuis le nom de branche
distante.

⚠️ Peut ralentir sur gros repositories.

------------------------------------------------------------------------

## 📦 Format de sortie

Chaque ligne affiche :

-   SHA court
-   Auteur (`@username`)
-   Date courte
-   Ticket (si détecté)
-   Type + message

Exemple :

    a1b2c3d4   @ccassinat   16/02/2026 - 15:42   [#12345] ✨ feat — Ajoute le tri des commits

------------------------------------------------------------------------

## 📄 Licence

À définir (MIT recommandé).
