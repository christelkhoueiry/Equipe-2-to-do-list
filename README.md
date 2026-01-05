# To-Do List - Préparation Examen

Application Front-End de gestion de tâches pour la préparation d'examens, utilisant HTML, CSS et JavaScript avec stockage localStorage.

## Contexte

Cette application permet de gérer des tâches de révision organisées par **matières** et **catégories de préparation**. L'urgence est calculée automatiquement selon la date limite.

## Structure des données JSON

### Tâche (`taskList`)

```json
{
	"idTask": 1,
	"title": "Réviser les fonctions",
	"description": "Revoir les chapitres sur les fonctions dérivées",
	"idCategory": 4,
	"idSubject": 1,
	"idStatus": 1,
	"deadline": "2025-12-18"
}
```

- **idTask** : Clé primaire auto-incrémentée
- **idCategory** : Clé étrangère vers `categories`
- **idSubject** : Clé étrangère vers `subjectList`
- **idStatus** : Clé étrangère vers `statuses`

### Urgences (`urgencies`)

4 niveaux calculés automatiquement selon le nombre de jours restants :
| ID | Niveau | Couleur | Condition |
|----|--------|---------|-----------|
| 1 | Peu urgent | #4CAF50 | > 6 jours |
| 2 | Modéré | #FFC107 | 5-6 jours |
| 3 | Urgent | #FF9800 | 3-4 jours |
| 4 | Très urgent | #F44336 | ≤ 2 jours |

### Statuts (`statuses`)

4 statuts possibles pour une tâche :
| ID | Statut | Couleur |
|----|--------|--------|
| 1 | En attente | #95a5a6 |
| 2 | En cours | #3498db |
| 3 | Terminée | #27ae60 |
| 4 | Annulée | #e74c3c |

### Catégories (`categories`)

5 catégories de préparation d'examen avec `idCategory`, `name` et `description`.

### Matières (`subjectList`)

Gérées dynamiquement par l'utilisateur avec `idSubject` et `name`. Stockées en localStorage sous la clé `studySubjects`.

## Fonctionnalités implémentées

### Étape 1 - Données JSON

- Structure JSON avec identifiants (clés primaires)
- Relations via clés étrangères (idCategory, idSubject, idStatus)
- Livrables dans les dossiers `etape-1a/`, `etape-1b/`, `etape-1c/`, `etape-1d/`, `etape-1e/`

### Étape 2 - Formulaire

- Formulaire HTML sémantique avec validation (`required`)
- Design responsive avec CSS Flexbox
- Listes déroulantes pour catégories et matières

### Étape 3A - Formulaire dynamique

- Génération dynamique des `<select>` via `refreshCategorySelect()`, `refreshSubjectSelect()` et `refreshStatusSelect()`
- Données JSON injectées dans le DOM au chargement

### Étape 3B - Enregistrement localStorage

- Clés : `studyTasks` (tâches), `studySubjects` (matières)
- Utilisation de `JSON.parse()` / `JSON.stringify()`
- ID auto-incrémenté basé sur le max existant + 1

### Étape 3C - Tableau récapitulatif

- Affichage dans `<table>` avec colonnes : ID, Nom, Description, Catégorie, Matière, Statut, Date limite, Urgence, Actions
- Résolution des clés étrangères via `findCategory()`, `findSubject()` et `findStatus()`
- Badge coloré pour l'urgence et le statut

### Étape 3D - Archivage et gestion

- Variable `idStatus` pour gérer le statut de la tâche (En attente, En cours, Terminée, Annulée)
- Style barré pour les tâches terminées ou annulées (`.task-completed`)
- Boutons Modifier/Supprimer pour chaque tâche
- Édition en place avec pré-remplissage du formulaire
- Archivage des tâches terminées/annulées

## Stockage localStorage

| Clé             | Contenu                 |
| --------------- | ----------------------- |
| `studyTasks`    | Array JSON des tâches   |
| `studySubjects` | Array JSON des matières |

## Technologies

- **HTML5** : Structure sémantique (`<header>`, `<main>`, `<section>`, `<footer>`)
- **CSS3** : Flexbox, gradients, transitions
- **JavaScript** : Vanilla JS, API localStorage, manipulation DOM

## Auteur

**Angela** - © 2025
