# Exemple de sortie d'initialisation L2/L3

Ce fichier présente un dialogue typique d'initialisation L2/L3. Après avoir envoyé l'instruction de codification (extraction), l'Agent, basé sur sa compréhension historique de l'utilisateur, sort les ébauches structurées L2 et L3.

> **Note** : Les préférences utilisateur dans cet exemple sont fictives et ne servent qu'à illustrer le format de sortie et la granularité d'extraction. Votre Agent générera une version qui vous appartient en fonction de vos conversations historiques.

---

## Sortie d'extraction de l'Agent

Basé sur ma compréhension actuelle de vous, voici le résultat de l'extraction :

### [L2·Logique utilisateur sous-jacente]

- **Préférences de communication** : concis et direct, sans formalités superflues ; limites claires, dire "non" = arrêter
- **Normes de qualité** : le code doit être accompagné d'une méthode de vérification ; la sortie doit être réutilisable, pas seulement correcte une fois
- **Mode de décision** : risque pré-positionné, exposer d'abord le problème complet avant de présenter la solution ; l'évaluation de second ordre primer sur l'intuition
- **Mode d'apprentissage** : migration théorique inter-domaine ; unité de savoir et d'action, la compréhension doit se traduire en action

### [L3·Règles fondamentales de scénario]

- **Création courte** :
  - L'émotion prime sur le développement de l'intrigue
  - Laisser de l'espace en fin, ne pas faire de résumé ni de moralisation
  - Créer l'image par la description visuelle, ne pas s'appuyer sur les métaphores

- **Sortie de code** :
  - Écrire d'abord les tests ou la méthode de vérification, puis l'implémentation
  - La complétude fonctionnelle prime sur la richesse des commentaires
  - Marquer "à vérifier" pour les comportements incertains, ne pas inventer

- **Conception d'architecture** :
  - Définir d'abord les limites du système et le flux de données, puis choisir la stack technique
  - Évaluer l'extensibilité et les modes de défaillance, ne pas se limiter au happy path
  - La sortie inclut une classification des risques (P0-P3) et leurs réponses

- **Résolution de problème** :
  - Localiser d'abord la cause racine dans les logs ou le site d'exécution, ne pas deviner par expérience
  - Marquer "à vérifier" pour les incertitudes
  - Fournir des étapes réutilisables de résolution, pas seulement la conclusion

---

## Actions d'examen que l'utilisateur peut effectuer

1. **Confirmation ligne par ligne** : Pour chaque principe, demandez-vous — " est-ce vraiment une préférence stable à moi ? "
2. **Correction des écarts** : Dites directement à l'Agent quelle règle est fausse, ce qu'elle devrait être
3. **Compléter les manques** : Si vous pensez qu'une dimension/scénario manque un principe clé, dites-le directement
4. **Supprimer les faux** : Si l'Agent a inventé (vous n'avez pas cette préférence), supprimez-la

---

## Exemples courants de corrections

| Extraction originale de l'Agent | Correction de l'utilisateur | Explication |
| :----------------- | :--------------------------------------- | :--------- |
| Préférences de communication : concis et direct | Préférences de communication : concis mais avec suffisamment de contexte | L'utilisateur découvre qu'il a besoin de contexte, pas seulement de brièveté |
| Court : laisser de l'espace en fin | Court : laisser de l'espace en fin ; mais les histoires en série peuvent avoir une fin douce | L'utilisateur a ajouté l'exception |
| Sortie de code : tests en priorité | Sortie de code : pour les prototypes rapides, les tests peuvent être ajoutés après | L'utilisateur distingue les normes des prototypes et des sorties formelles |

---

## Instruction d'écriture

Après examen :
> Écrire les L2 et L3 confirmés ci-dessus dans la mémoire (memory).

L'Agent les stockera dans la zone principale de la mémoire, en nœuds séparés [L2·Logique utilisateur sous-jacente] et [L3·Règles fondamentales de scénario].
