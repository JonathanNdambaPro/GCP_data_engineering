Les fonctionnalités de streaming de Dataflow

Défis liés aux données en streaming

![](Aspose.Words.50778bac-9367-4acf-b91b-0e6505e2ae86.001.png)

Dataflow, comme nous le savons déjà, offre un service sans serveur pour le traitement de données par lots et en continu. Il est évolutif et, pour le streaming, dispose d'un pipeline de traitement à faible latence pour les messages entrants.

![](Aspose.Words.50778bac-9367-4acf-b91b-0e6505e2ae86.002.png)

Nous avons discuté du fait que nous pouvons avoir des collections bornées et non bornées, donc maintenant nous examinons un tuyau non borné qui résulte d'un travail de streaming. Tout ce que nous avons fait jusqu'à présent, comme les branchements, les fusions, nous pouvons également le faire avec Dataflow pour les pipelines de streaming.

Cependant, maintenant, chaque étape du pipeline va agir en temps réel sur les messages entrants plutôt que par lots.

![](Aspose.Words.50778bac-9367-4acf-b91b-0e6505e2ae86.003.png)

Quels sont certains des défis liés au traitement des données en continu ?

- Un défi est la scalabilité, c'est-à-dire la capacité à gérer le volume de données à mesure qu'il devient plus important et/ou plus fréquent.
- Le deuxième défi est la tolérance aux pannes. Plus vous grandissez, plus vous êtes sensible à une panne inattendue.
- Le troisième défi concerne le modèle utilisé, qu'il s'agisse de flux continu ou de lots répétés.
- Un autre défi concerne la synchronisation ou la latence des données. Par exemple, que se passe-t-il si le réseau présente un retard ou si un capteur tombe en panne et que les messages ne peuvent pas être envoyés ?

![](Aspose.Words.50778bac-9367-4acf-b91b-0e6505e2ae86.004.png)De plus, il y a un défi lié à toute forme d'agrégation que vous pourriez essayer de réaliser. Par exemple, si vous essayez de calculer la moyenne des données, mais que celles-ci sont dans un scénario de flux continu. Vous ne pouvez pas simplement insérer les valeurs dans la formule pour obtenir une moyenne, la somme de 1 à n, car n est un nombre en constante augmentation.

![](Aspose.Words.50778bac-9367-4acf-b91b-0e6505e2ae86.005.png)

Dans un scénario de streaming, vous devez diviser le temps en fenêtres et nous pouvons obtenir la moyenne dans une fenêtre donnée. Cela peut être pénible si vous avez déjà dû écrire un système comme celui-ci. Vous pouvez imaginer que cela peut être difficile de maintenir la segmentation en fenêtres, les threads de défilement du temps, etc. La bonne nouvelle est que Dataflow va le faire automatiquement pour vous. Dans Dataflow, lorsque vous lisez des messages de Pub/Sub, chaque message aura un horodatage qui est l'horodatage du message Pub/Sub, puis vous pourrez utiliser cet horodatage pour placer les données dans les différentes fenêtres temporelles et agréger toutes ces fenêtres.

![](Aspose.Words.50778bac-9367-4acf-b91b-0e6505e2ae86.006.png)L'ordre des messages est important et il peut y avoir une latence entre le moment où un capteur est lu et le moment où le message est envoyé. Vous devrez peut-être modifier les horodatages si cette latence est importante.

![](Aspose.Words.50778bac-9367-4acf-b91b-0e6505e2ae86.007.png)

Si vous souhaitez modifier un horodatage et le baser sur une propriété de vos données elles-mêmes, vous pouvez le faire. Chaque message qui arrive, par exemple, le capteur fournit sa propre date-heure en tant que partie du message.

L'élément source ajoute une date-heure par défaut ou DTS, qui est l'heure d'entrée dans le système, plutôt que l'heure à laquelle les données du capteur ont été capturées.

Un PTransform extrait la date-heure des données de la partie de l'élément et modifie les métadonnées DTS afin que l'heure de capture des données puisse être utilisée dans le traitement par fenêtre.

![](Aspose.Words.50778bac-9367-4acf-b91b-0e6505e2ae86.008.png)

Voici le code utilisé pour modifier le timestamp de la date en remplaçant le timestamp du message par le timestamp des données de l'élément.

![](Aspose.Words.50778bac-9367-4acf-b91b-0e6505e2ae86.009.png)

Si PubsubIO est configuré pour utiliser des ID de message personnalisés, Dataflow déduplique les messages en maintenant une liste de tous les ID personnalisés qu'il a rencontrés au cours des 10 dernières minutes. Si l'ID d'un nouveau message se trouve dans cette liste, le message est considéré comme un doublon et est rejeté.

Fenêtrage dans Dataflow

![](Aspose.Words.50778bac-9367-4acf-b91b-0e6505e2ae86.010.png)

![](Aspose.Words.50778bac-9367-4acf-b91b-0e6505e2ae86.011.png)

Les fenêtres fixes sont celles qui sont divisées en tranches de temps, par exemple, horaires, quotidiennes, mensuelles. Les fenêtres de temps fixes sont constituées d'intervalles cohérents et non chevauchants.

Les fenêtres glissantes sont celles que vous utilisez pour effectuer des calculs. Par exemple, donnez-moi 30 minutes de données et calculez cela toutes les 5 minutes. Les fenêtres de temps glissantes peuvent se chevaucher, par exemple, dans une moyenne mobile. Les fenêtres glissantes sont définies par une durée d'écart minimale et le déclenchement du chronométrage est effectué par un autre élément.

Les fenêtres de session sont définies par une durée d'écart minimale et le déclenchement du chronométrage est effectué par un autre élément. Les fenêtres de session sont utilisées dans des situations où la communication est intermittente. Cela peut correspondre à une session Web. Un exemple pourrait être lorsqu'un utilisateur arrive, consulte quatre ou cinq pages, puis repart. Vous pouvez capturer cela comme une fenêtre de session. N'importe quelle clé de vos données peut être utilisée comme clé de session. Elle aura une période de temporisation et la fenêtre sera vidée à la fin de cette période de temporisation.

![](Aspose.Words.50778bac-9367-4acf-b91b-0e6505e2ae86.012.png)

Voici comment nous pouvons définir ces différents types de fenêtres sous Python dans le contexte de GCP :

Dans l'exemple de la fenêtre de temps fixe, nous pouvons utiliser les fonctions beam.WindowInto et window.FixedWindows avec un argument de 60 pour obtenir des fenêtres fixes démarrant toutes les 60 secondes.

Dans le deuxième exemple, avec une fenêtre temporelle glissante, nous utilisons window.SlidingWindows avec un argument de 30 et 5. Ici, le premier argument fait référence à la durée de la fenêtre, c'est-à-dire 30 secondes. Et le deuxième argument indique à quelle fréquence de nouvelles fenêtres s'ouvrent, c'est-à-dire cinq secondes.

Enfin, nous avons l'exemple d'une fenêtre de session. Nous utilisons windows.Sessions avec un argument de 10 multiplié par 60 pour définir une fenêtre de session avec un délai d'expiration de dix minutes, c'est-à-dire 600 secondes.

![](Aspose.Words.50778bac-9367-4acf-b91b-0e6505e2ae86.013.png)Comment fonctionne la fenêtrage ? Tout étant égal, voici comment le fenêtrage devrait fonctionner. S'il n'y avait pas de latence, si nous vivions dans un monde idéal, si tout était instantané, alors ces fenêtres temporelles fixes se videraient simplement à la fermeture de la fenêtre. Au tout dernier microseconde où il devient 8:05:00, une fenêtre de cinq minutes se termine et vide toutes les données. Cela se produit uniquement S'IL n'y a pas de latence.

![](Aspose.Words.50778bac-9367-4acf-b91b-0e6505e2ae86.014.png)

Dans le monde réel, la latence se produit. Nous avons des retards réseau, des files d'attente système, des retards de traitement, une latence Pub/Sub, etc. Alors, quand voulons-nous fermer la fenêtre ? Devrions-nous attendre un peu plus longtemps que 8h05, peut-être quelques secondes de plus ?

![](Aspose.Words.50778bac-9367-4acf-b91b-0e6505e2ae86.015.png)

Ceci est ce que nous appelons le filigrane (watermark), et Dataflow le suit automatiquement. Essentiellement, il va suivre le temps de retard et il est capable de le faire, par exemple,

si vous utilisez le connecteur Pub/Sub, car il connaît l'heure du message le plus ancien

non traité dans Pub/Sub. Ensuite, il connaît le dernier message qu'il a traité grâce à Dataflow.

Il prend ensuite cette différence et c'est le temps de retard.

![](Aspose.Words.50778bac-9367-4acf-b91b-0e6505e2ae86.016.png)

Donc, ce que Dataflow va faire, c'est calculer en continu le watermark, qui indique à quel point nous sommes en retard. Normalement, Dataflow va attendre que le watermark qu'il a calculé se soit écoulé. Ainsi, s'il y a un délai système de trois ou quatre secondes, il attendra quatre secondes avant de vider la fenêtre, car c'est à ce moment-là qu'il estime que toutes les données devraient avoir été reçues pour cette période de temps.

Qu'arrive-t-il alors aux données tardives ? Disons qu'il reçoit un événement avec un horodatage de 8h04, mais qu'il est maintenant 8h06. Il a deux minutes de retard, une minute après la fin de la fenêtre, que fait-il de ces données ? La réponse est que vous pouvez choisir. Par défaut, il les ignore simplement, mais vous pouvez également lui dire de retraiter la fenêtre en fonction de ces arrivées tardives.

La configuration par défaut de la fenêtrage de Beam essaie de déterminer quand toutes les données sont arrivées (en fonction du type de source de données) et fait avancer le watermark au-delà de la fin de la fenêtre. Cette configuration par défaut n'autorise pas les données tardives.

![](Aspose.Words.50778bac-9367-4acf-b91b-0e6505e2ae86.017.png)

Le comportement par défaut consiste à déclencher l'action à l'horodatage de la marque d'eau. Donc, si vous ne spécifiez pas de déclencheur, vous utilisez en réalité le déclencheur "AfterWatermark".

"AfterWatermark" est un déclencheur basé sur l'heure d'événement. Nous pouvons également appliquer n'importe quel autre déclencheur en utilisant l'heure d'événement. Les horodatages des messages sont utilisés pour mesurer le temps avec ces déclencheurs. Mais nous pouvons également ajouter des déclencheurs personnalisés.

Si le déclencheur est basé sur l'heure de traitement, l'horloge réelle / l'heure réelle est utilisée pour décider quand émettre les résultats. Par exemple, vous pouvez décider d'émettre exactement toutes les 30 secondes, indépendamment des horodatages des messages qui sont arrivés à la fenêtre.

"AfterCount" est un exemple de déclencheur basé sur les données. Au lieu d'émettre des résultats en fonction du temps, nous déclenchons ici en fonction de la quantité de données arrivées dans la fenêtre.

La combinaison de plusieurs types de déclencheurs ouvre un monde de possibilités avec les pipelines de streaming. Nous pouvons émettre certains résultats rapidement (en utilisant AfterProcessingTime), puis à nouveau à l'horodatage de la marque d'eau (lorsque les données sont complètes), et ensuite pour les cinq messages suivants qui arrivent en retard (après la marque d'eau).

![](Aspose.Words.50778bac-9367-4acf-b91b-0e6505e2ae86.018.png)

Maintenant, nous connaissons différentes techniques pour gérer l'accumulation des données arrivant tardivement. Nous savons également que les déclencheurs sont utilisés pour initier l'accumulation, et les marques d'eau aident à déterminer le délai de latence et les actions correctives associées pour le calcul des accumulations. Le code de cet exemple crée un déclencheur d'échantillon. Comme vous pouvez le voir dans le code, nous créons une fenêtre glissante de 60 secondes, qui se déplace toutes les cinq secondes. La méthode AfterWatermark nous donne des détails sur le moment où déclencher l'accumulation. Le code utilise deux options. Premièrement, un calcul anticipé ou spéculatif, qui est réglé sur 30 secondes. Deuxièmement, un calcul en retard, pour chaque élément arrivant tardivement. Le deuxième segment de code montre le déclencheur composite. Le déclencheur composite s'active soit après cent éléments disponibles pour l'accumulation, soit toutes les 60 secondes indépendamment de la marque d'eau. Ce segment de code utilise une fenêtre fixe d'une minute de durée.

![](Aspose.Words.50778bac-9367-4acf-b91b-0e6505e2ae86.019.png)

Voici comment la fenêtre est retraitée. Ce traitement tardif fonctionne en Java et en Python.

![](Aspose.Words.50778bac-9367-4acf-b91b-0e6505e2ae86.020.png)

Lorsque vous définissez un déclencheur dans le contexte de GCP (Google Cloud Platform), vous devez choisir entre le mode d'accumulation ou le mode de suppression.

Cet exemple montre les différents comportements causés par l'intersection de la gestion des fenêtres, des déclencheurs et du mode d'accumulation.

[Lab : Traitement de données en continu, pipelines de données en continu](https://www.cloudskillsboost.google/course_sessions/3849359/labs/345018)
