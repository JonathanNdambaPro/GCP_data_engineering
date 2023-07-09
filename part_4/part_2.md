Exécuter Spark sur Dataproc

Dans ce module, nous aborderons Dataproc, le service Hadoop géré par Google Cloud, et plus particulièrement Apache Spark.

L’Écosystème Hadoop

![](Aspose.Words.71968ec4-cb76-4c34-b13b-d7e85bbcac39.001.png)

Il est utile de replacer les services que vous allez apprendre dans un contexte historique, dans le cadre de GCP (Google Cloud Platform).

Avant 2006, le terme "big data" faisait référence à de grandes bases de données. La conception des bases de données était issue d'une époque où le stockage était relativement bon marché et le traitement était coûteux. Il était donc logique de copier les données depuis leur emplacement de stockage vers le processeur pour effectuer le traitement des données. Ensuite, le résultat était copié de nouveau vers le stockage.

![](Aspose.Words.71968ec4-cb76-4c34-b13b-d7e85bbcac39.002.png)

Vers 2006, le traitement distribué du Big Data est devenu pratique avec Hadoop. Le

l'idée derrière Hadoop est de créer un cluster d'ordinateurs et de tirer parti

traitement. HDFS - le système de fichiers distribué Hadoop - stockait les données sur le machines du cluster, et MapReduce a assuré le traitement distribué des données.

Tout un écosystème de logiciels liés à Hadoop s'est développé autour de Hadoop, y compris Ruche, cochon et étincelle.

![](Aspose.Words.71968ec4-cb76-4c34-b13b-d7e85bbcac39.003.png)

Les organisations utilisent Hadoop pour les charges de travail big data sur site. Elles utilisent diverses applications s'exécutant sur des clusters Hadoop, telles que Presto, mais de nombreux clients utilisent Spark.

Apache Hadoop est un projet de logiciel open source qui maintient le framework de traitement distribué de vastes ensembles de données sur des clusters d'ordinateurs en utilisant des modèles de programmation simples. HDFS est le système de fichiers principal utilisé par Hadoop pour distribuer les tâches aux nœuds du cluster.

Apache Spark est un projet de logiciel open source qui fournit un moteur d'analyse à haute performance pour le traitement de données par lots et en continu. Spark peut être jusqu'à 100 fois plus rapide que les tâches Hadoop équivalentes car il tire parti du traitement en mémoire. Spark propose également plusieurs fonctionnalités pour travailler avec les données, notamment les ensembles de données distribués résilients et les DataFrames. Spark est particulièrement puissant et expressif, et il est utilisé pour de nombreuses charges de travail.

Une grande partie de la complexité et de la surcharge d'Hadoop OSS provient des hypothèses de conception qui existaient dans les centres de données. En se libérant de ces limitations, le traitement des données devient une solution beaucoup plus riche avec de nombreuses options supplémentaires.

Il y a deux problèmes courants avec Hadoop OSS : l'optimisation et l'utilisation.

Dans de nombreux cas, l'utilisation de Dataproc tel que conçu permet de surmonter ces limitations.

![](Aspose.Words.71968ec4-cb76-4c34-b13b-d7e85bbcac39.004.png)

Les clusters Hadoop sur site, en raison de leur nature physique, souffrent de limitations. Le manque de séparation entre les ressources de stockage et de calcul entraîne des limites de capacité et une incapacité à se développer rapidement. La seule façon d'augmenter la capacité est d'ajouter davantage de serveurs physiques.

![](Aspose.Words.71968ec4-cb76-4c34-b13b-d7e85bbcac39.005.png)

Il existe de nombreuses façons d'utiliser Google Cloud Platform (GCP) pour gagner du temps, de l'argent et des efforts par rapport à l'utilisation d'une solution Hadoop sur site. Dans de nombreux cas, adopter une approche basée sur le cloud peut rendre votre solution globale plus simple et facile à gérer.

Prise en charge intégrée de Hadoop

Dataproc est un environnement Hadoop et Spark géré. Vous pouvez utiliser Dataproc pour exécuter la plupart de vos tâches existantes avec un minimum de modifications, vous n'avez donc pas besoin de renoncer à tous les outils Hadoop que vous connaissez déjà.

Gestion du matériel et de la configuration gérée

Lorsque vous exécutez Hadoop sur Google Cloud, vous n'avez jamais à vous soucier du matériel physique. Vous spécifiez la configuration de votre cluster et Dataproc alloue les ressources pour vous. Vous pouvez faire évoluer votre cluster à tout moment.

Gestion simplifiée des versions

Maintenir à jour et faire fonctionner ensemble des outils open source est l'une des parties les plus complexes de la gestion d'un cluster Hadoop. Lorsque vous utilisez Dataproc, une grande partie de ce travail est gérée pour vous grâce à la gestion des versions de Dataproc.

Configuration flexible des tâches

Une configuration Hadoop classique sur site utilise un seul cluster qui sert à de nombreuses tâches. Lorsque vous passez à Google Cloud, vous pouvez vous concentrer sur des tâches individuelles, en créant autant de clusters que nécessaire. Cela élimine une grande partie de la complexité liée à la maintenance d'un seul cluster avec des dépendances croissantes et des interactions de configuration logicielle.

![](Aspose.Words.71968ec4-cb76-4c34-b13b-d7e85bbcac39.006.png)

Exécuter MapReduce directement sur Hadoop est très utile. Cependant, cela présente la complication que le système Hadoop doit être "optimisé" pour le type de tâche en cours d'exécution afin d'utiliser efficacement les ressources sous-jacentes. Une explication simple de Spark est qu'il est capable de mélanger différents types d'applications et d'ajuster la manière dont il utilise les ressources disponibles.

Spark utilise un modèle de programmation déclaratif. En programmation impérative, vous dites au système quoi faire et comment le faire. En programmation déclarative, vous indiquez au système ce que vous voulez et il se charge de déterminer comment le mettre en œuvre. Vous apprendrez à travailler avec Spark dans les travaux pratiques de ce cours.

Il existe une implémentation SQL complète sur Spark. Il existe un modèle commun de DataFrame qui fonctionne avec Scala, Java, Python, SQL et R. De plus, il existe une bibliothèque d'apprentissage automatique distribuée appelée Spark ML-Lib.

Exécuter Hadoop sur Dataproc

![](Aspose.Words.71968ec4-cb76-4c34-b13b-d7e85bbcac39.007.png)

Dataproc vous permet de profiter des outils de données open source pour le traitement par lots, les requêtes, le streaming et l'apprentissage automatique. L'automatisation de Dataproc vous aide à créer rapidement des clusters, à les gérer facilement et à économiser de l'argent en éteignant les clusters lorsque vous n'en avez pas besoin.

Comparé aux produits traditionnels sur site et aux services cloud concurrents, Dataproc présente des avantages uniques pour les clusters de trois à des centaines de nœuds. Il n'est pas nécessaire d'apprendre de nouveaux outils ou API pour utiliser Dataproc, ce qui facilite le transfert de projets existants vers Dataproc sans avoir à les re-développer. Spark, Hadoop, Pig et Hive sont fréquemment mis à jour.

Voici quelques-unes des principales caractéristiques de Dataproc :

**Coût réduit :** Dataproc est facturé à 1 centime par CPU virtuel par cluster par heure, en plus des autres ressources Google Cloud que vous utilisez. De plus, les clusters Dataproc peuvent inclure des instances préemptibles à des prix de calcul inférieurs. Vous utilisez et payez seulement ce dont vous avez besoin, ce qui fait que Dataproc propose une tarification à la seconde avec une période de facturation minimale d'une minute.

**Très rapide :** Les clusters Dataproc démarrent, se mettent à l'échelle et s'arrêtent rapidement, chaque opération prenant en moyenne 90 secondes ou moins.

**Clusters redimensionnables :** Les clusters peuvent être créés et mis à l'échelle rapidement avec différents types de machines virtuelles, tailles de disque, nombre de nœuds et options de mise en réseau.

**Écosystème open source :** Vous pouvez utiliser les outils, bibliothèques et documentation Spark et Hadoop avec Dataproc. Dataproc propose des mises à jour fréquentes des versions natives de Spark, Hadoop, Pig et Hive, il n'est donc pas nécessaire d'apprendre de nouveaux outils ou API, et il est possible de transférer des projets ou des pipelines ETL existants sans les re-développer.

**Intégré :** L'intégration intégrée avec Cloud Storage, BigQuery et Cloud Bigtable garantit que les données ne seront pas perdues. Cela, associé à Cloud Logging et Cloud Monitoring, offre une plate-forme de données complète et pas seulement un cluster Spark ou Hadoop. Par exemple, vous pouvez utiliser Dataproc pour extraire sans effort des téraoctets de données brutes de journaux directement dans BigQuery pour les rapports commerciaux.

**Géré :** Interagissez facilement avec les clusters et les tâches Spark ou Hadoop, sans l'aide d'un administrateur ou d'un logiciel spécial, via la Console Cloud, le SDK Cloud ou l'API REST Dataproc. Lorsque vous avez terminé avec un cluster, il suffit de l'éteindre pour ne pas dépenser d'argent sur un cluster inactif.

**Versioning :** Le versioning de l'image vous permet de passer d'une version à une autre d'Apache Spark, Apache Hadoop et d'autres outils.

**Haute disponibilité :** Exécutez des clusters avec plusieurs nœuds principaux et configurez les tâches pour qu'elles redémarrent en cas de panne, afin de garantir une haute disponibilité de vos clusters et tâches.

**Outils de développement :** Plusieurs façons de gérer un cluster, notamment la Console Cloud, le SDK Cloud, les API RESTful et l'accès SSH.

**Actions d'initialisation :** Exécutez des actions d'initialisation pour installer ou personnaliser les paramètres et les bibliothèques dont vous avez besoin lors de la création de votre cluster.

**Et configuration automatique ou manuelle :** Dataproc configure automatiquement le matériel et le logiciel des clusters pour vous tout en permettant également un contrôle manuel.

![](Aspose.Words.71968ec4-cb76-4c34-b13b-d7e85bbcac39.008.png)

Dataproc propose deux façons de personnaliser les clusters : les composants optionnels et les actions d'initialisation. Les composants optionnels préconfigurés peuvent être sélectionnés lors du déploiement depuis la console ou via la ligne de commande et comprennent : Anaconda, Hive WebHCat, Jupyter Notebook, Zeppelin Notebook, Druid, Presto et Zookeeper.

Les actions d'initialisation vous permettent de personnaliser votre cluster en spécifiant des exécutables ou des scripts que Dataproc exécutera sur tous les nœuds de votre cluster Dataproc immédiatement après la configuration du cluster.

![](Aspose.Words.71968ec4-cb76-4c34-b13b-d7e85bbcac39.009.png)

Voici un exemple de la façon dont vous pouvez créer un cluster Dataproc en utilisant le Cloud SDK.

Et nous allons spécifier un script shell HBase à exécuter lors de l'initialisation des clusters.

Il existe de nombreux scripts de démarrage préconstruits que vous pouvez exploiter pour des tâches courantes de configuration de cluster Hadoop, comme Flink, Jupyter et autres. Vous pouvez consulter le lien du référentiel GitHub dans les ressources du cours pour en savoir plus. Voyez-vous le paramètre supplémentaire pour le nombre de nœuds maîtres et de travail dans le script ? Parlons davantage de l'architecture du cluster.

<https://github.com/GoogleCloudPlatform/dataproc-initialization-actions>

![](Aspose.Words.71968ec4-cb76-4c34-b13b-d7e85bbcac39.010.png)

Un cluster Dataproc peut contenir soit des workers secondaires préemptibles, soit des workers secondaires non préemptibles, mais pas les deux en même temps.

L'architecture de configuration standard ressemble beaucoup à ce que vous attendriez sur site. Vous disposez d'un cluster de machines virtuelles pour le traitement, ainsi que de disques persistants pour le stockage via HDFS. Vous avez également des machines virtuelles de nœud principal dans un ensemble de nœuds de travail.

Les nœuds de travail peuvent également faire partie d'un groupe d'instances gérées, ce qui permet de garantir que les machines virtuelles de ce groupe sont toutes basées sur le même modèle. L'avantage est que vous pouvez créer plus de machines virtuelles que nécessaire pour redimensionner automatiquement votre cluster en fonction des besoins. Il ne faut également que quelques minutes pour mettre à niveau ou rétrograder votre cluster.

En général, vous ne devriez pas considérer un cluster Dataproc comme étant de longue durée. Au lieu de cela, vous devriez les créer lorsque vous avez besoin de puissance de calcul pour un travail, puis simplement les arrêter. Vous pouvez également les conserver indéfiniment si vous le souhaitez.

Que se passe-t-il avec le stockage HDFS sur disque lorsque vous arrêtez ces clusters ? Le stockage disparaîtrait également, c'est pourquoi il est recommandé d'utiliser un stockage en dehors du cluster en se connectant à d'autres produits de Google Cloud.

![](Aspose.Words.71968ec4-cb76-4c34-b13b-d7e85bbcac39.011.png)

Au lieu d'utiliser HDFS natif sur un cluster, vous pouvez simplement utiliser un cluster de buckets sur Cloud Storage via le connecteur HDFS.

Il est assez facile d'adapter le code Hadoop existant pour utiliser Cloud Storage à la place de HDFS.

Modifiez le préfixe de stockage de hdfs// à gs//.

Et qu'en est-il de Hbase hors cluster ? Considérez plutôt l'écriture dans Cloud Bigtable. Et qu'en est-il des charges de travail analytiques volumineuses ? Considérez la lecture de ces données dans BigQuery et l'exécution de ces charges de travail analytiques là-bas.

![](Aspose.Words.71968ec4-cb76-4c34-b13b-d7e85bbcac39.012.png)

La configuration signifie la création d'un cluster. Et vous pouvez le faire via la console Cloud ou en utilisant la commande gcloud en ligne de commande. Vous pouvez également exporter un fichier YAML à partir d'un cluster existant ou créer un cluster à partir d'un fichier YAML. Vous pouvez créer un cluster à partir d'une configuration Terraform ou utiliser l'API REST.

![](Aspose.Words.71968ec4-cb76-4c34-b13b-d7e85bbcac39.013.png)

Le cluster peut être configuré en tant qu'une seule machine virtuelle (VM), ce qui est généralement fait pour réduire les coûts liés au développement et à l'expérimentation. La configuration standard comprend une seule node principale (Primary Node), tandis que la haute disponibilité inclut trois nodes principales. Vous pouvez choisir une région et une zone spécifiques, ou sélectionner une "région globale" et laisser le service choisir la zone pour vous. Le cluster est par défaut configuré avec un point de terminaison global, mais la définition d'un point de terminaison régional peut offrir une isolation accrue et, dans certains cas, une latence réduite.

La node principale est l'endroit où le Namenode HDFS s'exécute, ainsi que le nœud YARN et les pilotes de tâches. La réplication HDFS est configurée par défaut à 2 dans Dataproc.

Des composants optionnels de l'écosystème Hadoop incluent : Anaconda (distribution et gestionnaire de packages Python), Hive Webcat, Jupyter Notebook et Zeppelin Notebook.

Les propriétés du cluster sont des valeurs d'exécution qui peuvent être utilisées par des fichiers de configuration pour des options de démarrage plus dynamiques. Les étiquettes d'utilisateur peuvent être utilisées pour marquer le cluster dans le cadre de vos propres solutions ou à des fins de reporting.

Les nodes principaux (Primary Node), les nodes de travail (Worker Nodes) et les nodes de travail préemptibles, s'ils sont activés, ont des options VM distinctes, telles que le nombre de vCPU, la mémoire et le stockage.

Les nodes préemptibles incluent le NodeManager YARN, mais n'exécutent pas le HDFS.

Il y a un nombre minimum de nodes de travail, par défaut 2. Le nombre maximum de nodes de travail est déterminé par un quota et le nombre de SSD attachés à chaque node.

Vous pouvez également spécifier des actions d'initialisation, telles que des scripts d'initialisation qui permettent de personnaliser davantage les nodes de travail. Et vous pouvez définir des métadonnées pour que les machines virtuelles puissent partager des informations d'état.

![](Aspose.Words.71968ec4-cb76-4c34-b13b-d7e85bbcac39.014.png)

Les machines virtuelles préemptives peuvent être utilisées pour réduire les coûts. N'oubliez pas qu'ils peuvent être retirés de

service à tout moment et dans les 24 heures. Votre application devra donc peut-être être conçu pour la résilience afin d'éviter la perte de données.

Les types de machines personnalisés vous permettent de spécifier l'équilibre de la mémoire et du processeur à régler

la machine virtuelle à la charge, vous ne gaspillez donc pas de ressources.

Une image personnalisée peut être utilisée pour préinstaller le logiciel afin de réduire le temps de

nœud personnalisé pour devenir opérationnel que si vous avez installé le logiciel au démarrage

script d'utilisation et d'initialisation.

Vous pouvez également utiliser un disque de démarrage SSD persistant pour un démarrage plus rapide du cluster.

![](Aspose.Words.71968ec4-cb76-4c34-b13b-d7e85bbcac39.015.png)

Les emplois peuvent être soumis via la Console, la commande gcloud ou l'API REST. Ils peuvent également être lancés par des services d'orchestration tels que Dataproc Workflow et Cloud Composer.

N'utilisez pas les interfaces directes de Hadoop pour soumettre des emplois car les métadonnées ne seront pas disponibles pour Dataproc en ce qui concerne la gestion des emplois et des clusters, et pour des raisons de sécurité, elles sont désactivées par défaut. Par défaut, les emplois ne sont pas redémarrables. Cependant, vous pouvez créer des emplois redémarrables via la ligne de commande ou l'API REST. Les emplois redémarrables doivent être conçus de manière à être idempotents et à détecter la succession et à restaurer l'état.

![](Aspose.Words.71968ec4-cb76-4c34-b13b-d7e85bbcac39.016.png)

Enfin, une fois que vous avez soumis votre tâche, vous souhaiterez la surveiller. Vous pouvez le faire en utilisant Cloud Monitoring. Vous pouvez également créer un tableau de bord personnalisé avec des graphiques et configurer la surveillance des politiques d'alerte pour envoyer des e-mails, par exemple, afin de pouvoir être informé en cas d'incident. Tous les détails provenant de HDFS, YARN, des métriques sur une tâche particulière ou des métriques globales pour le cluster, tels que l'utilisation du CPU, du disque et du réseau, peuvent tous être surveillés et signalés avec Cloud Monitoring.

Cloud Storage Au lieu de HDFS

![](Aspose.Words.71968ec4-cb76-4c34-b13b-d7e85bbcac39.017.png)

Les vitesses de réseau étaient initialement lentes, c'est pourquoi nous conservions les données aussi près que possible du processeur. Maintenant, avec le réseau pétabit, vous pouvez traiter le stockage et le calcul de manière indépendante et déplacer rapidement le trafic sur le réseau.

![](Aspose.Words.71968ec4-cb76-4c34-b13b-d7e85bbcac39.018.png)

Vos clusters Hadoop sur site nécessitent un stockage local sur leurs disques, car le même serveur exécute, calcule et stocke les tâches. C'est l'un des premiers domaines à optimiser. Vous pouvez exécuter HDFS dans le Cloud en déplaçant simplement vos charges de travail Hadoop vers Dataproc. C'est souvent la première étape vers le Cloud et ne nécessite aucun changement de code. Ça fonctionne simplement, mais HDFS dans le Cloud est une solution inférieure à long terme. Cela est dû au fonctionnement d'HDFS sur les clusters, avec la taille des blocs, la localité des données et la réplication des données dans HDFS.

**Taille des blocs**

En ce qui concerne la taille des blocs dans HDFS, vous liez les performances des entrées et sorties au matériel réel sur lequel le serveur s'exécute. Encore une fois, le stockage n'est pas élastique dans ce scénario ; vous êtes dans le cluster. Si vous manquez d'espace disque persistant sur votre cluster, vous devrez le redimensionner, même si vous n'avez pas besoin de puissance de calcul supplémentaire.

**Localité**

En ce qui concerne la localité des données, il y a des préoccupations similaires concernant le stockage des données sur des disques persistants individuels.

**Réplication**

C'est particulièrement vrai en ce qui concerne la réplication. Pour qu'HDFS soit hautement disponible, il réplique trois copies de chaque bloc vers le stockage. Il serait préférable d'avoir une solution de stockage gérée séparément des contraintes de votre cluster.

![](Aspose.Words.71968ec4-cb76-4c34-b13b-d7e85bbcac39.019.png)

Le réseau de Google permet de nouvelles solutions pour le Big Data. La structure réseau Jupiter au sein d'un centre de données de Google offre plus de 1 pétabit par seconde de bande passante. Pour mettre cela en perspective, c'est environ deux fois la quantité de trafic échangée sur l'ensemble d'Internet public. (Voir l'estimation annuelle de Cisco de tout le trafic Internet.)

Si vous tracez une ligne quelque part dans un réseau, la bande passante bisectionnelle est le débit de communication auquel les serveurs d'un côté de la ligne peuvent communiquer avec les serveurs de l'autre côté. Avec une bande passante bisectionnelle suffisante, n'importe quel serveur peut communiquer avec n'importe quel autre serveur à la vitesse maximale du réseau.

Avec une bande passante bisectionnelle pétabit, la communication est tellement rapide qu'il n'est plus logique de transférer des fichiers et de les stocker localement. Au lieu de cela, il est logique d'utiliser les données là où elles sont stockées.

![](Aspose.Words.71968ec4-cb76-4c34-b13b-d7e85bbcac39.020.png)

Au sein d'un centre de données Google, le nom interne de la couche de stockage massivement distribuée est appelé Colossus, et le réseau à l'intérieur du centre de données est appelé Jupiter. Les clusters Dataproc bénéficient de l'avantage de pouvoir augmenter ou réduire le nombre de machines virtuelles (VM) dont ils ont besoin pour effectuer le traitement, tout en confiant les besoins de stockage persistant au réseau Jupiter ultra-rapide vers un produit de stockage tel que Cloud Storage, contrôlé en coulisses par Colossus.

![](Aspose.Words.71968ec4-cb76-4c34-b13b-d7e85bbcac39.021.png)

Un continuum historique de la gestion des données se présente comme suit :

Avant 2006, le terme "big data" désignait les grandes bases de données. La conception des bases de données provenait d'une époque où le stockage était relativement bon marché et le traitement coûteux.

Aux alentours de 2006, le traitement distribué des big data est devenu réalisable grâce à Hadoop.

Vers 2010, BigQuery a été lancé, ce qui a été le premier d'une série de services Big Data développés par Google. Aux alentours de 2015, Google a lancé Dataproc, qui offre un service géré pour la création de clusters Hadoop et Spark et la gestion des charges de travail de traitement des données.

![](Aspose.Words.71968ec4-cb76-4c34-b13b-d7e85bbcac39.022.png)

L'un des principaux avantages de Hadoop dans le cloud est la séparation du calcul et du stockage. Avec Cloud Storage en tant que backend, vous pouvez considérer les clusters eux-mêmes comme des ressources éphémères, ce qui vous permet de ne pas payer pour la capacité de calcul lorsque vous n'exécutez aucun travail. De plus, Cloud Storage est un service de stockage entièrement évolutif et durable, qui est connecté à de nombreux autres projets Google Cloud.

![](Aspose.Words.71968ec4-cb76-4c34-b13b-d7e85bbcac39.023.png)

Le stockage Cloud pourrait être un remplacement direct pour votre backend HDFS pour Hadoop. Le reste de votre code fonctionnerait simplement. De plus, vous pouvez utiliser manuellement le connecteur de stockage Cloud sur vos clusters Hadoop non cloud si vous ne souhaitez pas migrer l'ensemble de votre cluster vers le Cloud pour le moment.

Avec HDFS, vous devez prévoir une capacité supérieure à celle des données actuelles et potentielles, et vous devez utiliser des disques persistants partout.

Avec le stockage Cloud, cependant, vous ne payez que ce dont vous avez réellement besoin, lorsque vous l'utilisez.

![](Aspose.Words.71968ec4-cb76-4c34-b13b-d7e85bbcac39.024.png)

Cloud Storage est optimisé pour les opérations parallèles massives et en vrac. Il offre un débit très élevé, mais présente une latence significative.

Si vous avez des tâches volumineuses qui traitent de nombreux petits blocs, il est préférable d'utiliser HDFS.

De plus, il est conseillé d'éviter d'itérer de manière séquentielle sur de nombreux répertoires imbriqués dans une seule tâche.

![](Aspose.Words.71968ec4-cb76-4c34-b13b-d7e85bbcac39.025.png)

L'utilisation de Cloud Storage plutôt que HDFS présente plusieurs avantages clés grâce au service distribué, notamment l'élimination des goulots d'étranglement et des points de défaillance uniques. Cependant, il y a quelques inconvénients à prendre en compte, notamment les défis posés par le renommage d'objets et l'incapacité à ajouter du contenu à des objets.

![](Aspose.Words.71968ec4-cb76-4c34-b13b-d7e85bbcac39.026.png)

Google Cloud Storage est essentiellement un service de stockage d'objets. Il simule uniquement un répertoire de fichiers. Par conséquent, les changements de nom de répertoires dans HDFS ne fonctionnent pas de la même manière que dans Cloud Storage. Cependant, les nouveaux orientés objets committers de sortie permettent de résoudre ce problème, comme vous pouvez le voir ici.

![](Aspose.Words.71968ec4-cb76-4c34-b13b-d7e85bbcac39.027.png)

DistCp est un outil essentiel pour le déplacement de données. En général, vous souhaitez utiliser un modèle basé sur la poussée (push) pour toute donnée que vous savez que vous aurez besoin de déplacer, tandis que le modèle basé sur la demande (pull) peut être utile s'il y a beaucoup de données que vous n'aurez peut-être jamais besoin de migrer.

<https://hadoop.apache.org/docs/current/hadoop-distcp/DistCp.html>

Optimisation de Dataproc

![](Aspose.Words.71968ec4-cb76-4c34-b13b-d7e85bbcac39.028.png)

**Où se trouvent vos données et où se trouve votre cluster ?**

Connaître la localisation de vos données peut avoir un impact majeur sur les performances. Vous voulez vous assurer que la région de vos données et la zone de votre cluster sont physiquement proches en distance. Lorsque vous utilisez Dataproc, vous pouvez omettre la zone et laisser la fonctionnalité Auto-Zone de Dataproc sélectionner une zone pour vous dans la région que vous choisissez.

Bien que cette fonctionnalité pratique puisse optimiser l'emplacement de votre cluster, elle ne sait pas anticiper l'emplacement des données auxquelles votre cluster accédera. Assurez-vous que le bucket de stockage Cloud est dans la même localisation régionale que votre région Dataproc.

**Votre trafic réseau est-il canalisé ?**

Assurez-vous de ne pas avoir de règles ou de routes réseau qui canalisent le trafic Cloud Storage à travers un petit nombre de passerelles VPN avant d'atteindre votre cluster. Il existe de gros tuyaux réseau entre Cloud Storage et Compute Engine. Vous ne voulez pas restreindre votre bande passante en envoyant du trafic dans un goulot d'étranglement de votre configuration de réseau Google Cloud.

**Combien de fichiers d'entrée et de partitions Hadoop essayez-vous de gérer ?** Assurez-vous de ne pas traiter plus d'environ 10 000 fichiers d'entrée. Si vous vous retrouvez dans cette situation, essayez de combiner ou "fusionner" les données en fichiers de plus grande taille. Si cette réduction du volume de fichiers signifie que vous travaillez maintenant avec des ensembles de données plus grands (plus d'environ 50 000 partitions Hadoop), vous devriez envisager d'ajuster le paramètre fs.gs.block.size en conséquence pour une valeur plus grande.

**La taille de votre disque persistant limite-t-elle votre débit ?**

Souvent, lorsque vous commencez avec Google Cloud, vous pouvez avoir une petite table que vous souhaitez utiliser comme référence.

C'est généralement une bonne approche, tant que vous ne choisissez pas un disque persistant de taille adaptée à une si petite quantité de données ; cela limitera très probablement vos performances. Les disques persistants standard évoluent linéairement avec la taille du volume.

**Avez-vous alloué suffisamment de machines virtuelles à votre cluster ?**

Une question qui revient souvent lors de la migration du matériel sur site vers Google Cloud est de savoir comment dimensionner précisément le nombre de machines virtuelles nécessaires.

Comprendre vos charges de travail est essentiel pour identifier la taille d'un cluster. Exécuter des prototypes et des tests de référence avec des données réelles et des tâches réelles est crucial pour prendre une décision d'allocation réelle de machines virtuelles. Heureusement, la nature éphémère du cloud permet de redimensionner facilement votre cluster selon vos besoins. L'utilisation de clusters à portée de tâche est une stratégie courante pour les clusters Dataproc.

![](Aspose.Words.71968ec4-cb76-4c34-b13b-d7e85bbcac39.029.png)

Le HDFS local est une bonne option si :

- Vos tâches nécessitent de nombreuses opérations de métadonnées - par exemple, vous avez des milliers de partitions et de répertoires, et chaque fichier est relativement petit.
- Vous modifiez fréquemment les données HDFS ou renommez des répertoires. Les objets Cloud Storage sont immuables, donc le renommage d'un répertoire est une opération coûteuse car elle consiste à copier tous les objets vers une nouvelle clé et à les supprimer ensuite.
- Vous utilisez massivement l'opération d'ajout (append) sur les fichiers HDFS.
- Vous avez des charges de travail impliquant une forte E/S (entrée/sortie). Par exemple, vous avez beaucoup d'écritures partitionnées, comme dans cet exemple.
- Vous avez des charges de travail d'E/S particulièrement sensibles à la latence. Par exemple, vous avez besoin d'une latence de l'ordre de quelques millisecondes par opération de stockage.

![](Aspose.Words.71968ec4-cb76-4c34-b13b-d7e85bbcac39.030.png)

En général, nous recommandons d'utiliser Cloud Storage comme source initiale et finale de données dans un pipeline de traitement de données volumineuses (big-data).

Par exemple, si un flux de travail comprend cinq tâches Spark en série, la première tâche récupère les données initiales à partir de Cloud Storage, puis écrit les données de redistribution (shuffle) et les sorties intermédiaires des tâches dans HDFS.

La tâche Spark finale enregistre ses résultats dans Cloud Storage.

![](Aspose.Words.71968ec4-cb76-4c34-b13b-d7e85bbcac39.031.png)

L'utilisation de Dataproc avec Cloud Storage vous permet de réduire les besoins en matière de disque et d'économiser des coûts en plaçant vos données là-bas au lieu de les stocker dans HDFS. Lorsque vous conservez vos données sur Cloud Storage et ne les stockez pas dans HDFS local, vous pouvez utiliser des disques plus petits pour votre cluster. En rendant votre cluster véritablement à la demande, vous pouvez également séparer le stockage et le calcul, comme mentionné précédemment, ce qui vous aide à réduire considérablement les coûts. Même si vous stockez toutes vos données dans Cloud Storage, votre cluster Dataproc a besoin de HDFS pour certaines opérations telles que le stockage des fichiers de contrôle et de récupération, ou l'agrégation des journaux. Il a également besoin d'un espace disque local non-HDFS pour le shuffle. Vous pouvez réduire la taille du disque par travailleur si vous n'utilisez pas intensivement le HDFS local.

![](Aspose.Words.71968ec4-cb76-4c34-b13b-d7e85bbcac39.032.png)

Voici quelques options pour ajuster la taille du HDFS local :

- Réduisez la taille totale du HDFS local en diminuant la taille des disques persistants principaux pour le nœud principal et les nœuds de travail. Le disque persistant principal contient également le volume d'amorçage et les bibliothèques système, donc allouez au moins 100 Go.
- Augmentez la taille totale du HDFS local en augmentant la taille du disque persistant principal des nœuds de travail. Considérez cette option avec prudence, car il est rare d'avoir des charges de travail offrant de meilleures performances en utilisant HDFS avec des disques persistants standard par rapport à l'utilisation de Cloud Storage ou du HDFS local avec SSD.
- Attachez jusqu'à huit SSD à chaque nœud de travail et utilisez ces disques pour le HDFS. C'est une bonne option si vous avez besoin d'utiliser le HDFS pour des charges de travail intensives en I/O et que vous avez besoin d'une latence de l'ordre de la dizaine de millisecondes. Assurez-vous d'utiliser un type de machine qui dispose de suffisamment de CPU et de mémoire sur le nœud de travail pour prendre en charge ces disques.
- Et utilisez des disques persistants SSD pour votre nœud principal ou vos nœuds de travail en tant que disque principal.

![](Aspose.Words.71968ec4-cb76-4c34-b13b-d7e85bbcac39.033.png)

Vous devez comprendre les répercussions de la géographie et des régions avant de configurer vos données et vos tâches. De nombreux services Google Cloud vous demandent de spécifier des régions ou des zones dans lesquelles allouer des ressources. La latence des demandes peut augmenter lorsque les demandes sont effectuées depuis une région différente de celle où les ressources sont stockées.

De plus, si les ressources du service et vos données persistantes sont situées dans des régions différentes, certaines appels aux services Google Cloud peuvent copier l'ensemble des données nécessaires d'une zone à une autre avant le traitement. Cela peut avoir un impact important sur les performances.

![](Aspose.Words.71968ec4-cb76-4c34-b13b-d7e85bbcac39.034.png)

Google Cloud Storage est le principal moyen de stocker des données non structurées dans Google Cloud, mais ce n'est pas la seule option de stockage. Certaines de vos données peuvent être mieux adaptées au stockage dans des produits conçus spécifiquement pour les big data.

Vous pouvez utiliser Cloud Bigtable pour stocker de grandes quantités de données dispersées. Cloud Bigtable est une API compatible avec HBase qui offre une latence faible et une grande évolutivité pour s'adapter à vos tâches.

Pour la gestion de données, vous pouvez utiliser BigQuery.

![](Aspose.Words.71968ec4-cb76-4c34-b13b-d7e85bbcac39.035.png)

Étant donné que nous sommes dans le contexte de GCP (Google Cloud Platform) :

Étant donné que Dataproc exécute Hadoop sur Google Cloud, il peut sembler plus facile d'utiliser un cluster Dataproc persistant pour reproduire votre configuration sur site. Cependant, cette approche présente certaines limitations.

- Le maintien de vos données dans un cluster HDFS persistant à l'aide de Dataproc est plus coûteux que le stockage de vos données dans Cloud Storage, ce que nous recommandons. Le fait de conserver les données dans un cluster HDFS limite également votre capacité à utiliser vos données avec d'autres produits Google Cloud.
- Le remplacement ou l'ajout de certains de vos outils basés sur des logiciels open source par d'autres services Google Cloud connexes peut être plus efficace ou plus économique pour des cas d'utilisation spécifiques.
- Utiliser un seul cluster Dataproc persistant pour vos tâches est plus difficile à gérer que de passer à des clusters ciblés qui servent des tâches individuelles ou des zones de travail.

La manière la plus rentable et la plus flexible de migrer votre système Hadoop vers Google Cloud consiste à abandonner la mentalité de grands clusters persistants et polyvalents, et à plutôt envisager de petits clusters éphémères conçus pour exécuter des tâches spécifiques.

Vous stockez vos données dans Cloud Storage pour prendre en charge plusieurs clusters de traitement temporaires. Ce modèle est souvent appelé modèle éphémère, car les clusters utilisés pour les tâches de traitement sont alloués au besoin et libérés lorsque les tâches sont terminées.

![](Aspose.Words.71968ec4-cb76-4c34-b13b-d7e85bbcac39.036.png)

Si vous avez une utilisation efficace, ne payez pas pour des ressources que vous n'utilisez pas - employez

suppression programmée.

Un laps de temps fixe après que le cluster est entré dans un état d'inactivité, vous pouvez définir automatiquement

une minuterie. Vous pouvez lui donner un horodatage, et le décompte commence immédiatement une fois que le

l'expiration a été fixée.

Vous pouvez définir une durée, le temps en secondes à attendre avant de baisser automatiquement

la grappe. Vous pouvez aller de dix minutes au minimum à 14 jours au maximum

à une granularité d'une seconde.

![](Aspose.Words.71968ec4-cb76-4c34-b13b-d7e85bbcac39.037.png)

Le plus grand changement dans votre approche entre l'exécution d'un flux de travail Hadoop sur site et l'exécution du même flux de travail sur Google Cloud est le passage des clusters monolithiques et persistants à des clusters spécialisés et éphémères. Vous créez un cluster lorsque vous avez besoin d'exécuter une tâche, puis vous le supprimez une fois la tâche

terminée. Les ressources requises par vos tâches ne sont actives que lorsqu'elles sont utilisées, vous ne payez donc que ce que vous utilisez. Cette approche vous permet de configurer les clusters en fonction des besoins de chaque tâche. Étant donné que vous n'avez pas à entretenir et configurer un cluster persistant, vous réduisez les coûts d'utilisation des ressources et d'administration du cluster.

Cette section décrit comment passer votre infrastructure Hadoop existante à un modèle éphémère.

Pour tirer le meilleur parti de Dataproc, les clients doivent passer à un modèle "éphémère" en n'utilisant des clusters que lorsqu'ils en ont besoin. Cela peut sembler effrayant car un cluster persistant est plus confortable. Cependant, avec la persistance des données dans Cloud Storage et le démarrage rapide de Dataproc, un cluster persistant est une perte de ressources. Si un cluster persistant est nécessaire, faites-le de petite taille. Les clusters peuvent être redimensionnés à tout moment.

Le modèle éphémère est la voie recommandée, mais il nécessite que le stockage soit dissocié du calcul.

![](Aspose.Words.71968ec4-cb76-4c34-b13b-d7e85bbcac39.038.png)

Séparez les formes de travail et les clusters séparés. Décomposez encore davantage avec des clusters spécifiques aux travaux.

Isoler les environnements de développement, de préproduction et de production en les exécutant sur des clusters distincts.

Lire à partir de la même source de données sous-jacente sur Cloud Storage. Ajouter des contrôles d'accès appropriés aux comptes de service pour protéger les données.

![](Aspose.Words.71968ec4-cb76-4c34-b13b-d7e85bbcac39.039.png)

Le but des clusters éphémères est de les utiliser uniquement pendant la durée des tâches. Lorsqu'il est temps d'exécuter une tâche, suivez ce processus :

1) Créez un cluster correctement configuré.
1) Exécutez votre tâche en envoyant la sortie vers Cloud Storage ou un autre emplacement persistant.
1) Supprimez le cluster.
1) Utilisez la sortie de votre tâche selon vos besoins.
1) Consultez les journaux dans Cloud Logging ou Cloud Storage.

![](Aspose.Words.71968ec4-cb76-4c34-b13b-d7e85bbcac39.040.png)

Si vous ne pouvez pas accomplir votre travail sans un cluster persistant, vous pouvez en créer un. Cette option peut être coûteuse et n'est pas recommandée s'il existe un moyen de terminer votre tâcheavec des clusters éphémères.

Vous pouvez minimiser le coût d'un cluster persistant en :

- Créant le plus petit cluster possible.
- Limitant votre travail sur ce cluster au nombre minimal de tâches possible.
- Et en ajustant la taille du cluster au nombre minimum de nœuds nécessaires, en en ajoutant dynamiquement pour répondre à la demande.

![](Aspose.Words.71968ec4-cb76-4c34-b13b-d7e85bbcac39.041.png)

Le modèle de workflow Dataproc est un fichier YAML qui est traité à l'aide d'un graphe acyclique orienté (DAG).

Il peut :

- créer un nouveau cluster,
- sélectionner un cluster existant,
- soumettre des tâches (jobs),
- attendre que les dépendances soient terminées avant de soumettre les tâches,
- et supprimer un cluster une fois la tâche terminée.

Actuellement, il est uniquement accessible via la commande gcloud et l'API REST. Il n'est pas possible d'y accéder via la console Cloud.

Le modèle de workflow devient actif lorsqu'il est instancié dans le DAG. Le modèle peut être soumis plusieurs fois avec différentes valeurs de paramètres. Vous pouvez également écrire un modèle en ligne dans la commande gcloud, et vous pouvez répertorier les workflows et les métadonnées des workflows pour aider à diagnostiquer les problèmes.

![](Aspose.Words.71968ec4-cb76-4c34-b13b-d7e85bbcac39.042.png)

![](Aspose.Words.71968ec4-cb76-4c34-b13b-d7e85bbcac39.043.png)

Tout d'abord, nous récupérons toutes les choses qui doivent être installées dans le cluster à l'aide de nos scripts de démarrage et en affichant manuellement les commandes d'installation de pip, comme celle-ci, pour installer matplotlib. Vous pouvez exécuter plusieurs scripts de démarrage shell comme vous le voyez dans cet exemple.

![](Aspose.Words.71968ec4-cb76-4c34-b13b-d7e85bbcac39.044.png)

Ensuite, nous utilisons la commande gcloud pour créer un nouveau cluster avant d'exécuter notre tâche. Nous spécifions les paramètres du cluster tels que le modèle à utiliser dans notre architecture souhaitée, ainsi que les types de machines et les versions d'image que nous souhaitons pour le matériel et le logiciel.

![](Aspose.Words.71968ec4-cb76-4c34-b13b-d7e85bbcac39.045.png)

Après cela, nous devons ajouter une tâche au cluster nouvellement créé. Dans cet exemple, nous avons une tâche Spark écrite en Python qui se trouve dans un compartiment Cloud Storage que nous contrôlons.

![](Aspose.Words.71968ec4-cb76-4c34-b13b-d7e85bbcac39.046.png)

Enfin, nous devons soumettre ce modèle lui-même en tant que nouveau modèle de workflow, comme vous pouvez le voir avec la dernière commande.

![](Aspose.Words.71968ec4-cb76-4c34-b13b-d7e85bbcac39.047.png)

Dataproc autoscaling fournit des clusters qui ajustent leur taille en fonction des besoins de l'entreprise. Les principales fonctionnalités comprennent :

- Les tâches sont lancées sans intervention manuelle.
- Il n'est pas nécessaire d'intervenir manuellement lorsque le cluster est en surcapacité ou sous-capacité.
- Vous pouvez choisir entre des travailleurs standard et préemptibles,
- Vous pouvez économiser des ressources (quotas et coûts) à tout moment.

Les politiques d'autoscaling permettent un contrôle précis. Cela est basé sur la différence entre la mémoire YARN en attente et la mémoire disponible. Si davantage de mémoire est nécessaire, vous augmentez la taille. S'il y a un excès de mémoire, vous diminuez la taille. Respectez les limites de la machine virtuelle et ajustez la taille en fonction du facteur d'échelle.

sur le facteur d'échelle.

![](Aspose.Words.71968ec4-cb76-4c34-b13b-d7e85bbcac39.048.png)

Les améliorations de l'autoscaling peuvent être résumées comme suit :

- Des contrôles encore plus précis. Les politiques d'autoscaling peuvent être mises à jour ou supprimées à tout moment, l'intervalle de mise à l'échelle minimale a été réduit de 10 minutes à 2 minutes, et les politiques d'autoscaling peuvent être partagées entre plusieurs clusters.
- L'autoscaling est maintenant plus facile à comprendre. Les tableaux de bord YARN et HDFS peuvent être consultés sur une page dans le cluster, et l'historique des décisions d'autoscaling est disponible dans Cloud Logging.
- Et la stabilité des tâches est assurée grâce à la possibilité de mettre à l'échelle des tâches MapReduce et Spark sans perdre de progrès.

![](Aspose.Words.71968ec4-cb76-4c34-b13b-d7e85bbcac39.049.png)Dataproc autoscaling offre une capacité flexible pour une utilisation plus efficace, prenant des décisions de mise à l'échelle en fonction des métriques de Hadoop YARN. Il est conçu pour être utilisé uniquement avec des données persistantes en dehors du cluster, et non avec HDFS ou HBase sur le cluster lui-même. Il fonctionne mieux avec un cluster qui traite de nombreux travaux ou un seul travail volumineux. Il ne prend pas en charge Spark Structured Streaming, un service de streaming construit sur Spark SQL. Il n'est pas non plus conçu pour une mise à l'échelle à zéro. Par conséquent, il n'est pas idéal pour les clusters peu utilisés ou inactifs. Dans ces cas, il est tout aussi rapide de terminer un cluster inactif et de créer un nouveau cluster lorsque cela est nécessaire. À cette fin, vous pouvez envisager d'utiliser Dataproc Workflows ou Cloud Composer, ainsi que la suppression planifiée de clusters.

![](Aspose.Words.71968ec4-cb76-4c34-b13b-d7e85bbcac39.050.png)

Lorsque vous travaillez avec l'autoscaling dans le contexte de GCP, l'une des choses à prendre en compte est la configuration des travailleurs initiaux. Le nombre de travailleurs initiaux est défini à partir du nombre minimum de nœuds de travailleurs. En définissant cette valeur, vous garantissez que le cluster atteindra plus rapidement une capacité de base par rapport à si vous laissiez l'autoscaling s'en occuper. En effet, l'autoscaling pourrait nécessiter plusieurs périodes d'autoscaling pour se mettre à l'échelle.

Le nombre minimum de travailleurs peut être le même que le nombre minimum de nœuds du cluster. Il existe également une limite maximale qui fixe le nombre maximum de nœuds de travailleurs.

Si une charge importante est détectée sur le cluster, l'autoscaling décide qu'il est temps de l'augmenter. Le paramètre scale\_up.factor détermine combien de nœuds lancer. Par défaut, il s'agit généralement d'un seul nœud. Cependant, si vous savez qu'une forte demande va se produire simultanément, vous pouvez souhaiter augmenter l'échelle plus rapidement.

Après l'action, il y a une période de refroidissement pour permettre aux choses de se stabiliser avant que l'évaluation de l'autoscaling ne se produise à nouveau. Cette période de refroidissement réduit les chances que le cluster démarre et termine des nœuds en même temps.

Dans cet exemple, la capacité supplémentaire n'est pas nécessaire. De plus, il existe un délai de désactivation en douceur pour permettre aux tâches en cours de s'exécuter avant que le nœud ne soit mis hors service.

Remarquez qu'il y a un facteur de réduction d'échelle. Dans ce cas, la réduction se fait d'un nœud à la fois pour une diminution de capacité plus progressive.

Après l'action, il y a une autre période de refroidissement.

Enfin, une deuxième réduction d'échelle se produit, ramenant le nombre de travailleurs au minimum. Un paramètre secondaire, min\_workers et max\_workers, contrôle l'échelle des travailleurs préemptibles.

![](Aspose.Words.71968ec4-cb76-4c34-b13b-d7e85bbcac39.051.png)

Dans Google Cloud, vous pouvez utiliser Cloud Logging et Cloud Monitoring pour afficher et personnaliser les journaux, ainsi que pour surveiller les tâches et les ressources. La meilleure façon de déterminer l'erreur qui a causé l'échec d'une tâche Spark est d'examiner la sortie du pilote et les journaux générés par les exécuteurs Spark.

Notez cependant que si vous soumettez une tâche Spark en vous connectant directement au nœud principal à l'aide de SSH, il n'est pas possible d'obtenir la sortie du pilote.

Vous pouvez récupérer la sortie du programme du pilote en utilisant la Console Cloud ou une commande gcloud. La sortie est également stockée dans le bucket Cloud Storage du cluster Dataproc.

Tous les autres journaux se trouvent dans des fichiers différents à l'intérieur des machines du cluster. Il est possible de voir les journaux de chaque conteneur à partir de l'interface utilisateur Web de l'application Spark (ou depuis le serveur d'historique une fois le programme terminé) dans l'onglet Executors. Vous devez parcourir chaque conteneur Spark pour afficher chaque journal. Si vous écrivez des journaux ou imprimez sur stdout ou stderr dans votre code d'application, les journaux sont enregistrés dans la redirection de stdout ou stderr.

Dans un cluster Dataproc, YARN est configuré par défaut pour collecter tous ces journaux, et ils sont disponibles dans Cloud Logging. Logging offre une vue consolidée et concise de tous les journaux afin que vous n'ayez pas à passer du temps à naviguer parmi les journaux des conteneurs pour trouver des erreurs.

Cette capture d'écran montre la page de journalisation dans la Console Cloud. Vous pouvez afficher tous les journaux de votre cluster Dataproc en sélectionnant le nom du cluster dans le menu sélecteur. N'oubliez pas d'élargir la durée dans le sélecteur de plage de temps.

Vous pouvez obtenir les journaux d'une application Spark en les filtrant par son ID. Vous pouvez obtenir l'ID de l'application à partir de la sortie du pilote.

![](Aspose.Words.71968ec4-cb76-4c34-b13b-d7e85bbcac39.052.png)

Pour trouver les journaux plus rapidement, vous pouvez créer et utiliser vos propres étiquettes pour chaque cluster ou chaque tâche Dataproc. Par exemple, vous pouvez créer une étiquette avec la clé "environment" ou "ENV", en lui attribuant la valeur "exploration" et l'utiliser pour votre tâche d'exploration de données. Vous pouvez ensuite obtenir les journaux de toutes les créations de tâches d'exploration en filtrant avec l'étiquette "environment" et la valeur "exploration" dans Logging. Notez que ce filtre ne renverra pas tous les journaux de cette tâche, seulement les journaux de création de ressource.

![](Aspose.Words.71968ec4-cb76-4c34-b13b-d7e85bbcac39.053.png)

Vous pouvez définir le niveau de journalisation du pilote en utilisant la commande gcloud suivante : gcloud dataproc

jobs submit hadoop, avec le paramètre driver-log-levels.

Vous pouvez définir le niveau de journalisation pour le reste de l'application à partir du contexte Spark. Par

exemple : spark.sparkContext.setLogLevel. Ici, nous prendrons simplement l'exemple du niveau DEBUG.

![](Aspose.Words.71968ec4-cb76-4c34-b13b-d7e85bbcac39.054.png)

Cloud Monitoring peut surveiller l'utilisation du CPU, du disque, du réseau et des ressources YARN du cluster. Vous pouvez créer un tableau de bord personnalisé pour obtenir des graphiques à jour pour ces métriques et d'autres. Dataproc s'exécute sur Compute Engine. Si vous souhaitez visualiser l'utilisation du CPU, les E/S du disque ou les métriques de réseau dans un graphique, vous devez sélectionner une instance de machine virtuelle Compute Engine en tant que type de ressource, puis filtrer par nom de cluster. Ce schéma montre un exemple de sortie.

Pour afficher les métriques des requêtes Spark, des emplois, des étapes ou des tâches, connectez-vous à l'interface Web de l'application Spark.

[Lab : Exécution des tâches Apache Spark sur Dataproc](https://www.cloudskillsboost.google/course_sessions/3764053/labs/379232)
