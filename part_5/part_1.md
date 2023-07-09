# Introduction au traitement des données en continu

![](Aspose.Words.bc5327b5-467d-4e9d-8b6e-93f81ad0e843.001.png)

Étant donné que nous sommes dans le contexte de GCP (Google Cloud Platform), voici la traduction du texte :

Étant donné que ce module porte principalement sur le streaming, je vais parler de cette partie de l'architecture de référence.

Les données arrivent généralement via Pub/Sub, puis ces données passent par une phase d'agrégation et de transformation dans Dataflow. Ensuite, vous utilisez BigQuery ou Cloud Bigtable en fonction de l'objectif, que ce soit pour écrire des agrégats ou des enregistrements individuels provenant de sources de streaming.

![](Aspose.Words.bc5327b5-467d-4e9d-8b6e-93f81ad0e843.002.png)

Examinons d'abord les idées de diffusion en continu. Pourquoi diffusons-nous en continu ? La diffusion en continu nous permet d'obtenir des informations en temps réel dans un tableau de bord ou tout autre moyen pour visualiser l'état de votre organisation.

Dans le cas du New York City Cyber Command, Noam Dorogoyer a déclaré ce qui suit : "Nous recevons des données provenant de fournisseurs externes, et toutes ces données sont ingérées via Pub/Sub, et Pub/Sub les transmet à Dataflow, qui peut analyser ou enrichir les données."

Si les données arrivent en retard, notamment en ce qui concerne la cybersécurité, elles ne sont plus utiles, surtout en cas d'urgence. Ainsi, d'un point de vue de l'ingénierie des données, nous avons conçu le pipeline de manière à minimiser la latence à chaque étape. S'il s'agit peut-être d'un travail Dataflow, nous l'avons conçu de sorte que le plus grand nombre d'éléments possible se déroulent en parallèle, de manière à ce qu'il n'y ait jamais d'étape en attente d'une précédente."

La quantité de données qui circule au sein du Cyber Command varie chaque jour. Dorogoyer a déclaré que pendant les jours de semaine, aux heures de pointe, cela peut atteindre 5 ou 6 téraoctets. Le week-end, cela peut descendre à 2 ou 3 téraoctets. À mesure que le Cyber Command accroît sa visibilité auprès des agences, il devra gérer des pétaoctets de données.

Les analystes de sécurité peuvent accéder aux données de plusieurs manières. Ils exécutent des requêtes dans BigQuery ou utilisent d'autres outils qui fournissent des visualisations des données, comme Google Data Studio.

Article dans GCN : <https://gcn.com/cloud-infrastructure/2019/08/nycs-real-time-cyber-defense-platform/297548/>

Exposé à NEXT 2019 (diagramme de haut niveau à 19:48): <https://www.youtube.com/watch?v=x4yQY8yhVJY>

![](Aspose.Words.bc5327b5-467d-4e9d-8b6e-93f81ad0e843.003.png)

La diffusion en continu est le traitement des données sur des données non bornées. Les données bornées sont des données au repos.

Le traitement de flux est la manière dont vous traitez les données non bornées.

Un moteur de traitement en continu fournit : une latence faible, des résultats spéculatifs ou partiels, la capacité de raisonner de manière flexible sur le temps, des contrôles de correction et la puissance d'effectuer des analyses complexes.

![](Aspose.Words.bc5327b5-467d-4e9d-8b6e-93f81ad0e843.004.png)

Vous pouvez réellement utiliser le streaming pour obtenir des entrepôts de données en temps réel, puis créer un tableau de bord d'informations en temps réel. Par exemple, vous pourriez voir en temps réel les tweets positifs par rapport aux tweets négatifs concernant le produit de votre entreprise, l'utiliser pour détecter la fraude, l'utiliser pour les événements de jeux, ou pour des applications de back-office financières telles que la négociation d'actions, tout ce qui concerne les marchés, etc.

![](Aspose.Words.bc5327b5-467d-4e9d-8b6e-93f81ad0e843.005.png)

Donc, lorsque vous examinez les défis liés aux applications de streaming dans le contexte de GCP, vous parlez des trois V : Volume (volume), Velocity (vitesse) et Variety (variété) des données.

![](Aspose.Words.bc5327b5-467d-4e9d-8b6e-93f81ad0e843.006.png)

Le volume est un défi car les données ne cessent jamais d'arriver et augmentent rapidement.

![](Aspose.Words.bc5327b5-467d-4e9d-8b6e-93f81ad0e843.007.png)

Vitesse, en fonction de ce que vous faites, que ce soit le trading d'actions, le suivi des informations financières, l'ouverture des portillons du métro, vous pouvez avoir des dizaines de milliers d'enregistrements par seconde transférés. La vitesse peut également être très variable.

Par exemple, si vous êtes un détaillant concevant votre système de points de vente à l'échelle nationale, vous allez probablement transporter un volume raisonnablement stable tout au long de l'année jusqu'à arriver au Vendredi noir. À ce moment-là, les ventes et les données transférées explosent. Il est donc important de concevoir des systèmes capables de gérer cette charge supplémentaire.

![](Aspose.Words.bc5327b5-467d-4e9d-8b6e-93f81ad0e843.008.png)

La variété des données est le troisième défi. Si vous utilisez uniquement des données structurées, telles que celles provenant d'une application mobile, cela est assez facile à gérer. Mais que faire si vous avez des données non structurées, comme des données vocales ou des images ? Ce sont des enregistrements en continu et, dans certains cas, une valeur nulle peut être utilisée pour traiter ce type de données non structurées.

![](Aspose.Words.bc5327b5-467d-4e9d-8b6e-93f81ad0e843.009.png)

Nous allons donc examiner comment le streaming dans le cloud peut nous aider ici. Du côté du volume, nous allons examiner un outil pour aider à l'auto-ajustement du traitement et de l'analyse afin que le système puisse gérer le volume. Du côté de la vitesse, nous examinerons un outil capable de gérer la variabilité du processus de streaming. Et du côté de la variété, nous examinerons comment l'intelligence artificielle peut nous aider avec les données non structurées.

![](Aspose.Words.bc5327b5-467d-4e9d-8b6e-93f81ad0e843.010.png)

Les trois produits que vous allez examiner ici sont les suivants :

- Pub/Sub, qui vous permettra de gérer des volumes de données changeants et variables,
- Dataflow, qui peut vous aider à traiter les données sans délais indus,
- BigQuery, que vous utiliserez pour vos rapports ad hoc, même sur des données en continu.

![](Aspose.Words.bc5327b5-467d-4e9d-8b6e-93f81ad0e843.011.png)

Jetons un coup d'œil aux étapes qui se produisent.

- Tout d'abord, des données de quelque sorte arrivent, peut-être à partir d'une application, d'une base de données ou de l'Internet des objets, ou IoT. Elles génèrent des événements.
- Ensuite, une action se produit. Vous allez ingérer ces données et les distribuer avec Pub/Sub. Cela garantira que les messages sont fiables. Cela vous donnera une mise en tampon. Dataflow est ensuite utilisé pour agréger, enrichir et détecter les données.
- Ensuite, vous allez écrire dans une base de données de type BigQuery ou Bigtable, ou peut-être faire passer les données par un modèle d'apprentissage automatique. Par exemple, vous pouvez utiliser ces données en continu lorsqu'elles arrivent pour entraîner un modèle dans Vertex AI.
- Enfin, Dataflow ou Dataproc peuvent être utilisés pour le traitement par lots, le remplissage, etc.

Ainsi, c'est une façon assez courante de mettre les choses en place dans Google Cloud.
