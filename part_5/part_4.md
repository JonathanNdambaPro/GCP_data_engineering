Fonctionnalités de diffusion à haut débit pour BigQuery et Bigtable sur GCP

Transmettre en continu vers BigQuery et visualiser les résultats.

![](Aspose.Words.be7fe248-aabb-40bd-b9d7-e89fc1f4eeb9.001.png)

Les données en continu ne sont pas ajoutées à BigQuery via une tâche de chargement. Il existe une méthode distincte dans BigQuery appelée "insertions en continu" (streaming inserts). Les insertions en continu vous permettent d'insérer un élément à la fois dans une table. De nouvelles tables peuvent être créées à partir d'une table temporaire qui identifie le schéma à copier. En général, les données sont disponibles en quelques secondes. Les données entrent dans un tampon en continu, où elles sont brièvement conservées jusqu'à ce qu'elles puissent être insérées dans la table. La disponibilité et la cohérence des données sont des considérations importantes. Les flux de données adaptés à cette méthode sont des analyses ou des applications tolérantes aux données tardives, manquantes, désordonnées ou en double. Le flux peut passer par d'autres services, introduisant ainsi une latence supplémentaire et la possibilité d'erreurs.

Étant donné que les données en continu sont illimitées, vous devez prendre en compte les quotas de streaming. Il existe à la fois une limite quotidienne et une limite de débit simultané. Vous pouvez trouver plus d'informations à ce sujet dans la documentation en ligne.

Vous pouvez désactiver la déduplication de meilleure tentative en ne renseignant pas le champ "insertId" pour chaque ligne insérée. Lorsque vous ne renseignez pas "insertId", vous bénéficiez de quotas d'ingestion en continu beaucoup plus élevés pour la région américaine (1 million d'insertions par seconde contre 500 000 insertions par seconde).

Cela soulève une question pertinente : quand devriez-vous ingérer un flux de données plutôt que d'utiliser une approche par lots pour charger des données ?

La réponse est : lorsque la disponibilité immédiate des données est une exigence de la solution. Et la raison en est la suivante : dans la plupart des cas, le chargement de données par lots n'est pas facturé. Le chargement de données en continu est une activité facturée. Utilisez donc le chargement par lots ou le chargement par lots répétitif plutôt que le streaming, sauf si la fonctionnalité en temps réel est une exigence de l'application.

![](Aspose.Words.be7fe248-aabb-40bd-b9d7-e89fc1f4eeb9.002.png)

Voici un exemple de code utilisé pour insérer des données en streaming dans une table BigQuery.

Dans cet exemple, le corps du message a déjà été décodé. Dans un exemple complet, une étape serait nécessaire pour extraire les éléments de message appropriés à insérer.

![](Aspose.Words.be7fe248-aabb-40bd-b9d7-e89fc1f4eeb9.003.png)

Après avoir démarré le flux vers une table BigQuery, vous pouvez consulter les données dans BigQuery en interrogeant la table qui reçoit les données en continu.

![](Aspose.Words.be7fe248-aabb-40bd-b9d7-e89fc1f4eeb9.004.png)

Lorsque vous travaillez avec des données dans BigQuery, y compris des données en streaming, vous pouvez utiliser Data Studio pour explorer davantage les données. Après avoir exécuté une requête, vous pouvez choisir Data Studio parmi les options d'exploration des données pour commencer immédiatement à créer des visualisations dans le cadre d'un tableau de bord.

![](Aspose.Words.be7fe248-aabb-40bd-b9d7-e89fc1f4eeb9.005.png)

Voici la page d'accueil de Data Studio. Il existe deux façons de créer un nouveau rapport à partir de zéro :

- Sélectionnez "Rapport vierge" dans le panneau des modèles au milieu de l'écran.
- Ou cliquez sur le bouton "Créer" dans le volet de navigation à gauche de l'écran.

![](Aspose.Words.be7fe248-aabb-40bd-b9d7-e89fc1f4eeb9.006.png)

Notez que vous pouvez avoir l'une ou l'ensemble de ces sources de données dans un seul rapport Data Studio.

En plus des connecteurs Google, il existe également une liste croissante de connecteurs partenaires parmi lesquels choisir.

![](Aspose.Words.be7fe248-aabb-40bd-b9d7-e89fc1f4eeb9.007.png)

Étant donné que nous sommes dans le contexte de GCP :

Étant donné que les rapports Data Studio peuvent être partagés, vous devez être conscient des conséquences de l'ajout d'une source de données.

Lorsque vous ajoutez une source de données à un rapport, d'autres personnes qui peuvent consulter le rapport peuvent potentiellement voir toutes les données de cette source de données. Et toute personne pouvant modifier le rapport peut utiliser tous les champs de toutes les sources de données ajoutées pour créer de nouveaux graphiques avec eux. Cliquez sur "AJOUTER AU RAPPORT".

![](Aspose.Words.be7fe248-aabb-40bd-b9d7-e89fc1f4eeb9.008.png)

Une fois que vous avez sélectionné un jeu de données, vous pouvez spécifier quels éléments du jeu de données vous souhaitez visualiser. Cela comprend la sélection des dimensions et des métriques que vous souhaitez utiliser à partir des champs disponibles de votre jeu de données.

![](Aspose.Words.be7fe248-aabb-40bd-b9d7-e89fc1f4eeb9.009.png)

Le sélecteur de source de données "Edit" situé devant le nom de la source de données peut être sélectionné pour modifier les champs du jeu de données.

![](Aspose.Words.be7fe248-aabb-40bd-b9d7-e89fc1f4eeb9.010.png)

Modifiez facilement votre vue de tableau de données en un graphique en cliquant sur "Graphique" dans le panneau des propriétés et en sélectionnant un type de graphique parmi les options proposées. Vous pouvez ensuite modifier le style de votre graphique, voire même changer ultérieurement votre sélection de type de graphique. Vous pouvez également revenir à une vue de tableau de données.

Vous pouvez également ajouter des graphiques séparés en sélectionnant "Ajouter un graphique" dans la barre d'outils. Redimensionnez les composants sur le canevas pour organiser les tableaux de données et les différents types de graphiques selon vos besoins. De la même manière que vous avez défini les dimensions et les mesures précédemment, faites de même pour votre graphique en ajoutant des sélections à partir de la liste des champs disponibles.

Astuce : La séquence des champs sous "Mesure" déterminera l'ordre dans lequel les données sont affichées dans le graphique. Utilisez la fonction de glisser-déposer pour modifier facilement la séquence des champs.

![](Aspose.Words.be7fe248-aabb-40bd-b9d7-e89fc1f4eeb9.011.png)

Donnez un nom à votre rapport.

Étant donné que Data Studio est basé sur Google Drive, veuillez noter que vous pouvez avoir des noms de fichiers en double.

![](Aspose.Words.be7fe248-aabb-40bd-b9d7-e89fc1f4eeb9.012.png)

Cliquez sur le bouton bascule Afficher pour afficher la version destinée à l'utilisateur final du rapport.

![](Aspose.Words.be7fe248-aabb-40bd-b9d7-e89fc1f4eeb9.013.png)

Et voici votre rapport. Remarquez qu'il ressemble beaucoup à celui que vous avez modifié, mais en tant que spectateur, vous ne pouvez pas modifier le rapport.

Lorsqu'un spectateur survole le graphique, il peut voir les données en direct. Dans cet exemple, le spectateur peut voir qu'en l'an 2000, il y a eu 31 catastrophes naturelles attribuables à des températures extrêmes.

Notez que les utilisateurs ne peuvent pas modifier vos rapports à moins que vous ne leur donniez la permission.

![](Aspose.Words.be7fe248-aabb-40bd-b9d7-e89fc1f4eeb9.014.png)

L'un des produits de Google Cloud qui aide à gérer les performances des tableaux de bord est BigQuery BI Engine. BI Engine est un service d'analyse rapide en mémoire intégré directement dans BigQuery, disponible pour accélérer vos applications d'intelligence d'affaires.

Historiquement, les équipes d'intelligence d'affaires devaient construire, gérer et optimiser leurs propres serveurs d'intelligence d'affaires et cubes OLAP pour prendre en charge les applications de reporting. Maintenant, avec BI Engine, vous pouvez obtenir un temps de réponse aux requêtes inférieur à la seconde sur vos ensembles de données BigQuery sans

avoir à créer vos propres cubes. BI Engine est construit sur la même architecture de stockage et de calcul de BigQuery, ainsi que sur les mêmes serveurs, en tant que service de mise en cache intelligent en mémoire rapide qui maintient un état.

[Lab : Traitement de données en continu, analyse en continu et tableaux de bord](https://www.cloudskillsboost.google/course_sessions/3849359/labs/345023)

Flux haute performance avec Cloud Bigtable

Jusqu'à présent, nous avons examiné comment effectuer des requêtes sur des données, même si elles sont en streaming, à l'aide de BigQuery, et comment afficher les données à l'aide de Data Studio. BigQuery est une solution très performante, adaptée à la plupart des cas. Cependant, il peut arriver que la latence de BigQuery pose problème.

Dans BigQuery, les données en streaming sont disponibles en quelques secondes, mais parfois vous souhaiterez une latence encore plus faible. Vous voudrez que vos informations soient disponibles en millisecondes ou en microsecondes. Il se peut également que vous rencontriez des problèmes de débit avec BigQuery et que vous souhaitiez traiter un débit plus élevé.

Nous allons donc maintenant examiner comment gérer de tels besoins en débit ou en latence lorsque BigQuery ne suffit pas. Où vous tournez-vous dans ce cas ? Nous parlerons de Cloud Bigtable, qui convient aux applications à haute performance. Nous verrons comment concevoir pour Bigtable, notamment la conception des schémas et des clés de ligne dans Bigtable. Nous étudierons également comment ingérer des données dans Bigtable.

![](Aspose.Words.be7fe248-aabb-40bd-b9d7-e89fc1f4eeb9.015.png)

Pour utiliser Bigtable de manière efficace, il est nécessaire de connaître en détail vos données et comment elles seront interrogées à l'avance. Une grande partie des optimisations se produisent avant le chargement des données dans Bigtable.

![](Aspose.Words.be7fe248-aabb-40bd-b9d7-e89fc1f4eeb9.016.png)

Bigtable est idéal pour les applications qui nécessitent un débit très élevé et une mise à l'échelle pour des données clés/valeurs non structurées, où chaque valeur est généralement inférieure à 10 Mo. Bigtable n'est pas adapté aux données hautement structurées, aux données transactionnelles, aux volumes de données inférieurs à 1 To et à tout ce qui nécessite des requêtes SQL et des jointures similaires à SQL.

![](Aspose.Words.be7fe248-aabb-40bd-b9d7-e89fc1f4eeb9.017.png)

Voici quelques exemples de besoins en ingénierie des données qui ont été résolus en utilisant Bigtable.

Les algorithmes d'apprentissage automatique ont souvent tous ou certains de ces besoins. Les applications qui utilisent des données marketing, telles que des historiques d'achats ou des préférences de clients. Les applications qui utilisent des données financières, telles que des historiques de transactions, des prix d'actions ou des taux de change.

Les données de l'Internet des objets (IoT), telles que des rapports d'utilisation provenant de compteurs, de capteurs ou d'appareils.

Les données de séries temporelles, telles que la consommation de ressources comme l'utilisation du processeur et de la mémoire au fil du temps pour plusieurs serveurs.

![](Aspose.Words.be7fe248-aabb-40bd-b9d7-e89fc1f4eeb9.018.png)

Bigtable est le plus souvent utilisé dans le contexte de GCP pour des recherches en temps réel dans une application où un débit élevé est nécessaire.

![](Aspose.Words.be7fe248-aabb-40bd-b9d7-e89fc1f4eeb9.019.png)

Bigtable stocke des données dans un système de fichiers appelé Colossus. Colossus contient également des structures de données appelées Tablets, qui sont utilisées pour identifier et gérer les données. Les métadonnées concernant les Tablets sont stockées sur les VM (machines virtuelles) dans le cluster Bigtable lui-même.

Cette conception confère des qualités exceptionnelles à Bigtable. Il dispose de trois niveaux d'opération. Il peut manipuler les données réelles, les Tablets qui pointent vers les données et les décrivent, ou les métadonnées qui pointent vers les Tablets.

Le rééquilibrage des Tablets d'un nœud à un autre est très rapide car seuls les pointeurs sont mis à jour.

Bigtable est un système d'apprentissage. Il détecte les "points chauds" où une grande quantité d'activité passe par un seul Tablet et divise le Tablet en deux. Il peut également rééquilibrer le traitement en déplaçant le pointeur d'un Tablet vers une VM différente dans le cluster. Par conséquent, son meilleur cas d'utilisation concerne les gros volumes de données - supérieurs à 300 Go - nécessitant un accès très rapide mais une utilisation constante sur une plus longue période. Cela permet à Bigtable d'apprendre le schéma de trafic et de rééquilibrer les Tablets et le traitement.

Lorsqu'un nœud est perdu dans le cluster, aucune donnée n'est perdue. La récupération est rapide car seules les métadonnées doivent être copiées sur le nœud de remplacement. Colossus offre une durabilité supérieure aux 3 réplicas par défaut fournis par HDFS.

![](Aspose.Words.be7fe248-aabb-40bd-b9d7-e89fc1f4eeb9.020.png)

Bigtable stocke les éléments de données réels dans des tables. Pour commencer, il s'agit simplement d'une table avec des lignes et des colonnes. Cependant, contrairement à d'autres systèmes de données basés sur des tableaux tels que les feuilles de calcul et les bases de données SQL, Bigtable n'a qu'un seul index. Cet index s'appelle la Clé de Ligne (Row Key). Il n'y a pas d'index alternatifs ou d'index secondaires. Lorsque des données sont saisies, elles sont organisées de manière lexicographique par la Clé de Ligne.

Le principe de conception de Bigtable est la vitesse par la simplification. Si vous prenez une table traditionnelle et simplifiez les contrôles et les opérations que vous vous autorisez à effectuer dessus, vous pouvez optimiser ces tâches spécifiques.

C'est la même idée derrière RISC - Reduced Instruction Set Computing (informatique à jeu d'instructions réduit) - Simplifiez les opérations. Et lorsque vous n'avez pas besoin de tenir compte des variations, vous pouvez rendre celles qui restent très rapides.

Dans Bigtable, la première chose que nous devons abandonner dans notre conception est SQL. C'est une norme pour toutes les opérations qu'une base de données peut effectuer. Et pour accélérer les choses, nous abandonnerons la plupart d'entre elles et nous construirons à partir d'un ensemble minimal d'opérations. C'est pourquoi Bigtable est appelé une base de données NoSQL.

![](Aspose.Words.be7fe248-aabb-40bd-b9d7-e89fc1f4eeb9.021.png)

**Analyse**

Les éléments verts sont les résultats que vous souhaitez obtenir à partir de la requête. Dans le meilleur des cas, vous allez analyser la clé de ligne une fois, de haut en bas. Et vous trouverez toutes les données que vous souhaitez récupérer dans des lignes adjacentes et contiguës. Vous devrez peut-être sauter certaines lignes. Mais la requête effectue une seule analyse de l'index de haut en bas pour collecter l'ensemble des résultats.

**Tri**

La deuxième instance est le tri. Vous ne regardez toujours que la clé de ligne. Dans ce cas, la ligne jaune contient des données que vous souhaitez, mais elles sont désordonnées. Vous pouvez collecter les données en une seule analyse, mais l'ensemble des solutions sera désordonné. Vous devez donc effectuer une étape supplémentaire pour trier les résultats intermédiaires afin d'obtenir les résultats finaux. Maintenant, réfléchissez à ceci. Que fait l'opération de tri supplémentaire au niveau du temps ? Elle introduit quelques variables. Si l'ensemble des solutions ne comporte que quelques lignes, alors l'opération de tri sera rapide. Mais si l'ensemble des solutions est énorme, le tri prendra plus de temps. La taille de l'ensemble des solutions devient un facteur dans le temps. L'ordre des données d'origine est un autre facteur. Si la plupart des lignes sont déjà triées, il y aura moins de manipulation nécessaire que s'il y a de nombreuses lignes désordonnées. L'ordre des données d'origine devient un facteur dans le temps. Ainsi, l'introduction du tri signifie que le temps nécessaire pour produire le résultat est beaucoup plus variable que lors de l'analyse.

**Recherche**

La troisième instance est la recherche. Dans ce cas, l'une des colonnes contient des données critiques. Vous ne pouvez pas dire si une ligne fait partie de l'ensemble des solutions ou non sans examiner les données contenues dans la colonne critique. La clé de ligne n'est plus suffisante. Vous passez donc maintenant en aller-retour entre la clé de ligne et le contenu des colonnes. Il existe de nombreuses approches pour la recherche. Vous pourriez le diviser en plusieurs étapes, une analyse des clés de ligne, puis des analyses ultérieures des colonnes, et peut-être un tri final pour obtenir les données dans l'ordre souhaité. Et cela devient beaucoup plus compliqué s'il y a plusieurs colonnes contenant des informations critiques. Et cela devient plus compliqué si les conditions d'appartenance à

l'ensemble des solutions impliquent une logique telle qu'une valeur dans une colonne ET une valeur dans une autre colonne, ou une valeur dans une colonne OU une valeur dans une autre colonne. Cependant, tout algorithme ou stratégie que vous utilisez pour produire le résultat sera plus lent et plus variable que l'analyse ou le tri.

Quelle est la leçon de cette exploration ? Pour obtenir les meilleures performances avec la conception du service Bigtable, vous devez d'abord organiser vos données, si possible, et vous devez sélectionner ou construire une clé de ligne qui réduit au minimum le tri et la recherche, et qui transforme vos requêtes les plus courantes en analyses.

Toutes les données et toutes les requêtes ne sont pas de bons cas d'utilisation pour l'efficacité offerte par le service Bigtable. Mais lorsque c'est une bonne correspondance, Bigtable est si constamment rapide que c'est magique.

![](Aspose.Words.be7fe248-aabb-40bd-b9d7-e89fc1f4eeb9.022.png)

Voici un exemple utilisant des données de vols aériens.

Chaque entrée enregistre l'occurrence d'un vol.

Les données comprennent la ville d'origine, la date et l'heure de départ, la ville de destination

et la date et l'heure d'arrivée.

Chaque avion a une capacité maximale, et en relation avec cela, le nombre de passagers réellement à bord de chaque vol.

Enfin, il y a des informations sur l'avion lui-même, y compris le fabricant (appelé la marque), le numéro de modèle et l'âge actuel de l'avion au moment du

vol.

![](Aspose.Words.be7fe248-aabb-40bd-b9d7-e89fc1f4eeb9.023.png)

Dans cet exemple, la clé de ligne (Row Key) sera définie pour le cas d'utilisation le plus courant. La requête consiste à trouver tous les vols partant de l'aéroport d'Atlanta et arrivant entre le 21 et le 29 mars. L'aéroport de départ du vol est indiqué dans le champ "Origin", et la date d'arrivée de l'avion est indiquée dans le champ "Arrival".

Si vous utilisez "Origin" comme clé de ligne, vous pourrez extraire tous les vols en provenance d'Atlanta, mais le champ "Arrival" ne sera pas nécessairement trié. Cela signifie qu'il faudra rechercher dans la colonne pour obtenir l'ensemble de solutions.

Si vous utilisez le champ "Arrival" comme clé de ligne, il sera facile d'extraire tous les vols entre le 21 et le 29 mars, mais l'aéroport de départ ne sera pas organisé. Vous devrez donc rechercher dans la colonne "Arrival" pour obtenir l'ensemble de solutions.

![](Aspose.Words.be7fe248-aabb-40bd-b9d7-e89fc1f4eeb9.024.png)

Bigtable offre également des familles de colonnes. En accédant à la famille de colonnes, vous pouvez extraire certaines des données dont vous avez besoin sans extraire toutes les données de la ligne ou devoir les rechercher et les assembler. Cela rend l'accès plus efficace.

![](Aspose.Words.be7fe248-aabb-40bd-b9d7-e89fc1f4eeb9.025.png)

La requête la plus courante concerne le retard actuel d'arrivée en provenance d'Atlanta. Cela impliquera de calculer la moyenne des retards de vol au cours des 30 dernières minutes. Par conséquent, il s'agit de l'arrivée d'origine. Nous voulons cela en haut du tableau, d'où l'utilisation du timestamp inversé ou RTS.

![](Aspose.Words.be7fe248-aabb-40bd-b9d7-e89fc1f4eeb9.026.png)

Vous pouvez inverser les horodatages en soustrayant l'horodatage de la valeur maximale des entiers longs de votre langage de programmation, telle que java.lang.Long.MAX\_VALUE en Java, par exemple LONG MAX timestamp.millisecondsSinceEpoch.

En inversant l'horodatage, vous pouvez concevoir une clé de ligne où l'événement le plus récent apparaît au début de la table au lieu de la fin. En conséquence, vous pouvez obtenir les N événements les plus récents en récupérant simplement les N premières lignes de la table.

![](Aspose.Words.be7fe248-aabb-40bd-b9d7-e89fc1f4eeb9.027.png)

Lorsque vous supprimez des données, la ligne est marquée pour suppression et ignorée lors des traitements ultérieurs. Elle n'est pas supprimée immédiatement.

Si vous apportez une modification aux données, la nouvelle ligne est ajoutée de manière séquentielle à la fin de la table et la version précédente est marquée pour suppression. Ainsi, les deux lignes existent pendant un certain temps.

Périodiquement, Bigtable compresse la table, en supprimant les lignes marquées pour suppression et en réorganisant les données pour une efficacité en lecture et en écriture.

![](Aspose.Words.be7fe248-aabb-40bd-b9d7-e89fc1f4eeb9.028.png)

La distribution des écritures entre les nœuds offre les meilleures performances en écriture. Une façon d'y parvenir est de choisir des clés de ligne distribuées de manière aléatoire. Cependant, choisir une clé de ligne regroupant des lignes liées de manière à ce qu'elles soient adjacentes facilite beaucoup la lecture de plusieurs lignes en une seule fois.

Dans notre exemple d'entreprise aérienne, si nous collectons des données météorologiques des villes aéroportuaires, nous pourrions construire une clé composée d'un hachage du nom de la ville avec un horodatage. La clé de ligne de l'exemple montré permettrait de récupérer l'ensemble des données pour Delhi, en Inde, en tant qu'intervalle continu de lignes.

Chaque fois qu'il y a des lignes contenant plusieurs valeurs de colonnes liées, il est judicieux de les regrouper dans une famille de colonnes. Certaines bases de données NoSQL souffrent d'une dégradation des performances s'il y a trop de familles de colonnes. Bigtable peut gérer jusqu'à 100 familles de colonnes sans perdre de performances. De plus, il est beaucoup plus efficace de récupérer des données à partir d'une ou plusieurs familles de colonnes que de récupérer l'ensemble des données d'une ligne.

Il n'existe actuellement aucun paramètre de configuration dans Bigtable pour la compression. Cependant, les données aléatoires ne peuvent pas être compressées aussi efficacement que les données organisées. La compression fonctionne mieux si les valeurs identiques sont proches les unes des autres, que ce soit dans la même ligne ou dans des lignes adjacentes. Si vous organisez vos clés de ligne de manière à ce que les lignes avec des données identiques soient adjacentes, les données peuvent être compressées de manière plus efficace.

![](Aspose.Words.be7fe248-aabb-40bd-b9d7-e89fc1f4eeb9.029.png)

Bigtable réécrit périodiquement votre table pour supprimer les entrées supprimées et réorganiser vos données afin de rendre les lectures et écritures plus efficaces. Il essaie de répartir équitablement les lectures et écritures sur tous les nœuds Bigtable.

Dans cet exemple, A, B, C, D, E ne sont pas des données, mais plutôt des pointeurs ou des références et des caches, c'est pourquoi le rééquilibrage n'est pas long. Nous déplaçons simplement des pointeurs.

Les données réelles se trouvent dans les tablettes du système de fichiers Colossus.

![](Aspose.Words.be7fe248-aabb-40bd-b9d7-e89fc1f4eeb9.030.png)

En se basant sur les schémas d'accès appris, Bigtable rééquilibre les données en conséquence et répartit la charge de travail entre les nœuds.

![](Aspose.Words.be7fe248-aabb-40bd-b9d7-e89fc1f4eeb9.031.png)

Avec un schéma bien conçu, les lectures et écritures devraient être réparties de manière équitable sur l'ensemble d'une table et d'un cluster. Cependant, dans certains cas, il est inévitable que certaines lignes soient consultées plus fréquemment que d'autres.

Dans ces cas, Bigtable redistribuera les tablettes afin que les lectures soient réparties de manière égale entre les nœuds du cluster.

Notez que garantir une répartition uniforme des lectures a été privilégié par rapport à une répartition équitable du stockage dans le cluster.

![](Aspose.Words.be7fe248-aabb-40bd-b9d7-e89fc1f4eeb9.032.png)

En 2019, Spotify a exécuté le plus grand travail de Dataflow à ce jour sur GCP avec Bigtable "... utilisé comme outil de remédiation entre les travaux de Dataflow afin de leur permettre de traiter et de stocker davantage de données de manière parallèle, plutôt que de devoir toujours regrouper les données". En utilisant Bigtable, Spotify a pu découper les travaux de Dataflow en plus petits composants, réutiliser les fonctionnalités principales et accélérer les travaux tout en les rendant plus résilients.

[https://techcrunch.com/2020/02/18/how-spotify-ran-the-largest-google-dataflow-job-ever-for- wrapped-2019/](https://techcrunch.com/2020/02/18/how-spotify-ran-the-largest-google-dataflow-job-ever-for-wrapped-2019/)

Optimisation des performances de Cloud Bigtable

![](Aspose.Words.be7fe248-aabb-40bd-b9d7-e89fc1f4eeb9.033.png)

Il existe plusieurs facteurs pouvant entraîner des performances plus lentes :

Le schéma de la table n'est pas correctement conçu. Il est essentiel de concevoir un schéma qui permet la répartition équilibrée des lectures et écritures sur le cluster Bigtable. Sinon, des nœuds individuels peuvent être surchargés, ce qui ralentit les performances.

La charge de travail n'est pas adaptée à Bigtable. Si vous effectuez des tests avec une petite quantité de données (moins de 300 gigaoctets) ou pendant une très courte période (quelques secondes plutôt que des minutes ou des heures), Bigtable ne pourra pas optimiser correctement vos données. Il a besoin de temps pour apprendre vos modèles d'accès et il a besoin de fragments de données suffisamment importants pour utiliser tous les nœuds de votre cluster.

Le cluster Bigtable ne dispose pas d'un nombre suffisant de nœuds. En général, les performances augmentent de manière linéaire avec le nombre de nœuds dans un cluster. Ajouter plus de nœuds peut donc améliorer les performances. Utilisez les outils de surveillance pour vérifier si un cluster est surchargé.

Le cluster Bigtable a été récemment redimensionné. Bien que les nœuds soient disponibles presque immédiatement dans votre cluster, Bigtable peut mettre jusqu'à 20 minutes sous charge pour répartir de manière optimale la charge de travail du cluster sur les nouveaux nœuds.

Le cluster Bigtable utilise des disques HDD. L'utilisation de disques HDD au lieu de disques SSD entraîne des temps de réponse plus lents et une limite considérablement plus basse sur le nombre de requêtes de lecture traitées par seconde (500 QPS pour les disques HDD contre 10 000 QPS pour les disques SSD).

Il y a des problèmes avec la connexion réseau. Les problèmes de réseau peuvent réduire le débit et entraîner des lectures et des écritures plus longues que d'habitude. En particulier, vous rencontrerez des problèmes si vos clients ne s'exécutent pas dans la même zone que votre cluster Bigtable.

Étant donné que différentes charges de travail peuvent entraîner des variations de performances, vous devriez effectuer des tests avec vos propres charges de travail pour obtenir les résultats les plus précis.

![](Aspose.Words.be7fe248-aabb-40bd-b9d7-e89fc1f4eeb9.034.png)

Voici un exemple de certains des chiffres possibles en termes de débit dans le contexte de GCP :

Avec 100 nœuds, vous pouvez gérer 1 million de requêtes par seconde. Le débit augmente de manière linéaire jusqu'à des centaines de nœuds.

![](Aspose.Words.be7fe248-aabb-40bd-b9d7-e89fc1f4eeb9.035.png)

Il y a des choses que vous pouvez faire pour améliorer les performances en écriture et en lecture.

Il y a des choses que vous pouvez faire qui impliquent un compromis où l'amélioration de l'écriture peut entraîner un coût en termes de lecture.

![](Aspose.Words.be7fe248-aabb-40bd-b9d7-e89fc1f4eeb9.036.png)

Un débit plus élevé signifie que plus d'éléments sont traités dans une période donnée. Si vous avez des lignes plus grandes, alors moins d'entre elles seront traitées dans la même période de temps. En général, les lignes plus petites offrent un débit plus élevé et sont donc meilleures pour les performances en streaming.

Bigtable prend du temps pour traiter les cellules dans une ligne. Donc, s'il y a moins de cellules dans une ligne, cela offrira généralement de meilleures performances que s'il y en a plus.

Enfin, choisir la bonne clé de ligne est essentiel. Les lignes sont triées lexicographiquement. L'objectif lors de l'optimisation pour le streaming est d'éviter de créer des points chauds lors de l'écriture, ce qui obligerait Bigtable à diviser les tablettes et à ajuster les charges. Pour cela, vous voulez que les données soient réparties aussi uniformément que possible.

Les retards de lecture, ajoutés aux retards de traitement, entraînent un temps de réponse plus long.

<https://cloud.google.com/bigtable/docs/performance>

![](Aspose.Words.be7fe248-aabb-40bd-b9d7-e89fc1f4eeb9.037.png)

La réplication pour Bigtable vous permet d'augmenter la disponibilité et la durabilité de vos données en les copiant dans plusieurs régions ou plusieurs zones au sein d'une même région. Vous pouvez également isoler les charges de travail en acheminant différents types de requêtes vers différents clusters.

Utilisez "gcloud bigtable clusters create" pour créer un cluster de réplicas Bigtable. Si un cluster Bigtable devient non réactif, la réplication permet à un trafic entrant de basculer vers un autre cluster dans la même instance. Les basculements peuvent être manuels ou automatiques, selon le profil d'application utilisé par une application et la configuration du profil d'application.

La possibilité de créer plusieurs clusters dans une instance est précieuse pour les performances, car l'un peut être dédié à l'écriture et le cluster de réplicas exclusivement à la lecture. Bigtable prend également en charge le basculement automatique pour une haute disponibilité.

<https://cloud.google.com/bigtable/docs/replication-overview>

![](Aspose.Words.be7fe248-aabb-40bd-b9d7-e89fc1f4eeb9.038.png)

Les généralisations consistant à isoler la charge d'écriture, augmenter le nombre de nœuds et réduire la taille des lignes et des cellules ne s'appliqueront pas dans tous les cas. Dans la plupart des circonstances, l'expérimentation est la clé pour définir la meilleure solution.

Une estimation des performances est fournie dans la documentation en ligne pour les charges de travail en écriture seule. Bien sûr, l'objectif de l'écriture de données est de les lire ultérieurement, donc la situation idéale est un cas de référence.

Au moment de la rédaction de ceci, un cluster SSD à 10 nœuds avec des lignes de 1 kilooctet et une charge de travail en écriture seule peut traiter 10 000 lignes par seconde avec un délai de 6 millisecondes. Cette estimation sera affectée par la taille moyenne des lignes, l'équilibre et le timing des lectures qui peuvent perturber les écritures, ainsi que par d'autres facteurs.

Vous devrez exécuter des tests de performance avec vos données réelles et votre code d'application. Vous devez exécuter les tests sur au moins 300 gigaoctets de données pour obtenir des résultats valides. De plus, pour obtenir des résultats valides, vos tests doivent effectuer suffisamment d'actions sur une période suffisamment longue pour permettre à Bigtable d'apprendre le schéma d'utilisation et d'effectuer ses optimisations internes.

<https://cloud.google.com/bigtable/docs/performance>

![](Aspose.Words.be7fe248-aabb-40bd-b9d7-e89fc1f4eeb9.039.png)

Key Visualizer est un outil qui vous aide à analyser les schémas d'utilisation de votre Bigtable. Il génère des rapports visuels pour vos tables qui décomposent votre utilisation en fonction des clés de ligne auxquelles vous accédez. Key Visualizer génère automatiquement des analyses horaires et quotidiennes pour chaque table de votre instance qui répond à au moins l'un des critères suivants :

- Au cours des 24 dernières heures, la table contenait au moins 30 gigaoctets de données à un moment donné.
- Au cours des 24 dernières heures, la moyenne de toutes les lectures ou de toutes les écritures était d'au moins 10 000 lignes par seconde.

Le cœur d'une analyse Key Visualizer est la carte thermique, qui montre la valeur d'une métrique au fil du temps, décomposée en plages continues de clés de ligne. L'axe des x de la carte thermique représente le temps et l'axe des y représente les clés de ligne. Si la métrique a une faible valeur pour un groupe de clés de ligne à un moment donné, la métrique est "froide" et apparaît dans une couleur sombre. Une valeur élevée est "chaude" et apparaît dans une couleur vive ; les valeurs les plus élevées apparaissent en blanc.

[Lab : Traitement de données en continu, pipelines de traitement de données en continu vers Bigtable](https://www.cloudskillsboost.google/course_sessions/3849359/labs/345028)
