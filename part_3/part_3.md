Création d'un Data Warehouse

Nous commencerons par décrire ce qui constitue un entrepôt de données moderne. Nous parlerons également de ce qui distingue un lac de données d'un entrepôt de données d'entreprise. Ensuite, nous allons vous présenter BigQuery, une solution d'entrepôt de données sur Google Cloud. Une fois que vous serez familiarisé avec les bases de BigQuery, nous parlerons de la façon dont BigQuery organise vos données, ... et ensuite comment charger de nouvelles données dans BigQuery. Vous aurez également l'occasion de charger des données dans BigQuery grâce à un laboratoire pratique. Enfin, nous plongerons dans le monde des schémas d'entrepôt de données. Nous parlerons de la conception efficace des schémas d'entrepôt de données, ... et nous examinerons de plus près le support de BigQuery pour les champs imbriqués et répétés, et pourquoi ce type de conception de schéma est si populaire pour les entreprises. Vous aurez l'occasion de travailler avec des données JSON et ARRAY dans BigQuery grâce à un laboratoire pratique. Nous conclurons en discutant de la façon dont vous pouvez optimiser les tables de votre entrepôt de données avec le partitionnement et le regroupement.

Le Data Warehouse Moderne

![](Aspose.Words.5529591a-df34-4ff9-8fab-40a4fdf63547.001.png)

Un entrepôt de données d'entreprise devrait consolider les données provenant de nombreuses sources. Si vous vous souvenez du module précédent, un lac de données fait quelque chose de très similaire. La principale différence entre les deux réside dans le mot "consolider".

Un entrepôt de données impose un schéma. Un lac de données n'est que des données brutes, mais un entrepôt de données d'entreprise rassemble les données et les rend disponibles pour les requêtes et le traitement des données. Pour utiliser un entrepôt de données, un analyste doit connaître le schéma des données. Cependant, contrairement à un lac de données, l'analyste n'a pas besoin d'écrire de code pour lire et analyser les données.

Une autre raison de consolider toutes vos données, en plus de standardiser le format et de les rendre disponibles pour l'interrogation, est de vous assurer que les résultats de la requête soient significatifs. Vous voulez vous assurer que les données soient propres, précises et cohérentes.

Le but d'un entrepôt de données n'est pas de stocker des données. C'est le rôle d'un lac de données.

Si vous avez des données brutes que vous souhaitez conserver sans nécessairement les interroger, ne vous embêtez pas à les nettoyer et à les optimiser. Laissez-les dans un lac de données.

Toutes les données dans un entrepôt de données doivent être disponibles pour être interrogées. Il est important de s'assurer que ces requêtes sont rapides : vous ne voulez pas que les personnes attendent des heures, voire des jours pour obtenir des résultats.

![](Aspose.Words.5529591a-df34-4ff9-8fab-40a4fdf63547.002.png)

Nous avons décrit un entrepôt de données d'entreprise et comment il diffère d'un lac de données.

Qu'est-ce qui rend un entrepôt de données moderne ?

- Les besoins en données des entreprises continuent de croître. Vous voulez vous assurer que l'entrepôt de données peut gérer des ensembles de données qui ne rentrent pas en mémoire. Généralement, il s'agit de gigaoctets à téraoctets de données, mais parfois cela peut atteindre des pétaoctets. Vous ne voulez pas d'entrepôts séparés pour différents ensembles de données. Au lieu de cela, vous voulez un seul entrepôt de données qui puisse évoluer de gigaoctets à pétaoctets de données.
- Deuxièmement, vous voulez que l'entrepôt de données soit sans serveur et entièrement géré. Vous ne voulez pas être limité à des clusters que vous devez entretenir, ou à des index que vous devez ajuster finement. Le fait de supprimer ces responsabilités permettra aux analystes de données d'effectuer des requêtes ad hoc plus rapidement, ce qui est important car vous voulez que l'entrepôt de données accélère la prise de décision de votre entreprise.
- Ensuite, votre entrepôt de données n'est pas productif s'il vous permet d'effectuer des requêtes mais ne prend pas en charge la visualisation et les rapports détaillés. Idéalement, votre entrepôt de données peut s'intégrer parfaitement à l'outil de visualisation ou de reporting que votre entreprise connaît le mieux.
- De même, étant donné que l'entrepôt de données nécessite des données propres et cohérentes, vous devrez souvent construire des pipelines de données pour amener les données dans l'entrepôt. L'entrepôt de données moderne doit pouvoir s'intégrer à un écosystème d'outils de traitement pour la construction de pipelines ETL.
- Votre pipeline de données doit être capable de rafraîchir en permanence les données dans l'entrepôt afin de les maintenir à jour. Vous devez être capable de diffuser des données dans l'entrepôt et ne pas dépendre de mises à jour par lots.
- De plus, l'analyse prédictive devient de plus en plus importante pour les analystes de données. Par conséquent, un entrepôt de données moderne doit prendre en charge l'apprentissage automatique sans déplacer les données hors de l'entrepôt.
- Enfin, dans un entrepôt de données moderne, il devrait être possible d'imposer des mesures de sécurité de qualité entreprise telles que des contraintes d'exfiltration de données. Il devrait également être possible de partager des données et des requêtes avec des collaborateurs.

Introduction à BigQuery

![](Aspose.Words.5529591a-df34-4ff9-8fab-40a4fdf63547.003.png)

BigQuery dispose de nombreuses fonctionnalités qui en font un entrepôt de données idéal. Lorsque nous parlons d'un entrepôt de données moderne, nous parlons de la capacité de l'entrepôt à évoluer de quelques gigaoctets à plusieurs pétaoctets de manière transparente. Nous parlons de la possibilité d'effectuer des requêtes ad hoc et des opérations sans opérations (no-ops). BigQuery gère efficacement et à moindre coût des ensembles de données volumineux à l'échelle du pétaoctet, tant pour le stockage que pour les requêtes. En fait, cela est similaire au coût du stockage Cloud. Cela vous permet de stocker vos données sans avoir à vous soucier d'archiver les données plus anciennes pour économiser de l'espace de stockage. Contrairement aux entrepôts de données traditionnels, BigQuery dispose de fonctionnalités intégrées telles que les systèmes d'information géographique (GIS) et l'apprentissage automatique (machine learning). Il permet également de diffuser en continu les données, vous permettant ainsi d'analyser vos données en temps quasi réel. Étant donné qu'il fait partie de Google Cloud, vous bénéficiez de tous les avantages en matière de sécurité fournis par le cloud, tout en pouvant également partager des ensembles de données et des requêtes. BigQuery prend en charge les requêtes SQL standard et est compatible avec ANSI SQL 2011.

![](Aspose.Words.5529591a-df34-4ff9-8fab-40a4fdf63547.004.png)

BigQuery est un service géré entièrement sans serveur, ce qui signifie que l'équipe d'ingénierie de BigQuery se charge des mises à jour et de la maintenance pour vous. Les mises à niveau ne nécessitent pas d'interruption de service et n'affectent pas les performances du système.

Par exemple, la gestion du vieillissement des données et de leur expiration peut être une opération fastidieuse dans les entrepôts de données traditionnels. Dans BigQuery, il vous suffit de spécifier un indicateur d'expiration de table lors de la création de la table ou de mettre à jour une table pour ajouter cette fonctionnalité. La table expirera automatiquement lorsqu'elle atteindra cet âge ou cette durée.

De nombreux systèmes traditionnels nécessitent des processus de vidange intensifs en ressources, exécutés à intervalles réguliers, pour réorganiser et trier les blocs de données et récupérer de l'espace. BigQuery n'a pas d'équivalent du processus de vidange, car le moteur de stockage gère en continu et optimise la façon dont les données sont stockées et répliquées. De plus, comme BigQuery n'utilise pas d'index sur les tables, vous n'avez pas besoin de les reconstruire.

En résumé, vous pouvez libérer des heures de travail réelles en vous libérant des tâches courantes de gestion de base de données.

![](Aspose.Words.5529591a-df34-4ff9-8fab-40a4fdf63547.005.png)

Qu'est-ce qui rend BigQuery rapide ? Les tables BigQuery sont orientées colonne, contrairement aux tables RDBM traditionnelles qui sont orientées ligne.

![](Aspose.Words.5529591a-df34-4ff9-8fab-40a4fdf63547.006.png)

Les tables orientées par lignes sont efficaces pour effectuer des mises à jour sur les données contenues dans les champs. Pour les systèmes OLTP (traitement en ligne des transactions), les tables orientées par lignes sont nécessaires car ces systèmes effectuent fréquemment des mises à jour. Cependant, les opérations analytiques sont lentes sur les tables orientées par lignes car elles doivent lire tous les champs d'une ligne et, selon le type d'indexation ou de clé, elles peuvent devoir lire des lignes et des champs supplémentaires pour trouver les informations demandées dans une requête.

![](Aspose.Words.5529591a-df34-4ff9-8fab-40a4fdf63547.007.png)

BigQuery, cependant, est un système O-LAP. Il est conçu pour l'analyse. Les tables BigQuery sont immuables et sont optimisées pour la lecture et l'ajout de données. Les tables BigQuery ne sont pas optimisées pour les mises à jour.

BigQuery exploite le fait que la plupart des requêtes impliquent peu de colonnes, et donc il ne lit que les colonnes nécessaires à la requête. BigQuery est très efficace à cet égard et c'est la raison pour laquelle les tables sont orientées colonnes.

![](Aspose.Words.5529591a-df34-4ff9-8fab-40a4fdf63547.008.png)

BigQuery est mis en œuvre en deux parties : un moteur de stockage et un moteur analytique, comme illustré. La séparation du calcul et du stockage est un thème courant dans Google Cloud et fonctionne efficacement grâce à Jupiter, le réseau pétabit de Google. Jupiter permet une communication ultrarapide entre le calcul et le stockage. Les données de BigQuery sont physiquement stockées sur le système de fichiers distribué de Google, appelé Colossus, qui garantit la durabilité en utilisant un codage d'effacement pour stocker des morceaux redondants des données sur plusieurs disques physiques. De plus, les données sont répliquées sur plusieurs centres de données.

![](Aspose.Words.5529591a-df34-4ff9-8fab-40a4fdf63547.009.png)

Voici quelques-unes des optimisations effectuées par Capacitor. Capacitor effectue une compression par codage de longueur sur les données afin de réduire la quantité de données à lire. Il réordonne également les données pour les rendre plus propices à la compression par codage de longueur. Le réordonnancement des données est également appelé codage par dictionnaire.

Tout cela se produit "sous le capot" dans le stockage natif de BigQuery. Cela ne vous affecte en aucune façon. C'est tout l'intérêt d'une solution sans serveur et entièrement gérée.

![](Aspose.Words.5529591a-df34-4ff9-8fab-40a4fdf63547.010.png)

Vous n'avez pas besoin de provisionner des ressources avant d'utiliser BigQuery, contrairement à de nombreux systèmes de gestion de bases de données relationnelles. BigQuery alloue dynamiquement les ressources de stockage et de requête en fonction de vos schémas d'utilisation.

Les ressources de stockage sont allouées au fur et à mesure de votre consommation et libérées lorsque vous supprimez des données ou supprimez des tables.

Les ressources de requête sont allouées en fonction du type et de la complexité de la requête. Chaque requête utilise un certain nombre de slots, qui sont des unités de calcul comprenant une certaine quantité de CPU et de RAM.

Vous n'êtes pas obligé de vous engager à une utilisation minimale pour utiliser BigQuery. Le service alloue et facture les ressources en fonction de votre utilisation réelle. Par défaut, tous les clients de BigQuery ont accès à 2 000 slots pour les opérations de requête. Vous pouvez également réserver un nombre fixe de slots pour votre projet.

![](Aspose.Words.5529591a-df34-4ff9-8fab-40a4fdf63547.011.png)

BigQuery est mis en œuvre en utilisant une architecture microservices, ce qui signifie qu'il n'y a pas de machines virtuelles à configurer et à maintenir. En interne, le débit analytique est mesuré en termes de "slots" BigQuery. Un slot BigQuery représente une unité de capacité de calcul nécessaire pour exécuter des requêtes SQL. BigQuery calcule automatiquement le nombre de slots nécessaires à chaque étape d'une requête, en fonction de sa taille et de sa complexité.

Un slot BigQuery est une combinaison de ressources CPU, mémoire et réseau. Il inclut également plusieurs technologies et sous-services de soutien. Il est à noter que chaque slot n'a pas nécessairement les mêmes spécifications pendant l'exécution d'une requête. Certains slots peuvent avoir plus de mémoire, plus de CPU ou plus d'E/S que d'autres.

![](Aspose.Words.5529591a-df34-4ff9-8fab-40a4fdf63547.012.png)

Par défaut, chaque compte dispose d'une limite de quota de 2000 slots BigQuery pour les requêtes à la demande. Un modèle de tarification à taux fixe est disponible, offrant des slots réservés pour les clients souhaitant une tarification plus prévisible.

Si une seule requête simple est soumise et nécessite moins de slots que ceux disponibles, la requête s'exécutera généralement plus rapidement.

Si vous avez réservé 10 000 slots, mais que vous avez 30 requêtes simultanées qui demandent ensemble 15 000 slots, les requêtes n'obtiendront pas tous les slots nécessaires. Au lieu de cela, les slots sont répartis équitablement entre tous les projets de la réservation et toutes les requêtes du projet. Cela se traduira généralement par une exécution plus lente de chaque requête.

Commencez avec BigQuery

![](Aspose.Words.5529591a-df34-4ff9-8fab-40a4fdf63547.013.png)

BigQuery organise les tables de données en ensembles appelés "datasets". Ces datasets sont associés à votre projet Google Cloud. Lorsque vous faites référence à une table à partir de la ligne de commande dans des requêtes SQL ou dans du code, vous vous y référez en utilisant la structure suivante : projet.dataset.table.

![](Aspose.Words.5529591a-df34-4ff9-8fab-40a4fdf63547.014.png)

Quelles sont les raisons de structurer vos informations en ensembles de données, projets et tables ? Ces différents niveaux de portée - projet, ensemble de données et table - peuvent vous aider à structurer vos informations de manière logique. Vous pouvez utiliser plusieurs ensembles de données pour séparer les tables relatives à différents domaines analytiques, et vous pouvez utiliser la portée au niveau du projet pour isoler les ensembles de données les uns des autres en fonction de vos besoins commerciaux.

De plus, comme nous le verrons plus tard, vous pouvez associer les projets à la facturation et utiliser les ensembles de données pour le contrôle d'accès. Vous stockez les données dans des tables distinctes en fonction de considérations de schéma logique.

![](Aspose.Words.5529591a-df34-4ff9-8fab-40a4fdf63547.015.png)

Le projet est associé à la facturation. Par exemple, si vous interrogez une table qui appartient au projet `bigquery-public-data`, les coûts de stockage sont facturés à ce projet de données.

Pour exécuter une requête, vous devez être connecté à la Console Cloud. Vous exécuterez une requête dans votre propre projet Google Cloud et les frais de requête seront facturés à votre projet, et non au projet de données public.

Pour exécuter une requête dans un projet, vous avez besoin des autorisations de gestion d'accès aux identités (IAM) pour soumettre une tâche. N'oubliez pas que l'exécution d'une requête signifie que vous devez être en mesure de soumettre une tâche de requête au service.

![](Aspose.Words.5529591a-df34-4ff9-8fab-40a4fdf63547.016.png)

Le contrôle d'accès est géré via IAM (Identity and Access Management) et se fait au niveau du jeu de données, de la table/vue ou de la colonne. Pour pouvoir interroger des données dans une table ou une vue, vous avez besoin d'au moins des permissions de lecture sur la table ou la vue.

![](Aspose.Words.5529591a-df34-4ff9-8fab-40a4fdf63547.017.png)

Comme Cloud Storage, les jeux de données de BigQuery peuvent être régionaux ou multi-régionaux. Les jeux de données régionaux sont répliqués dans plusieurs zones de la région. Multi-régional signifie une réplication entre plusieurs régions.

![](Aspose.Words.5529591a-df34-4ff9-8fab-40a4fdf63547.018.png)

Chaque table possède un schéma. Vous pouvez entrer le schéma manuellement via la Console Cloud ou en fournissant un fichier JSON.

![](Aspose.Words.5529591a-df34-4ff9-8fab-40a4fdf63547.019.png)

Gestion des clés

Comme pour Cloud Storage, le stockage de BigQuery chiffre les données au repos et sur le réseau à l'aide de clés de chiffrement gérées par Google. Il est également possible d'utiliser des clés de chiffrement gérées par le client.

Authentification

L'authentification se fait via IAM, il est donc possible d'utiliser des adresses Gmail ou des comptes Google Workspace pour cette tâche.

Contrôle d'accès

Le contrôle d'accès se fait via les rôles IAM et implique l'octroi de permissions. Nous avons discuté de deux d'entre elles : l'accès en lecture et la possibilité de soumettre des tâches de requête. Cependant, de nombreuses autres permissions sont possibles. Rappelez-vous que le contrôle d'accès s'applique au niveau des jeux de données, des tables, des vues ou des colonnes. Lorsque vous accordez l'accès à un jeu de données, en lecture ou en écriture, vous accordez l'accès à toutes les tables de ce jeu de données.

Cloud Audit Logs

Les journaux dans BigQuery sont immuables et peuvent être exportés vers Cloud Operations. Toutes les activités administratives et les événements système sont enregistrés. Un exemple d'événement système est l'expiration d'une table. Si, lors de la création d'une table, vous la configurez pour expirer dans 30 jours, à la fin de ces 30 jours, un événement système sera généré et enregistré. Vous obtiendrez également des journaux immuables de chaque accès qui se produit dans un jeu de données sous votre projet.

![](Aspose.Words.5529591a-df34-4ff9-8fab-40a4fdf63547.020.png)

BigQuery propose des rôles prédéfinis pour contrôler l'accès aux ressources. Vous pouvez également créer des rôles personnalisés IAM comprenant votre ensemble défini de permissions, puis attribuer ces rôles à des utilisateurs ou des groupes. Vous pouvez attribuer un rôle à une adresse e-mail Google ou à un groupe Google Workspace.

Un aspect important de l'exploitation d'un entrepôt de données est de permettre un accès partagé mais contrôlé aux mêmes données pour différents groupes d'utilisateurs. Par exemple, les départements des finances, des ressources humaines et du marketing accèdent tous aux mêmes tables, mais leurs niveaux d'accès diffèrent. Les outils traditionnels d'entreposage de données rendent cela possible en appliquant une sécurité au niveau des lignes. Vous pouvez obtenir les mêmes résultats dans BigQuery grâce au contrôle d'accès aux ensembles de données, tables, vues ou colonnes, ou en définissant des vues autorisées et des autorisations au niveau des lignes.

![](Aspose.Words.5529591a-df34-4ff9-8fab-40a4fdf63547.021.png)

Dans BigQuery, la sécurité au niveau des lignes implique la création de politiques d'accès au niveau des lignes sur une table BigQuery cible. Cette politique agit ensuite comme un filtre pour masquer ou afficher certaines lignes de données, en fonction de la présence d'un utilisateur ou d'un groupe dans une liste autorisée.

Un utilisateur autorisé, ayant les rôles IAM BigQuery Admin ou BigQuery DataOwner, peut créer des politiques d'accès au niveau des lignes sur une table BigQuery.

Lorsque vous créez une politique d'accès au niveau des lignes, vous spécifiez le nom de la table et les utilisateurs ou groupes (appelés la liste des bénéficiaires) qui doivent avoir accès à certaines données de lignes. La politique inclut les données que vous souhaitez filtrer, appelées la filter\_expression. La filter\_expression fonctionne comme une clause WHERE dans une requête typique.

Dans cet exemple, les utilisateurs du groupe :apac ne peuvent voir que les partenaires de la région APAC.

![](Aspose.Words.5529591a-df34-4ff9-8fab-40a4fdf63547.022.png)

Accorder l'accès en lecture à un ensemble de données est également connu sous le nom de création d'une vue autorisée dans BigQuery. Une vue autorisée vous permet de partager les résultats d'une requête avec des utilisateurs et des groupes spécifiques sans leur donner accès aux données sources sous-jacentes.

<https://cloud.google.com/bigquery/docs/authorized-views>

![](Aspose.Words.5529591a-df34-4ff9-8fab-40a4fdf63547.023.png)

Vous pouvez également utiliser la requête SQL de la vue pour limiter les colonnes (champs) que les utilisateurs peuvent interroger.

![](Aspose.Words.5529591a-df34-4ff9-8fab-40a4fdf63547.024.png)

Le partage d'accès aux ensembles de données est facile.

Traditionnellement, l'intégration de nouveaux analystes de données nécessitait un délai important. Pour permettre aux analystes d'exécuter des requêtes simples, vous deviez leur montrer où se trouvent les sources de données, configurer des connexions ODBC, des outils et des droits d'accès. En utilisant Google Cloud, vous pouvez grandement accélérer le temps de productivité d'un analyste.

Pour intégrer un analyste sur Google Cloud, vous lui accordez l'accès aux projet(s) pertinents, vous le familiarisez avec la console Cloud et l'interface utilisateur Web BigQuery, et vous partagez quelques requêtes pour l'aider à se familiariser avec les données.

La console Cloud offre une vue centralisée de tous les actifs de votre environnement Google Cloud. L'actif le plus pertinent pour les analystes de données pourrait être les compartiments Cloud Storage, où ils peuvent collaborer sur des fichiers.

L'interface utilisateur Web BigQuery présente la liste des ensembles de données auxquels l'analyste a accès. Les analystes peuvent effectuer des tâches dans la console Cloud en fonction du rôle que vous leur attribuez, telles que la visualisation des métadonnées, la prévisualisation des données, l'exécution, l'enregistrement et le partage des requêtes.

![](Aspose.Words.5529591a-df34-4ff9-8fab-40a4fdf63547.025.png)

Lorsque vous accordez un accès en lecture à un jeu de données à un utilisateur dans le contexte de GCP (Google Cloud Platform), chaque table de ce jeu de données devient lisible par cet utilisateur.

Mais que faire si vous souhaitez avoir un contrôle plus précis ? En plus des contrôles d'accès au niveau de la table ou de la colonne, vous pouvez utiliser des vues. Dans cet exemple, nous créons une vue dans le jeu de données B, et cette vue est un sous-ensemble des données de la table du jeu de données A. En donnant aux utilisateurs l'accès au jeu de données B, nous créons une vue autorisée qui ne représente qu'une partie des données originales. Notez que vous ne pouvez pas exporter les données d'une vue, et le jeu de données B doit être dans la même région ou multi-région que le jeu de données A.

Une vue est une requête SQL qui ressemble à une table et possède des propriétés similaires. Vous pouvez interroger une vue de la même manière que vous interrogez une table. BigQuery prend également en charge les vues matérialisées. Ce sont des vues persistantes qui évitent de consulter la table à chaque utilisation de la vue. BigQuery maintiendra la vue matérialisée actualisée avec le contenu de la table source.

![](Aspose.Words.5529591a-df34-4ff9-8fab-40a4fdf63547.026.png)

Dans BigQuery, les vues matérialisées mettent périodiquement en cache les résultats d'une requête pour augmenter les performances et l'efficacité. BigQuery exploite les résultats précalculés des vues matérialisées et, lorsque cela est possible, ne lit que les modifications delta de la table de base pour calculer des résultats à jour. Les vues matérialisées peuvent être interrogées directement ou utilisées par l'optimiseur BigQuery pour traiter les requêtes sur les tables de base. Les requêtes utilisant des vues matérialisées sont généralement plus rapides et consomment moins de ressources que les requêtes qui récupèrent les mêmes données uniquement à partir de la table de base. Les vues matérialisées peuvent considérablement améliorer les performances des charges de travail présentant la caractéristique de requêtes courantes et répétées.

<https://cloud.google.com/bigquery/docs/materialized-views-intro>

![](Aspose.Words.5529591a-df34-4ff9-8fab-40a4fdf63547.027.png)

Dans les requêtes que nous avons vues précédemment, nous avons rédigé la requête en SQL et sélectionné "Exécuter" dans l'interface utilisateur (UI).

Ce que cela a fait, c'est soumettre un QueryJob au service BigQuery.

Le service de requête BigQuery est séparé du service de stockage BigQuery. Cependant, ils sont conçus pour collaborer et être utilisés ensemble. Dans ce cas, nous interrogeons des tables natives dans le projet bigquery-public-data. Interroger des tables natives est le cas le plus courant et le moyen le plus performant d'utiliser BigQuery.

BigQuery est le plus efficace lorsqu'il travaille avec des données contenues dans son propre service de stockage. Le service de stockage et le service de requête collaborent pour organiser les données en interne afin de rendre les requêtes efficaces sur des ensembles de données énormes de téraoctets et de pétaoctets.

Le service de requête peut également exécuter des jobs de requête sur des données contenues dans d'autres emplacements, tels que des tables dans des fichiers CSV hébergés dans Cloud Storage.

Ainsi, vous pouvez interroger des données dans des tables externes ou provenant de sources externes sans les charger dans BigQuery. On appelle cela des requêtes fédérées.

Dans les deux cas, le service de requête place les résultats dans une table temporaire et l'interface utilisateur récupère et affiche les données dans cette table temporaire. Cette table temporaire est conservée pendant 24 heures. Donc, si vous exécutez exactement la même requête à nouveau et que les résultats ne seraient pas différents, BigQuery renverra simplement un pointeur vers les résultats mis en cache. Les requêtes qui peuvent être servies à partir du cache ne génèrent aucun frais.

Il est également possible de demander au job de requête d'écrire dans une table de destination. Dans ce cas, vous pouvez contrôler quand la table est supprimée. Étant donné que la table de destination est permanente et non temporaire, vous serez facturé pour le stockage des résultats.

![](Aspose.Words.5529591a-df34-4ff9-8fab-40a4fdf63547.028.png)Pour calculer les tarifs, vous pouvez utiliser le validateur de requêtes de BigQuery en combinaison avec le calculateur de tarifs pour obtenir des estimations.

Le validateur de requêtes fournit une estimation de la taille des données qui seront traitées lors d'une requête. Vous pouvez utiliser cette estimation dans le calculateur pour obtenir une estimation du coût de l'exécution de la requête.

Ceci est valable si vous utilisez un plan à la demande où vous payez pour chaque requête en fonction de la quantité de données traitées par cette requête. Votre entreprise pourrait avoir opté pour un plan tarifaire fixe. Dans ce cas, votre entreprise paiera un prix fixe et le coût dépendra donc du nombre de slots utilisés par votre requête.

![](Aspose.Words.5529591a-df34-4ff9-8fab-40a4fdf63547.029.png)

Vous pouvez séparer le coût du stockage et le coût des requêtes.

En séparant les projets A et B, il est possible de partager des données sans accorder l'accès à l'exécution des tâches. Sur ce schéma, les Utilisateurs 1 et 2 ont accès à l'exécution des tâches et aux ensembles de données dans leurs propres projets respectifs. Si ils exécutent une requête, cette tâche est facturée à leur propre projet.

Que se passe-t-il si l'Utilisateur 1 a besoin de pouvoir accéder à l'ensemble de données D dans le Projet B ? La personne qui possède le Projet B peut autoriser l'Utilisateur 1 à interroger l'ensemble de données D du Projet B et les frais seront facturés au Projet A lorsqu'ils sont exécutés à partir du Projet A.

Le propriétaire du projet de l'ensemble de données public a accordé à tous les utilisateurs authentifiés l'accès à l'utilisation de leurs données. Le paramètre spécial "allAuthenticatedUsers" rend un ensemble de données public. Les utilisateurs authentifiés doivent utiliser BigQuery dans leur propre projet et avoir accès à l'exécution des tâches BigQuery afin de pouvoir interroger l'ensemble de données public. La facturation de la requête est affectée à leur projet, même si la requête utilise des données publiques ou partagées.

En résumé, le coût d'une requête est toujours attribué au projet actif à partir duquel la requête est exécutée. Le projet actif d'un utilisateur est affiché en haut de la console Cloud ou défini par une variable d'environnement dans le Cloud Shell ou les outils clients.

NOTE : BigQuery offre 1 To de requêtes gratuites chaque mois, donc les ensembles de données publics sont un moyen facile d'essayer BigQuery.

Charger des données dans BigQuery

![](Aspose.Words.5529591a-df34-4ff9-8fab-40a4fdf63547.030.png)

Rappelons-nous d'un module précédent que la méthode que vous utilisez pour charger les données dépend de la quantité de transformation nécessaire.

- E-L, ou Extract and Load, est utilisé lorsque les données sont importées telles quelles, où la source et la cible ont le même schéma.
- E-L-T, ou Extract, Load, Transform, est utilisé lorsque les données brutes seront chargées directement dans la cible et transformées là-bas.
- E-T-L, ou Extract, Transform, Load, est utilisé lorsque la transformation se produit dans un service intermédiaire avant d'être chargée dans la cible.

![](Aspose.Words.5529591a-df34-4ff9-8fab-40a4fdf63547.031.png)

Vous pourriez dire que le cas le plus simple est E-L. Si les données sont utilisables dans leur forme originale, il n'est pas nécessaire de les transformer. Il suffit de les charger.

![](Aspose.Words.5529591a-df34-4ff9-8fab-40a4fdf63547.032.png)

Vous pouvez charger des données en mode batch dans BigQuery. En plus du format CSV, vous pouvez également utiliser des fichiers de données avec des délimiteurs autres que des virgules en utilisant l'indicateur "field\_delimiter". BigQuery prend en charge le chargement de fichiers compressés au format gzip. Cependant, le chargement de fichiers compressés n'est pas aussi rapide que le chargement de fichiers non compressés. Pour les scénarios sensibles au temps ou les scénarios dans lesquels le transfert de fichiers non compressés vers Cloud Storage est limité par la bande passante ou le temps, effectuez un test de chargement rapide pour voir quelle alternative fonctionne le mieux. Étant donné que les tâches de chargement sont asynchrones, vous n'avez pas besoin de maintenir une connexion client pendant l'exécution de la tâche. Plus important encore, les tâches de chargement n'affectent pas vos autres ressources BigQuery.

Une tâche de chargement crée une table de destination si elle n'existe pas déjà. BigQuery détermine le schéma des données de la manière suivante :

- Si vos données sont au format Avro, qui est auto-descriptif, BigQuery peut déterminer le schéma directement.
- Si les données sont au format JSON ou CSV, BigQuery peut détecter automatiquement le schéma, mais une vérification manuelle est recommandée.

Vous pouvez spécifier un schéma explicitement en passant le schéma en argument de la tâche de chargement. Les tâches de chargement en cours peuvent ajouter des données à la même table en utilisant la même procédure que pour le chargement initial, mais elles ne nécessitent pas que le schéma soit passé à chaque tâche.

Si vos fichiers CSV contiennent toujours une ligne d'en-tête qui doit être ignorée après le chargement initial et la création de la table, vous pouvez utiliser l'indicateur "skip\_leading\_rows" pour ignorer la ligne. Pour plus de détails, consultez la documentation sur les indicateurs de chargement de BigQuery.

BigQuery fixe des limites quotidiennes sur le nombre et la taille des tâches de chargement que vous pouvez effectuer par projet et par table. De plus, BigQuery fixe des limites sur les tailles des fichiers de chargement individuels et des enregistrements. Vous pouvez lancer des tâches de chargement via l'interface utilisateur web de BigQuery. Pour automatiser le processus, vous pouvez configurer des fonctions Cloud pour écouter un événement de Cloud Storage associé à l'arrivée de nouveaux fichiers dans un compartiment donné et lancer une tâche de chargement BigQuery.

![](Aspose.Words.5529591a-df34-4ff9-8fab-40a4fdf63547.033.png)

BigQuery peut importer des données stockées au format JSON, à condition qu'elles soient délimitées par des sauts de ligne. Il peut également importer des fichiers aux formats Avro, Parquet et ORC. L'importation la plus courante se fait avec des fichiers CSV, qui servent de pont entre BigQuery et les feuilles de calcul.

BigQuery peut également importer directement des fichiers d'exportation Firestore et Datastore.

Une autre façon pour BigQuery d'importer des données est via l'API. Fondamentalement, n'importe quel endroit où vous pouvez exécuter du code peut théoriquement insérer des données dans les tables BigQuery. Vous pouvez utiliser l'API à partir d'une instance Compute Engine, d'un conteneur sur Kubernetes, d'App Engine ou de Cloud Functions. Cependant, dans ces cas, vous devriez recréer les fondations du traitement des données. En pratique, l'API est principalement utilisée à partir de Dataproc ou de Dataflow.

Le service BigQuery Data Transfer fournit des connecteurs et des tâches de chargement préconstruites pour BigQuery, qui effectuent les transformations nécessaires pour charger les données de rapport à partir de différents services directement dans BigQuery.

![](Aspose.Words.5529591a-df34-4ff9-8fab-40a4fdf63547.034.png)

Google Cloud Storage peut être utile dans le processus E-L. Vous pouvez transférer des fichiers vers Cloud Storage dans le schéma qui est natif au stockage de données sur site existant, puis charger ces fichiers dans BigQuery.

![](Aspose.Words.5529591a-df34-4ff9-8fab-40a4fdf63547.035.png)

Il est courant de procéder à l'automatisation de l'exécution de requêtes en fonction d'un planning ou d'un événement, et de mettre en cache les résultats pour une consultation ultérieure.

Vous pouvez planifier l'exécution de requêtes de manière récurrente. Les requêtes planifiées doivent être rédigées en SQL standard, ce qui peut inclure des instructions de langage de définition de données (DDL) et de langage de manipulation de données (DML). La chaîne de requête et la table de destination peuvent être paramétrées, ce qui vous permet d'organiser les résultats de la requête en fonction de la date et de l'heure.

<https://cloud.google.com/bigquery/docs/scheduling-queries>

![](Aspose.Words.5529591a-df34-4ff9-8fab-40a4fdf63547.036.png)

- En conservant un historique complet des modifications de vos tables sur une période de 7 jours, BigQuery vous permet d'interroger une capture instantanée de vos données à un moment donné. Vous pouvez facilement annuler les modifications sans avoir à demander une récupération à partir des sauvegardes. Cette diapositive montre comment effectuer une requête SELECT pour interroger la table telle qu'elle était il y a 24 heures. Étant donné qu'il s'agit d'une requête SELECT, vous pouvez faire plus que simplement restaurer une table. Vous pouvez effectuer une jointure avec une autre table ou corriger la valeur des colonnes individuelles.
- Vous pouvez également le faire en utilisant l'outil en ligne de commande BigQuery, comme le montre le deuxième extrait. Ici, nous restaurons les données telles qu'elles étaient il y a 120 secondes. Vous ne pouvez récupérer une table supprimée que si une autre table avec le même identifiant dans le jeu de données n'a pas été créée. En particulier, cela signifie que vous ne pouvez pas récupérer une table supprimée si elle est en cours de diffusion en continu. Il est probable que le flux de données ait déjà créé une table vide et commencé à y insérer des lignes. Faites également attention à l'utilisation de "CREATE OR REPLACE TABLE", car cela rend la table irrécupérable.

![](Aspose.Words.5529591a-df34-4ff9-8fab-40a4fdf63547.037.png)

BigQuery est un service géré, vous n'avez donc pas à vous soucier de l'exploitation, de la maintenance ou de la sécurité du système. Un système de entrepôt de données typique nécessite beaucoup de code pour la coordination et l'interfaçage. Vous pouvez exécuter le service de transfert de données BigQuery sans programmation. Le cœur du service de transfert de données BigQuery consiste en des transferts planifiés et automatiques de données depuis n'importe quel emplacement (dans votre centre de données, sur d'autres clouds, dans des services SaaS) vers BigQuery.

Le transfert des données n'est que la première étape de la construction d'un entrepôt de données. Si vous deviez assembler votre propre système, vous auriez besoin de préparer les données afin qu'elles puissent être nettoyées (qualité des données), transformées (E-L-T, extraction, chargement, transformation) et traitées (mise en forme finale et stable). Un problème courant avec les systèmes d'entrepôt de données est l'arrivée tardive des données. Par exemple, une caisse enregistreuse se ferme tard et ne signale pas ses recettes journalières pendant la période de transfert planifiée. Pour compléter les données, vous auriez besoin de détecter que toutes les données n'ont pas été reçues, puis de demander les données manquantes pour combler le vide. Cela s'appelle "remplissage de données" et c'est l'un des processus automatiques fournis par le service de transfert de données BigQuery.

"Remplir les données en arrière" signifie ajouter les données passées manquantes pour rendre un ensemble de données complet, sans lacunes, et maintenir le bon fonctionnement de tous les processus analytiques.

![](Aspose.Words.5529591a-df34-4ff9-8fab-40a4fdf63547.038.png)

Utilisez le service de transfert de données pour importer de manière répétée, périodique et planifiée des données directement depuis des systèmes en tant que service (SaaS) vers des tables dans BigQuery. Le service de transfert de données de BigQuery fournit des connecteurs, des modèles de transformation et la planification. Les connecteurs établissent des communications sécurisées avec le service source et collectent des données standard, des exports et des rapports. Ces informations sont ensuite transformées au sein de BigQuery. Les transformations peuvent être assez complexes, ce qui entraîne la création de 25 à 60 tables. De plus, le transfert peut être programmé pour se répéter aussi fréquemment qu'une fois par jour.

![](Aspose.Words.5529591a-df34-4ff9-8fab-40a4fdf63547.039.png)Le service BigQuery Data Transfer peut également être utilisé pour déplacer efficacement des données entre des régions.

![](Aspose.Words.5529591a-df34-4ff9-8fab-40a4fdf63547.040.png)

Remarquez que vous n'avez pas besoin de compartiments Cloud Storage. Le service de transfert de données BigQuery exécute des tâches BigQuery qui transforment les rapports provenant de sources SaaS en tables et vues BigQuery.

Google propose plusieurs connecteurs, notamment Campaign Manager, Cloud Storage, Amazon S3, Google Ad Manager, Google Ads, les transferts Google Play, la chaîne YouTube, le propriétaire de contenu YouTube, la migration Teradata, et plus de 100 autres connecteurs via des partenaires.

![](Aspose.Words.5529591a-df34-4ff9-8fab-40a4fdf63547.041.png)

Gardez à l'esprit que si vos transformations de données sont suffisamment simples, vous pourriez être en mesure de les effectuer uniquement avec SQL.

![](Aspose.Words.5529591a-df34-4ff9-8fab-40a4fdf63547.042.png)

Si Cloud Storage fait partie de votre flux de travail, vous pouvez charger des fichiers depuis Cloud Storage dans des tables de mise en scène (staging) dans BigQuery d'abord, puis transformer les données en utilisant des commandes SQL BigQuery pour les adapter au schéma idéal de BigQuery.

![](Aspose.Words.5529591a-df34-4ff9-8fab-40a4fdf63547.043.png)

BigQuery prend en charge les instructions DML standard telles que l'insertion, la mise à jour, la suppression et la fusion. Il n'y a aucune limite sur les instructions DML.

Cependant, vous ne devriez pas considérer BigQuery comme un système O-L-T-P. L'infrastructure sous-jacente n'est pas structurée pour fonctionner de manière optimale en tant qu'O-L-T-P. Il existe d'autres produits plus appropriés sur Google Cloud pour de telles charges de travail.

<https://cloud.google.com/bigquery/docs/managing-table-schemas>

![](Aspose.Words.5529591a-df34-4ff9-8fab-40a4fdf63547.044.png)

BigQuery prend également en charge les instructions DDL telles que CREATE OR REPLACE TABLE. Dans l'exemple de cette diapositive, l'instruction REPLACE est utilisée pour transformer une chaîne de genres en un ARRAY. Nous aborderons les ARRAYs plus en détail ultérieurement dans le cours.

![](Aspose.Words.5529591a-df34-4ff9-8fab-40a4fdf63547.045.png)

Enfin, que se passe-t-il si vos transformations vont au-delà des fonctions actuellement disponibles dans BigQuery ? Eh bien, vous pouvez créer les vôtres !

BigQuery prend en charge les fonctions définies par l'utilisateur, ou UDF (User-Defined Functions). Une UDF vous permet de créer une fonction en utilisant une autre expression SQL ou un langage de programmation externe. JavaScript est actuellement le seul langage externe pris en charge. Nous vous recommandons vivement d'utiliser le SQL standard, car BigQuery peut optimiser l'exécution du SQL beaucoup mieux que celle de JavaScript.

Les UDF vous permettent d'étendre les fonctions SQL intégrées. Les UDF prennent une liste de valeurs, qui peuvent être des tableaux (ARRAY) ou des structures (STRUCT), et renvoient une seule valeur, qui peut également être un tableau (ARRAY) ou une structure (STRUCT). Les UDF écrites en JavaScript peuvent inclure des ressources externes, telles que le chiffrement ou d'autres bibliothèques.

Auparavant, les UDF étaient uniquement des fonctions temporaires. Cela signifiait que vous ne pouviez les utiliser que pour la requête en cours ou la session en ligne de commande. Maintenant, nous avons des fonctions permanentes, des scripts et des procédures en version bêta, mais ils pourraient même être disponibles généralement au moment où vous lisez ceci. Veuillez consulter la documentation.

![](Aspose.Words.5529591a-df34-4ff9-8fab-40a4fdf63547.046.png)

Lorsque vous créez une UDF (User Defined Function) dans GCP (Google Cloud Platform), BigQuery la conserve et la stocke en tant qu'objet dans votre base de données. Cela signifie que vous pouvez partager vos UDF avec d'autres membres de votre équipe, voire même les rendre publics si vous le souhaitez. L'équipe BigQuery dispose d'un référentiel public sur GitHub pour les fonctions définies par l'utilisateur couramment utilisées, accessible via le lien que vous pouvez voir ici.

[https://cloud.google.com/blog/products/data-analytics/new-persistent-user-defined-functions- increased-concurrency-limits-gis-and-encryption-functions-and-more](https://cloud.google.com/blog/products/data-analytics/new-persistent-user-defined-functions-increased-concurrency-limits-gis-and-encryption-functions-and-more)

[Lab : Chargement de données dans BigQuery](https://www.cloudskillsboost.google/course_sessions/3754403/labs/382275)

Découvrez les schémas

![](Aspose.Words.5529591a-df34-4ff9-8fab-40a4fdf63547.047.png)

Concevoir des schémas efficaces et évolutifs est une responsabilité essentielle de toute équipe d'ingénierie des données dans le contexte de GCP (Google Cloud Platform). BigQuery héberge de nombreux ensembles de données publics et leurs schémas correspondants, que vous pouvez explorer sur des sujets populaires tels que les relevés météorologiques quotidiens, les journaux de courses de taxi, les données de santé, etc. Explorons quelques-uns de ces schémas d'ensemble de données publics en utilisant SQL.

<https://cloud.google.com/bigquery/public-data/>

Conception de schéma

![](Aspose.Words.5529591a-df34-4ff9-8fab-40a4fdf63547.048.png)

Voici la traduction du texte dans le contexte de GCP :

Jetez un œil au tableau de données original ici ainsi qu'aux tableaux de données normalisées qui contiennent les mêmes données.

Les données dans le tableau original sont organisées visuellement, comme vous pourriez l'avoir fait en fusionnant des cellules ou des colonnes dans une feuille de calcul. Mais si vous deviez écrire un algorithme pour traiter les données, comment vous y prendriez-vous ? L'accès pourrait se faire par lignes, par colonnes, par lignes puis colonnes. Et les différentes approches donneraient des performances différentes en fonction de la requête. De plus, votre méthode pourrait ne pas être parallélisable.

Les données d'origine peuvent être interprétées et stockées de différentes manières dans une base de données.

La normalisation des données consiste à les transformer en un système relationnel. Cela permet de stocker les données de manière efficace et de faciliter le traitement des requêtes. La normalisation augmente l'ordre des données. C'est utile pour économiser de l'espace. De nombreuses personnes ayant une expérience en bases de données reconnaîtront cette procédure. La normalisation des données se produit généralement lorsqu'un schéma est conçu pour une base de données.

![](Aspose.Words.5529591a-df34-4ff9-8fab-40a4fdf63547.049.png)

La dénormalisation est la stratégie qui consiste à permettre des valeurs de champ en double pour une colonne dans une table de données afin d'améliorer les performances de traitement.

Les données sont répétées plutôt que d'être relationnelles. Les données aplaties nécessitent plus d'espace de stockage, mais l'organisation aplaties (non relationnelle) rend les requêtes plus efficaces car elles peuvent être traitées en parallèle à l'aide d'un traitement par colonnes.

Plus précisément, la dénormalisation des données permet à BigQuery de répartir plus efficacement le traitement entre les emplacements, ce qui entraîne un traitement plus parallèle et de meilleures performances de requête.

En général, vous dénormaliseriez les données avant de les charger dans BigQuery.

![](Aspose.Words.5529591a-df34-4ff9-8fab-40a4fdf63547.050.png)

Cependant, il existe des cas où la dénormalisation des données est préjudiciable aux performances.

Plus précisément, si vous devez regrouper par une colonne présentant une relation de 1 à plusieurs. Dans l'exemple présenté, OrderID est une telle colonne.

Dans cet exemple, pour regrouper les données, elles doivent être mélangées. Cela se fait souvent en transférant les données sur un réseau entre des serveurs ou des systèmes. Le mélange est lent.

Heureusement, BigQuery propose une méthode pour améliorer cette situation.

![](Aspose.Words.5529591a-df34-4ff9-8fab-40a4fdf63547.051.png)

BigQuery prend en charge les colonnes contenant des données imbriquées et répétées. Dans cet exemple, une table aplatie dénormalisée est comparée à une table dénormalisée dont le schéma exploite des champs imbriqués et répétés.

OrderID est un champ répété. Étant donné que cela est déclaré à l'avance, BigQuery peut stocker et traiter les données en respectant une partie de l'organisation d'origine dans les données.

Plus précisément, tous les détails de commande pour chaque commande sont regroupés, ce qui facilite l'extraction de l'ensemble de la commande de manière plus efficace.

Pour cette raison, les champs imbriqués et répétés sont utiles pour travailler avec des données provenant de bases de données relationnelles.

Les colonnes imbriquées peuvent être comprises comme une forme de champ répété. Cela préserve les qualités relationnelles des données et du schéma d'origine tout en permettant le traitement en colonnes et parallèle des champs imbriqués répétés. C'est la meilleure alternative pour les données qui ont déjà un schéma relationnel. Transformer la relation en un champ imbriqué ou répété améliore les performances de BigQuery.

Les champs imbriqués et répétés aident BigQuery à travailler avec des données provenant de bases de données relationnelles.

Recherchez des champs imbriqués et répétés chaque fois que BigQuery est utilisé dans une solution hybride en association avec des bases de données traditionnelles.

Les champs imbriqués et répétés

![](Aspose.Words.5529591a-df34-4ff9-8fab-40a4fdf63547.052.png)

![](Aspose.Words.5529591a-df34-4ff9-8fab-40a4fdf63547.053.png)

Je vais illustrer cela en utilisant un exemple d'une entreprise réelle qui fonctionne sur Google Cloud.

GO-JEK est une entreprise en Indonésie bien connue pour son service de réservation de trajets. Ils traitent plus de 13 pétaoctets de données sur BigQuery chaque mois à partir de requêtes pour soutenir les décisions commerciales. Quel genre de décisions ?

Pour GO-JEK, ils suivent chaque fois qu'un nouveau client passe une commande, comme lorsqu'il demande un trajet via leur application mobile. Cette commande est stockée dans une table des commandes. Chaque commande a un lieu de prise en charge unique et une destination de dépose. Pour une seule commande, vous pouvez avoir un ou plusieurs événements tels que "Commande de trajet passée", "Trajet confirmé", "Chauffeur en route", "Dépose terminée", etc.

En tant qu'ingénieur de données, comment stockeriez-vous efficacement ces différentes données dans votre entrepôt de données ? Gardez à l'esprit que vous devez prendre en charge une grande base d'utilisateurs effectuant des requêtes de plusieurs pétaoctets par mois.

![](Aspose.Words.5529591a-df34-4ff9-8fab-40a4fdf63547.054.png)

Eh bien, comme vous l'avez vu précédemment, nous pourrions stocker un fait dans un seul endroit en utilisant l'approche de normalisation, qui est typique des systèmes relationnels. Ou nous pourrions emprunter la voie de la dénormalisation complète et simplement stocker tous les niveaux de granularité dans une seule grande table, où vous auriez un identifiant de commande tel que '123' répété dans une ligne pour chaque événement qui se produit sur cette commande. Plus rapide pour les requêtes, certes, mais quels sont les inconvénients ?

![](Aspose.Words.5529591a-df34-4ff9-8fab-40a4fdf63547.055.png)

Pour les schémas relationnels (schémas normalisés), les charges de travail informatiques les plus intensives sont souvent les JOINS entre de très grandes tables. Rappelez-vous que les SGBDR (systèmes de gestion de bases de données relationnelles) sont basés sur des enregistrements, donc ils doivent ouvrir chaque enregistrement en entier et extraire la clé de jointure de chaque table où il y a une correspondance. Et cela suppose que vous connaissiez toutes les tables qui doivent être jointes ensemble ! Imaginez, pour chaque nouvelle information sur une commande (comme des codes promotionnels ou des informations sur l'utilisateur), vous pourriez parler d'une jointure de 10 tables ou plus. L'alternative présente différents inconvénients. Pré-joindre toutes vos tables en une seule table massive permet de lire les données plus rapidement, mais vous devez maintenant faire très attention si vous avez des données à différents niveaux de granularité. Dans notre exemple, chaque ligne serait au niveau de granularité d'un événement spécifique (comme "Confirmation du conducteur") pour une commande donnée. Qu'est-ce que cela signifie pour un OrderID comme '123' ? Il est dupliqué pour chaque événement de cette commande. Imaginez si vous recherchez des informations de niveau supérieur telles que le chiffre d'affaires par commande, vous devez maintenant être extrêmement prudent avec les agrégations pour ne pas compter deux ou trois fois vos OrderIDs en double. Voyez-vous le problème ?

![](Aspose.Words.5529591a-df34-4ff9-8fab-40a4fdf63547.056.png)

Une solution courante dans les schémas des entrepôts de données d'entreprise consiste à tirer parti des champs de données imbriqués et répétés. Vous pouvez avoir UNE LIGNE pour chaque commande et des valeurs répétées au sein de cette UNE LIGNE pour les données qui se trouvent à un niveau plus granulaire. Par exemple, vous pourriez simplement avoir un TABLEAU de timestamps comme vos événements. Voyons un exemple pour illustrer ce point.

![](Aspose.Words.5529591a-df34-4ff9-8fab-40a4fdf63547.057.png)

Voici ce que vous voyez clairement. Sur l'écran, il y a seulement 4 lignes pour 4 OrderIDs uniques.

Remarquez tout cet espace gris entre les lignes ? C'est parce que event.status et event.time sont à un niveau de granularité plus profond. Cela signifie qu'il y a plusieurs valeurs répétées pour ces événements pour chaque commande. Un ARRAY est un type de données parfait pour gérer cette valeur répétée et conserver tous les avantages de stocker ces données dans une seule ligne.

J'ai mentionné les champs event.status et event.time. S'il s'agit d'une seule grande table, qu'est-ce que ce point fait dans ces noms de colonnes ? Il n'y a pas d'autres alias de table sur lesquels nous avons fait une jointure... Qu'est-ce qui se passe avec ces champs ?

![](Aspose.Words.5529591a-df34-4ff9-8fab-40a4fdf63547.058.png)

Événement, prise en charge et destination sont ce que l'on appelle des champs de type de données STRUCT ou structure dans SQL. Ce n'est pas spécifique à BigQuery, les STRUCTS sont des types de données SQL standard et BigQuery les prend simplement en charge de manière excellente. Les STRUCTS peuvent être considérés comme des tables pré-joinées à l'intérieur d'une table. Ainsi, au lieu d'avoir une table distincte pour ÉVÉNEMENT, PRISE EN CHARGE et DESTINATION, vous les NESTEZ simplement au sein de votre table principale.

Récapitulons donc.

![](Aspose.Words.5529591a-df34-4ff9-8fab-40a4fdf63547.059.png)

Vous pouvez approfondir un domaine spécifique et le rendre plus détaillé que le reste en utilisant un type de données ARRAY, comme vous le voyez ici pour STATUS et TIME. Et vous pouvez avoir des schémas vraiment LARGES en utilisant des STRUCTURES qui vous permettent d'avoir plusieurs champs du même type de données ou de types différents à l'intérieur (un peu comme une table distincte le ferait). Le principal avantage des STRUCTURES est que les données sont conceptuellement déjà préjointes, ce qui rend les requêtes beaucoup plus rapides.

Les gens se demandent souvent - avec des schémas vraiment larges (comme une centaine de colonnes), comment les requêtes restent-elles rapides ? Rappelez-vous que BigQuery stocke les données de manière orientée colonne et non orientée enregistrement sur le disque. Si vous effectuez simplement un COUNT(order\_id) ici pour obtenir l'ensemble de vos commandes, BigQuery n'aurait même pas besoin de tenir compte des 99 autres colonnes, dont certaines sont plus détaillées avec des types de données ARRAY ; il ne les regarderait même pas. Cela vous offre le meilleur des deux mondes si vous êtes un analyste. Beaucoup de données au même endroit et aucune difficulté avec les problèmes de granularité multiple lors des agrégations.

![](Aspose.Words.5529591a-df34-4ff9-8fab-40a4fdf63547.060.png)

Récapitulons quelques façons de concevoir le schéma des tables pour améliorer les performances des requêtes et réduire les coûts des requêtes.

- Il est beaucoup plus efficace de définir votre schéma en utilisant des champs imbriqués et répétés au lieu de joints. Supposons que vous ayez des commandes et des articles d'achat pour chaque commande. Dans un système de base de données relationnelle traditionnel, vous auriez deux tables : une table pour les articles d'achat et une autre pour les commandes, avec une clé étrangère pour relier les deux tables. Dans BigQuery, il est beaucoup plus efficace de stocker chaque commande dans une ligne et d'avoir une colonne imbriquée et répétée appelée "purchase\_item". Les tableaux (ARRAYs) sont un type natif dans BigQuery. Apprenez à penser en termes de tableaux.
- Lorsque vous avez des tables de dimension qui sont inférieures à 10 gigaoctets, gardez-les normalisées. L'exception à cela est si la table subit rarement des opérations de MISE À JOUR et de SUPPRESSION.
- Si vous ne pouvez pas définir votre schéma en termes de champs imbriqués et répétés, vous devez prendre une décision sur le fait de conserver les données dans deux tables ou de dénormaliser les tables en une seule grande table aplatie. À mesure que les tables d'un ensemble de données augmentent en taille, l'impact des performances d'une jointure augmente. À un certain point, il peut être préférable de dénormaliser vos données. Le point de basculement se situe autour de 10 Go. Si vos tables font moins de 10 Go, gardez les tables séparées et effectuez une jointure.

[Lab : Travailler avec des données JSON et des tableaux dans BigQuery](https://www.cloudskillsboost.google/course_sessions/3754403/labs/382283)

Optimisez avec la Partitioning et le Clustering.

![](Aspose.Words.5529591a-df34-4ff9-8fab-40a4fdf63547.061.png)

Dans une table partitionnée par une colonne de date ou d'horodatage, chaque partition contient les données d'une seule journée. Lorsque les données sont stockées, BigQuery veille à ce que toutes les données d'un bloc appartiennent à une seule partition. Une table partitionnée conserve ces propriétés lors de toutes les opérations qui la modifient : les travaux de requête, les instructions de manipulation des données (DML), les instructions de définition des données (DDL), les travaux de chargement et les travaux de copie. Cela nécessite que BigQuery maintienne plus de métadonnées qu'une table non partitionnée. À mesure que le nombre de partitions augmente, la quantité de surcharge de métadonnées augmente.

![](Aspose.Words.5529591a-df34-4ff9-8fab-40a4fdf63547.062.png)

L'une des façons d'optimiser les tables de votre entrepôt de données dans le contexte de GCP consiste à réduire le coût et la quantité de données lues en partitionnant vos tables. Par exemple, supposons que nous ayons partitionné cette table par la colonne eventDate. BigQuery modifiera alors son stockage interne de sorte que les dates soient stockées dans des fragments séparés.

Maintenant, lorsque vous exécutez une requête avec une clause WHERE qui recherche des dates entre le 01-03 et le 01-04, BigQuery ne devra lire que deux cinquièmes de l'ensemble des données. Cela peut entraîner des économies de coûts et de temps spectaculaires.

![](Aspose.Words.5529591a-df34-4ff9-8fab-40a4fdf63547.063.png)

Vous activez le partitionnement pendant le processus de création de la table. Cette diapositive montre comment migrer une table existante vers une table partitionnée par heure d'ingestion. En utilisant une table de destination, cela vous coûtera une analyse de table.

À mesure que de nouveaux enregistrements sont ajoutés à la table, ils seront placés dans la partition appropriée. BigQuery crée automatiquement de nouvelles partitions basées sur la date, sans nécessiter de maintenance supplémentaire. De plus, vous pouvez spécifier une durée d'expiration pour les données dans les partitions.

Le partitionnement peut être défini par heure d'ingestion, sur une colonne de type timestamp, date ou datetime, ou en fonction d'une plage de valeurs d'une colonne entière. Ici, nous partitionnons la colonne customer\_id dans la plage de 0 à 100 avec des incréments de 10.

![](Aspose.Words.5529591a-df34-4ff9-8fab-40a4fdf63547.064.png)

Bien que davantage de métadonnées doivent être maintenues, en veillant à ce que les données soient partitionnées de manière globale, BigQuery peut estimer de manière plus précise les octets traités par une requête avant son exécution. Ce calcul de coût fournit une limite supérieure sur le coût final de la requête. Une bonne pratique consiste à exiger que les requêtes incluent toujours le filtre de partition. Assurez-vous que le champ de partition est isolé du côté gauche, car c'est la seule façon pour BigQuery de rapidement écarter les partitions inutiles.

Un exemple concret de ceci peut être trouvé dans l'article de blog Optimizing BigQuery: Cluster your tables. Un lien vers le blog est disponible dans les ressources du cours.

<https://medium.com/google-cloud/bigquery-optimized-cluster-your-tables-65e2f684594b>

![](Aspose.Words.5529591a-df34-4ff9-8fab-40a4fdf63547.065.png)

Le clustering peut améliorer les performances de certains types de requêtes, telles que celles qui utilisent des clauses de filtrage et celles qui agrègent des données. Lorsque les données sont écrites dans une table clusterisée par une requête ou un job de chargement, BigQuery trie les données en utilisant les valeurs des colonnes de clustering. Ces valeurs

sont utilisées pour organiser les données en plusieurs blocs dans le stockage de BigQuery. Lorsque vous soumettez une requête contenant une clause qui filtre les données en fonction des colonnes de clustering, BigQuery utilise les blocs triés pour éliminer les analyses de données inutiles.

De même, lorsque vous soumettez une requête qui agrège des données en fonction des valeurs des colonnes de clustering, les performances sont améliorées car les blocs triés regroupent les lignes ayant des valeurs similaires.

Dans cet exemple, la table est partitionnée par eventDate et clusterisée par userId. Maintenant, parce que la requête recherche des partitions dans une plage spécifique, seules 2 des 5 partitions sont prises en compte. Parce que la requête recherche userId dans une plage spécifique, BigQuery peut passer à la plage de lignes et ne lire que ces lignes pour chaque colonne nécessaire.

![](Aspose.Words.5529591a-df34-4ff9-8fab-40a4fdf63547.066.png)

Vous configurez le regroupement au moment de la création de la table. Ici, nous créons la table, la partitionnant par "eventDate" et la regroupant par "userId". Nous indiquons également à BigQuery d'expirer les partitions qui ont plus de 3 jours.

Les colonnes que vous spécifiez dans le regroupement sont utilisées pour regrouper des données liées. Lorsque vous regroupez une table en utilisant plusieurs colonnes, l'ordre des colonnes que vous spécifiez est important. L'ordre des colonnes spécifiées détermine l'ordre de tri des données.

![](Aspose.Words.5529591a-df34-4ff9-8fab-40a4fdf63547.067.png)

Au fil du temps, à mesure que de plus en plus d'opérations modifient une table, le degré de tri des données commence à s'affaiblir et la table devient seulement partiellement triée. Dans une table partiellement triée, les requêtes qui utilisent les colonnes de regroupement peuvent nécessiter de scanner plus de blocs par rapport à une table entièrement triée. Vous pouvez re-trier les données de la table entière en exécutant une requête SELECT \* qui sélectionne et réécrit la table, mais devinez quoi ! Vous n'avez plus besoin de le faire.

![](Aspose.Words.5529591a-df34-4ff9-8fab-40a4fdf63547.068.png)

La bonne nouvelle est que BigQuery effectue désormais périodiquement une auto-réorganisation pour vous, vous n'avez donc pas à vous soucier de la mise à jour de vos clusters lorsque de nouvelles données arrivent. La réorganisation automatique est totalement gratuite et se fait automatiquement en arrière-plan. Vous n'avez rien d'autre à faire pour l'activer.

![](Aspose.Words.5529591a-df34-4ff9-8fab-40a4fdf63547.069.png)

La partition permet d'obtenir des estimations précises des coûts des requêtes et garantit une amélioration des coûts et des performances.

Le regroupement offre des avantages supplémentaires en termes de coûts et de performances, en plus des avantages de la partitionnement.

![](Aspose.Words.5529591a-df34-4ff9-8fab-40a4fdf63547.070.png)

BigQuery prend en charge le regroupement (clustering) pour les tables partitionnées et non partitionnées. Lorsque vous utilisez le regroupement et la partitionnement ensemble, les données peuvent être partitionnées par une colonne de type date, datetime ou timestamp, puis regroupées sur un ensemble différent de colonnes. Dans ce cas, les données de chaque partition sont regroupées en fonction des valeurs des colonnes de regroupement. La partitionnement permet d'obtenir des estimations de coûts précises pour les requêtes. Gardez à l'esprit que si vous n'avez pas de colonnes partitionnées et que vous souhaitez bénéficier des avantages du regroupement, vous pouvez créer une colonne "fake\_date" de type DATE et attribuer à toutes les valeurs la valeur NULL.
