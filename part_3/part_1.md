# Introduction à l'Ingénierie des Données sur GCP

Un ingénieur des données est quelqu'un qui construit des pipelines de données, nous commencerons donc par examiner ce que cela signifie - quels types de pipelines un ingénieur des données construit et leur objectif. Nous examinerons les défis associés à la pratique de l'ingénierie des données et comment beaucoup de ces défis sont plus faciles à résoudre lorsque vous construisez vos pipelines de données dans le cloud.

Ensuite, nous vous présenterons BigQuery, le data warehouse sans serveur à l'échelle du pétaoctet de Google Cloud.

Après avoir défini ce que sont les data lakes et les data warehouses, nous en discuterons plus en détail.

Les ingénieurs des données peuvent être responsables à la fois des systèmes de bases de données transactionnelles en backend qui prennent en charge les applications d'une entreprise et des data warehouses qui prennent en charge leurs charges de travail analytiques. Dans cette leçon, nous explorerons les différences entre les bases de données et les data warehouses, ainsi que les solutions Google Cloud pour chacune de ces charges de travail.

Étant donné qu'un data warehouse sert également d'autres équipes, il est crucial d'apprendre à collaborer efficacement avec elles.

Dans le cadre de votre rôle de partenaire efficace, votre équipe d'ingénierie sera chargée de mettre en place des politiques d'accès aux données et une gouvernance générale sur la manière dont les données doivent être utilisées et NON utilisées par vos utilisateurs. Nous discuterons de la manière de fournir un accès au data warehouse tout en respectant les meilleures pratiques de gouvernance des données.

Nous aborderons également la mise en production de l'ensemble de l'opération, ainsi que l'automatisation et la surveillance autant que possible.

Enfin, nous examinerons une étude de cas sur la façon dont un client de Google Cloud a résolu un problème commercial spécifique, avant de passer à un laboratoire pratique où vous utiliserez BigQuery pour analyser des données.

## Le rôle d'un ingénieur de données

![](Aspose.Words.0cb03f27-89c9-44eb-957f-9a25dcbaf91f.001.png)

Que fait un ingénieur de données ? Un ingénieur de données construit des pipelines de données.

Pourquoi l'ingénieur de données construit-il des pipelines de données ? Parce qu'il souhaite mettre ses données dans un endroit tel qu'un tableau de bord, un rapport ou un modèle d'apprentissage automatique, à partir duquel l'entreprise peut prendre des décisions basées sur les données.

Les données doivent être dans un état utilisable afin que quelqu'un puisse les utiliser pour prendre des décisions. Souvent, les données brutes ne sont pas très utiles par elles-mêmes.

![](Aspose.Words.0cb03f27-89c9-44eb-957f-9a25dcbaf91f.002.png)

Un terme que vous entendrez souvent lorsque vous faites de l'ingénierie des données dans le contexte de GCP est le concept de lac de données (data lake).

Un lac de données regroupe les données de toute l'entreprise en un seul emplacement. Ainsi, vous pouvez obtenir les données à partir d'une base de données relationnelle ou d'une feuille de calcul, et stocker les données brutes dans un lac de données.

Une option pour cet emplacement unique de stockage des données brutes consiste à les stocker dans un compartiment Cloud Storage.

Quels sont les principaux éléments à prendre en compte lors du choix entre les options de lac de données ? Qu'en pensez-vous ?

<https://cloud.google.com/solutions/build-a-data-lake-on-gcp#cloud-storage-as-data-lake>

![](Aspose.Words.0cb03f27-89c9-44eb-957f-9a25dcbaf91f.003.png)

Voici la traduction du texte dans le contexte de GCP (Google Cloud Platform) :

Il y a quelques considérations auxquelles vous devez penser lorsque vous construisez un lac de données.

1) Est-ce que votre lac de données gère tous les types de données que vous possédez
   1. Est-ce que tout peut tenir dans un bucket de stockage cloud ? Si vous avez une base de données relationnelle, il se peut que vous deviez placer les données dans Cloud SQL, une base de données gérée, plutôt que dans un stockage cloud.
1) Est-ce qu'il peut évoluer de manière élastique pour répondre à la demande ? À mesure que vos données collectées augmentent, est-ce que vous risquez de manquer d'espace disque ? C'est davantage un problème avec les systèmes sur site qu'avec le cloud.
1) Est-ce qu'il prend en charge une ingestion à débit élevé ? Quelle est la bande passante du réseau ? Avez-vous des points de présence en périphérie ?
1) Y a-t-il un contrôle d'accès granulaire aux objets ? Les utilisateurs ont-ils besoin de naviguer à l'intérieur d'un fichier ? Ou est-il suffisant d'obtenir un fichier dans son intégralité ? Cloud Storage est un stockage d'objets, donc vous devrez peut-être réfléchir à la granularité de ce que vous stockez.
1) Les autres outils peuvent-ils se connecter facilement ? Comment accèdent-ils au référentiel ? Ne perdez pas de vue que l'objectif d'un lac de données est de rendre les données accessibles pour l'analyse.

![](Aspose.Words.0cb03f27-89c9-44eb-957f-9a25dcbaf91f.004.png)

Nous avons mentionné notre premier produit Google Cloud, le compartiment de stockage Cloud Storage, qui est une bonne option pour regrouper toutes vos données brutes en un seul endroit avant de construire des pipelines de transformation vers votre entrepôt de données.

Pourquoi choisir le stockage Google Cloud ? Généralement, les entreprises utilisent Cloud Storage comme utilitaire de sauvegarde et d'archivage pour leurs activités. Grâce aux nombreux centres de données de Google et à la grande disponibilité du réseau, stocker des données dans un compartiment Cloud Storage est à la fois durable et performant.

En tant qu'ingénieur de données, vous utiliserez souvent un compartiment de stockage cloud dans le cadre de votre lac de données pour stocker différents fichiers de données brutes tels que CSV, JSON ou Avro. Vous pourriez ensuite les charger ou les interroger directement depuis BigQuery en tant qu'entrepôt de données.

Plus tard dans le cours, vous créerez des compartiments Cloud Shell à l'aide de la console Cloud et de la ligne de commande, comme vous le voyez ici. Une fois que vous avez configuré votre compartiment et chargé des données, d'autres produits et services de Google Cloud peuvent facilement interroger et s'intégrer avec votre compartiment.

![](Aspose.Words.0cb03f27-89c9-44eb-957f-9a25dcbaf91f.005.png)

Parlons du chargement des données. Et si vos données brutes nécessitent un traitement supplémentaire ? Vous devrez peut-être extraire les données de leur emplacement d'origine, les transformer, puis les charger.

Une option consiste à effectuer un traitement des données. Cela est souvent fait à l'aide de Dataproc ou de Dataflow. Nous aborderons l'utilisation de ces produits pour exécuter des pipelines par lots plus tard dans ce cours.

![](Aspose.Words.0cb03f27-89c9-44eb-957f-9a25dcbaf91f.006.png)

Mais que se passe-t-il si les pipelines par lots ne suffisent pas ? Et si vous avez besoin d'analyses en temps réel sur des données qui arrivent de manière continue et infinie ? Dans ce cas, vous pourriez recevoir les données dans Pub/Sub, les transformer à l'aide de Dataflow et les diffuser en continu dans BigQuery.

Nous aborderons les pipelines en continu plus tard dans ce cours.

## Défis en ingénierie des données sur GCP

![](Aspose.Words.0cb03f27-89c9-44eb-957f-9a25dcbaf91f.007.png)

En tant qu'ingénieur(e) des données, vous rencontrerez généralement quelques problèmes lors de la création de pipelines de données.

Vous pourriez avoir du mal à accéder aux données dont vous avez besoin. Vous pourriez constater que les données, même après y avoir accédé,... ne présentent pas la qualité requise par les analyses ou le modèle d'apprentissage automatique.

Vous prévoyez de construire un modèle, et même si la qualité des données est présente, vous pourriez constater que les transformations nécessitent des ressources de calcul qui pourraient ne pas être disponibles pour vous.

Enfin, vous pourriez rencontrer des défis en ce qui concerne les performances des requêtes et la possibilité d'exécuter toutes les requêtes et toutes les transformations dont vous avez besoin avec les ressources de calcul dont vous disposez.

![](Aspose.Words.0cb03f27-89c9-44eb-957f-9a25dcbaf91f.008.png)

Prenons le premier défi de consolider des ensembles de données disparates, des formats de données et de gérer l'accès à grande échelle dans le contexte de GCP.

![](Aspose.Words.0cb03f27-89c9-44eb-957f-9a25dcbaf91f.009.png)

For example, you want to compute the customer acquisition cost: how much does it cost in terms of marketing and promotions and discounts to acquire a customer? That data might be scattered across a variety of marketing products and customer relationship management software, … and finding a tool that can analyze all of this data might be difficult because it might come from different organizations, different tools, and different schemas, and maybe some of that data is not even structured. So in order to find something as essential to your business as how much getting a new customer costs, so that you can figure out what kind of discounts to offer to keep them from turning, you can’t have your data exist in silos.

![](Aspose.Words.0cb03f27-89c9-44eb-957f-9a25dcbaf91f.010.png)

Qu'est-ce qui rend l'accès aux données si difficile ? Principalement, cela est dû au fait que dans de nombreuses entreprises, les données sont cloisonnées par départements et chaque département crée ses propres systèmes transactionnels pour soutenir ses propres processus métier.

![](Aspose.Words.0cb03f27-89c9-44eb-957f-9a25dcbaf91f.011.png)

Donc, par exemple, vous pourriez avoir des systèmes opérationnels qui correspondent aux systèmes de magasins, un autre système opérationnel géré par vos entrepôts de produits qui gère votre inventaire, et un département marketing qui gère toutes les promotions que vous devez analyser à l'aide d'une requête analytique, par exemple, "Donnez-moi toutes les promotions en magasin pour les commandes récentes ainsi que leurs niveaux de stock."

Vous devez savoir comment combiner les données provenant des magasins, des promotions et des niveaux de stock, et parce que celles-ci sont toutes stockées dans des systèmes séparés - dont certains ont un accès restreint - la création d'un système analytique qui utilise ces trois ensembles de données pour répondre à une requête ad hoc comme celle-ci peut être très difficile.

![](Aspose.Words.0cb03f27-89c9-44eb-957f-9a25dcbaf91f.012.png)

Le deuxième défi est que le nettoyage, le formatage et la préparation des données pour les insights nécessitent la création de pipelines ETL.

Les pipelines ETL sont généralement nécessaires pour garantir l'exactitude et la qualité des données. Les données nettoyées et transformées sont généralement stockées, non pas dans un lac de données, mais dans un entrepôt de données.

Un entrepôt de données est un endroit consolidé pour stocker les données, et toutes les données peuvent être facilement jointes et interrogées. Contrairement à un lac de données, où les données sont au format brut, dans l'entrepôt de données, les données sont stockées de manière à ce qu'il soit efficace de les interroger.

![](Aspose.Words.0cb03f27-89c9-44eb-957f-9a25dcbaf91f.013.png)

Parce que les données ne deviennent utiles qu'après avoir été nettoyées, vous devriez supposer que toutes les données brutes que vous collectez à partir de systèmes sources doivent être nettoyées et transformées. Et si vous les transformez, autant les transformer dans un format qui les rende efficaces à interroger. En d'autres termes, effectuez une extraction-transformation-chargement (ETL) des données et stockez-les dans un entrepôt de données. Prenons l'exemple où vous êtes un détaillant et vous devez consolider les données provenant de plusieurs systèmes sources. Réfléchissez à l'utilisation prévue. Supposons que le cas d'utilisation consiste à obtenir les promotions en magasin les plus performantes en France.

Vous devez obtenir les données des magasins ainsi que les données des promotions. Cependant, il se peut que les données des magasins soient incomplètes. Peut-être que certaines transactions sont en espèces et, pour celles-ci, il se peut qu'il n'y ait pas d'informations sur l'identité du client ; ou certaines transactions peuvent être réparties sur plusieurs reçus, et vous devrez peut-être combiner ces transactions car elles proviennent du même client. Ou peut-être que les horodatages des produits sont stockés en heure locale, alors que vous devez travailler à l'échelle mondiale, et donc avant de pouvoir faire quoi que ce soit, vous devez convertir toutes les données en temps universel coordonné (UTC).

De même, les promotions peuvent ne pas du tout être stockées dans la base de données des transactions. Elles pourraient être simplement un fichier texte que quelqu'un charge sur sa page web et qui contient une liste de codes utilisés par l'application web pour appliquer des réductions.

Il peut être extrêmement difficile d'effectuer une requête pour trouver les promotions en magasin les plus performantes car les données posent de nombreux problèmes. Chaque fois que vous avez des données de ce type, vous devez obtenir les données brutes et les transformer en une forme avec laquelle vous pouvez réellement effectuer les analyses nécessaires.

Il est évidemment préférable de pouvoir effectuer ce type de nettoyage et de consolidation une seule fois et de stocker les données résultantes pour faciliter les analyses ultérieures. C'est là l'objectif d'un entrepôt de données (data warehouse).

![](Aspose.Words.0cb03f27-89c9-44eb-957f-9a25dcbaf91f.014.png)

Si vous devez effectuer une consolidation et un nettoyage importants, un problème courant qui se pose est l'endroit où effectuer ce calcul. La disponibilité des ressources de calcul peut être un défi dans le contexte de GCP (Google Cloud Platform).

![](Aspose.Words.0cb03f27-89c9-44eb-957f-9a25dcbaf91f.015.png)

Si vous utilisez un système sur site, les ingénieurs de données devront gérer la capacité des serveurs et des clusters, et s'assurer qu'il existe suffisamment de capacité pour exécuter les tâches ETL. Le problème est que les ressources de calcul nécessaires pour ces tâches ETL ne sont pas constantes dans le temps. Très souvent, elles varient d'une semaine à l'autre, en fonction de facteurs tels que les jours fériés et les ventes promotionnelles. Cela signifie que lorsque le trafic est faible, vous gaspillez de l'argent et lorsque le trafic est élevé, vos tâches prennent beaucoup trop de temps.

![](Aspose.Words.0cb03f27-89c9-44eb-957f-9a25dcbaf91f.016.png)

Une fois que vos données sont dans votre entrepôt de données, vous devez optimiser les requêtes que vos utilisateurs exécutent afin d'utiliser de manière optimale vos ressources de calcul.

![](Aspose.Words.0cb03f27-89c9-44eb-957f-9a25dcbaf91f.017.png)

Si vous gérez un cluster d'analyse de données sur site, vous serez responsable de choisir un moteur de requête, d'installer le logiciel du moteur de requête et de le maintenir à jour, ainsi que de provisionner des serveurs supplémentaires pour augmenter la capacité.

N'y a-t-il pas un moyen plus efficace de gérer la charge des serveurs afin que nous puissions nous concentrer sur les insights ?

## Introduction à BigQuery

Il existe une bien meilleure façon de gérer la charge des serveurs afin que nous puissions nous concentrer sur les informations essentielles. Il s'agit d'utiliser un entrepôt de données sans serveur. BigQuery est l'entrepôt de données sans serveur à l'échelle du pétaoctet de Google Cloud. Vous n'avez pas besoin de gérer des clusters. Concentrez-vous simplement sur les informations essentielles.

![](Aspose.Words.0cb03f27-89c9-44eb-957f-9a25dcbaf91f.018.png)

Le service BigQuery remplace la configuration matérielle typique d'un entrepôt de données traditionnel. En d'autres termes, il sert de lieu de rassemblement pour toutes les données analytiques d'une organisation.

Les ensembles de données sont des collections de tables qui peuvent être divisées selon les lignes métier ou un domaine analytique donné. Chaque ensemble de données est lié à un projet Google Cloud.

Un lac de données peut contenir des fichiers dans Cloud Storage ou Google Drive, voire des données transactionnelles de Cloud Bigtable. BigQuery peut définir un schéma et effectuer des requêtes directement sur des données externes en tant que sources de données fédérées.

Les tables de base de données et les vues fonctionnent de la même manière dans BigQuery que dans un entrepôt de données traditionnel, ce qui permet à BigQuery de prendre en charge les requêtes rédigées dans un dialecte SQL standard conforme à ANSI:2011.

La gestion des identités et des accès est utilisée pour accorder des autorisations permettant d'effectuer des actions spécifiques dans BigQuery. Cela remplace les instructions SQL GRANT et REVOKE utilisées pour gérer les autorisations d'accès dans les bases de données SQL traditionnelles.

![](Aspose.Words.0cb03f27-89c9-44eb-957f-9a25dcbaf91f.019.png)

Une considération clé derrière l'agilité est la capacité à faire plus avec moins, et il est important de s'assurer que vous ne faites pas des choses qui n'ajoutent pas de valeur.

Si vous effectuez un travail qui est commun à plusieurs industries, ce n'est probablement pas quelque chose que votre entreprise souhaite payer.

Le cloud vous permet, en tant qu'ingénieur de données, de passer moins de temps à gérer le matériel et plus de temps à faire des choses beaucoup plus personnalisées et spécifiques à l'activité.

Vous n'avez pas à vous soucier de la provision, de la fiabilité et des améliorations d'utilisation des performances ou de l'optimisation sur le cloud, vous pouvez donc consacrer tout votre temps à réfléchir à la manière d'obtenir de meilleures informations à partir de vos données.

![](Aspose.Words.0cb03f27-89c9-44eb-957f-9a25dcbaf91f.020.png)

Vous n'avez pas besoin de provisionner des ressources avant d'utiliser BigQuery, contrairement à de nombreux systèmes de gestion de bases de données relationnelles (RDBMS). BigQuery alloue dynamiquement des ressources de stockage et d'interrogation en fonction de vos modèles d'utilisation.

Les ressources de stockage sont allouées au fur et à mesure que vous les consommez et sont désallouées lorsque vous supprimez des données ou supprimez des tables.

Les ressources d'interrogation sont allouées en fonction du type et de la complexité de l'interrogation. Chaque requête utilise un certain nombre de slots, qui sont des unités de calcul comprenant une certaine quantité de CPU et de RAM.

## Data Lakes et Data Warehouses

![](Aspose.Words.0cb03f27-89c9-44eb-957f-9a25dcbaf91f.021.png)

Rappelez-vous que nous avons souligné que les données doivent être dans un état utilisable afin que quelqu'un puisse utiliser ces données pour prendre des décisions. Bien souvent, les données brutes ne sont pas très utiles en elles-mêmes.

![](Aspose.Words.0cb03f27-89c9-44eb-957f-9a25dcbaf91f.022.png)

Nous avons dit que les données brutes sont répliquées et stockées dans un lac de données. Afin de rendre les données exploitables, vous utiliserez des pipelines d'extraction-transformation-chargement (ETL) pour rendre les données utilisables et stocker ces données plus utilisables dans un entrepôt de données.

Considérons maintenant quels sont les principaux éléments à prendre en compte lors du choix entre les options d'entrepôt de données...

![](Aspose.Words.0cb03f27-89c9-44eb-957f-9a25dcbaf91f.023.png)

Nous devons nous poser ces questions :

- Le data warehouse va certainement servir de destination - vous allez y stocker des données. Mais sera-t-il alimenté par un pipeline par lots ou par un pipeline en continu
  - Le data warehouse doit-il être précis jusqu'à la minute ? Ou est-il suffisant de charger les données une fois par jour ou par semaine ?
- Le data warehouse pourra-t-il s'adapter à mes besoins en termes de mise à l'échelle
  - De nombreux entrepôts de données basés sur des clusters imposent des limites de requêtes concurrentes par cluster. Ces limites de requêtes poseront-elles un problème ? La taille du cluster sera-t-elle suffisante pour stocker et parcourir vos données ?
- Comment les données sont-elles organisées, répertoriées et contrôlées en termes d'accès ? Serez-vous en mesure de partager l'accès aux données avec toutes les parties prenantes ? Que se passe-t-il s'ils veulent interroger les données ? Qui paiera les requêtes ?
- Le data warehouse est-il conçu pour des performances optimales ? Encore une fois, considérez attentivement les performances des requêtes concurrentes. Et que ces performances soient fournies dès le départ, ou si vous devez créer des index et ajuster le data warehouse.
- Enfin, quel niveau de maintenance votre équipe d'ingénierie devra-t-elle assurer ?

![](Aspose.Words.0cb03f27-89c9-44eb-957f-9a25dcbaf91f.024.png)

Les entrepôts de données traditionnels sont difficiles à gérer et à exploiter. Ils ont été conçus pour un paradigme de traitement par lots de l'analyse de données et pour les besoins de reporting opérationnel. Les données dans l'entrepôt de données étaient destinées à être utilisées uniquement par quelques responsables pour des besoins de reporting. BigQuery est un entrepôt de données moderne qui change le mode conventionnel des entrepôts de données. Voici quelques-unes des principales comparaisons entre un entrepôt de données traditionnel et BigQuery.

BigQuery fournit des mécanismes de transfert de données automatisés et alimente les applications métier en utilisant une technologie que les équipes connaissent déjà et utilisent, de sorte que tout le monde a accès aux informations sur les données. Vous pouvez créer des sources de données partagées en lecture seule que les utilisateurs internes et externes peuvent interroger, et rendre les résultats des requêtes accessibles à tous via des outils conviviaux tels que Looker, Google Sheets, Tableau ou Google Data Studio.

BigQuery jette les bases de l'IA. Il est possible d'entraîner des modèles Tensorflow et Google Cloud Machine Learning directement avec des ensembles de données stockés dans BigQuery, et BigQuery ML peut être utilisé pour créer et entraîner des modèles d'apprentissage automatique avec du SQL simple. Une autre capacité étendue est BigQuery GIS, qui permet aux organisations d'analyser des données géographiques dans BigQuery, essentielles pour de nombreuses décisions commerciales critiques liées aux données de localisation.

BigQuery permet également aux organisations d'analyser en temps réel les événements commerciaux au fur et à mesure de leur déroulement, en ingérant automatiquement les données et en les rendant immédiatement disponibles pour les requêtes dans leur entrepôt de données. Cela est rendu possible par la capacité de BigQuery à ingérer jusqu'à 100 000 lignes de données par seconde et à interroger des pétaoctets de données à des vitesses extrêmement rapides.

Grâce à l'infrastructure entièrement gérée et sans serveur de Google, ainsi qu'à son réseau disponible mondialement, BigQuery élimine les travaux liés à la provision et à la maintenance d'une infrastructure d'entrepôt de données traditionnelle.

BigQuery simplifie également les opérations sur les données grâce à l'utilisation de la gestion des identités et des accès pour contrôler l'accès des utilisateurs aux ressources, en créant des rôles et des groupes et en attribuant des autorisations pour l'exécution de tâches et de requêtes dans un projet, tout en assurant également la sauvegarde automatique des données et les réplications.

![](Aspose.Words.0cb03f27-89c9-44eb-957f-9a25dcbaf91f.025.png)

Bien que nous ayons parlé de l'importation des données dans BigQuery en exécutant des pipelines ETL, il existe une autre option. Il s'agit de traiter BigQuery comme un moteur de requête et de lui permettre d'interroger les données sur place. Par exemple, vous pouvez utiliser BigQuery pour interroger directement les données de la base de données dans Cloud SQL - c'est-à-dire les bases de données relationnelles gérées telles que PostgreSQL et MySQL. Vous pouvez également utiliser BigQuery pour interroger directement des fichiers sur Cloud Storage tant que ces fichiers sont au format CSV ou Parquet. Le véritable avantage réside dans le fait que vous pouvez laisser vos données en place et les joindre à d'autres données dans l'entrepôt de données. Regardons cela de plus près.

## Bases de données transactionnelles versus entrepôts de données.

Les ingénieurs de données peuvent être responsables à la fois des systèmes de bases de données transactionnelles en arrière-plan qui soutiennent les applications de votre entreprise ET des entrepôts de données qui soutiennent les charges de travail analytiques. Dans cette leçon, vous explorerez les différences entre les bases de données et les entrepôts de données, ainsi que les solutions Google Cloud pour chaque charge de travail.

![](Aspose.Words.0cb03f27-89c9-44eb-957f-9a25dcbaf91f.026.png)

Si vous disposez de SQL Server, MySQL ou PostgreSQL comme base de données relationnelle, vous pouvez les migrer vers Cloud SQL, la solution de base de données relationnelle entièrement gérée de Google Cloud.

Cloud SQL offre des performances élevées et une évolutivité avec une capacité de stockage allant jusqu'à 64 téraoctets, 60 000 IOPS et 624 gigaoctets de RAM par instance. Vous pouvez profiter de l'auto-évolutivité du stockage pour gérer les besoins croissants de la base de données sans interruption.

Une question que l'on pourrait vous poser est : "Pourquoi ne pas simplement utiliser Cloud SQL pour les flux de travail de génération de rapports ? Vous pouvez exécuter directement des requêtes SQL sur la base de données, n'est-ce pas ?"

<https://cloud.google.com/products/databases/>

![](Aspose.Words.0cb03f27-89c9-44eb-957f-9a25dcbaf91f.027.png)

C'est une excellente question et elle sera abordée en détail dans le module "Construction d'un entrepôt de données". Google Cloud propose plusieurs options pour les SGBDR, notamment Spanner et Cloud SQL.

Lorsque vous envisagez d'utiliser Cloud SQL, sachez que Cloud SQL est optimisé pour être une base de données transactionnelle (ou écritures) et que BigQuery est un entrepôt de données optimisé pour les charges de travail de reporting (principalement des lectures). L'architecture fondamentale de ces options de stockage de données est assez différente. Les bases de données Cloud SQL utilisent un stockage basé sur les ENREGISTREMENTS, ce qui signifie que l'ensemble de l'enregistrement doit être ouvert sur le disque, même si vous ne sélectionnez qu'une seule colonne dans votre requête.

BigQuery utilise un stockage basé sur les COLONNES, ce qui permet, comme vous pouvez le deviner, d'avoir des schémas de reporting très larges, car vous pouvez simplement lire des colonnes individuelles à partir du disque.

![](Aspose.Words.0cb03f27-89c9-44eb-957f-9a25dcbaf91f.028.png)

Cela ne veut pas dire que les systèmes de gestion de bases de données relationnelles (RDBMS) ne sont pas performants par rapport aux entrepôts de données - ils servent à deux fins différentes. Les RDBMS aident votre entreprise à gérer de nouvelles transactions.

Prenons cet exemple de terminal de point de vente dans un magasin. Chaque commande et produit est probablement enregistré en tant que nouvelles entrées dans une base de données relationnelle quelque part. Cette base de données peut stocker l'ensemble des commandes reçues depuis leur site web, l'ensemble des produits répertoriés dans le catalogue ou le nombre d'articles en stock.

Cela permet de mettre à jour rapidement la base de données lorsque une commande existante est modifiée. Les systèmes transactionnels permettent de modifier une seule ligne dans une table de base de données de manière cohérente. Ils sont également construits sur certains principes de base de données relationnelles, tels que l'intégrité référentielle, pour éviter des cas tels qu'un client commandant un produit qui n'existe pas dans la table des produits.

Alors, où toutes ces données brutes se retrouvent-elles dans notre discussion sur le lac de données et l'entrepôt de données ? Quelle est l'image complète ?

![](Aspose.Words.0cb03f27-89c9-44eb-957f-9a25dcbaf91f.029.png)

Voici. Nos systèmes opérationnels, tels que nos bases de données relationnelles qui stockent les commandes en ligne, les stocks et les promotions, sont nos sources de données brutes à gauche. Notez que cela n'est pas exhaustif - vous pouvez également avoir d'autres systèmes sources qui sont manuels, tels que des fichiers CSV ou des feuilles de calcul.

Ces sources de données en amont sont rassemblées dans un emplacement consolidé unique dans notre Data Lake, qui est conçu pour la durabilité et une disponibilité élevée.

Once in the data lake, the data often needs to be processed via transformations that then output the data into our data warehouse where it is ready for use by downstream teams. Here are three quick examples of other teams that often build pipelines on our data warehouse:

- Une équipe ML peut construire un pipeline pour obtenir des caractéristiques (features) pour leurs modèles
- Une équipe d'ingénierie peut utiliser nos données dans le cadre de leur entrepôt de données sur la plateforme GCP.
- Et une équipe BI pourrait vouloir créer des tableaux de bord en utilisant certaines de nos données.

Alors, qui travaille dans ces équipes et comment collaborent-elles avec notre équipe d'ingénierie des données dans le contexte de GCP ?

## Collaborer efficacement avec d'autres équipes de données

![](Aspose.Words.0cb03f27-89c9-44eb-957f-9a25dcbaf91f.030.png)

N'oubliez pas qu'une fois que vous avez des données où elles peuvent être utiles et qu'elles sont dans un état exploitable, nous devons ajouter une nouvelle valeur aux données grâce à l'analyse et à l'apprentissage automatique. Quelles équipes pourraient compter sur nos données ?

![](Aspose.Words.0cb03f27-89c9-44eb-957f-9a25dcbaf91f.031.png)

Il existe de nombreuses équipes de données qui dépendent de votre entrepôt de données et de partenariats avec l'ingénierie des données pour construire et maintenir de nouvelles pipelines de données.

Les trois clients les plus courants sont :

- L'ingénieur en apprentissage automatique
- L'analyste de données ou BI, et
- Les autres ingénieurs de données

Examinons comment chacun de ces rôles interagit avec votre nouvel entrepôt de données et comment les ingénieurs de données peuvent travailler en partenariat avec eux.

![](Aspose.Words.0cb03f27-89c9-44eb-957f-9a25dcbaf91f.032.png)

Comme vous le verrez dans notre cours sur l'apprentissage automatique, les modèles d'une équipe de ML reposent sur la disponibilité de nombreuses données d'entrée de haute qualité pour créer, entraîner, tester, évaluer et déployer leurs modèles. Ils travailleront souvent en partenariat avec des équipes d'ingénierie des données pour construire des pipelines et des ensembles de données à utiliser dans leurs modèles.

Deux questions courantes auxquelles vous pourriez être confronté.

![](Aspose.Words.0cb03f27-89c9-44eb-957f-9a25dcbaf91f.033.png)

"Combien de temps faut-il pour qu'une transaction passe de données brutes jusqu'à l'entrepôt de données ?" Ils posent cette question car toutes les données sur lesquelles ils entraînent leurs modèles doivent également être disponibles au moment des prédictions. S'il y a un délai important dans la collecte et l'agrégation des données brutes, cela affectera la capacité de l'équipe d'apprentissage automatique à créer des modèles utiles.

![](Aspose.Words.0cb03f27-89c9-44eb-957f-9a25dcbaf91f.034.png)

Une deuxième question à laquelle on vous demandera certainement de répondre est de savoir à quel point il serait difficile d'ajouter des colonnes ou des lignes de données supplémentaires à certains ensembles de données. Encore une fois, l'équipe d'apprentissage automatique compte sur l'identification des relations entre les colonnes de données et sur l'existence d'un historique riche pour former des modèles. Vous gagnerez la confiance de vos partenaires d'équipe en apprentissage automatique en rendant vos ensembles de données facilement découvrables, documentés et disponibles pour les équipes d'apprentissage automatique afin de pouvoir y expérimenter rapidement.

![](Aspose.Words.0cb03f27-89c9-44eb-957f-9a25dcbaf91f.035.png)

Une caractéristique unique de BigQuery est que vous pouvez créer des modèles d'apprentissage automatique performants directement dans BigQuery en utilisant simplement SQL grâce à BigQuery ML. Voici le code réel du modèle pour CRÉER un modèle, L'ÉVALUER, et ensuite FAIRE des prédictions. Vous verrez cela à nouveau dans nos cours sur l'apprentissage automatique plus tard.

![](Aspose.Words.0cb03f27-89c9-44eb-957f-9a25dcbaf91f.036.png)

D'autres parties prenantes essentielles sont vos équipes d'intelligence d'affaires et d'analystes de données qui dépendent de données propres et fiables pour effectuer des requêtes afin de découvrir des informations et créer des tableaux de bord. Ces équipes ont besoin d'ensembles de données avec des définitions de schéma clairement définies, la possibilité de prévisualiser rapidement les lignes et des performances pouvant s'adapter à de nombreux utilisateurs de tableaux de bord simultanés.

![](Aspose.Words.0cb03f27-89c9-44eb-957f-9a25dcbaf91f.037.png)

Un des produits Google Cloud qui aide à gérer les performances des tableaux de bord est BigQuery BI Engine. BI Engine est un service d'analyse rapide en mémoire intégré directement dans BigQuery et disponible pour accélérer vos applications d'intelligence d'affaires.

Historiquement, les équipes d'intelligence d'affaires devaient construire, gérer et optimiser leurs propres serveurs BI et cubes OLAP pour prendre en charge les applications de reporting. Maintenant, avec BI Engine, vous pouvez obtenir un temps de réponse aux requêtes inférieur à la seconde sur vos ensembles de données BigQuery sans avoir à créer vos propres cubes. BI Engine est construit sur la même architecture de stockage et de calcul BigQuery, et utilise des serveurs en mémoire rapide pour fournir un service de mise en cache intelligent qui maintient l'état.

<https://www.youtube.com/watch?v=TqlrIcmqPgo>

![](Aspose.Words.0cb03f27-89c9-44eb-957f-9a25dcbaf91f.038.png)

Un dernier groupe de parties prenantes concerne les autres ingénieurs de données qui dépendent de la disponibilité et des performances de votre entrepôt de données et de vos pipelines pour leurs lacs de données et entrepôts de données en aval.

Ils demanderont souvent : "Comment pouvez-vous garantir que le pipeline de données dont nous dépendons sera toujours disponible lorsque nous en aurons besoin ?"

Ou bien : "Nous constatons une demande élevée pour certains ensembles de données très populaires. Comment pouvez-vous surveiller et mettre à l'échelle la santé de l'ensemble de votre écosystème de données ?"

![](Aspose.Words.0cb03f27-89c9-44eb-957f-9a25dcbaf91f.039.png)

- Une manière populaire est d'utiliser la surveillance Cloud intégrée de toutes les ressources sur Google Cloud.
- Étant donné que Google Cloud Storage et BigQuery sont des ressources, vous pouvez configurer des alertes et des notifications pour des métriques telles que "Nombre de requêtes" ou "Octets de données traités" afin de mieux suivre l'utilisation et les performances.
- Deux autres raisons pour lesquelles la surveillance Cloud est utilisée sont le suivi des dépenses de toutes les différentes ressources utilisées et les tendances de facturation de votre équipe ou organisation.
- Enfin, vous pouvez utiliser les journaux d'audit Cloud pour afficher des informations réelles sur les travaux de requête afin de voir des détails granulaires sur les requêtes exécutées et par qui. Cela est utile si vous avez des ensembles de données sensibles que vous devez surveiller de près. Nous en discuterons plus en détail dans la suite.

<https://cloud.google.com/bigquery/docs/monitoring>

## Gérer l'accès aux données et la gouvernance

Dans le cadre de votre rôle en tant que partenaire efficace, votre équipe d'ingénierie sera chargée de mettre en place des politiques d'accès aux données et une gouvernance générale sur la manière dont les données doivent être utilisées et NE doivent PAS être utilisées par vos utilisateurs.

![](Aspose.Words.0cb03f27-89c9-44eb-957f-9a25dcbaf91f.040.png)

Voici ce que nous entendons lorsque nous disons qu'un ingénieur des données doit gérer les données. Cela comprend des sujets critiques tels que la confidentialité et la sécurité. Quelles sont quelques considérations clés lors de la gestion de certains ensembles de données ?

![](Aspose.Words.0cb03f27-89c9-44eb-957f-9a25dcbaf91f.041.png)

Clairément communiquer un modèle de gouvernance des données pour :

- Qui devrait avoir accès et qui ne devrait pas avoir accès ?
- Comment les informations personnellement identifiables (comme les numéros de téléphone ou les adresses e-mail) sont-elles gérées ?
- Et même des tâches plus basiques comme comment nos utilisateurs finaux découvriront les différents ensembles de données que nous avons pour l'analyse ?

![](Aspose.Words.0cb03f27-89c9-44eb-957f-9a25dcbaf91f.042.png)

Une solution pour la gouvernance des données dans le contexte de GCP est le Cloud Data Catalog et l'API Data Loss Prevention (DLP).

- Le Data Catalog rend toutes les métadonnées de vos ensembles de données disponibles pour une recherche par vos utilisateurs. Vous regroupez des ensembles de données avec des balises, marquez certaines colonnes comme sensibles, etc.
- Pourquoi est-ce utile ? Si vous disposez de nombreux ensembles de données différents avec de nombreuses tables différentes auxquelles différents utilisateurs ont différents niveaux d'accès, le Data Catalog offre une expérience utilisateur unifiée pour découvrir rapidement ces ensembles de données. Fini la recherche de noms de table spécifiques en SQL au préalable.
- Souvent utilisée conjointement avec le Data Catalog, l'API Data Loss Prevention (DLP) ou DLP API, vous aide à mieux comprendre et gérer les données sensibles. Elle offre une classification et une suppression rapides et évolutives pour les éléments de données sensibles tels que les numéros de carte de crédit, les noms, les numéros de sécurité sociale, les numéros d'identification américains et internationaux sélectionnés, les numéros de téléphone et les identifiants de Google Cloud.

## Créer des pipelines prêts pour la production.

Une fois que vos data lakes et vos entrepôts de données sont mis en place et que votre politique de gouvernance est en place, il est temps de rendre l'ensemble de l'opération opérationnel et d'automatiser et de surveiller autant que possible.

![](Aspose.Words.0cb03f27-89c9-44eb-957f-9a25dcbaf91f.043.png)

C'est ce que nous entendons lorsque nous disons "industrialiser le processus de données". Il doit s'agir d'un système de traitement de données complet, évolutif et pouvant être mis en production.

![](Aspose.Words.0cb03f27-89c9-44eb-957f-9a25dcbaf91f.044.png)

Votre équipe d'ingénierie des données est responsable de la santé des infrastructures - c'est-à-dire des pipelines - et veille à ce que les données soient disponibles et à jour pour les charges de travail analytiques et d'apprentissage automatique (ML).

Les questions courantes que vous devriez poser à cette étape sont les suivantes :

- Comment pouvons-nous garantir la santé des pipelines et la propreté des données ?
- Comment pouvons-nous industrialiser ces pipelines afin de réduire la maintenance et maximiser le temps de disponibilité ?
- Comment pouvons-nous réagir et nous adapter aux schémas et aux besoins métier changeants ?
- Et utilisons-nous les outils et les meilleures pratiques les plus récents en ingénierie des données ?

![](Aspose.Words.0cb03f27-89c9-44eb-957f-9a25dcbaf91f.045.png)

Un outil couramment utilisé pour l'orchestration des flux de travail par les entreprises est Apache Airflow dans le cadre de Google Cloud Platform (GCP).

![](Aspose.Words.0cb03f27-89c9-44eb-957f-9a25dcbaf91f.046.png)

Google Cloud propose une version entièrement gérée d'Airflow appelée Cloud Composer. Cloud Composer aide votre équipe d'ingénierie des données à orchestrer toutes les pièces du puzzle de l'ingénierie des données dont nous avons discuté jusqu'à présent (et même plus que vous n'avez pas encore rencontrées !).

Par exemple, lorsque un nouveau fichier CSV est déposé dans Cloud Storage, vous pouvez automatiquement déclencher un événement qui lance un flux de travail de traitement des données et place ces données directement dans votre entrepôt de données.

La puissance de cet outil réside dans le fait que les produits et services Google Cloud pour le big data disposent de points d'API que vous pouvez appeler.

Une tâche Cloud Composer peut ensuite s'exécuter chaque nuit ou chaque heure et lancer l'intégralité de votre pipeline, depuis les données brutes jusqu'au lac de données, en passant par l'entrepôt de données.

Nous aborderons plus en détail l'orchestration des flux de travail dans les modules ultérieurs et vous réaliserez également un laboratoire sur Cloud Composer.

[Lab : Utilisation de BigQuery pour effectuer des analyses](https://www.cloudskillsboost.google/course_sessions/3754403/labs/382256)
