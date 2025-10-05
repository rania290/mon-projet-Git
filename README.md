#  TP1 - Maîtrise de Git & GitFlow

<div align="center">

**Formation DevOps 2025-26**  
*Dr. Salah Gontara*

[![Git](https://img.shields.io/badge/Git-F05032?style=for-the-badge&logo=git&logoColor=white)](https://git-scm.com/)
[![GitHub](https://img.shields.io/badge/GitHub-181717?style=for-the-badge&logo=github&logoColor=white)](https://github.com)
[![GitLab](https://img.shields.io/badge/GitLab-FC6D26?style=for-the-badge&logo=gitlab&logoColor=white)](https://gitlab.com)

</div>

---

##  Table des matières

- [Introduction](#-introduction)
- [Prérequis](#-prérequis)
- [Configuration initiale](#-configuration-initiale)
- [Exercices pratiques](#-exercices-pratiques)
- [Commandes Git essentielles](#-commandes-git-essentielles)
- [GitFlow Workflow](#-gitflow-workflow)
- [Résolution de problèmes](#-résolution-de-problèmes)
- [Ressources](#-ressources)

---

##  Introduction

Ce travail pratique couvre l'ensemble des compétences nécessaires pour maîtriser Git, depuis la configuration de base jusqu'aux workflows avancés avec GitFlow. Vous apprendrez à :

- ✅ Configurer un environnement Git professionnel
- ✅ Gérer des dépôts locaux et distants
- ✅ Collaborer efficacement avec d'autres développeurs
- ✅ Utiliser les branches et résoudre les conflits
- ✅ Appliquer le workflow GitFlow

---

##  Prérequis

| Outil | Version minimale | Installation |
|-------|-----------------|--------------|
| Git | 2.x | [Télécharger Git](https://git-scm.com/downloads) |
| Compte GitHub/GitLab | - | [GitHub](https://github.com) / [GitLab](https://gitlab.com) |
| Terminal | - | Linux/Mac: Terminal / Windows: Git Bash |

---

##  Configuration initiale

### Étape 1 : Génération de la clé SSH

```bash
# Générer une nouvelle clé SSH
ssh-keygen -t rsa -b 4096 -C "votre@email.com"

# Afficher votre clé publique
cat ~/.ssh/id_rsa.pub
```

>  **Astuce** : Copiez la clé affichée et ajoutez-la dans `Settings > SSH Keys` de votre compte GitHub/GitLab

### Étape 2 : Configuration de Git

```bash
# Configurer votre identité
git config --global user.name "Prénom Nom"
git config --global user.email "votre@email.com"

# Vérifier la configuration
git config --list
```

### Étape 3 : Test de connexion SSH

```bash
# Pour GitHub
ssh -T git@github.com

# Pour GitLab
ssh -T git@gitlab.com
```

**Réponse attendue** : `Hi username! You've successfully authenticated...`

---

##  Exercices pratiques

### 🔷 Partie 1 : Création du projet

#### 1.1 Créer un nouveau dépôt

1. Connectez-vous à GitHub/GitLab
2. Cliquez sur **New Repository**
3. Nommez votre projet : `tp-git-devops`
4. Sélectionnez **Public** et cochez **Add README**
5. Créez le dépôt

#### 1.2 Cloner le projet

```bash
# Cloner le dépôt
git clone git@github.com:votre-username/tp-git-devops.git

# Accéder au répertoire
cd tp-git-devops
```

#### 1.3 Questions de réflexion

<details>
<summary><b>❓ Comment ajouter un README après création ?</b></summary>

```bash
echo "# Mon Projet" > README.md
git add README.md
git commit -m "Ajout du README"
git push origin main
```
</details>

<details>
<summary><b>❓ Comment définir un dépôt distant ?</b></summary>

```bash
git remote add origin git@github.com:username/repo.git
git remote -v  # Vérifier les dépôts distants
```
</details>

---

### 🔷 Partie 2 : Concepts de base

#### 2.1 Créer et committer des fichiers

```bash
# Créer un fichier HTML
touch index.html
echo "<!DOCTYPE html><html><body><h1>Hello Git</h1></body></html>" > index.html

# Ajouter à l'index
git add index.html

# Créer un commit
git commit -m "Premier commit : ajout de index.html"

# Pousser vers GitHub
git push origin main
```

#### 2.2 Visualiser l'historique

```bash
# Afficher l'historique complet
git log

# Afficher l'historique simplifié
git log --oneline --graph --all

# Comparer deux commits
git diff <commit-id-1> <commit-id-2>
```

#### 2.3 Questions de réflexion

<details>
<summary><b>❓ Comment annuler les modifications locales ?</b></summary>

```bash
# Annuler les modifications d'un fichier
git checkout -- fichier.txt

# Ou avec Git 2.23+
git restore fichier.txt
```
</details>

<details>
<summary><b>❓ Comment voir les fichiers en staging ?</b></summary>

```bash
git status
# ou
git diff --cached
```
</details>

---

### 🔷 Partie 3 : Collaboration et branches

#### 3.1 Créer une branche

```bash
# Créer une nouvelle branche
git branch ma-fonctionnalite

# Basculer sur la branche
git checkout ma-fonctionnalite

# Ou en une seule commande
git checkout -b ma-fonctionnalite
```

#### 3.2 Travailler sur la branche

```bash
# Modifier des fichiers
echo "<p>Nouvelle fonctionnalité</p>" >> index.html

# Ajouter et committer
git add .
git commit -m "Ajout d'une nouvelle fonctionnalité"

# Pousser la branche
git push origin ma-fonctionnalite
```

#### 3.3 Gérer les conflits

```bash
# Sur la branche de fonctionnalité
git checkout ma-fonctionnalite
echo "Modification branche feature" > fichier.txt
git commit -am "Modification dans ma-fonctionnalite"

# Sur la branche main
git checkout main
echo "Modification branche main" > fichier.txt
git commit -am "Modification dans main"

# Fusionner et résoudre le conflit
git merge ma-fonctionnalite
# Éditez le fichier en conflit
git add fichier.txt
git commit -m "Résolution du conflit"
```

#### 3.4 Questions de réflexion

<details>
<summary><b>❓ Comment suivre un dépôt distant ?</b></summary>

```bash
# Ajouter un dépôt distant
git remote add upstream git@github.com:user/repo.git

# Récupérer toutes les branches
git fetch upstream

# Voir les branches distantes
git branch -r
```
</details>

<details>
<summary><b>❓ Comment supprimer une branche fusionnée ?</b></summary>

```bash
# Supprimer localement
git branch -d ma-fonctionnalite

# Supprimer sur le dépôt distant
git push origin --delete ma-fonctionnalite
```
</details>

---

### 🔷 Partie 4 : Rebase

#### 4.1 Processus de rebase

```bash
# 1. Mettre à jour main
git checkout main
git pull origin main

# 2. Rebaser votre branche
git checkout ma-fonctionnalite
git rebase main

# 3. Résoudre les conflits si nécessaire
git add fichier-conflit
git rebase --continue

# 4. Fusionner dans main
git checkout main
git merge ma-fonctionnalite

# 5. Pousser les changements
git push origin main
```

#### 4.2 Questions de réflexion

<details>
<summary><b>❓ Comment annuler un rebase ?</b></summary>

```bash
git rebase --abort
```
</details>

<details>
<summary><b>❓ Comment voir les commits à rebaser ?</b></summary>

```bash
git log main..ma-fonctionnalite --oneline
```
</details>

---

### 🔷 Partie 5 : GitFlow

#### 5.1 Installation et initialisation

```bash
# Installer GitFlow (si nécessaire)
# Ubuntu/Debian
sudo apt-get install git-flow

# macOS
brew install git-flow

# Initialiser GitFlow
git flow init
```

#### 5.2 Workflow des features

```bash
# Créer une feature
git flow feature start authentification

# Travailler sur la feature
git add .
git commit -m "Implémentation de l'authentification"

# Terminer la feature
git flow feature finish authentification
```

#### 5.3 Workflow des releases

```bash
# Créer une release
git flow release start 1.0.0

# Finaliser la release
git flow release finish 1.0.0
git push origin --tags
```

#### 5.4 Workflow des hotfixes

```bash
# Créer un hotfix
git flow hotfix start correction-bug

# Finaliser le hotfix
git flow hotfix finish correction-bug
git push origin --tags
```

#### 5.5 Questions de réflexion

<details>
<summary><b>❓ Comment lister les branches actives ?</b></summary>

```bash
git flow feature list
git flow release list
git flow hotfix list
```
</details>

<details>
<summary><b>❓ Comment annuler un hotfix ?</b></summary>

```bash
# Revenir sur develop et supprimer la branche
git checkout develop
git branch -D hotfix/mon-correctif
```
</details>

---

## 🛠️ Commandes Git essentielles

### Commandes de base

| Commande | Description |
|----------|-------------|
| `git init` | Initialiser un dépôt Git |
| `git clone <url>` | Cloner un dépôt distant |
| `git status` | Voir l'état du dépôt |
| `git add <fichier>` | Ajouter un fichier à l'index |
| `git commit -m "message"` | Créer un commit |
| `git push origin <branche>` | Pousser vers le dépôt distant |
| `git pull origin <branche>` | Récupérer les modifications |

### Gestion des branches

| Commande | Description |
|----------|-------------|
| `git branch` | Lister les branches |
| `git branch <nom>` | Créer une branche |
| `git checkout <branche>` | Changer de branche |
| `git checkout -b <branche>` | Créer et changer de branche |
| `git merge <branche>` | Fusionner une branche |
| `git branch -d <branche>` | Supprimer une branche |

### Historique et différences

| Commande | Description |
|----------|-------------|
| `git log` | Voir l'historique |
| `git log --oneline` | Historique simplifié |
| `git diff` | Voir les différences |
| `git show <commit>` | Afficher un commit |

---

##  GitFlow Workflow

```
main (production)
  │
  ├─── release/1.0.0
  │
develop (développement)
  │
  ├─── feature/login
  ├─── feature/dashboard
  │
hotfix/urgent-bug → main + develop
```

### Branches principales

- **main** : Code en production
- **develop** : Code en développement

### Branches de support

- **feature/** : Nouvelles fonctionnalités
- **release/** : Préparation des versions
- **hotfix/** : Corrections urgentes

---

## 🆘 Résolution de problèmes

### Problème : Conflit lors d'un merge

```bash
# 1. Identifier les fichiers en conflit
git status

# 2. Ouvrir et éditer les fichiers
# 3. Marquer comme résolu
git add fichier-conflit

# 4. Finaliser le merge
git commit
```

### Problème : Annuler le dernier commit

```bash
# Garder les modifications
git reset --soft HEAD~1

# Supprimer les modifications
git reset --hard HEAD~1
```

### Problème : Récupérer un fichier supprimé

```bash
git checkout HEAD -- fichier-supprime.txt
```

---

## 📖 Ressources

- [Documentation officielle Git](https://git-scm.com/doc)
- [GitHub Guides](https://guides.github.com/)
- [GitFlow Cheatsheet](https://danielkummer.github.io/git-flow-cheatsheet/)
- [Learn Git Branching](https://learngitbranching.js.org/)

---

<div align="center">

**📧 Contact** : Dr. Salah Gontara  
**📅 Année** : 2025-26  
**🎓 Cours** : DevOps

---

⭐ **N'oubliez pas de star ce repo si vous l'avez trouvé utile !**

</div>
