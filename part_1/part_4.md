Opérationnalisation des modèles d'apprentissage automatique

Analyse des données et Activation de l'apprentissage automatique

Dans la première section, nous examinerons l'analyse des données et la mise en place de l'apprentissage automatique. La manière dont ces deux éléments sont liés est que de nombreuses entreprises commencent par analyser les données. Après avoir tiré profit de cette analyse, elles commencent à creuser davantage et se rendent souvent compte qu'elles disposent de données non structurées pouvant fournir des informations commerciales. Cela les amène donc à vouloir mettre en place l'apprentissage automatique. Il s'agit donc d'une évolution naturelle.

![](Aspose.Words.d9e0735c-1fbf-47e1-a45f-7f7fbbeab371.001.png)

Assurez-vous de bien connaître chaque modèle d'apprentissage automatique pré-entraîné. Par exemple, quels sont les trois modes de l'API de Traitement du Langage Naturel ?

La réponse est l'analyse des sentiments, les entités et la syntaxe.

L'API de Traitement du Langage Naturel serait-elle un outil approprié pour identifier tous les lieux mentionnés dans un document ?

Oui, cela pourrait être utile à cette fin.

![](Aspose.Words.d9e0735c-1fbf-47e1-a45f-7f7fbbeab371.002.png)

Les modèles pré-entraînés peuvent transformer des données apparemment dénuées de sens en données significatives. Je pense que l'API de traduction en est un bon exemple. Si vous avez du texte dans une langue que vous ne comprenez pas, la signification contenue dans les données n'est pas accessible pour vous. Utilisez l'API de traduction pour le convertir dans une langue que vous COMPRENEZ, et soudainement il y a du sens et de la valeur. Les modèles pré-entraînés créent de la valeur à partir de la parole, du texte et des images - des sources courantes de données non structurées.

![](Aspose.Words.d9e0735c-1fbf-47e1-a45f-7f7fbbeab371.003.png)

Si aucun des modèles pré-entraînés ne convient, vous pouvez utiliser TensorFlow et AI Platform pour créer vos propres modèles.

![](Aspose.Words.d9e0735c-1fbf-47e1-a45f-7f7fbbeab371.004.png)

TensorFlow est une bibliothèque open-source performante pour le calcul numérique. Ce n'est pas seulement pour l'apprentissage automatique. Il peut fonctionner avec n'importe quel calcul numérique. En fait, les gens ont utilisé TensorFlow pour toutes sortes de calculs sur GPU ; par exemple, vous pouvez utiliser TensorFlow pour résoudre des équations aux dérivées partielles - cela est utile dans des domaines tels que la dynamique des fluides. TensorFlow en tant que bibliothèque de programmation numérique est attrayant car vous pouvez écrire votre code de calcul dans un langage de haut niveau, comme Python, et l'exécuter de manière rapide.

La façon dont TensorFlow fonctionne est que vous créez un graphe dirigé pour représenter votre calcul. Par exemple, les nœuds pourraient représenter des opérations mathématiques

- des choses comme l'addition, la soustraction et la multiplication, ainsi que des fonctions plus complexes. L'entraînement et l'évaluation des réseaux neuronaux peuvent être représentés sous forme de graphes de flux de données. La représentation des données tensorielles est transmise de nœud en nœud où elle est traitée. Cela est analogue au flux de données et à un pipeline, mais l'entrée et la sortie sont des opérations mathématiques. TensorFlow a été développé chez Google et est portable sur les GPU, les CPU et un matériel spécial appelé TPU, qui signifie TensorFlow Processing Units.

Déploiement d'un Pipeline ML

Si vous êtes un Data Analyst, vous pourriez utiliser SQL pour analyser des données. C'est un domaine spécifique dans lequel BigQuery excelle.

En tant qu'Ingénieur des données, vous êtes probablement plus intéressé par la mise en place de l'infrastructure permettant l'analyse des données par un Data Analyst que par la génération effective de connaissances à partir des données.

Est-ce que cela a du sens ?

Dans le contexte d'un Ingénieur des données, l'analyse de données concerne les systèmes que vous pourriez mettre en place pour rendre l'analyse possible pour vos utilisateurs ou clients.

![](Aspose.Words.d9e0735c-1fbf-47e1-a45f-7f7fbbeab371.005.png)

Si vous n'exécutez pas de requêtes, il est probable que vous exécutiez des programmes pour analyser les données.

C'est là que les notebooks se démarquent.

Les notebooks sont un environnement de développement autonome et sont souvent utilisés dans le développement moderne de traitement de données et d'apprentissage automatique, car ils combinent la gestion du code, le code source, le contrôle, la visualisation et l'exécution étape par étape pour un développement progressif et le débogage. Un notebook est un excellent cadre pour expérimenter dans un environnement de programmation.

Il existe plusieurs frameworks de notebook populaires utilisés aujourd'hui, notamment Colab et Datalab.

![](Aspose.Words.d9e0735c-1fbf-47e1-a45f-7f7fbbeab371.006.png)Parlons de l'analyse des données lorsque les données sont non structurées ou ne sont pas organisées de manière appropriée à votre objectif.

Si vous pouvez utiliser un modèle ML pré-entraîné, il peut rapidement transformer ces données en quelque chose d'utile.

Mais si vous n'avez pas de modèle approprié, vous devrez peut-être en développer un.

Un des concepts de base de l'apprentissage automatique est l'erreur corrigeable. Si vous pouvez faire une supposition sur quelque chose, comme une valeur ou un état, et si vous savez si cette supposition est correcte ou non, et surtout si vous savez dans quelle mesure la supposition est erronée, vous pouvez la corriger. Répétez cela des centaines et des milliers de fois et il devient possible d'améliorer l'algorithme de supposition jusqu'à ce que l'erreur soit acceptable pour votre application. Des concepts tels que "échec rapide", cycle de vie et itérations deviennent importants dans le développement et le raffinement d'un modèle.

Dans cet exemple, le développement du modèle commence dans un notebook sur un sous-ensemble simple de données.

![](Aspose.Words.d9e0735c-1fbf-47e1-a45f-7f7fbbeab371.007.png)

Une fois que vous avez un modèle qui fonctionne localement, lorsque vous avez configuré et testé les différentes parties, vous pouvez le mettre à l'échelle en utilisant la technologie sans serveur de Vertex AI sur GCP (Google Cloud Platform).

C'est à ce moment-là que les Big Data sont traitées et que le modèle commence à devenir suffisamment précis pour vos besoins.

Chaque fois que vous parcourez les données d'entraînement, cela s'appelle une époque (Epoch). Et vous pouvez modifier certains paramètres pour aider le modèle à développer une précision prédictive accrue.

Comme dans cet exemple, vous pouvez facilement connecter et faire évoluer une application d'exemple dans un notebook vers Vertex AI.

![](Aspose.Words.d9e0735c-1fbf-47e1-a45f-7f7fbbeab371.008.png)

Voici le modèle pour développer vos propres modèles d'apprentissage automatique dans le contexte de GCP :

- Tout d'abord, préparez les données.
- Cela signifie que vous collectez les données d'entraînement, nettoyez les données et les divisez en pools ou groupes à des fins différentes.
- Ensuite, sélectionnez les caractéristiques et améliorez-les avec l'ingénierie des caractéristiques.
- Ensuite, stockez les données d'entraînement dans un emplacement en ligne auquel Vertex AI peut accéder, tel que Cloud Storage.

Ensuite, suivez ces étapes. Utilisez TensorFlow pour créer l'application d'entraînement. Emballez-la. Ensuite, configurez et lancez une tâche Vertex AI.

Apprentissage automatique Revue de terminologie

![](Aspose.Words.d9e0735c-1fbf-47e1-a45f-7f7fbbeab371.009.png)

Dans le contexte de GCP (Google Cloud Platform), voici la traduction du texte :

Pour les questions concernant l'apprentissage automatique (Machine Learning), assurez-vous d'identifier l'étape en question. Certaines étapes impliquent des actions similaires ou connexes.

Sur Google Cloud, nous pouvons utiliser :

- Les API de journalisation (Logging APIs), Pub/Sub, etc. et d'autres méthodes de streaming en temps réel pour collecter les données.
- BigQuery, Dataflow et le kit de développement prétraitement de l'apprentissage automatique (ML preprocessing SDK) pour organiser les données en utilisant différents types de structures.
- Utilisez TensorFlow pour créer le modèle.
- Et utilisez Cloud ML pour entraîner et déployer le modèle.

![](Aspose.Words.d9e0735c-1fbf-47e1-a45f-7f7fbbeab371.010.png)

Même les données qui ont un schéma peuvent encore être non structurées si elles ne sont pas utiles à votre objectif spécifique. Voici un exemple. Imaginez que vous vendiez des produits en ligne. Après la livraison du produit, un e-mail est envoyé demandant un retour d'expérience. En examinant les premiers douze ou e-mails, vous commencez à regretter de ne pas avoir envoyé une sorte de sondage. En effet, compiler les résultats du texte de chaque e-mail va être impossible. Dans le but d'identifier les bonnes pratiques et les mauvaises pratiques, les données textuelles des e-mails sont non structurées. Cependant, vous pourriez utiliser l'analyse de sentiment pour étiqueter les e-mails et les regrouper. Laissez l'apprentissage automatique lire pour vous et trier les e-mails en groupes représentatifs. Maintenant, vous pouvez examiner les e-mails les plus positifs et les plus négatifs pour identifier les comportements à encourager ou à éviter. Le processus d'apprentissage automatique a transformé les données non structurées en données structurées pour vos besoins.

![](Aspose.Words.d9e0735c-1fbf-47e1-a45f-7f7fbbeab371.011.png)Distinguer entre les problèmes ponctuels (de raisonnement) qui sont mieux résolus par des humains et les problèmes de Big Data qui peuvent être résolus en traitant une grande quantité de données, ainsi que les problèmes d'apprentissage automatique qui sont mieux résolus en utilisant la modélisation.

On m'a déjà demandé si un modèle d'apprentissage automatique pouvait distinguer les images à l'envers des images à l'endroit. Pourrais-tu entraîner un modèle à le faire ? Je suppose que oui. Mais la plupart des appareils photo modernes ajoutent des métadonnées dans l'en-tête de l'image concernant l'orientation de l'appareil photo au moment où l'image a été prise. Ces données sont précises et facilement accessibles. Ainsi, dans ce cas, il serait préférable de lire les métadonnées plutôt que d'entraîner un modèle d'apprentissage automatique.

![](Aspose.Words.d9e0735c-1fbf-47e1-a45f-7f7fbbeab371.012.png)

Il est important de reconnaître que l'apprentissage automatique comporte deux étapes : l'entraînement et l'inférence.

Parfois, le terme "prédiction" est préféré à "inférence" car il implique un état futur. Par exemple, reconnaître l'image du chat n'est pas vraiment "prédire" qu'il s'agit d'un chat, il s'agit en réalité d'inférer à partir des données des pixels que l'image représente un chat. Les ingénieurs de données se concentrent souvent sur l'entraînement du modèle et minimisent ou oublient l'inférence. Il ne suffit pas de construire un modèle. Il faut l'opérationnaliser. Il faut le mettre en production afin qu'il puisse effectuer des inférences.

![](Aspose.Words.d9e0735c-1fbf-47e1-a45f-7f7fbbeab371.013.png)

Si vous avez une question ML qui concerne les ÉTIQUETTES, il s'agit d'une question sur l'APPRENTISSAGE SUPERVISÉ.

![](Aspose.Words.d9e0735c-1fbf-47e1-a45f-7f7fbbeab371.014.png)

Si la question concerne la RÉGRESSION ou la CLASSIFICATION, elle utilise l'apprentissage supervisé en ML (Machine Learning) dans le cadre de GCP (Google Cloud Platform).

![](Aspose.Words.d9e0735c-1fbf-47e1-a45f-7f7fbbeab371.015.png)

Une source très courante de données structurées pour l'apprentissage automatique est votre entrepôt de données. Les données non structurées comprennent des éléments tels que des images, du son ou des vidéos, ainsi que du texte libre.

Les gens oublient parfois que les données structurées peuvent constituer un excellent ensemble de données d'entraînement car elles sont déjà pré-étiquetées.

Cet exemple montre que les données de naissance peuvent être utilisées pour entraîner un modèle à prédire les naissances.

Un autre exemple que j'aime utiliser est celui des données immobilières. Il existe une tonne d'informations en ligne sur les maisons, leur taille, le nombre de chambres, et ainsi de suite. Et aussi l'historique des ventes de maisons et du montant payé pour elles. Ce sont de formidables données d'entraînement pour construire un modèle d'évaluation des prix des logements. En d'autres termes, l'objectif serait de décrire la maison au modèle d'apprentissage automatique et de lui faire retourner un prix estimé de ce que la maison pourrait valoir.

![](Aspose.Words.d9e0735c-1fbf-47e1-a45f-7f7fbbeab371.016.png)

Si vous ne définissez pas une métrique ou une mesure pour évaluer le bon fonctionnement de votre modèle, comment saurez-vous s'il fonctionne suffisamment bien pour être utile à votre entreprise ?

Vous devriez vous familiariser avec l'Erreur Quadratique Moyenne (Mean Square Error ou MSE en anglais).

![](Aspose.Words.d9e0735c-1fbf-47e1-a45f-7f7fbbeab371.017.png)

La descente de gradient est une méthode importante à comprendre. C'est COMMENT un problème de ML est transformé en un problème de recherche.

![](Aspose.Words.d9e0735c-1fbf-47e1-a45f-7f7fbbeab371.018.png)

L'erreur quadratique moyenne (MSE) et la racine carrée de l'erreur quadratique moyenne (RMSE) sont des mesures de la précision avec laquelle le modèle correspond à la réalité, de son efficacité pour catégoriser ou prédire.

La racine carrée de l'erreur quadratique moyenne.

Une raison d'utiliser la racine carrée de l'erreur quadratique moyenne plutôt que l'erreur quadratique moyenne est que la RMSE est exprimée dans les unités de mesure, ce qui la rend plus facile à lire et à comprendre la signification de la valeur.

![](Aspose.Words.d9e0735c-1fbf-47e1-a45f-7f7fbbeab371.019.png)

La catégorisation produit des valeurs discrètes et la régression produit des valeurs continues.

Chacune utilise des méthodes différentes.

Le résultat que vous recherchez est-il similaire à la décision de savoir si une instance appartient à la catégorie "A" ou à la catégorie "B" ? Si c'est le cas, il s'agit d'une valeur discrète et utilise donc la classification.

Le résultat que vous recherchez est-il plutôt semblable à un nombre, comme la valeur actuelle d'une maison ? Si c'est le cas, il s'agit d'une valeur continue et utilise donc la régression.

Si la question décrit l'entropie croisée, il s'agit d'un problème de classification en apprentissage automatique (ML).

![](Aspose.Words.d9e0735c-1fbf-47e1-a45f-7f7fbbeab371.020.png)

Voici la traduction du texte dans le contexte de GCP :

Ceci est la mise en œuvre du principe de "Pratique, pas parfait". Quand votre modèle sera-t-il utilisable ? Quand devriez-vous cesser de l'améliorer ?

Si cette étape est manquante, vous pourriez avoir des coûts incontrôlables, des performances médiocres ou un modèle qui ne fonctionne pas suffisamment et qui est trompeur.

Notez qu'après avoir calculé l'erreur sur le lot de données, nous pouvons soit continuer, soit évaluer le modèle. L'évaluation du modèle doit se faire sur l'ensemble des données, pas seulement sur un petit lot !

![](Aspose.Words.d9e0735c-1fbf-47e1-a45f-7f7fbbeab371.021.png)

Si vous disposez d'un ensemble de données, vous aurez besoin de données d'entraînement et de données de validation. Vous ne pouvez pas les utiliser toutes deux au même endroit, sinon vous n'obtiendrez pas d'erreur mesurable.

L'entraînement et l'évaluation d'un modèle d'apprentissage automatique constituent une expérience visant à trouver le modèle généralisable approprié qui correspond à votre ensemble de données d'entraînement sans le mémoriser. Comme vous pouvez le voir ici, nous avons un modèle linéaire excessivement simpliste qui ne correspond pas aux relations dans les données. Vous pourrez immédiatement constater à quel point cela est mauvais en examinant votre métrique de perte pendant l'entraînement et visuellement sur ce graphique, car il y a plusieurs points en dehors de la forme de la ligne de tendance. Cela s'appelle le sous-apprentissage.

À l'opposé, nous avons le surapprentissage, comme le montre l'extrémité droite. Ici, nous avons considérablement augmenté la complexité de notre modèle linéaire en le transformant en un polynôme d'ordre n qui semble très bien correspondre à l'ensemble de données d'entraînement, peut-être même un peu trop bien. C'est là que les données d'évaluation entrent en jeu. Vous pouvez utiliser l'ensemble de données d'évaluation pour déterminer si les paramètres du modèle conduisent à un surapprentissage. Le surapprentissage, c'est-à-dire la mémorisation de l'ensemble de données d'entraînement, peut être bien pire que d'avoir un modèle qui correspond seulement de manière adéquate à vos données.

Si quelqu'un prétendait avoir un modèle d'apprentissage automatique qui reconnaît de nouvelles instances et les catégorise correctement 100% du temps, cela indiquerait que les données de validation se sont étrangement mélangées avec les données d'entraînement et que ces données ne sont plus une bonne mesure de l'efficacité du modèle.

![](Aspose.Words.d9e0735c-1fbf-47e1-a45f-7f7fbbeab371.022.png)

Lisez ces diapositives à l'envers. Si la question dit "les données sont rares"... alors vous devriez penser que "données de test indépendantes" ou "validation croisée" sont des réponses possibles. Familiarisez-vous avec les différentes méthodes de validation croisée, y compris l'entraînement, la validation et les tests, ainsi que la validation croisée.

Modélisation des processus métier pour l'analyse et l'optimisation

Modélisation des processus métier pour l'analyse et l'optimisation.

La modélisation des processus signifie les considérer dans un contexte formel ou paradigme.

Certaines de ces compétences ne sont pas spécifiques à Google ou aux technologies Google Cloud.

Cependant, nous aborderons quelques cadres communs.

![](Aspose.Words.d9e0735c-1fbf-47e1-a45f-7f7fbbeab371.023.png)

Une matrice de confusion classe les types d'erreurs. Il existe deux types d'erreurs que votre modèle peut commettre. Les conséquences ne sont pas les mêmes.

Voici un exemple. Imaginez que vous prédisiez une condition dangereuse dans une pièce automobile. La valeur positive signifie que la pièce est dangereuse. La valeur négative signifie que la pièce est sûre. Un faux positif signifie que votre modèle a prédit que la pièce était dangereuse alors qu'elle ne l'était pas. Vous avez donc retiré une pièce dont vous n'aviez pas besoin d'éliminer. Un faux négatif signifie que votre modèle a prédit que la pièce était sûre alors qu'elle était en réalité dangereuse. La pièce a donc été utilisée dans une automobile car on pensait qu'elle était sûre, ce qui a entraîné des accidents.

La logique peut être inversée. Si vous prédisiez qu'une pièce était sûre, le faux positif serait qu'elle est en réalité dangereuse. Vous devez donc réfléchir à ce type de problème logique pour comprendre quelle décision commerciale, procédure ou action doit être prise en conséquence du modèle ML.

![](Aspose.Words.d9e0735c-1fbf-47e1-a45f-7f7fbbeab371.024.png)Vous devrez peut-être prévoir d'expliquer votre raisonnement et votre conception. Dans cet exemple, une matrice de confusion est utilisée pour rendre les choix d'ingénierie des données compréhensibles pour les utilisateurs métier.

Votre conseil pour l'examen est le suivant : Utilisez une matrice de confusion pour décrire les performances des modèles de classification.

![](Aspose.Words.d9e0735c-1fbf-47e1-a45f-7f7fbbeab371.025.png)

Quelles sont les priorités commerciales ?

Un modèle de haute qualité nécessite du temps, de l'argent, ou les deux pour être développé.

L'utilisation de modèles pré-entraînés est rapide et peu coûteuse, mais ils peuvent ne pas être adaptés à vos besoins.

Un compromis consiste à utiliser un modèle pré-entraîné existant, mais à y ajouter des fonctionnalités supplémentaires. Et c'est la solution proposée par AutoML.

Conseil pour l'examen : Pensez aux scénarios en termes de qualité, rapidité et coût. Et identifiez ce que la question indique que le client considère comme important.

![](Aspose.Words.d9e0735c-1fbf-47e1-a45f-7f7fbbeab371.026.png)

L'un des thèmes de l'apprentissage automatique (ML) est de commencer simplement et d'évoluer vers la production. On peut voir ci-dessous la progression générale de la construction d'une solution ML : commencer par les Big Data, passer par l'ingénierie des caractéristiques (Feature Engineering), puis créer le modèle et le déployer.

![](Aspose.Words.d9e0735c-1fbf-47e1-a45f-7f7fbbeab371.027.png)

L'ingénierie des fonctionnalités est une discipline unique. Sélectionner quelle(s) fonctionnalité(s) utiliser dans un modèle est crucial. Et il y a beaucoup de choses à prendre en compte, notamment si les données de la fonctionnalité sont denses ou dispersées, et si la valeur numérique est significative ou abstraite. De plus, une bonne fonctionnalité doit disposer d'assez d'exemples disponibles pour entraîner, valider et évaluer le modèle.

![](Aspose.Words.d9e0735c-1fbf-47e1-a45f-7f7fbbeab371.028.png)

Les hyperparamètres peuvent déterminer si votre modèle converge rapidement vers la vérité ou pas du tout ! Des pas de petite taille : En mettant de côté la direction pour le moment, si votre pas est trop petit, votre entraînement pourrait prendre une éternité. Vous êtes assuré de trouver le minimum tant qu'il n'y a qu'un seul minimum, comme cette courbe de perte de régression linéaire ici, si vous utilisez une taille de pas suffisamment petite.

![](Aspose.Words.d9e0735c-1fbf-47e1-a45f-7f7fbbeab371.029.png)

Tailles de pas plus grandes : Si votre taille de pas est trop grande, vous pourriez rebondir d'un mur à l'autre ou rebondir complètement hors de votre vallée, et vous retrouver dans une toute nouvelle partie de la surface de perte. En raison de cela, lorsque la taille de pas est trop grande, le processus n'est pas garanti de converger.

![](Aspose.Words.d9e0735c-1fbf-47e1-a45f-7f7fbbeab371.030.png)

Taille de pas correcte : Si votre taille de pas est juste comme il faut... Eh bien, dans ce cas, vous êtes prêt. Mais quelle que soit cette valeur, il est peu probable qu'elle soit aussi efficace pour un problème différent.

Votre conseil pour l'examen : Mieux vaut connaître la vitesse d'apprentissage (learning rate) et l'ajustement des hyperparamètres en apprentissage automatique (Machine Learning).

![](Aspose.Words.d9e0735c-1fbf-47e1-a45f-7f7fbbeab371.031.png)

La performance est cruciale pour les solutions pratiques. Dans une étude de cas, il existe souvent des exigences qui aident à définir le niveau de performance requis. Voici quelques questions à prendre en compte.

- Données d'entrée et sources de données (E/S) : Combien d'octets votre requête lit-elle ?
- Communication entre les nœuds (mélange) : Combien d'octets votre requête transmet-elle à l'étape suivante ? Combien d'octets votre requête transmet-elle à chaque emplacement (slot) ?
- Calcul : Combien de travail CPU votre requête nécessite-t-elle ?
- Sorties, également appelées matérialisation : Combien d'octets votre requête écrit-elle ?
- Modèles de requêtes à éviter : Vos requêtes respectent-elles les meilleures pratiques SQL dans le contexte de GCP ?

![](Aspose.Words.d9e0735c-1fbf-47e1-a45f-7f7fbbeab371.032.png)

Page 10 du formulaire 990 de l'IRS répertorie 24 types de dépenses différents.

Que se passe-t-il si j'ai besoin d'ajouter un autre type de dépense ? Dois-je modifier le schéma et fournir des valeurs NULL historiquement ? Ah...

![](Aspose.Words.d9e0735c-1fbf-47e1-a45f-7f7fbbeab371.033.png)Si nous ajoutons chaque champ de dépense en tant que nouvelle colonne, la table devient très large. Et le traitement de cette table large n'est pas scalable (évolutif).

![](Aspose.Words.d9e0735c-1fbf-47e1-a45f-7f7fbbeab371.034.png)

Le compromis entre le relationnalisme et la structure plate est appelé normalisation. Ce processus de séparation des champs dans une autre table de recherche, augmentant ainsi les relations entre les tables, est appelé normalisation.

![](Aspose.Words.d9e0735c-1fbf-47e1-a45f-7f7fbbeab371.035.png)

La normalisation représente les relations entre les tables.

Les données dénormalisées présentent les informations dans un format plat.

Les champs répétés permettent de manipuler des données liées dans une boucle, ce qui les rend plus efficaces à traiter.

![](Aspose.Words.d9e0735c-1fbf-47e1-a45f-7f7fbbeab371.036.png)

Le compromis concerne la performance par rapport à l'efficacité. La normalisation est plus efficace. La dénormalisation est plus performante. Les données d'origine sont organisées visuellement, mais si vous deviez écrire un algorithme pour traiter les données, comment pourriez-vous l'aborder ? Vous pourriez le faire par lignes, par colonnes, par lignes puis par champs. Les différentes approches auraient des performances différentes en fonction de la requête. De plus, votre méthode pourrait ne pas être parallélisable. Les données d'origine peuvent être interprétées et stockées de différentes manières dans une base de données. La normalisation des données consiste à les transformer en un système relationnel. Cela permet de stocker les données de manière efficace et facilite le traitement des requêtes de manière claire et directe. La normalisation augmente l'ordre des données.

![](Aspose.Words.d9e0735c-1fbf-47e1-a45f-7f7fbbeab371.037.png)

La dénormalisation est la stratégie consistant à accepter des champs répétés dans les données afin d'optimiser les performances de traitement.

Les données doivent d'abord être normalisées avant de pouvoir être dénormalisées. La dénormalisation est une autre étape visant à rendre les données plus ordonnées. En raison des champs répétés (dans l'exemple, le champ "Nom" est répété), la forme dénormalisée nécessite plus d'espace de stockage. Cependant, étant donné qu'elle n'est plus relationnelle, les requêtes peuvent être traitées de manière plus efficace et en parallèle à l'aide du traitement colonne par colonne.

Conseil pour votre examen : connaître et comprendre la normalisation et la dénormalisation, ainsi que le moment approprié pour appliquer chacune d'entre elles dans la conception de la représentation de vos données.

![](Aspose.Words.d9e0735c-1fbf-47e1-a45f-7f7fbbeab371.038.png)

BigQuery peut utiliser des schémas imbriqués pour des requêtes hautement évolutives. Dans l'exemple présenté, le champ "company" possède plusieurs transactions (imbriquées).

![](Aspose.Words.d9e0735c-1fbf-47e1-a45f-7f7fbbeab371.039.png)Voici quelques éléments à prendre en compte lorsque l'on pense à l'efficacité. La vitesse de traitement, le coût et l'efficacité sont liés.

Je soulignerais simplement que le mélange des données d'une étape à une autre dans le but de regroupement peut être une source d'inefficacité qui n'est pas aussi facile à voir ou à détecter que des entrées ou sorties lentes.

Les tâches longues en cours d'exécution sont un symptôme. Vous voudrez donc peut-être mesurer les ressources et le temps entre les étapes ou effectuer des tests sur des échantillons de plus en plus grands pour vérifier comment le pipeline se met à l'échelle.

![](Aspose.Words.d9e0735c-1fbf-47e1-a45f-7f7fbbeab371.040.png)

N'oubliez pas d'éviter d'utiliser le caractère générique SELECT dans les instructions SQL. Filtrez avec la clause WHERE en SQL, pas avec LIMIT.

LIMIT limite uniquement la sortie, pas le travail effectué pour y parvenir.

WHERE effectue un filtrage sur les entrées.

![](Aspose.Words.d9e0735c-1fbf-47e1-a45f-7f7fbbeab371.041.png)

Nous avons déjà discuté du mélange (shuffling). Cependant, une cause cachée d'inefficacité peut être le déséquilibre des données.

Les données déséquilibrées font que la majeure partie du travail est attribuée à un seul travailleur, tandis que les autres travailleurs attendent que ce travailleur termine.

![](Aspose.Words.d9e0735c-1fbf-47e1-a45f-7f7fbbeab371.042.png)

La clause GROUP BY fonctionne mieux lorsque le nombre de groupes est petit et que les données peuvent être facilement réparties entre eux.

Un grand nombre de groupes ne s'adaptera pas bien à l'échelle. Par exemple, un tri de cardinalité sur un identifiant (ID) pourrait entraîner des résultats de plus en plus médiocres à mesure que les données augmentent et que le nombre de groupes possibles change.

![](Aspose.Words.d9e0735c-1fbf-47e1-a45f-7f7fbbeab371.043.png)

Comprenez quels champs vous utilisez comme clés lors de l'utilisation de JOIN.

![](Aspose.Words.d9e0735c-1fbf-47e1-a45f-7f7fbbeab371.044.png)

Limitez l'utilisation des fonctions définies par l'utilisateur. Utilisez le SQL natif autant que possible.

![](Aspose.Words.d9e0735c-1fbf-47e1-a45f-7f7fbbeab371.045.png)

Il existe des outils disponibles tels que la Carte d'explication de requête qui montre comment le traitement s'est déroulé à chaque étape.

C'est un excellent moyen de diagnostiquer les problèmes de performance et de se concentrer sur des parties spécifiques de la requête qui pourraient en être la cause.

![](Aspose.Words.d9e0735c-1fbf-47e1-a45f-7f7fbbeab371.046.png)

Vous trouverez également des statistiques générales et des ratios qui peuvent être instructifs. Par exemple, le temps passé par le travailleur le plus lent à lire les données d'entrée, liées au CPU ou à l'écriture des données de sortie, que vous pouvez comparer à la moyenne.

![](Aspose.Words.d9e0735c-1fbf-47e1-a45f-7f7fbbeab371.047.png)

La partition par le temps est souvent une manière de répartir équitablement le travail et d'éviter les points chauds lors du traitement des données. Dans cet exemple, une table partitionnée inclut une pseudo-colonne appelée "\_PARTITIONTIME" qui contient un horodatage basé sur la date pour les données chargées dans la table. Cela améliore l'efficacité de BigQuery. Il y a plus d'informations utiles disponibles dans la documentation et en ligne.

Cependant, le conseil contraire est recommandé pour la sélection des données d'entraînement pour l'apprentissage automatique (Machine Learning). Lorsque vous identifiez des données pour l'entraînement d'un modèle d'apprentissage automatique, veillez à les randomiser plutôt qu'à les organiser par ordre chronologique. En effet, si vous entraînez le modèle sur la première partie, par exemple les données d'été, et que vous effectuez les tests sur la deuxième partie qui peut être constituée de données d'hiver, il semblera que le modèle ne fonctionne pas correctement.

![](Aspose.Words.d9e0735c-1fbf-47e1-a45f-7f7fbbeab371.048.png)

Considérez également la nécessité de transférer des données d'un emplacement à un autre via le réseau. Le transfert de données peut être coûteux par rapport à un changement d'approche qui pourrait produire le même résultat avec moins de transfert de données. Dans cet exemple, GroupByKey ne peut utiliser qu'un seul worker par clé, qui utilise toutes les valeurs à mélanger afin qu'elles soient toutes transmises via le réseau. Ensuite, il y a un worker pour la clé 'x' et un worker pour la clé 'y', créant un goulot d'étranglement.

Combine permet à Dataflow de distribuer une clé à plusieurs workers et de la traiter en parallèle. Dans cet exemple, CombineByKey agrège d'abord les valeurs, puis traite les agrégats avec plusieurs workers. De plus, seules 6 valeurs agrégées doivent être transmises via le réseau.

![](Aspose.Words.d9e0735c-1fbf-47e1-a45f-7f7fbbeab371.049.png)

Lorsqu'il s'agit de données non bornées ou en continu dans le contexte de GCP, il est intéressant d'utiliser des fenêtres pour diviser les données en groupes afin de faciliter leur traitement. Bien sûr, il est important de prendre en compte la taille de la fenêtre et de déterminer si les fenêtres se chevauchent.

![](Aspose.Words.d9e0735c-1fbf-47e1-a45f-7f7fbbeab371.050.png)

Cette diapositive explique en détail comment Bigtable stocke les données en interne. Une table Bigtable est fragmentée en blocs de lignes contiguës, appelés tablettes, afin d'équilibrer la charge de travail des requêtes.

Les données ne sont jamais stockées dans les nœuds Cloud Bigtable eux-mêmes ; chaque nœud contient des pointeurs vers un ensemble de tablettes stockées dans un service de stockage. Le rééquilibrage des tablettes d'un nœud à un autre est très rapide car les données réelles ne sont pas copiées. La récupération en cas de défaillance d'un nœud Cloud Bigtable est très rapide car seules les métadonnées doivent être migrées vers le nœud de remplacement.

Lorsqu'un nœud Cloud Bigtable tombe en panne, aucune donnée n'est perdue.

Bigtable est efficace en ce qui concerne l'ingestion rapide en continu, en stockant simplement les données... tandis que BigQuery est efficace pour les requêtes car il est optimisé pour la prise en charge du langage SQL.

![](Aspose.Words.d9e0735c-1fbf-47e1-a45f-7f7fbbeab371.051.png)

Dans Bigtable, chaque table ne possède qu'un seul index, la clé de ligne. Il n'y a pas d'index secondaires. De plus, les données sont stockées dans la clé de ligne selon un ordre croissant. Toutes les opérations sont atomiques au niveau de la ligne.

![](Aspose.Words.d9e0735c-1fbf-47e1-a45f-7f7fbbeab371.052.png)

Cette diapositive explique comment utiliser la clé de ligne.

L'exemple concerne des données de trafic qui sont associées à un code de borne kilométrique et à un horodatage, indiquant l'emplacement des véhicules à des moments spécifiques. La question que nous essayons de résoudre est la suivante : "Quelle valeur doit être utilisée comme index ?"

Si vous stockez les données dans l'ordre des horodatages, les données les plus récentes se trouveront en bas du tableau. Si vous exécutez des requêtes basées sur les données les plus récentes et n'utilisez les données plus anciennes que pour certaines requêtes, cette organisation est le pire cas de figure.

![](Aspose.Words.d9e0735c-1fbf-47e1-a45f-7f7fbbeab371.053.png)

Au lieu de cela, pour optimiser la requête pour le cas d'utilisation, vous pourriez envisager d'utiliser un horodatage inverse, de sorte que les données les plus récentes se trouvent toujours en haut. Mais cela ne fonctionne pas bien non plus... cela introduit un nouveau problème.

![](Aspose.Words.d9e0735c-1fbf-47e1-a45f-7f7fbbeab371.054.png)

Étant donné que nous sommes dans le contexte de GCP (Google Cloud Platform) :

Étant donné que les données sont stockées de manière séquentielle dans Bigtable, les événements commençant par la même horodatage seront tous stockés sur la même tablette. Cela signifie que le traitement n'est pas distribué.

![](Aspose.Words.d9e0735c-1fbf-47e1-a45f-7f7fbbeab371.055.png)

À la fin, cet exemple utilisait le code "milemarker" comme clé de ligne. Cela n'a pas nécessairement facilité la lecture des données ou accéléré une requête spécifique, mais cela a permis de distribuer l'accès de manière aléatoire.

Astuce pour l'examen : Sachez comment les index et les valeurs de clé influencent les performances et peuvent introduire un biais éventuel. Un autre exemple concerne les séries chronologiques, où vos données de référence proviennent de l'hiver et votre validation de l'été, ce qui introduit un biais saisonnier dans votre analyse.

![](Aspose.Words.d9e0735c-1fbf-47e1-a45f-7f7fbbeab371.056.png)

Cloud Bigtable est plus sophistiqué que ce que nous avons décrit jusqu'à présent. En réalité, il apprend de vos modèles d'utilisation et ajuste sa façon de fonctionner pour équilibrer et optimiser ses performances.

![](Aspose.Words.d9e0735c-1fbf-47e1-a45f-7f7fbbeab371.057.png)

Cloud Bigtable analyse les schémas d'accès pour s'améliorer.

![](Aspose.Words.d9e0735c-1fbf-47e1-a45f-7f7fbbeab371.058.png)

Cet exemple illustre que parce que A, B, C, D, E ne sont pas des données mais plutôt des pointeurs et des références, et que le rééquilibrage du cache n'est pas chronophage.

![](Aspose.Words.d9e0735c-1fbf-47e1-a45f-7f7fbbeab371.059.png)

Déplacer les pointeurs rééquilibre les nœuds qui effectuent le travail, mais les données ne sont pas copiées ou transférées.

![](Aspose.Words.d9e0735c-1fbf-47e1-a45f-7f7fbbeab371.060.png)

Et voici un exemple où 25 % du volume de lectures atteint un nœud unique. La condition de surcharge est détectée, et les pointeurs sont réorganisés pour répartir les lectures. Il existe plusieurs copies des données dans le service de fichiers. Pour assurer la résilience, les données doivent exister sur différents nœuds. Ainsi, Bigtable sait utiliser des copies sur d'autres nœuds du système de fichiers pour améliorer les performances.

![](Aspose.Words.d9e0735c-1fbf-47e1-a45f-7f7fbbeab371.061.png)

Voici quelques conseils pour faire croître un cluster Bigtable. Il existe plusieurs mesures que vous pouvez prendre pour améliorer les performances.

Un élément que je tiens à souligner est qu'il peut y avoir un délai de plusieurs minutes à plusieurs heures lorsque vous ajoutez des nœuds à un cluster avant de constater une amélioration des performances. Cela a du sens, n'est-ce pas ? Parce que les données et les pointeurs doivent être réorganisés, et cela prend du temps à Bigtable pour déterminer comment ajuster les schémas d'utilisation aux nouvelles ressources.

![](Aspose.Words.d9e0735c-1fbf-47e1-a45f-7f7fbbeab371.062.png)

Le calculateur de tarification peut être utilisé avec BigQuery pour estimer le coût d'une requête avant de la soumettre.

![](Aspose.Words.d9e0735c-1fbf-47e1-a45f-7f7fbbeab371.063.png)

Il existe trois éléments de tarification de BigQuery. Le stockage, le traitement et les activités gratuites, telles que le chargement des données.

Ainsi, vous ne payez pas pour le chargement des données, pour l'ingestion, mais vous payez pour stocker les données une fois qu'elles sont chargées.

Un conseil pour l'examen est de se méfier de tout ce qui implique un SELECT all. Vous devez comprendre l'utilisation des caractères génériques.

![](Aspose.Words.d9e0735c-1fbf-47e1-a45f-7f7fbbeab371.064.png)

Le validateur de requêtes estime également la quantité de données utilisées par la requête avant de l'exécuter. Vous pouvez utiliser cette estimation dans le calculateur de tarification pour obtenir une estimation du montant que vous dépenserez avant d'exécuter la requête.

[Lab : Opérations et maintenance de cluster Cloud Dataproc](https://www.cloudskillsboost.google/course_sessions/3663395/labs/343602)
