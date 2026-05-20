[English](../en/README.md) | [简体中文](../../README.md) | [繁體中文](../zh_TW/README.md) | Français | [日本語](../ja/README.md) | [한국어](../ko/README.md) | [Русский](../ru/README.md) | [Deutsch](../de/README.md)

#Formation d'agents IA avec l'ingénierie cybernétique de Qian Xuesen

> N'enseignez pas de nouvelles connaissances à l'IA. Utilisez **prévision, contrôle intégral, décomposition hiérarchique et auto-surveillance** — quatre concepts — pour remodeler l'architecture de mémoire et de compétences de l'agent, le transformant d'un outil passif en un moteur de collaboration qui s'auto-corrige et évolue.

---

## Qu'est-ce que c'est

Un tutoriel complet, reproductible et pratique.

Il adapte les idées principales de l'*Ingénierie Cybernétique* de Qian Xuesen pour les plateformes d'agents IA modernes (Hermes, Claude avec MCP, GPTs personnalisés, etc.). Sans ajouter d'entrées de prompt ni introduire de nouveaux modèles, il utilise **restructuration architecturale** pour rendre l'agent :

- 🎯 **Prévision pour éviter les pièges** — charge proactivement vos préférences et leçons historiques avant qu'une tâche ne commence
- 🔧 **Contrôle intégral pour empêcher les oscillations** — une plainte ponctuelle ne reçoit qu'une correction temporaire ; la même plainte deux fois déclenche un changement systématique
- 🧹 **Séparation hiérarchique** — la mémoire ne stocke que le "pourquoi" ; les compétences stockent le "comment" ; jamais mélangés
- 🚦 **Porte de livraison avec auto-surveillance** — cinq points de contrôle de qualité sont exécutés avant toute sortie ; les résultats non qualifiés ne sont jamais livrés
- 🔄 **Évolution en boucle fermée** — dites "décollage" une fois par semaine et l'agent s'examine et s'optimise automatiquement

---

## Démarrage Rapide

Envoyez cette commande à votre agent, et il complètera automatiquement toute la formation (≈ 40 minutes) :

```
按 github.com/zeronesun/cybernetic-your-agent 的 scripts/deployment-commands.md 训练我。每步确认，完成后闭环测试。
```

**Configuration requise** : Votre agent doit pouvoir accéder à GitHub, écrire dans la mémoire et créer des compétences. Si ce n'est pas le cas, suivez les étapes manuelles ci-dessous.

1. Assurez-vous que votre plateforme d'agents a : **mémoire persistante** + **compétences / modules procéduraux**
2. Lisez le tutoriel (dans l'ordre est recommandé, ou du moins lisez le chapitre 1 pour comprendre l'approche)
3. Allez au [Chapitre 5](chapters/05-deployment.md), copiez-collez les instructions et déployez étape par étape (≈ 1 heure)
4. Le [Chapitre 6](chapters/06-daily-usage.md) vous explique comment l'utiliser quotidiennement et comment vérifier qu'il fonctionne

---

## Structure du Tutoriel

| Chapitre | Fichier | Résumé en une phrase |
| :------- | :----------------------------------------------------------- | :--------------------------------------------------- |
| Préface | [`PREFACE.md`](PREFACE.md) | Pourquoi l'IA apprend toutes les connaissances mais ne vous "comprend" toujours pas |
| Chapitre 1 | [`chapters/01-background.md`](chapters/01-background.md) | Contexte et philosophie principale |
| Chapitre 2 | [`chapters/02-prerequisites.md`](chapters/02-prerequisites.md) | Conditions préalables et préparation |
| Chapitre 3 | [`chapters/03-core-theory.md`](chapters/03-core-theory.md) | Quatre concepts de cybernétique en détail (prévision / intégral / séparation / auto-surveillance) |
| Chapitre 4 | [`chapters/04-architecture.md`](chapters/04-architecture.md) | Architecture système détaillée (mémoire à trois niveaux + couche de compétences + flux de données) |
| Chapitre 5 | [`chapters/05-deployment.md`](chapters/05-deployment.md) | Guide pratique (instructions de déploiement étape par étape que vous pouvez copier directement) |
| Chapitre 6 | [`chapters/06-daily-usage.md`](chapters/06-daily-usage.md) | Usage quotidien et vérification |
| Chapitre 7 | [`chapters/07-faq-extensions.md`](chapters/07-faq-extensions.md) | Dépannage + extensions multi-agents / nouvelle théorie |
| Épilogue | [`EPILOGUE.md`](EPILOGUE.md) | Après le déploiement : sens et directions futures |

### Note sur la Convention de Nommage des Fichiers

Le répertoire racine et les noms de fichiers des chapitres utilisent l'anglais pour la compatibilité multiplateforme et d'outils. Mappage des noms de fichiers sources chinois vers les noms GitHub :

| Nom de fichier local (chinois) | Nom de fichier GitHub |
| :---------------------------------- | :---------------------------- |
| 序章：为什么 AI…md | `PREFACE.md` |
| 第一章：背景与核心理念.md | `chapters/01-background.md` |
| 第二章：适用条件与准备工作.md | `chapters/02-prerequisites.md` |
| 第三章：核心理论详解.md | `chapters/03-core-theory.md` |
| 第四章：系统架构详解.md | `chapters/04-architecture.md` |
| 第五章：实操指南.md | `chapters/05-deployment.md` |
| 第六章：日常使用与验证.md | `chapters/06-daily-usage.md` |
| 第七章：常见问题与延伸思考.md | `chapters/07-faq-extensions.md` |
| 结尾：架构之后.md | `EPILOGUE.md` |

Les titres et le texte du corps à l'intérieur des fichiers restent en chinois. Le répertoire `translations/` est réservé aux traductions dans d'autres langues (par exemple `en/`, `fr/`).

### Fichiers Complémentaires

| Fichier | Description |
| :----------------------------------------------------------- | :----------------------------------------------------------- |
| [`scripts/deployment-commands.md`](scripts/deployment-commands.md) | Extraction pure de toutes les commandes du Chapitre 5 (pas d'explications, pour exécution rapide) |
| [`examples/`](examples/) | Exemples L2/L3, exemple de tableau de contrôle intégral, exemple de sortie de revue approfondie |
| [`CONTRIBUTING.md`](CONTRIBUTING.md) | Guide de contribution |
| [`LICENSE`](LICENSE) | Licence open source |

---

## Plateformes Prises en Charge

- ✅ **Hermes 3** (support natif complet, toutes les instructions fonctionnent parfaitement)
- ✅ **Claude (avec MCP)** (ajustements mineurs de syntaxe pour les appels d'outils ; architecture principale entièrement applicable)
- ✅ **GPTs Personnalisés** (utilisez des fichiers de connaissances pour simuler la mémoire, des Actions pour simuler les compétences)
- 🔸 Autres plateformes d'agents avec **mémoire persistante + compétences / modules procéduraux**
- 🔸 Plateformes sans fonctionnalité de Compétences (peut fonctionner en mode dégradé, voir [Chapitre 7 §7.1](chapters/07-faq-extensions.md))

---

## Aperçu Général : Avant vs Après

| Dimension | Avant | Après |
| :--------------- | :----------------------------------------- | :------------------------------------------- |
| Début de tâche | Vous énoncez le besoin ; l'agent commence directement | L'agent affiche d'abord une liste de contrôle des pièges et une évaluation des risques ; vous confirmez |
| Erreurs récurrentes | Correction à chaque fois ; même erreur la fois suivante | S'enregistre automatiquement comme règle après la deuxième occurrence ; n'arrivera pas une troisième fois |
| Rapport signal/bruit de la mémoire | Principes, étapes, exemples tous mélangés | Séparation à trois niveaux ; principes et étapes ont chacun leur place |
| Qualité de sortie | Vous inspectez, trouvez des clichés / problèmes de formatage, puis demandez des corrections | L'agent exécute ses propres cinq points de contrôle de qualité ; ne livre pas avant d'avoir réussi |
| Évolution du système | Ajusté occasionnellement basé sur l'intuition | Dites "décollage" hebdomadairement ; revue et auto-optimisation automatiques |

---

## Philosophie Principale

> **Ce que vous faites n'est pas de l'ingénierie de prompt. C'est de l'ingénierie architecturale.**
>
> Vous n'enseignez pas de nouvelles connaissances à l'agent. Vous utilisez la pensée de l'ingénierie des systèmes pour concevoir une architecture interne qui fonctionne de manière stable et évolue continuellement.

Pour plus de contexte et d'élaboration, voir la [Préface](PREFACE.md) et le [Chapitre 1](chapters/01-background.md).

---

## Nom du Projet

**Cybernetic Your Agent** — injection de gènes cybernétiques dans votre agent.

Nous n'enseignons pas de nouvelles connaissances à l'IA. Nous utilisons les quatre concepts de l'Ingénierie Cybernétique de Qian Xuesen — prévision, contrôle intégral, décomposition hiérarchique et auto-surveillance — pour remodeler l'architecture de mémoire et de compétences de l'agent. L'agent passe de comprendre les commandes à comprendre *votre logique de jugement* — devenant vraiment *votre* agent.

---

## Licence

Ce projet est sous licence [MIT License](LICENSE).

---

## Remerciements

- L'*Ingénierie Cybernétique* de Qian Xuesen — la base théorique de ce tutoriel
- L'auteur de la note originale qui a proposé pour la première fois l'idée d'"organiser la mémoire de l'agent avec la cybernétique" et tous ceux qui ont testé et fourni des commentaires dans la section des commentaires
- Tous ceux qui ont aidé à tester et améliorer l'architecture dans ses premières versions

## Historique des Étoiles

<a href="https://www.star-history.com/?zeronesun%2Fcybernetic-your-agent&date">
 <picture>
   <source media="(prefers-color-scheme: dark)" srcset="https://api.star-history.com/chart?zeronesun%2Fcybernetic-your-agent&date&theme=dark" />
   <source media="(prefers-color-scheme: light)" srcset="https://api.star-history.com/chart?zeronesun%2Fcybernetic-your-agent&date&theme=light" />
   <img alt="Star History Chart" src="https://api.star-history.com/chart?zeronesun%2Fcybernetic-your-agent&date" />
 </picture>
</a>
