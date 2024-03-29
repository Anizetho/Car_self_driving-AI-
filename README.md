# Intelligence artificielle pour une voiture autonome

## 1) Contexte
*Ce dépôt présente le design et le développement d'une intelligence artificielle (IA) prévu pour conduire une voiture dans un environnement simplifié, c'est-à-dire dans un environnement ne contenant ni piétons, ni croisements de route. L'objectif est uniquement de pouvoir faire rouler une voiture sur la route. Ce projet a été entièrement réalisé au moyen du langage de programmation Python.*

## 2) Installation du simulateur
Il est nécessaire de télécharger le simulateur de conduite développé par Udacity. Pour ce faire, référez-vous au guide d'installation suivant : https://github.com/udacity/self-driving-car-sim

  Ce simulateur permet :
  * D'une part, d'enregistrer des données d'apprentissage sur l'un des deux circuits disponibles (*training phase*).
  * D'autre part, de lancer la simulation pour tester le modèle d'intelligence artificiel élaboré (*test phase*).

Ce simulateur se comporte comme un client *socketIO*. Pour lancer une simulation (*Autonomous Mode*), tout ce que vous avez à faire est de créer un serveur *socketIO* qui écoute sur le port 4567 pour recevoir les évènements du simulateur et les envoyer aux commandes de la voiture. Plus de précisions suivront au point (4).

## 3) Description des fichiers et répertoires
Ce dépot contient 3 fichiers ainsi que 2 dossiers : 
* Fichier **[*Features.py*](https://github.com/Anizetho/Car_self_driving-AI-/blob/master/Features.py)**  --> Ce script python est utilisé pour calculer les *features* du modèle (distances droite et gauche) ainsi que pour créer un fichier CSV (*Result.csv* par défaut) reprennant ces *features* associées à l'angle de volant correspondant (voiture).
* Fichier **[*Linear_regression_model.py*](https://github.com/Anizetho/Car_self_driving-AI-/blob/master/Linear_regression_model.py)**  --> Ce script python est utilisé pour créer le modèle de régression linéaire. Pour ce faire, il utilise le fichier CSV précédemment créé avec *Features.py*.
* Fichier **[*drive.py*](https://github.com/Anizetho/Car_self_driving-AI-/blob/master/drive.py)** --> Ce script python est utilisé pour lancer la simulation (*Autonomous Mode* sur Udacity). Pour ce faire, il charge le modèle préalablement créé (*Linear_regression_model.py*). Ensuite, il est configuré de façon à envoyer en temps réel des prédictions de valeurs au simulateur par *socketIO* sur base des informations provenant de la voiture (envoyées du simulateur). 
* Dossier **[*Linear_regression_model*](https://github.com/Anizetho/Car_self_driving-AI-/tree/master/Linear_regression_model)** --> Ce dossier contient les nouveaux modèles créés mais aussi les anciens modèles créés précédemment et directement utilisables avec le fichier *drive.py* (exemple : *model4.pkl*).  
* Dossier **[*Training_data*](https://github.com/Anizetho/Car_self_driving-AI-/tree/master/Training_data)** --> Ce dossier contient les données d'entrainement obtenues via le simulateur d'Udacity (*Training Mode*). Pour sauvegarder les données, l'utilisateur doit définir le chemin du dossier de sauvegarde (sur son ordinateur) de ces données. Cependant, le chemin de ce dossier fera toujours référence à la racine de l'ordinateur sur lequel la simulation a été opérée. Pour cette raison, les données présentes dans ce dossier dépendent de l'ordinateur employé et ne peuvent être utilisées que par cet ordinateur. Par conséquent, le dossier *Training_data* ne contient qu'un seul ensemble de données (Data_2), indicatives pour mieux comprendre le fonctionnement. 

## 4) Algorithmes et bibliothèques utilisées
Au total, 10 bibliothèques ont été utilisées :
* Pour le *préprocessing* : Utilisation de la bibliotèque *openCV* afin de réaliser le traitement d'image nécessaire pour le calcul des distances gauches et droites.
* Pour le modèle : Utilisation de la librairie *scikit learn (sk-learn)* afin de réaliser la régression linéaire. *pickle* est également utilisé afin de sauvegarder et charger le modèle.
* Pour le lancement de la simulation : Utilisation de *socketio* et *eventlet* pour communicquer avec le simulateur Udacity. 
* Autres : Utilisation de *os*, *numpy*, *matplotlib*, *mpl_toolkits* ou encore *pandas* pour diverses opérations et traitements.

## 5) Lancement de la simulation 
Avant de pouvoir lancer la simulation, il faut tout d'abord réaliser les 4 étapes suivantes : 
1. Sur l'application Udacity, lancer le mode d'entrainement (*training mode*). Vous pouvez alors enregistrer des données d'entrainement.
2. Ouvrez le script python *Features.py* et exécutez-le. Vous obtenez alors vos features.
3. Ouvrez le script python *Linear_regression_model.py* et exécutez-le. Vous obtenez alors votre modèle.
4. Ouvrez le script python *drive.py* ainsi que le simulteur Udacity. Cette fois-ci, lancez le mode autonome (*Autonomous Mode*) sur Udacity. Une fois la voiture prête à démarrer, exécutez le script python (*drive.py*). À condition que le modèle ait été correctement élaboré, votre voiture doit rouler.
