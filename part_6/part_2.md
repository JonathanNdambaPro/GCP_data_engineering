# APIs de modèles d'apprentissage automatique préconstruits pour les données non structurées

## Les données non structurées sont difficiles

![](Aspose.Words.da23e318-859f-4c72-91fa-57fbf4443580.001.png)

Comme vous pouvez le voir sur cette diapositive, deux images sont affichées. L'une contient une page de journal et l'autre représente un événement sportif. Il se passe beaucoup de choses dans ces images et vraisemblablement, beaucoup d'informations utiles peuvent être extraites de chacune d'entre elles.

Par exemple, dans quelle langue est rédigé l'extrait de journal ? Que dit l'article ?

En quelle année a-t-il été publié ?

Quel sport est pratiqué dans l'image de droite ?

Quel drapeau est agité ?

La question importante est probablement de savoir comment nous pouvons extraire ces métadonnées. Possédons-nous une telle technologie ? En bref, la réponse est oui. Nous allons en parler dans ce module.

![](Aspose.Words.da23e318-859f-4c72-91fa-57fbf4443580.002.png)

Uniqlo a conçu un chatbot de shopping en utilisant Dialogflow, une offre d'intelligence artificielle de Google Cloud.

Dialogflow est une plateforme de compréhension du langage naturel qui facilite la conception et l'intégration d'une interface utilisateur conversationnelle dans les applications mobiles, les applications Web, les appareils, les bots, les systèmes de réponse vocale interactive, et ainsi de suite. En utilisant Dialogflow, il est possible de proposer de nouvelles façons engageantes aux utilisateurs d'interagir avec votre organisation.

Jetons un coup d'œil à d'autres cas d'utilisation de l'apprentissage automatique (ML) dans les entreprises.

<https://youtu.be/BwWg__HVfsM?t=4m41s>

![](Aspose.Words.da23e318-859f-4c72-91fa-57fbf4443580.003.png)

Prenons l'exemple d'Airbus. Airbus utilise l'apprentissage automatique pour différencier entre les nuages et la couverture neigeuse sur les images satellites.

Si vous êtes aussi perplexe que moi, les nuages se trouvent dans la partie supérieure droite de l'image de droite, mise en évidence en rouge. Le reste est de la neige. [https://cloud.google.com/blog/products/gcp/google-cloud-machine-learning-now-open-to-all- with-new-professional-services-and-education-programs](https://cloud.google.com/blog/products/gcp/google-cloud-machine-learning-now-open-to-all-with-new-professional-services-and-education-programs)

![](Aspose.Words.da23e318-859f-4c72-91fa-57fbf4443580.004.png)

Vous pourriez être une entreprise de prévisions économiques souhaitant suivre la flotte mondiale de porte-conteneurs grâce à des images satellites. Savoir la quantité de marchandises transportées pourrait vous aider à améliorer vos prévisions économiques plusieurs jours voire plusieurs mois avant la publication des chiffres officiels.

![](Aspose.Words.da23e318-859f-4c72-91fa-57fbf4443580.005.png)

Les images médicales sont propices à l'innovation. Par exemple, il est possible de diagnostiquer des affections médicales telles que la rétinopathie diabétique plus tôt, lorsqu'il est plus facile de les traiter et de prévenir la cécité. Comment peut-on passer de telles images à un diagnostic grâce à l'apprentissage automatique ? En ajoutant à la complexité, il faut garder à l'esprit que les images médicales sont généralement d'une résolution extrêmement élevée, ce qui nécessite beaucoup de ressources informatiques pour les traiter.

<https://ai.googleblog.com/2016/11/deep-learning-for-detection-of-diabetic.html>

![](Aspose.Words.da23e318-859f-4c72-91fa-57fbf4443580.006.png)

Ces produits, tels que Vision API et Dialogflow, sont basés à la fois sur les données et les modèles de Google. Vous n'avez pas à vous soucier de former des modèles avec vos propres données. Il vous suffit de transmettre vos données aux produits via une API, et ils vous renverront des prédictions. Il est vraiment difficile de former des modèles sur des données non structurées. Par conséquent, développer quelque chose comme un modèle de reconnaissance visuelle est hors de portée pour la plupart des organisations. Le principal inconvénient est que si vos données non structurées ne font pas partie de l'étendue des données utilisées pour former les modèles pré-entraînés de Google, les API ne vous donneront pas de bons résultats.

## APIs ML pour enrichir les données

![](Aspose.Words.da23e318-859f-4c72-91fa-57fbf4443580.007.png)

Nous savons qu'en général, dans un contexte d'entreprise, une société finit par utiliser des données générées à partir de sources multiples. Des exemples courants de données largement utilisées sont les bases de données relationnelles, les systèmes d'inventaire, les systèmes ERP tels que SAP et les feuilles de calcul. Ces sources de données utilisent des règles strictes de formatage des données et hébergent les données en conséquence. Par conséquent, les données sont appelées données structurées. En dehors de cela, de nombreuses données sont générées à partir de diverses autres sources sous forme de courriels, d'audio, de vidéo, d'images, de textes, de likes et de commentaires sur les réseaux sociaux. Tous ces types de données sont généralement exemptes de règles strictes de formatage et sont donc appelées données non structurées.

En tant qu'entreprise, une question importante et prédominante est la manière de traiter les données non structurées, qui représentent généralement près de 90% des données d'une entreprise. Les données non structurées ont un énorme potentiel pour fournir des informations détaillées qui peuvent bénéficier à l'entreprise. Dans cette section, nous verrons quelles technologies d'IA peuvent être utilisées pour traiter ces données non structurées et avoir un impact sur l'entreprise.

![](Aspose.Words.da23e318-859f-4c72-91fa-57fbf4443580.008.png)Dans ce module, nous allons nous concentrer sur l'API Cloud Natural Language pour le traitement de données non structurées sous forme de texte. Cependant, gardez à l'esprit qu'il existe des API équivalentes pour les données d'image, de vidéo et d'audio. Encore une fois, lorsque nous disons que nous "enrichissons" des données non structurées, nous voulons dire que nous leur appliquons des étiquettes. Nous fournissons des étiquettes pour des questions telles que : "Quel est le sujet de cet e-mail ?" et "Ce commentaire a-t-il un sentiment positif ou négatif ?"

![](Aspose.Words.da23e318-859f-4c72-91fa-57fbf4443580.009.png)

L'API Cloud Natural Language offre de nombreuses fonctionnalités permettant d'effectuer des analyses de texte. La première fonctionnalité est l'analyse syntaxique. L'analyse syntaxique décompose d'abord le texte en une série de jetons, qui sont généralement des mots et des phrases, et fournit des informations sur la structure interne du jeton et son rôle dans la phrase. Elle peut étiqueter un jeton en tant que nom ou verbe, singulier ou pluriel, première personne ou deuxième personne, masculin, féminin ou neutre en termes de genre, et fournit des informations grammaticales telles que le cas, le temps, le mode et la voix.

Au moment de la rédaction de ce texte, l'API Cloud Natural Language prend en charge 10 langues. Consultez la documentation en ligne pour connaître les langues prises en charge actuellement.

<https://cloud.google.com/natural-language/docs/languages>

![](Aspose.Words.da23e318-859f-4c72-91fa-57fbf4443580.010.png)

L'API Natural Language propose également une analyse des entités pour reconnaître les personnes, les lieux, les organisations, les événements, les œuvres d'art, les produits de consommation, les numéros de téléphone, les adresses, les dates et les nombres.

![](Aspose.Words.da23e318-859f-4c72-91fa-57fbf4443580.011.png)

L'analyse des sentiments permet d'identifier l'opinion émotionnelle de l'attitude d'un rédacteur. Elle est présentée sous forme d'un score numérique et d'une magnitude pour l'intensité du sentiment. Elle ne permet pas d'identifier des émotions spécifiques, mais les regroupe généralement en positif, négatif ou neutre. Ainsi, "triste" et "en colère" sont tous deux négatifs, tandis que "drôle" et "heureux" sont tous deux positifs. Étant donné que ce sont des valeurs continues, vous devez définir vos propres seuils qui fonctionnent pour votre application. Par exemple, peut-être qu'une magnitude inférieure à 10 % ne représente pas un sentiment suffisamment fort, ou qu'une valeur comprise entre -1,0 et +1,0 n'exprime pas clairement une émotion.

![](Aspose.Words.da23e318-859f-4c72-91fa-57fbf4443580.012.png)

L'analyse de sentiment des entités combine à la fois l'analyse des entités et l'analyse des sentiments et tente de déterminer le sentiment (positif ou négatif) exprimé à propos des entités présentes dans le texte. Le sentiment des entités est représenté par des valeurs numériques de score et d'amplitude, et est déterminé pour chaque mention d'une entité. Ces scores sont ensuite regroupés pour obtenir un score et une amplitude globaux de sentiment pour une entité donnée.

![](Aspose.Words.da23e318-859f-4c72-91fa-57fbf4443580.013.png)

Au moment de la rédaction, le contenu peut être classifié dans 620 catégories. [Lab : Utilisation de l'API Natural Language pour classifier du texte non structuré](https://www.cloudskillsboost.google/course_sessions/3856018/labs/367826)
