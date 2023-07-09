Sécurité, Politique et Fiabilité

Conception pour la sécurité et la conformité

Conception pour la sécurité et la conformité.

La sécurité est un terme large. Elle englobe la confidentialité, l'authentification, l'autorisation, la gestion des identités et des accès. Elle peut inclure la détection d'intrusions, la mitigation des attaques, la résilience et la récupération. Ainsi, la sécurité se retrouve réellement dans l'ensemble des technologies, et pas uniquement à un seul endroit.

Il est nécessaire de prendre en compte la granularité du contrôle pour chaque service. L'exercice consiste à imaginer deux personnes : l'une doit avoir accès et l'autre ne doit pas y avoir accès. Quelle est l'unité ou le degré de contrôle le plus petit que la technologie prend en charge ? Pouvez-vous distinguer la sécurité au niveau d'un champ individuel, d'une ligne ou d'un enregistrement, de colonnes, d'une base de données ou d'une entité spécifique, ou uniquement des types d'actions qui peuvent être effectuées sur le service ?

![](Aspose.Words.deb3f7c9-4b41-4ecc-8a36-2843102a6613.001.png)

Mémorisez une liste de contrôle de sécurité. Parfois, il suffit de parcourir une liste pour identifier rapidement une solution.

Un concept clé est d'attribuer des rôles aux groupes et d'utiliser l'appartenance à un groupe pour accorder des autorisations aux individus.

Comment le service sera-t-il surveillé ou signalé, et à quelle fréquence ces éléments seront-ils examinés ?

Enfin, vous devez savoir quels types de journaux et de rapports sont disponibles pour chaque technologie.

![](Aspose.Words.deb3f7c9-4b41-4ecc-8a36-2843102a6613.002.png)

Une politique est définie sur une ressource, et chaque politique contient un ensemble de rôles et de membres de rôle.

Les ressources héritent des politiques de leurs parents. Ainsi, une politique peut être définie sur une ressource, par exemple un service. Et une autre politique peut être définie sur un parent, tel qu'un projet qui contient ce service.

La politique finale est l'union de la politique parente et de la politique de la ressource.

Que se passe-t-il lorsque ces deux politiques entrent en conflit ? Que se passe-t-il si la politique sur la ressource ne donne accès qu'à un seul compartiment de stockage Cloud et restreint l'accès à tous les autres compartiments. Cependant, au niveau du projet, une règle existe qui accorde l'accès à tous les compartiments du projet ? Quelle règle l'emporte ? La règle plus restrictive sur la ressource, ou la règle plus générale sur le projet ?

Si la politique parente est moins restrictive, elle remplace une politique de ressource plus restrictive. Ainsi, dans ce cas, la politique du projet l'emporte.

![](Aspose.Words.deb3f7c9-4b41-4ecc-8a36-2843102a6613.003.png)

Les dossiers correspondent bien à la structure organisationnelle. C'est une manière d'isoler des organisations, des utilisateurs ou des produits tout en leur permettant de partager la facturation et les ressources de l'entreprise.

![](Aspose.Words.deb3f7c9-4b41-4ecc-8a36-2843102a6613.004.png)

Il existe de nombreuses options de chiffrement pour les données au repos et en stockage. Le chiffrement par défaut des données au repos utilise le système de gestion des clés (KMS) pour générer des KEK (clés de chiffrement de clé) et des DEK (clés de chiffrement de données).

Lorsque vous utilisez Dataproc, les données du cluster et des tâches sont stockées sur des disques persistants (PD) associés aux machines virtuelles Compute Engine de votre cluster et dans un compartiment Cloud Storage. Ces données PD et compartiment sont chiffrées à l'aide d'une clé de chiffrement de données (DEK) et d'une clé de chiffrement de clé (KEK) générées par Google.

Les clés de chiffrement gérées par le client (CMEK) sont une fonctionnalité qui vous permet de créer, d'utiliser et de révoquer la clé de chiffrement de clé (KEK). Google conserve toujours la clé de chiffrement de données (DEK).

Le chiffrement côté client signifie simplement que vous chiffrez les données ou le fichier avant de les télécharger dans le cloud.

![](Aspose.Words.deb3f7c9-4b41-4ecc-8a36-2843102a6613.005.png)

Concepts clés : Cloud Armor, Cloud Load Balancing, Cloud Firewall Rules, Comptes de service, séparation en frontal et en arrière-plan, isolation des ressources en utilisant des comptes de service distincts entre les services.

En raison de la disponibilité omniprésente des règles de pare-feu, vous n'avez pas besoin d'installer un routeur dans le réseau à un emplacement particulier pour bénéficier d'une protection pare-feu. Cela signifie que vous pouvez superposer les pare-feu comme indiqué dans cet exemple.

Grâce au support généralisé des comptes de service, vous pouvez "verrouiller" les connexions entre les composants.

Lorsque vous êtes confronté à une question de sécurité lors d'un examen (ou dans la pratique), déterminez les technologies/services spécifiques dont il est question (authentification, chiffrement), par exemple. Ensuite, déterminez exactement quels sont les objectifs pour une sécurité suffisante. S'agit-il de dissuasion ? S'agit-il de respecter une norme de conformité ? L'objectif est-il d'éliminer un risque ou une vulnérabilité particulière ? Cela vous aidera à définir la portée d'une solution, que ce soit lors d'un examen ou dans une application.

Effectuer un contrôle qualité

![](Aspose.Words.deb3f7c9-4b41-4ecc-8a36-2843102a6613.006.png)

La surveillance intégrée des services peut simplifier l'activité de surveillance d'une solution. Vous pouvez obtenir des graphiques pour plusieurs valeurs dans un seul tableau de bord. Il est possible de mettre en évidence les valeurs d'application en tant que métriques personnalisées dans Cloud Monitoring.

Ces graphiques montrent l'utilisation des slots, les slots disponibles et les requêtes en cours pendant une période d'une heure dans BigQuery.

Le conseil de l'examen ici est que vous pouvez surveiller l'infrastructure et les services de données avec Cloud Monitoring.

![](Aspose.Words.deb3f7c9-4b41-4ecc-8a36-2843102a6613.007.png)

TensorBoard est un ensemble d'outils de visualisation conçus spécifiquement pour vous aider à visualiser TensorFlow dans le contexte de GCP (Google Cloud Platform).

- Graphique TensorFlow
- Tracer des métriques quantitatives
- Transmettre et tracer des données supplémentaires

Les événements en haut à gauche montrent la "perte" (loss).

Les autres graphiques montrent le graphique du modèle linéaire tel que construit par TensorFlow.

L'astuce ici est que la surveillance spécifique au service peut être disponible. TensorBoard est un exemple de surveillance adaptée à TensorFlow.

![](Aspose.Words.deb3f7c9-4b41-4ecc-8a36-2843102a6613.008.png)

Voici quelques conseils pour garantir la fiabilité avec l'apprentissage automatique (Machine Learning) dans le contexte de GCP.

Il y a plusieurs choses que vous pouvez faire pour améliorer la fiabilité. Par exemple, vous pouvez détecter les défaillances des machines, créer des fichiers de point de contrôle et récupérer des pannes. Vous pouvez également contrôler la fréquence des évaluations pour rendre l'ensemble du processus plus efficace.

Le conseil présenté est que "Dans TensorFlow, les données sont souvent divisées en ensembles d'entraînement et d'évaluation, ce qui permet de mesurer l'efficacité et d'apporter des améliorations."

Donc, le conseil général est qu'il peut y avoir des processus de qualité ou des processus de fiabilité intégrés à la technologie, comme cela est démontré ici.

![](Aspose.Words.deb3f7c9-4b41-4ecc-8a36-2843102a6613.009.png)

Le conseil d'examen ici est que le dépannage et l'amélioration de la qualité des données et des performances de traitement sont répartis dans toutes les technologies. Il serait judicieux de vous assurer de connaître les principales méthodes de dépannage pour chaque technologie et service d'ingénierie des données.

La sécurité et le dépannage sont des sujets transversaux qui touchent toutes les technologies. Vous devez les rechercher dans chaque domaine technologique et approfondir la documentation au besoin.

![](Aspose.Words.deb3f7c9-4b41-4ecc-8a36-2843102a6613.010.png)

La formation aborde bien les mécanismes de génération et de rapports. Cependant, elle n'explique pas explicitement comment présenter et défendre des politiques.

Ce sujet fait partie du programme d'examen. Il s'agit d'une compétence professionnelle générale plutôt que d'une compétence technique et n'est pas spécifiquement abordé dans la formation technique de Google. Néanmoins, il fait partie du travail et peut être inclus dans l'examen. Je vous suggère donc de vous assurer de le connaître, même s'il ne figure pas dans notre formation.

Garantir la fiabilité

Fiable signifie que le service produit des résultats cohérents et fonctionne comme prévu. Si nous devions le quantifier, ce serait une mesure de la durée pendant laquelle le service effectue sa fonction prévue.

![](Aspose.Words.deb3f7c9-4b41-4ecc-8a36-2843102a6613.011.png)

Disponibilité et durabilité sont des valeurs concrètes dans le contexte de GCP et ne sont généralement pas de 100%.

La disponibilité signifie que le service est accessible à la demande. C'est une mesure du pourcentage de temps où l'élément est dans un état opérationnel.

La durabilité concerne la perte de données. Cela signifie que les données ne disparaissent pas et que les informations ne sont pas perdues avec le temps. Plus précisément, c'est une mesure du taux auquel les données sont perdues.

Ces qualités sont liées. Si un service échoue -- connaît une panne -- alors il ne produit pas de résultats fiables pendant cette période.

![](Aspose.Words.deb3f7c9-4b41-4ecc-8a36-2843102a6613.012.png)

Un service alternatif ou un basculement pourrait remettre le service en ligne et le rendre à nouveau disponible. En général, une panne qui entraîne une perte de données nécessite plus de temps pour récupérer. Si cela est récupéré à partir d'une sauvegarde ou d'un plan de reprise après sinistre. Cependant, notez que si vous disposez d'un service alternatif tel qu'une copie qui peut être rapidement activée, il peut y avoir peu ou pas de perte de données ou de temps de récupération.

Il est donc important de prendre en compte les exigences commerciales pour récupérer à partir de différents types de problèmes, et combien de temps est accordé pour chaque type de récupération. Par exemple, une reprise après sinistre d'une semaine peut être acceptable pour des dégâts causés par une inondation à une devanture de magasin. En revanche, la perte d'une transaction financière peut être totalement inacceptable, il est donc nécessaire que la transaction elle-même soit atomique, sauvegardée et redondante.

![](Aspose.Words.deb3f7c9-4b41-4ecc-8a36-2843102a6613.013.png)

La simple augmentation de l'échelle peut améliorer la fiabilité. Si la solution est conçue pour être tolérante aux pannes, une augmentation de l'échelle peut améliorer la fiabilité.

Dans cet exemple, si le service s'exécute sur un nœud et que ce dernier tombe en panne, le service est complètement indisponible. En revanche, si le service a été redimensionné et s'exécute sur neuf nœuds, et qu'un nœud tombe en panne, le service n'est indisponible qu'à hauteur de 11%.
