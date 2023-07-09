# Analyse des Big Data avec des notebooks

## Qu’est-ce qu’un Notebook?

![](Aspose.Words.658a9cc3-ad85-4237-9def-ed668be6d357.001.png)

Les outils de développement logiciel standard ne sont pas très efficaces pour écrire du code pour l'analyse de données et l'apprentissage automatique.

La programmation pour l'analyse de données et l'apprentissage automatique implique souvent l'examen de graphiques, l'exécution répétée de petits morceaux de code avec de légères modifications et la nécessité fréquente d'afficher des résultats. Exécuter des scripts entiers de manière itérative pour cette tâche est fastidieux.

Ces problèmes ont été à l'origine du développement des notebooks.

Les environnements de notebooks intègrent parfaitement les commentaires, les graphiques et le code. Au lieu d'avoir un script qui effectue une analyse, les notebooks organisent des morceaux de code individuellement exécutables dans des cellules.

![](Aspose.Words.658a9cc3-ad85-4237-9def-ed668be6d357.002.png)

Avez-vous déjà utilisé Google Docs ? Comment est-ce différent des documents édités dans un éditeur de bureau ?

Avez-vous déjà rempli vos déclarations de revenus en ligne ? Comment cette expérience diffère-t-elle de celle d'utiliser un programme de bureau ?

Il y a de nombreux avantages, mais un aspect clé est la collaboration. Vous n'avez pas besoin d'envoyer des documents par e-mail aller-retour.

Quand j'ai commencé à faire de la recherche scientifique, collaborer sur un seul résultat était pénible. J'écrivais du code et créais un graphique. Ensuite, je prenais une capture d'écran, créais un fichier image, l'insérais dans un document, créais un PDF et l'envoyais à mon collaborateur. Quelques heures plus tard, mon collègue me disait : "C'est génial, mais pourrais-tu ajouter les données d'une année supplémentaire ? Ça semble un peu vide." Et je recommençais tout le processus. Pourquoi ? Parce que le PDF que j'avais envoyé n'était pas modifiable. Les allers-retours prenaient beaucoup de temps.

Entrez les notebooks Python. J'écrivais le code, créais le graphique, rédigeais des commentaires et envoyais le lien du notebook à mon collègue. Ainsi, lorsque mon collègue voulait ajouter une année de données supplémentaire, il pouvait simplement modifier la cellule, regarder le nouveau graphique et dire : "Regarde, c'est bien mieux." Et c'était génial ; nous avions maintenant un meilleur notebook pour l'étape suivante. Un problème avec les notebooks traditionnels : qui exécute le serveur qui héberge ces pages ? À qui appartient la machine ? Si c'est la mienne et que ma machine se met en veille, mon collègue ne peut pas travailler !

Lorsque vos notebooks sont hébergés dans le cloud, vous pouvez facilement développer ensemble. Et tout comme les Google Docs sont disponibles même lorsque votre ordinateur est éteint, les notebooks le sont aussi lorsque vous les exécutez dans le Cloud.

Pour partager un notebook au sein d'un projet, les autres utilisateurs peuvent simplement se "connecter" à la machine virtuelle et travailler en utilisant l'URL. Une autre façon de partager des notebooks est d'utiliser des systèmes de contrôle de version, tels que Git.

![](Aspose.Words.658a9cc3-ad85-4237-9def-ed668be6d357.003.png)

Lancer un notebook peut être fait en un clic. Vous avez peut-être entendu parler des notebooks Jupyter. Les notebooks Jupyter sont essentiellement synonymes de Notebooks sur Google Cloud (Vertex AI et AI Platform). L'environnement Python fourni dispose d'une bibliothèque d'apprentissage automatique standard préinstallée.

![](Aspose.Words.658a9cc3-ad85-4237-9def-ed668be6d357.004.png)

Les Notebooks utilisent la dernière version open source de JupyterLab, la norme industrielle.

![](Aspose.Words.658a9cc3-ad85-4237-9def-ed668be6d357.005.png)

Lorsque vous configurez initialement le matériel de vos Notebooks dans le contexte de GCP, vous pouvez utiliser n'importe quel type d'instance Compute Engine.

![](Aspose.Words.658a9cc3-ad85-4237-9def-ed668be6d357.006.png)

Vous pouvez également facilement ajuster le matériel sous-jacent, y compris les types de machines.

![](Aspose.Words.658a9cc3-ad85-4237-9def-ed668be6d357.007.png)

Compute Engine propose des Unités de traitement graphique, ou GPUs, que vous pouvez ajouter à vos instances de machines virtuelles. Vous pouvez utiliser ces GPUs pour accélérer des charges de travail spécifiques sur vos VM, telles que l'apprentissage automatique et le traitement des données. Si vous n'avez pas attaché de GPUs lors de la création de votre VM, vous pouvez ajouter des GPUs à vos VM existantes en fonction de vos besoins applicatifs au fur et à mesure qu'ils se présentent. Si vous attachez des GPUs pendant ou après la création de la VM, vous pouvez les détacher de ces VM lorsque vous n'en avez plus besoin.

![](Aspose.Words.658a9cc3-ad85-4237-9def-ed668be6d357.008.png)

Notez que les instances de Notebooks sont traitées de la même manière que les instances standard de Compute Engine qui se trouvent dans vos projets. Si vous démarrez un Notebook, connectez-vous à la Console Cloud et accédez aux instances de VM. Vous verrez vos instances de Notebooks sous Compute Engine.

![](Aspose.Words.658a9cc3-ad85-4237-9def-ed668be6d357.009.png)

Comme mentionné précédemment, les Notebooks exécutent la dernière version de JupyterLab, qui dans ce cas est hébergée sur Compute Engine. Cela concerne le matériel et les bibliothèques. Pour la collaboration, les Notebooks sont intégrés à Git par défaut, vous permettant ainsi de versionner vos Notebooks.

Les Notebooks offrent également des connecteurs vers et depuis BigQuery, vous permettant d'importer facilement des données dans votre Notebook.

## BigQuery Magics et Liens avec Pandas

![](Aspose.Words.658a9cc3-ad85-4237-9def-ed668be6d357.010.png)

Vous êtes peut-être familier avec les fonctions magiques dans Jupyter labs. Les fonctions magiques vous permettent d'exécuter des commandes système à partir des cellules de notebook. Il existe des fonctions magiques pour vérifier le contenu de votre répertoire actuel. Vous pouvez également définir des fonctions magiques personnalisées. La fonction magique BigQuery présentée dans cette diapositive vous permet d'exécuter des requêtes BigQuery. Cela est utile pour vérifier le format, l'exactitude et les résultats des requêtes.

![](Aspose.Words.658a9cc3-ad85-4237-9def-ed668be6d357.011.png)

La fonction magique BigQuery vous permet de sauvegarder la sortie de la requête dans un DataFrame Pandas, afin de pouvoir le manipuler davantage.

Dans cet exemple, nous sauvegardons la sortie d'une requête dans un DataFrame Pandas nommé "df". Pandas est une bibliothèque numérique pour Python, qui affiche les données dans une structure tabulaire. Elle affiche également des métadonnées afin que vous puissiez effectuer des opérations telles que la description des DataFrames, les types d'objets et la génération de statistiques sommaires sur les colonnes.

C'est vraiment puissant de pouvoir extraire directement les résultats de la requête dans un DataFrame en seulement deux lignes de code. Gardez à l'esprit que vous travaillez dans un notebook et qu'il y aura une quantité limitée de mémoire. Vous ne voudriez donc pas accéder à BigQuery et extraire un jeu de données volumineux de plusieurs téraoctets ou plus. Utilisez plutôt une technique d'échantillonnage pour extraire un sous-ensemble des données.

![](Aspose.Words.658a9cc3-ad85-4237-9def-ed668be6d357.012.png)

Voici un exemple de la manière dont vous pouvez exécuter une requête BigQuery pour extraire des données dans deux objets de type data frame Pandas. Ensuite, un diagramme à barres simple est généré à partir du data frame.

[Lab : BigQuery dans JupyterLab sur Vertex AI](https://www.cloudskillsboost.google/course_sessions/3856018/labs/367832)
