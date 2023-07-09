Construction de modèles personnalisés avec SQL dans BigQuery ML

![](Aspose.Words.7ed1f3e1-9f26-473e-b8ba-995fcb6110ac.001.png)

Eh bien, contrairement aux API ML, vous pouvez créer vos propres modèles personnalisés avec BigQuery ML.

![](Aspose.Words.7ed1f3e1-9f26-473e-b8ba-995fcb6110ac.002.png)

Nous aborderons AutoML plus tard, mais en bref, AutoML nous permet d'utiliser les modèles de ML de Google dans certains cas pour construire vos propres modèles à partir de zéro en utilisant le transfert d'apprentissage et une forme de recherche d'architecture neuronale.

![](Aspose.Words.7ed1f3e1-9f26-473e-b8ba-995fcb6110ac.003.png)

Pour travailler avec BigQuery ML, il suffit de suivre quelques étapes, du début à l'inférence.

- Tout d'abord, vous devez rédiger une requête sur les données stockées dans BigQuery afin d'extraire vos données d'entraînement.
- Ensuite, vous pouvez créer un modèle, où vous spécifiez un type de modèle et d'autres hyperparamètres.
- Une fois que le modèle est entraîné, vous pouvez l'évaluer et vérifier s'il répond à vos exigences.
- Enfin, vous pouvez effectuer des prédictions à l'aide de votre modèle sur des données extraites de BigQuery.

![](Aspose.Words.7ed1f3e1-9f26-473e-b8ba-995fcb6110ac.004.png)

Connaissez-vous Hacker News ? Hacker News est un site web d'agrégation de nouvelles sociales axé sur l'informatique et l'entrepreneuriat. Je ne vais pas entrer dans tous les détails, mais posons une question. Parmi ces trois articles à droite, où ont-ils été réellement publiés ? Techcrunch, GitHub ou The New York Times ? Bien sûr, vous pouvez peut-être le deviner en fonction du style des articles, mais que se passerait-il si vous vouliez construire un modèle d'apprentissage automatique pour le faire ?

![](Aspose.Words.7ed1f3e1-9f26-473e-b8ba-995fcb6110ac.005.png)

Tout d'abord, écrivons une requête ad hoc pour explorer vos données. Voici un exemple rapide où vous examinez simplement le titre de l'article et l'URL. Vous pouvez extraire les informations de l'éditeur à partir de l'URL en utilisant des fonctions d'expressions régulières.

![](Aspose.Words.7ed1f3e1-9f26-473e-b8ba-995fcb6110ac.006.png)

C'est exactement ce que vous ferez en utilisant la requête sur cette diapositive. Le plan sera le suivant :

Extraire la source de publication en utilisant une fonction REGEXP\_EXTRACT, puis séparer les cinq premiers mots de chaque titre, ou les remplacer par des valeurs NULL dans le cas où le titre est trop court. L'objectif sera ensuite de déterminer si le titre de l'article provient de Github, The New York Times ou TechCrunch en utilisant BigQuery ML.

![](Aspose.Words.7ed1f3e1-9f26-473e-b8ba-995fcb6110ac.007.png)

Voici la traduction du texte dans le contexte de GCP :

Jetons un coup d'œil à la syntaxe nécessaire pour créer un modèle. Vous avez la déclaration CREATE OR REPLACE MODEL en haut où vous donnez le nom du modèle, les options du modèle et d'autres hyperparamètres. Après la clause AS, vous avez votre requête qui définit l'ensemble d'entraînement à partir de la diapositive précédente. C'est tout ! Dans ce cas, vous spécifiez que vous souhaitez construire un modèle de régression logistique. Il s'agit d'un type de modèle de classification que vous pouvez utiliser pour classer votre entrée comme étant un article de GitHub, du New York Times ou de TechCrunch.

[https://towardsdatascience.com/choosing-between-tensorflow-keras-bigquery-ml-and-automl -natural-language-for-text-classification-6b1c9fc21013](https://towardsdatascience.com/choosing-between-tensorflow-keras-bigquery-ml-and-automl-natural-language-for-text-classification-6b1c9fc21013)

![](Aspose.Words.7ed1f3e1-9f26-473e-b8ba-995fcb6110ac.008.png)Pour obtenir les métriques, il vous suffit d'appeler ML.EVALUATE sur votre modèle entraîné ou de cliquer sur le modèle dans l'interface BigQuery et de cliquer sur l'onglet "Évaluation". Concernant les métriques, elles sont évaluées sur une échelle de 0 à 1. En général, plus la valeur se rapproche de 1, mieux c'est, mais cela dépend vraiment de votre métrique.

La précision représente la précision de vos prédictions pour les articles sur lesquels vous avez fait des suppositions. Une précision élevée signifie un faible taux de faux positifs, ce qui pénalise vraiment la précision du modèle s'il fait beaucoup de mauvaises suppositions. D'autre part, le rappel (recall) est le ratio d'observations positives correctement prédites sur l'ensemble des observations de la classe réelle. Combien en avez-vous correctement prédit parmi les vrais positifs et les faux négatifs ?

L'exactitude (accuracy) correspond simplement à la somme des vrais positifs et des vrais négatifs sur l'ensemble de l'ensemble des observations.

Il existe d'autres métriques telles que le score F1 (f1\_score), la perte logarithmique (log\_loss) et les courbes ROC (roc\_curves) que vous pouvez également utiliser.

Vous pouvez également consulter la matrice de confusion, où vous pouvez voir les prédictions incorrectes du modèle. Comme vous pouvez le voir ici, le modèle a eu quelques confusions entre les articles de Techcrunch et ceux du New York Times.

![](Aspose.Words.7ed1f3e1-9f26-473e-b8ba-995fcb6110ac.009.png)

Si le modèle répond à vos besoins, super ! Vous êtes prêt à effectuer des prédictions avec votre modèle.

Vous n'avez pas besoin de vous soucier du déploiement de votre modèle dans un processus distinct. Il est automatiquement disponible pour effectuer des prédictions dans BigQuery. Voici un exemple d'exécution de prédictions en mode batch à l'aide de BigQuery ML. Le premier exemple présenté ici a "gouvernement, arrêt, laisse, travailleurs et désemparés" comme les cinq premiers mots du titre. La prédiction du modèle dans ce cas est "The New York Times".

Modèles pris en charge

Avant de commencer votre premier laboratoire en utilisant BigQuery ML, je vais vous donner un bref aperçu des différents types de modèles actuellement pris en charge. Pour la tâche de prédiction d'articles dans la leçon précédente, rappelez-vous que vous avez utilisé un modèle de régression logistique. Il existe d'autres modèles qui auraient pu être utilisés. Examinons les options de modèles disponibles dans BigQuery ML pour classer les choses.

![](Aspose.Words.7ed1f3e1-9f26-473e-b8ba-995fcb6110ac.010.png)

Tout d'abord, vous avez un autre exemple de classification linéaire, ou ce qu'on appelle aussi régression logistique.

Dans cet exemple, vous utilisez un ensemble de données sur les arrivées de vols pour prédire si un vol sera à l'heure ou non - un résultat binaire. Pour la régression logistique, vous devez simplement spécifier le type de modèle et l'étiquette que vous essayez de prédire. Pour les utilisateurs plus avancés, il existe d'autres options, comme si vous souhaitez que votre modèle utilise une régularisation.

![](Aspose.Words.7ed1f3e1-9f26-473e-b8ba-995fcb6110ac.011.png)Bien que les modèles de régression logistique soient le couteau suisse de l'apprentissage automatique, les réseaux neuronaux profonds, ou DNN, vous permettent de modéliser plus efficacement les relations non linéaires dans vos données.

Un exemple de relation non linéaire se trouve dans la dépréciation des voitures. Une voiture perd une grande partie de sa valeur au cours des premières années, après quoi sa valeur se stabilise plus ou moins. Nous n'entrerons pas dans les détails des réseaux neuronaux profonds dans ce cours, mais sachez que vous pouvez les utiliser dans BigQuery ML. Il vous suffit de spécifier DNN comme type de modèle dans l'instruction CREATE OR REPLACE MODEL.

Cette diapositive montre comment faire cela pour le même exemple d'heure d'arrivée des vols utilisé dans la diapositive précédente.

![](Aspose.Words.7ed1f3e1-9f26-473e-b8ba-995fcb6110ac.012.png)

Si vous êtes familier avec les arbres stimulés par gradient et XGBoost, vous pouvez utiliser cet algorithme pour entraîner des modèles dans BigQuery ML.

Dans cet exemple, vous spécifiez le type de modèle comme "boosted\_tree\_classifier" pour utiliser les arbres stimulés par gradient comme classifieur. Vous pouvez sélectionner plusieurs hyperparamètres pour ce modèle, y compris la profondeur maximale de l'arbre. Encore une fois, je ne vais pas entrer dans les détails ici, mais l'idée derrière les arbres stimulés par gradient est d'ajuster itérativement un arbre de décision aux résidus des arbres de décision précédents.

![](Aspose.Words.7ed1f3e1-9f26-473e-b8ba-995fcb6110ac.013.png)

Nous allons maintenant examiner les options de modèles disponibles dans BigQuery ML pour prévoir des valeurs numériques, telles que des prévisions.

Jusqu'à présent, j'ai seulement parlé de classification. Vous pouvez également utiliser BigQuery ML pour effectuer une régression. Dans cet exemple, vous ajustez un modèle de régression linéaire pour prédire le tarif des taxis en fonction de caractéristiques telles que l'heure de la journée, le lieu de prise en charge et de dépôt, et le jour de la semaine.

![](Aspose.Words.7ed1f3e1-9f26-473e-b8ba-995fcb6110ac.014.png)

Si vous avez besoin d'un modèle plus complexe que la régression linéaire, vous pouvez utiliser un régresseur DNN (Deep Neural Network) dans BigQuery ML. Tout ce que vous avez à faire est de spécifier le type de modèle comme "dnn\_regressor" et de définir les unités cachées, tout comme dans la version de classification des DNN.

![](Aspose.Words.7ed1f3e1-9f26-473e-b8ba-995fcb6110ac.015.png)

Tout comme pour la classification, vous pouvez également utiliser XGBoost pour la régression ! Il vous suffit de spécifier que vous souhaitez utiliser un "boosted\_tree\_regressor".

![](Aspose.Words.7ed1f3e1-9f26-473e-b8ba-995fcb6110ac.016.png)

Et si vous avez déjà entraîné un modèle dans TensorFlow ? Eh bien, vous pouvez importer votre modèle sauvegardé dans BigQuery pour effectuer des prédictions par lots.

Dans cet exemple, la première instruction est celle où vous chargez votre modèle dans BigQuery. Vous spécifiez le nom du modèle, le chemin du modèle dans Cloud Storage, et vous indiquez à BigQuery que le type de modèle est "tensorflow".

Lorsque vous souhaitez effectuer des prédictions, vous pouvez le faire comme indiqué dans la moitié inférieure de la requête de cet exemple. Remarquez l'utilisation de l'instruction ML.PREDICT pour générer les prédictions, puis cette requête réelle est utilisée pour afficher les prédictions dans un format convivial pour l'utilisateur.

![](Aspose.Words.7ed1f3e1-9f26-473e-b8ba-995fcb6110ac.017.png)

Jetons maintenant un coup d'œil aux options de modèle disponibles dans BigQuery ML pour recommander des éléments basés sur des évaluations.

Vous pouvez également servir des recommandations aux utilisateurs dans BigQuery ML ! Le type de modèle utilisé à cet effet s'appelle un modèle de factorisation matricielle. En bref, les modèles de factorisation matricielle sont une forme d'algorithmes de filtrage collaboratif utilisés dans les systèmes de recommandation. Les algorithmes de factorisation matricielle fonctionnent en décomposant la matrice d'interaction utilisateur-élément. Autrement dit, la matrice composée d'utilisateurs et de recommandations est décomposée en produit de deux matrices rectangulaires de plus basse dimensionalité. Tous les détails complets peuvent être trouvés dans de nombreuses sources en ligne différentes sur les systèmes de recommandation.

Cette famille de méthodes est devenue largement connue lors du défi Netflix Prize en raison de son efficacité dans la formulation de recommandations.

Pour créer un moteur de recommandation dans BigQuery ML, vous devez définir le type de modèle sur "factorisation matricielle" et fournir une table d'interactions utilisateur-élément.

![](Aspose.Words.7ed1f3e1-9f26-473e-b8ba-995fcb6110ac.018.png)

Une fois que vous avez un modèle de recommandation entraîné, vous pouvez l'utiliser pour fournir des recommandations ! Voici un exemple de requête où vous obtenez vos utilisateurs et produits à l'aide d'une requête, puis vous obtenez les produits suggérés en utilisant l'instruction ML.PREDICT.

![](Aspose.Words.7ed1f3e1-9f26-473e-b8ba-995fcb6110ac.019.png)

Voici à quoi ressemblera la sortie pour un seul utilisateur. Vous pouvez trier par note prédite pour chaque user\_id et fournir les 5 meilleures recommandations environ à l'aide d'une requête SQL simple.

![](Aspose.Words.7ed1f3e1-9f26-473e-b8ba-995fcb6110ac.020.png)

Enfin, je vais parler d'un algorithme d'apprentissage non supervisé utilisant le regroupement K-Means, disponible dans BigQuery ML. Je n'entrerai pas dans les détails de l'algorithme, mais en bref, dans ce cas, vous n'avez pas d'étiquette que vous essayez de prédire. Au contraire, vous essayez d'explorer les motifs dans vos données.

Dans cet exemple, vous regrouperez les données en quatre clusters, normaliserez les caractéristiques pour tenir compte des différentes plages de valeurs des caractéristiques, ce qui est vraiment important pour le regroupement, et supprimerez tout champ d'identifiant afin de ne pas regrouper les informations en fonction d'informations d'identification uniques.

![](Aspose.Words.7ed1f3e1-9f26-473e-b8ba-995fcb6110ac.021.png)

Après avoir entraîné un modèle de regroupement, vous pouvez facilement voir à quel cluster vos données appartiennent grâce à une requête SQL rapide. Voici un exemple de la requête à utiliser. La colonne CENTROID\_ID fait référence au cluster attribué à chaque ligne de données. Le jeu de données utilisé ici concerne une entreprise de location de vélos qui possède des stations réparties dans tout Londres.

![](Aspose.Words.7ed1f3e1-9f26-473e-b8ba-995fcb6110ac.022.png)

Une fois que vous avez des clusters, comment en tirez-vous réellement parti ? La clé est d'effectuer une analyse des données dans chaque cluster. Vous pouvez explorer les plages de fonctionnalités et les statistiques agrégées pour essayer de comprendre ce qui est "spécial" dans chaque cluster individuel.

![](Aspose.Words.7ed1f3e1-9f26-473e-b8ba-995fcb6110ac.023.png)

Par exemple, vous pourriez utiliser Google Data Studio pour visualiser certaines des attributs des données dans les clusters. Par exemple, ici vous pouvez voir que le Cluster 1 a les trajets les plus longs en termes de durée.

![](Aspose.Words.7ed1f3e1-9f26-473e-b8ba-995fcb6110ac.024.png)

Nous avons couvert beaucoup de syntaxe dans BigQuery ML. Voici une petite feuille de triche rapide avec la syntaxe pour entraîner un modèle, l'évaluer et faire des prédictions, entre autres choses. Utilisez cette feuille de triche pour vous aider lorsque vous commencez à construire des modèles dans BigQuery ML.

[Lab](https://www.cloudskillsboost.google/course_sessions/3856018/labs/367846) [:](https://www.cloudskillsboost.google/course_sessions/3856018/labs/367846) [Prédire](https://www.cloudskillsboost.google/course_sessions/3856018/labs/367846) [la](https://www.cloudskillsboost.google/course_sessions/3856018/labs/367846) [durée](https://www.cloudskillsboost.google/course_sessions/3856018/labs/367846) [d'un](https://www.cloudskillsboost.google/course_sessions/3856018/labs/367846) [trajet](https://www.cloudskillsboost.google/course_sessions/3856018/labs/367846) [à](https://www.cloudskillsboost.google/course_sessions/3856018/labs/367846) [vélo](https://www.cloudskillsboost.google/course_sessions/3856018/labs/367846) [avec](https://www.cloudskillsboost.google/course_sessions/3856018/labs/367846) [un](https://www.cloudskillsboost.google/course_sessions/3856018/labs/367846) [modèle](https://www.cloudskillsboost.google/course_sessions/3856018/labs/367846) [de](https://www.cloudskillsboost.google/course_sessions/3856018/labs/367846) [régression](https://www.cloudskillsboost.google/course_sessions/3856018/labs/367846) [dans](https://www.cloudskillsboost.google/course_sessions/3856018/labs/367846) [BigQuery](https://www.cloudskillsboost.google/course_sessions/3856018/labs/367846) [ML](https://www.cloudskillsboost.google/course_sessions/3856018/labs/367846)

[Lab](https://www.cloudskillsboost.google/course_sessions/3856018/labs/367848) [:](https://www.cloudskillsboost.google/course_sessions/3856018/labs/367848) [Recommandations](https://www.cloudskillsboost.google/course_sessions/3856018/labs/367848) [de](https://www.cloudskillsboost.google/course_sessions/3856018/labs/367848) [films](https://www.cloudskillsboost.google/course_sessions/3856018/labs/367848) [dans](https://www.cloudskillsboost.google/course_sessions/3856018/labs/367848) [BigQuery](https://www.cloudskillsboost.google/course_sessions/3856018/labs/367848) [ML](https://www.cloudskillsboost.google/course_sessions/3856018/labs/367848)
