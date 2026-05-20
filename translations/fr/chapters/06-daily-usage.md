| Chapitre 6 : Utilisation quotidienne et vérification

Après l'achèvement du déploiement, ce chapitre répond à deux questions : **comment utiliser ce système chaque jour**, et **comment savoir qu'il fonctionne normalement**.

---

## 6.1 Nouveaux rythmes de collaboration quotidienne

Après le déploiement, le mode de collaboration entre vous et l'Agent subira un changement subtil mais important — vous passez de "correcteur" à "confirmeur".

| Phase | Ordre d'occurrence précédent | Ordre d'occurrence actuel |
| :--- | :--------------------------------------- | :----------------------------------------------------------- |
| Démarrage | Vous envoyez tâche → Agent fait directement | Vous envoyez tâche → Agent sort la liste de démarrage → Vous confirmez (ou dites "faire directement") → Commencer |
| Exécution | Agent sort → Vous vérifiez → Vous corrigez | Agent exécute selon Skill, injecte automatiquement les éléments d'évitement |
| Livraison | Vous vérifiez → Trouvez clichés/format → Vous dites → Il corrige | Agent passe automatiquement cinq barrières → Vous obtenez un résultat propre |
| Feedback | Vous dites une phrase → Il parfois corrige excessivement parfois ne se souvient pas | Vous dites une phrase → Il enregistre dans le tableau intégral, la deuxième fois modifie la règle |
| Revue | Vous résumez par feeling | Vous dites "décoller" → Agent exécute automatiquement neuf étapes de revue |

**Changement central** : Auparavant vous agissiez comme contrôleur de feedback dans la boucle, maintenant la plupart des boucles de feedback sont internalisées par l'Agent en anticipation et auto-surveillance.

---

## 6.2 Scénarios d'utilisation typiques et exemples de dialogue

### Scénario A : Démarrer une nouvelle tâche

**Vous dites** :
> Aide-moi à écrire un court récit sur "le dernier jour d'automne", environ 2000 mots.

**Agent exécute automatiquement** (sans instruction supplémentaire) :
1. Appeler `feedforward_startup`
2. Sort la liste de démarrage suivante :

```
Liste de démarrage
Type de tâche : création de courts récits
Lois de scène L3 : la définition émotionnelle est prioritaire sur l'intrigue, la fin laisse de l'espace sans élévation
Principes utilisateur L2 : narration froide, refus des résumés IA ; concise sans s'accumuler en adjectifs
Leçons historiques : la fois précédente "insuffisance de sensation visuelle", cette fois renforcer la description de l'environnement
Prévision des risques :
- P0 : écart de nombre de mots trop important
- P1 : fin acquiescement involontaire récapitulatif
- P2 : proportion trop élevée de dialogue causant la narration fine
Liste d'évitement des pièges : établir l'image au début, fin naturelle ne touchant pas au sujet ; narration froide tout au long, sans accumulation d'adjectifs.

(en attente de confirmation ou de dire "faire directement")
```

**Vous dites** :
> Faire directement

**Agent** : commence l'écriture, et avant la livraison passe automatiquement `delivery_gate`.

> *Si la tâche est particulièrement simple (comme "aide-moi à traduire un paragraphe"), la liste d'anticipation doit aussi être simplifiée, ne forcer pas à de longs discours. Vous pouvez随时 dire "sauter la liste et faire directement".*

---

### Scénario B : Donner des commentaires négatifs

**Vous dites** :
> Cette fois encore résumé "l'automne finira par passer", je n'aime pas.

**Agent exécute automatiquement en interne** (vous n'avez pas besoin d'instruction supplémentaire) :
1. Classification : Type A (violation du principe esthétique L2)
2. Chercher dans le tableau de contrôle intégral : si déjà entrée "fin résumé IA", +1 ; sinon créer.
3. Jugement :
   - Nombre = 1 → seulement corriger cette fois, répondre : "enregistré, cette fois corrigé."
   - Nombre = 2 → déclencher automatiquement la stagnation, répondre : "'fin résumé IA' est apparu 2 fois, je stagnerai cette règle dans L2 principe esthétique : 'refus toute forme de conclusion récapitulative de fin'. Accepté ?"

> *Plus votre feedback est spécifique (comme "fin prolixe"), plus l'Agent peut facilement abstraire en modèle d'erreur précis. Évitez les feedbacks vagues comme "mal écrit".*

---

### Scénario C : Revue quotidienne/hebdomadaire

**Vous dites** :
> Décoller

**Agent appelle automatiquement** `control_loop_review`, suit le processus en neuf étapes, finalement vous verrez quelque chose comme :

```
[Revue en boucle fermée complétée]

- Revue en anticipation : cette semaine feedforward 5 fois, toutes appelées normalement
- Stagnation intégrale : 1 stagné (fin résumé IA → L2)
- Purification des couches : aucune confusion
- Mise à niveau de la barrière : suggérer d'ajouter dans P1 l'élément de contrôle "paragraphes de dialogue continus ne dépassant pas 6 lignes", accepté ?
- Analyse des causes profondes : ... etc
- Abstraction réutilisable : suggérer créer skill : dialogue_density_check
- Proposition de migration : ce tour non nécessaire (ou : suggérer introduire la théorie de l'information de Shannon pour contrôler la densité de dialogue)
```

Vous confirmez/rejetez ligne par ligne, l'Agent écrit dans la mémoire et appelle la maintenance de profil.

---

### Scénario D : Demande d'état du système à tout moment

**Vous dites** :
> Combien de couches ta mémoire actuellement sépare ? Et stocke quoi ?

**Agent** doit répondre précisément les cinq L1, les dimensions L2, la liste de scènes L3, le nombre d'entrées du tableau intégral.

**Vous dites** :
> Quelles entrées le tableau de contrôle intégral a-t-il actuellement ?

**Agent** sort l'état actuel du tableau.

---

## 6.3 Liste de contrôle de santé du système

Chaque semaine prenez 2 minutes pour passer cette liste, assurez-vous que le système ne s'est pas dégradé silencieusement.

### Éléments d'auto-contrôle (vous n'avez qu'à observer, pas besoin d'instruction supplémentaire)

| #    | Point de contrôle   | Comportement normal                                | Signal anormal                         |
| :--- | :------- | :-------------------------------------- | :------------------------------- |
| 1    | Démarrage en anticipation | Agent sort une liste de démarrage à chaque nouvelle tâche | Agent commence directement l'exécution, a sauté la liste |
| 2    | Qualité de livraison | Livraison propre, sans clichés IA, format correct | Vous voyez encore "en conclusion" "il est à noter" |
| 3    | Contrôle intégral | Deuxième fois que vous soulevez un problème de même type, Agent propose stagnation | Troisième fois vous devez encore corriger le même problème |
| 4    | Séparation des couches | memory n'a pas d'étapes d'opération, skill n'a pas de principes | Une fois vous ouvrez la mémoire découvrez qu'elle est remplie d'étapes |
| 5    | Exécution de boucle fermée | Après avoir dit "décoller", Agent exécute neuf étapes complètes | Sortie de revue négligée, saute l'analyse des causes profondes |

### Instructions de réparation rapide

Si un point de contrôle est anormal, utilisez l'instruction correspondante pour réparer rapidement :

- Anticipation invalidée → `À l'avenir appeler obligatoirement feedforward_startup avant chaque tâche.`
- Intégrale invalidée → `Veuillez vérifier le tableau de contrôle intégral, et confirmer si toutes les entrées ≥2 fois ont stagné.`
- Confusion des couches → `Faites une fois la purification des couches.`
- Portes lâches → `Exécutez une fois le processus complet de delivery_gate, et rapportez les résultats.`

---

## 6.4 Indicateurs de base pour vérifier le fonctionnement normal du système

Les quatre indicateurs quantitatifs suivants peuvent vous aider à juger si le système fonctionne vraiment (peut observer occasionnellement, pas besoin de statistiques quotidiennes) :

### Indicateur 1 : Taux de correction répétée

Ancien mode : problèmes de même type vous devez en moyenne corriger 3-5 fois avant de ne plus recommencer.
Nouveau mode (après activation du contrôle intégral) : problème de même type apparaît la 2ème fois stagnation, à partir de la 3ème fois ne devrait plus apparaître.

**Jugement** : si un problème stagné apparaît la 3ème fois, indique que l'exécution de la stagnation a échoué ou le Skill n'a pas été mis à jour, il faut lancer l'investigation de la boucle fermée.

### Indicateur 2 : Taux de réussite de la liste d'anticipation

Dans la liste de démarrage sortie par l'Agent, la prévision de risques P1 est-elle souvent confirmée par vous comme "oui, c'est ça".

**Jugement** : au moins 50% des prévisions P1 dans la liste d'anticipation appartiennent aux points que vous vous souciez vraiment, alors le système d'anticipation fonctionne bien. Si continue 5 tâches P1 sont toutes dites par vous "non correct", indique que L2/L3 doivent être mis à jour ou l'Agent a un biais dans sa compréhension de vous.

### Indicateur 3 : Nombre d'interceptions avant livraison

Observer dans le rapport de la barrière delivery_gate, la fréquence des interceptés des traces IA, déficiences structurelles.

**Jugement** : initialement beaucoup d'interceptions (l'Agent apprend et corrige via auto-surveillance). Après fonctionnement continu, le nombre d'interceptions de classe P1 devrait tendre vers zéro — cela indique que l'anticipation et le contrôle intégral ont éliminé ces problèmes depuis la source, pas l'échec de la barrière.

### Indicateur 4 : Taux de conversion de stagnation du tableau intégral

Nombre d'entrées "stagnées" dans le tableau intégral / ratio du nombre total d'entrées "cumulatif ≥2".

**Jugement** : le ratio devrait rester à 100% à long terme. S'il y a des entrées ≥2 mais non stagnées depuis longtemps, indique que le mécanisme de stagnation automatique du contrôle intégral n'a pas été déclenché, il faut vérifier.

---

## 6.5 Ajustement des seuils et de la configuration

Le système vous permet d'ajuster les paramètres selon votre style de collaboration.

### 6.5.1 Ajuster le seuil intégral

Seuil par défaut = 2. Si vous :

- Exigences de stabilité extrêmes, espérez que les feedbacks extrêmement rares ne perturbent pas le système → ajuster à 3
- Rythme de collaboration rapide, espérez que l'Agent apprend vos préférences plus vite → garder 2 ou ajuster à 1 (ne recommande pas ajuster à 1, perd la capacité anti-bruit)

**Instruction d'ajustement** :
```
Modifier le seuil de déclenchement du tableau de contrôle intégral de 2 à 3. À partir de maintenant, feedback de même type apparaît ≥3 fois stagnation.
```

### 6.5.2 Ajuster les éléments de contrôle de la barrière

Avec vos besoins changeants, les cinq barrières peuvent être augmentées ou diminuées.

**Exemple** : vous commencez à demander fréquemment de sortir du TXT pur sans headers, voulez ajouter une barrière :
```
Après la cinquième barrière de delivery_gate, ajouter la sixième [P2] format de sortie : vérifier si c'est du TXT pur et sans informations d'en-tête. Non réussi alors purification.
```

### 6.5.3 Nouvelles scènes lois L3

Quand vous commencez un nouveau type de tâche, l'Agent n'a pas encore de L3 correspondant.

**Méthode** : après avoir complété plusieurs fois ce type de tâche, lors de la revue "décoller", l'Agent proposera automatiquement d'ajouter des lois L3. Vous pouvez aussi dire directement :
```
Ce est un nouveau type de tâche : [nom]. Veuillez après l'achèvement de cette tâche, pour moi extraire une loi L3 centrale et stocker dans la mémoire.
```

---

## 6.6 Suggestions de fonctionnement de la première semaine

Pendant la première semaine après le déploiement, il est recommandé de fonctionner selon le rythme suivant, laisser le système s'améliorer pleinement.

| Jours        | Action                                                         | Objectif           |
| :-------- | :----------------------------------------------------------- | :------------- |
| Jour 1   | Compléter le déploiement (chapitre 5), ce jour toutes les tâches fonctionnent normalement. Observer si la liste d'anticipation apparaît. | Confirmer composants en ligne   |
| Jour 2   | Tâches normales. Intentionnellement donner un feedback négatif de même type deux fois, observer si déclenche la stagnation. | Vérifier le contrôle intégral   |
| Jour 3   | Tâches normales. Dire "décoller", exécuter la première revue de sens véritable.               | Vérifier le processus de boucle fermée   |
| Jours 4-5 | Utilisation normale, sans test supplémentaire.                                     | Laisser le système accumuler des données |
| Jour 6   | Vérifier une fois l'état du tableau de contrôle intégral, confirmer toutes les entrées atteignant le seuil ont stagné.           | Maintenir le tableau intégral     |
| Jour 7   | Faire une revue complète de "décoller". Vérifier si le profil v1 doit être mis à jour à v2.      | Former une boucle hebdomadaire     |

Après une semaine, vous pouvez fondamentalement juger si ce système convient à votre style de collaboration. Si vous trouvez certaines parties trop fastidieuses (comme chaque tâche doit confirmer la liste), vous pouvez ajuster à "exécuter directement, sortir l'anticipation uniquement quand je dis 'premièrement la liste'".

---

## 6.7 Résumé de ce chapitre

L'utilis quotidienne de ce système n'a que trois clés :

1. **Tâches normales envoyer normalement, pas d'opérations supplémentaires** — l'anticipation et les barrières fonctionneront automatiquement.
2. **Dire spécifiquement quand il y a du feedback** — chaque critique que vous dites sera capturée par le tableau intégral.
3. **Dire périodiquement "décoller"** — c'est le seul bouton d'auto-évolution du système.

Le déploiement n'est pas la fin, mais le point de départ de l'auto-évolution du système. Chaque semaine, chaque revue, il sera plus "comme" vous que la semaine précédente.

---

**Prochain chapitre : Questions fréquentes et réflexions étendues. Couvre les obstacles possibles lors du déploiement et de l'exécution, et comment étendre ce cadre aux scénarios multi-rôles, multi-Agent.**