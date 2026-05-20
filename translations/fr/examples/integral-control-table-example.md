# Exemple de tableau de contrôle intégral

Ce fichier présente l'état réel d'un tableau de contrôle intégral après un mois d'exécution, ainsi qu'un dialogue typique d'inférence (système inféré).

> **Note** : Les entrées ci-dessous sont fictives et ne servent qu'à illustrer la structure des données et la logique d'exécution.

---

## Tableau de contrôle intégral après un mois d'exécution

```
【Tableau de contrôle intégral】
| Catégorie | Modèle d'erreur(≤8 caractères) | Premier date | Occurrences cumulées | Seuil | Système inféré | Cible d'inférence                            |
| ---- | -------------- | ---------- | -------- | ---- | ------ | ----------------------------------- |
| Cat A  | Résumé AI en fin     | 2025-05-10 | 2/2      | 2    | Oui     | L2·Esthétique : refuser la conclusion de type résumé             |
| Cat A  | Trop enthousiaste   | 2025-05-12 | 1/2      | 2    | Non     | -                                   |
| Cat B  | Image insuffisante courte | 2025-05-10 | 2/2      | 2    | Oui     | L3·Court : ouverture avec description blanche pour l'image             |
| Cat B  | Code sans tests   | 2025-05-15 | 1/2      | 2    | Non     | -                                   |
| Cat C  | Porte non détectée AI cliché | 2025-05-10 | 2/2      | 2    | Oui     | delivery_gate : règle de détection P1 cliché AI mise à jour |
| Cat C  | Rétroaction non récupérée archive | 2025-05-18 | 1/2      | 2    | Non     | -                                   |
| Cat D  | Une métaphore mal choisie   | 2025-05-08 | 1        | -    | -      | (occasional, non cumulé)                    |
```

---

## Exemple de déclenchement d'inférence

### Scénario : L'utilisateur souligne pour la deuxième fois "résumé AI en fin"

**Utilisateur** :
> Cette fois-ci, à la fin, il y a encore une phrase " quoi qu'il en soit, la vie doit continuer", je n'aime pas ce genre de résumé.

**Processus interne de l'Agent** :
1. Classification d'erreur → Cat A (violation du principe esthétique L2)
2. Recherche dans le tableau d'intégrale → trouve "résumé AI en fin", le nombre cumulé passe de 1 à 2
3. Le nombre = seuil 2, déclenche l'inférence

**Sortie de l'Agent** :
> Enregistré. "résumé AI en fin" est apparu 2 fois. Je suggère d'inférer cette règle vers **[L2·Logique utilisateur sous-jacente] Orientation esthétique**, en ajoutant l'entrée : **"refuser toute forme de conclusion de type résumé"**.
> 
> Êtes-vous d'accord ?

**Utilisateur** :
> D'accord.

**Exécution de l'Agent** :
1. Écriture de cette entrée dans L2
2. Mise à jour du tableau d'intégrale : inféré → Oui
3. Confirmation : "Inférence terminée. Dans les créations futures, lors du démarrage de la rétroaction, je chargerai activement ce principe."

---

## Exemple de rapport du tableau d'intégrale dans chaque révision de boucle de phase

> Ce tableau d'intégral pour cette phase contient 7 enregistrements :
> - 3 inférés (résumé AI en fin, image insuffisante, porte non détectée AI cliché), aucun traitement supplémentaire nécessaire
> - 3 n'ont pas atteint le seuil (trop enthousiaste, code sans tests, rétroaction non récupérée archive), tous 1/2 fois, observation continue
> - 1 événement occasionnel (une métaphore mal choisie), non compté dans le système cumulatif
> 
> Taux de conversion d'inférence actuel : 100% (tous ceux qui ont atteint le seuil ont été inférés)

---

## Comment vérifier si votre tableau d'intégrale fonctionne correctement

Observez les signaux suivants :
- Après chaque retour négatif, l'Agent classifie-t-il et cumule-t-il clairement ?
- Pour les entrées cumulées à 2 fois, l'Agent propose-t-il activement l'inférence ?
- Après l'inférence, les mêmes types de problèmes n'apparaissent-ils plus ?
- Dans les révisions mensuelles de boucle, les entrées inférées du tableau d'intégrale doivent être clairement traçables
