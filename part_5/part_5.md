# Fonctionnalités et performances avancées de BigQuery

## Les fonctions de fenêtre analytiques

![](Aspose.Words.c0ddfc05-2164-4a0b-95e3-b2b6873ae9c5.001.png)

BigQuery, tout comme d'autres bases de données, dispose de fonctions intégrées pour permettre le calcul rapide des résultats.

Celles-ci comprennent des fonctions de fenêtre pour prendre en charge des analyses avancées.

Il existe trois groupes de fonctions :

- Les agrégations standard,
- Les fonctions de navigation, et
- Les fonctions de classement et de numérotation.

![](Aspose.Words.c0ddfc05-2164-4a0b-95e3-b2b6873ae9c5.002.png)

La fonction Count est une fonction fréquemment utilisée et auto-explicative.

![](Aspose.Words.c0ddfc05-2164-4a0b-95e3-b2b6873ae9c5.003.png)

D'autres fonctions d'agrégation standard sont répertoriées ici avec plus de détails et des instructions sur la manière de les utiliser correctement disponibles dans la documentation.

<https://cloud.google.com/bigquery/docs/reference/standard-sql/aggregate_functions>

![](Aspose.Words.c0ddfc05-2164-4a0b-95e3-b2b6873ae9c5.004.png)

La fonction LEAD renverra une valeur pour une ligne ultérieure par rapport à la ligne actuelle. Dans l'exemple, l'heure de location du vélo suivant est indiquée avec la ligne de location actuelle.

![](Aspose.Words.c0ddfc05-2164-4a0b-95e3-b2b6873ae9c5.005.png)

Les fonctions de navigation calculent généralement une expression de valeur sur une ligne différente de la fenêtre de la ligne actuelle. Voici quelques fonctions de navigation couramment utilisées.

<https://cloud.google.com/bigquery/docs/reference/standard-sql/navigation_functions>

![](Aspose.Words.c0ddfc05-2164-4a0b-95e3-b2b6873ae9c5.006.png)

Rank renvoie le rang ordinal (basé sur 1) de chaque ligne au sein de la partition ordonnée. Dans l'exemple, la durée de chaque station est renvoyée dans l'ordre décroissant des rangs, la durée la plus longue étant renvoyée en premier.

![](Aspose.Words.c0ddfc05-2164-4a0b-95e3-b2b6873ae9c5.007.png)

Cet exemple présente le classement des employés par ancienneté en utilisant la date de début dans chaque département.

Tout d'abord, les lignes sont partitionnées par département, puis triées par date de début, et enfin classées par rang.

![](Aspose.Words.c0ddfc05-2164-4a0b-95e3-b2b6873ae9c5.008.png)

Voici le code SQL utilisé pour effectuer l'opération RANK de l'exemple "classement des employés par ancienneté" sur la diapositive précédente.

![](Aspose.Words.c0ddfc05-2164-4a0b-95e3-b2b6873ae9c5.009.png)

L'addition de classement et de numérotation existe pour des cas d'utilisation spécifiques. Les exemples présentés ici sont fréquemment utilisés lors de la détermination des relations entre les lignes de données plutôt que par une mesure externe.

![](Aspose.Words.c0ddfc05-2164-4a0b-95e3-b2b6873ae9c5.010.png)

Les clauses WITH sont des instances d'une sous-requête nommée dans BigQuery. Les clauses WITH sont un moyen simple d'isoler les opérations SQL et de rendre les requêtes complexes plus faciles à gérer.

## Fonctions SIG (Système d'Information Géographique)

BigQuery dispose de nombreuses fonctionnalités intégrées de Système d'Information Géographique (SIG ou GIS en anglais). Vous en apprendrez davantage sur certaines d'entre elles dans cette leçon.

![](Aspose.Words.c0ddfc05-2164-4a0b-95e3-b2b6873ae9c5.011.png)

Dans l'exemple donné, un code postal est utilisé pour déterminer combien de stations de vélo se trouvent à moins d'un kilomètre du code postal et ont au moins 30 vélos disponibles. ST\_GeogPoint et ST\_DWithin sont utilisés ensemble pour localiser précisément les stations d'intérêt.

ST signifie simplement "type spatial".

![](Aspose.Words.c0ddfc05-2164-4a0b-95e3-b2b6873ae9c5.012.png)

ST\_DWithin est utilisé en conjonction avec les limites géospatiales des codes postaux américains. Les latitudes et longitudes des stations de vélo sont jointes ensemble avec ST\_GeogPoint pour créer un objet géospatial. La valeur de 1000 est utilisée pour représenter 1000 mètres, soit 1 kilomètre, comme distance entre les objets - la limite du code postal et le point de la station. Cela renverra uniquement ceux qui se trouvent à moins de 1 kilomètre.

![](Aspose.Words.c0ddfc05-2164-4a0b-95e3-b2b6873ae9c5.013.png)

ST\_GeogPoint crée un objet géospatial au format Well Known Text (WKT) à partir des valeurs fournies dans la base de données. Dans ce cas, nous utilisons la latitude et la longitude.

Si la latitude et la longitude sont fournies au format JSON, la fonction ST\_GeogFromGeoJSON peut être utilisée pour générer un objet géospatial.

![](Aspose.Words.c0ddfc05-2164-4a0b-95e3-b2b6873ae9c5.014.png)

Pour permettre des tests rapides de données géospatiales, Google Cloud propose l'application BigQuery GeoViz légère.

Cette application permettra de visualiser les données SIG avec une configuration minimale.

![](Aspose.Words.c0ddfc05-2164-4a0b-95e3-b2b6873ae9c5.015.png)

Comme mentionné précédemment, ST\_GeogPoint est utilisé pour créer un objet géospatial à partir de données pertinentes.

L'image montre les coordonnées exactes des valeurs d'ID sur une carte de Londres.

![](Aspose.Words.c0ddfc05-2164-4a0b-95e3-b2b6873ae9c5.016.png)

ST\_MakeLine et ST\_MakePolygon sont deux fonctions géospatiales supplémentaires qui peuvent être utilisées pour superposer des informations sur une carte afin de mettre en évidence les relations dans les données.

![](Aspose.Words.c0ddfc05-2164-4a0b-95e3-b2b6873ae9c5.017.png)

Comme mentionné dans notre exemple précédent, ST\_DWithin peut être utilisé pour déterminer la localisation relative de deux points ou objets.

Cette image montre des villes qui se trouvent toutes à une distance linéaire de 150 kilomètres de Terre Haute, Indiana.

![](Aspose.Words.c0ddfc05-2164-4a0b-95e3-b2b6873ae9c5.018.png)

Les fonctions ST\_Intersects, ST\_Contains et ST\_CoveredBy permettent de signaler la superposition ou la co-localisation d'objets géospatiaux.

## Considérations de performance

![](Aspose.Words.c0ddfc05-2164-4a0b-95e3-b2b6873ae9c5.019.png)

L'objectif de pratiquement chaque système d'information est de favoriser des décisions rapides et intelligentes.

Voici quelques bonnes pratiques à prendre en compte :

- Utilisez Dataflow pour effectuer le traitement et les transformations de données.
- Créez plusieurs tables pour une analyse facile.
- Utilisez BigQuery pour l'analyse en continu et les tableaux de bord, et stockez les données dans BigQuery pour un stockage à long terme à faible coût.
- De plus, créez des vues pour les requêtes courantes.

![](Aspose.Words.c0ddfc05-2164-4a0b-95e3-b2b6873ae9c5.020.png)

Explorer un ensemble de données à l'aide de SQL, ce n'est pas seulement écrire un bon code. Vous devez savoir quelle destination vous visez et la structure générale de vos données. Les bons analystes de données exploreront la façon dont l'ensemble de données est structuré avant même d'écrire une seule ligne de code.

![](Aspose.Words.c0ddfc05-2164-4a0b-95e3-b2b6873ae9c5.021.png)

Les gens analysent souvent des données et établissent un schéma au début d'un projet, sans jamais revoir ces décisions par la suite. Les hypothèses qu'ils ont formulées au départ peuvent avoir changé et ne sont plus valides. Ils tentent alors d'ajuster les processus ultérieurs sans jamais revoir et envisager de modifier certaines des décisions initiales.

Examinez les données. Peut-être étaient-elles réparties de manière équilibrée au début du projet, mais à mesure que le travail a progressé, les données ont pu devenir biaisées.

Examinez les schémas. Quels étaient les objectifs à l'époque ? Sont-ils toujours les mêmes aujourd'hui ? L'organisation des données est-elle optimisée pour les opérations actuelles ? Arrêtez d'accumuler du travail qui pourrait être fait plus tôt. Analogie : la vaisselle sale. Si vous la nettoyez au fur et à mesure de son utilisation, la cuisine reste propre. Si vous les sauvegardez, vous vous retrouvez avec un évier plein de vaisselle sale et beaucoup de travail.

![](Aspose.Words.c0ddfc05-2164-4a0b-95e3-b2b6873ae9c5.022.png)

Il existe cinq domaines clés pour l'optimisation des performances dans BigQuery, à savoir :

- Entrée et sortie - combien d'octets ont été lus depuis le disque ?
- Shuffling - combien d'octets ont été transmis à l'étape suivante du traitement de la requête ?
- Groupement - combien d'octets ont été transmis à chaque groupe ?
- Materialisation - combien d'octets sont écrits de manière permanente sur le disque ?
- Enfin, les fonctions et les UDF (User-Defined Functions), à quel point la requête est-elle coûteuse en termes de calcul sur votre CPU ?

Il existe un vieux dicton de la Silicon Valley : "Ne faites pas grossir vos problèmes. Résolvez-les tôt, quand ils sont encore petits."

![](Aspose.Words.c0ddfc05-2164-4a0b-95e3-b2b6873ae9c5.023.png)

Voici une liste de bonnes pratiques que vous devriez suivre dans le contexte de GCP :

- Ne sélectionnez pas plus de colonnes de données que nécessaire, évitez à tout prix d'utiliser SELECT \* lorsque vous le pouvez.
- Si vous avez un ensemble de données très volumineux, envisagez d'utiliser des fonctions d'agrégation approximatives plutôt que des fonctions régulières.
- Ensuite, utilisez largement la clause WHERE à tout moment pour filtrer les données.
- Ensuite, n'utilisez pas ORDER BY sur une clause ou des sous-requêtes larges, ou sur toute autre sous-requête que vous avez, appliquez ORDER BY seulement comme dernière opération que vous effectuerez.
- Pour les jointures, placez la table la plus volumineuse à gauche si possible, cela aidera BigQuery à l'optimiser et à effectuer ses jointures. Si vous oubliez, BigQuery fera probablement ces optimisations pour vous, vous ne verrez donc peut-être aucune différence.
- Vous pouvez utiliser des jokers dans les suffixes de table pour interroger plusieurs tables, mais essayez d'être aussi spécifique que possible avec ces jokers.
- Pour vos GROUP BY, si vous regroupez par les noms de chaque auteur de Wikipédia, ce qui signifie un grand nombre de valeurs distinctes ou une cardinalité élevée, c'est une mauvaise pratique ou un anti-pattern. Restez plutôt sur des groupements à faible valeur unique.
- Enfin, utilisez des tables partitionnées chaque fois que possible.

<https://cloud.google.com/bigquery/docs/best-practices-performance-compute>

![](Aspose.Words.c0ddfc05-2164-4a0b-95e3-b2b6873ae9c5.024.png)

Plus tôt, nous avons parlé de la façon de construire un entrepôt de données. Nous avons mentionné que vous pouvez optimiser les tables de votre entrepôt de données en réduisant le coût et la quantité de données lues. Cela peut être réalisé en partitionnant vos tables.

La partition des tables est très pertinente en termes de performances, donc revenons dans les prochaines diapositives sur certains des points principaux déjà abordés.

Vous activez la partition lors du processus de création de la table.

La diapositive montre comment migrer une table existante vers une table partitionnée en fonction de l'heure d'ingestion : utilisez simplement la table de destination. Cela vous coûtera une analyse de table.

BigQuery crée automatiquement de nouvelles partitions basées sur la date, sans nécessiter de maintenance supplémentaire. De plus, vous pouvez spécifier un délai d'expiration pour les données dans les partitions.

Les nouvelles données insérées dans une table partitionnée sont écrites dans la partition brute au moment de l'insertion. Pour contrôler explicitement dans quelle partition les données sont chargées, votre tâche de chargement peut spécifier une partition de date particulière.

![](Aspose.Words.c0ddfc05-2164-4a0b-95e3-b2b6873ae9c5.025.png)

Dans une table partitionnée par une colonne de date ou d'horodatage, chaque partition contient une seule journée de données. Lorsque les données sont stockées, BigQuery garantit que toutes les données dans un bloc appartiennent à une seule partition. Une table partitionnée maintient ces propriétés lors de toutes les opérations qui la modifient : les jobs de requête, les déclarations du langage de manipulation de données (DML), les déclarations du langage de définition de données (DDL), les jobs de chargement et les jobs de copie. Cela nécessite que BigQuery conserve plus de métadonnées qu'une table non partitionnée. À mesure que le nombre de partitions augmente, la quantité de surcharge de métadonnées augmente.

Bien que davantage de métadonnées doivent être conservées, en veillant à ce que les données soient partitionnées de manière globale, BigQuery peut estimer plus précisément le nombre d'octets traités par une requête avant son exécution. Ce calcul de coût fournit une limite supérieure sur le coût final de la requête.

Une bonne pratique consiste à exiger que les requêtes incluent toujours le filtre de partition. Assurez-vous que le champ de partition est isolé du côté gauche car c'est la seule façon pour BigQuery de rapidement éliminer les partitions inutiles.

![](Aspose.Words.c0ddfc05-2164-4a0b-95e3-b2b6873ae9c5.026.png)

Le clustering peut améliorer les performances de certains types de requêtes, telles que les requêtes utilisant des clauses de filtrage et celles agrégeant des données. Lorsque des données sont écrites dans une table clusterisée par une requête ou un job de chargement, BigQuery trie les données en utilisant les valeurs des colonnes de clustering. Ces valeurs sont utilisées pour organiser les données en plusieurs blocs dans le stockage de BigQuery. Lorsque vous soumettez une requête contenant une clause qui filtre les données en fonction des colonnes de clustering, BigQuery utilise les blocs triés pour éliminer les analyses de données inutiles.

De même, lorsque vous soumettez une requête qui agrège des données en fonction des valeurs des colonnes de clustering, les performances sont améliorées car les blocs triés regroupent les lignes ayant des valeurs similaires.

Dans cet exemple, la table est partitionnée par eventDate et clusterisée par userId. Maintenant, parce que la requête recherche des partitions dans une plage spécifique, seules 2 des 5 partitions sont prises en compte.

Étant donné que la requête recherche des userId dans une plage spécifique, BigQuery peut passer à la plage de lignes et ne lire que les lignes nécessaires pour chaque colonne.

![](Aspose.Words.c0ddfc05-2164-4a0b-95e3-b2b6873ae9c5.027.png)

Vous configurez le clustering lors de la création de la table. Ici, nous créons la table en partitionnant par "eventDate" et en regroupant par "userId". Nous indiquons également à BigQuery d'expirer les partitions qui ont plus de 3 jours.

Les colonnes que vous spécifiez dans le regroupement sont utilisées pour regrouper des données liées. Lorsque vous regroupez une table en utilisant plusieurs colonnes, l'ordre des colonnes que vous spécifiez est important. L'ordre des colonnes spécifiées détermine l'ordre de tri des données.

![](Aspose.Words.c0ddfc05-2164-4a0b-95e3-b2b6873ae9c5.028.png)

Au fil du temps, à mesure que de plus en plus d'opérations modifient une table, le degré de tri des données commence à s'affaiblir et la table devient seulement partiellement triée. Dans une table partiellement triée, les requêtes utilisant les colonnes de regroupement peuvent nécessiter la numérisation de plus de blocs par rapport à une table entièrement triée. Vous pouvez re-trier les données dans l'ensemble de la table en exécutant une requête SELECT \* qui sélectionne et réécrit la table, mais devinez quoi ! Vous n'avez plus besoin de le faire.

![](Aspose.Words.c0ddfc05-2164-4a0b-95e3-b2b6873ae9c5.029.png)

La bonne nouvelle est que BigQuery effectue désormais périodiquement l'auto-reclustering pour vous, de sorte que vous n'avez pas à vous soucier de vos clusters devenant obsolètes lorsque vous recevez de nouvelles données. Le re-clustering automatique est totalement gratuit et se déroule automatiquement en arrière-plan - vous n'avez rien d'autre à faire pour l'activer.

[https://cloud.google.com/blog/products/data-analytics/whats-happening-bigquery-adding-spe ed-and-flexibility-10x-streaming-quota-cloud-sql-federation-and-more](https://cloud.google.com/blog/products/data-analytics/whats-happening-bigquery-adding-speed-and-flexibility-10x-streaming-quota-cloud-sql-federation-and-more)

![](Aspose.Words.c0ddfc05-2164-4a0b-95e3-b2b6873ae9c5.030.png)

La partition permet d'obtenir des estimations de coûts précises pour les requêtes et garantit une amélioration des coûts et des performances.

Le regroupement offre des avantages supplémentaires en termes de coûts et de performances, en plus des avantages de la partition.

![](Aspose.Words.c0ddfc05-2164-4a0b-95e3-b2b6873ae9c5.031.png)

BigQuery prend en charge le regroupement (clustering) pour les tables partitionnées et non partitionnées.

Lorsque vous utilisez le regroupement (clustering) et la partitionnement ensemble, les données peuvent être partitionnées par une colonne de date ou de timestamp, puis regroupées (clustered) selon un ensemble de colonnes différent. Dans ce cas, les données de chaque partition sont regroupées (clustered) en fonction des valeurs des colonnes de regroupement (clustering). La partitionnement permet d'obtenir des estimations de coûts précises pour les requêtes.

Gardez à l'esprit que si vous n'avez pas de colonnes partitionnées et que vous souhaitez bénéficier des avantages du regroupement (clustering), vous pouvez créer une colonne "fake\_date" de type DATE et avoir toutes les valeurs à NULL.

![](Aspose.Words.c0ddfc05-2164-4a0b-95e3-b2b6873ae9c5.032.png)

Si vous créez une requête complexe à plusieurs étapes, chaque fois que vous l'exécutez, BigQuery lit l'ensemble des données requises par la requête. Cela signifie que toutes les données sont lues à chaque exécution de la requête. La matérialisation des tables intermédiaires consiste à diviser la requête en étapes. Chaque étape matérialise les résultats de la requête en les écrivant dans une table de destination. Le fait de consulter la petite table de destination réduit la quantité de données lues. En général, stocker les résultats matérialisés plus petits est plus efficace que traiter une plus grande quantité de données.

L'analogie utilisée est un vol en avion entre Sunnyvale, Californie, aux États-Unis et le Japon. Il existe un vol direct ou une série de quatre vols de correspondance plus courts. Le vol direct doit transporter le carburant pour l'ensemble du voyage, tandis que les vols de correspondance n'ont besoin que du carburant nécessaire pour chaque étape du voyage. La quantité totale de carburant utilisée pour l'atterrissage et le décollage (analogie de la matérialisation des tables intermédiaires) est inférieure à celle utilisée pour transporter l'ensemble des bagages pendant tout le voyage.

Voici un conseil : comparez les coûts de stockage des données avec les coûts de traitement des données. Le traitement d'un ensemble de données volumineux nécessitera davantage de ressources de traitement. La création de tables intermédiaires utilisera davantage de ressources de stockage. En général, le traitement des données est plus coûteux que le stockage des données. Cependant, vous pouvez effectuer vos propres calculs pour déterminer le point d'équilibre pour votre cas d'utilisation spécifique.

![](Aspose.Words.c0ddfc05-2164-4a0b-95e3-b2b6873ae9c5.033.png)

Une autre façon de vérifier combien d'enregistrements sont en cours de traitement consiste à cliquer sur l'onglet "Explication" dans l'interface utilisateur de BigQuery après avoir exécuté une requête.

Nous avons commencé avec 9,1 millions de lignes et les avons filtrées pour obtenir environ 36 000.

Les étapes de la requête représentent la façon dont BigQuery a planifié le travail nécessaire pour exécuter la tâche de requête.

![](Aspose.Words.c0ddfc05-2164-4a0b-95e3-b2b6873ae9c5.034.png)

Les fonctions approximatives sont un excellent moyen d'améliorer les performances. La fonction APPROX\_COUNT\_DISTINCT renvoie un résultat approximatif pour COUNT(DISTINCT expression). Le résultat est moins précis, mais il s'exécute beaucoup plus efficacement.

![](Aspose.Words.c0ddfc05-2164-4a0b-95e3-b2b6873ae9c5.035.png)

Un moyen simple de comprendre les performances de vos opérations BigQuery est par le biais de Cloud Monitoring, un composant par défaut de chaque projet Google Cloud.

Ces graphiques montrent l'utilisation des emplacements, les emplacements disponibles et les requêtes en cours pour une période d'une heure.

[Lab : Optimisation de vos requêtes BigQuery pour des performances optimales](https://www.cloudskillsboost.google/course_sessions/3849359/labs/345036)

![](Aspose.Words.c0ddfc05-2164-4a0b-95e3-b2b6873ae9c5.036.png)

La tarification du stockage est basée sur la quantité de données stockées dans vos tables lorsqu'elles ne sont pas compressées. La taille des données est calculée en fonction des types de données des colonnes individuelles. La tarification du stockage actif est calculée au prorata par Mo, par seconde.

Si une table n'est pas modifiée pendant 90 jours consécutifs, elle est considérée comme un stockage à long terme. Le prix du stockage pour cette table diminue automatiquement d'environ 50 pour cent. Il n'y a aucune dégradation des performances, de la durabilité, de la disponibilité ou de toute autre fonctionnalité.

Si la table est modifiée, le prix revient à la tarification normale du stockage et le compte à rebours de 90 jours recommence à zéro. Toute action qui modifie les données dans une table réinitialise le compte à rebours, y compris :

- Chargement de données dans une table
- Copie de données dans une table
- Écriture des résultats d'une requête dans une table
- Utilisation du langage de manipulation de données (Data Manipulation Language)
- Utilisation du langage de définition de données (Data Definition Language)
- Diffusion en continu de données dans la table

Toutes les autres actions ne réinitialisent pas le compte à rebours, notamment :

- Interrogation d'une table
- Création d'une vue qui interroge une table
- Exportation de données à partir d'une table
- Copie d'une table (vers une autre table de destination)
- Mise à jour ou modification d'une ressource de table.

<https://cloud.google.com/bigquery/pricing>

![](Aspose.Words.c0ddfc05-2164-4a0b-95e3-b2b6873ae9c5.037.png)

Étant donné que vous ne pouvez pas voir les machines virtuelles en cours d'exécution en arrière-plan, BigQuery expose des emplacements (slots) pour vous aider à gérer la consommation des ressources et les coûts. BigQuery calcule automatiquement le nombre d'emplacements requis par chaque requête, en fonction de la taille et de la complexité de la requête. La capacité et l'allocation par défaut des emplacements fonctionnent bien dans la plupart des cas. Vous pouvez surveiller l'utilisation des emplacements dans Cloud Monitoring.

Les circonstances où une capacité d'emplacement supplémentaire pourrait améliorer les performances sont des solutions avec des requêtes très complexes sur des ensembles de données très volumineux avec des charges de travail très concurrentes. Vous pouvez en savoir plus sur les emplacements dans la documentation en ligne ou contacter un représentant commercial.

![](Aspose.Words.c0ddfc05-2164-4a0b-95e3-b2b6873ae9c5.038.png)

La tarification à taux fixe est de 10 000 dollars pour 500 emplacements par mois. Une réduction de 25 % est offerte aux clients choisissant une durée minimale d'un an (7 500 dollars pour 500 emplacements).

La capacité est vendue par incréments de 500 emplacements, avec un minimum actuel de 500 emplacements.

Les emplacements Flex sont une option disponible pour vous permettre d'acheter des emplacements BigQuery pour de courtes durées.

![](Aspose.Words.c0ddfc05-2164-4a0b-95e3-b2b6873ae9c5.039.png)

Les "Flex Slots" vous permettent d'acheter des emplacements BigQuery pour de courtes durées, aussi peu que 60 secondes à la fois. Un emplacement est l'unité de capacité d'analyse de BigQuery. Les "Flex Slots" vous permettent de répondre rapidement à une demande d'analyse rapide et de vous préparer à des événements commerciaux tels que les jours fériés du commerce de détail et les lancements d'applications.

Les "Flex Slots" offrent aux utilisateurs des réservations BigQuery une immense flexibilité sans sacrifier la prévisibilité des coûts ou le contrôle. Les "Flex Slots" sont tarifés à 0,04 $ par emplacement par heure et sont disponibles par incréments de 100 emplacements. Il ne faut généralement que quelques minutes pour déployer les "Flex Slots" dans les réservations BigQuery.

Une fois déployés, vous pouvez les annuler après seulement 60 secondes et vous ne serez facturé que pour les secondes pendant lesquelles les "Flex Slots" sont déployés.

![](Aspose.Words.c0ddfc05-2164-4a0b-95e3-b2b6873ae9c5.040.png)

Vous pouvez combiner sans effort les Flex Slots avec les engagements annuels et mensuels existants pour compléter les charges de travail en état stable avec une capacité analytique à forte intensité. Pour de nombreuses entreprises, certains jours ou semaines de l'année revêtent une importance cruciale. Les détaillants se préoccupent du Black Friday et du Cyber Monday, les studios de jeux se concentrent sur les premiers jours de lancement de nouveaux titres, et les entreprises de services financiers se soucient des rapports trimestriels et de la saison des impôts. Les Flex Slots permettent à de telles organisations d'augmenter leur capacité analytique pendant les quelques jours nécessaires pour soutenir l'événement commercial, puis de la réduire par la suite, en ne payant que ce qu'elles ont consommé.

![](Aspose.Words.c0ddfc05-2164-4a0b-95e3-b2b6873ae9c5.041.png)

Il y a plusieurs considérations pour la tarification à forfait :

- Les Flex slots sont un type d'engagement spécial.
  - La durée de l'engagement est de seulement 60 secondes.
  - Vous pouvez annuler les Flex slots à tout moment par la suite.
  - Vous êtes facturé uniquement pour les secondes pendant lesquelles votre engagement était déployé.
  - Les Flex slots dépendent de la disponibilité de capacité. Lorsque vous essayez d'acheter des Flex slots, la réussite de cet achat n'est pas garantie. Cependant, une fois votre achat d'engagement réussi, votre capacité est garantie jusqu'à ce que vous l'annuliez.
- Les engagements mensuels ne peuvent pas être annulés pendant 30 jours après que votre engagement est actif. Après les premiers 30 jours calendaires, vous pouvez annuler ou rétrograder à tout moment. Si vous annulez ou rétrogradez, les frais sont calculés au prorata par seconde au taux mensuel. Par exemple :
  - Vous ne pouvez pas annuler le jour 29,
  - Si vous annulez pendant la première seconde du jour 31, vous êtes facturé pour 30 jours et 1 seconde, et
  - Si vous annulez à la moitié du troisième mois, vous êtes facturé 50% de votre taux mensuel pour ce mois.
- Avant l'anniversaire de la date de votre engagement, vous pouvez choisir de le renouveler pour une autre année, ou le convertir en engagement mensuel ou flexible. Si vous passez au tarif mensuel, vous pouvez annuler à tout moment, et vous êtes facturé au prorata par seconde au taux mensuel. Par exemple :
  - Si vous renouvelez pour une autre année après la date de votre engagement annuel, vous entrez dans un nouvel engagement annuel, et vous continuez à être facturé au taux d'engagement annuel.
  - De plus, si vous ne renouvelez pas pour une autre année après la date de votre engagement annuel, vous pouvez annuler à tout moment, et les frais sont calculés au prorata par seconde au taux mensuel.
  - Si vous déterminez que vous avez besoin de plus de slots BigQuery, vous pouvez acheter des incréments supplémentaires de 500. Cependant, cela créera un nouvel engagement.
- Lorsque vous achetez un plan à tarif fixe, vous spécifiez l'allocation des slots par emplacement. Pour utiliser des slots dans plusieurs emplacements, vous devez acheter des slots dans chaque emplacement.
- Un projet peut utiliser soit une tarification à forfait, soit une tarification à la demande. Si vous avez plusieurs projets dans un emplacement donné, vous pouvez choisir quels projets utilisent la tarification à forfait et quels projets utilisent la tarification à la demande.
- Enfin, pour interrompre un plan tarifaire à forfait, vous devez annuler ou rétrograder votre engagement, mais seulement APRÈS la période initiale d'engagement (30 jours ou 1 an).

![](Aspose.Words.c0ddfc05-2164-4a0b-95e3-b2b6873ae9c5.042.png)

BigQuery ne prend pas en charge la priorisation fine des requêtes interactives ou par lots. Afin d'éviter l'accumulation de tâches BigQuery et d'assurer une exécution dans les délais, il est crucial d'estimer correctement l'allocation des emplacements BigQuery. Actuellement, BigQuery interrompt toute requête qui dépasse 6 heures d'exécution.

![](Aspose.Words.c0ddfc05-2164-4a0b-95e3-b2b6873ae9c5.043.png)

Si une requête s'exécute dans BigQuery, elle a accès à la totalité des slots disponibles pour le projet ou la réservation, par défaut 2000.

Si nous exécutons soudainement une deuxième requête, BigQuery répartira les slots entre les 2 requêtes, en attribuant à chacune la moitié du nombre total de slots disponibles, dans ce cas 1000 chacune.

Cette subdivision des ressources de calcul continuera à se produire à mesure que d'autres requêtes sont exécutées.

En d'autres termes, il est peu probable qu'une requête gourmande en ressources domine le système et vole des ressources aux autres requêtes en cours d'exécution.

![](Aspose.Words.c0ddfc05-2164-4a0b-95e3-b2b6873ae9c5.044.png)

Dans le modèle tarifaire à forfait, les organisations disposent d'un nombre fixe d'emplacements. La simultanéité est équitable entre les projets, les utilisateurs et les requêtes. Par exemple, si vous disposez de 2 000 emplacements et de 2 projets, chaque projet peut bénéficier de jusqu'à 1 000 emplacements. Si l'un des projets en utilise moins, l'autre projet pourra utiliser tout le reste. Si vous avez 2 utilisateurs dans chaque projet, chaque utilisateur pourra obtenir 500 emplacements. Et si chacun des deux utilisateurs des deux projets lance deux requêtes, ils obtiendront chacun 500 emplacements.

Autrement dit, l'ajout de projets ne risque pas de dégrader les performances de manière significative.

[Lab : Tables partitionnées dans BigQuery](https://www.cloudskillsboost.google/course_sessions/3849359/labs/345039)
