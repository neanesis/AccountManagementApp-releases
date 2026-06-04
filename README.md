# Account Management

Application de bureau Windows pour rechercher et modifier des comptes utilisateurs sur plusieurs systèmes depuis une interface unifiée.

---

## Téléchargement

| Version | Installeur | MSI (déploiement silencieux) |
|---|---|---|
| **1.1.2** *(dernière)* | [AccountManagementApp-1.1.2-Setup.exe](https://github.com/neanesis/AccountManagementApp-releases/releases/download/v1.1.2/AccountManagementApp-1.1.2-Setup.exe) | [AccountManagementApp-1.1.2.msi](https://github.com/neanesis/AccountManagementApp-releases/releases/download/v1.1.2/AccountManagementApp-1.1.2.msi) |

Toutes les versions : [Releases →](https://github.com/neanesis/AccountManagementApp-releases/releases)

---

## Installation

1. Télécharger `AccountManagementApp-X.X.X-Setup.exe`
2. Double-cliquer → installation **sans droits administrateur** (per-user, dans `%LocalAppData%`)
3. L'application est disponible dans le menu Démarrer et sur le bureau

> Aucun prérequis — Python n'est pas nécessaire. L'installeur est autonome.

### Prérequis optionnels (selon les connecteurs utilisés)

| Connecteur | Outil requis |
|---|---|
| **Salesforce** | [Salesforce CLI](https://developer.salesforce.com/tools/salesforcecli) (`sf`) |
| **Microsoft Graph** | [Azure CLI](https://learn.microsoft.com/fr-fr/cli/azure/install-azure-cli) (`az`) |
| **Canvas LMS** | Token API Canvas (Paramètres du compte → Tokens d'accès) |
| **SpotMe** | Clé API SpotMe |

> L'application propose d'installer SF CLI et Azure CLI automatiquement via **winget** au premier lancement si ces outils sont manquants.

---

## Fonctionnalités

### Connecteurs

| Onglet | Ce que vous pouvez faire |
|---|---|
| **Canvas LMS** | Recherche par nom, email, login, SIS ID — édition inline — rollback depuis l'audit |
| **Salesforce** | Recherche et édition via SF CLI, sélecteur d'objet et de champs dynamique |
| **Microsoft Graph** | Utilisateurs Azure AD, attributs d'extension, identités B2C |
| **SpotMe** | Participants par email, édition des champs du profil |
| **Liaisons** | Vue cross-connecteur : Canvas ↔ Salesforce ↔ Graph ↔ SpotMe sur la même ligne |

### Fonctionnalités transversales

- **Multi-profils** — profils nommés avec tous les paramètres de connexion, export/import JSON
- **Multi-instances** — plusieurs orgs Salesforce, plusieurs instances Canvas dans le même profil
- **Édition inline** — cellules modifiées mises en évidence (fond jaune), confirmation avant sauvegarde
- **Validation des champs** — cellule rouge et blocage du save si le format est incorrect (email, date ISO…)
- **Journal d'audit** — toutes les modifications sont tracées dans un fichier `audit.jsonl` append-only
- **Rollback** — restaurer n'importe quelle modification depuis le journal d'audit via appels API directs
- **Fusion de comptes** — merge API direct Canvas et Salesforce SOAP depuis l'onglet Liaisons
- **Export CSV / Excel** — résultats de recherche et journal d'audit exportables
- **CSV aller-retour** — exporter → modifier dans Excel → réimporter comme modifications en attente
- **Mise à jour automatique** — vérification au démarrage, téléchargement et installation silencieux
- **Thème clair / sombre** — Menu Outils → Mode sombre, préférence sauvegardée par profil
- **Connecteurs extensibles** — un connecteur standard s'ajoute en déposant un fichier `.py` dans `%APPDATA%\AccountManagementApp\connectors\` (sans réinstaller) ; il obtient automatiquement un onglet et un formulaire de configuration. Menu **Outils → Connecteurs** pour voir les connecteurs chargés

---

## Mise à jour

L'application vérifie les mises à jour à chaque démarrage. Si une nouvelle version est disponible, elle se télécharge et s'installe silencieusement, puis l'application redémarre automatiquement.

Pour mettre à jour manuellement : **Aide → Vérifier les mises à jour…**

---

## Licence

L'application nécessite un fichier `license.json` fourni par votre administrateur. Si l'application affiche une erreur de licence au démarrage, utiliser le bouton **"Choisir un fichier license.json…"** pour localiser le fichier.

---

## Données stockées localement

| Fichier | Contenu |
|---|---|
| `%APPDATA%\AccountManagementApp\profiles.json` | Configuration des profils (tokens non inclus) |
| `%APPDATA%\AccountManagementApp\audit.jsonl` | Journal de toutes les modifications |
| `%LocalAppData%\AccountManagementApp\license.json` | Fichier de licence |

**Les tokens d'accès ne sont jamais écrits sur disque.** Ils sont saisis à la connexion et conservés en mémoire uniquement pendant la session.

---

## Changelog

### 1.1.2 — 2026-06-03
- **Connecteurs extensibles** : ajout d'un connecteur en déposant un fichier, sans réinstaller (menu Outils → Connecteurs)
- Correction du **surlignage des cellules** (jaune « modifié » / rouge « invalide ») qui disparaissait — texte devenu illisible en mode sombre
- Correctifs de la **fusion de comptes** Canvas + champ **Département** SpotMe passé en lecture seule

### 1.1.1 — 2026-06-02
- Correction du rollback Canvas sur les champs identifiant (login, SIS ID) — endpoint logins corrigé
- Correction d'un plantage lors de la sauvegarde de liaisons
- Couleurs des en-têtes dans l'onglet Liaisons restaurées
- Spinner de recherche animé sur tous les onglets, affiché à côté du texte de chargement

### 1.1.0 — 2026-06-02
- Thème clair / sombre (Menu Outils → Mode sombre)
- Icône AM intégrée (barre de titre, barre des tâches, installeur)
- Design enterprise Fusion blanc/gris avec accent bleu

### 1.0.3 — 2026-06-02
- Vérification des mises à jour (manuelle + automatique au démarrage)
- Validation inline des champs avec blocage du save
- Spinner de recherche dans la barre de statut
- Résumé post-sauvegarde en cas d'erreur partielle
- Raccourci F5 pour relancer la dernière recherche

[Voir le changelog complet →](https://github.com/neanesis/AccountManagementApp-releases/releases)
