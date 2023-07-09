Construction d'un datalake

Nous commencerons par revoir ce qu'est un data lake, et discuterons des options de stockage de données ainsi que des options d'extraction, de transformation et de chargement de vos données dans Google Cloud. Ensuite, nous approfondirons pourquoi Google Cloud Storage est un choix populaire pour servir de Data Lake. La sécurisation de votre data lake fonctionnant sur le stockage cloud est d'une importance capitale. Nous discuterons des principales fonctionnalités de sécurité que vous devez connaître en tant qu'ingénieur de données pour contrôler l'accès à vos objets. Cloud Storage n'est pas votre seul choix en matière de stockage de données dans un data lake sur Google Cloud, nous examinerons donc le stockage de différents types de données. Enfin, nous examinerons Cloud SQL, le choix par défaut pour les charges de travail OLTP (traitement en ligne des transactions) sur Google Cloud. Vous réaliserez également un laboratoire pratique où vous pratiquerez la création d'un data lake pour vos données relationnelles avec Cloud SQL.

Introduction auxDatalakes

![](Aspose.Words.a31beb3f-fb98-45c7-be4a-3b0e8a4b1f30.001.png)

Qu'est-ce qu'un data lake après tout ?

C'est un terme assez large, mais il décrit généralement un endroit où vous pouvez stocker de manière sécurisée différents types de données de toutes tailles, pour le traitement et l'analyse.

Les data lakes sont généralement utilisés pour alimenter des analyses de données, des travaux de science des données et d'apprentissage automatique (ML), ou des pipelines de données en mode batch ou en continu.

Les data lakes acceptent tous les types de données.

Enfin, les data lakes sont portables, qu'ils soient sur site ou dans le cloud.

![](Aspose.Words.a31beb3f-fb98-45c7-be4a-3b0e8a4b1f30.002.png)

Voici où les Data Lakes s'intègrent dans l'écosystème global de l'ingénierie des données pour votre équipe dans le contexte de GCP.

- Vous devez commencer avec un ou plusieurs systèmes d'origine qui sont la source de toutes vos données, ce sont vos sources de données.
- En tant qu'ingénieur de données, vous devez ensuite construire des moyens fiables de récupérer et de stocker ces données, ce sont vos réceptacles de données (data sinks).
  - La première ligne de défense dans un environnement de données d'entreprise est votre Data Lake. Encore une fois, c'est le centre où vous pouvez obtenir n'importe quelle donnée, quelle que soit son volume, sa variété de formats et sa vélocité. Nous aborderons les considérations clés et les options pour la construction d'un Data Lake dans ce module.
  - Une fois que vos données sont extraites des systèmes sources et qu'elles sont à l'intérieur de votre environnement, un nettoyage et un traitement considérables sont généralement nécessaires pour transformer ces données en un format utile pour l'entreprise. Elles finiront ensuite dans votre Data Warehouse. C'est notre objectif pour le prochain module.
- Qui effectue réellement le nettoyage et le traitement des données ? Ce sont vos pipelines de données ! Ils sont responsables des transformations et du traitement de vos données à grande échelle, et ils donnent vie à tout votre système avec des données nouvellement traitées et fraîches pour l'analyse.
- Une couche d'abstraction supplémentaire au-dessus de vos pipelines est ce que j'appellerai votre flux de travail complet. Vous devrez souvent coordonner les efforts entre de nombreux composants différents à une cadence régulière ou déclenchée par un événement. Alors que votre pipeline de données peut traiter les données de votre Data Lake vers votre Data Warehouse, votre flux de travail d'orchestration peut être responsable de déclencher ce pipeline de données en premier lieu lorsqu'il constate la disponibilité de nouvelles données brutes à partir d'une source.

\-

<https://cloud.google.com/solutions/data-lake/>

![](Aspose.Words.a31beb3f-fb98-45c7-be4a-3b0e8a4b1f30.003.png)

Avant d'aborder les produits cloud qui correspondent à chaque rôle, je souhaite vous présenter une analogie qui aidera à dissiper les ambiguïtés liées à ces composants.

Imaginez-vous dans le monde du génie civil pendant un instant. On vous a confié la tâche de construire un incroyable gratte-ciel en plein centre-ville. Avant de commencer les travaux, vous devez vous assurer d'avoir tous les matériaux bruts nécessaires pour atteindre votre objectif final. Bien sûr, certains matériaux peuvent être obtenus ultérieurement dans le projet, mais pour simplifier notre exemple, supposons que vous les ayez tous dès le départ.

Le fait de transporter l'acier, le béton, l'eau, le bois, le sable et le verre depuis leur source jusqu'au chantier est analogue à l'arrivée des données en provenance des systèmes sources et à leur intégration dans votre lac de données.

Super ! Maintenant, vous disposez de tous ces matériaux bruts, mais vous ne pouvez pas les utiliser tels quels pour construire votre bâtiment. Vous devez découper le bois et le métal, mesurer et préparer le verre afin qu'ils conviennent à la construction. Le résultat final, le verre découpé, le métal façonné, constitue les données formatées stockées dans votre entrepôt de données. Ces données sont prêtes à être utilisées pour ajouter directement de la valeur à votre entreprise, ce qui, dans notre analogie, équivaut à la construction du bâtiment. Comment avez-vous transformé ces matériaux bruts en pièces utilisables ? Sur un chantier de construction, c'est le travailleur qui s'en charge.

Comme vous le verrez plus tard lorsque nous aborderons les pipelines de données, l'unité individuelle en coulisses est littéralement appelée un travailleur (qui est simplement une machine virtuelle) et il prend une petite partie des données et la transforme pour vous.

Et que dire du bâtiment lui-même ? Il représente l'objectif final ou les objectifs que vous souhaitez atteindre avec ce projet d'ingénierie.

Dans le domaine de l'ingénierie des données, ce nouveau bâtiment étincelant pourrait être un nouvel aperçu analytique qui n'était pas possible auparavant, ou un modèle d'apprentissage automatique, ou tout autre résultat que vous souhaitez obtenir maintenant que vous disposez des données nettoyées.

Le dernier élément de l'analogie est la couche d'orchestration. Sur un chantier de construction, vous avez un gestionnaire ou un superviseur qui indique quand les travaux doivent être effectués et les éventuelles dépendances. Il peut dire : "Une fois que le nouveau métal est arrivé, envoyez-le dans cette zone du chantier pour le découper et le façonner, puis informez cette autre équipe qu'il est prêt pour la construction". Dans le domaine de l'ingénierie des données, cela correspond à votre couche d'orchestration ou flux de travail global.

Vous pourriez dire : "Chaque fois qu'un nouveau fichier de données CSV est déposé dans ce compartiment de stockage cloud, je veux que vous le transmettiez automatiquement à notre pipeline de données pour le traitement. ET, une fois le traitement terminé, je veux que vous, le pipeline, le diffusiez dans l'entrepôt de données. ET, une fois qu'il est dans l'entrepôt de données, je notifierai le modèle d'apprentissage automatique que de nouvelles données d'entraînement nettoyées sont disponibles pour l'entraînement, et je lui donnerai l'ordre de commencer à entraîner une nouvelle version du modèle."

Pouvez-vous visualiser la séquence d'actions qui se met en place ? Que se passe-t-il en cas d'échec d'une étape ? Que se passe-t-il si vous souhaitez exécuter tout cela chaque jour ? Vous commencez à comprendre la nécessité d'un orchestrateur, qui, dans notre solution, sera Apache Airflow exécuté sur Cloud Composer ultérieurement.

<https://cloud.google.com/solutions/data-lake/>

![](Aspose.Words.a31beb3f-fb98-45c7-be4a-3b0e8a4b1f30.004.png)

Ramenons un exemple d'architecture de solution que vous avez déjà vu dans le cours. Le lac de données est représenté ici par des compartiments Cloud Storage au centre du schéma. C'est l'emplacement centralisé de vos données brutes, qui est durable et hautement disponible. Dans cet exemple, notre lac de données est un Cloud Storage, mais cela ne signifie pas que le Cloud Storage est votre seule option pour les lacs de données. Le

Cloud Storage est l'une des bonnes options pour servir de lac de données. Dans d'autres exemples que nous examinerons, BigQuery peut être à la fois votre lac de données et votre entrepôt de données, et vous n'utilisez pas du tout de compartiments Cloud Storage. C'est pourquoi il est si important de comprendre ce que vous voulez faire en premier lieu, puis de trouver les solutions qui répondent le mieux à vos besoins. Quels que soient les outils et technologies cloud que vous utilisez, votre lac de données sert généralement de lieu centralisé unique pour toutes vos données brutes. Pensez-y comme une zone de préparation durable. Les données peuvent ensuite être envoyées dans de nombreux autres endroits, tels qu'un pipeline de transformation qui les nettoie, les déplace vers l'entrepôt, puis elles sont lues par un modèle d'apprentissage automatique. MAIS tout commence par l'importation de ces données dans votre lac en premier lieu.

Faisons un bref aperçu de certains des principaux produits Big Data de Google Cloud que vous devez connaître en tant qu'ingénieur de données et que vous pratiquerez ultérieurement dans vos laboratoires.

![](Aspose.Words.a31beb3f-fb98-45c7-be4a-3b0e8a4b1f30.005.png)

Voici une liste de produits de données volumineuses (big data) et de l'apprentissage automatique (ML), organisée selon l'endroit où vous les trouveriez probablement dans une charge de travail typique de traitement des données, de l'enregistrement des données à gauche à l'ingestion dans vos outils natifs du cloud pour l'analyse, l'entraînement de modèles d'apprentissage automatique et la fourniture d'informations.

![](Aspose.Words.a31beb3f-fb98-45c7-be4a-3b0e8a4b1f30.006.png)

Dans ce module Data Lake, nous nous concentrerons sur deux des produits de stockage fondamentaux qui constitueront votre Data Lake : Cloud Storage et Cloud SQL pour vos données relationnelles. Plus tard dans le cours, vous travaillerez également avec Cloud Bigtable lorsque vous utiliserez des pipelines de streaming à haut débit.

Vous pourriez être surpris de ne pas voir BigQuery dans la colonne de stockage. En général, BigQuery est utilisé comme entrepôt de données - quelle est donc la différence fondamentale entre un Data Lake et un entrepôt de données ?

![](Aspose.Words.a31beb3f-fb98-45c7-be4a-3b0e8a4b1f30.007.png)

Un lac de données est essentiellement l'endroit où vous capturez tous les aspects de vos opérations commerciales. Étant donné que vous souhaitez capturer chaque aspect, vous avez tendance à stocker les données dans leur format brut naturel, c'est-à-dire le format dans lequel elles sont produites par votre application. Ainsi, vous pouvez avoir un fichier journal et les fichiers journaux sont stockés tels quels... dans un lac de données. Vous pouvez essentiellement stocker tout ce que vous souhaitez et, étant donné que vous voulez tout stocker... vous avez tendance à stocker ces éléments sous forme de blocs d'objets ou de fichiers.

L'avantage de la flexibilité du data lake en tant que point de collecte central est également son problème. Avec un data lake, le format des données est largement déterminé par l'application qui écrit les données, et il est dans le format dans lequel elles se trouvent. L'avantage d'un data lake est que chaque fois que l'application est mise à niveau, elle peut commencer à écrire immédiatement les nouvelles données, car il s'agit simplement d'une capture des données brutes existantes. Alors, comment pouvez-vous prendre cette quantité importante et flexible de données brutes et en faire quelque chose d'utile ? Accédez au Data Warehouse.

D'un autre côté, un entrepôt de données est beaucoup plus réfléchi. Vous pourriez charger les données dans un entrepôt de données uniquement après avoir défini un schéma et identifié le cas d'utilisation.

Vous pourriez prendre les données brutes existantes dans un lac de données, les transformer, les organiser, les traiter, les nettoyer, puis les stocker dans un entrepôt de données.

Pourquoi utilisez-vous l'entrepôt de données ? Peut-être parce que les données dans l'entrepôt de données sont utilisées pour générer des graphiques, des rapports, des tableaux de bord, et ainsi de suite.

L'idée est que, parce que le schéma est cohérent et partagé entre toutes les applications, quelqu'un peut ensuite analyser les données et en tirer des informations beaucoup plus rapidement.

Ainsi, un entrepôt de données a tendance à contenir des données structurées et semi-structurées qui sont organisées et placées dans un format qui facilite les requêtes et l'analyse.

Options de stockage de données et d'ETL sur Google Cloud

![](Aspose.Words.a31beb3f-fb98-45c7-be4a-3b0e8a4b1f30.008.png)

Vos options sur Google Cloud pour la création d'un Data Lake sont vos solutions de stockage que vous avez vues précédemment.

- Vous disposez de Cloud Storage comme solution polyvalente.
- Cloud SQL et Cloud Spanner pour les données relationnelles.
- Et Firestore et Cloud Bigtable pour les données NoSQL.

Le choix de l'option ou des options à utiliser dépend fortement de votre cas d'utilisation et de ce que vous essayez de construire. Dans cette leçon, nous nous concentrerons sur Cloud Storage et Cloud SQL, mais vous verrez les options NoSQL telles que Cloud Bigtable plus tard dans le cours lorsque nous aborderons le traitement en continu à très haut débit.

Alors, comment décider quelle voie choisir pour votre lac ?

![](Aspose.Words.a31beb3f-fb98-45c7-be4a-3b0e8a4b1f30.009.png)

- La destination finale de vos données sur le cloud et les chemins empruntés pour transférer vos données vers le cloud dépendent de l'endroit où se trouvent actuellement vos données.
- La taille de vos données, c'est-à-dire le volume, est l'un des trois V du Big Data.
- Et finalement, où doivent-elles aller ? Dans les diagrammes d'architecture, le point d'arrivée des données est appelé un puits de données. Un puits de données courant après un lac de données est votre entrepôt de données.
- N'oubliez pas un aspect essentiel à prendre en compte est la quantité de traitement et de transformation nécessaire pour que vos données soient utiles à votre entreprise.

Vous pourriez vous demander : est-ce que je termine le traitement avant de charger les données dans mon lac de données ou après, avant de les envoyer ailleurs ? Parlons de ces schémas.

La méthode que vous utilisez pour charger les données dans le cloud dépend de la quantité de transformation nécessaire entre les données brutes que vous avez et le format final souhaité. Dans cette leçon, nous examinerons certaines considérations pour le format final souhaité.

![](Aspose.Words.a31beb3f-fb98-45c7-be4a-3b0e8a4b1f30.010.png)

EL

Le cas le plus simple pourrait être que vous ayez des données dans un format directement utilisable par le produit cloud dans lequel vous souhaitez les stocker.

Prenons par exemple le cas où vous avez vos données au format Avro et que vous souhaitez les stocker dans BigQuery car votre cas d'utilisation correspond à ce que BigQuery fait bien. Dans ce cas, vous effectuez simplement une extraction et un chargement (E-L). BigQuery chargera directement les fichiers Avro. E-L fait référence au moment où les données peuvent être importées "telles quelles" dans un système. Cela peut inclure l'importation de données à partir d'une base de données où la source et la cible ont le même schéma.

L'une des fonctionnalités qui rendent BigQuery unique est que, comme vous l'avez vu précédemment avec l'exemple de requête fédérée, vous pouvez même ne pas charger les données dans BigQuery et toujours effectuer des requêtes dessus. Les fichiers Avro, ORC et Parquet sont tous désormais pris en charge pour les requêtes fédérées.

ELT

Le T dans E-L-T signifie "TRANSFORM" (TRANSFORMATION).

C'est lorsque les données chargées dans le produit cloud ne sont pas dans le format final souhaité. Vous souhaiterez peut-être les nettoyer ou les transformer de manière à corriger les données, par exemple. En d'autres termes, vous extrayez les données de votre système local, les chargez dans le produit cloud, puis effectuez la transformation. Cela s'appelle extraction, chargement et transformation, ou E-L-T. Vous avez tendance à faire cela lorsque la quantité de transformation nécessaire n'est pas très élevée et que la transformation ne réduit pas considérablement la quantité de données que vous avez. L'E-L-T permet de charger les données brutes directement dans la cible et de les transformer là-bas. Par exemple, dans BigQuery, vous pouvez utiliser SQL pour transformer les données et écrire une nouvelle table.

ETL

La troisième option est l'extraction, la transformation et le chargement, ou E-T-L. C'est le cas lorsque vous souhaitez extraire les données, leur appliquer plusieurs traitements, puis les charger dans le produit cloud.

C'est généralement ce que vous choisissez lorsque cette transformation est essentielle ou si cette transformation réduit considérablement la taille des données. En transformant les données avant de les charger dans le cloud, vous pourrez peut-être réduire considérablement la bande passante réseau dont vous avez besoin. Si vous avez vos données dans un format binaire propriétaire et que vous devez les convertir avant de les charger, vous aurez également besoin de l'E-T-L.

L'E-T-L est un processus d'intégration de données dans lequel la transformation a lieu dans un service intermédiaire avant d'être chargée dans la cible. Par exemple, les données peuvent être transformées dans un pipeline de données tel que Dataflow avant d'être chargées dans BigQuery.

Créez un Data Lake en utilisant le stockage Cloud.

Google Cloud Storage est le service de stockage essentiel pour travailler avec des données, notamment des données non structurées, dans le cloud. Plongeons plus en profondeur pour comprendre pourquoi Google Cloud Storage est un choix populaire pour servir de lac de données.

![](Aspose.Words.a31beb3f-fb98-45c7-be4a-3b0e8a4b1f30.011.png)Les données stockées dans Cloud Storage persistent au-delà de la durée de vie des machines virtuelles ou des clusters (c'est-à-dire qu'elles sont persistantes). Elles sont également relativement peu coûteuses par rapport au coût de calcul. Par conséquent, par exemple, il peut être avantageux de mettre en cache les résultats des calculs précédents dans Cloud Storage. Si vous n'avez pas besoin qu'une application s'exécute en permanence, il peut être utile de sauvegarder l'état de votre application dans Cloud Storage et d'éteindre la machine sur laquelle elle s'exécute lorsque vous n'en avez pas besoin.

Cloud Storage est un service de stockage d'objets, il stocke simplement des objets binaires sans se soucier des données contenues dans ces objets. Cependant, dans une certaine mesure, il offre également une compatibilité avec les systèmes de fichiers et permet de faire en sorte que les objets ressemblent à des fichiers et fonctionnent comme tels, vous pouvez donc copier des fichiers dedans et en sortir.

- Les données stockées dans Cloud Storage restent essentiellement là pour toujours (en d'autres termes, elles sont durables), mais elles sont instantanément disponibles
  - elles sont fortement cohérentes.
- Vous pouvez partager des données à l'échelle mondiale, mais elles sont chiffrées et entièrement contrôlées et privées si vous le souhaitez.
- C'est un service mondial et vous pouvez accéder aux données depuis n'importe où (en d'autres termes, il offre une disponibilité mondiale). Mais les données peuvent également être conservées dans un seul emplacement géographique si vous en avez besoin.
- Les données sont servies avec une latence modérée et un débit élevé.

En tant qu'ingénieur de données, il est important de comprendre comment Cloud Storage parvient à concilier ces qualités apparemment contradictoires, ainsi que quand et comment les utiliser dans vos solutions.

![](Aspose.Words.a31beb3f-fb98-45c7-be4a-3b0e8a4b1f30.012.png)Beaucoup des propriétés incroyables de Cloud Storage sont liées au fait qu'il s'agit d'un magasin d'objets. D'autres fonctionnalités sont construites sur cette base.

Les deux principales entités dans Cloud Storage sont les buckets et les objets. Les buckets sont des conteneurs pour les objets. Les objets existent à l'intérieur des buckets et non à part. Ainsi, les buckets sont des conteneurs pour les données.

- Les buckets sont identifiés dans un seul espace de noms mondial unique. Cela signifie que, une fois qu'un nom est donné à un bucket, il ne peut pas être utilisé par quelqu'un d'autre tant que ce bucket n'est pas supprimé et que le nom est libéré. Avoir un espace de noms mondial pour les buckets simplifie la localisation d'un bucket spécifique.
- Lorsqu'un bucket est créé, il est associé à une région particulière ou à plusieurs régions. Choisir une région proche des données à traiter réduira la latence, et si vous traitez les données à l'aide de services cloud dans la région, vous économiserez sur les frais de sortie du réseau.
- Lorsqu'un objet est stocké, Cloud Storage le réplique. Il surveille les répliques et, si l'une d'entre elles est perdue ou corrompue, la remplace par une copie fraîche. C'est ainsi que Cloud Storage obtient une durabilité élevée. Pour un bucket multi-régions, les objets sont répliqués entre les régions, et pour un bucket mono-région, les objets sont répliqués entre les zones. Dans tous les cas, lorsque l'objet est récupéré, il est servi à partir de la réplique la plus proche du demandeur. C'est ainsi que la latence est réduite. Plusieurs demandeurs peuvent récupérer les objets en même temps à partir de répliques différentes. C'est ainsi que le débit élevé est atteint.
- Enfin, les objets sont stockés avec des métadonnées. Les métadonnées sont des informations sur l'objet. Des fonctionnalités supplémentaires de Cloud Storage utilisent les métadonnées à des fins telles que le contrôle d'accès, la compression, le chiffrement et la gestion du cycle de vie. Par exemple, Cloud Storage sait quand un objet a été stocké, et il peut être configuré pour être automatiquement supprimé après une certaine période. Cette fonctionnalité utilise les métadonnées de l'objet pour déterminer quand supprimer l'objet.

![](Aspose.Words.a31beb3f-fb98-45c7-be4a-3b0e8a4b1f30.013.png)

Vous pouvez avoir différents besoins de stockage pour une multitude de cas d'utilisation. Cloud Storage propose différentes classes pour répondre à ces besoins, basées sur la fréquence d'accès aux données.

Stockage standard

- Le stockage standard est idéal pour les données auxquelles on accède fréquemment (également appelées données "chaudes") et/ou stockées pendant de courtes périodes.
- Lorsqu'il est utilisé dans une région, la co-localisation de vos ressources maximise les performances pour les calculs intensifs en données et peut réduire les frais de réseau.
- Lorsqu'il est utilisé dans une région double, vous obtenez toujours des performances optimisées lors de l'accès aux produits Google Cloud situés dans l'une des régions associées, mais vous bénéficiez également d'une disponibilité améliorée grâce au stockage des données dans des emplacements géographiquement distincts.
- Lorsqu'il est utilisé dans une multi-région, le stockage standard convient pour stocker des données qui sont consultées dans le monde entier, telles que la diffusion de contenu de site web, la diffusion de vidéos, l'exécution de charges de travail interactives ou la fourniture de données pour des applications mobiles et de jeux.

Stockage Nearline

- Le stockage Nearline est un service de stockage peu coûteux et hautement durable pour les données consultées rarement.
- Le stockage Nearline est un meilleur choix que le stockage standard dans les scénarios où une disponibilité légèrement plus faible, une durée de stockage minimale de 30 jours et des coûts d'accès aux données sont des compromis acceptables pour des coûts de stockage au repos réduits.
- Le stockage Nearline est idéal pour les données que vous prévoyez de lire ou de modifier en moyenne une fois par mois ou moins.
- Le stockage Nearline convient pour les sauvegardes de données, le contenu multimédia peu utilisé et l'archivage de données.

Stockage Coldline

- Le stockage Coldline est un service de stockage très peu coûteux et hautement durable pour les données consultées rarement.
- Le stockage Coldline est un meilleur choix que le stockage standard ou le stockage Nearline dans les scénarios où une disponibilité légèrement plus faible, une durée de stockage minimale de 90 jours et des coûts plus élevés pour l'accès aux données sont des compromis acceptables pour des coûts de stockage au repos réduits.
- Le stockage Coldline est idéal pour les données que vous prévoyez de lire ou de modifier au maximum une fois par trimestre.

Stockage Archive

- Le stockage Archive est le service de stockage le moins coûteux et hautement durable pour l'archivage de données, les sauvegardes en ligne et la reprise après sinistre.
- Le stockage Archive a des coûts plus élevés pour l'accès aux données et les opérations, ainsi qu'une durée de stockage minimale de 365 jours.
- Le stockage Archive est le meilleur choix pour les données auxquelles vous prévoyez d'accéder moins d'une fois par an. Par exemple, le stockage de données froides, telles que les données stockées pour des raisons légales ou réglementaires, et la reprise après sinistre.

Cloud Storage présente plusieurs caractéristiques uniques : une API unique, une latence d'accès aux données en millisecondes et une durabilité de onze 9s pour toutes les classes de stockage. Cloud Storage propose également une gestion du cycle de vie des objets, qui utilise des stratégies pour déplacer automatiquement les données vers des classes de stockage moins coûteuses à mesure qu'elles sont consultées moins fréquemment au fil du temps.

<https://cloud.google.com/storage/docs/storage-classes>

![](Aspose.Words.a31beb3f-fb98-45c7-be4a-3b0e8a4b1f30.014.png)

Cloud Storage utilise le nom du bucket et le nom de l'objet pour simuler un système de fichiers. Voici comment cela fonctionne :

- Le nom du bucket est le premier terme dans l'URI.
- Un slash est ajouté à la suite,
- Et ensuite il est concaténé avec le nom de l'objet. Le nom de l'objet permet d'inclure le caractère slash comme un caractère valide dans le nom.
- Le nom de l'objet très long avec des caractères de slash donne l'apparence d'un chemin de système de fichiers, même s'il s'agit en réalité d'un seul nom.

Dans l'exemple donné, le nom du bucket est "D-E-class".

Le nom de l'objet est "de/modules/02/script.sh". Les slashs ne sont que des caractères dans le nom.

Si ce chemin était dans un système de fichiers, il apparaîtrait comme un ensemble de répertoires imbriqués, commençant par "D-E-class".

Maintenant, pour tous les besoins pratiques, cela fonctionne comme un système de fichiers. Mais il y a quelques différences.

Par exemple, imaginez que vous vouliez déplacer tous les fichiers du répertoire 02 vers le répertoire 03 à l'intérieur du répertoire modules.

Dans un système de fichiers, vous auriez des structures de répertoires réelles et vous modifieriez simplement les métadonnées du système de fichiers pour que le déplacement soit entièrement atomique. Mais dans un magasin d'objets qui simule un système de fichiers, vous devriez rechercher tous les objets contenus dans le bucket pour trouver ceux dont le nom contient "02" à la bonne position. Ensuite, vous devriez modifier le nom de chaque objet et les renommer en utilisant "03". Cela produirait apparemment le même résultat : déplacer les fichiers entre les répertoires. Cependant, au lieu de travailler avec une douzaine de fichiers dans un répertoire, le système devrait rechercher parmi des milliers d'objets dans le bucket pour localiser ceux ayant les bons noms et les modifier. Les caractéristiques de performance sont donc différentes. Il peut prendre plus de temps pour déplacer une douzaine d'objets du répertoire 02 vers le répertoire 03 en fonction du nombre d'autres objets stockés dans le bucket. Pendant le déplacement, il y aura une incohérence de liste, avec certains fichiers dans l'ancien répertoire et d'autres dans le nouveau répertoire.

Une bonne pratique est d'éviter d'utiliser des informations sensibles comme partie des noms de bucket car les noms de bucket sont dans un espace de noms global. Les données dans les buckets peuvent être gardées privées si vous en avez besoin.

Cloud Storage peut être accédé en utilisant une méthode d'accès de fichier. Cela vous permet, par exemple, d'utiliser une commande de copie à partir d'un fichier local directement vers Cloud Storage.

Cloud Storage peut également être accédé via le web. Le site (https://storage.cloud.google.com) utilise TLS (HTTPS) pour transporter vos données, ce qui protège à la fois les informations d'identification et les données en transit.

![](Aspose.Words.a31beb3f-fb98-45c7-be4a-3b0e8a4b1f30.015.png)

Cloud Storage dispose de nombreuses fonctionnalités de gestion des objets. Par exemple, vous pouvez définir une politique de rétention sur tous les objets du bucket. Par exemple, les objets devraient expirer après 30 jours.

Vous pouvez également utiliser la versioning, de sorte que plusieurs versions d'un objet soient suivies et disponibles si nécessaire. Vous pouvez même configurer la gestion du cycle de vie pour déplacer automatiquement les objets qui n'ont pas été consultés depuis 30 jours vers Nearline, puis après 90 jours vers Coldline.

Stockage sécurisé dans le cloud

![](Aspose.Words.a31beb3f-fb98-45c7-be4a-3b0e8a4b1f30.016.png)

Cloud Storage implémente deux méthodes distinctes mais qui se chevauchent pour contrôler l'accès aux objets : la politique IAM (Identity and Access Management) et les listes de contrôle d'accès (ACL, Access Control Lists). IAM est standard dans l'ensemble de Google Cloud. Il est défini au niveau du bucket et applique des règles d'accès uniformes à tous les objets à l'intérieur d'un bucket. Les listes de contrôle d'accès peuvent être appliquées au niveau du bucket ou sur des objets individuels, offrant ainsi un contrôle d'accès plus précis.

Les contrôles IAM fonctionnent comme prévu. IAM fournit des rôles au niveau du projet et des rôles au niveau du bucket, y compris le rôle de lecteur de bucket (Bucket Reader), le rôle de rédacteur de bucket (Bucket Writer) et le rôle de propriétaire de bucket (Bucket Owner). La capacité de créer ou de modifier des listes de contrôle d'accès est un rôle de bucket IAM. La capacité de créer et de supprimer des buckets, ainsi que de définir des politiques IAM, relève d'un rôle au niveau du projet. Des rôles personnalisés sont également disponibles. Les rôles au niveau du projet de Visualiseur (Viewer), Rédacteur (Editor) et Propriétaire (Owner) font des utilisateurs des membres de groupes internes spéciaux qui leur donnent accès en tant que membres de rôles de bucket. Consultez la documentation en ligne pour plus de détails.

Lorsque vous créez un bucket, vous avez la possibilité de désactiver les listes de contrôle d'accès et d'utiliser uniquement IAM. Les listes de contrôle d'accès sont actuellement activées par défaut. Ce choix était autrefois immuable, mais maintenant vous pouvez désactiver les listes de contrôle d'accès même si elles étaient déjà en vigueur. Par exemple, vous pouvez accorder à bob@example.com l'accès en lecture au bucket via IAM, tout en lui donnant également l'accès en écriture à un fichier spécifique dans ce bucket via les listes de contrôle d'accès.

Vous pouvez également accorder de telles autorisations à des comptes de service associés à des applications individuelles.

![](Aspose.Words.a31beb3f-fb98-45c7-be4a-3b0e8a4b1f30.017.png)

Toutes les données dans Google Cloud sont chiffrées au repos et en transit. Il n'est pas possible de désactiver ce chiffrement.

GMEK

Le chiffrement est effectué par Google en utilisant des clés de chiffrement que nous gérons - les clés de chiffrement gérées par Google ou G-MEK.

Nous utilisons deux niveaux de chiffrement : premièrement, les données sont chiffrées à l'aide d'une clé de chiffrement des données. Ensuite, la clé de chiffrement des données elle-même est chiffrée à l'aide d'une clé de chiffrement des clés ou K-E-K.

Les K-E-K sont automatiquement tournées selon un calendrier et la K-E-K actuelle est stockée dans Cloud KMS, le service de gestion des clés Cloud. Vous n'avez rien à faire. Il s'agit d'un comportement automatique.

CMEK

Si vous souhaitez gérer vous-même la K-E-K, vous le pouvez. Au lieu que Google gère la clé de chiffrement, vous pouvez contrôler la création et l'existence de la K-E-K utilisée. Cela s'appelle les clés de chiffrement gérées par le client ou C-MEK.

CSEK

Vous pouvez éviter complètement Cloud KMS et fournir votre propre mécanisme de chiffrement et de rotation. Cela s'appelle les clés de chiffrement fournies par le client ou C-SEK.

Le choix de l'option de chiffrement des données dépend des exigences commerciales, juridiques et réglementaires. Veuillez consulter le conseiller juridique de votre entreprise.

![](Aspose.Words.a31beb3f-fb98-45c7-be4a-3b0e8a4b1f30.018.png)

La quatrième option de chiffrement est le chiffrement côté client. Le chiffrement côté client signifie simplement que vous avez chiffré les données avant de les télécharger et que vous devez les déchiffrer vous-même avant de les utiliser. Cloud Storage effectue toujours le chiffrement G-MEK, C-MEK ou C-SEK sur l'objet. Il n'a aucune connaissance de la couche de chiffrement supplémentaire que vous avez pu ajouter.

Cloud Storage prend en charge la journalisation de l'accès aux données, et ces journaux sont immuables. En plus des journaux d'audit Cloud et des journaux d'accès à Cloud Storage, il existe différentes restrictions et verrous que vous pouvez placer sur les données elles-mêmes.

À des fins d'audit, vous pouvez placer une restriction sur un objet, et toutes les opérations susceptibles de modifier ou de supprimer l'objet sont suspendues jusqu'à la levée de la restriction. Vous pouvez également verrouiller un compartiment, et aucune modification ou suppression ne peut avoir lieu tant que le verrou n'est pas levé.

Enfin, il y a la politique de conservation verrouillée dont nous avons déjà discuté. Et elle continue à rester en vigueur et à empêcher la suppression, que ce soit en cas de verrouillage de compartiment ou de restriction sur un objet. Le verrouillage des données est différent du chiffrement. Alors que le chiffrement empêche quelqu'un de comprendre les données, le verrouillage les empêche de les modifier.

Cloud Storage prend en charge toute une série de cas d'utilisation spéciaux. Par exemple, le codage décompressif...

- Par défaut, les données que vous téléchargez sont les mêmes données que vous obtenez de Cloud Storage. Cela inclut les archives gzip, qui sont généralement renvoyées sous forme d'archives gzip. Cependant, si vous étiquetez correctement un objet dans les métadonnées, vous pouvez amener Cloud Storage à décompresser le fichier pendant son transfert. Les avantages du fichier compressé plus petit sont un téléchargement plus rapide et des coûts de stockage inférieurs par rapport aux fichiers non compressés.
- Vous pouvez configurer un compartiment pour qu'il soit "payant pour l'accès par le demandeur". Normalement, si des données sont consultées à partir d'une région différente, vous devrez payer des frais de sortie réseau. Mais vous pouvez faire en sorte que le demandeur paie, de sorte que vous ne payez que le stockage des données.
- Vous pouvez créer une URL signée pour partager anonymement un objet dans Cloud Storage, et même faire en sorte que l'URL expire après une période de temps.
- Il est possible de télécharger un objet en morceaux et de créer un objet composite sans avoir à concaténer les morceaux après le téléchargement.

Il y a beaucoup de fonctionnalités utiles dans Cloud Storage, mais nous devons passer à autre chose !

Stocker tous types de données

![](Aspose.Words.a31beb3f-fb98-45c7-be4a-3b0e8a4b1f30.019.png)

Vous ne voulez pas utiliser Cloud Storage pour les charges de travail transactionnelles. Bien que la latence de Cloud Storage soit faible, elle n'est pas suffisamment basse pour prendre en charge des écritures à haute fréquence. Pour les charges de travail transactionnelles, utilisez Cloud SQL ou Firestore en fonction de votre préférence pour SQL ou NoSQL.

Vous ne voulez également pas utiliser Cloud Storage pour l'analyse de données structurées. Si vous le faites, vous devrez consacrer une quantité significative de calcul à l'analyse des données, il est donc préférable d'utiliser Cloud Bigtable ou BigQuery pour les charges de travail d'analyse sur des données structurées, en fonction de la latence requise.

![](Aspose.Words.a31beb3f-fb98-45c7-be4a-3b0e8a4b1f30.020.png)

Nous continuons à parler des charges de travail transactionnelles par rapport aux charges de travail analytiques. Que voulons-nous dire exactement ?

Les charges de travail transactionnelles sont celles dans lesquelles vous avez besoin d'insertions et de mises à jour rapides. Vous souhaitez maintenir un instantané, un état actuel du système. Le compromis est que les requêtes ont tendance à être relativement simples et à affecter seulement quelques enregistrements.

Par exemple, dans un système bancaire, déposer votre salaire sur votre compte est une transaction. Cela met à jour le champ du solde. La banque effectue un traitement de transaction en ligne ou O-L-T-P (Online Transaction Processing).

D'autre part, une charge de travail analytique a tendance à lire l'ensemble des données et est souvent utilisée pour la planification ou le support décisionnel. Les données peuvent provenir d'un système de traitement des transactions, mais elles sont souvent consolidées à partir de nombreux systèmes O-L-T-P.

Par exemple, un régulateur bancaire peut nous demander de fournir un rapport de chaque client ayant transféré plus de 10 000 $ sur un compte à l'étranger. Ils peuvent demander à la banque d'inclure les clients qui tentent de transférer les 10 000 $ en plusieurs morceaux sur une semaine. Un rapport de ce type nécessitera une analyse approfondie d'un ensemble de données considérable et nécessitera une requête complexe impliquant une agrégation sur des fenêtres temporelles mobiles.

Il s'agit d'un exemple de traitement analytique en ligne ou d'une charge de travail O-LAP (Online Analytical Processing).

![](Aspose.Words.a31beb3f-fb98-45c7-be4a-3b0e8a4b1f30.021.png)

La raison pour laquelle nous traitons ces cas d'utilisation différemment est que les systèmes transactionnels sont orientés vers l'écriture.

Ceux-ci ont tendance à être des systèmes opérationnels. Par exemple, les données de catalogue d'un détaillant devront être mises à jour chaque fois que le détaillant ajoute un nouvel article ou modifie le prix.

Les données d'inventaire devront être mises à jour chaque fois que le détaillant vend un article. Cela est dû au fait que les systèmes de catalogue et d'inventaire doivent maintenir une image instantanée de l'activité de l'entreprise.

![](Aspose.Words.a31beb3f-fb98-45c7-be4a-3b0e8a4b1f30.022.png)

Les systèmes analytiques peuvent être périodiquement alimentés à partir des systèmes opérationnels. Nous pourrions utiliser cela une fois par jour pour générer un rapport des articles de notre catalogue dont les ventes augmentent, mais dont les niveaux de stock sont faibles. Un tel rapport devra lire une grande quantité de données, mais n'aura pas besoin d'écrire beaucoup. Les systèmes OLAP sont axés sur la lecture.

![](Aspose.Words.a31beb3f-fb98-45c7-be4a-3b0e8a4b1f30.023.png)

Rappelez-vous ce que nous avons dit. Les systèmes analytiques peuvent être périodiquement alimentés à partir des systèmes opérationnels.

Les ingénieurs de données construisent les pipelines pour alimenter le système O-LAP à partir du système OLTP.

Une façon simple pourrait consister à exporter la base de données sous forme de fichier et à la charger dans l'entrepôt de données. C'est ce que nous appelons E-L.

![](Aspose.Words.a31beb3f-fb98-45c7-be4a-3b0e8a4b1f30.024.png)

Sur Google Cloud, le data warehouse tend à être BigQuery. Il y a une limite à la taille des données que vous pouvez charger directement dans BigQuery. Cela est dû au fait que votre réseau peut constituer un goulot d'étranglement.

Au lieu de charger les données directement dans BigQuery, il peut être beaucoup plus pratique de les charger d'abord dans Cloud Storage, puis de les charger depuis Cloud Storage vers BigQuery. Le chargement depuis Cloud Storage sera également plus rapide en raison de son débit élevé.

![](Aspose.Words.a31beb3f-fb98-45c7-be4a-3b0e8a4b1f30.025.png)

Revenons à la discussion sur les charges de travail transactionnelles, vous avez quelques options pour les bases de données relationnelles. Le choix par défaut ici est Cloud SQL, mais si vous avez besoin d'une base de données distribuée à l'échelle mondiale, utilisez Cloud Spanner.

Vous voudriez une base de données distribuée à l'échelle mondiale si votre base de données doit recevoir des mises à jour à partir d'applications s'exécutant dans différentes régions géographiques. La capacité True Time de Spanner est très attrayante pour ce type de cas d'utilisation.

Une autre raison pour laquelle vous pourriez choisir Spanner est si votre base de données est trop volumineuse pour tenir dans une seule instance de Cloud SQL. Si notre base de données fait plusieurs gigaoctets, vous avez besoin d'une base de données distribuée. La capacité de mise à l'échelle de Spanner est très attrayante pour ce cas d'utilisation.

Mis à part cela, vous utiliseriez Cloud SQL car il est plus rentable en termes de coûts.

![](Aspose.Words.a31beb3f-fb98-45c7-be4a-3b0e8a4b1f30.026.png)

Pour les charges de travail analytiques, le choix par défaut est BigQuery.

Cependant, si vous avez besoin d'insertions à haut débit, de plusieurs millions de lignes par seconde, ou si vous avez besoin d'une faible latence, de l'ordre des millisecondes, utilisez Cloud Bigtable.

Mis à part cela, vous utiliseriez BigQuery car il est plus rentable en termes de coûts.

Cloud SQL en tant que Data Lake relationnel

![](Aspose.Words.a31beb3f-fb98-45c7-be4a-3b0e8a4b1f30.027.png)

Cloud SQL est un service facile à utiliser qui offre des bases de données relationnelles entièrement gérées.

Cloud SQL vous permet de confier à Google les tâches ennuyeuses mais nécessaires et souvent chronophages, telles que l'application de correctifs et de mises à jour, la gestion des sauvegardes et la configuration des réplications, afin que vous puissiez vous concentrer sur la création d'excellentes applications.

Cloud SQL est notre service géré pour les SGBDR (systèmes de gestion de bases de données relationnelles) tiers. Il prend en charge MySQL, PostgreSQL et Microsoft SQL Server, et d'autres SGBDR seront ajoutés avec le temps.

Ce que cela signifie, c'est que nous fournissons une instance de moteur de calcul avec MySQL déjà installé. Nous gérerons l'instance pour vous.

Nous effectuerons des sauvegardes, des mises à jour de sécurité et mettrons à jour les versions mineures du logiciel afin que vous n'ayez pas à vous en soucier.

En d'autres termes, Google Cloud gère la base de données MySQL au point que vous pouvez la considérer comme un service.

Nous faisons même des choses similaires à un administrateur de base de données. Vous pouvez nous demander d'ajouter une réplication de basculement pour votre base de données. Nous la gérerons pour vous et vous aurez un SLA (accord de niveau de service) de disponibilité de 99,95 %.

![](Aspose.Words.a31beb3f-fb98-45c7-be4a-3b0e8a4b1f30.028.png)

Un autre avantage des instances Cloud SQL est qu'elles sont accessibles par d'autres services Google Cloud et même par des services externes. Vous pouvez utiliser Cloud SQL avec App Engine en utilisant des pilotes standard tels que Connector/J pour Java ou MySQLdb pour Python.

Vous pouvez autoriser les instances Compute Engine à accéder aux instances Cloud SQL et configurer l'instance Cloud SQL pour qu'elle se trouve dans la même zone que votre machine virtuelle.

Cloud SQL prend également en charge d'autres applications et outils auxquels vous pourriez être habitué, tels que SQL Workbench, Toad et d'autres applications externes utilisant des pilotes MySQL standard.

![](Aspose.Words.a31beb3f-fb98-45c7-be4a-3b0e8a4b1f30.029.png)

- Un des avantages de la gestion de votre base de données par Google est que vous bénéficiez des avantages de la sécurité de Google. Les données des clients de Cloud SQL sont chiffrées lorsqu'elles circulent sur les réseaux internes de Google et lorsqu'elles sont stockées dans les tables de la base de données, les fichiers temporaires et les sauvegardes. Chaque instance de Cloud SQL inclut un pare-feu réseau, ce qui vous permet de contrôler l'accès réseau à votre instance de base de données en accordant des autorisations d'accès.
- Cloud SQL est facile à utiliser : il ne nécessite aucune installation de logiciel ni aucune maintenance. De plus, Google gère les sauvegardes. Cloud SQL se charge de stocker vos données sauvegardées de manière sécurisée et vous permet de les restaurer facilement à partir d'une sauvegarde et d'effectuer une récupération à un instant précis de l'instance. Cloud SQL conserve jusqu'à 7 sauvegardes pour chaque instance, ce qui est inclus dans le coût de votre instance.
- Vous pouvez effectuer une mise à l'échelle verticale de Cloud SQL en augmentant simplement la taille de votre machine. Vous pouvez passer jusqu'à 64 cœurs de processeur et plus de 100 Go de RAM.
- Horizontalement, vous pouvez rapidement mettre à l'échelle avec des répliques de lecture. Google Cloud SQL prend en charge trois scénarios de réplication de répliques de lecture :
  - Des instances de Cloud SQL répliquant à partir d'une instance principale de Cloud SQL.
  - Des instances de Cloud SQL répliquant à partir d'une instance principale externe.
  - Des instances MySQL externes répliquant à partir d'une instance principale de Cloud SQL.

Si vous avez besoin d'une mise à l'échelle horizontale en lecture-écriture, envisagez d'utiliser Cloud Spanner.

![](Aspose.Words.a31beb3f-fb98-45c7-be4a-3b0e8a4b1f30.030.png)

Dans le cas spécifique de la reprise après incident, Cloud SQL prend en charge cela.

Les instances de Cloud SQL peuvent être configurées avec une réplication de basculement dans une zone différente de la même région. Ainsi, les données de Cloud SQL sont répliquées entre les zones au sein d'une région pour assurer la durabilité. En cas de panne improbable d'un centre de données, une instance de Cloud SQL sera automatiquement disponible dans une autre zone. Toutes les modifications apportées aux données sur le principal sont répliquées vers le basculement.

Si la zone de l'instance principale connaît une panne, Cloud SQL bascule automatiquement vers la réplique. Si le principal rencontre des problèmes non liés à une panne de zone, la bascule ne se produit pas. Cependant, vous pouvez déclencher manuellement la bascule.

<https://cloud.google.com/sql/docs/mysql/high-availability>

![](Aspose.Words.a31beb3f-fb98-45c7-be4a-3b0e8a4b1f30.031.png)

Il y a quelques points à prendre en compte :

- Notez que la réplique de basculement est facturée comme une instance distincte.
- Lorsqu'une panne de zone se produit et que votre instance principale bascule vers votre réplique de basculement, toutes les connexions existantes à l'instance sont fermées. Cependant, votre application peut se reconnecter en utilisant la même chaîne de connexion ou la même adresse IP ; vous n'avez pas besoin de mettre à jour votre application après une bascule.
- Après la bascule, la réplique devient la principale et Cloud SQL crée automatiquement une nouvelle réplique de basculement dans une autre zone. Si vous avez positionné votre instance Cloud SQL à proximité d'autres ressources, telles qu'une instance Compute Engine, vous pouvez ramener votre instance Cloud SQL dans sa zone d'origine lorsque celle-ci redevient disponible. Sinon, il n'est pas nécessaire de déplacer votre instance après une bascule. Vous pouvez utiliser la réplique de basculement comme réplique en lecture pour décharger les opérations de lecture de la principale.

![](Aspose.Words.a31beb3f-fb98-45c7-be4a-3b0e8a4b1f30.032.png)

Nous ne cessons de dire que Cloud SQL est entièrement géré. Nous avons également utilisé le terme "serverless" pour décrire BigQuery, par exemple. Quelle est la différence ?

- En tant que service entièrement géré, Cloud SQL vous offre un accès similaire à celui que vous auriez avec une installation sur site. Par exemple, vous pouvez vous connecter directement à l'instance Cloud SQL via le client gcloud et effectuer des tâches directement via SQL. Cependant, Google vous aide à gérer l'instance en automatisant les sauvegardes, en configurant des instances de basculement, et ainsi de suite.
- Le serverless est le niveau supérieur. Vous pouvez considérer un produit serverless comme une simple API que vous appelez. Vous payez pour l'utilisation du produit, mais vous n'avez pas à gérer de serveurs.

![](Aspose.Words.a31beb3f-fb98-45c7-be4a-3b0e8a4b1f30.033.png)

BigQuery est sans serveur. Il en va de même pour Pub/Sub pour la messagerie asynchrone et Dataflow pour le traitement parallèle des données.

Vous pouvez considérer que Cloud Storage est également sans serveur. Bien sûr, Cloud Storage utilise des disques, mais vous n'interagissez jamais directement avec le matériel. L'une des choses uniques de Google Cloud est que vous pouvez créer un pipeline de traitement des données composé de composants bien conçus, tous entièrement sans serveur.

D'autre part, Dataproc est entièrement géré. Il vous aide à exécuter des charges de travail Spark et Hadoop sans avoir à vous soucier de la configuration.

Si vous avez le choix entre démarrer un nouveau projet sur BigQuery ou Dataflow (qui sont sans serveur), et Dataproc (qui est entièrement géré), lequel devriez-vous choisir ?

Toutes choses étant égales par ailleurs, choisissez le produit sans serveur.

[Lab : Chargement des données de taxi dans Cloud SQL.](https://www.cloudskillsboost.google/course_sessions/3754403/video/382265)
