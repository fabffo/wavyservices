
# 📄 Déploiement Git pour Wavy Services

## 📁 Répertoires

| Usage          | Dossier local                                     |
|----------------|---------------------------------------------------|
| Développement  | `C:\Program Files\Apache24\htdocs\wavyservicesEnDev` |
| Production     | `C:\Program Files\Apache24\htdocs\wavyservices`     |

---

## 🧱 1. Initialiser Git dans le dossier de développement

```bash
cd "C:\Program Files\Apache24\htdocs\wavyservicesEnDev"
git init
git add .
git commit -m "Initialisation du projet Wavy Services"
```

---

## ☁️ 2. Lier à GitHub et pousser

### 🔗 Ajouter le dépôt distant GitHub

```bash
git remote add origin https://github.com/fabffo/wavyservices.git
git branch -M developpement
git push -u origin developpement
```

---

## 🚀 3. Préparer le dossier de production

### ⚠️ Si `wavyservices` contient déjà des fichiers…

**Tu dois choisir UNE des trois options suivantes :**

---

### ✅ Option A — Écraser et cloner proprement (si tu n’as plus besoin des fichiers actuels)

```bash
rmdir /s /q "C:\Program Files\Apache24\htdocs\wavyservices"
git clone -b developpement https://github.com/fabffo/wavyservices.git "C:\Program Files\Apache24\htdocs\wavyservices"
```

---

### ✅ Option B — Sauvegarder l'existant, puis cloner

```bash
rename "C:\Program Files\Apache24\htdocs\wavyservices" "wavyservices_backup"
git clone -b developpement https://github.com/fabffo/wavyservices.git "C:\Program Files\Apache24\htdocs\wavyservices"
```

---

### ✅ Option C — Cloner ailleurs, puis recopier (sans utiliser `git clone` dans Apache)

```bash
cd D:\
git clone -b developpement https://github.com/fabffo/wavyservices.git wavy_temp

robocopy D:\wavy_temp "C:\Program Files\Apache24\htdocs\wavyservices" /MIR
```

---

## 🔄 4. Mettre à jour la production à tout moment

Dans le dossier de prod :

```bash
cd "C:\Program Files\Apache24\htdocs\wavyservices"
git pull origin developpement
```

---

## 🧰 Astuce : Script `.bat` de mise à jour

Tu peux créer un fichier `maj-prod.bat` avec ce contenu :

```bat
@echo off
cd /d "C:\Program Files\Apache24\htdocs\wavyservices"
git pull origin developpement
pause
```

➡️ Tu double-cliques pour mettre à jour la prod automatiquement.

---

## 📌 Résumé visuel

```
[Dev local] wavyservicesEnDev
      │
      ├── git push → GitHub (branche developpement)
      │
      ↓
[GitHub] fabffo/wavyservices.git
      │
      └── git pull → [Prod local] wavyservices
```
