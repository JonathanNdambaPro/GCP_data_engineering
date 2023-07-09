# Gérer les pipelines de données avec Cloud Data Fusion et Cloud Composer

## Créer visuellement des pipelines de données par lots avec Cloud Data Fusion

![](Aspose.Words.0efdaf06-10aa-4981-92e1-1568730c0497.001.png)

Cloud Data Fusion fournit une interface utilisateur graphique ainsi que des API qui améliorent l'efficacité temporelle et réduisent la complexité. Il permet aux utilisateurs métier, aux développeurs et aux scientifiques des données de construire, déployer et gérer rapidement et facilement des pipelines d'intégration de données. Cloud Data Fusion est essentiellement un outil graphique sans code pour construire des pipelines de données.

![](Aspose.Words.0efdaf06-10aa-4981-92e1-1568730c0497.002.png)

Cloud Data Fusion est utilisé aussi bien par les développeurs, les data scientists que les analystes métier.

- Pour les développeurs, Cloud Data Fusion permet de nettoyer, faire correspondre, supprimer les doublons, mélanger, transformer, partitionner, transférer, normaliser, automatiser et surveiller les données.
- Les data scientists peuvent utiliser Cloud Data Fusion pour construire visuellement des pipelines d'intégration, tester, déboguer et déployer des applications.
- Les analystes métier peuvent exécuter Cloud Data Fusion à grande échelle sur Google Cloud, opérationnaliser les pipelines et inspecter des métadonnées d'intégration détaillées.

![](Aspose.Words.0efdaf06-10aa-4981-92e1-1568730c0497.003.png)

Cloud Data Fusion offre plusieurs avantages :

- Intégration avec n'importe quelle donnée - grâce à un écosystème riche de connecteurs pour une variété de systèmes anciens et modernes, bases de données relationnelles, systèmes de fichiers, services cloud, stockages d'objets, NoSQL, EBCDIC, et plus encore.
- Augmentation de la productivité - Si vous devez constamment passer d'un système à un autre pour recueillir des informations, votre productivité est considérablement réduite. Avec Cloud Data Fusion, vos données provenant de différentes sources peuvent être regroupées dans une vue similaire à BigQuery, Cloud Spanner ou toute autre technologie Google Cloud, ce qui vous permet d'être plus productif plus rapidement.
- Réduction de la complexité - grâce à une interface visuelle pour la création de pipelines de données, des transformations sans code et des modèles de pipeline réutilisables.
- Augmentation de la flexibilité - grâce à la prise en charge des environnements sur site et cloud, l'interopérabilité avec le logiciel open source CDAP.

![](Aspose.Words.0efdaf06-10aa-4981-92e1-1568730c0497.004.png)

À un niveau élevé, Cloud Data Fusion vous permet de construire des pipelines de données à l'aide d'une interface graphique, sans avoir à écrire de code. Vous pouvez utiliser des modèles existants, des connecteurs vers Google Cloud et d'autres fournisseurs de services cloud, ainsi qu'une bibliothèque complète de transformations pour vous aider à obtenir vos données dans le format et la qualité souhaités. De plus, vous pouvez tester et déboguer le pipeline et suivre chaque nœud pendant qu'il reçoit et traite les données.

![](Aspose.Words.0efdaf06-10aa-4981-92e1-1568730c0497.005.png)

Comme vous le verrez dans la prochaine leçon, vous pouvez étiqueter des pipelines pour les organiser de manière plus efficace pour votre équipe, et vous pouvez utiliser la fonctionnalité de recherche unifiée pour trouver rapidement des valeurs de champ ou d'autres mots-clés dans vos pipelines et schémas.

Enfin, nous parlerons de la façon dont Cloud Data Fusion trace la généalogie des transformations qui se produisent avant et après un champ donné dans votre ensemble de données.

![](Aspose.Words.0efdaf06-10aa-4981-92e1-1568730c0497.006.png)

Un des avantages de Cloud Data Fusion est qu'il est extensible. Cela inclut la possibilité de créer des modèles de pipelines, de créer des déclencheurs conditionnels, de gérer et de créer des modèles de plugins. Il existe également un plugin de widget d'interface utilisateur ainsi que des provisionneurs personnalisés, des profils de calcul personnalisés et la possibilité de s'intégrer à des hubs.

![](Aspose.Words.0efdaf06-10aa-4981-92e1-1568730c0497.007.png)

Les deux principaux composants de l'interface utilisateur sur lesquels nous allons concentrer notre attention dans ce cours sont l'interface utilisateur Wrangler pour explorer visuellement des ensembles de données et créer des pipelines sans code, ainsi que l'interface utilisateur Data Pipeline pour dessiner des pipelines directement sur une toile. Vous pouvez choisir parmi des modèles existants pour des tâches courantes de traitement de données telles que le stockage Cloud ou BigQuery.

![](Aspose.Words.0efdaf06-10aa-4981-92e1-1568730c0497.008.png)

Il existe d'autres fonctionnalités de Cloud Data Fusion dont vous devriez également prendre connaissance. Il y a un moteur de règles intégré où les utilisateurs métier peuvent programmer leurs vérifications et transformations prédéfinies, et les stocker à un seul endroit. Ensuite, les ingénieurs des données peuvent appeler ces règles dans le cadre d'un livre de règles ou d'un pipeline ultérieur.

Nous avons mentionné la traçabilité des données en tant que métadonnée de champ précédemment. Vous pouvez utiliser l'agrégateur de métadonnées pour accéder à la traçabilité de chaque champ dans une seule interface utilisateur et analyser d'autres métadonnées riches sur vos pipelines et schémas également. Par exemple, vous pouvez créer et partager un dictionnaire de données pour vos schémas directement dans l'outil.

![](Aspose.Words.0efdaf06-10aa-4981-92e1-1568730c0497.009.png)

D'autres fonctionnalités telles que le framework de microservices vous permettent de développer une logique spécialisée pour le traitement des données.

Vous pouvez également utiliser l'application Event Condition Action (ECA) pour analyser n'importe quel événement, déclencher des conditions et exécuter une action en fonction de ces conditions.

![](Aspose.Words.0efdaf06-10aa-4981-92e1-1568730c0497.010.png)

Gérer vos pipelines est plus facile lorsque vous disposez des bons outils. Nous allons maintenant jeter un coup d'œil global à l'interface utilisateur de Cloud Data Fusion telle que vous l'avez vue dans l'aperçu des composants. Voici quelques-uns des principaux éléments de l'interface utilisateur que vous rencontrerez lors de l'utilisation de Data Fusion. Examinons-les un par un.

![](Aspose.Words.0efdaf06-10aa-4981-92e1-1568730c0497.011.png)

Sous Control Center, il existe une section pour les applications, les artefacts et un ensemble de données. Ici, vous pouvez avoir plusieurs pipelines associés à une application spécifique. Le Control Center vous permet de tout voir d'un coup d'œil et de rechercher ce dont vous avez besoin, que ce soit un ensemble de données particulier, un pipeline ou un autre artefact comme un dictionnaire de données, par exemple.

![](Aspose.Words.0efdaf06-10aa-4981-92e1-1568730c0497.012.png)

Dans la section Pipelines de GCP, vous disposez d'un Studio de développement. Vous pouvez prévisualiser, exporter et planifier une tâche ou un projet. Vous avez également un connecteur et une palette de fonctions, ainsi qu'une section de navigation.

![](Aspose.Words.0efdaf06-10aa-4981-92e1-1568730c0497.013.png)

Sous la section Wrangler, vous avez des connexions, des transformations, la qualité des données, des aperçus (insights) et des fonctions.

![](Aspose.Words.0efdaf06-10aa-4981-92e1-1568730c0497.014.png)

Sous la section "Métadonnées d'intégration", vous pouvez rechercher, ajouter des balises et des propriétés, et visualiser la traçabilité des données pour les champs et les données.

![](Aspose.Words.0efdaf06-10aa-4981-92e1-1568730c0497.015.png)

Le Hub vous permet de voir tous les plugins disponibles, les cas d'utilisation d'échantillons et les pipelines pré-construits.

![](Aspose.Words.0efdaf06-10aa-4981-92e1-1568730c0497.016.png)

Les entités comprennent la possibilité de créer des pipelines, de télécharger une application, un plug-in, un pilote, une bibliothèque et des directives.

![](Aspose.Words.0efdaf06-10aa-4981-92e1-1568730c0497.017.png)

Il y a deux composants dans l'administration : la gestion et la configuration. Sous la gestion, vous avez des services et des métriques. Sous la configuration, vous avez des espaces de noms, des profils de calcul, des préférences, des artefacts système et le client REST.

![](Aspose.Words.0efdaf06-10aa-4981-92e1-1568730c0497.018.png)

Maintenant que nous avons examiné les composants de l'interface utilisateur, nous allons discuter du processus de création d'un pipeline de données.

Un pipeline est représenté visuellement sous la forme d'une série d'étapes disposées dans un graphe. Ces graphes sont appelés DAG (directed acyclic graphs) ou graphes acycliques dirigés car ils se déplacent d'une direction à une autre et ne peuvent pas se rétro-alimenter. Acyclique signifie simplement qu'il n'y a pas de cercle.

Chaque étape est un nœud, et comme vous pouvez le voir ici, les nœuds peuvent être de types différents. Vous pouvez commencer par un nœud qui récupère des données depuis Cloud Storage, puis le transmettre à un nœud qui analyse un fichier CSV. Le nœud suivant regroupe plusieurs nœuds, a une entrée et les combine avant de transmettre les données combinées à deux nœuds de synchronisation de données distincts.

![](Aspose.Words.0efdaf06-10aa-4981-92e1-1568730c0497.019.png)

Comme vous l'avez vu dans notre exemple précédent, vous pouvez avoir plusieurs nœuds qui se détachent d'un seul nœud parent. Cela est utile car vous pouvez vouloir lancer un autre flux de traitement des données qui ne doit pas être bloqué par un traitement sur une série distincte de nœuds. Vous pouvez combiner les données de deux ou plusieurs nœuds en une seule sortie dans une synchronisation. .

![](Aspose.Words.0efdaf06-10aa-4981-92e1-1568730c0497.020.png)

Dans Cloud Data Fusion, le studio est l'interface utilisateur où vous créez et concevez de nouveaux pipelines.

La zone où vous créez des nœuds et les reliez dans votre pipeline est votre canevas.

Si vous avez de nombreux nœuds dans un pipeline, le canevas peut devenir visuellement encombré, utilisez donc la mini-carte pour vous déplacer rapidement dans un pipeline volumineux.

Vous pouvez interagir avec le canevas et ajouter des objets en utilisant le Panneau de contrôle du canevas.

Lorsque vous êtes prêt à enregistrer et exécuter l'ensemble du pipeline, vous pouvez le faire avec la barre d'actions du pipeline en haut.

N'oubliez pas de donner un nom et une description à votre pipeline, et utilisez également les nombreux modèles et plugins préexistants pour ne pas avoir à écrire votre pipeline à partir de zéro.

Ici, nous avons utilisé un modèle ou un pipeline de données en mode batch, ce qui nous donne les trois nœuds que vous voyez ici pour déplacer des données à partir d'un fichier Cloud Storage, les traiter dans un wrangler et les exporter vers BigQuery.

![](Aspose.Words.0efdaf06-10aa-4981-92e1-1568730c0497.021.png)

Vous devriez utiliser le mode de prévisualisation avant de déployer et d'exécuter votre pipeline en production afin de vous assurer que tout fonctionne correctement. Lorsqu'un pipeline est en mode de prévisualisation, vous pouvez cliquer sur chaque nœud et voir des exemples de données ou des erreurs que vous devrez corriger avant le déploiement.

![](Aspose.Words.0efdaf06-10aa-4981-92e1-1568730c0497.022.png)

Après le déploiement, vous pouvez surveiller la santé de votre pipeline et recueillir des statistiques clés sur chaque exécution. Ici, nous collectons des données provenant de Twitter et de Google Cloud, et nous analysons chaque tweet avant de les charger dans

diverses sources de données. Si vous avez plusieurs pipelines, il est recommandé d'utiliser abondamment la fonctionnalité des balises pour vous aider à trouver et organiser rapidement chaque pipeline pour votre organisation. Vous pouvez consulter l'heure de démarrage, la durée de l'exécution du pipeline et le résumé global des exécutions pour chaque pipeline. Vous pouvez rapidement voir le débit de données à chaque nœud du pipeline simplement en interagissant avec le nœud. Notez le profil de calcul utilisé dans le Cloud.

![](Aspose.Words.0efdaf06-10aa-4981-92e1-1568730c0497.023.png)

En cliquant sur un nœud, vous obtenez des détails sur les entrées, les sorties et les erreurs de ce nœud spécifique. Ici, nous intégrons l'API de conversion de la parole en texte (Speech-to-Text) pour traiter des fichiers audio et les transformer en texte consultable. Vous pouvez suivre la santé individuelle de chaque nœud et obtenir des métriques utiles telles que le nombre d'enregistrements produits par seconde, le temps de traitement moyen et le temps de traitement maximal, ce qui peut vous alerter sur d'éventuelles anomalies dans votre pipeline.

![](Aspose.Words.0efdaf06-10aa-4981-92e1-1568730c0497.024.png)

Vous pouvez configurer vos pipelines pour s'exécuter automatiquement à intervalles réguliers. Si votre pipeline prend généralement beaucoup de temps pour traiter l'ensemble des données, vous pouvez également spécifier un nombre maximal d'exécutions simultanées pour éviter de traiter les données inutilement. Gardez à l'esprit que Cloud Data Fusion est conçu pour les pipelines de données en mode batch. Nous aborderons les pipelines de données en mode streaming dans les modules futurs.

![](Aspose.Words.0efdaf06-10aa-4981-92e1-1568730c0497.025.png)

L'une des grandes fonctionnalités de Cloud Data Fusion est la capacité à suivre la généalogie d'une valeur de champ donnée. Prenons l'exemple d'un champ de campagne dans un ensemble de données DoubleClick et suivons chaque opération de transformation qui s'est produite avant et après ce champ.

![](Aspose.Words.0efdaf06-10aa-4981-92e1-1568730c0497.026.png)

Ici, vous pouvez voir la généalogie des opérations appliquées au champ de campagne entre l'ensemble de données de campagne et l'ensemble de données DoubleClick. Notez l'heure à laquelle ce champ a été modifié pour la dernière fois par une exécution de pipeline, ainsi que chacun des champs d'entrée et les descriptions qui ont interagi avec le champ dans le cadre de son traitement entre les ensembles de données. Imaginez les cas d'utilisation si vous avez hérité d'un ensemble de rapports analytiques et que vous souhaitez remonter en amont de toute la logique qui a été utilisée pour un certain champ. Eh bien, maintenant vous le pouvez.

![](Aspose.Words.0efdaf06-10aa-4981-92e1-1568730c0497.027.png)

Nous avons discuté des composants principaux, des outils et des processus de création de pipelines de données. Maintenant, nous allons examiner l'utilisation de Wrangler pour explorer l'ensemble de données.

Jusqu'à présent dans le cours, nous nous sommes concentrés sur la création de nouveaux pipelines pour nos ensembles de données. Cela suppose que nous savons déjà ce que sont les données et quelles transformations doivent être effectuées. Souvent, un nouvel ensemble de données doit encore être exploré et analysé pour obtenir des informations. L'interface utilisateur de Wrangler est l'environnement Cloud Data Fusion pour explorer visuellement de nouveaux ensembles de données en vue d'obtenir des informations. Ici, vous pouvez inspecter l'ensemble de données et créer une série d'étapes de transformation appelées directives pour assembler un pipeline.

![](Aspose.Words.0efdaf06-10aa-4981-92e1-1568730c0497.028.png)

À partir de la gauche, vous avez vos connexions aux ensembles de données existants. Vous pouvez ajouter de nouvelles connexions à diverses sources de données telles que Google Cloud Storage, BigQuery, ou même d'autres fournisseurs de cloud.

Une fois que vous spécifiez votre connexion, vous pouvez parcourir tous les fichiers ou tables de cette source.

Ici, vous voyez un compartiment Cloud Storage contenant des ensembles de données de démonstration et tous les fichiers CSV des plaintes des clients. Une fois que vous avez trouvé un exemple d'ensemble de données tel que customers.csv ici, vous pouvez explorer visuellement les lignes et les colonnes et voir des aperçus d'échantillons.

En explorant les données, vous pouvez souhaiter créer de nouveaux champs calculés, supprimer des colonnes, filtrer des lignes ou manipuler les données d'autres manières. Vous pouvez le faire en utilisant l'interface Wrangler en ajoutant de nouvelles directives pour former une recette de transformation des données.

Lorsque vous êtes satisfait de vos transformations, vous pouvez créer un pipeline que vous pouvez ensuite exécuter à intervalles réguliers.

[Lab : Construire et exécuter un pipeline graphique dans Cloud Data Fusion](https://www.cloudskillsboost.google/course_sessions/3764053/labs/379262)

## Orchestrer le travail entre les services Google Cloud avec Cloud Composer

La prochaine grande tâche pour la gestion des pipelines de données est d'orchestrer le travail à travers plusieurs services de Google Cloud. Par exemple, si vous disposez de trois pipelines Cloud Data Fusion et de deux modèles d'apprentissage automatique que vous souhaitez exécuter dans un certain ordre, vous avez besoin d'un moteur d'orchestration. Dans ce module, nous examinerons l'utilisation de Cloud Composer pour vous aider dans des tâches de ce genre.

![](Aspose.Words.0efdaf06-10aa-4981-92e1-1568730c0497.029.png)

Cloud Composer contrôlera les services Google Cloud dont nous avons besoin pour fonctionner. Cependant, Cloud Composer est simplement un environnement sans serveur sur lequel s'exécute un outil de flux de travail open source.

![](Aspose.Words.0efdaf06-10aa-4981-92e1-1568730c0497.030.png)

Cet outil de flux de travail s'appelle Apache Airflow, qui est un moteur d'orchestration open source.

![](Aspose.Words.0efdaf06-10aa-4981-92e1-1568730c0497.031.png)

Le cœur de tout flux de travail est un DAG. Comme vous l'avez vu avec Cloud Data Fusion, vous construisez également des DAG avec Apache Airflow, comme vous le voyez ici. Ce qui se passe dans ce DAG particulier, ce sont quatre tâches qui mettent à jour nos données d'entraînement, les exportent, entraînent notre modèle et le déploient. Vous pouvez demander à votre DAG de faire pratiquement tout ce dont vous avez besoin. Ici, il envoie des tâches à BigQuery, Cloud Storage et Vertex AI, mais le vôtre pourrait orchestrer entre quatre services complètement différents.

![](Aspose.Words.0efdaf06-10aa-4981-92e1-1568730c0497.032.png)

Permettez-moi de vous présenter un aperçu de l'environnement réel de Cloud Composer. Une fois que vous utilisez la ligne de commande ou l'interface utilisateur Web de Google Cloud pour lancer une instance de Cloud Composer, vous serez confronté à une interface comme celle-ci. Gardez à l'esprit que vous pouvez avoir plusieurs environnements Cloud Composer, et avec chaque environnement, vous pouvez avoir une instance distincte d'Apache Airflow, qui peut contenir de zéro à plusieurs DAG (Directed Acyclic Graphs).

Une note importante ici est que parfois, vous devrez modifier les variables d'environnement pour vos flux de travail, telles que spécifier le compte de projet Google Cloud spécifique. Normalement, vous ne le ferez pas au niveau de Cloud Composer, mais au niveau de l'instance réelle d'Apache Airflow. Encore une fois, généralement, vous êtes uniquement sur la page Cloud Composer pour créer de nouveaux environnements avant de lancer directement le serveur web Airflow.

![](Aspose.Words.0efdaf06-10aa-4981-92e1-1568730c0497.033.png)

Pour accéder à l'interface d'administration d'Airflow où vous pouvez surveiller et interagir avec vos flux de travail, cliquez sur le lien situé sous Airflow webserver.

La deuxième boîte que vous voyez est le dossier DAGs, où le code de vos flux de travail réels sera stocké.

![](Aspose.Words.0efdaf06-10aa-4981-92e1-1568730c0497.034.png)

Le dossier DAGs pour chaque instance Airflow est simplement un bucket de stockage Cloud qui est automatiquement créé pour vous lorsque vous créez votre instance Cloud Composer. C'est ici que vous téléversez vos fichiers DAG, écrits en Python, et donnez vie à votre premier flux de travail dans Airflow.

![](Aspose.Words.0efdaf06-10aa-4981-92e1-1568730c0497.035.png)

Maintenant que vous êtes familiarisé(e) avec la configuration de l'environnement de base, il est temps de parler de votre principal artefact, qui est votre DAG, ainsi que des opérateurs que vous utilisez pour appeler les services vers lesquels vous souhaitez envoyer des tâches.

Tout d'abord, les workflows Airflow sont écrits en Python. Vous aurez un fichier Python pour chaque DAG. Par exemple, ici nous avons simple\_load\_dag.py dans notre répertoire DAG du compartiment Cloud Storage, et vous pouvez voir un aperçu de ce à quoi ressemble le fichier DAG. Ne vous inquiétez pas de lire le code, nous y reviendrons plus tard. Pour l'instant, il suffit de savoir qu'il y a une série de tâches créées par l'utilisateur dans chaque fichier DAG qui invoquent des opérateurs prédéfinis.

Comme cette tâche, qui utilise l'opérateur DataFlowPythonOperator et est donnée avec l'identifiant de tâche process-delimited-and-push.

Nous verrons un peu plus tard comment créer un fichier DAG et ses composants.

![](Aspose.Words.0efdaf06-10aa-4981-92e1-1568730c0497.036.png)

Une fois que vous avez téléchargé le fichier Python dans le dossier DAGs, vous pouvez revenir à la page web du serveur Airflow et sous DAGs, vous verrez le DAG que vous avez créé avec le code représenté visuellement sous forme de graphe dirigé, avec des nœuds et des arêtes.

Vous vous souviendrez que le code Python qui définissait une tâche que nous avons appelée "process-delimited-and-push" est maintenant un nœud dans notre graphe ici. Explorons un peu plus l'interface web d'Airflow.

![](Aspose.Words.0efdaf06-10aa-4981-92e1-1568730c0497.037.png)

Vous pouvez constater que ce flux de travail particulier s'appelle GcsToBigQueryTriggered et qu'il comporte trois TÂCHES lors de son exécution.

![](Aspose.Words.0efdaf06-10aa-4981-92e1-1568730c0497.038.png)

Un, processus-limité-et-pousser. Je sais simplement, d'après ce fichier Python que vous avez vu précédemment, que cette tâche invoque un job Dataflow pour lire un nouveau fichier CSV à partir d'un bucket Cloud Storage, le traiter et écrire le résultat dans BigQuery.

![](Aspose.Words.0efdaf06-10aa-4981-92e1-1568730c0497.039.png)

Deuxièmement, success-move-to-completion, déplace le fichier CSV d'un compartiment de stockage Cloud d'entrée vers un compartiment de stockage Cloud traité ou terminé pour archivage, ou...

![](Aspose.Words.0efdaf06-10aa-4981-92e1-1568730c0497.040.png)

Trois, si le pipeline échoue en cours de route, le fichier est déplacé vers le bucket de complétion mais marqué comme un échec. C'est un exemple d'un DAG qui n'est pas strictement séquentiel. Là, une décision est prise pour exécuter un nœud ou un autre en fonction du résultat du nœud parent.

![](Aspose.Words.0efdaf06-10aa-4981-92e1-1568730c0497.041.png)

Mais quelle que soit la taille et la forme de votre DAG de flux de travail, un fil conducteur commun à tous les flux de travail est l'utilisation d'opérateurs communs. Si le DAG lui-même définit COMMENT exécuter le flux de travail (d'abord effectuer l'étape 1, puis passer à l'étape 2 ou 3), les opérateurs spécifient CE QUI est réellement accompli dans le cadre de la tâche.

Dans cet exemple simple, nous utilisons l'opérateur DataFlowPythonOperator et l'opérateur Python général. Ce ne sont pas les seuls opérateurs disponibles, donc arrêtons-nous ici et examinons tous les opérateurs à notre disposition pour atteindre notre objectif de réentrainement automatique et de déploiement de notre modèle ML.

![](Aspose.Words.0efdaf06-10aa-4981-92e1-1568730c0497.042.png)

Airflow dispose de nombreux opérateurs que vous pouvez utiliser pour invoquer les TÂCHES que vous souhaitez accomplir. Les opérateurs sont généralement atomiques dans une tâche, ce qui signifie généralement que vous ne voyez qu'un seul opérateur par tâche. Cette liste de tous les services que Airflow peut orchestrer est directement extraite de la documentation Apache Airflow. Examinons ceux qui sont probablement les plus pertinents pour nous en tant qu'ingénieurs de données.

![](Aspose.Words.0efdaf06-10aa-4981-92e1-1568730c0497.043.png)

Comme vous l'avez peut-être deviné, nous utiliserons certainement les opérateurs BigQuery, car nos flux de travail dépendent des données qui leur sont fournies via Cloud Storage et BigQuery. Voici une liste des opérateurs spécifiques que nous pouvons invoquer dans une tâche pour appeler le service BigQuery afin d'effectuer des requêtes et d'autres tâches liées aux données. Dans ce cours, vous travaillerez principalement avec les trois premiers, mais je vous encourage à parcourir le lien de ressource sur tous les opérateurs afin de vous familiariser avec les possibilités offertes.

![](Aspose.Words.0efdaf06-10aa-4981-92e1-1568730c0497.044.png)

Une fois que nous avons nos données d'entraînement bien préparées, la prochaine étape logique de notre flux de travail consiste à réentraîner et redéployer notre modèle. Dans le même fichier DAG après l'achèvement des opérations BigQuery, nous pouvons effectuer un appel de service via un opérateur Vertex AI pour lancer un nouveau travail d'entraînement et gérer notre modèle en incrémentant la version.

![](Aspose.Words.0efdaf06-10aa-4981-92e1-1568730c0497.045.png)

Vous avez peut-être remarqué que votre DAG Airflow peut avoir des opérateurs qui envoient des tâches à d'autres fournisseurs de cloud. C'est idéal pour les workflows hybrides où vous avez des composants sur plusieurs plateformes cloud ou même sur site. Apache Airflow est open source et ajoute constamment de nouveaux opérateurs pour d'autres services, alors assurez-vous de consulter régulièrement la liste dans la documentation si vous attendez l'ajout d'un nouveau service.

![](Aspose.Words.0efdaf06-10aa-4981-92e1-1568730c0497.046.png)

Voici quatre tâches, t1, t2, t3 et t4, ainsi que quatre opérateurs correspondant à quatre services Google Cloud. Les noms devraient vous sembler familiers et vous pouvez probablement commencer à deviner, en les lisant dans l'ordre, ce que fait cette pipeline à un niveau élevé.

![](Aspose.Words.0efdaf06-10aa-4981-92e1-1568730c0497.047.png)

Les deux premiers concernent l'obtention de données de modèle actualisées à partir d'un ensemble de données BigQuery et leur stockage dans Cloud Storage pour une utilisation ultérieure par notre modèle ML dans le pipeline. Dans le laboratoire sur lequel vous allez travailler plus tard, l'ensemble de données sera celui que vous connaissez déjà, l'échantillon d'articles d'actualités de Google Analytics. Voyons les paramètres pris en charge par l'opérateur BigQueryOperator.

![](Aspose.Words.0efdaf06-10aa-4981-92e1-1568730c0497.048.png)

L'opérateur BigQuery vous permet de spécifier une requête SQL à exécuter sur un ensemble de données BigQuery.

![](Aspose.Words.0efdaf06-10aa-4981-92e1-1568730c0497.049.png)

Dans cet exemple rapide, nous analysons une requête qui renvoie les 100 publications les plus populaires de Stackoverflow à partir de l'ensemble de données public de BigQuery pour une plage de dates spécifiée que vous pouvez voir dans la clause WHERE. Remarquez-vous quelque chose de différent à propos des filtres dans la clause WHERE ? Oui ! Ce sont des paramètres. Dans ce cas, il s'agit de la date maximale et de la date minimale.

![](Aspose.Words.0efdaf06-10aa-4981-92e1-1568730c0497.050.png)

Vous pouvez paramétrer des parties de l'instruction SQL, comme nous l'avons fait ici, pour ne renvoyer que les articles de janvier 2018 avec une date de requête minimale et une date de requête maximale.

![](Aspose.Words.0efdaf06-10aa-4981-92e1-1568730c0497.051.png)

Ce qui est vraiment puissant, c'est que vous pouvez même rendre les paramètres dynamiques (au lieu des paramètres statiques montrés ici) et les baser sur la date de planification du DAG, par exemple: macros.ds underscore add ds dash 7, qui correspond à une semaine avant la date d'exécution prévue du DAG.

![](Aspose.Words.0efdaf06-10aa-4981-92e1-1568730c0497.052.png)

Les deux opérateurs suivants gèrent la réentraînement du modèle en soumettant une tâche au service Machine Learning Engine, puis en déployant le modèle mis à jour sur App Engine.

![](Aspose.Words.0efdaf06-10aa-4981-92e1-1568730c0497.053.png)

À la fin de presque tous les fichiers DAG, vous trouverez l'ordre réel dans lequel nous voulons que ces opérateurs s'exécutent. C'est là que le "D" dans DAG intervient : Directed (orienté).

Dans notre exemple, t2 ou la tâche 2 ne s'exécutera pas tant que t1 n'aura pas été terminée. C'est ce qui donne à notre graphe les dépendances d'un flux de travail. Je peux probablement deviner ce que vous pensez à ce stade, vous pourriez créer une structure de branches intéressante avec plusieurs nœuds enfants par parent en amont, et c'est tout à fait possible. N'oubliez simplement pas de commenter votre code afin de savoir où commence une branche, où elle se dirige et quelles tâches sont impliquées.

En guise de conseil, après avoir chargé votre fichier DAG dans le dossier DAG, vous pouvez visualiser votre DAG dans l'interface utilisateur d'Airflow sous la forme d'un graphe orienté, d'un diagramme de Gantt ou d'une liste, si vous le souhaitez. Examiner la représentation visuelle des tâches ordonnées vous aidera à confirmer que vos tâches sont correctement ordonnées.

![](Aspose.Words.0efdaf06-10aa-4981-92e1-1568730c0497.054.png)

Maintenant que vous êtes familiarisé avec les environnements Cloud Composer et Apache Airflow, ainsi qu'avec les bases de la création d'une liste de tâches pour les services Google Cloud dans votre DAG, il est temps de discuter d'un sujet vraiment important : la planification des workflows.

Comme nous l'avons mentionné précédemment, il existe deux façons différentes d'exécuter votre workflow sans avoir à cliquer manuellement sur "Exécuter le DAG". La première et la plus courante est une planification fixe ou périodique d'un workflow, par exemple une fois par jour à 6 heures du matin ou chaque semaine le samedi. La deuxième façon est basée sur des déclencheurs, par exemple si vous souhaitez exécuter votre workflow chaque fois que de nouveaux fichiers de données CSV sont chargés dans un compartiment de stockage Cloud Storage, ou si de nouvelles données sont reçues depuis un sujet Pub/Sub auquel vous êtes abonné.

![](Aspose.Words.0efdaf06-10aa-4981-92e1-1568730c0497.055.png)

Ensuite, accédez à l'onglet DAGs pour afficher les flux de travail existants pour lesquels vous disposez de fichiers DAG Python. Ici, nous avons deux DAG. Le dernier, composer\_sample\_simple\_greeting, a une planification quotidienne mais...

![](Aspose.Words.0efdaf06-10aa-4981-92e1-1568730c0497.056.png)

Pourquoi cette DAG principale ne dispose-t-elle pas d'un planning ? Comment serait-elle exécutée ?

![](Aspose.Words.0efdaf06-10aa-4981-92e1-1568730c0497.057.png)

La réponse réside dans le fait qu'il n'est pas du tout basé sur un calendrier fixe. Il est déclenché par des événements. Le déclencheur de l'exécution de ce flux de travail est une Cloud Function que nous créons. Dans la prochaine leçon, nous allons effectivement créer notre propre Cloud Function qui surveille un bucket Cloud Storage à la recherche de nouveaux fichiers CSV.

![](Aspose.Words.0efdaf06-10aa-4981-92e1-1568730c0497.058.png)

Si vous souhaitez suivre l'itinéraire régulier, vous pouvez spécifier l'`schedule\_interval` dans votre code DAG, comme vous le voyez ici. Au fait, en cliquant sur l'emploi du temps d'une journée ici dans l'interface utilisateur, vous ne pourrez pas le modifier là, mais vous serez redirigé vers l'historique de toutes les exécutions de ce flux de travail.

![](Aspose.Words.0efdaf06-10aa-4981-92e1-1568730c0497.059.png)

Comme vous l'avez vu précédemment dans ce cours, il existe deux modèles généraux pour les flux de travail ETL (Extract, Transform, Load) dans le contexte de GCP (Google Cloud Platform) :

- Déclenché par événement ou poussé (Push) - c'est-à-dire que vous poussez un nouveau fichier vers le stockage Cloud et votre flux de travail démarre.
- Ou bien le modèle de récupération (Pull), où Airflow, à un moment défini, peut consulter votre dossier de stockage Cloud et prendre tous les contenus qu'il trouve pour son exécution de flux de travail.

![](Aspose.Words.0efdaf06-10aa-4981-92e1-1568730c0497.060.png)

Nous pouvons utiliser les Cloud Functions pour créer notre flux de travail basé sur l'architecture événementielle ou push.

J'ai mentionné la déclenchement d'événements dans un compartiment Cloud Storage, mais vous pouvez également déclencher des événements en fonction des requêtes HTTP, de Pub/Sub, de Firestore, de Firebase et plus encore, comme vous le voyez ici.

En général, la technologie push est EXCELLENTE lorsque l'on souhaite distribuer les transactions au fur et à mesure de leur survenue. Les flux de données boursières et autres types de transactions financières sont très importants en ce qui concerne la technologie push. Et qu'en est-il des catastrophes et des notifications ? Encore une fois, c'est important. Pour les flux de travail d'apprentissage automatique où vos données amont n'arrivent pas à un rythme régulier (par exemple, obtenir toutes les transactions à la fin de chaque journée), envisagez d'expérimenter une architecture push. Votre dernier laboratoire, car il est basé sur les données régulières d'articles de nouvelles de Google Analytics, sera une architecture pull, mais j'ai ajouté un laboratoire facultatif pour vous permettre de vous exercer aux Cloud Functions et aux flux de travail basés sur les événements pour ceux qui sont intéressés, donc parlons-en plus en détail maintenant.

![](Aspose.Words.0efdaf06-10aa-4981-92e1-1568730c0497.061.png)

Pour notre exemple, supposons que nous avons un fichier CSV ou un ensemble de fichiers chargés dans Cloud Storage, nous choisirons donc un déclencheur Cloud Storage pour notre fonction.

![](Aspose.Words.0efdaf06-10aa-4981-92e1-1568730c0497.062.png)

Ensuite, nous spécifions un type d'événement (Finaliser/Créer de nouveaux fichiers) et un bucket à surveiller.

![](Aspose.Words.0efdaf06-10aa-4981-92e1-1568730c0497.063.png)

Dans le cadre de Cloud Function, nous devons créer une fonction réelle en JavaScript que nous voulons appeler. La bonne nouvelle est que la majeure partie de ce code pour déclencher des DAG (Directed Acyclic Graphs) Airflow dans une fonction est un modèle standard que vous pouvez copier pour démarrer.

1) Ici, nous spécifions un nom pour notre fonction appelée "triggerDag".
1) Ensuite, nous indiquons où votre environnement Airflow doit être déclenché et quel DAG dans cet environnement Airflow. Dans ce cas, il recherche un DAG appelé "GcsToBigQueryTriggered".
1) Gardez à l'esprit que vous pouvez avoir plusieurs workflows ou DAG dans un seul environnement Airflow, donc assurez-vous de spécifier le bon "DAG\_NAME" à déclencher !
1) Ensuite, nous avons quelques constantes qui construisent l'URL Airflow vers laquelle nous allons envoyer une requête POST, ainsi que l'expéditeur de la requête et le corps de la requête.
1) Enfin, la fonction "triggerDag" effectue la requête réelle vers le serveur Airflow pour démarrer un workflow DAG.

![](Aspose.Words.0efdaf06-10aa-4981-92e1-1568730c0497.064.png)

Une fois que le code de la fonction Cloud est prêt dans votre fichier index.js et que les métadonnées

à propos de la fonction dans package.json (qui contient la dépendance du code et la gestion des versions

informations), vous devez toujours spécifier la fonction que vous souhaitez réellement exécuter. Dans ce

cas, nous en avons créé un appelé triggerDag, nous le copions donc simplement.

Je vais également vous épargner environ 20 minutes de frustration et vous dire que la "fonction de

la case d'exécution est sensible à la casse, donc toutes les lettres majuscules D-A-G sont différentes du D majuscule

a et g minuscules.

![](Aspose.Words.0efdaf06-10aa-4981-92e1-1568730c0497.065.png)

Une fois que vous avez le code de la fonction Cloud prêt dans votre fichier index.js et les métadonnées sur la fonction dans package.json (qui contient des informations sur les dépendances et les versions du code), vous devez encore spécifier quelle fonction vous souhaitez réellement exécuter. Dans ce cas, nous en avons créé une appelée triggerDag, nous la copions simplement.

Je vais également vous épargner environ 20 minutes de frustration en vous disant que la case "fonction à exécuter" est sensible à la casse, donc toutes les lettres majuscules D-A-G sont différentes de la majuscule D en minuscule a et g.

![](Aspose.Words.0efdaf06-10aa-4981-92e1-1568730c0497.066.png)

À ce stade, nous avons configuré notre environnement avec nos DAG en cours d'exécution selon un calendrier prédéfini ou en fonction d'événements déclencheurs. Le dernier sujet que nous aborderons avant que vous ne mettiez en pratique ce que vous avez appris dans vos laboratoires, c'est la surveillance et le dépannage de vos fonctions Cloud et de vos flux de travail Airflow.

L'une des raisons les plus courantes pour lesquelles vous voudrez examiner les exécutions historiques de vos DAG est lorsque votre flux de travail cesse simplement de fonctionner. Notez que vous pouvez configurer une nouvelle tentative automatique pour un nombre défini d'essais en cas de bogue transitoire, mais parfois vous ne parvenez tout simplement pas à exécuter votre flux de travail dès le départ.

Dans la section "Exécutions de DAG", vous pouvez surveiller quand vos pipelines s'exécutent et dans quel état, comme réussite, en cours d'exécution ou échec. Le moyen le plus rapide d'accéder à cette page est de cliquer sur le calendrier de l'un de vos DAG à partir de la page principale des DAG. Ici, nous avons 5 exécutions réussies sur 5 jours pour ce DAG, donc celui-ci semble fonctionner très bien.

![](Aspose.Words.0efdaf06-10aa-4981-92e1-1568730c0497.067.png)

De retour sur la page principale des DAG (Directed Acyclic Graphs) dans le contexte de GCP, nous constatons la présence de rouge, ce qui indique des problèmes avec certaines de nos exécutions récentes de DAG.

![](Aspose.Words.0efdaf06-10aa-4981-92e1-1568730c0497.068.png)

En parlant des exécutions DAG, vous remarquerez les trois cercles ci-dessous qui indiquent combien d'exécutions ont réussi, sont actuellement en cours ou ont échoué. Ce n'est certainement pas bon signe que 268 exécutions ont échoué et que 0 ont réussi pour ce premier DAG. Voyons ce qui s'est passé. Nous cliquons sur le nom du DAG pour accéder à la représentation visuelle.

![](Aspose.Words.0efdaf06-10aa-4981-92e1-1568730c0497.069.png)

Il semble que la première tâche réussisse, comme l'indique la bordure verte, mais la tâche suivante "success-move-to-completion" échoue. Notez que la couleur rose clair pour le nœud "failure-move-to-completion" signifie que ce nœud a été sauté. En lisant un peu entre les lignes, le fichier CSV a été correctement traité par Dataflow dans la première tâche, mais il y a un problème pour déplacer le fichier CSV vers un autre compartiment de stockage Cloud dans le cadre de la deuxième tâche.

Pour résoudre le problème, cliquez sur le nœud d'une tâche spécifique, puis cliquez sur LOGS.

![](Aspose.Words.0efdaf06-10aa-4981-92e1-1568730c0497.070.png)

Voici les journaux pour cette exécution spécifique d'Airflow. Je recherche le mot "erreur" et je commence mon diagnostic à partir de là. Ici, il s'agit d'une erreur assez simple où il essayait de copier un fichier d'un bucket d'entrée vers un bucket de sortie, mais le bucket de sortie n'existait pas ou était mal nommé.

![](Aspose.Words.0efdaf06-10aa-4981-92e1-1568730c0497.071.png)

Un autre outil dans votre boîte à outils pour diagnostiquer les échecs d'Airflow est l'utilisation des journaux généraux de Google Cloud. Étant donné qu'Airflow lance d'autres services Google Cloud via des tâches, vous pouvez consulter et filtrer les erreurs de ces services dans Cloud Logging, tout comme vous le feriez pour le débogage d'une application normale. Ici, j'ai filtré les erreurs des étapes Dataflow pour résoudre le problème de l'échec de mon flux de travail.

Il s'est avéré que je n'avais pas changé le nom du bucket de sortie pour le fichier CSV. Ainsi, après que le fichier a été traité par Dataflow dans le cadre de l'étape 1, il a été renvoyé vers le bucket d'entrée, ce qui a déclenché un autre travail Dataflow pour le traitement, et ainsi de suite.

![](Aspose.Words.0efdaf06-10aa-4981-92e1-1568730c0497.072.png)

Vous vous demandez peut-être ce qui se passe si une erreur se produit avec ma fonction Cloud et que mon instance Airflow n'est jamais déclenchée ou ne génère aucun journal du tout (car elle n'était pas consciente que nous essayions de la déclencher) et vous avez tout à fait raison. Si vous utilisez des fonctions Cloud, assurez-vous de vérifier les journaux normaux de Google Cloud pour les erreurs et les avertissements, en plus de vos journaux Airflow.

Dans cet exemple, chaque fois que j'envoie un fichier CSV dans mon compartiment de stockage Cloud en espérant déclencher une fonction Cloud, puis mon DAG, je reçois un message d'erreur qui indique : « une fonction nommée triggerDAG est attendue ». Vous vous souvenez quand j'ai dit que les fonctions Cloud sont sensibles à la casse ? Si vous recherchez une fonction avec un D majuscule pour DAG, elle n'existera pas si D est en majuscule et a et g sont en minuscule. Donc, veillez à faire attention lors de la configuration de vos fonctions Cloud pour la première fois.

[Lab : Présentation de Cloud Composer](https://www.cloudskillsboost.google/course_sessions/3764053/labs/379269)
