# 🏥 Gestion Hospitalière

<div align="center">

![PHP](https://img.shields.io/badge/PHP-777BB4?style=for-the-badge&logo=php&logoColor=white)
![MySQL](https://img.shields.io/badge/MySQL-4479A1?style=for-the-badge&logo=mysql&logoColor=white)
![HTML5](https://img.shields.io/badge/HTML5-E34F26?style=for-the-badge&logo=html5&logoColor=white)
![CSS3](https://img.shields.io/badge/CSS3-1572B6?style=for-the-badge&logo=css3&logoColor=white)
![Font Awesome](https://img.shields.io/badge/Font_Awesome-528DD7?style=for-the-badge&logo=fontawesome&logoColor=white)

**Application web complète pour centraliser et optimiser l'administration d'un établissement de santé.**

[Fonctionnalités](#-fonctionnalités) · [Architecture](#️-architecture-technique) · [Installation](#-installation) · [Structure](#-structure-du-projet) · [Sécurité](#-sécurité)

</div>

---

## 📋 Présentation

**Gestion Hospitalière** est une application web conçue pour répondre aux besoins opérationnels d'un hôpital moderne. Elle centralise la gestion des patients, du personnel médical, des infrastructures (chambres, lits) et de la logistique pharmaceutique dans une interface unifiée, sécurisée et responsive.

---

## ✨ Fonctionnalités

### 📊 Tableau de bord (Dashboard)
- Vue d'ensemble interactive des statistiques clés de l'hôpital
- Indicateurs en temps réel : patients admis, chambres disponibles, stock médicaments
- Graphiques et métriques de performance

### 🧑‍⚕️ Gestion des patients
- Admission et création de dossiers médicaux complets
- Suivi personnalisé : informations personnelles, antécédents, état de santé
- Historique consultable et archivage des dossiers

### 🩺 Consultations médicales
- Suivi chronologique des visites et rendez-vous
- Enregistrement des diagnostics et prescriptions médicales
- Liaison directe entre consultation, patient et médecin traitant

### 🛏️ Gestion des chambres
- Contrôle en temps réel de la disponibilité des lits
- Affectation et transfert des patients entre chambres
- Vue par service, étage et type d'hébergement

### 💊 Pharmacie & Stock
- Inventaire complet des médicaments et produits médicaux
- Système de réservation et de vente intégré
- Alertes de stock bas et gestion des péremptions

### 📅 Réservations

| Type | Description |
|------|-------------|
| **Chambre** | Planification et gestion des hospitalisations |
| **Produits** | Commande et distribution de médicaments |

### 📈 Rapports & Analyses
- Génération de rapports détaillés sur l'activité hospitalière
- Options d'exportation pour analyse externe (Excel, PDF)
- Statistiques par période, service ou praticien

### 🔐 Authentification & Rôles
- Système multi-utilisateurs avec gestion fine des droits
- Accès restreint selon le rôle : Administrateur, Médecin, Infirmier, Pharmacien
- Sessions PHP sécurisées avec hachage des mots de passe

---

## 🛠️ Architecture technique

```
┌──────────────────────────────────────────────────────┐
│                   FRONTEND (Client)                  │
│        HTML5 · CSS3 · Glassmorphism · Font Awesome   │
└────────────────────────┬─────────────────────────────┘
                         │ HTTP Requests
┌────────────────────────▼─────────────────────────────┐
│                  BACKEND (Serveur)                   │
│              PHP · Sessions · PDO                    │
│                                                      │
│  ┌─────────────┐  ┌───────────────┐  ┌───────────┐  │
│  │Auth/Session │  │ Logique Métier│  │  Rapports │  │
│  └─────────────┘  └───────────────┘  └───────────┘  │
└────────────────────────┬─────────────────────────────┘
                         │ PDO (requêtes préparées)
┌────────────────────────▼─────────────────────────────┐
│               BASE DE DONNÉES (MySQL)                │
│                  gestion_hopital                     │
│                                                      │
│  patients · consultations · chambres · reservations  │
│  produits · utilisateurs · rapports · roles          │
└──────────────────────────────────────────────────────┘
```

| Couche | Technologie | Rôle |
|--------|-------------|------|
| **Frontend** | HTML5, CSS3, Font Awesome | Interface responsive & Glassmorphism UI |
| **Backend** | PHP (PDO) | Logique métier, sessions, sécurité |
| **Base de données** | MySQL (`gestion_hopital`) | Stockage des données cliniques & administratives |


---

## 🚀 Installation

### Prérequis

- **Serveur web** : Apache ou Nginx
- **PHP** ≥ 7.4 avec extensions PDO et PDO_MySQL activées
- **MySQL** ≥ 5.7 ou MariaDB ≥ 10.3
- **XAMPP / WAMP / LAMP** recommandé pour un environnement local

### Étapes

**1. Cloner le dépôt**
```bash
git clone https://github.com/VOTRE_USERNAME/gestion-hospitaliere.git
cd gestion-hospitaliere
```

**2. Placer le projet dans le serveur web**

Sous XAMPP :
```
C:/xampp/htdocs/gestion-hospitaliere/
```
Sous Linux/Apache :
```bash
sudo cp -r gestion-hospitaliere/ /var/www/html/
```

**3. Créer la base de données**

Ouvrez **phpMyAdmin** ou votre client MySQL, puis exécutez :
```sql
CREATE DATABASE gestion_hopital CHARACTER SET utf8mb4 COLLATE utf8mb4_unicode_ci;
USE gestion_hopital;
SOURCE sql/gestion_hopital.sql;
```

**4. Configurer la connexion**

Éditez le fichier `config/database.php` :
```php
<?php
$host     = 'localhost';
$dbname   = 'gestion_hopital';
$username = 'root';          // Votre utilisateur MySQL
$password = '';              // Votre mot de passe MySQL

try {
    $pdo = new PDO("mysql:host=$host;dbname=$dbname;charset=utf8mb4", $username, $password);
    $pdo->setAttribute(PDO::ATTR_ERRMODE, PDO::ERRMODE_EXCEPTION);
} catch (PDOException $e) {
    die("Erreur de connexion : " . $e->getMessage());
}
```

**5. Lancer l'application**

Démarrez Apache et MySQL, puis ouvrez votre navigateur :
```
http://localhost/gestion-hospitaliere/
```

### Compte administrateur par défaut

| Champ | Valeur |
|-------|--------|
| **Identifiant** | `admin` |
| **Mot de passe** | `admin123` |

> ⚠️ Changez ces identifiants immédiatement après la première connexion.

---

## 🔒 Sécurité

- **PDO avec requêtes préparées** — protection contre les injections SQL
- **Hachage des mots de passe** via `password_hash()` (bcrypt)
- **Sessions PHP sécurisées** — vérification de l'authentification sur chaque page protégée
- **Gestion des rôles** — accès restreint selon les privilèges de l'utilisateur
- **Validation des données** — filtrage côté serveur de toutes les entrées utilisateur

---

## 📸 Interface

L'interface utilise un design **Glassmorphism** avec :
- Dégradés premium et effets de transparence
- Composants cards avec flou d'arrière-plan (`backdrop-filter: blur`)
- Design entièrement **responsive** — desktop, tablette, mobile
- Iconographie complète via **Font Awesome 6**

---

## 🤝 Contribution

Les contributions sont les bienvenues !

1. Forkez le projet
2. Créez une branche : `git checkout -b feature/nouvelle-fonctionnalite`
3. Commitez : `git commit -m "feat: description de la fonctionnalité"`
4. Poussez : `git push origin feature/nouvelle-fonctionnalite`
5. Ouvrez une **Pull Request**

---

## 📄 Licence

Ce projet est sous licence **MIT** — voir le fichier [LICENSE](LICENSE) pour plus de détails.

---

<div align="center">

Développé avec ❤️ pour optimiser la gestion des établissements de santé

</div>
