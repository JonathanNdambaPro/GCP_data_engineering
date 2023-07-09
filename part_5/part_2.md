# Serverless Messaging avec Pub/Sub

Introduction à Pub/Sub, Alors que nous commençons ce module, je vous demanderais de garder l'esprit ouvert à de nouvelles façons de

faire des choses. Pub/Sub fait du streaming différemment de tout ce que vous avez probablement

utilisé dans le passé. Il peut s'agir d'un modèle différent de ce que vous avez vu auparavant.

![](Aspose.Words.faac24b9-2ef7-44fa-8bcc-5c53c0f9a1d5.001.png)

Pub/Sub offre un système de distribution et de livraison de données entièrement géré. Il peut être utilisé à de nombreuses fins. Il est le plus souvent utilisé pour découpler les différentes parties d'un système. Vous pouvez utiliser Pub/Sub pour connecter des applications au sein de Google Cloud, ainsi qu'avec des applications sur site ou dans d'autres clouds, afin de créer des solutions d'ingénierie de données hybrides. Avec Pub/Sub, les applications n'ont pas besoin d'être en ligne et disponibles en permanence. De plus, les différentes parties n'ont pas besoin de savoir comment communiquer entre elles, mais seulement avec Pub/Sub, ce qui simplifie la conception du système.

Tout d'abord, Pub/Sub n'est pas un logiciel ; c'est un service. Donc, comme tous les autres services sans serveur que nous avons étudiés, vous n'avez rien à installer pour utiliser Pub/Sub.

Des bibliothèques clientes Pub/Sub sont disponibles en C#, GO, Java, Node.js, Python et Ruby. Elles encapsulent les appels d'API REST, qui peuvent être effectués dans n'importe quel langage.

Il est également hautement disponible. Pub/Sub offre une durabilité des messages. Par défaut, il conserve vos messages pendant sept jours, dans le cas où vos systèmes seraient indisponibles et incapables de les traiter.

Enfin, Pub/Sub est également hautement évolutif. Google traite environ 100 millions de messages par seconde sur toute son infrastructure. En fait, c'était l'un des cas d'utilisation initiaux de Pub/Sub chez Google, permettant de distribuer le moteur de recherche et l'index à travers le monde, car nous conservons des copies locales de la recherche partout dans le monde, comme vous pouvez l'imaginer, afin de pouvoir fournir des résultats avec une latence minimale.

Si l'on réfléchit à la façon dont nous pourrions concevoir cela, nous parcourons l'ensemble du World Wide Web, nous devons donc envoyer l'intégralité du Web dans le monde. Soit cela, soit nous aurions besoin de multiples crawlers partout dans le monde, mais alors nous aurions des problèmes de cohérence des données ; ils obtiendraient tous des index différents.

C'est pourquoi nous utilisons Pub/Sub pour la distribution. Lorsque le crawler parcourt le Web, il récupère chaque page du World Wide Web, et nous envoyons chaque page individuelle en tant que message sur Pub/Sub, qui est récupéré par toutes les copies locales de l'index de recherche pour être indexé.

Actuellement, Google indexe le Web toutes les deux semaines, ce qui est le plus lent, jusqu'à plus d'une fois par heure, par exemple sur les sites d'actualités très populaires. En moyenne, Google indexe le Web trois fois par jour. Ainsi, ce que nous faisons, c'est envoyer l'intégralité du World Wide Web via Pub/Sub trois fois par jour. Cela explique comment Pub/Sub parvient à scaler.

Pub/Sub est un service conforme à la norme HIPAA, offrant des contrôles d'accès détaillés et un chiffrement de bout en bout. Les messages sont chiffrés en transit et au repos. Les messages sont stockés dans plusieurs emplacements pour assurer la durabilité et la disponibilité.

Vous pouvez contrôler les caractéristiques de votre solution Pub/Sub en fonction du nombre de producteurs, du nombre de souscripteurs, de la taille et du nombre de messages. Ces facteurs offrent un compromis entre l'évolutivité, la latence réduite et le débit élevé.

![](Aspose.Words.faac24b9-2ef7-44fa-8bcc-5c53c0f9a1d5.002.png)

Comment fonctionne Pub/Sub ? Le modèle est très simple. L'histoire de Pub/Sub est l'histoire de deux structures de données, le "Topic" (sujet) et la "Subscription" (abonnement). Le "Topic" et la "Subscription" sont des abstractions qui existent indépendamment de tout travailleur, abonné, etc., dans le framework Pub/Sub. Le client Pub/Sub qui crée le "Topic" est appelé le "Publisher" (éditeur). Et le client Pub/Sub qui crée la "Subscription" est appelé le "Subscriber" (abonné).

Dans cet exemple, la "Subscription" est abonnée au "Topic".

Pour recevoir des messages publiés sur un sujet, vous devez créer une "Subscription" pour ce sujet. Seuls les messages publiés sur le sujet après la création de la "Subscription" sont disponibles pour les applications abonnées. La "Subscription" connecte le sujet à une application abonnée qui reçoit et traite les messages publiés sur le sujet.

Un sujet peut avoir plusieurs "Subscriptions", mais une "Subscription" donnée appartient à un seul sujet.

![](Aspose.Words.faac24b9-2ef7-44fa-8bcc-5c53c0f9a1d5.003.png)

Essentiellement, il s'agit d'un bus de messagerie d'entreprise. Alors, comment cela fonctionne-t-il ?

Comme vous le voyez ici, il y a un sujet RH qui concerne les événements liés aux nouvelles embauches. Par exemple, une nouvelle personne rejoint votre entreprise et cette notification devrait permettre à d'autres applications qui doivent être informées de l'arrivée d'un nouvel utilisateur de s'abonner et de recevoir ce message.

Quelles applications pourraient vous informer qu'une nouvelle personne a rejoint l'entreprise ?

![](Aspose.Words.faac24b9-2ef7-44fa-8bcc-5c53c0f9a1d5.004.png)

Un exemple est l'Annuaire de l'entreprise. C'est un client de l'Abonnement également appelé Abonné. Cependant, Pub/Sub n'est pas limité à un Abonné ou à un Abonnement unique.

![](Aspose.Words.faac24b9-2ef7-44fa-8bcc-5c53c0f9a1d5.005.png)

Voici plusieurs Abonnements et plusieurs Abonnés. Peut-être que le Système des Installations doit être informé de l'arrivée d'un nouvel employé pour la création de badges, et que le système de provisionnement de la comptabilité doit être informé pour la paie. Chaque Abonnement garantit la livraison du message au service.

Ces clients abonnés sont découplés les uns des autres et isolés de l'éditeur. En fait, nous verrons plus tard que le Système des Ressources Humaines peut se déconnecter après avoir envoyé son message au Sujet des Ressources Humaines, et le message sera quand même livré aux abonnés.

Ces exemples montrent un Abonnement et un Abonné. Mais il est en réalité possible d'avoir plusieurs Abonnés pour un seul Abonnement.

![](Aspose.Words.faac24b9-2ef7-44fa-8bcc-5c53c0f9a1d5.006.png)

Dans cet exemple, le système d'activation de badge de GCP nécessite l'intervention d'un être humain pour activer le badge. Il y a plusieurs travailleurs, mais tous ne sont pas disponibles en permanence. Pub/Sub rend le message disponible pour tous les travailleurs. Cependant, une seule personne doit récupérer le message et le traiter. Cela s'appelle une souscription par extraction (Pull Subscription). Les autres exemples sont des souscriptions par envoi (Push Subscriptions).

![](Aspose.Words.faac24b9-2ef7-44fa-8bcc-5c53c0f9a1d5.007.png)

Maintenant, un nouveau sous-traitant arrive. Au lieu de passer par le système des ressources humaines (HR System), il passe par le bureau du fournisseur (Vendor Office). Les mêmes types d'actions doivent être effectuées pour ce travailleur. Il doit être répertorié dans l'annuaire de l'entreprise. Ensuite, les installations doivent lui attribuer un bureau. La provision des comptes doit configurer son identité et ses comptes d'entreprise. Et le système d'activation des badges doit imprimer et activer son badge de sous-traitant. Un message peut être publié par le bureau du fournisseur sur le sujet RH (HR Topic). Le bureau du fournisseur et le système des ressources humaines sont totalement indépendants l'un de l'autre, mais peuvent utiliser les mêmes services de l'entreprise.

Vous pouvez voir à partir de cette illustration à quel point le service Pub/Sub est important. Par conséquent, il bénéficie de la plus haute priorité.

![](Aspose.Words.faac24b9-2ef7-44fa-8bcc-5c53c0f9a1d5.008.png)

Lorsque vous recevez des messages à partir d'un abonnement avec un filtre, vous ne recevez que les messages qui correspondent au filtre. Le service Pub/Sub reconnaît automatiquement les messages qui ne correspondent pas au filtre. Vous pouvez filtrer les messages en fonction de leurs attributs. Vous ne supportez pas de frais de sortie pour les messages que Pub/Sub reconnaît automatiquement. Vous supportez des frais de livraison de messages et des frais de stockage liés à la recherche pour ces messages.

Vous pouvez créer un abonnement avec un filtre en utilisant la Console Cloud, l'outil en ligne de commande gcloud ou l'API Pub/Sub.

Vous avez appris en général ce que fait Pub/Sub. Ensuite, vous apprendrez comment cela fonctionne et de nombreuses fonctionnalités avancées qu'il offre.

## Pub/Sub Push versus Pull

![](Aspose.Words.faac24b9-2ef7-44fa-8bcc-5c53c0f9a1d5.009.png)

Nous commencerons par comprendre la répartition des messages et les différents motifs. Ici, les différentes couleurs représentent des messages différents.

![](Aspose.Words.faac24b9-2ef7-44fa-8bcc-5c53c0f9a1d5.010.png)

Le premier schéma est simplement un flux basique sans interruption, où un éditeur publie des messages dans un sujet, qui sont ensuite consommés par un abonné unique via un abonnement unique.

![](Aspose.Words.faac24b9-2ef7-44fa-8bcc-5c53c0f9a1d5.011.png)

Le deuxième modèle est le "fan in" ou l'équilibrage de charge. Plusieurs éditeurs peuvent publier le même sujet, et plusieurs abonnés peuvent extraire de la même souscription, en utilisant le traitement parallèle. Ce que vous voyez ici, ce sont deux éditeurs différents qui envoient trois messages différents, tous sur le même sujet. Cela signifie que la souscription recevra les trois messages.

![](Aspose.Words.faac24b9-2ef7-44fa-8bcc-5c53c0f9a1d5.012.png)

Le troisième schéma est la propagation, où vous avez de nombreux cas d'utilisation pour la même donnée, et toutes les données sont envoyées à de nombreux abonnés différents. Comme vous pouvez le voir ici, nous avons deux abonnements. Donc, les deux vont recevoir les messages, à la fois le message rouge et le message bleu.

![](Aspose.Words.faac24b9-2ef7-44fa-8bcc-5c53c0f9a1d5.013.png)

Pub/Sub permet à la fois la livraison par Push et Pull.

Le modèle Pull

Dans le modèle Pull, vos clients sont des abonnés et ils appellent périodiquement les messages, et Pub/Sub se contente de livrer les messages depuis le dernier appel.

Dans le modèle Pull, vous devrez acknowledge (reconnaître) le message en tant qu'étape distincte. Ainsi, ce que vous voyez ici, c'est que nous faisons initialement l'appel aux abonnés, ils récupèrent les messages, ils reçoivent un message en retour, puis, séparément, ils reconnaissent ce message.

La raison à cela est que les files d'attente de pull sont souvent utilisées pour mettre en œuvre un système de file d'attente pour le travail à effectuer. Ainsi, vous ne voulez pas acknowledge (reconnaître) le message tant que vous ne l'avez pas réellement et que vous ne l'avez pas traité, sinon vous risquez de perdre le message si le système tombe en panne. Par conséquent, nous recommandons généralement d'attendre jusqu'à ce que vous l'ayez obtenu pour le reconnaître.

Dans le modèle Pull, les messages sont stockés pendant une durée maximale de sept jours. Le modèle Push

Dans le modèle Push, il utilise en réalité un point de terminaison HTTP. Vous enregistrez un webhook en tant qu'abonnement, et l'infrastructure Pub/Sub elle-même vous appelle avec les derniers messages.

Dans le cas de Push, vous répondez simplement avec "statut 200 ok" pour l'appel HTTP, et cela indique à Pub/Sub que la livraison du message a réussi.

Il utilisera en fait le taux de vos réponses réussies pour s'auto-limiter afin de ne pas surcharger votre travailleur.

![](Aspose.Words.faac24b9-2ef7-44fa-8bcc-5c53c0f9a1d5.014.png)

La façon dont les accusés de réception fonctionnent est de garantir que chaque message soit livré au moins une fois. Ce qui se passe, c'est que lorsque vous accusez réception d'un message, vous le faites sur une base d'abonnement. Ainsi, si vous avez deux abonnements, que l'un est accusé de réception et que l'autre ne l'est pas, celui qui a été accusé de réception continuera de recevoir les messages. Pub/Sub continuera d'essayer de livrer le message pendant une période pouvant aller jusqu'à sept jours tant qu'il n'est pas accusé de réception.

Il existe également un mécanisme de relecture qui vous permet de revenir en arrière dans le temps et de rejouer les messages, mais dans tous les cas, vous pourrez toujours remonter jusqu'à sept jours.

Vous pouvez également définir le délai d'accusé de réception par abonnement. Ainsi, si vous savez qu'en moyenne il vous faut 15 secondes pour traiter un message dans votre file de travail, vous pouvez définir votre délai d'accusé de réception à 20 secondes. Cela garantira qu'il n'essaie pas de redistribuer les messages.

![](Aspose.Words.faac24b9-2ef7-44fa-8bcc-5c53c0f9a1d5.015.png)

La configuration d'un sujet avec une rétention de messages vous offre plus de flexibilité, permettant à toute souscription attachée au sujet de remonter dans le temps et de rejouer des messages déjà confirmés. La rétention des messages du sujet permet également à une souscription de rejouer des messages publiés avant la création de cette souscription. Des instantanés sont utilisés pour rendre la relecture extrêmement efficace.

Si la rétention des messages du sujet est activée, les coûts de stockage des messages conservés par le sujet seront facturés au projet du sujet.

![](Aspose.Words.faac24b9-2ef7-44fa-8bcc-5c53c0f9a1d5.016.png)

Les abonnés peuvent travailler individuellement ou en groupe. Si nous n'avons qu'un seul abonné, il recevra chaque message livré via cet abonnement. Cependant, vous pouvez configurer des groupes de travail en ayant plusieurs abonnés partageant le même abonnement. Dans ce cas, le message sera distribué, de sorte que le message un et trois iront à l'abonnement 1, et le message deux ira à l'abonnement 2. Et c'est simplement aléatoire en fonction du moment où il extrait les messages tout au long de la journée.

Dans le cas d'un abonnement Push, vous n'avez qu'un seul point de terminaison web, vous aurez donc généralement qu'un seul abonné. Cependant, cet abonné peut être une application App Engine standard ou une image de conteneur Cloud Run qui s'adapte automatiquement. Ainsi, il s'agit d'un seul point de terminaison web, mais il peut avoir des travailleurs qui s'adaptent automatiquement en arrière-plan. Et c'est en réalité un très bon modèle.

## La publication avec le code Pub/Sub

![](Aspose.Words.faac24b9-2ef7-44fa-8bcc-5c53c0f9a1d5.017.png)

Voici la traduction du texte dans le contexte de GCP :

Regardons maintenant un peu de code. Cet exemple utilise la bibliothèque cliente pour Pub/Sub.

Si nous voulons publier le message, nous commençons par créer le sujet (topic).

Ensuite, nous pouvons publier le sujet en ligne de commande.

Plus couramment, cela se fera dans le code. Ici, nous obtenons un PublisherClient, créons un sujet et publions le message.

Remarquez la lettre b devant "Mon premier message !". C'est parce que Pub/Sub envoie simplement des octets bruts. Cela signifie que vous n'êtes pas limité au texte seul. Vous pouvez envoyer d'autres données, comme des images si vous le souhaitez. La limite est de 10 Mo.

Il existe également des attributs supplémentaires que vous pouvez inclure dans les messages. Dans cet exemple, vous voyez "auteur" égal à "dylan". Pub/Sub suivra ces attributs pour permettre à vos systèmes aval de récupérer des métadonnées sur vos messages sans avoir à les inclure tous dans le message et à les analyser. Ainsi, au lieu de les sérialiser et de les désérialiser, il se contentera de suivre ces paires clé-valeur.

Certains d'entre eux ont une signification spéciale. Nous verrons certains d'entre eux sous peu.

![](Aspose.Words.faac24b9-2ef7-44fa-8bcc-5c53c0f9a1d5.018.png)

Pour vous abonner à Pub/Sub en utilisant la méthode Pull, le code est similaire.

- Sélectionnez le sujet.
- Nommez l'abonnement.
- Il s'agit d'un abonnement pull, nous définirons donc un rappel (callback).

![](Aspose.Words.faac24b9-2ef7-44fa-8bcc-5c53c0f9a1d5.019.png)

Lorsque vous effectuez une souscription de type pull, cela ressemble à ceci. Vous pouvez extraire les messages depuis la ligne de commande. Vous verrez cela dans le laboratoire. Par défaut, il récupère simplement un message, le message le plus récent, mais vous pouvez définir une limite avec le paramètre "dash-dash limit". Peut-être souhaitez-vous extraire 10 messages à la fois, vous pouvez essayer cela dans le laboratoire.

![](Aspose.Words.faac24b9-2ef7-44fa-8bcc-5c53c0f9a1d5.020.png)

Vous pouvez également publier des messages par lots. Cela évite simplement les frais généraux liés à l'appel de messages individuels du côté de la publication. Cela permet au moteur de publication Pub/Sub d'attendre et d'envoyer 10 ou 50 messages à la fois, ce qui augmente l'efficacité. Cependant, si vous attendez 50 messages, cela signifie que le premier a désormais une latence associée. Il s'agit donc d'un compromis dans votre système. Que souhaitez-vous optimiser ? Quoi qu'il en soit, même si vous publiez par lots, les messages sont toujours livrés un par un à vos abonnés. Nous pratiquerons cette technique dans le laboratoire.

![](Aspose.Words.faac24b9-2ef7-44fa-8bcc-5c53c0f9a1d5.021.png)

Voici comment vous pouvez définir le mode batch dans du code Python.

Explorez la documentation pour découvrir d'autres options de commande et paramètres.

![](Aspose.Words.faac24b9-2ef7-44fa-8bcc-5c53c0f9a1d5.022.png)

Si les messages ont la même clé de tri et se trouvent dans la même région, vous pouvez activer la mise en ordre des messages et recevoir les messages dans l'ordre où le service Pub/Sub les reçoit.

Lorsque le service Pub/Sub redélivre un message avec une clé de tri, le service Pub/Sub redélivre également tous les messages suivants avec la même clé de tri, y compris les messages accusés de réception. Si à la fois la mise en ordre des messages et un sujet de lettre morte sont activés sur un abonnement, l'ordre peut ne pas être préservé, car Pub/Sub transfère les messages vers les sujets de lettre morte de manière optimale.

Pour recevoir les messages dans l'ordre, définissez la propriété de mise en ordre des messages sur l'abonnement à partir duquel vous recevez les messages. Veuillez noter que recevoir les messages dans l'ordre peut augmenter la latence.

Vous pouvez définir la propriété de mise en ordre des messages lors de la création d'un abonnement à l'aide de la console Cloud, de l'outil en ligne de commande gcloud ou de l'API Pub/Sub.

![](Aspose.Words.faac24b9-2ef7-44fa-8bcc-5c53c0f9a1d5.023.png)

Pub/Sub va également nous aider en termes de résilience du streaming, ou de mise en mémoire tampon. Que se passe-t-il si vos systèmes sont surchargés par de grands volumes de transactions, comme lors du Black Friday ? Ce dont vous avez réellement besoin, c'est d'une sorte de tampon ou de file d'attente afin de pouvoir envoyer les messages seulement aussi rapidement que les systèmes sont capables de les traiter. Pub/Sub dispose de cette capacité intégrée.

![](Aspose.Words.faac24b9-2ef7-44fa-8bcc-5c53c0f9a1d5.024.png)

Récapitulons donc. Lorsque vous regardez l'exemple sur cette diapositive, dans l'exemple de gauche, une surcharge de données arrivantes provoque une augmentation du trafic. Cela surcharge les ressources de l'application, comme illustré par la fumée. Une solution à ce problème consiste à dimensionner l'application pour gérer le pic de trafic le plus élevé, plus une capacité supplémentaire en tant que tampon de sécurité. Cela gaspille non seulement des ressources, qui doivent être maintenues à pleine capacité même lorsqu'elles ne sont pas utilisées, mais cela crée également une recette pour une attaque par déni de service distribué en créant une limite supérieure à laquelle l'application cessera de se comporter normalement et présentera un comportement non déterministe.

La solution de droite utilise Pub/Sub en tant qu'intermédiaire, recevant et stockant les données jusqu'à ce que l'application dispose des ressources nécessaires pour les traiter, soit en traitant la file d'attente de travail, soit en adaptant automatiquement l'échelle pour répondre à la demande.

![](Aspose.Words.faac24b9-2ef7-44fa-8bcc-5c53c0f9a1d5.025.png)

Les enregistrements erronés peuvent bloquer ou faire échouer votre pipeline. Nous vous recommandons vivement de mettre en place une file d'attente des messages erronés (dead-letter queue) et une journalisation des erreurs afin de prévenir ces modes de défaillance. Cela peut aider à détecter les problèmes dans le code utilisateur et/ou la structure des données.

![](Aspose.Words.faac24b9-2ef7-44fa-8bcc-5c53c0f9a1d5.026.png)

L'idée derrière le "exponential backoff" est d'ajouter des délais de plus en plus longs entre les tentatives de réessai. Après le premier échec de livraison, Pub/Sub attendra un délai minimal de backoff avant de réessayer. Pour chaque échec consécutif sur ce message, davantage de temps sera ajouté au délai, jusqu'à atteindre un délai maximal. Les intervalles de délai maximum et minimum ne sont pas fixes et doivent être configurés en fonction des facteurs locaux de votre application.

![](Aspose.Words.faac24b9-2ef7-44fa-8bcc-5c53c0f9a1d5.027.png)

Journaux d'audit Cloud

Cloud Audit Logs conserve trois journaux d'audit pour chaque projet, dossier et organisation Google Cloud : Activité d'administration, Accès aux données et Événement système.

Les journaux d'audit d'activité d'administration contiennent des entrées de journal pour les appels d'API ou autres actions administratives qui modifient la configuration ou les métadonnées des ressources.

Les journaux d'audit d'accès aux données contiennent des appels d'API qui lisent la configuration ou les métadonnées des ressources, ainsi que des appels d'API déclenchés par l'utilisateur qui créent, modifient ou lisent des données de ressources fournies par l'utilisateur.

Les journaux d'audit d'activité d'administration sont toujours écrits ; vous ne pouvez pas les configurer ou les désactiver.

Les journaux d'audit d'accès aux données sont désactivés par défaut car ils peuvent être assez volumineux ; ils doivent être explicitement activés pour être écrits.

Métriques de Cloud Logging

Pub/Sub rapporte des métriques à Cloud Logging, notamment pubsub\_topic et pubsub\_subscription, que vous pouvez surveiller par rapport à l'utilisation des quotas de service dans un tableau de bord, et pour définir des notifications et des alertes. Authentification

L'authentification est assurée par des comptes de service. Vous pouvez également authentifier directement les utilisateurs par leurs comptes d'utilisateur et leur identité est consignée dans les journaux d'audit. Cependant, l'authentification par compte utilisateur n'est pas recommandée.

Contrôle d'accès

Le contrôle d'accès est assuré par IAM.

[Lab : Traitement de données en streaming, publier des données en streaming dans PubSub.](https://www.cloudskillsboost.google/course_sessions/3849359/labs/345012)
