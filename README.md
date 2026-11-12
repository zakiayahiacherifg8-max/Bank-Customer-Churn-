# Bank-Customer-Churn-
Analyse et prédiction du départ des clients d'une banque.

## Présentation du projet :

Ce projet consiste à analyser et prédire le départ des clients d'une banque (Customer Churn) à partir de leurs caractéristiques démographiques, financières et comportementales.

L'objectif est d'identifier les principaux facteurs associés au départ des clients et de développer des modèles de Machine Learning capables de détecter les profils présentant un risque de churn.

Cette analyse s'inscrit dans une démarche d'aide à la décision : permettre à la banque d'anticiper les départs et de mettre en place des actions de fidélisation ciblées.

## Problématique : 

Comment prédire le départ des clients en banque et quels sont les facteurs associés à leur départ ?

Les enjeux du projet sont de :
- Comprendre le comportement des clients et identifier les profils les plus exposés au churn.
- Explorer les données et mettre en évidence les tendances significatives.
- Comparer plusieurs algorithmes de classification.
Identifier le modèle le plus adapté à la prédiction du départ des clients.
Formuler des recommandations opérationnelles pour améliorer la rétention client.

## Présentation du dataset : 
Le jeu de données contient 10 000 clients et 18 variables décrivant leur profil et leur relation avec la banque.

La variable cible qui nous intéresse particulièrement est Exited qui nous permet de savoir si le client a quitté la banque ou s'il est toujours présent :

0 : le client est toujours présent.
1 : le client a quitté la banque.

## EDA :

Avant de commencer l’analyse, j'ai effectué un 1 er contrôle de qualité des données, le dataset est relativement propre puisque on n’a ni doublons ni valeurs manquantes.

La 1 ere étape consite à identifier les variables qui sont réellement pertinentes pour notre problematique,  j'ai notament supprimé les colonnes inutiles parceque elles servent principalement à identifier les clients ne présentent pas d’interet métier direct pour prédir leur comportement .
On remarque que presque toutes les personnes ayant portés plainte sont partis, donc la variable complain qui indique si le client a fait une réclamation corespond à la variable cible  donc  elle doit etre exclu de la modélisation sinon le modele triche et on aura un score presque parfait totalement inutile en pratique car cette info n’existe  pas avant que le client parte.

Suppression des colonnes d'identification non pertinentes : RowNumber, CustomerId, Surname et Complain

J'ai ensuite calculé différentes statistiques descriptives pour mieux comprendre la population étudiée et surtout savoir si nous avons des valeurs abérrantes dans ce cas non,

## Le problème est-il réel ? 

sur 10000 clients étudiés, 7962 sont toujours présents, soit 79%, à l’inverse 2038 clients sont partis soit 20%, donc on a environ 1 client sur 5 qui a quitté la banque. 
Ce résultat montre que le probleme étudié est loin d’être marginal, car un client perdu coûte nettement plus cher à remplacer qu’à retenir. Et d’une manière générale dans le secteur bancaire le taux réel de désabonnement est < 10%.

## Visualisation : 

Concernant les principales visualisations issues de l'analyse pour connaitre d'avantage le profil des clients qui partent : 

-	tout d’abord concerant la geographie, une différence assez importante entre les pays, y a plus de départ en allemagne,qlq chose ne va pas avec l’offre, le service client ou la concurrence en allemagne.
-	On remarque que l’age pourrait etre un facteur potentiel de désabonnement. Le départ concerne massivement les clients d’age moyen entre 35 et 65 ans, ils sont probablement à un stade de leur vie ou ils ont des besoins financiers importants comme crédit, ils sont la cible principale des offres de la concurrence.
-	Enfin j’ai étudié le niveau d’activité des client, le taux de départ est nettement plus élevé chez les clients inactifs donc l’inactivité est un signal d’alerte majeur.

On passe maintenant à l’étape Machine learning afin d’identifier les variables les plus pertinantes pour la predection du départ.

## Modélisation : 
Donc 2 modeles ont été realisés, la il s’agit d’un tableau de comparaison de performance des 2 modeles àtravers plusieurs métriques
<img width="1177" height="200" alt="image" src="https://github.com/user-attachments/assets/d896e381-1d59-4e30-8f82-2b52050c0ea5" />
-	Concerant  l’Accuracy, la RL obtient 71% contre 82% pour le RF, donc on observe une meilleure performance globale pour le random forest
-	Ensuite les 2 modeles ont une capacité similaire à identifier les client qui vont réelement partir (rappel classe 1)
-	Ce qui concerne les faux négatifs c’est à dire les clients qui vont réellement partir mais que le modele n’a pas identifié comme tels, la aussi les résultats sont très proche
-	EN revanche les faux positif  l’écart est très important, le RF est bien plus précis que la RL donc il ne fait que 237 fausse alertes contre 464 pour la RL.
Au regard de l’ensemble de ces indicateurs le random forest qui a été retenu grace à sa meilleur accuracy et à son nombre plus faible de faux positifs 

Le modele confirme nos hypotheses : pour prédir le départ il faut d’abord regarder l’age et le nombre de produits 

## Recommandation : 

L’analyse des variables nous donne 3 recommandations claires : 
1 erement, cibler en priorité les clients agés de 45 à 55 ans et les membres inactifs, car ce sont eux qui partent le plus, en mettant en place des offres de fidélisation
2 ement, une alerte rouge sur la vente de produits, les clients qui ont 3 produits ou plus partent massivement , il faut en urgence revoir la stratégie de vente croisée,
3 ement, le marché allemand est le point faible, la banque doit lancer une enquete de satisfaction locale particulier auprès de la clientèle féminine

## Conclusion : 

Les modèles testés montrent qu'il est possible d'anticiper le départ des clients d'une banque et d'agir avant qu'il ne se concrétise, à partir de données comportementales simples à collecter.
- Limite du projet :
 La variable Complain (plainte) a été exclue de la modélisation pour éviter une fuite de données. Or, dans la réalité, une plainte est souvent le tout premier signe d'un départ imminent.
- Perspective : 
 Les moyens et ressources nécessaires pour analyser le contenu de ces plaintes ne sont pas disponibles à ce stade. Comprendre la cause racine de l'insatisfaction reste une piste ouverte pour de futures recherches.
