# Chapitre 3 : Théorie Fondamentale — Quatre Concepts Cybernétiques en Détail

Ce chapitre explique en détail les quatre concepts que la théorie cybernétique de Qian Xuesen fournit pour l'ingénierie pratique. Ils sont la source du pouvoir de l'architecture complète.

## 3.1 Premier Concept : Prévision — Éviter les Erreurs Avant Qu'Elles Ne Surviennent

### 3.1.1 Problème de Fondation

Les agents modernes sont des systèmes à réactions pures : vous donnez un ordre, ils exécutent. S'ils n'avaient pas appris vos préférences ou n'étaient pas au courant des pièges connus dans cette scène, ils vont presque certainement les répéter. Chaque fois que vous devez dire "je ne veux pas cela, faites-le comme ça", vous perdez du temps et accumulez de la frustration.

### 3.1.2 Idée Cybernétique

La théorie de la commande predictive chaque avance : maximiser l'information sur le "futur proche" au moment de la prise de décision, et ajuster à l'avance le plan. Par analogie : les bonnes entreprises n'attendent pas que les clients se plaignent pour chercher les problèmes, elles construisent des mécanismes de détection préalable ; les bons pilotes ne réagissent pas seulement aux scénèmes courants, ils anticipent déjà les problèmes possibles.

### 3.1.3 Mise en œuvre pour les Agents

Bloc de Capacités de Prévision (celui que nous construirons pour le "skill" `feedforward_startup`) :

**Quand déclencher** : Avant chaque nouvelle tâche, exécutez-les automatiquement.

**Étapes d'exécution** :

1. **Identifier le type de tâche** : Classifiez-la dans les catégories connues (création d'histoire courte / sortie de code / conception d'architecture / dépannage / quotidien Q&A / autre)
2. **Lire les principes pertinents L2** : Récupérer les entrées de [Logique Fondamentale Utilisateur L2] liées à la tâche actuelle de la mémoire, prendre ≤3 articles
3. **Lire les modèles correspondants L3** : Récupérer les entrées de [Motifs Fondamentaux de Scénario L3] correspondant au type de tâche actuel de la mémoire
4. **Récupérer les leçons historiques** : Si la plate-forme prend en charge la récupération de session, trouver les enregistrements de correction de la dernière tâche similaire
5. **Sortir la liste de contrôle de lancement** : Combiner les éléments ci-dessus et générer une "liste de contrôle d'évitement des pièges"

### 3.1.4 Forme de Sortie Requise

Un format de sortie structuré pour la liste de contrôle de lancement de prévision :

```
Type de tâche : [Identifié]
Motifs de scénario L3 : [
  - Modèle A
  - Modèle B
]
Principes utilisateur L2 : [
  - Principe Q
  - Principe R
]
Leçons historiques : [
  - [Si détecté dans l'enregistrement historique, remplir ; sinon, écrire "pas d'enregistrement"]
]
Prédiction de risque (niveau P) :
- P0 [Risque bloquant dur] : [
  - Ce qui doit être fait correctement cette fois,
  - Ce qui ne doit pas être fait
]
- P1 [Probable déviation haute] : [
  - Ce que vous avez nui par le passé
]
- P2 [Direction d'optimisation] : [
  - Ce qui peut être fait mieux
]
Liste d'évitement des pièges (une phrase) :
[Comprimé en 1-2 phrases]
```

### 3.1.5 Attente de Réponse Utilisateur

Au lieu de devoir attendre que vous corrections les erreurs après qu'elles se produisent, l'agent **proactivement sort la liste de contrôle des pièges probables et demande votre confirmation.** Les trois situations de traitement standard :

- Utilisateur dit "faire directement" ou "débuter" → exécuter immédiatement avec la liste de contrôle
- Utilisateur propose des modifications → ajuster la liste de contrôle puis exécuter
- Pas de réponse pendant 30 secondes → commencer l'exécution

### 3.1.6 Comment Vérifier qu'Il Fonctionne

- Après lancer un nouveau projet ou une nouvelle tâche, l'agent peut-il rappeler proactivement ce que vous avez nui par le passé ?
- Dans les scènes P0 à haute priorité, l'agent peut-il réellement éviter ces erreurs dans la sortie ?
- Si le type de tâche était vu pour la première fois, l'agent peut-il le dire franchement et demander plus d'informations (au lieu de deviner aveuglément) ?

## 3.2 Deuxième Concept : Contrôle Intégral — Atteindre des Seuils de Feedback Stables

### 3.2.1 Problème de Fondation

Dans la réalité, il y a du bruit dans le feedback utilisateur. Parfois, vous vous plaignez de quelque chose qui est en fait occasionnel ; parfois, vous soulevez mot d'un même problème plusieurs fois parce que vous voulez vraiment le solidifier. Comment l'agent établit-il la distinction entre "un incident isolé, ne changez pas trop de règles" et "une préférence réelle à long terme, devez réellement changer" ?

Les approches sophistiquées mais mauvaises sont : une plainte change tout (oscillation) ; ou une plainte n'a aucun effet (trop lent).

### 3.2.2 Idée Cybernétique

Dans la théorie du contrôle, l'intégrateur est l'élément clé du contrôle de rejet de perturbation. Il accumule l'erreur (déviations de la consigne) et n'agit que lorsque l'accumulation dépasse un seuil. Cela transforme :
- "Réagir chaque fois que l'erreur se produit" en "intervenir après N fois"
- "Filtrer les fluctuations à haute fréquence en reconnaissant la tendance lente de fond"

L'essence est : **Séparer le bruit aléatoire des préférences récurrentes, et ne changer les règles que sur la base de tendances.**

### 3.2.3 Mise en œuvre pour les Agents

Technique de Tableau de Contrôle Intégral (créé et maintenu dans la mémoire) :

```[Tableau de Contrôle Intégral]
| Catégorie | Motif d'Erreur (≤8 caractères) | Date Première | Compte Cumulatif | Seuil(2) | Sunk | Cible de Sinking (Sinking Target) |
| --------- | ------------------------ | ---------- | ---------------- | --------- | ---- | -------------- |
| (Vide, à remplir) | | | | | | |
```

**Règles de Maintenance** (exécuté automatiquement par l'agent) :

Lorsqu'il reçoit votre feedback négatif :

1. **Classification de l'erreur** :
   - Type A : Violation de [Logique Fondamentale Utilisateur L2]
   - Type B : Violation de [Motifs Fondamentaux de Scénario L3]
   - Type C : Étapes de compétence manquantes ou erreurs d'exécution
2. **Écriture/Mise à jour** :
   - Même entrée de modèle → compte +1
   - Nouvelle entrée → créer et définir le compte à 1
3. **Jugement de Sinking (exécution automatique)** :
   - Compte = 2 et "Sunk" est non → enfoncer automatiquement (sink)
   - Écrire la règle dans l'emplacement cible (L2, L3 ou compétence spécifique)
   - Mettre à jour "Sunk" à oui
   - Confirmer avec vous : "Le motif d'erreur a eu lieu 2 fois, je l'ai enfoncé vers [Emplacement cible], êtes-vous d'accord ?"

### 3.2.4 Valeurs et Risques des Paramètres

Le seuil par défaut est **2**. Signification : chaque préférence récurrente doit être signalée ≥2 fois avant d'être solidifiée en règle formelle.

- **Pourquoi 2 et non 1 ou 3 ?**
  - 1 : trop sensible, bruit élevé, facile à l'oscillation
  - 3 : trop lent, l'utilisateur peut s'ennuyer de dire la même chose plusieurs fois et perdre confiance
  - 2 : équilibre entre sensibilité et stabilité, test empirique recommandé

- **Rendez le seuil ajustable** : un paramètre "Seuil(2)" dans la table, ajustable ultérieurement après beaucoup de données d'observation sur "combien de fois un utilisateur répète pour indiquer que c'est une vraie préférence"

### 3.2.5 Comment Vérifier qu'Il Fonctionne

- Chaque fois que vous vous plaignez, l'agent peut-il classifier et enregistrer dans la table ?
- Après la deuxième plainte sur le même problème, l'agent peut-il proposer proactivement de l'enfoncer (sink) ?
- Après l'enfoncement, ce problème ne se produit-il plus réellement ?

## 3.3 Troisième Concept : Décomposition Hiérarchique — Garantir un Rapport Signal/Bruit Élevé de la Mémoire

### 3.3.1 Problème de Fondation

"La mémoire se transforme en poubelle" est un goulot d'étranglement très rencontré. Au début, c'est propre et facile à utiliser ; progressivement, différentes sources d'information, différentes étapes de détail, règles temporaires et définitions à long terme sont mélangées, et l'agent lui-même ne peut plus distinguer ce qui est utile et ce qui est bruit. Le rapport signal/bruit chute, le comportement devient instable, et le collecteur de mémoire devient un problème à nettoyer lui-même.

### 3.3.2 Idée Cybernétique

L'ingénierie cybernétique de Qian Xuesen distingue rigoureusement les **trois niveaux** de représentation de l'information dans les systèmes de commande :

- **L1 — Cadre Méta-cognitif (Constitution)** : Définit l'ensemble du système de règles de fonctionnement et de méthodes de prise de décision, ne peut pas être modifié indépendamment
- **L2 — Pourquoi** : Fondement théorique, modèle de conception, raison "pourquoi le faire ainsi"
- **L3 — Comment** : Étapes de mise en œuvre, méthodologies opératoires, canevas, listes de contrôle "comment faire"
- **L0 — Données** : Entrées brutes, paramètres, données de l'environnement

Sans cette séparation nette, n'importe quel système de commande deviendra un non-sens d'information mélangée.

Dans notre architecture de notre agent :

- La mémoire doit stocker seulement le "pourquoi" : les principes de jugement, les lignes directrices, les règles de la loi
- Les compétences doivent stocker seulement le "comment" : les étapes opératoires, les listes de contrôle, des canevas de travail
- Ne jamais choisir la mauvaise position

### 3.3.3 Mise en œuvre pour les Agents

Règles de Garantie de Pureté des Couches :

1. **Entièrement Séparé au Niveau du Stockage** :
   - `memory` ne stocke que les principes, modèles, définitions ne répondant jamais aux questions "comment exécuter"
   - `skill` ne stocke que les étapes opératoires, canevas de travail ne répondant jamais aux questions "pourquoi le faire ainsi"

2. **Détecter la Confusion Pendant l'Examen et Corriger Suivant la Catégorie** :
   - Scannez toutes les entrées de mémoire : si vous trouvez "première étape X, deuxième étape Y" → Poussez vers les compétences
   - Scannez les compétences : si vous trouvez des définitions de préférences utilisateur ou l'explication de principes → Déplacez vers L2 ou L3
   - Faites-le une fois par : le système reste propre

3. **Rappeler les Règles avec un Concept de Constitution** :
   - Le cadre méta-cognitif L1 contient une règle de niv : "Mémoire et compétences ne peuvent pas être mélées entre le pourquoi et le comment."
   - L'agent suit cette règle lors de l'écriture ou la correction

### 3.3.4 Exemples de Conduite vs Erronés

**Correct** :

```memory
[Logique Fondamentale Utilisateur L2]
- Esthétique : Je préfère le récit sobre et rejette les résumés style IA.
```

```skill
[Compétence de Récit Court]
1. Entrée : thème, tonalité émotionnelle, personnages
2. Lire l'esthétique L2 avant d'écrire
3. Abstraction de scène et mise en place (laisser de l'espace)
4. Contrôle de la tonalité pour atteindre la tonalité émotionnelle
5. Contrôle de la fin : ne pas ajouter de réflexions ou résumés
```

**Erroné** (confusion de mémoire) :

```memory
[Logique Fondamentale Utilisateur L2]
- Écrire : D'abord penser à la scène (étape opératoire) ; puis écrire le premier paragraphe ; puis...
```

**Erroné** (confusion de compétence) :

```skill
[Compétence de Récit Court]
Rappel : l'utilisateur ne veut pas de fins avec des résumés style IA (c'est un principe, ne pas mettre ici)
```

### 3.3.5 Comment Vérifier qu'Il Fonctionne

- La mémoire ne contient-elle pas d'instructions opératoires étape par étape ?
- Les compétences ne contiennent-elles pas de terminologie de principe abstrait (comme "esthétique", "rationnel") ?
- Lorsque vous scannez la mémoire, pouvez-vous clairement dire "ceci répond à un pourquoi" ?

## 3.4 Quatrième Concept : Auto-surveillance — Porte de Livraison Auto-Inspection Avant Sortie

### 3.4.1 Problème de Fondation

Les agents sont naturellement visqueux : les formats de code sont complètement faux, des clichés AI comme "En résumé" et "Il est à noter" sont restés dans la sortie, des incohérences logiques sont négligées. Vous devez chercher ces erreurs par vous-même et retourner pour correction, ce qui consomme du temps et de l'énergie.

### 3.4.2 Idée Cybernétique

La cybernétique moderne met l'accent sur **le deuxième niveau de feedback** : le système a ses propres mécanismes de surveillance et de refus de sortie de produits défectueux. L'architecture de l'Agile, l'inspection de qualité avant livraison, les tests automatisés sont tous des applications de cette idée.

### 3.4.3 Mise en œuvre pour les Agents

Porte de Livraison à 5 Fosses (livrée par la compétence `delivery_gate`) :

**Cadre d'Action** : Avant toute sortie finale, l'agent ne livre qu'après avoir passé les 5 fosses. Chaque fosse correspond à un niveau de priorité.

| Fosse | Niveau Priorité | Contenu de Vérification | Si Non Passé |
| :--- | :--- | :--- | :--- |
| **Première Fosse** | P0 Blocage dur | Exigences dures : nombre de mots, format, interdictions, inclusions obligatoires | Bloquer la livraison, corriger en interne, redémarrer |
| **Deuxième Fosse** | P0 Blocage dur | Exactitude factuelle : logique de code, données référencées, noms de fichiers, chemins | Marquer comme "en attente de vérification", ne pas inventer |
| **Troisième Fosse** | P1 Priorité haute | Épuration des traces IA : phrases cliché comme "En résumé", "En tant qu'IA", etc. | Forcer la suppression, redémarrer |
| **Quatrième Fosse** | P1 Priorité haute | Intégrité structurelle : la chaîne logique est-elle close, des chapitres/étapes manquent-ils | Compléter, redémarrer |
| **Cinquième Fosse** | P2 Optimisation | Purification de livraison : il y a des commentaires internes, notes de révision, excès de balises | Purifier le contenu, puis passer |

**Processus Plus Concret** :
1. Avant de livrer le résultat final, l'appeler explicitement par "delivery_gate"
2. Il vérifie dans l'ordre requis, corrige immédiatement les erreurs, puis recheck la fosse
3. Si échoue encore la fosse, restrtuure pour refaire, ne continue pas aveuglément
4. Ce n'est que lorsque les 5 fosses sont toutes passées que le contenu peut être sorti

### 3.4.4 Sortie de Fosse la Plus Élevée

Une fois la porte de livraison passée, l'agent doit explicitement sortir :

```
- P0 Exigences dures ✓
- P0 Exactitude factuelle ✓
- P1 Traces AI ✓
- P1 Intégrité structurelle ✓
- P2 Purification de livraison ✓

Conclusion : Livraison autorisée / Doit être corrigée et re-passée
```

### 3.4.5 Pourquoi 5 Fosses et Pas plus/Moins ?

- P0 : les erreurs "ne pas tolérer" (format, exactitude), doivent bloquer la sortie
- P1 : les erreurs "ne pas vouloir voir" (clichés AI, trou structurel), doivent corriger
- P2 : les erreurs "faire mieux s'il y a le temps" (propreté, fibres intégrales), peuvent passer après purification

Si beaucoup de P0 se produisent régulièrement, le problème est L1/L2/L3 désaligné, l'agent ne comprend pas vraiment ce que vous voulez—solvable par "examen en boucle fermée".

### 3.4.6 Comment Vérifier qu'Il Fonctionne

- Le ratio de clichés AI est-il significativement bas ?
- Le taux d'erreurs basiques semble-t-il être nettement plus bas qu'avant (comme des chemins ou noms de fichiers mal écrits) ?
- Y a-t-il des cas où vous trouvez encore des incohérences logiques flagrantes (cas d'échec de la P1) ?

## 3.5 Résumé

Les quatre concepts cybernétiques, en association, créent un agent capable de :

- Charger activement vos préférences au début des tâches (prévision)
- Ne changer les règles que sur des ensembles de feedback stables (contrôle intégral)
- Garder la mémoire propre à long terme (décomposition hiérarchique)
- Livrer moins d'erreurs et de bruit (auto-surveillance)

Le chapitre suivant est leur incarnation concrète dans l'architecture système.
