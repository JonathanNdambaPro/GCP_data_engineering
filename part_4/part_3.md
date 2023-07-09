Traitement de données en serverless avec Dataflow

Ce module complet traitera des pipelines de données en batch avec Dataflow et expliquera pourquoi Dataflow est un outil de pipeline de données couramment utilisé sur Google Cloud. Sans trop dévoiler la réponse, sachez que vous pouvez écrire le même code pour créer à la fois des pipelines en batch et en continu avec Dataflow. Nous aborderons les pipelines en continu plus tard.

Les sujets que nous aborderons sont les suivants : comment choisir entre Dataflow et Dataproc, pourquoi les clients apprécient Dataflow, les pipelines Dataflow et les modèles Dataflow. Commençons.

![](Aspose.Words.fd289511-773e-48d8-a454-46446f297eda.001.png)

La raison pour laquelle Dataflow est le moyen privilégié de traiter les données sur Google Cloud est que Dataflow est sans serveur. Vous n'avez pas du tout à gérer de clusters. Contrairement à Dataproc, la mise à l'échelle automatique dans Dataflow se fait étape par étape. C'est très précis. De plus, comme nous le verrons dans le prochain cours, Dataflow vous permet d'utiliser le même code à la fois pour le traitement par lots et en continu. Cela devient de plus en plus important.

Lorsque vous construisez un nouveau pipeline de traitement des données, nous vous recommandons d'utiliser Dataflow. En revanche, si vous disposez déjà de pipelines existants écrits à l'aide des technologies Hadoop, il peut ne pas être nécessaire de tout réécrire. Migrez-le vers Google Cloud en utilisant Dataproc, puis modernisez-le si nécessaire.

![](Aspose.Words.fd289511-773e-48d8-a454-46446f297eda.002.png)

En tant qu'ingénieur de données, nous vous recommandons d'apprendre à la fois Dataflow et Dataproc et de faire le choix en fonction de ce qui convient le mieux à un cas d'utilisation spécifique.

Si le projet a des dépendances existantes sur Hadoop ou Spark, utilisez Dataproc.

Veuillez garder à l'esprit qu'il existe de nombreux problèmes subjectifs lors de la prise de cette décision et qu'aucun guide simple ne conviendra à tous les cas d'utilisation.

Parfois, l'équipe de production peut être beaucoup plus à l'aise avec une approche DevOps où elle provisionne des machines qu'avec une approche sans serveur. Dans ce cas également, vous pourriez choisir Dataproc.

Si vous ne vous souciez pas du traitement en continu et que votre objectif principal est de déplacer des charges de travail existantes, alors Dataproc conviendrait.

Dataflow, cependant, est notre approche recommandée pour la construction de pipelines.

![](Aspose.Words.fd289511-773e-48d8-a454-46446f297eda.003.png)

Dataflow offre une manière sans serveur d'exécuter des pipelines sur des données en mode batch et en streaming. Il est scalable, ce qui signifie que pour traiter davantage de données, Dataflow se mettra à l'échelle en ajoutant plus de machines de manière transparente. Sa capacité de traitement en streaming lui confère également une faible latence. Vous pouvez ainsi traiter les données au fur et à mesure de leur arrivée.

![](Aspose.Words.fd289511-773e-48d8-a454-46446f297eda.004.png)

Cette capacité à traiter des lots (batch) et des flux (stream) avec le même code est plutôt unique. Pendant longtemps, la programmation par lots et le traitement des données étaient deux choses très distinctes.

**La programmation par lots** remonte aux années 1940, aux premiers jours de l'informatique où il a été réalisé que l'on pouvait penser à deux concepts distincts : le code et les données. Utilisez le code pour traiter les données. Bien sûr, les deux étaient sur des cartes perforées, c'est donc ce que vous traitiez, une boîte de cartes perforées, appelée un lot. C'était un travail qui commençait et se terminait lorsque les données étaient entièrement traitées.

**Le traitement par flux**, en revanche, est plus fluide. Il est apparu dans les années 1970 avec l'idée que le traitement des données est quelque chose de continu. L'idée est que les données continuent d'arriver et que vous traitez les données. Le traitement lui-même était généralement effectué par micro-lots.

![](Aspose.Words.fd289511-773e-48d8-a454-46446f297eda.005.png)

Le génie de Beam réside dans sa capacité à fournir des abstractions qui unifient les concepts traditionnels de programmation par lots et les concepts traditionnels de traitement de données. L'unification de la programmation et du traitement représente une grande innovation dans l'ingénierie des données. Les quatre concepts principaux sont les PTransforms, les PCollections, les Pipelines et les Pipeline runners.

- Un pipeline identifie les données à traiter et les actions à effectuer sur ces données. Les données sont stockées dans une abstraction de données distribuée appelée PCollection. La PCollection est immuable. Toute modification effectuée dans un pipeline ingère une PCollection existante et en crée une nouvelle. Cela n'affecte pas la PCollection d'origine.
- Les actions ou le code sont encapsulés dans une abstraction appelée PTransform. Le PTransform gère l'entrée, la transformation et la sortie des données.
- Les données d'une PCollection sont transmises le long d'un graphe d'un PTransform à un autre.
- Les pipeline runners sont similaires aux hôtes de conteneurs, tels que Google Kubernetes Engine. Un même pipeline peut être exécuté sur un ordinateur local, une machine virtuelle dans un centre de données ou sur un service tel que Dataflow dans le cloud. La seule différence réside dans l'échelle et l'accès aux services spécifiques à la plateforme. Les services utilisés par le runner pour exécuter le code sont appelés système backend.

Les données immuables constituent l'une des principales différences entre la programmation par lots et le traitement de données. Les données immuables, où chaque transformation génère une nouvelle "copie", signifient qu'il n'est pas nécessaire de coordonner le contrôle d'accès ou le partage des données d'origine ingérées. Ainsi, cela facilite (ou du moins simplifie) le traitement distribué.

![](Aspose.Words.fd289511-773e-48d8-a454-46446f297eda.006.png)

La structure d'un pipeline n'est pas simplement une progression linéaire unique, mais plutôt un graphe orienté avec des branches et des agrégations. Pour des raisons historiques, nous l'appelons un pipeline, mais "datagraph" ou "dataflow" pourraient être des descriptions plus précises.

![](Aspose.Words.fd289511-773e-48d8-a454-46446f297eda.007.png)

Une PCollection représente à la fois des données en continu (streaming) et des données en lot (batch). Il n'y a pas de limite de taille pour une PCollection. Les données en continu sont une PCollection non bornée qui ne se termine pas.

![](Aspose.Words.fd289511-773e-48d8-a454-46446f297eda.008.png)

Chaque élément à l'intérieur d'une PCollection peut être individuellement accédé et traité. C'est ainsi que le traitement distribué de la PCollection est mis en œuvre. Vous définissez donc le pipeline et les transformations sur la PCollection, et l'exécuteur se charge de mettre en œuvre les transformations sur chaque élément, en distribuant le travail selon les besoins d'échelle et les ressources disponibles.

Une fois qu'un élément est créé dans une PCollection, il est immuable. Il ne peut donc jamais être modifié ou supprimé. Les éléments représentent différents types de données. Dans les programmes traditionnels, un type de données est stocké en mémoire avec un format qui favorise le traitement. Les entiers en mémoire sont différents des caractères, qui sont différents des chaînes de caractères et des types de données composés. Dans une PCollection, tous les types de données sont stockés sous forme d'état sérialisé en tant que chaînes de caractères binaires. Ainsi, il n'est pas nécessaire de sérialiser les données avant leur transfert sur le réseau et de les désérialiser lorsqu'elles sont reçues. Au lieu de cela, les données se déplacent à travers le système sous forme sérialisée et ne sont désérialisées que lorsque cela est nécessaire pour les actions d'une PTransform.

Pourquoi les clients apprécient Dataflow

![](Aspose.Words.fd289511-773e-48d8-a454-46446f297eda.009.png)

Pour comprendre cela, il est utile de comprendre un peu comment fonctionne Dataflow. Dataflow offre un mécanisme d'exécution efficace pour Apache Beam.

Le pipeline Beam spécifie CE QU'IL faut faire. Les services Dataflow choisissent COMMENT exécuter le pipeline.

Le pipeline consiste généralement à lire des données à partir d'une ou plusieurs sources, à appliquer des traitements aux données, puis à les écrire dans une ou plusieurs destinations. Afin d'exécuter le pipeline, le service Dataflow optimise d'abord le graphe en fusionnant, par exemple, les transformations ensemble.

Il divise ensuite les tâches en unités de travail et les planifie sur différents travailleurs. L'un des grands avantages de Dataflow est que l'optimisation est toujours en cours. Les unités de travail sont continuellement rééquilibrées.

Les ressources, à la fois de calcul et de stockage, sont déployées à la demande et pour chaque tâche. Les ressources sont supprimées à la fin de la tâche, de l'étape ou lors de la réduction d'échelle. Le travail planifié sur une ressource est garanti d'être traité. Le travail peut être dynamiquement rééquilibré entre les ressources, ce qui garantit la tolérance aux pannes.

Le marquage des horodatages gère les arrivées tardives de données et est associé à des redémarrages, à la surveillance et à la journalisation. Plus besoin d'attendre que d'autres tâches se terminent. Plus de planification préemptive.

Dataflow offre un moyen fiable, sans serveur et spécifique à la tâche pour traiter vos données.

![](Aspose.Words.fd289511-773e-48d8-a454-46446f297eda.010.png)

Pour résumer, les avantages de Dataflow sont les suivants :

Tout d'abord, Dataflow est entièrement géré et automatiquement configuré. Il vous suffit de déployer votre pipeline.

![](Aspose.Words.fd289511-773e-48d8-a454-46446f297eda.011.png)

Deuxièmement, Dataflow n'exécute pas simplement les transformations Apache Beam telles quelles. Il optimise le graphe en fusionnant les opérations, comme nous le voyons avec C et D. De plus, il n'attend pas la fin d'une étape précédente avant de démarrer une nouvelle étape. Nous observons cela avec A et le Group-by-key.

![](Aspose.Words.fd289511-773e-48d8-a454-46446f297eda.012.png)

Troisièmement, la mise à l'échelle automatique se produit étape par étape, au milieu d'une tâche. Lorsque les tâches nécessitent davantage de ressources, elles reçoivent ces ressources supplémentaires. Vous n'avez pas besoin de redimensionner manuellement les ressources pour correspondre aux besoins de la tâche.

![](Aspose.Words.fd289511-773e-48d8-a454-46446f297eda.013.png)

Si certaines machines ont terminé leurs tâches tandis que d'autres sont toujours en cours, les tâches en attente pour les machines occupées sont rééquilibrées vers les machines inactives. De cette manière, le travail global se termine plus rapidement.

Le rééquilibrage dynamique du travail en cours élimine la nécessité de consacrer du temps opérationnel ou des ressources d'analystes à la recherche des clés les plus sollicitées.

![](Aspose.Words.fd289511-773e-48d8-a454-46446f297eda.014.png)

Tout cela se produit tout en maintenant une sémantique de streaming solide.

Les agrégations, comme les sommes et les comptages, sont correctes même si la source d'entrée envoie

enregistrements en double.

Dataflow est capable de gérer les enregistrements arrivés en retard.

Enfin, Dataflow fonctionne comme le ciment qui relie de nombreux services sur

Google Cloud. Avez-vous besoin de lire depuis BigQuery et d'écrire dans Bigtable ? Utiliser Flux de données.

Avez-vous besoin de lire depuis Pub/Sub et d'écrire dans Cloud SQL ? Utilisez Dataflow.

Pipelines Dataflow

![](Aspose.Words.fd289511-773e-48d8-a454-46446f297eda.015.png)

Tout cela se passe tout en maintenant des sémantiques de streaming robustes.

Les agrégations, telles que les sommes et les comptages, sont correctes même si la source d'entrée envoie des enregistrements en double.

Dataflow est capable de gérer les enregistrements arrivant tardivement.

Enfin, Dataflow agit comme le lien qui rassemble de nombreux services sur Google Cloud. Vous avez besoin de lire depuis BigQuery et d'écrire dans Bigtable ? Utilisez Dataflow. Vous avez besoin de lire depuis Pub/Sub et d'écrire dans Cloud SQL ? Utilisez Dataflow.

![](Aspose.Words.fd289511-773e-48d8-a454-46446f297eda.016.png)

Voici comment construire un pipeline simple dans le contexte de GCP, où vous avez une PCollection en entrée que vous faites passer à travers trois PTransforms pour obtenir une PCollection en sortie. La syntaxe est illustrée en Python. Vous avez l'entrée, le symbole de pipeline "|", le premier PTransform, le symbole de pipeline "|", le deuxième PTransform, etc.

L'opérateur de pipeline applique essentiellement la transformation à la PCollection en entrée et renvoie une PCollection en sortie. Les trois premières fois, nous ne donnons pas de nom à la sortie, nous la passons simplement à l'étape suivante. Cependant, la sortie de PTransform 3 est sauvegardée dans une variable PCollection nommée "out".

En Java, c'est la même chose, sauf qu'au lieu du symbole de pipeline, nous utilisons la méthode "apply".

![](Aspose.Words.fd289511-773e-48d8-a454-46446f297eda.017.png)

Si vous souhaitez effectuer des branchements, il vous suffit d'envoyer la même PCollection à travers deux transformations différentes.

Donnez un nom à la variable de sortie de la PCollection dans chaque cas. Ensuite, vous pouvez l'utiliser dans le reste de votre programme. Ici, par exemple, nous prenons la PCollection\_in et la passons d'abord à la fois à PTransform 1, puis à PTransform 2.

Le résultat dans le premier cas est stocké en tant que PCollection out 1. Dans le second cas, nous le stockons en tant que PCollection out 2.

![](Aspose.Words.fd289511-773e-48d8-a454-46446f297eda.018.png)

Ce que nous vous avons montré jusqu'à présent était la partie centrale d'un pipeline. Vous aviez déjà une PCollection à laquelle vous avez appliqué plusieurs transformations, et vous obtenez finalement une autre PCollection. Mais où commence le pipeline ? Comment obtenez-vous la première PCollection ? Vous l'obtenez à partir d'une source.

Que fait un pipeline avec la dernière PCollection ? En général, il l'écrit dans une destination (sink). C'est ce que nous montrons ici. Il s'agit de Python.

Nous créons une PCollection en prenant l'objet pipeline P et en le passant sur un fichier texte dans Google Cloud Storage. C'est la ligne "ReadFromText".

Ensuite, nous appliquons la transformation PTransform appelée "FlatMap" aux lignes lues à partir du fichier texte.

Ce que FlatMap fait, c'est qu'il applique une fonction à chaque ligne de l'entrée et concatène toutes les sorties. Lorsque la fonction est appliquée à une ligne, elle peut renvoyer zéro ou plusieurs éléments qui vont dans la PCollection de sortie.

La fonction dans ce cas est la fonction appelée "count words". Elle prend une ligne de texte et renvoie un entier.

La PCollection de sortie est donc composée d'un ensemble d'entiers. Ces entiers sont écrits dans un fichier texte dans Cloud Storage.

Comme le pipeline a été créé dans une clause WITH et que ce n'est pas un pipeline en continu, la sortie de la clause WITH arrête automatiquement le pipeline.

![](Aspose.Words.fd289511-773e-48d8-a454-46446f297eda.019.png)

Une fois que vous avez écrit le pipeline, il est temps de l'exécuter. L'exécution du programme Python sur la diapositive précédente exécutera le programme. Par défaut, le programme est exécuté à l'aide de DefaultRunner, qui s'exécute sur la même machine où le programme Python a été exécuté.

Lorsque vous créez le pipeline, vous pouvez transmettre un ensemble d'options. L'une de ces options est le runner. Spécifiez Dataflow pour que le pipeline s'exécute sur Google Cloud.

Cet exemple contient des variables codées en dur, ce qui n'est généralement pas une pratique préférée pour la programmation à grande échelle.

![](Aspose.Words.fd289511-773e-48d8-a454-46446f297eda.020.png)

Bien sûr, normalement, vous allez configurer des paramètres en ligne de commande pour basculer de manière transparente entre le mode local et le cloud.

En exécutant simplement la fonction principale, le pipeline s'exécute en local. Pour l'exécuter sur le cloud, spécifiez les paramètres cloud.

![](Aspose.Words.fd289511-773e-48d8-a454-46446f297eda.021.png)

Pour concevoir des pipelines, il est nécessaire de comprendre le fonctionnement de chaque étape sur les éléments de données individuels contenus dans une PCollection. Commençons par les entrées et les sorties du pipeline.

Tout d'abord, nous configurons notre pipeline Beam avec `beam.pipeline` et nous passons toutes les options nécessaires. Ici, nous appellerons le pipeline "P".

Maintenant, il est temps d'obtenir des données en tant qu'entrée. Si nous voulons lire une série de fichiers CSV dans Cloud Storage, nous pouvons utiliser `beam.io.ReadFromText` et simplement spécifier le répertoire et le nom du fichier dans Cloud Storage. Notez que l'utilisation d'un astérisque générique permet de gérer plusieurs fichiers.

Si nous voulons plutôt lire à partir d'un sujet Pub/Sub, nous utiliserions toujours `beam.io`, mais cette fois-ci ce serait `ReadStringsFromPubSub`, et vous devriez spécifier le nom du sujet.

Et si vous souhaitez lire des données déjà présentes dans BigQuery ? Voici comment cela se présenterait. Vous préparez votre requête SQL, spécifiez BigQuery comme source d'entrée, puis vous spécifiez la requête et la source en tant que fonction de lecture à utiliser dans Dataflow. Ce ne sont là que quelques-unes des sources de données à partir desquelles Dataflow peut lire. Mais maintenant, que se passe-t-il si nous voulons écrire vers des destinations (sinks) ?

![](Aspose.Words.fd289511-773e-48d8-a454-46446f297eda.022.png)

Prenons l'exemple de BigQuery mais cette fois-ci en tant que destination des données. Avec Dataflow, vous pouvez écrire dans une table BigQuery, comme vous pouvez le voir ici. Tout d'abord, vous établissez la référence à la table BigQuery avec ce que BigQuery attend, c'est-à-dire l'identifiant de votre projet, l'identifiant de l'ensemble de données et le nom de la table.

Ensuite, vous utilisez beam.io.WriteToBigQuery en tant que destination de votre pipeline. Notez que nous utilisons ici les options normales de BigQuery pour la disposition du débit. Ici, nous tronquons la table si elle existe, ce qui signifie que les lignes de données sont supprimées. Si la table n'existe pas, nous pouvons la créer si nécessaire. Naturellement, il s'agit d'un pipeline par lots si nous tronquons la table à chaque chargement.

![](Aspose.Words.fd289511-773e-48d8-a454-46446f297eda.023.png)

Vous pouvez également créer une PCollection en mémoire sans lire à partir d'une source particulière.

Pourquoi pourriez-vous le faire ? Si vous disposez d'un petit ensemble de données tel qu'une table de recherche ou une liste codée en dur, vous pouvez créer la PCollection vous-même, comme vous pouvez le voir ici. Ensuite, nous pouvons appeler une étape du pipeline sur cette nouvelle PCollection comme si elle provenait d'un autre endroit.

![](Aspose.Words.fd289511-773e-48d8-a454-46446f297eda.024.png)

Maintenant que nous avons examiné comment obtenir les données, regardons comment nous transformons chaque élément de données dans la PCollection avec des PTransforms. La première étape de tout processus de production de map consiste en la phase de map où vous faites quelque chose en parallèle. Dans l'exemple de la longueur des mots, il y a une sortie de longueur pour chaque entrée de mot. Ainsi, le mot "chien" serait associé à trois pour la longueur. Dans l'exemple du graphique inférieur, la fonction "my\_grep" renvoie chaque instance du terme qu'elle recherche dans la ligne. Il peut y avoir plusieurs occurrences du terme dans une seule ligne, ce qui crée une relation de un à plusieurs. Dans ce cas, vous souhaiterez peut-être que "my-grep" renvoie l'instance suivante à chaque appel, c'est pourquoi la fonction a été implémentée avec un générateur utilisant des "yields". La commande "yield" a pour effet de conserver l'état de la fonction afin que la prochaine fois qu'elle soit appelée, elle puisse reprendre là où elle s'est arrêtée. "FlatMap" a pour effet de parcourir les relations de un à plusieurs. L'exemple de "map" renvoie une paire clé-valeur. En Python, il s'agit simplement d'un couple à deux éléments pour chaque mot. L'exemple de "FlatMap" renvoie la ligne uniquement pour les lignes qui contiennent le terme recherché.

![](Aspose.Words.fd289511-773e-48d8-a454-46446f297eda.025.png)

ParDo est une étape intermédiaire courante dans un pipeline. Vous pouvez l'utiliser pour extraire certains champs d'un ensemble d'enregistrements bruts en entrée, ou convertir une entrée brute dans un format différent ; vous pouvez également utiliser ParDo pour convertir des données traitées dans un format de sortie, comme des lignes de table pour BigQuery ou des chaînes de caractères pour l'impression.

- Vous pouvez utiliser ParDo pour prendre en compte chaque élément d'une PCollection et soit produire cet élément dans une nouvelle collection, soit le rejeter.
- Si votre PCollection d'entrée contient des éléments d'un type ou format différent de ce que vous souhaitez, vous pouvez utiliser ParDo pour effectuer une conversion sur chaque élément et produire le résultat dans une nouvelle PCollection.
- Si vous disposez d'une PCollection d'enregistrements avec plusieurs champs, par exemple, vous pouvez utiliser un ParDo pour extraire uniquement les champs que vous souhaitez considérer dans une nouvelle PCollection.
- Vous pouvez utiliser ParDo pour effectuer des calculs simples ou complexes sur chaque élément, ou certains éléments, d'une PCollection et produire les résultats dans une nouvelle PCollection.

![](Aspose.Words.fd289511-773e-48d8-a454-46446f297eda.026.png)

Lorsque vous appliquez une transformation ParDo, vous devez fournir du code sous la forme d'un DoFn

objet. Une fonction Do est une classe SDK de faisceau qui définit un traitement distribué fonction. Votre code DoFn doit être entièrement sérialisable, puissant et thread-safe. Dans cet exemple, nous comptons simplement le nombre de mots dans une ligne et renvoyons le longueur de la ligne. Les transformations vont toujours travailler sur un élément à la fois

ici.

![](Aspose.Words.fd289511-773e-48d8-a454-46446f297eda.027.png)

Voici un exemple en Python qui peut renvoyer plusieurs variables. Dans cet exemple, nous avons des éléments de données situés en dessous et au-dessus d'une certaine limite. Nous renvoyons deux variables différentes, en référençant ces propriétés des résultats.

[Lab Analyse de données sans serveur avec Flux de données : un flux de données simple pipeline (Python)](https://www.cloudskillsboost.google/course_sessions/3764053/labs/379242)

Agréger avec GroupByKey et Combine

![](Aspose.Words.fd289511-773e-48d8-a454-46446f297eda.028.png)

Que faites-vous après la phase de mapping ? La phase non nommée est la phase de shuffle, où vous regroupez des clés similaires. Cela fonctionne sur une PCollection de paires clé-valeur ou de tuples à deux éléments. Il regroupe les clés communes et renvoie une seule paire clé-valeur où la valeur est en réalité un groupe de valeurs.

L'idée ici est de trouver tous les codes postaux associés à une ville. Par exemple, New York est une ville et elle peut avoir les codes postaux un-zero-zero-zero-un et un-zero-zero-zero-deux. Vous pourriez d'abord créer une paire clé-valeur et utiliser ParDo, puis regrouper par la clé. Les paires clé-valeur résultantes sont simplement deux tuples.

![](Aspose.Words.fd289511-773e-48d8-a454-46446f297eda.029.png)

Nous devons prendre en compte le problème de déséquilibre des données lors de cette opération. Lorsque le même exemple est mis à l'échelle en présence de données déséquilibrées, la situation devient bien pire. Prenons l'exemple où vous effectuez votre opération GroupByKey, mais votre groupe contient 1 million d'éléments. Un million n'est pas trop important pour les équipements modernes, mais avec un milliard, vous forcez tous ces éléments à être envoyés vers un seul groupe de travail pour être comptés. Cela pourrait certainement poser des problèmes au niveau du réseau. Cette préoccupation de performance est la même lors de l'exécution de requêtes de regroupement à haute cardinalité sur des milliards d'enregistrements dans BigQuery.

Dans cet exemple, il y a un million de valeurs X et seulement mille valeurs Y. GroupByKey regroupera toutes les valeurs X sur un seul worker. Le worker mettra beaucoup plus de temps à traiter les millions de valeurs que l'autre worker, qui n'a que mille valeurs à traiter.

Bien sûr, vous payez pour le worker qui reste inactif en attendant que l'autre worker ait terminé. Dataflow est conçu pour éviter les inefficacités en maintenant un équilibre des données. Vous pouvez aider en concevant votre application de manière à diviser le travail en étapes d'agrégation et étapes ultérieures, et à éviter le regroupement ou à repousser le regroupement vers la fin du pipeline de traitement.

![](Aspose.Words.fd289511-773e-48d8-a454-46446f297eda.030.png)

CoGroupByKey est très similaire. Il regroupe les résultats de plusieurs PCollections par clé. Le résultat pour chaque clé est un tuple des valeurs associées à cette clé dans chaque collection d'entrée.

![](Aspose.Words.fd289511-773e-48d8-a454-46446f297eda.031.png)

Maintenant, nous pouvons passer à la phase de réduction. Comment calculons-nous les totaux, les moyennes ou autres agrégations sur nos PCollections ? La fonction "Combine" est utilisée pour combiner des collections d'éléments ou de valeurs dans vos données. "Combine" a des variantes qui fonctionnent sur des PCollections entières et d'autres qui combinent les valeurs pour chaque clé et PCollections de paires clé-valeur. "CombineGloballyfn" réduit une PCollection à une seule valeur en appliquant la fonction FN ou la fonction spécifiée.

"CombinePerKey" est similaire à "GroupByKey", mais combine les valeurs à l'aide d'une fonction de combinaison ou d'un appelable prenant une action itérable telle que la somme ou le maximum.

Lorsque vous appliquez une transformation "combine", vous devez fournir la fonction contenant la logique pour combiner les éléments ou les valeurs. Il existe des fonctions combinées prédéfinies pour les opérations de combinaison numérique courantes telles que la somme, le minimum et le maximum. Les opérations de combinaison simples telles que les sommes peuvent généralement être mises en œuvre en tant que fonction simple. Des opérations de combinaison plus complexes peuvent nécessiter la création d'une sous-classe d'une fonction de combinaison ayant un type d'accumulation distinct de l'entrée et/ou de la sortie.

![](Aspose.Words.fd289511-773e-48d8-a454-46446f297eda.032.png)

La fonction de combinaison doit être commutative et associative, car la fonction n'est pas nécessairement invoquée exactement une fois sur toutes les valeurs d'une clé donnée. Étant donné que les données d'entrée, y compris la collection de valeurs, peuvent être réparties sur plusieurs travailleurs, la fonction de combinaison peut être appelée plusieurs fois pour effectuer plusieurs combinaisons sur des sous-ensembles de la collection de valeurs.

Pour des fonctions de combinaison plus complexes, vous pouvez définir une sous-classe de la fonction de combinaison.

Vous devriez utiliser la fonction de combinaison si l'action requise nécessite un accumulateur plus sophistiqué, doit effectuer un prétraitement ou un post-traitement supplémentaire, peut changer le type de sortie ou tient compte de la clé.

Une opération de combinaison générale se compose de quatre opérations. Lorsque vous créez une sous-classe de la fonction de combinaison, vous devez fournir quatre opérations en remplaçant les méthodes correspondantes. La création de l'accumulateur crée un nouvel accumulateur local. Dans l'exemple donné, en prenant une moyenne, un accumulateur local suit la somme en cours des valeurs.

![](Aspose.Words.fd289511-773e-48d8-a454-46446f297eda.033.png)

Combine est plusieurs ordres de grandeur plus rapide que GroupByKey car Dataflow sait comment paralléliser une étape de combinaison.

GroupByKey fonctionne de telle manière que Dataflow ne peut utiliser qu'un seul worker par clé. Dans cet exemple, GroupByKey provoque le mélange de toutes les valeurs afin qu'elles soient toutes transmises via le réseau. Ensuite, il y a un worker pour la clé 'x' et un worker pour la clé 'y'.

Combine permet à Dataflow de distribuer une clé à plusieurs workers et de la traiter en parallèle. Dans cet exemple, CombineByKey agrège d'abord les valeurs, puis traite les agrégats avec plusieurs workers. De plus, seules 6 valeurs agrégées doivent être transmises via le réseau.

Combine est une interface Java qui indique à Dataflow que l'opération de combinaison (comme Count) est à la fois commutative et associative. Cela permet à Dataflow de répartir les shards au sein d'une clé plutôt que de regrouper chaque clé d'abord. En tant que développeur, vous pouvez créer votre propre classe Combine personnalisée pour toute opération ayant des propriétés commutatives et associatives.

![](Aspose.Words.fd289511-773e-48d8-a454-46446f297eda.034.png)

Flatten fonctionne de manière similaire à une UNION SQL. C'est une transformation de flux pour les objets PCollection qui stockent le même type de données. Flatten fusionne plusieurs objets PCollection en une seule PCollection logique. Partition est également une transformation de flux pour les objets PCollection qui stockent le même type de données.

![](Aspose.Words.fd289511-773e-48d8-a454-46446f297eda.035.png)

La fonction Partition divise une seule PCollection en un nombre fixe de collections plus petites. Vous pourriez utiliser Partition si, par exemple, vous souhaitez calculer des pourcentages ou des quartiles et que le quartile supérieur nécessite un traitement différent de tous les autres.

[Lab : Analyse de données sans serveur avec Beam](https://www.cloudskillsboost.google/course_sessions/3764053/labs/379246)

Side Inputs et Windows

![](Aspose.Words.fd289511-773e-48d8-a454-46446f297eda.036.png)

En plus de la principale PCollection d'entrée, vous pouvez fournir des entrées supplémentaires à une transformation ParDo sous forme de side inputs (entrées secondaires). Un side input est une entrée supplémentaire à laquelle votre DoFn peut accéder à chaque fois qu'il traite un élément de la PCollection d'entrée. Lorsque vous spécifiez un side input, vous créez une vue sur d'autres données qui peuvent être lues à partir de la fonction DoFn de la transformation ParDo lors du traitement de chaque élément. Les side inputs sont utiles si votre ParDo a besoin d'injecter des données supplémentaires lors du traitement de chaque élément de la PCollection d'entrée, mais que ces données supplémentaires doivent être déterminées à l'exécution et non codées en dur. Ces valeurs peuvent être déterminées par les données d'entrée ou dépendre d'une autre branche de votre pipeline.

![](Aspose.Words.fd289511-773e-48d8-a454-46446f297eda.037.png)

Voici comment fonctionnent les "side inputs" (entrées secondaires). C'est un exemple en Python.

Cet ensemble d'étapes est en fait un sous-graphe de notre graphe global. Il commence par les mots qui passent par la fonction "map" pour obtenir leur longueur, puis se combinent globalement pour calculer les longueurs totales sur l'ensemble du jeu de données.

Donc, si nous essayons de déterminer si un mot donné est plus court ou plus long que la longueur moyenne des mots, d'abord nous devons calculer la longueur moyenne des mots en utilisant ces étapes. Ensuite, toute cette branche peut être alimentée dans cette méthode. C'est ce qui crée la vue qui est statique et devient disponible pour tous les nœuds travailleurs pour une utilisation ultérieure.

Ceci est ce qu'on appelle une "side input" que vous voyez ici.

Avant de passer au prochain laboratoire, voici quelques notes sur les fonctionnalités supplémentaires.

De nombreuses transformations comportent deux parties : l'une se produit élément par élément jusqu'à ce que tous les éléments soient traités, et l'autre se produit après le traitement du dernier élément. Une des analogies les plus simples est la moyenne arithmétique. Vous additionnez la valeur de chaque élément et vous gardez le compte. C'est l'étape d'accumulation. Après avoir traité tous les éléments, vous obtenez un total de toutes les valeurs lues et un compte du nombre de valeurs lues. La dernière chose à faire est de diviser le total par le compte. C'est bon tant que vous savez que vous avez lu le dernier élément. Mais si vous avez un ensemble de données illimité, il n'y a pas de fin prédéterminée. Vous continuez donc simplement à ajouter sans jamais sortir de la boucle et effectuer la division.

![](Aspose.Words.fd289511-773e-48d8-a454-46446f297eda.038.png)

La fenêtre globale n'est pas très utile pour une PCollection sans limite, c'est-à-dire des données en continu. Le timing associé aux éléments et à une PCollection sans limite est généralement important pour le traitement des données. Une PCollection sans limite n'a pas de fin définie ni de dernier élément, elle ne peut donc jamais effectuer l'étape de terminaison. Cela est particulièrement important pour GroupByKey et Combined, qui effectuent le shuffle après la fin. La discussion sur les PCollections sans limite et les fenêtres sera poursuivie dans le cours sur le traitement des données en continu.

![](Aspose.Words.fd289511-773e-48d8-a454-46446f297eda.039.png)

La fenêtre globale est une valeur par défaut et voici comment vous pouvez la définir avec beam.WindowInto window.GlobalWindows.

![](Aspose.Words.fd289511-773e-48d8-a454-46446f297eda.040.png)

Alors, les pipelines de streaming sont-ils malchanceux s'ils ne peuvent pas utiliser la fenêtre globale ?

Non, vous pouvez utiliser des fenêtres basées sur le temps, ce qui peut être utile pour traiter des données qui arrivent en streaming à différents moments. Nous aborderons cela en détail dans le cours sur le streaming.

![](Aspose.Words.fd289511-773e-48d8-a454-46446f297eda.041.png)

Pour les entrées en lot, vous pouvez également les regrouper par intervalle de temps. Vous pouvez explicitement ajouter un horodatage dans votre pipeline au lieu de la sortie standard. Dans cet exemple, un journal d'accès hors ligne est lu, et la date/l'heure est extraite et utilisée pour le regroupement par fenêtre. Nous utilisons ici des fenêtres pour agréger nos données en lot par intervalle de temps.

Les groupes, les agrégations, et ainsi de suite, ultérieurs sont calculés uniquement dans la fenêtre temporelle.

Cet exemple utilise une fenêtre glissante, comme vous pouvez le voir avec `beam.WindowInto beam.window.SlidingWindows 60 30`, ce qui signifie capturer 60 secondes de données, mais commencer une nouvelle fenêtre toutes les 30 secondes.

Par exemple, supposons que vous ayez tous vos enregistrements de ventes et que vous vouliez calculer les ventes par jour. Vous devez simplement extraire ce champ d'horodatage qui représente l'horodatage. Ensuite, vous créeriez des fenêtres fixes d'une durée d'un jour et le flux de données calculera automatiquement la somme sur chaque fenêtre pour obtenir ces totaux. La chose principale à retenir ici est que vous pouvez le faire en mode batch.

[Lab : Analyse de données sans serveur avec DataFlow](https://www.cloudskillsboost.google/course_sessions/3764053/labs/379250)

Dataflow Templates

![](Aspose.Words.fd289511-773e-48d8-a454-46446f297eda.042.png)

Les modèles Dataflow permettent aux utilisateurs qui n'ont aucune capacité de programmation d'exécuter leur tâche Dataflow. Cela permet le déploiement rapide de types standard de tâches de transformation de données, en évitant le besoin de développer le code du pipeline et en supprimant la nécessité de prendre en compte la gestion des dépendances des composants dans le code du pipeline.

![](Aspose.Words.fd289511-773e-48d8-a454-46446f297eda.043.png)

Dans le flux de travail traditionnel, le développeur crée le pipeline dans l'environnement de développement en utilisant le SDK Dataflow en Java ou Python. Et il existe des dépendances aux fichiers de langue et de SDK d'origine. Chaque fois qu'un travail est soumis, il est entièrement retraité ou recompilé. Il n'y a pas de séparation entre les développeurs et les utilisateurs. Ainsi, les utilisateurs doivent essentiellement être des développeurs ou avoir le même accès et les mêmes ressources que les développeurs.

![](Aspose.Words.fd289511-773e-48d8-a454-46446f297eda.044.png)

Les modèles de Dataflow permettent un nouveau flux de développement et d'exécution. Les modèles aident à séparer les activités de développement et les développeurs des activités d'exécution et des utilisateurs. L'environnement utilisateur n'a plus de dépendances avec l'environnement de développement. Le besoin de recompilation pour exécuter une tâche est limité. Cette nouvelle approche facilite la planification des tâches par lots et ouvre davantage de possibilités aux utilisateurs pour soumettre des tâches, ainsi que plus d'opportunités d'automatisation.

![](Aspose.Words.fd289511-773e-48d8-a454-46446f297eda.045.png)

Les développeurs d'applications, les administrateurs de bases de données, les analystes et les data scientists peuvent utiliser des modèles en tant que solution.

![](Aspose.Words.fd289511-773e-48d8-a454-46446f297eda.046.png)

Vous pouvez également les exécuter à l'aide de l'outil en ligne de commande ou de l'API REST, comme vous le voyez ici.

Il vous suffit de spécifier l'emplacement du stockage Cloud de votre modèle que vous possédez déjà.

![](Aspose.Words.fd289511-773e-48d8-a454-46446f297eda.047.png)

Après avoir créé et préparé votre modèle Dataflow, exécutez-le à l'aide de la Console Cloud, de l'API REST ou de l'outil en ligne de commande gcloud. Vous pouvez déployer des jobs de modèle Dataflow à partir de nombreux environnements, y compris l'environnement standard d'App Engine, Cloud Functions et d'autres environnements contraints.

![](Aspose.Words.fd289511-773e-48d8-a454-46446f297eda.048.png)

Et si vous vouliez créer votre propre modèle ? Pour créer votre propre modèle, vous allez ajouter vos propres fournisseurs de valeur. C'est ce qui analyse la ligne de commande ou les arguments optionnels de votre modèle, et c'est ainsi que les utilisateurs peuvent spécifier des arguments optionnels. Une fois qu'un fichier de modèle est créé, vous l'appelez depuis une API.

![](Aspose.Words.fd289511-773e-48d8-a454-46446f297eda.049.png)

Vous n'y avez peut-être pas pensé auparavant, mais des valeurs telles que "options utilisateur" et "fichier d'entrée" qui sont intégrées à votre tâche. Ce ne sont pas seulement des paramètres, ce sont des paramètres de compilation. Pour rendre ces valeurs accessibles aux utilisateurs non développeurs, elles doivent être converties en paramètres d'exécution. Cela fonctionne via l'interface ValueProvider afin que vos utilisateurs puissent définir ces valeurs lors de la soumission du modèle. ValueProvider peut être utilisé dans les entrées/sorties, les transformations et vos fonctions. Il existe également des versions statiques et imbriquées de ValueProvider pour des cas plus complexes.

![](Aspose.Words.fd289511-773e-48d8-a454-46446f297eda.050.png)

Voici un exemple en Java pour créer votre propre modèle. Notez que les ValueProviders sont transmis tout au long de la phase de construction du pipeline.

![](Aspose.Words.fd289511-773e-48d8-a454-46446f297eda.051.png)

Parfois, nous devons transformer une valeur à partir de ce que l'utilisateur passe au moment de l'exécution en ce que la source ou le destinataire attendent de consommer. Les Nested ValueProviders répondent à ce besoin.

![](Aspose.Words.fd289511-773e-48d8-a454-46446f297eda.052.png)

Chaque modèle possède des métadonnées associées lors de sa création. Cela permet à vos utilisateurs ultérieurs de savoir ce que fait votre modèle et quels paramètres il attend. Le fichier de métadonnées se trouve dans le même répertoire que votre modèle et a simplement le suffixe de métadonnées avec un trait de soulignement ajouté à son nom.
