# Construction de modèles personnalisés avec AutoML

## Pourquoi AutoML?

![](Aspose.Words.824b27aa-2451-4c3d-ba49-00aad9ea075f.001.png)

AutoML occupe une place importante dans la gamme de produits Google Cloud pouvant être utilisés pour l'apprentissage automatique (machine learning).

![](Aspose.Words.824b27aa-2451-4c3d-ba49-00aad9ea075f.002.png)

D'un côté, avec des produits tels que Vertex AI et BigQuery ML, vous pouvez construire des modèles d'apprentissage automatique très personnalisés.

Cependant, pour utiliser ces produits, vous aurez besoin de quelqu'un ayant une expertise en apprentissage automatique et une expérience en codage. Vous serez responsable de former le modèle d'apprentissage automatique vous-même, ce qui peut prendre beaucoup de temps.

![](Aspose.Words.824b27aa-2451-4c3d-ba49-00aad9ea075f.003.png)

D'autre part, sur Google Cloud, vous pouvez appeler des modèles pré-entraînés en utilisant des services tels que l'API Vision et l'API Speech-to-Text. Aucune formation de modèle n'est nécessaire pour ces services. Vous fournissez simplement vos données à l'API et elle vous renvoie des prédictions. L'inconvénient de l'utilisation de modèles pré-entraînés est qu'ils ne produisent des prédictions précises que lorsque vos données sont relativement courantes, comme dans les images des réseaux sociaux ou les avis des clients.

![](Aspose.Words.824b27aa-2451-4c3d-ba49-00aad9ea075f.004.png)

AutoML se situe quelque part entre ces deux approches. Un modèle est entraîné spécifiquement à partir de vos données, mais vous n'avez pas besoin de code pour l'entraîner.

![](Aspose.Words.824b27aa-2451-4c3d-ba49-00aad9ea075f.005.png)

Si vous souhaitez entraîner un modèle d'apprentissage automatique à partir de zéro, vous avez besoin de compétences en apprentissage automatique et en codage. De manière anecdotique, la construction de modèles d'apprentissage automatique suit le principe de Pareto, où vous pouvez rapidement lancer un modèle fonctionnel d'apprentissage automatique. Cependant, la majeure partie du temps et des efforts sera consacrée au débogage et à l'optimisation des performances du modèle d'apprentissage automatique.

![](Aspose.Words.824b27aa-2451-4c3d-ba49-00aad9ea075f.006.png)

AutoML suit une procédure standard divisée en trois phases : l'entraînement, le déploiement et l'utilisation.

**Entraînement**

La phase d'entraînement comprend plusieurs étapes :

- Tout d'abord, vous devez préparer un ensemble de données qui sera utilisé dans le processus d'entraînement supervisé.
- Ensuite, vous devez analyser l'ensemble de données pour vous assurer qu'il possède les qualités nécessaires pour être efficace. Il se peut que vous deviez corriger l'ensemble de données.
- Une fois que l'ensemble de données est prêt et validé, vous l'utilisez pour entraîner le modèle.
- Enfin, le modèle est utilisé avec des données de test pour évaluer s'il sera efficace pour prédire et classer de nouveaux cas.
- Si le modèle ne fonctionne pas bien à ce stade, vous devrez peut-être revenir en arrière, modifier l'ensemble de données et réessayer.

**Déploiement**

La deuxième phase consiste à déployer le modèle et à le gérer. Cela signifie se débarrasser des anciens modèles ou des modèles inutilisés.

**Utilisation**

La troisième phase consiste à héberger le modèle sur un service où il peut être utilisé pour prédire et classer.

Dans l'apprentissage automatique traditionnel, les phases de déploiement et d'utilisation sont complexes et impliquent de déplacer le modèle d'un système de création de modèles tel que TensorFlow vers un système d'hébergement de modèles comme Vertex AI. Cependant, AutoML gère la majeure partie de la complexité de ces activités pour vous, rendant ainsi ces activités faciles.

![](Aspose.Words.824b27aa-2451-4c3d-ba49-00aad9ea075f.007.png)

AutoML utilise un ensemble de données préparé pour entraîner un modèle personnalisé. Vous pouvez créer de petits ensembles de données préparées pour des expérimentations directement dans l'interface utilisateur Web, mais il est plus courant de rassembler les informations dans un fichier CSV (valeurs séparées par des virgules). Le fichier CSV doit être encodé en UTF-8 et situé dans le même compartiment de stockage Cloud que les fichiers sources. Vous pouvez également créer et gérer des ensembles de données préparées de manière programmative en Python, Java ou Node.js.

La première colonne du fichier CSV est facultative. Elle attribue les données de chaque ligne à l'un des trois groupes : ENTRAÎNEMENT, VALIDATION ou TEST. Si vous omettez cette colonne, les lignes seront automatiquement réparties avec 80 % pour l'ENTRAÎNEMENT et 10 % pour la VALIDATION et le TEST.

La colonne suivante du fichier CSV identifie les fichiers sources hébergés dans le stockage Cloud. Il s'agit de chemins commençant par gs://. Le format des fichiers sources dépend du type de modèle que vous entraînez, mais ils peuvent également être des fichiers ZIP compressés.

Les colonnes suivantes spécifient les étiquettes. Les étiquettes sont alphanumériques et peuvent contenir des tirets bas, mais pas de caractères spéciaux. Le fichier CSV ne doit pas contenir de lignes en double et ne peut pas contenir de lignes vides ou de caractères unicode.

Actuellement, le fichier CSV et tous les fichiers sources doivent être situés dans un compartiment de stockage Cloud du projet où AutoML s'exécute.

Les ensembles de données préparées n'expirent pas. Vous pouvez accumuler de nombreux ensembles de données préparées dans un projet. Vous pouvez répertorier et supprimer ceux dont vous n'avez pas besoin.

![](Aspose.Words.824b27aa-2451-4c3d-ba49-00aad9ea075f.008.png)

AutoML effectue des vérifications de base et une analyse préliminaire de l'ensemble de données préparé afin de déterminer s'il contient suffisamment d'informations et s'il est correctement organisé. Si l'ensemble de données préparé n'est pas prêt, vous devrez ajouter plus de lignes ou de libellés au fichier CSV. Une fois prêt, vous pouvez commencer l'entraînement.

L'entraînement peut prendre de dix minutes à plusieurs heures selon le type de modèle. Vous pouvez vérifier l'état de l'entraînement pendant qu'il est en cours. Les tâches d'importation et d'entraînement peuvent être annulées.

Le groupe TRAIN de données est utilisé pour entraîner le modèle personnalisé. Les fichiers source ont déjà été associés aux bons libellés dans l'ensemble de données préparé, donc AutoML utilise une méthode d'apprentissage supervisé pour entraîner le modèle personnalisé. Une partie du processus utilise les données du groupe VALIDATION pour vérifier la précision du modèle en termes de classification et de prédiction. L'apprentissage supervisé se base sur les erreurs corrigibles. AutoML construit un algorithme qui devine les libellés des données source. Lorsque la devinette est correcte, cela renforce l'algorithme. Lorsque la devinette est incorrecte, l'erreur est utilisée pour corriger l'algorithme. C'est ainsi que se produit l'apprentissage. Un passage complet à travers toutes les données du groupe TRAIN est appelé une époque. L'erreur totale est suivie et minimisée à travers plusieurs époques pour créer le meilleur modèle possible à partir des données d'entraînement fournies.

Le résultat est un modèle personnalisé entraîné.

Le modèle personnalisé fonctionne bien avec les données d'entraînement. Mais est-il bon pour catégoriser de nouvelles instances de données qu'il n'a jamais vues auparavant ?

![](Aspose.Words.824b27aa-2451-4c3d-ba49-00aad9ea075f.009.png)

Les données du groupe TEST sont utilisées pour évaluer le modèle personnalisé et éliminer les biais lors de l'évaluation. Les prédictions et classifications sont comparées aux libellés présents dans l'ensemble de données préparé.

Le rapport d'évaluation fournit des indicateurs spécifiques au type de modèle et aide à comprendre l'efficacité du modèle dans la prédiction et la classification.

![](Aspose.Words.824b27aa-2451-4c3d-ba49-00aad9ea075f.010.png)

Il n'y a rien que vous devez faire pour activer un modèle. Cependant, s'il s'est écoulé un certain temps depuis que vous avez utilisé un modèle, le système peut avoir besoin de se "réchauffer" pendant quelques minutes avant que le modèle ne devienne actif.

Une fois qu'il existe, si vous avez les informations d'identification du projet et le nom du modèle, vous pouvez accéder et utiliser le modèle personnalisé.

À chaque fois que vous entraînez un ensemble de données préparé, cela crée un nouveau modèle personnalisé.

Vous pouvez répertorier et supprimer les modèles inutiles.

Les modèles personnalisés sont temporaires. Ils sont finalement supprimés et ne peuvent pas être exportés ou sauvegardés en externe.

Les modèles qui ne sont pas utilisés pour les prédictions sont automatiquement supprimés après un certain temps. Et les modèles utilisés sont finalement supprimés. Vous devrez donc périodiquement entraîner un nouveau modèle personnalisé pour continuer à prédire et à classer.

La durée pendant laquelle les modèles restent avant d'être supprimés dépend du type de modèle.

![](Aspose.Words.824b27aa-2451-4c3d-ba49-00aad9ea075f.011.png)

L'interface principale de classification se trouve à l'URI indiquée. Vous pouvez effectuer une classification en utilisant l'interface Web ou en ligne de commande à l'aide de CURL pour envoyer une demande structurée en JSON. Il existe également des bibliothèques clientes pour Python, Java et Node.js.

Une fois que vous avez configuré l'authentification pour utiliser l'API REST, vous pouvez envoyer une demande avec le nom du modèle et la charge utile, qui est la donnée que vous souhaitez classer.

Le service renvoie un JSON contenant plusieurs champs appelés "displayName". Ce sont les libellés qui correspondent. Ensuite, il contient la classification par mot-clé, suivie d'un score. Le score est une valeur de confiance, où 1.0 représente une confiance absolue, et les nombres fractionnaires inférieurs représentent une confiance moins élevée dans la précision de la classification.

Des quotas s'appliquent à la fois à la création de modèles et aux demandes de service.

![](Aspose.Words.824b27aa-2451-4c3d-ba49-00aad9ea075f.012.png)

AutoML réduit l'effort nécessaire pour créer un modèle par rapport à l'apprentissage automatique traditionnel. Avec l'apprentissage automatique traditionnel, la création de modèles était difficile, il y avait donc une tendance à essayer d'inclure à la fois l'ensemble de données et le modèle.

Avec AutoML, vous pouvez créer des modèles personnalisés plus petits et plus spécialisés et les utiliser de manière programmatique. Ainsi, vous n'avez pas besoin de tout regrouper dans un seul modèle. Vous pouvez diviser une classification en plusieurs étapes. De plus, vous pouvez utiliser les résultats d'une classification pour prendre des décisions sur le type de classification à effectuer ensuite.

Voici un exemple :

Une entreprise qui vend des vêtements dispose d'un service client qui reçoit des e-mails de clients. Le premier travail pourrait consister à distinguer les e-mails contenant des commentaires sur les produits des e-mails demandant des informations sur l'entreprise. Le Modèle 1 pourrait être utilisé pour classifier les e-mails de commentaires.

Le deuxième travail pourrait consister à distinguer si l'e-mail décrit des pantalons, des chemises, des chaussures ou des chapeaux. Et cela pourrait être le travail du Modèle 2.

Le Modèle 3 pourrait être utilisé uniquement pour les e-mails parlant de chemises, pour voir si le style de la chemise est mentionné. Et le Modèle 4 pourrait être utilisé uniquement pour les e-mails concernant les chaussures, pour voir si le style de la chaussure est mentionné. Vous pouvez voir à partir de cet exemple qu'une collection de modèles pourrait accomplir des prouesses dans votre application en se concentrant sur la portée et le but des modèles. Vous pouvez également combiner de manière programmatique votre modèle personnalisé avec un modèle standard, tel que l'API Cloud Natural Language.

![](Aspose.Words.824b27aa-2451-4c3d-ba49-00aad9ea075f.013.png)

Ceci conclut la discussion sur AutoML.

La stratégie d'application recommandée consiste tout d'abord à utiliser les services d'intelligence artificielle pré-construits. Ensuite, vous pouvez utiliser AutoML pour produire des modèles personnalisés qui peuvent être utilisés avec les services pré-construits ou indépendamment. N'oubliez pas que vous pouvez diviser un problème en parties spécialisées et utiliser plusieurs modèles personnalisés ensemble. Enfin, si vous découvrez que vous avez besoin de fonctionnalités plus avancées, vous pouvez utiliser les services d'apprentissage automatique et d'intelligence artificielle pour créer de nouveaux modèles.

## AutoML Vision

![](Aspose.Words.824b27aa-2451-4c3d-ba49-00aad9ea075f.014.png)

AutoML Vision se spécialise dans l'entraînement de modèles pour la classification d'images. Vous pouvez charger le fichier CSV et les fichiers d'images à partir du stockage Cloud ou les télécharger depuis votre ordinateur local en utilisant l'option d'importation.

La formation prend en charge plusieurs formats de fichiers, y compris JPEG et PNG. Les images peuvent avoir une taille allant jusqu'à 30 mégaoctets. Les images doivent être converties en encodage base64 qui stocke l'image sous la forme d'un fichier texte. Ainsi, le fichier préparé sera un fichier TXT ou un fichier ZIP compressé.

Le service ne reconnaît que les fichiers JPEG, PNG et GIF jusqu'à 1,5 mégaoctet.

Le modèle entraîné fonctionnera mieux lorsque le nombre d'images pour l'étiquette la plus courante sera au maximum 100 fois supérieur à celui de l'étiquette la moins courante. Par conséquent, pour des performances optimales du modèle, il est recommandé de supprimer les étiquettes de fréquence très faible.

Vous pouvez étiqueter les images dans l'interface utilisateur Web ou, dans certains cas, vous pouvez utiliser le service d'étiquetage humain proposé par Google si vous avez plus de 100 images non étiquetées.

Pour évaluer la préparation de votre modèle entraîné, AutoML Vision crée une matrice de confusion pour jusqu'à 10 étiquettes. Si vous avez plus de 10 étiquettes, la matrice inclut les 10 étiquettes avec le plus grand nombre de prédictions incorrectes.

Utilisez ces données pour évaluer la préparation de votre modèle.

Les formats de fichier pris en charge pour l'entraînement incluent JPEG, PNG, WEBP, GIF, BMP, TIFF, ICO jusqu'à 30 Mo.

Les requêtes du service prennent en charge les fichiers JPEG, PNG ou GIF jusqu'à 1,5 Mo.

![](Aspose.Words.824b27aa-2451-4c3d-ba49-00aad9ea075f.015.png)

La qualité des modèles personnalisés de Vision dépend grandement du choix des données d'entraînement.

Entraînez-vous sur des images ayant des caractéristiques similaires à celles que vous prévoyez de classifier. Par exemple,

des images avec une résolution similaire, un éclairage similaire, une mise au point similaire et un niveau de détail similaire.

Des scores de confusion élevés, des scores moyens de précision faibles ou des scores de précision et de rappel faibles peuvent

indiquer que votre modèle a besoin de données d'entraînement supplémentaires ou présente des étiquettes incohérentes.

Le perfectionnisme est l'ennemi du bien. Des scores de précision moyenne parfaits ou très élevés pourraient

indiquer qu'il y a quelque chose qui cloche dans le modèle. Les données sont trop faciles et pas assez variées.

Cela pourrait signifier que le modèle risque de ne pas bien fonctionner au-delà des données de test. Dans ce

cas, augmentez la variété d'images dans l'ensemble de données préparées.

## AutoML Natural Language

![](Aspose.Words.824b27aa-2451-4c3d-ba49-00aad9ea075f.016.png)

AutoML Natural Language se spécialise dans la formation de modèles pour les données textuelles. Par exemple, si vous disposez d'un ensemble d'articles de journaux, vous pouvez utiliser le service AutoML Natural Language pour classer si un article donné concerne, par exemple, le sport ou la politique.

- Le texte à reconnaître peut être un texte en ligne dans la cellule du fichier CSV.
- Plus couramment, le texte est contenu dans des documents qui sont des fichiers .txt ou compressés au format zip.
- Le chemin d'accès à l'emplacement de stockage Cloud du document apparaît dans le fichier CSV.
- Actuellement, les documents doivent être du texte standard et ne prennent pas en charge l'unicode.
- Les documents peuvent être aussi petits qu'une phrase ou jusqu'à un maximum de 128 kilo-octets.
- Vous pouvez avoir de 2 à 100 étiquettes.

Le modèle personnalisé est évalué selon la précision moyenne. Il s'agit d'une valeur de 0,5 à 1,0.

Son nom officiel est "l'aire sous la courbe de précision/rappel". Un nombre plus élevé indique une classification et une prédiction plus précises. Le rapport d'évaluation fournit également des courbes de seuil de confiance, qui caractérisent la classification des faux positifs par rapport aux vrais positifs. Pour les modèles qui appliquent une étiquette par document, l'évaluation comprend une matrice de confusion. Vous pouvez en savoir plus sur les évaluations et leur interprétation dans la documentation en ligne.

Vous pouvez également consulter les évaluations pour chaque étiquette.

Si un modèle personnalisé de traitement du langage naturel n'est pas utilisé pendant 60 jours, il sera supprimé. Si un modèle personnalisé de traitement du langage naturel est utilisé, il sera supprimé après 6 mois. Pour conserver un modèle, vous devrez le réentraîner. Les méthodes de formation et de service à l'intérieur d'AutoML sont régulièrement améliorées et mises à jour. Ces changements ne sont pas garantis d'être rétrocompatibles. Ils peuvent rendre un modèle personnalisé incompatible avec le service actuel. Vous devez donc prévoir de régénérer périodiquement le modèle personnalisé pour continuer à l'utiliser.

<https://cloud.google.com/natural-language/automl/docs/evaluate>

![](Aspose.Words.824b27aa-2451-4c3d-ba49-00aad9ea075f.017.png)

Un score de confusion élevé et des scores de précision moyenne faibles indiquent qu'un jeu de données préparé nécessite des entrées supplémentaires ou que les étiquettes sont utilisées de manière incohérente. Vous pouvez améliorer les évaluations de faible qualité pour des étiquettes particulières avec l'une de ces méthodes :

- Ajouter plus de documents associés à ces étiquettes. En d'autres termes, il se peut simplement qu'il n'y ait pas suffisamment de données d'entraînement pour obtenir un bon résultat.
- Vous devrez peut-être également augmenter la variété des documents en ajoutant des exemples plus longs ou plus courts, des documents avec différents styles d'écriture ou choix de mots, ou provenant d'auteurs différents.
- Enfin, pour les étiquettes qui ne sont pas utiles ou de qualité médiocre, vous voudrez peut-être les supprimer complètement afin d'augmenter la précision des étiquettes restantes.

## AutoML Tables

![](Aspose.Words.824b27aa-2451-4c3d-ba49-00aad9ea075f.018.png)

Alors que AutoML Vision et Natural Language sont destinés aux données non structurées, AutoML Table est conçu pour les données structurées. Le développement d'AutoML Table a été réalisé en collaboration entre Google Cloud et l'équipe Google Brain. Bien que les détails techniques du projet n'aient pas été rendus publics, l'équipe a essentiellement repris l'architecture utilisée pour la capacité de recherche dans les problèmes de classification d'images et de traduction, et a trouvé un moyen de l'appliquer aux données tabulaires.

![](Aspose.Words.824b27aa-2451-4c3d-ba49-00aad9ea075f.019.png)

Décrivons un ensemble de données dans lequel AutoML Tables se comporte très bien : le défi de suggestion de prix de Mercari. Mercari est la plus grande application de shopping communautaire et de place de marché du Japon. Mercari a créé un défi de suggestion de prix pour prédire le prix d'un produit proposé sur leur place de marché, afin de pouvoir donner des suggestions de prix à leurs vendeurs. Les participants ont reçu environ 1,5 million de lignes de données riches avec beaucoup de bruit. Le défi a duré 3 mois et s'est terminé par un prix de 100 000 $. Plus de 2000 data scientists ont participé au concours.

![](Aspose.Words.824b27aa-2451-4c3d-ba49-00aad9ea075f.020.png)

Ce graphique montre les performances d'AutoML Tables sur le défi Mercari pour différentes durées d'entraînement. Vous pouvez voir qu'après 24 heures d'entraînement, AutoML Tables vous place pratiquement en tête du classement. Même après seulement une heure d'entraînement, vous atteignez le palier des leaders, ce qui est une performance extrêmement impressionnante sur un ensemble de données de plus d'un million de lignes avec une complexité significative. Comparé au prix de 100 000 dollars de ce défi, une heure d'entraînement ne coûte que 19 dollars.

Étant donné que le processus de recherche d'AutoML Tables est aléatoire, vous pourriez obtenir des résultats légèrement différents si vous essayiez de reproduire ces performances.

![](Aspose.Words.824b27aa-2451-4c3d-ba49-00aad9ea075f.021.png)

Le moyen le plus simple d'importer vos données dans AutoML Tables est via BigQuery. Vous pouvez également importer des données à l'aide de fichiers CSV stockés localement ou dans Cloud Storage. L'un des avantages d'importer des données via BigQuery est sa prise en charge des tableaux (arrays) et des structures (structs). Quelle que soit la source d'importation, vos données doivent contenir entre 1 000 et 100 millions de lignes, entre 2 et 1 000 colonnes, et avoir une taille inférieure ou égale à 100 gigaoctets.

![](Aspose.Words.824b27aa-2451-4c3d-ba49-00aad9ea075f.022.png)

Une fois vos données importées, la prochaine étape consiste à sélectionner les fonctionnalités que vous souhaitez utiliser et à spécifier la colonne que vous essayez de prédire.

![](Aspose.Words.824b27aa-2451-4c3d-ba49-00aad9ea075f.023.png)

Dans la prochaine étape de la construction d'un modèle de table AutoML, vous passez par une phase de validation des données. Le but de cette étape est de vous assurer que vous ne transmettez pas de mauvaises données à votre modèle. Cela inclut la vérification des colonnes qui contiennent trop de valeurs nulles, des colonnes aberrantes qui faussent la distribution d'une colonne, ainsi que des colonnes qui ne sont pas corrélées à la cible que vous essayez de prédire.

![](Aspose.Words.824b27aa-2451-4c3d-ba49-00aad9ea075f.024.png)

Comme vous l'avez vu sur la diapositive sur les performances d'AutoML Table dans le défi Mercari, vous pouvez entraîner un modèle pendant une durée variable. Vous pouvez définir un budget d'entraînement en heures de nœud pour limiter les coûts. Par défaut, AutoML Tables arrêtera l'entraînement si le modèle ne montre plus de gains de performance significatifs.

![](Aspose.Words.824b27aa-2451-4c3d-ba49-00aad9ea075f.025.png)

Une fois que votre modèle est entraîné, vous devriez examiner les métriques d'entraînement. Méfiez-vous des modèles qui semblent trop beaux pour être vrais. Dans ce cas, il est probable que vous ayez un problème de données à résoudre. Pour la classification, le rapport comprend des métriques telles que l'aire sous la courbe pour la courbe précision-rappel, l'exactitude et le score F1. De plus, une matrice de confusion est générée ainsi que des importances de fonctionnalités. Ces deux ensembles de métriques sont particulièrement utiles pour diagnostiquer les modèles à faible performance. Pour les modèles de régression, l'erreur quadratique moyenne, l'erreur absolue moyenne en pourcentage et les importances de fonctionnalités sont renvoyées, parmi d'autres métriques. Consultez la documentation d'AutoML Table pour obtenir une liste complète des métriques générées après l'entraînement du modèle.

![](Aspose.Words.824b27aa-2451-4c3d-ba49-00aad9ea075f.026.png)

Il est probablement plus important d'examiner les mesures de performance générées sur l'ensemble de tests pour avoir une idée de la capacité de généralisation de votre modèle. Les mêmes mesures générées pour les données d'entraînement sont disponibles pour les données de test. Pour les modèles de classification, il peut être utile de définir le seuil de score sur une valeur autre que la valeur par défaut de 0,5. Augmentez le seuil de score pour que votre classificateur attribue une étiquette positive avec plus de confiance.

![](Aspose.Words.824b27aa-2451-4c3d-ba49-00aad9ea075f.027.png)

Une fois que vous êtes satisfait de la performance de votre modèle, vous pouvez le déployer.

Vous avez la possibilité de faire des prédictions par lots ou en ligne. Pour les prédictions en ligne, vous pouvez effectuer des appels à l'aide d'une commande curl, ou en utilisant l'une des API Java, node.js ou Python.

Les mêmes API sont disponibles pour les prédictions par lots. Vous pouvez effectuer des prédictions par lots sur des tables BigQuery ou des fichiers CSV. Cependant, les tables de source de données BigQuery ne doivent pas dépasser 100 gigaoctets. Pour les fichiers CSV, chaque fichier source de données ne peut pas dépasser 10 gigaoctets, et si vous incluez plusieurs fichiers, la somme de tous les fichiers ne peut pas dépasser 100 gigaoctets.

![](Aspose.Words.824b27aa-2451-4c3d-ba49-00aad9ea075f.028.png)

Pour conclure ce module, revenons à la question de quand utiliser BigQuery ML ou AutoML par rapport à la construction d'un modèle personnalisé.

La réponse courte est que cela dépend du temps que vous avez pour construire le modèle et des ressources dont vous disposez. Ce tableau peut vous fournir quelques indications. Étant donné la facilité de construction d'un modèle avec BigQuery ML ou AutoML, essayez d'abord l'un ou l'autre. Si le modèle obtenu n'est pas suffisant, alors vous devriez investir davantage de ressources dans le problème que vous cherchez à résoudre.
