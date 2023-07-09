# Conception de systèmes de traitement de données

![](Aspose.Words.26c0f64e-6eda-41da-9774-5d9b364446b8.001.png)

Vous allez voir que ces trois éléments apparaissent dans la première partie de l'examen avec des considérations similaires, mais pas identiques.

Les mêmes questions ou intérêts apparaissent dans différents contextes. Représentation des données, pipelines, infrastructure de traitement. Par exemple, les innovations technologiques pourraient rendre obsolète la représentation des données d'une solution choisie. Le pipeline de traitement des données pourrait avoir mis en œuvre une transformation très complexe qui est maintenant disponible sous la forme d'une commande unique et efficace. Et l'infrastructure pourrait être remplacée par un service offrant des qualités plus désirables.

Cependant, comme vous le verrez, chaque partie présente des préoccupations supplémentaires. Par exemple, la "Disponibilité du système" est importante pour le traitement des pipelines, mais pas pour la représentation des données. Et la "Capacité" est importante pour le traitement, mais pas pour le pipeline abstrait ou la représentation.

![](Aspose.Words.26c0f64e-6eda-41da-9774-5d9b364446b8.002.png)

Stockage et bases de données - Services qui permettent de stocker et de récupérer des données ; ils diffèrent par leurs méthodes de stockage et de récupération qui les rendent plus efficaces pour des cas d'utilisation spécifiques.

![](Aspose.Words.26c0f64e-6eda-41da-9774-5d9b364446b8.003.png)

Traitement basé sur le serveur - Des services qui permettent à du code d'application et à des logiciels de s'exécuter, en utilisant des données stockées pour effectuer des opérations - des actions et des transformations - et produire des résultats.

![](Aspose.Words.26c0f64e-6eda-41da-9774-5d9b364446b8.004.png)

Services intégrés - combine le stockage et le traitement évolutif dans un cadre conçu pour traiter les données (plutôt que des applications générales). Plus efficace et flexible que les solutions de serveur/base de données isolées.

![](Aspose.Words.26c0f64e-6eda-41da-9774-5d9b364446b8.005.png)

Intelligence artificielle - Méthodes pour aider à identifier (taguer), catégoriser et prédire ; trois actions qui sont très difficiles, voire impossibles à réaliser dans le traitement des données sans apprentissage automatique.

![](Aspose.Words.26c0f64e-6eda-41da-9774-5d9b364446b8.006.png)

Services de pré et post-traitement - Travailler avec les données et les pipelines avant le traitement (comme le nettoyage des données) ou après le traitement (comme la visualisation des données). Le pré et le post-traitement sont des éléments importants d'une solution de traitement des données.

![](Aspose.Words.26c0f64e-6eda-41da-9774-5d9b364446b8.007.png)

Services d'infrastructure - Tous les services de base qui connectent et intègrent le traitement des données et les éléments informatiques dans une solution complète. Cela inclut la messagerie, les systèmes, l'import/export des données, la sécurité, la surveillance, et ainsi de suite.

![](Aspose.Words.26c0f64e-6eda-41da-9774-5d9b364446b8.008.png)

Le stockage et les systèmes de base de données sont conçus et optimisés pour le stockage et la récupération de données. Ils ne sont pas vraiment conçus pour effectuer des transformations de données. On suppose dans leur conception que la puissance de calcul nécessaire pour effectuer ces transformations est externe au stockage ou à la base de données.

La méthode d'organisation et la méthode d'accès de chacun de ces services sont efficaces pour des cas spécifiques. Par exemple, une base de données Cloud SQL est très performante pour stocker des transactions individuelles cohérentes. Cependant, elle n'est pas réellement optimisée pour stocker de grandes quantités de données non structurées telles que des fichiers vidéo.

Les services de base de données effectuent des opérations minimales sur les données dans le contexte de la méthode d'accès. Par exemple, les requêtes SQL peuvent regrouper, accumuler, compter et résumer les résultats d'une requête de recherche.

Voici un conseil d'examen : Connaissez les différences entre Cloud SQL et Cloud Spanner, et quand utiliser chacun d'entre eux.

![](Aspose.Words.26c0f64e-6eda-41da-9774-5d9b364446b8.009.png)

Les éléments différenciateurs du service comprennent les méthodes d'accès, le coût ou la vitesse des actions spécifiques, la taille des données et la manière dont les données sont organisées et stockées.

Les détails et les différences entre les technologies de données seront abordés ultérieurement dans ce cours.

Conseil d'examen : apprenez à identifier les technologies à partir de leurs propriétés. Par exemple, quelle technologie de données offre l'ingestion la plus rapide des données ? Quelle technologie utiliseriez-vous pour l'ingestion de données en continu ?

![](Aspose.Words.26c0f64e-6eda-41da-9774-5d9b364446b8.010.png)

Les services gérés sont ceux dans lesquels vous pouvez voir l'instance individuelle ou le cluster.

Conseil d'examen - les services gérés impliquent toujours une certaine charge informatique. Cela n'élimine pas complètement la charge ou les procédures manuelles, mais les réduit au minimum par rapport aux solutions sur site.

![](Aspose.Words.26c0f64e-6eda-41da-9774-5d9b364446b8.011.png)

Les services sans serveur réduisent davantage la responsabilité de l'informatique, de sorte que la gestion des serveurs sous-jacents ne fait pas partie de vos tâches et les instances individuelles ne sont pas visibles.

![](Aspose.Words.26c0f64e-6eda-41da-9774-5d9b364446b8.012.png)

Une addition plus récente à cette liste est Firestore. Firestore est une base de données de documents NoSQL conçue pour un dimensionnement automatique. Elle offre des performances élevées et une facilité de développement d'applications. De plus, elle comprend un "mode de compatibilité Datastore".

![](Aspose.Words.26c0f64e-6eda-41da-9774-5d9b364446b8.013.png)

Comme mentionné, le stockage et les bases de données offrent des capacités de traitement limitées. De plus, ce qu'ils offrent est dans le contexte de la recherche et de la récupération. Mais si vous avez besoin d'effectuer des actions et des transformations plus sophistiquées sur les données, vous aurez besoin d'un logiciel de traitement des données et de puissance de calcul. Alors, où pouvez-vous obtenir ces ressources ?

Vous pourriez utiliser l'une de ces plateformes de calcul pour écrire votre propre application ou des parties d'une application qui utilisent des services de stockage ou de base de données.

Vous pourriez installer un logiciel open source tel que MySQL, une base de données open source, ou Hadoop, une plateforme de traitement de données open source, sur un moteur de calcul.

Les solutions de création personnalisée sont principalement motivées par les besoins de l'entreprise. Elles impliquent généralement plus de frais généraux liés aux technologies de l'information que l'utilisation d'un service de plateforme cloud.

![](Aspose.Words.26c0f64e-6eda-41da-9774-5d9b364446b8.014.png)

Ces trois services de traitement des données sont présents dans presque toutes les solutions d'ingénierie des données. Chacun se chevauche avec les autres, ce qui signifie que certains travaux peuvent être accomplis dans deux ou trois de ces services. Une solution avancée peut utiliser un, deux ou les trois services.

Les services de traitement des données combinent le stockage et le calcul et automatisent les aspects de stockage et de calcul du traitement des données grâce à des abstractions. Par exemple, dans Dataproc, l'abstraction des données (avec Spark) est un ensemble de données réparti résilient (RDD) et l'abstraction de traitement est un graphe acyclique dirigé (DAG).

La mise en œuvre du stockage et du traitement sous forme d'abstractions permet aux systèmes sous-jacents de s'adapter à la charge de travail et permet à l'utilisateur / ingénieur de données de se concentrer sur les données et les problèmes commerciaux qu'il essaie de résoudre.

![](Aspose.Words.26c0f64e-6eda-41da-9774-5d9b364446b8.015.png)

Il y a une grande valeur potentielle dans l'innovation de produits ou de processus en utilisant l'apprentissage automatique (Machine Learning). L'apprentissage automatique peut rendre les données non structurées, telles que les journaux, utiles en identifiant ou en catégorisant les données, permettant ainsi l'intelligence d'affaires. Reconnaître une occurrence de quelque chose qui existe est étroitement lié à prédire une occurrence future basée sur une expérience passée. L'apprentissage automatique est utilisé pour l'identification, la catégorisation et la prédiction. Il peut rendre les données non structurées utiles.

Votre astuce pour l'examen est de comprendre la gamme de technologies d'apprentissage automatique proposées sur Google Cloud et de savoir quand utiliser chacune d'entre elles.

![](Aspose.Words.26c0f64e-6eda-41da-9774-5d9b364446b8.016.png)

Une solution d'ingénierie des données implique l'ingestion des données, leur gestion pendant le traitement, l'analyse et la visualisation. Ces éléments peuvent être cruciaux pour les besoins commerciaux.

Voici quelques services avec lesquels vous devriez généralement être familiarisé :

- Les services de transfert de données fonctionnent en ligne, et un appareil de transfert de données est un dispositif expédiable utilisé pour synchroniser les données dans le cloud avec une source externe.
- Cloud Data Studio est utilisé pour la visualisation des données une fois qu'elles ont été traitées.
- Dataprep est utilisé pour préparer ou conditionner les données et préparer les pipelines avant le traitement des données.

Notebooks est un espace de travail autonome qui contient du code, exécute le code et affiche les résultats.

Dialogflow est un service de création de chatbots. Il utilise l'intelligence artificielle pour fournir une méthode d'interaction directe avec les données.

![](Aspose.Words.26c0f64e-6eda-41da-9774-5d9b364446b8.017.png)

Votre conseil pour l'examen est de vous familiariser avec les services d'infrastructure qui sont couramment utilisés dans les solutions d'ingénierie des données. Ils sont souvent utilisés en raison des fonctionnalités clés qu'ils offrent.

![](Aspose.Words.26c0f64e-6eda-41da-9774-5d9b364446b8.018.png)

Par exemple, Pub/Sub peut conserver un message pendant jusqu'à sept jours, offrant une résilience aux solutions d'ingénierie des données qui seraient autrement très difficiles à mettre en œuvre. Chaque service dans Google Cloud peut être utilisé dans une solution d'ingénierie des données. Cependant, certains des services les plus courants et importants sont présentés ici. Pub/Sub, un service de messagerie, est présent dans pratiquement toutes les solutions de données en direct ou en streaming car il sépare l'arrivée des données de leur ingestion.

![](Aspose.Words.26c0f64e-6eda-41da-9774-5d9b364446b8.019.png)

VPN Cloud, Interconnexion avec un partenaire (Partner Interconnect) ou Interconnexion dédiée (Dedicated Interconnect) jouent un rôle chaque fois qu'il y a des données sur site qui doivent être transmises vers des services dans le cloud.

![](Aspose.Words.26c0f64e-6eda-41da-9774-5d9b364446b8.020.png)

IAM, les règles de pare-feu et la gestion des clés sont essentiels pour certains secteurs verticaux, tels que les industries de la santé et des services financiers. Et chaque solution doit être surveillée et gérée, ce qui implique généralement des panneaux affichés dans la console Cloud et l'envoi de données vers le service Cloud Monitoring.

![](Aspose.Words.26c0f64e-6eda-41da-9774-5d9b364446b8.021.png)

Il est judicieux d'examiner des solutions d'échantillons qui utilisent des technologies de traitement des données ou d'ingénierie des données, et de porter une attention particulière aux composants d'infrastructure de la solution. Il est important de savoir ce que les services apportent aux solutions de données et de se familiariser avec leurs fonctionnalités clés et options.

Il y a beaucoup de détails que je ne mémoriserais pas. Par exemple, le nombre exact d'IOPS pris en charge par une instance spécifique est quelque chose que je m'attendrais à consulter plutôt qu'à connaître par cœur. De même, le coût d'un type d'instance particulier

par rapport à un autre type d'instance, avec des valeurs réelles, n'est pas quelque chose que je m'attendrais à connaître en tant qu'ingénieur des données. Je chercherais ces détails si j'en avais besoin. Cependant, le fait qu'une instance n4-standard ait un nombre d'IOPS supérieur à une instance n1-standard, ou que l'instance n4-standard coûte plus cher qu'une instance n1-standard, sont des concepts que je DOIS connaître en tant qu'ingénieur des données.

## Conception de représentations de données flexibles

Le concept clé que nous allons explorer est de comprendre comment les données sont stockées et donc comment elles sont traitées.

Il existe différentes abstractions pour stocker les données. Et si vous stockez les données dans une abstraction plutôt qu'une autre, cela facilite ou accélère différents processus.

Par exemple, si vous stockez les données dans un système de fichiers, il est plus facile de récupérer ces données par leur nom.

Si vous stockez les données dans une base de données, il est plus facile de trouver des données en utilisant la logique, telle que SQL.

Et si vous stockez les données dans un système de traitement, il est plus facile et plus rapide de transformer les données, pas seulement de les récupérer.

![](Aspose.Words.26c0f64e-6eda-41da-9774-5d9b364446b8.022.png)

L'ingénieur Data doit être familier avec les concepts de base et la terminologie de la représentation des données.

Par exemple, si un problème est décrit en utilisant les termes "rangées" et "colonnes", puisque ces concepts sont utilisés dans SQL, vous pourriez déjà penser à une base de données SQL telle que Cloud SQL ou Cloud Spanner.

Si une question d'examen décrit une Entité et un Type ("Kind") - qui sont des concepts utilisés dans Datastore - et que vous ne savez pas ce qu'ils sont, vous aurez du mal à répondre à la question.

Vous n'aurez pas le temps ni les ressources pour les rechercher pendant l'examen. Vous devez les connaître avant de commencer.

Un conseil pour l'examen est qu'il est bon de savoir COMMENT les données sont stockées et dans quel but ou cas d'utilisation la base de données est optimisée.

![](Aspose.Words.26c0f64e-6eda-41da-9774-5d9b364446b8.023.png)

Les données plates et sérialisées sont faciles à manipuler, mais elles manquent de structure et donc de signification. Si vous souhaitez représenter des données qui ont des relations significatives, vous avez besoin d'une méthode qui non seulement représente les données, mais aussi les relations.

- CSV, qui signifie Comma Separated Values, est un format de fichier simple utilisé pour stocker des données tabulaires.
- XML, qui signifie Extensible Markup Language, a été conçu pour stocker et transporter des données, et a été conçu pour être auto-descriptif.
- JSON, qui signifie JavaScript Object Notation, est un format d'échange de données léger basé sur des paires nom/valeur et une liste ordonnée de valeurs, qui se mappe facilement aux objets courants dans de nombreux langages de programmation.

![](Aspose.Words.26c0f64e-6eda-41da-9774-5d9b364446b8.024.png)

Le réseau transmet des données sérielles sous forme d'un flux de bits - des zéros et des uns. Et les données sont stockées sous forme de bits. Cela signifie que si vous avez un objet de données avec une structure significative, vous avez besoin d'une méthode pour aplatir et sérialiser les données en premier lieu, afin qu'elles ne contiennent que des zéros et des uns. Ensuite, elles peuvent être transmises et stockées. Et lorsqu'elles sont récupérées, les données doivent être désérialisées pour restaurer la structure en un objet de données significatif. Un exemple de logiciel qui fait cela est Avro.

Avro est un framework de sérialisation de données et d'appels de procédures à distance développé au sein du projet Hadoop d'Apache. Il utilise JSON pour définir les types de données et les protocoles, et sérialise les données dans un format binaire compact. Son utilisation principale se trouve dans Apache Hadoop, où il peut fournir à la fois un format de sérialisation pour les données persistantes et un format de communication entre les nœuds Hadoop, ainsi qu'entre les programmes clients et les services Hadoop.

![](Aspose.Words.26c0f64e-6eda-41da-9774-5d9b364446b8.025.png)

Il est utile de comprendre les types de données pris en charge dans différents systèmes de représentation. Par exemple, il existe un type de données dans SQL moderne appelé NUMERIC. NUMERIC est similaire au point flottant. Cependant, il permet de stocker une valeur de 38 chiffres avec 9 chiffres pour représenter l'emplacement de la virgule décimale. NUMERIC est très utile pour stocker les fractions courantes associées à l'argent. NUMERIC évite l'erreur d'arrondi qui se produit dans une représentation en point flottant complète, c'est pourquoi il est principalement utilisé pour les transactions financières.

Maintenant, pourquoi ai-je mentionné le type de données NUMERIC ? Parce que pour comprendre NUMERIC, vous devez déjà connaître la différence entre les nombres entiers et les nombres à virgule flottante, et vous devez déjà connaître les erreurs d'arrondi qui peuvent se produire lors de l'exécution de calculs sur certains types de représentations de données à virgule flottante. Donc, si vous comprenez cela, vous comprenez déjà beaucoup des autres éléments que vous devez connaître pour SQL et l'ingénierie des données.

Vous devriez également vous assurer de connaître ces types de données de base.

![](Aspose.Words.26c0f64e-6eda-41da-9774-5d9b364446b8.026.png)

Vos données dans BigQuery sont stockées dans des tables d'un ensemble de données. Voici un exemple des abstractions associées à une technologie particulière. Vous devez déjà savoir que chaque ressource dans Google Cloud existe à l'intérieur d'un projet. Et en plus de la sécurité et du contrôle d'accès, un projet lie l'utilisation d'une ressource à une carte de crédit - c'est ce qui rend une ressource facturable.

Ensuite, dans BigQuery, les données sont stockées dans des ensembles de données. Et les ensembles de données contiennent des tables. Et les tables contiennent des colonnes. Lorsque vous traitez les données, BigQuery crée un job. Souvent, le job exécute une requête SQL. Bien qu'il existe également des activités de mise à jour et de maintenance prises en charge à l'aide du langage de manipulation des données, ou DML.

Astuce pour l'examen : connaître la hiérarchie des objets au sein d'une technologie de données et comment ils sont liés les uns aux autres.

![](Aspose.Words.26c0f64e-6eda-41da-9774-5d9b364446b8.027.png)

BigQuery est appelé un "magasin colonne", ce qui signifie qu'il est conçu pour le traitement des colonnes, pas des lignes. Le traitement des colonnes est très économique et rapide dans BigQuery, tandis que le traitement des lignes est lent et coûteux.

La plupart des requêtes ne portent que sur un petit nombre de champs et BigQuery n'a besoin de lire que les colonnes pertinentes pour exécuter une requête. Étant donné que chaque colonne contient des données du même type, BigQuery peut compresser les données de colonne de manière beaucoup plus efficace.

Vous pouvez facilement ajouter des données en continu aux tables BigQuery, mais vous ne pouvez pas facilement modifier les valeurs existantes.

La réplication des données trois fois aide également le système à déterminer les nœuds de calcul optimaux pour effectuer des opérations de filtrage, de mélange, et ainsi de suite.

![](Aspose.Words.26c0f64e-6eda-41da-9774-5d9b364446b8.028.png)

Vous traitez vos données dans Dataproc sur Spark comme une entité unique. Mais Spark connaît la vérité.

Vos données sont stockées dans des ensembles de données distribués et résilients, appelés RDD (Resilient Distributed Datasets).

Les RDD sont une abstraction qui masque les détails complexes sur la façon dont les données sont localisées et répliquées dans un cluster.

Spark partitionne les données en mémoire à travers le cluster et sait comment récupérer les données grâce à la généalogie d'un RDD, au cas où quelque chose se passe mal.

Spark a la capacité de diriger le traitement là où il y a des ressources de traitement disponibles.

La partition des données, la réplication des données, la récupération des données, le pipeline de traitement - tout cela est automatisé par Spark afin que vous n'ayez pas à vous en soucier.

Voici un conseil pour l'examen : vous devriez savoir comment différentes services stockent les données et comment chaque méthode est optimisée pour des cas d'utilisation spécifiques, comme mentionné précédemment. Mais comprenez également la valeur clé de l'approche. Dans ce cas, les RDD masquent la complexité et permettent à Spark de prendre des décisions à votre place.

![](Aspose.Words.26c0f64e-6eda-41da-9774-5d9b364446b8.029.png)

Il existe plusieurs concepts que vous devez connaître concernant Dataflow.

Vos données dans Dataflow sont représentées par des PCollections.

Le pipeline présenté dans cet exemple lit les données à partir de BigQuery, effectue un ensemble de traitements et écrit sa sortie dans Cloud Storage.

![](Aspose.Words.26c0f64e-6eda-41da-9774-5d9b364446b8.030.png)

Dans Dataflow, chaque étape est une transformation, et l'ensemble des transformations forme un pipeline.

![](Aspose.Words.26c0f64e-6eda-41da-9774-5d9b364446b8.031.png)

L'ensemble du pipeline est exécuté par un programme appelé runner.

Pour le développement, il existe un Runner local, et pour la production, il existe un Runner Cloud.

![](Aspose.Words.26c0f64e-6eda-41da-9774-5d9b364446b8.032.png)

Lorsque le pipeline s'exécute sur le cloud GCP, chaque étape, chaque transformation, est appliquée à une PCollection et donne lieu à une autre PCollection. Ainsi, la PCollection est l'unité de données qui traverse le pipeline. De plus, chaque étape est mise à l'échelle de manière élastique.

L'idée est d'écrire du code Python ou Java et de le déployer sur Dataflow, qui exécute ensuite le pipeline dans un contexte évolutif et sans serveur.

Contrairement à Dataproc, il n'est pas nécessaire de lancer ou de mettre à l'échelle un cluster. Tout cela est géré automatiquement.

![](Aspose.Words.26c0f64e-6eda-41da-9774-5d9b364446b8.033.png)

Dataflow est conçu pour utiliser le même pipeline, les mêmes opérations, le même code à la fois pour le traitement par lots (Batch) et le traitement en continu (Stream). Rappelons que les données par lots sont également appelées données bornées, et elles sont généralement stockées dans un fichier. Les données par lots ont une fin définie.

Les données en continu sont également appelées données non bornées et peuvent être générées de manière dynamique. Par exemple, elles peuvent provenir de capteurs ou de transactions de vente. Les données en continu continuent à être générées jour après jour, année après année, sans fin définie. Les algorithmes qui dépendent d'une fin définie ne fonctionneront pas avec des données en continu. Un exemple est la moyenne simple. Vous additionnez toutes les valeurs et divisez par le nombre total de valeurs. Cela fonctionne bien avec les données par lots, car vous finirez par avoir toutes les valeurs. Mais cela ne fonctionne pas avec les données en continu, car il peut ne pas y avoir de fin. Vous ne savez donc jamais quand diviser ni quelle valeur utiliser. Ce que Dataflow fait, c'est vous permettre de définir une période ou une fenêtre et de calculer la moyenne dans cette fenêtre. C'est un exemple de la façon dont les deux types de données peuvent être traités avec le même bloc de code.

Le filtrage et le regroupement sont également pris en charge.

De nombreuses charges de travail Hadoop peuvent être exécutées plus facilement et sont plus faciles à entretenir avec Dataflow. Cependant, les PCollections et les RDD ne sont pas identiques. Par conséquent, le code existant doit être repensé et adapté pour s'exécuter dans le pipeline Dataflow. Cela peut être une considération, car cela peut ajouter du temps et des coûts à un projet.

![](Aspose.Words.26c0f64e-6eda-41da-9774-5d9b364446b8.034.png)

Vos données dans TensorFlow sont représentées sous forme de tenseurs.

D'où vient le nom Tensorflow ? Eh bien, le "flow" fait référence à un pipeline, tout comme nous l'avons discuté dans Dataflow. Cependant, l'objet de données dans Tensorflow n'est pas une PCollection, mais quelque chose appelé un Tensor. Un Tensor est un objet mathématique spécial qui unifie les scalaires, les vecteurs et les matrices. Tensor-zero est simplement une seule valeur, un scalaire. Tensor-one est un vecteur, ayant une direction et une magnitude. Tensor-two est une matrice. Tensor-three est une forme cubique. Les tenseurs sont très efficaces pour représenter certains types de fonctions mathématiques, tels que les coefficients dans une équation. Et Tensorflow rend possible le travail avec des objets de données Tensor de n'importe quelle dimension.

Tensorflow est le code open source que vous utilisez pour créer des modèles d'apprentissage automatique.

Un tensor est une abstraction puissante car elle permet de relier différents types de données. De plus, il existe des transformations dans l'algèbre des tenseurs qui s'appliquent à n'importe quelle dimension ou rang de tenseur. Cela rend donc la résolution de certains problèmes beaucoup plus facile.

## Conception de pipelines de données

La prochaine section du guide d'examen porte sur la conception de pipelines de données. Vous savez déjà comment les données sont représentées. Dans Dataproc avec Spark, il s'agit de RDDs (Resilient Distributed Datasets) et dans Dataflow, il s'agit d'un PCollection. Dans BigQuery, les données sont dans un ensemble de données (Dataset) sous forme de tables.

Et vous savez qu'un pipeline est une sorte de séquence d'actions ou d'opérations à effectuer sur la représentation des données. Cependant, chaque service gère un pipeline différemment.

![](Aspose.Words.26c0f64e-6eda-41da-9774-5d9b364446b8.035.png)

Dataproc est un service Hadoop géré. Il y a plusieurs choses que vous devriez savoir, notamment les logiciels standards de l'écosystème Hadoop et les composants de Hadoop. Cependant, les principales choses que vous devriez savoir sur Dataproc concernent sa différence d'utilisation par rapport à Hadoop standard. Si vous stockez vos données en dehors du cluster, en stockant les données de type HDFS dans Cloud Storage et les

données de type HBASE dans Cloud Bigtable, vous pouvez arrêter votre cluster lorsque vous ne traitez pas réellement une tâche. C'est très important. Quels sont les deux problèmes avec Hadoop ? Premièrement, essayer d'ajuster tous ses paramètres pour qu'il puisse s'exécuter efficacement avec différents types de tâches, et deuxièmement, essayer de justifier le coût de l'utilisation. Vous cherchez donc des utilisateurs pour augmenter votre utilisation. Et cela signifie ajuster le cluster. Et si vous parvenez à le rendre efficace, il est probablement temps de faire croître le cluster. Vous pouvez sortir de ce cycle avec Dataproc en stockant les données de manière externe, en démarrant un cluster et en l'exécutant pour un type de travail. Ensuite, arrêtez-le lorsque vous avez terminé.

Lorsque vous disposez d'un cluster Dataproc sans état, il ne faut généralement que 90 secondes environ pour que le cluster démarre et devienne actif.

Dataproc prend en charge Hadoop, Pig, Hive et Spark.

Un conseil pour l'examen : Spark est important car il effectue une partie de son traitement en pipeline en mémoire, plutôt que de copier depuis le disque. Pour certaines applications, cela rend Spark extrêmement rapide.

![](Aspose.Words.26c0f64e-6eda-41da-9774-5d9b364446b8.036.png)

Avec un pipeline SPARK, vous avez deux types d'opérations différents : les transformations et les actions. Spark construit son pipeline en utilisant une abstraction appelée "Graph Directed". Chaque transformation ajoute des nœuds supplémentaires au graphique. Cependant, Spark n'exécute pas le pipeline tant qu'il n'observe pas une action. En somme, Spark attend d'avoir toute l'histoire, c'est-à-dire toutes les informations. Cela permet à Spark de choisir la meilleure façon de distribuer le travail et d'exécuter le pipeline. Le processus d'attente des transformations et d'exécution des actions est appelé "Lazy Execution" (exécution différée).

Pour une transformation, l'entrée est un RDD (Resilient Distributed Dataset) et la sortie est également un RDD. Lorsque Spark rencontre une transformation, elle l'enregistre dans le graphique dirigé, puis elle attend.

Une action déclenche le traitement du pipeline par Spark. Le résultat est généralement un "format de résultat", tel qu'un fichier texte, plutôt qu'un RDD.

Les transformations et les actions sont des appels d'API qui font référence aux fonctions que vous souhaitez exécuter.

En Python, les fonctions anonymes, appelées fonctions lambda, sont couramment utilisées pour effectuer ces appels d'API. Elles constituent une manière autonome de faire une demande à Spark. Chacune d'entre elles est limitée à un seul objectif spécifique. Elles sont définies en ligne, ce qui rend la séquence du code plus facile à lire et à comprendre. Et parce que le code est utilisé en un seul endroit, la fonction n'a pas besoin d'un nom et n'encombre pas l'espace de noms.

Une approche intéressante et opposée, où le système essaie de traiter les données dès leur réception, est appelée "Eager Execution" (exécution immédiate). TensorFlow, par exemple, peut utiliser à la fois des approches "lazy" et "eager".

![](Aspose.Words.26c0f64e-6eda-41da-9774-5d9b364446b8.037.png)

Dataproc dispose de connecteurs vers toutes sortes de ressources Google Cloud. Vous pouvez lire à partir de sources Google Cloud et écrire vers des sources Google Cloud, et utiliser Dataproc comme le lien interconnectant.

Vous pouvez également exécuter des logiciels open source de l'écosystème Hadoop sur le cluster. Il serait judicieux de connaître au moins les logiciels Hadoop les plus populaires et de savoir si des services alternatifs existent dans le cloud. Par exemple, Kafka est un service de messagerie. Et l'alternative sur Google Cloud serait Pub/Sub. Savez-vous quelle est l'alternative sur Google Cloud à HBASE en open source ? Il s'agit de Cloud Bigtable. Et l'alternative à HDFS ? Cloud Storage.

L'installation et l'exécution de logiciels open source Hadoop sur le cluster Dataproc sont également disponibles.

![](Aspose.Words.26c0f64e-6eda-41da-9774-5d9b364446b8.038.png)

Utilisez des actions d'initialisation, qui sont des scripts d'initialisation, pour charger, installer et personnaliser des logiciels. Le cluster lui-même a des propriétés limitées que vous pouvez modifier. Mais si vous utilisez Dataproc comme suggéré, en démarrant un cluster pour chaque type de travail, vous n'aurez pas besoin de modifier les propriétés de la même manière que vous le feriez avec Hadoop dans un centre de données.

Voici un conseil sur la modification du cluster Dataproc. Si vous avez besoin de modifier le cluster, réfléchissez à la solution de traitement des données la plus adaptée. Il existe de nombreux services disponibles sur Google Cloud, il se peut que vous puissiez utiliser un service plutôt que d'héberger votre propre solution sur le cluster.

Si vous migrez Hadoop d'un centre de données vers Dataproc, vous avez peut-être déjà des paramètres Hadoop personnalisés que vous souhaitez appliquer au cluster. Vous voudrez peut-être personnaliser certaines configurations du cluster afin qu'elles fonctionnent de manière similaire. Cela est pris en charge de manière limitée par les propriétés du cluster. La sécurité dans Dataproc est contrôlée par l'accès au cluster en tant que ressource.

![](Aspose.Words.26c0f64e-6eda-41da-9774-5d9b364446b8.039.png)

Voici quelques informations que vous devriez connaître à propos de Dataflow. Vous pouvez écrire du code de pipeline en Java ou en Python. Vous pouvez utiliser l'API open source Apache Beam pour définir le pipeline et le soumettre à Dataflow. Ensuite, Dataflow fournit le framework d'exécution. Les tâches parallèles sont automatiquement mises à l'échelle par le framework. Et le même code permet à la fois le traitement en continu en temps réel et le traitement par lots. Un avantage important de Dataflow est que vous pouvez obtenir des données en entrée à partir de nombreuses sources et écrire les résultats dans de nombreuses destinations, mais le code du pipeline reste le même. Dataflow prend en charge les entrées secondaires, où vous pouvez prendre des données, les transformer d'une manière, puis les transformer d'une autre manière en parallèle, de sorte que les deux puissent être utilisées ensemble dans le même pipeline. La sécurité de Dataflow est basée sur l'attribution de rôles qui limitent l'accès aux ressources de Dataflow. Ainsi, votre conseil pour l'examen est le suivant : "Pour les utilisateurs de Dataflow, utilisez des rôles pour limiter l'accès uniquement aux ressources de Dataflow, et pas seulement au projet."

![](Aspose.Words.26c0f64e-6eda-41da-9774-5d9b364446b8.040.png)

Le pipeline Dataflow n'apparaît pas seulement sous forme de code, mais il est également affiché dans la console Cloud sous la forme d'un diagramme. Les pipelines permettent de visualiser la progression d'une solution de traitement des données et l'organisation des étapes, ce qui les rend beaucoup plus faciles à maintenir que d'autres solutions de code. Chaque étape du pipeline effectue des opérations de filtrage, regroupement, transformation, comparaison, jointure, etc.

Les transformations peuvent être effectuées en parallèle.

![](Aspose.Words.26c0f64e-6eda-41da-9774-5d9b364446b8.041.png)

Voici quelques-unes des opérations Dataflow les plus couramment utilisées. Savez-vous quelles opérations sont potentiellement gourmandes en termes de puissance de calcul ? GroupByKey, par exemple, pourrait consommer des ressources sur des volumes importants de données. C'est l'une des raisons pour lesquelles vous voudriez tester votre pipeline plusieurs fois sur des données d'échantillon afin de vous assurer de sa capacité à s'adapter à l'échelle avant de l'exécuter en production.

Astuce pour l'examen : Un pipeline est une façon plus maintenable d'organiser le code de traitement des données que, par exemple, une application s'exécutant sur une instance.

![](Aspose.Words.26c0f64e-6eda-41da-9774-5d9b364446b8.042.png)

Avez-vous besoin de séparer les développeurs de pipelines Dataflow des utilisateurs consommateurs de Dataflow, des utilisateurs des pipelines ? Les modèles créent la seule étape d'indirection qui permet aux deux catégories d'utilisateurs d'avoir un accès différent. Les modèles de Dataflow permettent un nouveau flux de travail de développement et d'exécution. Les modèles aident à séparer les activités de développement et les développeurs des activités d'exécution et des utilisateurs. L'environnement utilisateur n'a

plus de dépendances vis-à-vis de l'environnement de développement. Le besoin de recompilation pour exécuter un travail est limité. La nouvelle approche facilite la planification des travaux par lots et ouvre plus de possibilités aux utilisateurs pour soumettre des travaux, ainsi que davantage d'opportunités d'automatisation.

Votre conseil pour l'examen est que les modèles Dataflow ouvrent de nouvelles options de séparation des travaux, ce qui signifie une meilleure sécurité et une meilleure responsabilité des ressources.

![](Aspose.Words.26c0f64e-6eda-41da-9774-5d9b364446b8.043.png)

BigQuery est composé de deux services. Un service frontal qui effectue l'analyse et un service arrière qui effectue le stockage. Il offre une analyse quasi temps réel de vastes ensembles de données. Le stockage des données est durable et peu coûteux. De plus, vous pouvez connecter et travailler avec différents ensembles de données pour obtenir de nouvelles informations et une valeur commerciale. BigQuery utilise le langage SQL pour les requêtes, ce qui le rend immédiatement utilisable par de nombreux analystes de données. BigQuery est rapide. Mais à quelle vitesse exactement ? Eh bien, si vous l'utilisez avec des données structurées pour l'analyse, cela peut prendre quelques secondes.

BigQuery se connecte à de nombreux services pour une ingestion et une sortie flexibles. De plus, il prend en charge les champs imbriqués et répétés (pour une efficacité accrue) ainsi que les fonctions définies par l'utilisateur pour l'extensibilité.

![](Aspose.Words.26c0f64e-6eda-41da-9774-5d9b364446b8.044.png)

Voici un conseil de conception majeur. Séparer le calcul et le traitement du stockage et de la base de données permet des opérations sans serveur.

BigQuery possède sa propre interface d'analyse/requête SQL, disponible dans la console et en ligne de commande avec bq. C'est simplement un moteur de requête.

La partie entrepôt de données en arrière-plan de BigQuery stocke les données dans des tables.

Mais BigQuery possède également un connecteur vers Cloud Storage. Celui-ci est couramment utilisé pour travailler directement avec des fichiers CSV.

BigQuery dispose également d'un connecteur vers Cloud Bigtable.

Si vous avez besoin de plus de fonctionnalités qu'un moteur de requête, envisagez Dataproc ou Dataflow.

Ce qui rend tout cela possible, c'est le réseau Cloud avec des vitesses de pétabits. Cela signifie que le stockage des données dans un service comme Cloud Storage peut être presque aussi rapide, voire plus rapide, que le stockage des données localement où elles seront traitées. En d'autres termes, le réseau renverse le concept de Hadoop et HDFS. Il est plus efficace, une fois de plus, de stocker les données séparément des ressources de traitement.

![](Aspose.Words.26c0f64e-6eda-41da-9774-5d9b364446b8.045.png)

Nous commençons maintenant à explorer comment toutes ces parties de la plateforme s'emboîtent pour créer des solutions vraiment flexibles et robustes.

Dataproc peut utiliser Cloud Storage à la place de HDFS pour les données persistantes. Si vous utilisez Cloud Storage, vous pouvez (A) arrêter le cluster lorsqu'il ne traite pas réellement les données, et (B) démarrer un cluster par tâche ou par catégorie de travail, de sorte que vous n'ayez pas à ajuster le cluster pour prendre en compte différents types de tâches.

Cloud Bigtable est un remplacement plug-and-play pour HBASE, une fois de plus en séparant l'état du cluster afin que le cluster puisse être arrêté lorsqu'il n'est pas utilisé et démarré pour exécuter un type spécifique de tâche.

![](Aspose.Words.26c0f64e-6eda-41da-9774-5d9b364446b8.046.png)

Dataproc et Dataflow peuvent produire des fichiers distincts au format CSV dans Cloud Storage. En d'autres termes, vous pouvez avoir un ensemble distribué de nœuds ou de serveurs traitant les données en parallèle et enregistrant les résultats dans des petits fichiers séparés. C'est une manière simple d'accumuler des résultats distribués pour les regrouper ultérieurement.

- Accédez à n'importe quel service de stockage depuis n'importe quel service de traitement de données.
- Dataflow est une excellente solution ETL (Extract, Transform, Load) pour BigQuery.
- Utilisez Dataflow pour agréger les données afin de les utiliser dans des requêtes courantes.

## Conception de l'infrastructure de traitement des données

Maintenant que vous disposez de toutes les pièces, commençons à examiner comment les assembler pour créer une infrastructure de traitement des données.

Il existe quelques ensembles courants de services et de technologies. Vous les verrez utilisés à plusieurs reprises dans différents contextes.

![](Aspose.Words.26c0f64e-6eda-41da-9774-5d9b364446b8.047.png)

Voici un exemple montrant les nombreuses solutions d'ingestion manuelle disponibles.

Vous pouvez utiliser l'outil en ligne de commande gsutil pour charger des fichiers dans Cloud Storage. Mais si vous souhaitez charger des données dans BigQuery, vous devez être capable d'identifier la structure.

L'outil en ligne de commande BigQuery, bq, est utile pour télécharger de grands fichiers de données et pour planifier des téléchargements de fichiers de données. Vous pouvez utiliser la commande pour créer des tables, définir des schémas, charger des données et exécuter des requêtes. La commande bq est disponible sur une instance Compute Engine, dans Cloud Shell, ou vous pouvez l'installer sur n'importe quelle machine cliente dans le cadre du kit de développement logiciel Google Cloud ou du Cloud SDK.

![](Aspose.Words.26c0f64e-6eda-41da-9774-5d9b364446b8.048.png)

Vous pouvez charger des données dans BigQuery depuis la Console Cloud.

Vous pouvez diffuser en continu des données à l'aide de Dataflow, depuis Cloud Logging, ou vous pouvez effectuer des appels POST à partir d'un programme.

Et il est très pratique que BigQuery puisse détecter automatiquement les fichiers au format CSV et JSON.

![](Aspose.Words.26c0f64e-6eda-41da-9774-5d9b364446b8.049.png)

Un autre conseil ; pensez aux données en termes des trois "V" -- Volume, Vitesse, Variété. Combien, à quelle fréquence et à quelle cohérence ?

Cela vous guidera vers la meilleure approche pour l'ingestion des données. En résumé, utilisez gsutil pour le téléchargement de fichiers. Utilisez le service de transfert de stockage lorsque les données se trouvent dans un autre emplacement, tel qu'un autre cloud. Et utilisez l'Appliance de transfert lorsque les données sont trop volumineuses pour être transférées électroniquement.

![](Aspose.Words.26c0f64e-6eda-41da-9774-5d9b364446b8.050.png)

Le courtier de messages Pub/Sub permet des solutions d'ingestion complètes. Il offre un couplage lâche entre les systèmes et des connexions de longue durée entre les systèmes. Astuce pour l'examen : Vous devez savoir combien de temps Pub/Sub conserve les messages, jusqu'à sept jours. Il y a plus de détails sur Pub/Sub que vous devriez connaître. Donc, si vous n'êtes pas familier, vous voudrez peut-être consulter la documentation.

![](Aspose.Words.26c0f64e-6eda-41da-9774-5d9b364446b8.051.png)

Pub/Sub relie les applications et les services grâce à une infrastructure de messagerie. Pub/Sub simplifie la distribution d'événements en remplaçant les connexions synchrones point à point par un bus asynchrone unique et hautement disponible. Vous pouvez éviter la surprovisionnement pour les pics de trafic avec Pub/Sub.

Si vous utilisez Pub/Sub avec Dataflow, vous pouvez obtenir un traitement exactement une fois et ordonné. À quelques exceptions près, Pub/Sub délivre chaque message publié au moins une fois pour chaque abonnement, et Dataflow gère la déduplication, l'ordonnancement et la fenêtre de traitement.

La séparation des tâches permet une solution scalable qui surpasse les goulots d'étranglement des systèmes de messagerie concurrents.

![](Aspose.Words.26c0f64e-6eda-41da-9774-5d9b364446b8.052.png)

Voici le modèle que vous verrez souvent dans le contexte de GCP :

Pub/Sub pour l'ingestion des données. Dataflow pour le traitement et l'ETL des données. Et BigQuery pour l'analyse interactive.

Conseil d'examen : soyez capable de reconnaître ce modèle dans des scénarios donnés.

![](Aspose.Words.26c0f64e-6eda-41da-9774-5d9b364446b8.053.png)

Cette architecture de référence pour les jeux mobiles illustre le schéma en action.

Les jeux mobiles populaires peuvent attirer des millions de joueurs et générer des téraoctets de données liées au jeu en peu de temps. Cela crée une pression sur l'infrastructure de traitement des données, qui doit fournir des informations exploitables en temps opportun de manière rentable.
