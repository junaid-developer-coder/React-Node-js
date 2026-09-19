<p align="center">
  <img src="./assets/logos.svg" alt="Project logo" width="140" />
</p>

<h1 align="center">My React App</h1>

<p align="center">
  A modern React + Node.js project, ready for professional development.
</p>

<p align="center">
  <a href="https://github.com/Junaid_developer/react_nodejs/actions"><img alt="CI" src="https://github.com/YOUR_USERNAME/YOUR_REPO/actions/workflows/ci.yml/badge.svg" /></a>
  <img alt="Node" src="https://img.shields.io/badge/node-%3E%3D20-339933?logo=node.js&logoColor=white" />
  <img alt="React" src="https://img.shields.io/badge/react-18%2B-61dafb?logo=react&logoColor=black" />
  <img alt="License" src="https://img.shields.io/badge/license-MIT-blue" />
</p>

---

## Table of Contents

1. [Prerequisites](#prerequisites)
2. [Install Node.js](#install-nodejs)
3. [Create the React project](#create-the-react-project)
4. [Push to GitHub](#push-to-github)
5. [Project structure](#project-structure)
6. [Code quality](#code-quality)
7. [Continuous integration](#continuous-integration)
8. [Contributing and license](#contributing-and-license)

---

## Prerequisites

- Git 2.30+
- Node.js 20 LTS or newer (npm is included)
- A GitHub account
- Optional: [GitHub CLI](https://cli.github.com/) (`gh`)

## Install Node.js

Use a **version manager**. It lets you switch Node versions per project and avoids permission problems.

### Windows

**Option A: Official installer via winget (simplest)**

```powershell
winget install OpenJS.NodeJS.LTS
```

**Option B: nvm-windows (recommended for multiple projects)**

```powershell
winget install CoreyButler.NVMforWindows
# Close and reopen the terminal, then:
nvm install lts
nvm use lts
```

Install Git if you don't have it:

```powershell
winget install Git.Git
```

### Linux (Ubuntu / Debian / Fedora / Arch)

**Recommended: nvm**

```bash
curl -o- https://raw.githubusercontent.com/nvm-sh/nvm/v0.40.3/install.sh | bash
# Restart the terminal (or run: source ~/.bashrc), then:
nvm install --lts
nvm use --lts
```

Install Git:

```bash
# Debian/Ubuntu
sudo apt update && sudo apt install -y git
# Fedora
sudo dnf install -y git
# Arch
sudo pacman -S git
```

### Verify the installation (both systems)

```bash
node -v
npm -v
git --version
```

Pin the Node version for the whole team by adding an `.nvmrc` file:

```bash
echo "lts/*" > .nvmrc
```

## Create the React project

Create React App is deprecated. Use **Vite**:

```bash
npm create vite@latest my-react-app -- --template react-ts
cd my-react-app
npm install
npm run dev
```

Use `--template react` for plain JavaScript. The dev server runs at `http://localhost:5173`.

| Command | Purpose |
| --- | --- |
| `npm run dev` | Start the development server |
| `npm run build` | Production build into `dist/` |
| `npm run preview` | Preview the production build |
| `npm run lint` | Run ESLint |

## Push to GitHub

Add the logo first: create an `assets/` folder and place `logo.svg` in it.

Create a `.gitignore` (Vite generates one, but confirm it contains):

```
node_modules
dist
.env
.env.local
.DS_Store
```

Then:

```bash
git init
git add .
git commit -m "chore: initial commit"
git branch -M main
```

**With GitHub CLI:**

```bash
gh auth login
gh repo create my-react-app --public --source=. --remote=origin --push
```

**Without GitHub CLI:** create an empty repository on github.com, then:

```bash
git remote add origin https://github.com/YOUR_USERNAME/my-react-app.git
git push -u origin main
```

Recommended repository settings (Settings → Branches): protect `main`, require pull requests, and require the CI check to pass before merging.

## Project structure

```
my-react-app/
├── .github/
│   └── workflows/
│       └── ci.yml
├── assets/
│   └── logo.svg
├── public/
├── src/
│   ├── components/
│   ├── hooks/
│   ├── pages/
│   ├── App.tsx
│   └── main.tsx
├── .editorconfig
├── .gitignore
├── .nvmrc
├── CONTRIBUTING.md
├── LICENSE
├── package.json
└── README.md
```

## Code quality

Add Prettier alongside the ESLint setup that Vite includes:

```bash
npm install -D prettier eslint-config-prettier
```

`.prettierrc`:

```json
{
  "semi": true,
  "singleQuote": true,
  "trailingComma": "all",
  "printWidth": 100
}
```

Use [Conventional Commits](https://www.conventionalcommits.org/) for clean history: `feat:`, `fix:`, `docs:`, `chore:`, `refactor:`, `test:`.

## Continuous integration

Create `.github/workflows/ci.yml`:

```yaml
name: CI

on:
  push:
    branches: [main]
  pull_request:

jobs:
  build:
    runs-on: ubuntu-latest
    strategy:
      matrix:
        node-version: [20, 22]
    steps:
      - uses: actions/checkout@v4
      - uses: actions/setup-node@v4
        with:
          node-version: ${{ matrix.node-version }}
          cache: npm
      - run: npm ci
      - run: npm run lint
      - run: npm run build
```

## Contributing and license

1. Fork the repository and create a branch: `git checkout -b feat/my-feature`
2. Commit your changes using Conventional Commits.
3. Push the branch and open a Pull Request.

Released under the [MIT License](./LICENSE). Add a `LICENSE` file (GitHub can generate one when you create the repository, or use https://choosealicense.com).
