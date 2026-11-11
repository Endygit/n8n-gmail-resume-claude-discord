# Résumé automatique d'e-mails avec n8n et l'API Claude

Workflow d'automatisation construit avec **n8n**. Quand un e-mail arrive dans une boîte **Gmail**, il en fait générer un résumé par l'**API Claude** (Anthropic), envoie ce résumé sur un salon **Discord** et archive les fichiers produits (PDF…) dans **Google Drive**, classés par jour.

> Projet personnel, réalisé dans le cadre de mon parcours **Builder IA (OpenClassrooms)**.

---

## Le problème

Lire chaque e-mail en entier prend du temps, surtout quand beaucoup ne demandent pas d'action immédiate. L'idée : recevoir **l'essentiel de chaque message en quelques lignes**, là où je suis déjà (Discord), sans ouvrir ma boîte mail.

## Ce que fait le workflow

```
 Gmail              n8n                  API Claude           Discord           Google Drive
┌─────────┐    ┌──────────────┐    ┌──────────────┐    ┌──────────────┐    ┌──────────────┐
│ Nouvel  │ ─▶ │ Déclencheur  │ ─▶ │ Résumé de    │ ─▶ │ Message posté│ ─▶ │ Fichiers     │
│ e-mail  │    │ + extraction │    │ l'e-mail     │    │ dans un salon│    │ (PDF…) rangés│
│         │    │ du contenu   │    │              │    │              │    │1 dossier/jour│
└─────────┘    └──────────────┘    └──────────────┘    └──────────────┘    └──────────────┘
```

1. **Déclencheur Gmail** : n8n détecte l'arrivée d'un nouvel e-mail.
2. **Préparation** : récupération de l'expéditeur, de l'objet et du corps du message.
3. **Appel à l'API Claude** : envoi du contenu avec une consigne (prompt) demandant un résumé court et clair.
4. **Envoi sur Discord** : le résumé est publié dans un salon dédié.
5. **Archivage dans Google Drive** : les fichiers issus du workflow (PDF, etc.) sont enregistrés dans Google Drive, rangés automatiquement dans **un dossier par jour**.

## Aperçu

<!-- À COMPLÉTER : ajouter une capture d'écran du workflow dans l'éditeur n8n, puis décommenter la ligne ci-dessous. -->
<!-- ![Workflow dans n8n](capture-workflow.png) -->

## Outils utilisés

| Outil | Rôle |
|---|---|
| **n8n** (n8n Cloud) | Orchestration du workflow, sans serveur à gérer |
| **Gmail** | Source des e-mails (déclencheur) |
| **API Claude** (Anthropic) | Génération du résumé (IA générative) |
| **Discord** | Réception des résumés |
| **Google Drive** | Stockage final des fichiers (PDF…), classés dans un dossier par jour |

## Ce que ce projet m'a appris

- Concevoir un **flux d'automatisation de bout en bout** : déclencheur, traitement, action.
- **Intégrer un LLM** dans un processus réel via une API, et rédiger un prompt adapté à une tâche précise.
- Organiser automatiquement des fichiers (création d'un **dossier par date** dans Google Drive).
- Connecter des **services tiers** entre eux (authentification, format des données d'un nœud à l'autre).
- **Tester et ajuster** le workflow jusqu'à obtenir un résultat exploitable.

## Utiliser ce workflow

1. Télécharger le fichier `workflow.json` de ce dépôt.
2. Dans n8n : **Workflows → Import from file**.
3. Créer ses propres identifiants dans n8n (Gmail, clé API Anthropic, webhook ou bot Discord, Google Drive) et les associer aux nœuds correspondants.
4. Activer le workflow.

> 🔒 Le fichier exporté ne contient **aucune clé d'API ni identifiant** : chacun doit utiliser les siens.

## Pistes d'amélioration

- Filtrer les e-mails à résumer (expéditeurs, libellés Gmail) pour ignorer les newsletters.
- Classer automatiquement chaque e-mail (urgent / à traiter / information) en plus du résumé.

---

**Andy Pauriac** — alternance Builder IA · [github.com/Endygit](https://github.com/Endygit)
