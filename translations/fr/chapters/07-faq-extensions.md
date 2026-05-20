| Chapitre 7 : Questions fréquentes et réflexions étendues

C'est le dernier chapitre du tutoriel, couvrant deux sections : les obstacles typiques possibles lors du déploiement et de l'exécution ainsi que leurs méthodes de résolution, et les idées d'extension de ce cadre à des scénarios plus complexes.

---

## 7.1 Questions liées au déploiement

### Q1 : Après avoir écrit L1, l'Agent ne suit pas les cinq principes fondamentaux, que faire ?

**Causes courantes** :
- La mémoire n'est pas en tête, couverte ou diluée par les écritures ultérieures
- La fenêtre de contexte est surchargée par de longues conversations, L1 est tronqué
- La plate-forme Agent a un retard dans l'injection de mémoire

**Étapes de diagnostic** :
1. Faire répéter les cinq principes fondamentaux L1 à l'Agent. Si incapable de répéter intégralement, indique un problème d'écriture ou de lecture de mémoire.
2. Si répété correctement mais toujours non exécuté, répéter une phrase au début d'une nouvelle session : `Avant le début de cette session, tout d'abord revoir les cinq principes fondamentaux du cadre métacognitif L1 dans memory.`
3. Si le problème persiste, envisager de simplifier les règles centrales de L1 en une ou deux phrases, et de les écrire dans la zone "instruction système" ou "prompt système" de la plate-forme (si supporté), double assurance.

---

### Q2 : L'Agent dit qu'il n'a pas de fonction `skill_manage` ou d'outils de gestion de compétences similaires

** deux options** :

**Option A (recommandée)** : Simuler des compétences avec la mémoire.
- Dans memory créer des entrées marquées `[Skill-NomCompétence]`, le contenu est les étapes d'opération de la compétence.
- Dans L1 ajouter la règle : `Chaque fois qu'il faut exécuter une compétence, rechercher depuis memory l'entrée [Skill-*] correspondante et exécuter strictement selon les étapes.`
- Inconvénient : occupe l'espace de mémoire ; avantage : logique complète.

**Option B** : Simplifier l'architecture, utiliser seulement L1 + L2 + L3 + tableau intégral.
- Abandonner l'automatisation de la couche de compétences, changer pour que vous rappeliez manuellement au début de la tâche à l'Agent de suivre les étapes d'auto-contrôle.
- Convient à l'utilisation légère ou à la collaboration à court terme.

---

### Q3 : Lors de l'initialisation L2/L3, l'extraction de l'Agent de moi est complètement inexacte

Cela ne signifie pas que l'architecture a un problème, mais indique exactement que la compréhension précédente de l'Agent de vous a un biais — ce est précisément le problème que ce tutoriel vise à résoudre.

**Méthode de traitement** :
- N'acceptez pas intégralement l'extraction de l'Agent. Corrigez ligne par ligne, traitez-le comme une "dialogue de calibration".
- Après correction, dites clairement à l'Agent : `Votre compréhension précédente de moi a un biais, j'ai déjà corrigé le contenu de L2/L3. Dans la mémoire, veuillez vous baser sur ma correction.`
- Dans les revues en boucle fermée ultérieures, l'Agent mettra automatiquement à jour la compréhension. Habituellement après 2-3 revues, la précision de L2/L3 s'améliorera significativement.

---

### Q4 : Les entrées dans le tableau de contrôle intégral sont de plus en plus nombreuses, que faire ?

C'est un signal que le système fonctionne normalement — indique que vous collaborez effectivement continuellement, l'Agent apprend continuellement.

**Stratégie de maintenance** :
1. À chaque revue "décoller", vérifier le tableau intégral.
2. Pour les entrées déjà stagnées et fonctionnant stablement, peuvent être archivées comme "solidifiées", réduire le nombre d'entrées actives.
3. Pour les entrées mal classées ou non applicables, supprimer manuellement.

```
Déplacer dans le tableau de contrôle intégral "fin résumé IA" (stagné, sans réapparition depuis 6 mois) vers la zone d'archive, plus compter dans les entrées actives.
```

---

### Q5 : Après déploiement, la liste d'anticipation est trop longue, affectant l'efficacité

La longueur de la liste d'anticipation devrait être proportionnelle à la complexité de la tâche. Si des tâches simples aussi sortent une longue liste, méthode d'ajustement :

**Instruction de simplification** :
```
Modifier feedforward_startup : pour les tâches simples (comme traduction, question-réponse courte), la liste d'anticipation compressée en une ligne — "évitement : xxx". Seules les tâches complexes sortent la liste de démarrage complète. Le jugement de tâches simples est fait par vous lors de l'exécution et me le dire.
```

Vous pouvez aussi à tout moment au début de la tâche dire "sauter la liste et faire directement", l'Agent devrait exécuter en cela.

---

## 7.2 Questions fréquentes lors de l'exécution

### Q6 : L'Agent deux fois consécutives je n'ai pas corrigé l'erreur de même type, mais a déclenché la stagnation

**Diagnostic direct** :
```
S'il vous plaît sortir l'état complet actuel du tableau de contrôle intégral.
```

**Causes possibles** :
- L'Agent n'a pas correctement classé votre premier feedback (comme classé dans type D accidentel).
- L'Agent a classé deux feedbacks comme modèles d'erreur différents, plutôt que la même entrée.

**Méthode de correction** :
```
Unifiez [description des deux feedbacks] comme un même modèle d'erreur : "[nom de modèle ≤8 caractères]". Mettez à jour le tableau intégral et vérifiez si le seuil de stagnation est atteint.
```

---

### Q7 : L'Agent dans le rapport de la barrière de livraison passe toujours "tous", mais j'ai découvert des problèmes

Cela indique que les éléments de contrôle de la barrière ne sont pas assez détaillés, ou que l'Agent exécute la barrière de manière négligente.

**Méthode de renforcement** :
1. Problème découvert indique immédiatement : `delivery_gate la troisième barrière n'a pas découvert "il est à noter" ce cliché. Expliquer la raison, et mettre à jour les standards de détection de la barrière.`
2. Si des problèmes spécifiques répètent, dans la barrière ajouter des règles de contrôle ciblées :
```
Dans les éléments de contrôle de la troisième barrière de delivery_gate ajouter : "contient-il 'd'une certaine manière', 'on peut dire' etc. mots de qualification flous ? Découvrir à supprimer."
```

---

### Q8 : La sortie de revue en boucle fermée est trop modèle, manquant d'analyse des causes profondes de véritable valeur

Cela peut être parce que l'Agent n'a pas rencontré de véritables problèmes pendant une phase plus longue, ou parce que le paramétrage du processus cause l'Agent à tendre à "remplir le formulaire" plutôt que "penser".

**Méthode d'activation** :
- Lors de "décoller", ajouter une pointe spécifique : `cette revue focalise sur [un problème spécifique], analyser en profondeur les causes profondes.`
- Si longtemps sans problème, dire à l'Agent : `Si la boucle fermée ne découvre aucun problème nécessitant correction, peut être raccourcie en 3 phrases brèves, pas besoin des neuf étapes complètes.`

---

### Q9 : Je crains que la mémoire de l'Agent continue à écrire plus, finalement dépassant la limite

C'est un problème déjà considéré dans la conception de l'architecture. Trois mécanismes intégrés contrôlent l'expansion :

1. **La séparation des couches elle-même est une conception anti-expansion** : Le volume des principes et des lois est beaucoup plus petit que les étapes d'操作 et les cas.
2. **Limite supérieure d'entrées L2/L3** : L2 limite supérieure 10 entrées, L3 chaque scène limite supérieure 3 entrées. Au-delà demander le nettoyage.
3. **Étape de purification dans la revue en boucle fermée** : Chaque revue vérifier et migrer le contenu confus.

Si vous craignez toujours, pouvez nettoyer manuellement périodiquement :
```
Lister dans memory les entrées non accédées depuis 30 jours, évaluer si elles peuvent être supprimées.
```

---

## 7.3 Réflexions étendues

### 7.3.1 De单 Agent à collaboration multi-Agent

Le cœur de cette architecture — quatre concepts de cybernétique + séparation des couches — s'applique naturellement aux scénarios multi-Agent.

**Idées d'extension** :
- **Agent principal** (orchestrateur) : détient le cadre métacognitif L1, responsable de la distribution de tâches et du contrôle qualité.
- **Sous-Agent** (exécuteur) : détient各自的 lois L3 de scènes spécifiques et compétences correspondantes.
- **Zone de mémoire partagée** : L2 logique sous-jacente de l'utilisateur visible à tous les Agents, garantir que différents rôles suivent une esthétique et des principes unifiés.
- **Tableau intégral unifié** : Tous les feedbacks négatifs de tous les Agents convergent vers le même tableau intégral, l'Agent principal exécute les décisions de stagnation.

C'est essentiellement mapper la frontière "stratégie/exécution" dans la "séparation des couches", en frontière physique "Agent principal / sous-Agent".

---

### 7.3.2 Introduction d'autres cadres théoriques

Le tutoriel utilise toute la théorie de l'ingénierie cybernétique de Qian Xuesen comme cadre sous-jacent. Mais L1 n'est pas fermé — votre capacité de transfert d'apprentissage peut continuellement introduire de nouvelles théories pour le système via l'étape "proposition de migration".

Les tentatives d'extension déjà apparues dans la section commentaires :

| Théorie introduite              | Direction d'application         | Extension possible correspondant à L1                         |
| :-------------------- | :--------------- | :----------------------------------------- |
| Gestion active des investissements        | Décision et allocation de ressources   | Dans L1 ajouter le principe "rééquilibrage dynamique"                 |
| Inférence bayésienne            | Jugement sous incertitude | Dans le contrôle intégral ajouter la correction "probabilité antérieure" du poids de feedback     |
| Critère de Kelly + théorie de l'information de Shannon | Évaluation de la valeur de l'information     | Dans l'auto-surveillance ajouter le contrôle de "densité d'information"               |
| Principes d'invention TRIZ         | Résolution de conflits         | Dans l'analyse des causes profondes ajouter le jugement "contradiction physique vs contradiction technique" |

Méthode d'introduction de nouvelles théories : dans la revue "décoller", lorsque l'Agent propose une proposition de migration, ou quand vous avez une idée claire, dire activement :
```
Je veux introduire dans L1 [nom théorique], le principe est [découverte en une phrase]. Veuillez concevoir comment ajouter une sixième règle dans le cadre des quatre concepts existants, et expliquer comment cela affecte l'exécution de Skill.
```

---

### 7.3.3 Re-réflexion des limites d'application du cadre

Dans la section des commentaires est apparue une mise en question qui mérite d'être prise au sérieux : **"La théorie de l'ingénierie cybernétique pour l'Agent actuel n'est peut-être pas nécessaire, ou ce n'est que d'ajouter des étapes au LLM dans le contexte, pas une contrainte forte."**

Après le déploiement complet de ce tutoriel, à cette mise en question peut être donnée la réponse suivante :

1. **"Ajouter des étapes au LLM" lui-même est une contrainte efficace**. LLM est un système promptable, les contraintes contextuelles structurées peuvent effectivement changer sa distribution de comportement. L'effet ne vient pas d'une rigidité codée en dur, mais d'un guidage structuré continu.

2. **La valeur de l'architecture n'est pas dans l'exécution unique, mais dans la stabilité à long terme**. Vue unique, vous ne donnez à l'Agent aucun cadre, seulement en vous reposant sur des instructions improvisées pouvez obtenir un résultat qualifié. Mais après 50 tâches consécutives, le système avec une architecture converge mieux, dérive moins. C'est une assurance, pas un carburant.

3. **Pas tous les scénarios n'en ont besoin**. Les conversations légères, uniques, hautement aléatoires n'ont pas besoin de cette architecture. Ses limites d'application sont : **collaboration à long terme × demande de haute précision × types de tâches avec lois résumables**. Si vous vous trouvez dans cette zone, le coût d'investissement dans le déploiement sera récupéré dans la réduction des répétitions de corrections.

---

### 7.3.4 Conditions d'auto-termination du cadre

Un système sain devrait pouvoir identifier "quand il devrait être simplifié".

**Signaux de terminaison ou de réduction de niveau** :
- Le tableau de contrôle intégral n'a pas de nouvelle entrée depuis 3 mois consécutifs (indique que la collaboration est complètement stable, ou la fréquence de collaboration a considérablement diminué).
- Chaque revue "décoller" sans découverte substantielle.
- Vous découvrez que dans la collaboration vous n'avez plus besoin de la liste d'anticipation, les préférences sont hautement internalisées.

Lorsque ces signaux apparaissent, pouvez réduire la fréquence de la boucle fermée (comme de hebdomadaire à mensuelle), ou simplifier l'architecture (comme supprimer le tableau intégral, garder l'anticipation et l'auto-surveillance).

C'est un choix de conception de l'auto-modestie du système : **il ne poursuit pas l'existence éternelle, mais une exécution efficace lorsque nécessaire, et une réduction gracieuse lorsque non nécessaire.**

---

## 7.4 Revue du tutoriel

| Chapitre     | Livraison centrale       | Point en une phrase                                       |
| :----- | :------------- | :----------------------------------------------- |
| Chapitre1 | Contexte et philosophie     | N'enseigne pas de nouvelles connaissances à l'IA, mais construit l'architecture                       |
| Chapitre2 | Conditions d'application et préparation | D'abord inventorier votre Agent et préférences                        |
| Chapitre3 | Quatre concepts de cybernétique | Anticipation évite pièges, intégral prévient oscillations, séparation des couches traite le désordre, auto-surveillance contrôle | 
| Chapitre4 | Architecture du système       | Trois couches de logique cognitive + correspondance avec stockage physique et flux de données            |
| Chapitre5 | déploiement pratique       | Six étapes d'instructions copiables, envoyer directement à l'Agent                     |
| Chapitre6 | Utilisation quotidienne et vérification | Nouveau rythme de collaboration + contrôle santé + indicateurs centraux                 |
| Chapitre7 | Questions fréquentes et extensions | Diagnostic, extension, limites d'application                             |

L'essence du tutoriel entier peut être résumée en une phrase : **vous ne faites pas une fois de l'ingénierie de prompt, mais une fois de l'ingénierie d'architecture — vous n'enseignez pas à l'Agent de nouvelles connaissances, mais utilisez la pensée de l'ingénierie des systèmes, pour lui concevoir un ensemble d'architecture interne pouvant fonctionner de manière stable, évoluer continuellement.**

---

## 7.5 Dernière étape

Le tutoriel se termine ici. Si vous avez complété le déploiement selon le chapitre 5, maintenant vous n'avez besoin de faire que trois choses :

1. **Utiliser normalement** — envoyer normalement des tâches, donner normalement des feedbacks.
2. **Revue périodique** — souvenir de dire "décoller".
3. **Ajuster si nécessaire** — rencontrer des problèmes, revenir à ce chapitre.

Votre Hermes n'est plus un outil nécessitant des corrections continuelles, mais un moteur de collaboration qui vous comprend de plus en plus, continue alignant des principes. Ce n'est pas de la science-fiction, mais l'atterrissage de la pensée de la science des systèmes du 20ème siècle dans l'architecture des Agent AI du 21ème siècle.

**Ravi d'avoir parcouru avec vous les sept chapitres complets.**