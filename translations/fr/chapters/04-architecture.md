# Chapitre 4 : Détails de l'architecture du système — Triple couche de mémoire + Couche de compétences

Les trois premiers chapitres ont respectivement résolu les problèmes du "pourquoi" et du "quoi". Ce chapitre les assemble en une architecture de système complète et véritablement fonctionnelle, permettant aux quatre concepts de cybernétique d'avoir un emplacement clair et un flux de données clair dans le système de mémoire et de l'Agent.

---

## 4.1 Vue d'ensemble de l'architecture

Le principe central de cette architecture est : **utiliser la stratification logique pour définir les limites cognitives, utiliser la stratification physique pour séparer stockage et exécution**.

```
┌────────────────────────────────────────────┐
│          Ton Agent (système contrôlé)       │
├────────────┬───────────────────────────────┤
│  Couche logique │  Stockage physique       │
├────────────┼───────────────────────────────┤
│  L1 Méta-cognitif │ Zone mémoire en-tête (modification autonome impossible) │
│  L2 Logique Utilisateur │ Zone mémoire principale │
│  L3 Modèles Scénario │ Zone mémoire principale │
│  Tableau de contrôle intégral │ Zone mémoire principale │
├────────────┼───────────────────────────────┤
│  Couche d'Exécution │ Modules de compétences      │
│  Liste de prévision │ Contexte intra-session (temporaire)   │
│  Enregistrement corrections historiques │ Archives de session (lecture-seule à long terme) │
└────────────┴───────────────────────────────┘
         ↑ ↓ Flux de contrôle et de données
    ┌─────┴──────┐
    │  Ta tâche   │ ← Système contrôlé
    └────────────┘
```

Chaque couche a des critères stricts d'entrée d'information. Elles sont détaillées ci-dessous.

---

## 4.2 L1 : Cadre méta-cognitif — Constitution du système

### 4.2.1 Positionnement

L1 est la "constitution mentale" de l'Agent, définissant **comment il traite l'information, comment il évalue son propre comportement, comment il prend des décisions**. Il ne vise aucune tâche spécifique ou préférence utilisateur, mais impose des contraintes obligatoires sur le mode de fonctionnement de l'Agent lui-même.

### 4.2.2 Stockage physique

- **Emplacement** : zone en-tête de `memory` (par exemple, à l'avant de `memory(target='memory')` dans Hermes).
- **Attribut** : **modification autonome impossible**. L'Agent peut *proposer* des modifications lors d'une revue en boucle fermée, mais doit attendre votre confirmation. Cela assure que le squelette du système ne sera pas accidentellement tordu par le processus d'évolution de l'Agent lui-même.

### 4.2.3 Structure du contenu

L1 stocke les règles de comportement spécifiques des quatre concepts cybernétiques, et non des définitions abstraites. Chaque règle doit respecter :
- Commencer par "Tu dois" ou "Tu ne dois pas".
- Contenir des conditions de déclenchement claires et des actions d'exécution.
- Être assez courte pour être chargée en une seule fois dans le contexte.

**Exemple d'entrée standard** :

```
① Prévision : Pour chaque nouvelle tâche, tu dois d'abord récupérer L2, L3 et les archives de session,
   et sortir une "liste de démarrage" et anticiper les risques P0-P3.
② Contrôle intégral : En recevant des retours négatifs, tu dois les comptabiliser dans le tableau de contrôle intégral.
   Lorsque le cumul de la même catégorie atteint ≥2, proposer un plan de descente et confirmer avec l'utilisateur.
③ Séparation hiérarchique : Le contenu que tu écris dans la mémoire ne peut contenir que des "principes/lois",
   il ne doit pas contenir d'étapes opératoires. Les étapes opératoires doivent être écrites dans la compétence.
④ Auto-surveillance : Avant de livrer tout résultat, tu dois exécuter delivery_gate,
   et passer les cinq contrôles avant de sortir le résultat final.
⑤ Analyse des causes profondes : Dans la revue en boucle fermée, pour chaque problème, il faut remonter jusqu'au niveau "loi erronée" ou "exécution erronée".
```

Le nombre total d'entrées est recommandé à 5-7, garantissant que l'Agent peut se souvenir complètement d'un coup.

---

## 4.3 L2 : Logique Utilisateur — Ta "Bibliothèque de Principes"

### 4.3.1 Positionnement

L2 stocke tes **préférences stables et principes fondamentaux** qui traversent différentes tâches. Ces préférences ne sont pas limitées à des scénarios spécifiques, mais définissent la direction fondamentale du comportement de l'Agent lorsqu'il collabore avec toi.

Si L1 est la coque cybernétique, L2 est le **noyau personnalisé**, le modèle calculable de l'Agent sur tes modèles de jugement.

### 4.3.2 Stockage physique

- **Emplacement** : zone principale de `memory`, juste après L1.
- **Permission de mise à jour** : écrit par l'Agent lors de la descente intégrale ou de la revue en boucle fermée, après ta confirmation.
- **Contrôle de capacité** : chaque entrée ne dépasse pas 30 caractères, le total ne dépasse pas 10 entrées (ajustable). Éviter que L2 ne devienne un "mémo", forcer la rétention uniquement des principes stables trans-scénarios.

### 4.3.3 Structure et exemples de contenu

**Mode d'organisation** : groupé par dimension pour faciliter la récupération.

| Dimension | Exemple de stockage | Explication |
| :------- | :--------------------------------- | :----------------------- |
| Style de communication | Préférence utilisateur : concis et direct, sans formules de politesse | Ne pas sortir "J'espère que cela peut vous aider" |
| Norme de sortie | Besoin utilisateur : code prioritaire, avec méthode de vérification | Ne pas donner seulement le plan, donner "comment vérifier" |
| Mode de décision | Décision utilisateur : risques en premier, exposer d'abord les risques complets | D'abord énumérer les risques, ensuite parler des bénéfices |
| Orientation esthétique | Esthétique utilisateur : narration froide, refuse les résumés de style IA | Laisser un blanc à la fin de la nouvelle, ne pas faire de synthèse |

**Contraintes clés** :
- Pas de scénarios spécifiques : par exemple, "comment devrait être la création de nouvelles courtes" devrait aller dans L3.
- Pas d'étapes opératoires : par exemple, "supprimer le résumé à la troisième étape" devrait aller dans la Compétence.
- Chaque entrée doit être une abstraction du jugement de l'utilisateur, et non une description du résultat de la tâche.

### 4.3.4 Interface avec d'autres couches

- **Appelé par L1 en prévision** : au démarrage d'une tâche, l'Agent lit les principes de dimension pertinents dans L2 et les intègre à la liste d'évitement des pièges.
- **Écrit par contrôle intégral** : lorsqu'une règle esthétique reçoit 2 retours, l'Agent la descend dans L2.
- **Audité par revue en boucle fermée** : chaque revue vérifie si L2 est obsolète ou s'il y a de nouveaux principes à ajouter.

---

## 4.4 L3 : Modèles Principaux de Scénario — "Mot de passe de succès" des tâches

### 4.4.1 Positionnement

L3 stocke les **lois de succès** pour des types de tâches spécifiques. Il répond à : "Pour faire ce type de tâche, quelle loi faut-il suivre pour être correct."

L2 est un "axiome" trans-scénario, L3 est un "théorème" scénario-spécifique. Une entrée L3 devrait être une sagesse condensée d'un type de tâche, et non un manuel d'instructions.

### 4.4.2 Stockage physique

- **Emplacement** : zone principale de `memory`, sous L2, divisée par types de tâches.
- **Permission de mise à jour** : même que L2, écrit par descente intégrale ou revue en boucle fermée, après ta confirmation.
- **Contrôle de capacité** : 1-3 lois par type de tâche, chaque loi expliquant en une phrase la "contradiction la plus centrale ou le principe le plus critique dans ce scénario".

### 4.4.3 Structure et exemples de contenu

**Mode d'organisation** : divisé par types de tâches, chaque noeud contenant 1-3 entrées.

```
[L3·Modèles Principaux de Scénario]

- Nouvelle courte :
  • La définition émotionnelle prime sur le développement du scénario
  • Laisser un blanc à la fin, ne pas faire de résumé axiologique
- Revue de code :
  • D'abord vérifier la rationalité de l'architecture et les conditions aux limites, après vérifier les normes de nommage
  • Pour chaque type de problème, il faut donner des suggestions de modification, ne pas seulement signaler l'erreur
- Dépannage de problèmes :
  • D'abord localiser la cause profonde dans les journaux, ne pas deviner par l'expérience
  • Les points incertains sont annotés "à vérifier", ne pas tirer de conclusions hâtives
- Conception d'architecture :
  • D'abord définir les limites du système et le flux de données, ensuite choisir la pile technologique
  • Évaluer l'extensibilité et les modes d'échec, ne pas écrire seulement le chemin heureux
```

**Contraintes clés** :
- La "loi" doit pouvoir guider la conception de compétences : si une entrée L3 ne permet pas à la compétence d'écrire des éléments de vérification, elle n'est pas assez abstraite ou essentielle.
- Interdiction d'avoir des noms de fichiers, noms d'outils et autres informations sujettes à expiration.
- Interdiction d'avoir des étapes opératoires comme "ce qu'il faut faire à la troisième étape".

### 4.4.4 Relation avec la couche de compétences

L3 est la **norme de conception** de la couche de compétences. Une compétence devrait être un pipeline d'exécution dérivé des lois L3 correspondantes. Lorsque la revue en boucle fermée découvre des problèmes dans les résultats d'exécution, vérifier d'abord les étapes de la compétence (couche d'exécution). Si la compétence n'est pas fautive, vérifier ensuite si la loi L3 a été mal extraite (couche de stratégie).

---

## 4.5 Tableau de contrôle intégral — "Régulateur de seuil de rétrocation" du système

### 4.5.1 Positionnement

Le tableau de contrôle intégral est le support physique du deuxième concept cybernétique (contrôle intégral). C'est un journal structuré léger, enregistre les **schémas d'erreurs récurrents et leur statut de disposition**.

### 4.5.2 Stockage physique

- **Emplacement** : zone principale de `memory`, noeud indépendant.
- **Opération** : maintenu automatiquement par l'Agent lors de la réception de rétroactions négatives, pas besoin de gestion manuelle.

### 4.5.3 Structure de données

| Champ | Explication | Exemple |
| :------- | :------------------------------------------------ | :----------------- |
| Catégorie | Classe A (viole L2) / Classe B (viole L3) / Classe C (mauvaise étape de compétence) | Classe B |
| Modèle d'erreur | Résumé abstrait en ≤8 caractères | "Conclusion IA fin nouvelle" |
| Date de première occurrence | Date de la première occurrence | 2026-05-10 |
| Nombre cumulé | Nombre cumulé actuel | 2/2 |
| Seuil | Par défaut 2 | 2 |
| Descente effectuée | Si déjà écrit dans L2/L3/Compétence | Oui |
| Cible de descente | Où est descendu | L3·Nouvelle courte |

### 4.5.4 Logique de fonctionnement

Lorsque l'utilisateur donne une rétroaction négative → l'Agent l'abstrait en modèle d'erreur → recherche dans le tableau un modèle similaire :
- Existe et a atteint le seuil : indiquer à l'utilisateur que ce modèle a déjà été descendu.
- Existe et n'a pas atteint le seuil : nombre cumulé +1. Si le seuil est atteint, descendre automatiquement et confirmer.
- N'existe pas : créer une nouvelle entrée, nombre à 1.

À chaque revue en boucle fermée, l'Agent doit sortir l'état complet de ce tableau.

---

## 4.6 Couche d'Exécution : Compétences (Skill) — Pipeline opérationnel

### 4.6.1 Positionnement

La couche des compétences est la **main et le pied** du système, responsable de toutes les opérations spécifiques. Elle comprend trois types de compétences :

| Type | Exemple | Concept cybernétique correspondant |
| :------- | :----------------------------------------------------------- | :----------------- |
| Méta-compétences | `feedforward_startup`, `delivery_gate`, `control_loop_review` | Prévision, auto-surveillance, boucle |
| Compétences de tâches | `short_story_writer`, `code_reviewer` etc. | Guidé par L3 |
| Compétences de maintenance | `user_profile_maintainer` | Maintenance du profil |

### 4.6.2 Norme de conception des compétences

Chaque compétence doit inclure les champs suivants (exemple avec `short_story_writer`) :

```
- Condition de déclenchement : lorsque l'utilisateur demande d'écrire une nouvelle courte
- Dépendance L3 : [L3·Nouvelle courte] définition émotionnelle prioritaire, blanc à la fin
- Injection de prévision : charger les orientations esthétiques L2 + lois L3 correspondantes
- Étapes d'exécution :
  1. Confirmer le thème et le nombre de mots
  2. Définir le ton émotionnel (froid/chaud/suspense)
  3. Écriture (les trois premières phrases établissent l'ambiance visuelle)
  4. ...
- Étapes d'auto-examen : appeler delivery_gate pour le contrôle des cinq portes
```

Aucune compétence ne peut coder en dur "préférences utilisateur" dans ses étapes. Les préférences doivent être injectées par prévision. Cela garantit que lorsque vous modifiez un principe esthétique dans L2, toutes les compétences prennent effet automatiquement sans modification individuelle.

### 4.6.3 Versionnage des compétences

Chaque nom de compétence porte un suffixe de version (par exemple `_v1`). En cas de mise à jour, créer une nouvelle version, l'ancienne restant à titre de référence. Le versionnage permet de revenir en arrière à tout moment et facilite les comparaisons de modifications lors des revues en boucle fermée.

---

## 4.7 Vue d'ensemble du flux de données : comment une tâche parcourt toutes les couches

Exemple avec "Écrire une nouvelle courte" pour montrer le flux de données complet :

```
Task: Écrire nouvelle courte
  │
  ├─[1. Démarrage de prévision] Compétence : feedforward_startup
  │    ├─ Lire L1 : confirmer les règles de prévision
  │    ├─ Lire L2 : extraire "narration froide, refus résumé IA"
  │    ├─ Lire L3 : extraire "nouvelle : définition émotionnelle prioritaire, blanc à la fin"
  │    ├─ Rechercher archives : dernière correction "ambiance insuffisante"
  │    └─ Sortir "liste de démarrage" → attendre confirmation
  │
  ├─[2. Exécution de tâche] Compétence : short_story_writer
  │    ├─ Injecter les éléments d'évitement de la liste de prévision
  │    ├─ Organiser le contenu selon les lois L3
  │    └─ Compléter le brouillon
  │
  ├─[3. Auto-examen de livraison] Compétence : delivery_gate
  │    ├─ P0 : contrôle des exigences strictes
  │    ├─ P1 : traces IA + intégrité structurelle
  │    ├─ P2 : propreté de livraison
  │    └─ Tout passe → sortir la version finale
  │
  └─[4. Rétrocation utilisateur → contrôle intégral]
       ├─ Rétrocation négative → abstraire en modèle
       ├─ Écrire dans le tableau de contrôle intégral
       ├─ Si cumulé ≥2 → descendre dans L2/L3/Compétence
       └─ Attendre le prochain appel de prévision de tâche
```

**Revue en boucle fermée (exécution périodique)** :
1. Déclencheur (utilisateur dit "décollage").
2. L'Agent appelle `control_loop_review`.
3. Par les quatre standards de L1 + processus standard d'analyse des causes profondes, auditer tous les L2, L3, compétences, tableau intégral.
4. Sortir le plan de rectification.
5. Appeler `user_profile_maintainer` pour mettre à jour le profil.

---

## 4.8 Mécanisme d'auto-préservation de l'architecture

Pour éviter que le système ne dérive ou n'enflamme lu-même, trois règles d'auto-préservation sont intégrées :

1. **L1 ne peut être modifié de manière autonome** : si l'Agent veut modifier L1, il doit proposer et attendre la confirmation.
2. **Limite supérieure des entrées L2/L3** : chaque catégorie au-delà de 10/3 entrées, demander à l'utilisateur de nettoyer les éléments obsolètes.
3. **Versionnage et abolition des compétences** : les anciennes compétences sont archivées ou supprimées une fois confirmées inutiles, éviter l'accumulation.

---

## 4.9 Conclusion du chapitre

Ce chapitre présente une architecture de système complète, avec **quatre concepts cybernétiques comme couche logique, mémoire et compétences comme couche physique, flux de données comme nerf opérationnel**. Il s'agit essentiellement d'un "pattern de conception", une redéfinition du système de mémoire et de compétences de l'Agent, et non l'ajout de nouvelles fonctionnalités.

**Dans le prochain chapitre, nous traduirons cette architecture en commandes de déploiement directement exécutables, étape par étape, pour construire un moteur cybernétique complet sur ton Agent.**