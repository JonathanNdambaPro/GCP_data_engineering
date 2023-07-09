# Introduction à la création de pipelines de données par lots

## EL, ELT, ETL

![](Aspose.Words.f139ae72-8cf8-4a58-b8dd-ecc56355c941.001.png)

E-L signifie Extraction et Chargement. Cela fait référence à la possibilité d'importer des données "telles quelles" dans un système.

E-L-T ou Extraction, Chargement et Transformation permet de charger directement les données brutes dans la cible et de les transformer lorsque cela est nécessaire. Par exemple, vous pourriez donner accès aux données brutes via une vue qui détermine si l'utilisateur souhaite toutes les transactions ou seulement celles réconciliées.

E-T-L ou Extraction, Transformation et Chargement est un processus d'intégration de données dans lequel la transformation a lieu dans un service intermédiaire avant d'être chargée dans la cible. Par exemple, les données pourraient être transformées dans Dataflow avant d'être chargées dans BigQuery.

![](Aspose.Words.f139ae72-8cf8-4a58-b8dd-ecc56355c941.002.png)

Quand utiliseriez-vous E-L ?

En fin de compte, vous devriez utiliser E-L uniquement si les données sont déjà propres et correctes.

Peut-être avez-vous des fichiers journaux dans Cloud Storage. Vous pouvez extraire des données à partir de fichiers sur Cloud Storage et les charger dans le stockage natif de BigQuery. Il s'agit d'un appel simple à l'API REST.

Vous pouvez déclencher ce pipeline à partir de Cloud Composer, Cloud Functions ou via une requête planifiée.

Vous pouvez même le configurer pour fonctionner par lots micro - pas tout à fait en streaming, mais presque en temps réel : chaque fois qu'un nouveau fichier arrive dans Cloud Storage, la fonction cloud s'exécute et la fonction invoque un travail BigQuery. Le service de transfert de données de BigQuery fonctionnera également ici.

Utilisez E-L pour le chargement par lots de données historiques ou pour effectuer des chargements planifiés de fichiers journaux. Mais laissez-moi insister : utilisez E-L uniquement si les données sont déjà propres et correctes.

![](Aspose.Words.f139ae72-8cf8-4a58-b8dd-ecc56355c941.003.png)

E-L-T commence par E-L. Ainsi, le chargement est identique et peut fonctionner de la même manière. Le fichier est stocké dans Cloud Storage, puis la fonction invoque le chargement BigQuery, et la table est ajoutée.

La grande différence réside dans ce qui se passe ensuite. La table peut être stockée dans un jeu de données privé, et tout le monde accède aux données via une vue qui impose des contrôles d'intégrité des données.

Ou peut-être avez-vous une tâche qui exécute une requête SQL avec une table de destination. De cette manière, les données transformées sont stockées dans une table à laquelle tout le monde accède.

Quand utilise-t-on E-L-T ? Un cas courant est lorsque vous ne savez pas quelles transformations sont nécessaires pour rendre les données exploitables. Par exemple, supposons que quelqu'un télécharge une nouvelle image. Vous invoquez l'API Vision, qui renvoie un long message JSON contenant toutes sortes d'informations sur l'image : texte dans l'image, présence de repères, logo, objets, etc. Quelles informations un analyste

pourrait-il avoir besoin à l'avenir ? Vous ne le savez pas. Vous stockez donc le JSON brut tel quel. Plus tard, si quelqu'un souhaite compter le nombre de fois où les logos d'une entreprise spécifique apparaissent dans cet ensemble d'images, il peut extraire les logos du JSON, puis les compter.

Bien sûr, cela ne fonctionne que si la transformation nécessaire peut être exprimée en SQL. Dans le cas de l'API Vision, le résultat est du JSON, et BigQuery SQL prend en charge l'analyse JSON. Ainsi, l'E-L-T fonctionnera dans ce cas.

## Considérations Qualité

Maintenant que nous avons examiné EL et ELT, examinons quelques-unes des transformations que vous pourriez vouloir effectuer et comment elles peuvent être réalisées dans BigQuery.

Pour rester précis, supposons que nos besoins de traitement des données tournent tous autour d'améliorations de qualité.

![](Aspose.Words.f139ae72-8cf8-4a58-b8dd-ecc56355c941.004.png)

Quelles sont certaines des raisons liées à la qualité pour lesquelles nous pourrions vouloir traiter des données ?

La première ligne représente les caractéristiques de l'information - l'information peut être valide, précise, complète, cohérente et/ou uniforme. Ces termes sont définis dans la science de la logique. Chacun est indépendant. Par exemple, des données peuvent être complètes sans être cohérentes. Elles peuvent être valides sans être uniformes. Il existe des définitions formelles pour chacun de ces termes que vous pouvez consulter en ligne.

Mais la principale raison pratique de les rechercher est présentée dans la deuxième ligne - les problèmes qu'ils posent dans l'analyse des données. Il est une chose de rechercher chacun des cinq critères de qualité pour vos données ; avoir des données objectivement de bonne qualité. Cependant, c'en est une autre lorsque des données de mauvaise qualité interfèrent avec l'analyse des données et conduisent à des décisions commerciales

incorrectes. Ainsi, la raison de consacrer du temps, de l'énergie et des ressources à la détection et à la résolution des problèmes de qualité est que cela peut avoir un impact sur les résultats commerciaux.

Ainsi, si les données ne correspondent pas à vos règles commerciales, vous avez un problème de validité. Par exemple, supposons que vous vendiez des billets de cinéma et que chaque billet coûte 10 $. Si vous avez une transaction de 7 $, vous avez alors un problème de validité.

De même, les problèmes de précision sont dus au fait que les données ne correspondent pas à la vérité objective. La complétude concerne le fait de ne pas traiter toutes les données. Les problèmes de cohérence surviennent lorsque deux opérations différentes qui devraient donner le même résultat donnent des résultats différents, et parce que vous ne savez pas à quoi vous fier, vous ne pouvez pas tirer d'enseignements des données. L'uniformité signifie que les valeurs de données dans la même colonne de différentes lignes ont des significations différentes.

Les principales causes de ces problèmes sont énumérées dans la troisième ligne. Nous explorerons des méthodes de détection pour chacun de ces problèmes dans les données.

![](Aspose.Words.f139ae72-8cf8-4a58-b8dd-ecc56355c941.005.png)

Maintenant que vous avez identifié les problèmes, que faites-vous à leur sujet ?

Dans le contexte de GCP (Google Cloud Platform), la méthode E-L-T (Extract, Load, Transform) dans BigQuery peut souvent aider à résoudre de nombreux problèmes de qualité des données. Voici un exemple.

Imaginez que vous prévoyiez d'analyser des données, mais qu'il y ait des enregistrements en double qui donnent l'impression qu'un certain type d'événement est plus courant, alors qu'en réalité il s'agit simplement d'un problème de qualité des données. Vous ne pouvez pas obtenir de insights à partir des données tant que les doublons ne sont pas supprimés.

Donc, avez-vous besoin d'une étape de transformation pour supprimer les doublons avant de stocker les données ?

Peut-être...

Mais une solution plus simple existe, qui consiste à compter les enregistrements uniques. Vous disposez bien sûr de la fonction COUNT DISTINCT dans BigQuery, que vous pouvez utiliser à la place.

De même, un problème tel que des données hors de la plage peut être résolu dans BigQuery sans étape de transformation intermédiaire. Les données non valides peuvent être filtrées à l'aide d'une vue BigQuery, et tout le monde peut accéder à la vue plutôt qu'aux données brutes.

## Comment réaliser Opérations en BigQuery

Dans cette leçon, nous examinerons divers problèmes de qualité et parlerons de certaines fonctionnalités de BigQuery qui peuvent vous aider à résoudre ces problèmes de qualité.

![](Aspose.Words.f139ae72-8cf8-4a58-b8dd-ecc56355c941.006.png)

Nous pouvons utiliser des vues pour filtrer les lignes ayant des problèmes de qualité.

Par exemple, supprimer les quantités inférieures à zéro en utilisant une clause WHERE. Après avoir effectué un GROUP BY, vous pouvez supprimer les groupes dont le nombre total d'enregistrements est inférieur à 10 en utilisant la clause HAVING.

Réfléchissez attentivement à la façon dont vous souhaitez traiter les valeurs nulles et les valeurs vides. NULL représente l'absence de données. BLANK représente une chaîne vide. Réfléchissez si vous souhaitez filtrer à la fois les NULL et les BLANK, ou seulement les NULL ou seulement les BLANK.

Vous pouvez facilement compter les valeurs non nulles en utilisant COUNTIF et utiliser l'instruction IF pour éviter d'utiliser des valeurs spécifiques dans les calculs.

![](Aspose.Words.f139ae72-8cf8-4a58-b8dd-ecc56355c941.007.png)

Les problèmes de cohérence sont souvent dus à des doublons. Vous vous attendez à ce qu'une chose soit unique, mais ce n'est pas le cas, ce qui entraîne des erreurs telles que des totaux incorrects.

COUNT fournit le nombre de lignes dans une table contenant une valeur non nulle. COUNT DISTINCT fournit le nombre de valeurs uniques. S'ils sont différents, cela signifie que vous avez des valeurs en double.

De même, si vous effectuez un GROUP BY et qu'un groupe contient plus d'une ligne, alors vous savez que vous avez deux occurrences ou plus de cette valeur.

Une autre raison pour laquelle vous pourriez rencontrer des problèmes de cohérence est si des caractères supplémentaires ont été ajoutés aux champs. Par exemple, vous pouvez obtenir des horodatages, dont certains peuvent inclure un fuseau horaire. Ou vous avez des chaînes de caractères qui sont remplies. Utilisez des fonctions de chaîne pour nettoyer de telles données avant de les transmettre.

![](Aspose.Words.f139ae72-8cf8-4a58-b8dd-ecc56355c941.008.png)

Pour assurer l'exactitude, testez les données par rapport aux valeurs connues. Par exemple, si vous avez une commande, vous pouvez calculer le sous-total à partir de la quantité commandée et du prix de l'article, et vous assurer que les calculs sont précis. De même, vous pouvez vérifier si une valeur qui est insérée appartient à une liste canonique de valeurs acceptables. Vous pouvez le faire avec une instruction SQL IN.

![](Aspose.Words.f139ae72-8cf8-4a58-b8dd-ecc56355c941.009.png)

Pour garantir l'exhaustivité, identifiez toutes les valeurs manquantes et soit filtrez-les, soit remplacez-les par quelque chose de raisonnable.

Si la valeur manquante est NULL, utilisez les fonctions fournies par SQL telles que NULLIF, COUNTIF, COALESCE, etc. pour filtrer les valeurs manquantes lors des calculs.

Il est possible d'effectuer une UNION à partir d'une autre source afin de prendre en compte les mois de données manquants. Le processus automatique de détection des baisses de données et de demande d'éléments de données pour combler les lacunes est appelé "backfilling". Il s'agit d'une fonctionnalité de certains services de transfert de données.

Lors du chargement des données, vérifiez l'intégrité du fichier avec des valeurs de contrôle (hash, MD5).

![](Aspose.Words.f139ae72-8cf8-4a58-b8dd-ecc56355c941.010.png)

Que se passe-t-il si vous stockez une valeur en centimètres et soudainement vous obtenez la valeur en millimètres ? Votre entrepôt de données finira par avoir des données non uniformes. Vous devez vous protéger contre cela.

Utilisez la fonction SQL CAST pour éviter les problèmes liés aux changements de types de données au sein d'une table. Utilisez la fonction SQL FORMAT() pour indiquer clairement les unités. Et en général, documentez-les très clairement.

J'espère que ce que vous retenez, c'est que le SQL de BigQuery est très puissant et que vous pouvez en tirer parti.

## Limitations

Dans la leçon précédente, nous vous avons montré quelques-unes des façons dont vous pouvez utiliser SQL dans un pipeline E-L-T pour vous protéger contre les problèmes de qualité. Le point est que vous n'avez pas toujours besoin d'E-T-L. E-L-T pourrait être une option même si vous avez besoin de transformation. Cependant, il existe des situations où E-L-T ne sera pas suffisant. Dans ce cas, E-T-L pourrait être ce que vous devez faire. Quels sont les types de situations où cela est approprié ?

![](Aspose.Words.f139ae72-8cf8-4a58-b8dd-ecc56355c941.011.png)

Le premier exemple - traduire l'espagnol en anglais - nécessite l'appel à une API externe. Cela ne peut pas être fait en SQL. Le deuxième exemple - examiner un flux d'actions de clients sur une fenêtre temporelle - est plutôt complexe. Vous pouvez le faire avec des agrégations fenêtrées, mais c'est beaucoup plus simple avec de la logique programmable. Donc, si les transformations ne peuvent pas être exprimées en SQL ou sont trop complexes à réaliser en SQL, vous voudrez peut-être transformer les données avant de les charger dans BigQuery.

![](Aspose.Words.f139ae72-8cf8-4a58-b8dd-ecc56355c941.012.png)

L'architecture de référence pour Google Cloud suggère d'utiliser Dataflow comme outil E-T-L (Extraction-Transformation-Loading). Nous vous recommandons de construire des pipelines E-T-L avec Dataflow et de stocker les données dans BigQuery. L'architecture ressemble à ceci :

- Extraire les données de Pub/Sub, Cloud Storage, Cloud Spanner, Cloud SQL, etc.
- Transformer les données à l'aide de Dataflow,
- Et faire écrire les données par le pipeline Dataflow dans BigQuery.

Dans quels cas utiliseriez-vous cela ?

- Lorsque les données brutes doivent être contrôlées en termes de qualité, transformées ou enrichies avant d'être chargées dans BigQuery. Et lorsque les transformations sont difficiles à réaliser en SQL.
- Lorsque le chargement des données doit se faire en continu, c'est-à-dire si le cas d'utilisation nécessite un flux de données en continu. Dataflow prend en charge le streaming. Nous examinerons le streaming plus en détail dans le prochain cours.
- Et lorsque vous souhaitez intégrer des systèmes d'intégration continue / livraison continue (CI/CD) et effectuer des tests unitaires sur tous les composants. Il est facile de planifier le lancement d'un pipeline Dataflow.

![](Aspose.Words.f139ae72-8cf8-4a58-b8dd-ecc56355c941.013.png)

Dataflow n'est pas la seule option que vous avez sur Google Cloud si vous souhaitez réaliser des opérations E-T-L (Extraction-Transformation-Loading). Dans ce cours, nous examinerons plusieurs services de traitement et de transformation des données fournis par Google Cloud : Dataflow, Dataproc et Data Fusion. Dataproc et Dataflow peuvent être utilisés pour des pipelines E-T-L plus complexes. Dataproc est basé sur Apache Hadoop et nécessite une expertise significative en Hadoop pour être utilisé directement. Data Fusion fournit une interface graphique simple pour construire des pipelines E-T-L, qui peuvent ensuite être facilement déployés à grande échelle sur des clusters Dataproc.

Dataflow est un service de traitement de données entièrement géré et sans serveur, basé sur Apache Beam, qui prend en charge à la fois les pipelines de traitement de données par lots et en continu. Bien qu'une expertise significative en Apache Beam soit souhaitable pour tirer pleinement parti de Dataflow, Google fournit également des modèles de démarrage rapide pour Dataflow, ce qui vous permet de déployer rapidement plusieurs pipelines de données utiles.

Vous pouvez utiliser l'un de ces trois produits pour effectuer des transformations de données, puis stocker les données dans un data lake ou un entrepôt de données pour prendre en charge les analyses avancées.

## ETL pour résoudre des données Problèmes de qualité

![](Aspose.Words.f139ae72-8cf8-4a58-b8dd-ecc56355c941.014.png)

À moins d'avoir des besoins spécifiques, nous recommandons d'utiliser Dataflow et BigQuery. Quels sont quelques besoins qui ne peuvent pas être facilement satisfaits avec Dataflow et BigQuery ?

- Faible latence et débit élevé. Les requêtes BigQuery sont soumises à une latence de l'ordre de quelques centaines de millisecondes et vous pouvez diffuser environ un million de lignes par seconde dans une table BigQuery - cela était autrefois limité à 100 000 lignes, mais récemment cette limite a été portée à 1 million par projet (si vous pouvez vous passer de la déduplication d'effort optimale). Le chiffre typique de latence cité pour BigQuery est de l'ordre d'une seconde, mais avec le moteur BI, il est possible d'obtenir une latence de l'ordre de 100 millisecondes - vous devriez toujours consulter la documentation et les pages de solutions pour les valeurs les plus récentes. Si vos considérations de latence et de débit sont plus strictes, Cloud Bigtable pourrait être un meilleur choix pour le traitement de vos pipelines de données.
- Réutilisation de pipelines Spark. Peut-être avez-vous déjà investi considérablement dans Hadoop et Spark. Dans ce cas, vous pourriez être beaucoup plus productif avec une technologie familière. Utilisez Spark si c'est ce que vous connaissez vraiment bien.
- Besoin de création visuelle de pipelines. Dataflow vous oblige à coder des pipelines de données en Java ou Python. Si vous souhaitez que des analystes de données et des utilisateurs non techniques créent des pipelines de données, utilisez Cloud Data Fusion. Ils peuvent faire glisser-déposer et créer visuellement des pipelines.

Nous examinerons brièvement toutes ces options maintenant et en détail dans le reste de ce cours.

![](Aspose.Words.f139ae72-8cf8-4a58-b8dd-ecc56355c941.015.png)

Dataproc est un service géré pour le traitement par lots, les requêtes, le streaming et l'apprentissage automatique dans le cadre de GCP (Google Cloud Platform).

C'est un service destiné aux charges de travail Hadoop et il est très rentable si l'on prend en compte l'élimination des tâches liées à l'exécution de Hadoop sur du matériel nu et la prise en charge de toutes les activités de maintenance associées.

Il offre également quelques fonctionnalités puissantes telles que la mise à l'échelle automatique et une intégration prête à l'emploi avec les produits Google Cloud tels que BigQuery.

![](Aspose.Words.f139ae72-8cf8-4a58-b8dd-ecc56355c941.016.png)

Cloud Data Fusion est un service d'intégration de données d'entreprise entièrement géré, natif du cloud, qui permet de créer et de gérer rapidement des pipelines de données. Vous pouvez l'utiliser pour alimenter un entrepôt de données, mais également pour effectuer des transformations et des opérations de nettoyage, ainsi que garantir la cohérence des données.

Les utilisateurs, qui peuvent occuper des rôles ne nécessitant pas de compétences en programmation, peuvent créer des pipelines visuels pour répondre à des impératifs commerciaux tels que la conformité réglementaire, sans avoir à attendre qu'une équipe informatique rédige un pipeline Dataflow. Data Fusion dispose également d'une API flexible permettant au personnel informatique de créer des scripts pour automatiser l'exécution.

![](Aspose.Words.f139ae72-8cf8-4a58-b8dd-ecc56355c941.017.png)

Quelle que soit l'outil E-T-L utilisé - Dataflow, Dataproc, Data Fusion -, il y a quelques aspects cruciaux à garder à l'esprit.

Premièrement : il est important de maintenir la traçabilité des données. Que signifie-t-on par traçabilité ?

D'où viennent les données, les processus qu'elles ont traversés et leur état actuel sont tous des éléments de traçabilité. Si vous disposez de la traçabilité, vous savez à quelles utilisations les données conviennent. Si vous constatez des résultats étranges avec les données, vous pouvez consulter la traçabilité pour déterminer s'il existe une cause qui peut être corrigée.

La traçabilité aide également à instaurer la confiance et à respecter les réglementations.

L'autre préoccupation transversale est que vous devez conserver les métadonnées. Vous avez besoin d'un moyen de suivre la traçabilité des données au sein de votre organisation pour les découvrir et les identifier en fonction de leur pertinence pour certaines utilisations.

Sur Google Cloud, Data Catalog offre des fonctionnalités de découverte. Mais vous devez faire votre part en ajoutant des libellés.

![](Aspose.Words.f139ae72-8cf8-4a58-b8dd-ecc56355c941.018.png)

Une étiquette est une paire clé-valeur qui vous aide à organiser vos ressources. Dans BigQuery, vous pouvez attacher des étiquettes à des ensembles de données (datasets), des tables et des vues.

Les étiquettes sont utiles pour la gestion de ressources complexes car vous pouvez les filtrer en fonction de leurs étiquettes. Les étiquettes sont une première étape vers un catalogue de données (Data Catalog).

Parmi les choses auxquelles les étiquettes aident, il y a la facturation Cloud. Si vous attachez des étiquettes à des instances d'Compute Engine, à des compartiments (buckets) et à des pipelines Dataflow, vous avez alors un moyen d'obtenir un aperçu détaillé de votre facture Cloud car les informations sur les étiquettes sont transmises au système de facturation. Ainsi, vous pouvez analyser vos frais de facturation par étiquette.

![](Aspose.Words.f139ae72-8cf8-4a58-b8dd-ecc56355c941.019.png)

Data Catalog est un service de découverte de données et de gestion des métadonnées entièrement géré et hautement évolutif. Il est sans serveur et ne nécessite aucune infrastructure à configurer ou à gérer. Il offre des contrôles d'accès au niveau de l'utilisateur et respecte les listes de contrôle d'accès (ACL) sources pour la lecture, l'écriture et la recherche des actifs de données, vous offrant ainsi un contrôle d'accès de niveau professionnel. Pensez à Data Catalog comme un service de métadonnées en tant que service. Il fournit un service de gestion des métadonnées pour cataloguer les actifs de données via des API personnalisées et une interface utilisateur, offrant ainsi une vue unifiée des données, où qu'elles se trouvent. Il prend en charge des balises schématisées (par exemple, E-num, Bool, DateTime) et pas seulement des balises textuelles simples, ce qui permet aux organisations d'avoir des métadonnées commerciales riches et organisées.

Il offre une découverte unifiée des données pour tous les actifs de données, répartis sur plusieurs projets et systèmes. Il est doté d'une interface de recherche simple et facile à utiliser qui permet de trouver rapidement et facilement des actifs de données, alimentée par la même technologie de recherche Google utilisée par Gmail et Drive. En tant que catalogue central, il fournit un système de catalogage flexible et puissant pour capturer à la fois les métadonnées techniques (automatiquement) et les métadonnées commerciales (balises) dans un format structuré. L'un des grands avantages de la découverte de données est qu'elle s'intègre à l'API Cloud Data Loss Prevention. Vous pouvez l'utiliser pour découvrir et classifier les données sensibles, fournissant ainsi des informations et aidant à simplifier le processus de gouvernance de vos données.

Data Catalog permet aux utilisateurs d'annoter les métadonnées commerciales de manière collaborative et fournit la base de la gouvernance des données.

![](Aspose.Words.f139ae72-8cf8-4a58-b8dd-ecc56355c941.020.png)

Plus précisément, Data Catalog rend toutes les métadonnées de vos ensembles de données disponibles pour que vos utilisateurs puissent les rechercher, indépendamment de l'endroit où les données sont stockées. En utilisant Data Catalog, vous pouvez regrouper des ensembles de données avec des balises, signaler certaines colonnes comme contenant des données sensibles, etc.

Pourquoi est-ce utile ? Si vous avez de nombreux ensembles de données différents avec de nombreuses tables différentes, auxquelles différents utilisateurs ont différents niveaux d'accès, le Data Catalog offre une expérience utilisateur unifiée pour découvrir rapidement ces ensembles de données.

Plus besoin de chercher des noms de tables spécifiques dans les bases de données, qui peuvent ne pas être accessibles à tous les utilisateurs.
