# Les pipelines de production pour l'apprentissage automatique

## Méthodes pour faire du machine learning sur Google Cloud

![](Aspose.Words.72c13ac8-4bdc-4073-815d-b8fc286c2804.001.png)

Les modèles pré-entrainés à droite ont déjà été discutés. Maintenant, nous allons passer à l'autre côté du spectre et construire votre propre modèle personnalisé et le mettre en production sur Google Cloud. Il existe plusieurs façons de développer, entraîner et servir des modèles personnalisés.

![](Aspose.Words.72c13ac8-4bdc-4073-815d-b8fc286c2804.002.png)

Qu'est-ce que Vertex AI exactement ? C'est un service entièrement géré pour les modèles d'apprentissage automatique personnalisés, à la fois pour l'entraînement et la fourniture de prédictions. Il peut passer de l'étape de l'expérimentation à la production. Vous pouvez également, en utilisant les fonctionnalités de TensorFlow, inclure des transformations sur les données d'entrée et effectuer un ajustement des hyperparamètres pour choisir le meilleur modèle pour votre cas. Vous pouvez déployer vos modèles sur Vertex AI pour fournir des prédictions, qui s'adapteront automatiquement aux demandes de vos clients. Essentiellement, Vertex AI est le moteur qui permet de réaliser de l'apprentissage automatique à grande échelle sur Google Cloud. Un scientifique des données peut entraîner et déployer des modèles de production à partir de Notebooks avec seulement quelques commandes.

![](Aspose.Words.72c13ac8-4bdc-4073-815d-b8fc286c2804.003.png)

Puisque nous utilisons Vertex AI, nous penserons souvent à utiliser des modèles TensorFlow. Cependant, ce cours n'est pas destiné à approfondir les détails de TensorFlow. Vous pouvez en apprendre

plus à ce sujet dans le cours "Machine Learning on Google Cloud", qui fait partie du

parcours d'apprentissage "Machine Learning and AI" pour les Data Scientists et les Machine Learning Engineers.

## Vertex AI Pipelines

Où interviennent les ingénieurs de données dans ce contexte ? N'oublions pas que les ingénieurs de données construisent des pipelines de données, et les pipelines d'apprentissage automatique ne font pas exception. Si nous voulons avoir un pipeline flexible pour toutes les étapes de l'apprentissage automatique, les pipelines Vertex AI sont une excellente option.

Qu'est-ce que les pipelines ML ? La construction de modèles d'apprentissage automatique nécessite des flux de travail complexes et multi-étapes. Lors de la construction d'un modèle, vous devez peut-être nettoyer et transformer des données, créer des fonctionnalités, entraîner plusieurs modèles et évaluer ces modèles. La gestion et l'exécution de ces flux de travail peuvent être difficiles, en particulier si vous souhaitez vous assurer qu'ils sont exécutés de manière reproductible, auditable, rentable et évolutive.

Un pipeline est une façon de modéliser un flux de travail comme un ensemble d'étapes connectées. Chaque étape prend en entrée les sorties des étapes précédentes, effectue des calculs supplémentaires et produit des sorties qui peuvent être utilisées par les composants futurs.

![](Aspose.Words.72c13ac8-4bdc-4073-815d-b8fc286c2804.004.png)

Par exemple, un pipeline ML simple pourrait effectuer les opérations suivantes :

- Charger un ensemble de données à partir d'un fichier de valeurs séparées par des virgules.
- Analyser l'ensemble de données pour identifier et supprimer les valeurs aberrantes.
- Diviser l'ensemble de données nettoyé en un ensemble d'entraînement et un ensemble d'évaluation.
- Entraîner un modèle sur l'ensemble d'entraînement.
- Évaluer le modèle par rapport à l'ensemble d'évaluation.

Dans cet exemple, chaque étape (à l'exception de la première) prend en entrée le résultat de l'étape précédente et produit une sortie qui peut être utilisée par une étape ultérieure.

![](Aspose.Words.72c13ac8-4bdc-4073-815d-b8fc286c2804.005.png)

Les pipelines constituent le cœur des systèmes ML de production et sont utilisés à tous les niveaux de développement, de test et de déploiement. Les pipelines permettent l'achèvement des étapes courantes pour accélérer les expérimentations. Ils sont essentiels lors de l'entraînement et de la réévaluation, car ils permettent l'isolation des étapes et des phases afin de cibler les domaines à optimiser.

Les pipelines sont également le moyen le plus fiable de déployer des modèles en production, en particulier à grande échelle.

Enfin, les pipelines fournissent une variété de points de contrôle pour la surveillance continue et l'optimisation des actifs de production.

![](Aspose.Words.72c13ac8-4bdc-4073-815d-b8fc286c2804.006.png)

En raison de l'ampleur du défi pour permettre les pipelines d'apprentissage automatique, de nombreuses solutions ont été explorées et développées.

Kubeflow Pipelines est un produit open source natif de Kubernetes qui est devenu la norme de l'industrie pour l'exécution de pipelines d'apprentissage automatique au fil des ans.

La prochaine solution était AI Platform Pipelines, un service optimisé pour GKE qui vise à faciliter le déploiement de Kubeflow Pipelines sur les ressources de Google Cloud.

Avec Vertex Pipelines, la gestion des ressources est déplacée loin des utilisateurs, ce qui réduit les désagréments quotidiens liés à la gestion des fichiers de configuration. Par exemple, il n'est plus nécessaire de créer un cluster Kubernetes dédié à l'aide de GKE pour exécuter vos pipelines. Au lieu de cela, Vertex AI gère les clusters Kubernetes et les pods qui s'exécutent dessus en arrière-plan.

![](Aspose.Words.72c13ac8-4bdc-4073-815d-b8fc286c2804.007.png)

Les pipelines peuvent être facilement développés en utilisant des kits de développement logiciel Python flexibles. Cela permet une itération rapide et des cycles de développement vers le déploiement plus rapides en exploitant probablement les compétences présentes dans votre organisation.

![](Aspose.Words.72c13ac8-4bdc-4073-815d-b8fc286c2804.008.png)

Pour résumer, les pipelines gérés dans le contexte de GCP :

1. Sont construits avec des kits de développement Python faciles à utiliser et adaptés aux data scientists.
1. Sont évolutifs car ils exploitent les meilleurs services gérés de Google Cloud.
1. Stockent automatiquement les métadonnées de chaque artefact produit par le pipeline.
1. Bénéficient d'outils robustes pour la gestion des pipelines.
1. Sont sécurisés.
1. Sont très rentables car les ressources sont allouées selon un processus par étape de pipeline.

## AI Hub

![](Aspose.Words.72c13ac8-4bdc-4073-815d-b8fc286c2804.009.png)

AI Hub est un référentiel pour les composants d'apprentissage automatique (ML). Ne réinventez pas la roue ! Évitez de construire un composant si quelqu'un d'autre l'a déjà construit, et très probablement, l'a déjà optimisé. Vous pouvez trouver et déployer non seulement des applications conteneurisées pour l'apprentissage automatique, mais aussi des pipelines complets d'apprentissage automatique sur AI Hub.

![](Aspose.Words.72c13ac8-4bdc-4073-815d-b8fc286c2804.010.png)

Quels types d'actifs pouvons-nous trouver sur AI Hub ? Parmi les actifs stockés sur AI Hub se trouvent des pipelines Kubeflow complets, des notebooks Jupyter, des modules TensorFlow, des modèles entièrement entraînés, des services et des images de machine virtuelle (VM).

![](Aspose.Words.72c13ac8-4bdc-4073-815d-b8fc286c2804.011.png)

Voici à quoi ressemble généralement un actif dans le contexte de GCP. Vous pouvez voir des informations sur le pipeline, telles que les entrées et les sorties, ainsi que des options de téléchargement.

![](Aspose.Words.72c13ac8-4bdc-4073-815d-b8fc286c2804.012.png)

Les ressources sur AI Hub sont regroupées en deux catégories : les ressources publiques et les ressources restreintes. Les ressources publiques sont accessibles à tous les utilisateurs d'AI Hub. Les ressources restreintes comprennent les composants d'IA que vous avez téléchargés ainsi que ceux qui ont été partagés avec vous. Par exemple, vous pourriez avoir des ressources disponibles uniquement pour les personnes au sein de votre organisation ou de vos équipes.

[Lab : Exécution des pipelines sur Vertex AI](https://www.cloudskillsboost.google/course_sessions/3856018/labs/367839)
