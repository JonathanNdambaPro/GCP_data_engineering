Construction et opérationnalisation de systèmes de traitement des données

Construction et Maintenance de Structures de Données et Bases de Données

Le premier domaine de traitement des données que nous examinerons concerne la création et la maintenance de structures et de bases de données.

Ainsi, il ne s'agit pas seulement de choisir un type de base de données ou de service particulier, mais aussi de réfléchir aux qualités qui sont offertes et de commencer à envisager comment organiser les données.

![](Aspose.Words.e79873e8-3438-4e0d-ab81-7a553aabca8b.001.png)

Vous pouvez également vous familiariser avec ce diagramme.

- BigQuery est recommandé comme entrepôt de données.
- BigQuery est le stockage par défaut pour les données tabulaires.
- Utilisez Cloud Bigtable si vous souhaitez une faible latence / un débit élevé.

![](Aspose.Words.e79873e8-3438-4e0d-ab81-7a553aabca8b.002.png)

Voici quelques conseils concrets sur la représentation flexible des données. Vous souhaitez que les données soient divisées de manière à être logiques pour votre cas d'utilisation spécifique. Si les données sont trop divisées, cela crée un travail supplémentaire.

Dans l'exemple de gauche, chaque élément de données est stocké séparément, ce qui facilite le filtrage sur des champs spécifiques et les mises à jour.

Dans l'exemple de droite, toutes les données sont stockées dans un seul enregistrement, comme une seule chaîne. L'édition/la mise à jour est difficile. Il serait difficile de filtrer sur un champ particulier.

Dans l'exemple du bas, une relation est définie par deux tables. Cela pourrait faciliter la gestion et la génération de rapports sur la liste des emplacements.

![](Aspose.Words.e79873e8-3438-4e0d-ab81-7a553aabca8b.003.png)ACID vs BASE est une connaissance essentielle des données que vous voudrez connaître très bien afin de pouvoir déterminer facilement si une solution de données particulière est compatible avec les exigences identifiées dans le cas. Par exemple, pour une transaction financière, un service qui ne fournit qu'une cohérence éventuelle pourrait être incompatible.

![](Aspose.Words.e79873e8-3438-4e0d-ab81-7a553aabca8b.004.png)

Cloud Storage est persistant. Il possède des classes de stockage - nearline, coldline, régional et multi-régional. Il dispose d'un contrôle d'accès granulaire. Vous devriez connaître toutes les méthodes de contrôle d'accès, y compris les rôles IAM et les URL signées.

Cloud Storage possède de nombreuses fonctionnalités que les gens manquent souvent. Ils finissent par essayer de dupliquer la fonction en code, alors qu'en réalité, tout ce qu'ils ont à faire est d'utiliser la capacité déjà disponible.

Par exemple, vous pouvez modifier les classes de stockage. Vous pouvez diffuser des données vers Cloud Storage. Cloud Storage prend en charge une sorte de versioning. Et il existe plusieurs options de chiffrement pour répondre à différents besoins. De plus, vous pouvez automatiser certaines de ces fonctionnalités à l'aide de la gestion du cycle de vie. Par exemple, vous pouvez modifier la classe de stockage pour un objet ou supprimer cet objet après une période de temps.

![](Aspose.Words.e79873e8-3438-4e0d-ab81-7a553aabca8b.005.png)

Cloud SQL est le service géré qui fournit une instance MySQL.

Je tiens à souligner qu'il existe plusieurs moyens de se connecter en toute sécurité à une instance Cloud SQL. Il serait donc important que vous vous familiarisiez avec les différentes approches et les avantages de chacune d'entre elles.

![](Aspose.Words.e79873e8-3438-4e0d-ab81-7a553aabca8b.006.png)

Cloud Bigtable est conçu pour traiter des volumes importants de données avec une latence de l'ordre de la milliseconde, ce qui le rend beaucoup plus rapide que BigQuery, par exemple. Il s'agit d'une base de données NoSQL. C'est donc idéal pour un stockage en colonnes.

Dans quels cas voudriez-vous sélectionner un SSD plutôt qu'un HDD pour les machines du cluster ? Je suppose que cela serait nécessaire si vous avez besoin de performances plus élevées.

![](Aspose.Words.e79873e8-3438-4e0d-ab81-7a553aabca8b.007.png)

Cet exemple montre des opérations boursières.

Chaque opération est représentée par une ligne distincte. Cela aboutira à des centaines de millions de lignes par jour. Ce qui est tout à fait acceptable avec Cloud Bigtable.

![](Aspose.Words.e79873e8-3438-4e0d-ab81-7a553aabca8b.008.png)

Cloud Spanner est fortement typé et globalement cohérent. Les deux caractéristiques qui le distinguent de Cloud SQL sont les transactions globalement cohérentes et la taille. Cloud Spanner peut fonctionner avec des bases de données beaucoup plus grandes que Cloud SQL.

![](Aspose.Words.e79873e8-3438-4e0d-ab81-7a553aabca8b.009.png)

Cloud SQL est suffisant si vous pouvez vous contenter d'une seule base de données. Mais si vous avez besoin de plusieurs bases de données, Cloud Spanner est un excellent choix. MySQL atteint un mur de performance. Si vous regardez le 99e percentile de la latence, il est clair que les performances se dégradent. La distribution de MySQL est difficile. Cependant, Spanner se distribue facilement (même à l'échelle mondiale) et offre des performances constantes. Pour prendre en charge un débit plus élevé, il suffit d'ajouter plus de nœuds.

![](Aspose.Words.e79873e8-3438-4e0d-ab81-7a553aabca8b.010.png)

Datastore est une solution NoSQL qui était auparavant réservée à App Engine. Elle offre de nombreuses fonctionnalités principalement utiles aux applications, telles que la persistance des informations d'état. Elle est maintenant disponible pour d'autres clients en dehors d'App Engine.

![](Aspose.Words.e79873e8-3438-4e0d-ab81-7a553aabca8b.011.png)

Mémorisez cette table et soyez capable de l'utiliser à l'envers. Exemple : si la question de l'examen mentionne "Entrepôt de données", vous devriez penser "BigQuery est un candidat". Si le cas évoque quelque chose à propos de gros fichiers média, vous devriez immédiatement penser à Cloud Storage.

Construire et opérationnaliser des pipelines

![](Aspose.Words.e79873e8-3438-4e0d-ab81-7a553aabca8b.012.png)

Apache Beam est une plateforme de programmation ouverte visant à unifier le traitement par lots et en continu.

Avant Apache Beam, il était nécessaire d'avoir deux pipelines distincts pour équilibrer la latence, le débit et la tolérance aux erreurs.

Dataflow est le service Apache Beam en tant que service, un service entièrement géré et à mise à l'échelle automatique qui exécute les pipelines Beam.

Les données continues peuvent arriver dans un ordre non séquentiel. La fenêtre de regroupement simple peut séparer les événements liés en fenêtres indépendantes, entraînant la perte d'informations sur les relations.

Le regroupement basé sur le temps (shuffling) surmonte cette limitation.

![](Aspose.Words.e79873e8-3438-4e0d-ab81-7a553aabca8b.013.png)

Les ressources Dataflow sont déployées à la demande, par travail, et le travail est constamment rééquilibré entre les ressources.

Dataflow résout de nombreux problèmes liés au traitement en continu, y compris les variations de taille (pics) et la croissance au fil du temps. Il peut se mettre à l'échelle tout en restant tolérant aux pannes. De plus, il dispose d'un modèle de programmation flexible et de méthodes pour travailler avec des données arrivant tardivement ou désordonnées.

![](Aspose.Words.e79873e8-3438-4e0d-ab81-7a553aabca8b.014.png)Tout le traitement des données est en retard ou est retardé simplement en raison de la latence dans la livraison du message d'événement.

La fenêtrage est trop compliqué à expliquer ici. Je veux simplement souligner que vous pourriez avoir besoin de le connaître, alors assurez-vous de le comprendre.

Il n'y a vraiment aucun remplacement pour la capacité de fenêtrage de Dataflow pour les données en continu.

![](Aspose.Words.e79873e8-3438-4e0d-ab81-7a553aabca8b.015.png)

La création de fenêtres génère des résultats individuels pour différentes tranches de temps d'événement.

La création de fenêtres divise une PCollection en morceaux finis en fonction du temps d'événement de chaque message. Cela peut être utile dans de nombreux contextes, mais est nécessaire lors de l'agrégation de données infinies.

Connaissez-vous les méthodes de fenêtrage de base, y compris la fenêtre temporelle fixe (comme une fenêtre quotidienne), les fenêtres glissantes et chevauchantes (comme les dernières 24 heures) et les fenêtres basées sur les sessions qui sont déclenchées pour capturer les rafales d'activité ?

![](Aspose.Words.e79873e8-3438-4e0d-ab81-7a553aabca8b.016.png)

N'oubliez pas d'étudier les entrées annexes (side-inputs). Si vous comprenez les entrées annexes, vous comprendrez nécessairement de nombreux concepts dépendants qui font partie de Dataflow.

Construction et opérationnalisation de l'infrastructure de traitement dans le contexte de GCP.

![](Aspose.Words.e79873e8-3438-4e0d-ab81-7a553aabca8b.017.png)

Toute la manipulation des données est retardée ou prend du retard par simple effet de latence dans la livraison du message d'événement.

Vous pouvez diffuser en continu des données non bornées vers BigQuery.

Pub/Sub garantit la livraison mais peut livrer les messages dans le désordre.

Si vous disposez d'un horodatage, Dataflow peut éliminer les doublons et déterminer l'ordre des messages.

![](Aspose.Words.e79873e8-3438-4e0d-ab81-7a553aabca8b.018.png)

BigQuery est un entrepôt de données peu coûteux pour les données tabulaires. Son coût est comparable à celui de Cloud Storage, il est donc logique de les ingérer dans BigQuery et de laisser les données là-bas. Ce schéma est utile car il montre la progression et les options d'entrée et de visualisation aux extrémités de la conception de solution courante.

![](Aspose.Words.e79873e8-3438-4e0d-ab81-7a553aabca8b.019.png)

Pourquoi Bigtable et pas Cloud Spanner ? Coût ! Notez que nous pouvons prendre en charge 100 000 qps avec 10 nœuds sur Bigtable, mais aurions besoin d'environ 150 nœuds sur Cloud Spanner.

[Labs : BigQuery Essentials](https://www.cloudskillsboost.google/course_sessions/3663395/labs/343580)
