# Chapitre 2 : Conditions Applicables et Préparations

## 2.1 Exigences Minimales pour les Plateformes d'Agents

Avant de commencer, confirmez si la plateforme d'agents que vous utilisez possède les capacités suivantes. Ce sont les fondations physiques pour mettre en œuvre cette architecture.

### 2.1.1 Capacités Essentielles (Manquer d'Empêche Une Mise en Œuvre Complète)

| Capacité | Description | Objectif |
| :--- | :--- | :--- |
| **Mémoire Persistante** | Systèmes de mémoire capables de stocker, lire et mettre à jour entre sessions | Héberge le cadre méta-cognitif L1, la logique utilisateur L2, les modèles de scénario L3, les tables de contrôle intégral |
| **Modules Procéduraux** | Capacité à créer, appeler et mettre à jour des compétences/Skills/GPTs, etc. | Héberge la couche d'exécution (portes de livraison, lancement de prévision, organisation en boucle fermée, etc.) |
| **Fenêtre de Contexte Suffisante** | Recommandé 100k tokens ou plus | Accommode les listes de prévision dans les sessions, les enregistrements de pièges, les processus d'exécution de tâches |

Si votre plateforme possède les trois capacités ci-dessus, vous pouvez mettre en œuvre complètement tout le contenu de ce tutoriel.

### 2.1.2 Capacités Bonus (Plus Fort avec Elles, Peut Fonctionner à Niveau Réduit Sans Elles)

| Capacité | Description | Alternative en Cas d'Absence |
| :--- | :--- | :--- |
| **Récupération de Session** | Rechercher le contenu et les enregistrements de correction dans les sessions historiques | Écrire manuellement les leçons clés dans la mémoire après chaque correction, comme matériel de prévision |
| **Appel d'Outils** | L'agent peut appeler activement des outils externes (recherche, exécution de code, etc.) | La portée est limitée mais l'architecture de base n'est pas affectée |

### 2.1.3 Si Votre Plateforme Manque de Fonctionnalité de Compétence

Certaines plates-formes (comme ChatGPT de base, interfaces de chat simples) n'ont pas de modules de compétence. Dans ce cas, vous pouvez adopter la **"Méthode de Simulation parla Mémoire"** :

- Stocker le contenu des compétences sous forme d'entrées de mémoire structurées, comme `[Compétence-Porte de Livraison] Contenu : ...`
- Ajouter des règles obligatoires dans le cadre méta-cognitif L1 : "Avant chaque livraison, doit lire et exécuter toutes les entrées de mémoire marquées [Compétence-*]"
- Inconvénient : consomme la capacité de mémoire et nécessite que l'agent récupère activement ; avantage : la logique est entièrement préservée, convient aux scénarios d'utilisation légère.

## 2.2 Auto-Évaluation : Êtes-vous Approprié pour Utiliser Ce Tutoriel ?

### 2.2.1 Profils d'Utilisateurs Fortement Recommandés

- **Utilisateurs de Collaboration Haute Précision** : Vous avez des exigences de qualité stables pour les sorties d'agents (telles que le style d'écriture, les normes de code)
- **Utilisateurs de Tâches Répétitives** : Vous effectuez fréquemment des tâches similaires avec des agents (tels que flux de travail similaires quotidiens/hebdomadaires)
- **Utilisateurs à Pensée Systémique** : Vous êtes prêt à investir des coûts de configuration initiaux en échange d'une efficacité de collaboration à long terme
- **Utilisateurs à Frontières Claires** : Vous pouvez exprimer clairement les préférences et les lignes rouges, et êtes prêt à les indiquer lorsque les agents font des erreurs

### 2.2.2 Utilisateurs Moins Appropriés

- Effectuer uniquement des questions-réponses aléatoires ponctuelles sans réutilisation
- Les cas d'utilisation s'étendent très largement, rendant difficile l'abstraction de modèles stables
- Ne pas souhaiter établir des relations de collaboration à long terme avec des agents

## 2.3 Travail de Préparation Avant de Commencer

Avant le déploiement formel, complétez les quatre préparations suivantes, qui peuvent significativement réduire les coûts d'ajustement ultérieurs.

### 2.3.1 Prendre l'Inventaire de l'État Actuel de l'Agent

Exécutez les deux commandes suivantes et enregistrez l'état actuel comme base de référence :

```
Énumérez toutes les compétences que vous avez actuellement, ainsi que leurs résumés de contenu.
```

```
Énumérez tout le contenu actuellement stocké dans votre mémoire et évaluez le taux d'utilisation.
```

**Points d'Enregistrement Clés** :
- Combien de compétences existent actuellement ? Sont-elles encore en usage ?
- Quel pourcentage de mémoire est utilisé ? Le contenu est-il déjà mélangé/confus ?
- Y a-t-il une grande quantité d'informations obsolètes ?

### 2.3.2 Lister les Préférences et Règles que Vous Voulez Solidifier

Utilisez un tableau simple pour lister les principes que vous voulez que l'agent suive à long terme. Cette étape vous aide à extraire des règles actionnables à partir de "sentiments" vagues :

| Dimension | Vos Principes | Exemple |
| :--- | :--- | :--- |
| Style de Communication | Concis et direct, pas de politesses | Ne pas sortir "j'espère que cela vous aide" |
| Format de Sortie | Code d'abord, avec méthodes de vérification | Inclure les étapes de test lors de la sortie de solutions |
| Préférence de Décision | Risques en premier, exposer les problèmes avant | Lister les risques avant de discuter des avantages |
| Préférence Esthétique | Narrative sobre, rejeter les résumés IA | Laisser les fins des nouvelles ouvertes, ne pas élever |

Vous n'avez pas besoin d'épuiser tout à la fois, 4 à 6 principes fondamentaux suffisent. L'agent vous aidera à les compléter continuellement dans la boucle fermée ultérieurement.

### 2.3.3 Rappeler 3 à 5 Types de Tâches que Vous Exécutez Fréquemment

- Par exemple : écriture de nouvelles courtes / revue de code / dépannage opérationnel / conception d'architecture / analyse de données
- Pour chaque type, essayez d'écrire une phrase décrivant ce que vous considérez comme le modèle clé pour "le faire correctement" pour ce type de tâche

**Exemples** :
- Création de nouvelles courtes : "Le réglage du ton émotionnel prime sur le déploiement de l'intrigue, les fins doivent être laissées ouvertes."
- Revue de code : "D'abord chercher les problèmes architecturaux, puis vérifier les conventions de dénomination ; pour chaque type de problème trouvé, fournir des suggestions de modification."
- Dépannage de problèmes : "D'abord vérifier les journaux pour localiser les causes racines, ne pas attendre et deviner ; en cas d'incertitude, marquer comme 'en attente de vérification'."

Ces éléments deviendront directement le contenu initial de vos modèles de scénario L3.

### 2.3.4 Sauvegarder l'État Actuel

Avant de commencer le déploiement, **sauvegardez votre état actuel de mémoire et de compétences**. Les méthodes spécifiques dépendent de votre plateforme :

- Si la plateforme prend en charge l'exportation, exportez d'abord une copie
- Si non pris en charge, copiez manuellement les listes de mémoire et de compétences actuelles vers un document local
- S'il y a une gestion de version (telle que les instantanés de mémoire sur certaines plateformes), créer un point de restauration

L'objectif de cette étape : en cas de désordre pendant le déploiement, vous pouvez restaurer à l'état initial et recommencer.

## 2.4 Indicateurs d'Achèvement de la Phase de Préparation

Lorsque vous pouvez répondre aux trois questions suivantes, la phase de préparation est terminée et vous pouvez entrer dans le chapitre 3 :

1. Ma plateforme d'agents possède-t-elle la mémoire persistante + les modules de compétences ? (Oui / Non / Partiellement)
2. Combien de préférences et principes fondamentaux ai-je identifiés ? (Recommandé ≥ 4)
3. Combien de types de tâches à haute fréquence ai-je listés, et pour chaque type ai-je des "jugements de modèle" préliminaires ? (Recommandé ≥ 3)
