---
layout: default
title: Documentation Gardena-Husqvarna
lang: fr_FR
pluginId: gardena
---

# Description

Plugin permettant d'intégrer tous les appareils de la gamme Gardena Smart System (Water Control, sensor, irrigation control, power socket et Sileno mower) ainsi que les robots Husqvarna Automower Connect.
Il est possible d'accéder aux données des appareils, de les monitorer et d'effectuer certaine actions (en fonction de l'appareil, voir ci-dessous pour plus de détails)

> **Important**
>
> Quelque soit le matériel (Gardena et Husqvarna) il faut une connectivité internet. Ce plugin ne fonctionnera pas avec tout autre technologie de connexion locale, comme par exemple mais pas uniquement, le bluetooth.

# Installation

Afin d’utiliser le plugin, vous devez le télécharger, l’installer et l’activer comme tout plugin Jeedom.

> **Important**
>
> Il est indispensable d'être sous Debian 10 Buster minimum pour faire fonctionner le plugin.
>
> Si vous aviez tenté d'installer le plugin "Gardena Smart System", il est nécessaire de le désactiver avant d'activer celui-ci. En effet, un problème dans le plugin "Gardena Smart System" crée un conflit avec ce plugin qui risque de rendre Jeedom indisponible. Ce problème doit être réglé dans l'autre plugin, il m'est malheureusement impossible de l'éviter.

# Configuration du plugin

Dans la configuration du plugin, il faudra renseigner l'application key et l'application secret permettant l'accès aux API.
Vous devez également sélectionner les API que vous voulez activer parmi les 2 options possibles (les 2 peuvent être activées en même temps):

- Gardena Smart System
- Husqvarna Automower

Vous trouverez plus d'information directement disponible sur la page de configuration du plugin.

# Synchronisation et configuration des équipements

Dès que la configuration du plugin est complète et correcte, le plugin synchronisera les équipements selon les API activées.
Il créera les équipements manquants avec leurs commandes et mettra à jour les commandes de tout les appareils connectés.

Les commandes de tous les équipements, que ce soit de la gamme Gardena Smart System ou les robots Husqvarna, seront mises à jours en temps réel, il n'y a donc pas de configuration supplémentaire à faire.

Une commande **Rafraichir** existe pour demander une actualisation supplémentaire manuelle pour les tondeuses robots Husqvarna Automower mais cela n'est en principe pas nécessaire puisque tout changement d'état sera mis à jour en temps réel. **Attention** il y a une limite de 10.000 actualisations par mois pour les actualisations manuelles, cette limite est imposée par Husqvarna.

> **Tip**
>
> Le plugin ne supprimera jamais un équipement dans votre Jeedom. Si effectivement un équipement jeedom ne correspond plus à aucun appareil en votre possession, veuillez le supprimer manuellement.

Dans la page de configuration d'un équipement, il existe un bouton pour créer les commandes manquantes sur celui-ci (dans le cas où vous auriez supprimé une commande par erreur par exemple).

# Les équipements et leurs commandes

## Les commandes communes à tous les appareils Gardena Smart System

Chaque équipement Gardena Smart System dispose des commandes suivantes:

- **Batterie** indique le niveau de charge la batterie (si applicable) en pourcent
- **Etat batterie** donne une description de l'état de la batterie: *OK*, *LOW*, *REPLACE_NOW*, *OUT_OF_OPERATION*, *CHARGING*, *NO_BATTERY*, *UNKNOWN*
- **Niveau connexion** indique la niveau de la connexion avec la passerelle en pourcent
- **Etat connexion** donne une description de l'état de connexion: *ONLINE*, *OFFLINE*, *UNKNOWN*

## Gardena Smart Sensor

- **Température** indique la température ambiante
- **Luminosité** indique la luminosité en lux
- **Humidité du sol** indique le pourcentage d'humidité du sol
- **Température du sol** indique la température du sol

## Gardena Smart Water Control

- **Santé** indique l'état général de la valve: *OK*, *WARNING*, *ERROR*, *UNAVAILABLE*
- **Dernière erreur** donne la dernière erreur le cas échéant, uniquement valable si la commande **Santé** à la valeur *WARNING* ou *ERROR* (voir ci-dessous pour une liste des valeurs possibles)
- **Activité** indique l'activité en cours: *CLOSED*, *MANUAL_WATERING*, *SCHEDULED_WATERING*
- **Etat** commande info binaire indiquant si la valve est ouverte ou fermée
- **Démarrer** commande action pour démarrer l'arrosage demandant en option le nombre de minute (entière) d'arrosage
- **Arrêter** commande action pour arrêter l'arrosage
- **Durée restante** commande info donnant le temps restant (en minute) lorsque l'arrosage est en cours
- **Pause programmation** commande action demandant en option le nombre de minutes
- **Reprise programmation** commande action

## Gardena Smart Power Socket

- **Santé** indique l'état général de la prise: *OK*, *WARNING*, *ERROR*, *UNAVAILABLE*
- **Dernière erreur** donne la dernière erreur le cas échéant, uniquement valable si la commande **Santé** à la valeur *WARNING* ou *ERROR*; peut avoir la valeur: *TIMER_CANCELLED*, *UNKNOWN*
- **On** commande action pour allumer la prise
- **Off** commande action pour éteindre la prise
- **On minuteur** command action pour allumer la prise avec auto extinction après x minutes (entières) passées en option de la commande
- **Activité** indique l'activité en cours: *OFF*, *FOREVER_ON*, *TIME_LIMITED_ON*, *SCHEDULED_ON*
- **Etat** commande info binaire indiquant si la prise est allumée ou éteinte
- **Durée restante** commande info donnant le temps restant de la minuterie (si applicable)
- **Pause programmation** commande action demandant en option le nombre de minutes
- **Reprise programmation** commande action

## Gardena Smart Mower

- **Santé** indique l'état général de la tondeuse: *OK*, *WARNING*, *ERROR*, *UNAVAILABLE*
- **Activité** indique l'activité en cours: *PAUSED*, *OK_CUTTING*, *OK_CUTTING_TIMER_OVERRIDDEN*, *OK_SEARCHING*, *OK_LEAVING*, *OK_CHARGING*, *PARKED_TIMER*, *PARKED_PARK_SELECTED*, *PARKED_AUTOTIMER*, *NONE*
- **Active** commande binaire indiquant si la tondeuse est active ou non; elle sera indiquée comme active lors de ces activités: *OK_CUTTING*, *OK_CUTTING_TIMER_OVERRIDDEN*, *OK_SEARCHING*, *OK_LEAVING*, *OK_CHARGING*
- **Dernière erreur** donne la dernière erreur le cas échéant, uniquement valable si la commande **Santé** à la valeur *WARNING* ou *ERROR* (voir ci-dessous pour une liste des valeurs possibles)
- **Heures de travail** commande info donnant le nombre d'heures de travail
- **Durée restante** commande info donnant le temps restant de la minuterie (si applicable)
- **Démarrage mode manuel** commande action pour démarrer en mode manuel demandant en option le nombre de minute d'activité
- **Démarrage mode auto** commande action pour démarrer en mode auto (en suivant la programmation)
- **Annulation et retour à la base** commande action, la tondeuse redémarrera lors de la prochaine tâche
- **Stop et retour à la base** commande action, la tondeuse ne redémarrera pas pour la prochaine tâche

## Gardena Smart Irrigation Control

L'équipement permet de contrôler jusqu'à 6 valves 24v. Il dispose des commandes suivantes:

- **Santé contrôleur** indique l'état général du contrôleur: *OK*, *WARNING*, *ERROR*, *UNAVAILABLE*
- **Dernière erreur** donne la dernière erreur le cas échéant, uniquement valable si la commande **Santé** à la valeur *WARNING* ou *ERROR* (voir ci-dessous pour une liste des valeurs possibles)
- **Arrêter toutes les valves** permet d'arrêter l'arrosage de toutes les valves en une commande, l'arrosage reprendra à la prochaine programmation

Ainsi que des commandes suivantes pour chacune des valves (où X aura donc une valeur de 1 à 6):

- **Activité valve X** indique l'activité en cours: *CLOSED*, *MANUAL_WATERING*, *SCHEDULED_WATERING*
- **Etat valve X** commande info binaire indiquant si la valve est ouverte ou fermée
- **Santé valve X** indique l'état général de la prise: *OK*, *WARNING*, *ERROR*, *UNAVAILABLE*
- **Démarrer valve X** commande action pour démarrer l'arrosage demandant en option le nombre de minute (entière) d'arrosage
- **Arrêter valve X** commande action pour arrêter l'arrosage
- **Durée restante valve X** commande info donnant le temps restant (en minute) lorsque l'arrosage est en cours
- **Pause programmation valve X** commande action demandant en option le nombre de minutes
- **Reprise programmation valve X** commande action

## Husqvarna Automower

- **Connecté** commande info binaire indiquant si la tondeuse est connectée
- **Batterie** indique le niveau de charge la batterie (si applicable) en pourcent
- **Mode** aura une des valeurs suivantes: *MAIN_AREA*, *DEMO*, *SECONDARY_AREA*, *HOME*, *UNKNOWN* (voir ci-dessous pour une description des valeurs)
- **Etat** aura une des valeurs suivantes: *UNKNOWN*, *NOT_APPLICABLE*, *PAUSED*, *IN_OPERATION*, *WAIT_UPDATING*, *WAIT_POWER_UP*, *RESTRICTED*, *OFF*, *STOPPED*, *ERROR*, *FATAL_ERROR*, *ERROR_AT_POWER_UP* (voir ci-dessous pour une description des valeurs)
- **Activité** aura une des valeurs suivantes: *UNKNOWN*, *NOT_APPLICABLE*, *MOWING*, *GOING_HOME*, *CHARGING*, *LEAVING*, *PARKED_IN_CS*, *STOPPED_IN_GARDEN* (voir ci-dessous pour une description des valeurs)
- **Latitude** commande info donnant la latitude de la dernière position
- **Longitude** commande info donnant la longitude de la dernière position
- **Dernière position** commande info donnant la dernière position GPS avec le format *latitude,longitude*
- **Positions** contenant l'historique des 50 dernières positions du robot au format *position1,position2,position3,...*
- **Hauteur de coupe** et **Réglage hauteur de coupe** permettant de connaître et définir la hauteur de coupe (entre 1 et 9)
- **Phare** et **Réglage phare** permettant de connaître et définir le mode d'allumage des phare, valeurs possibles: *ALWAYS_ON*, *ALWAYS_OFF*, *EVENING_ONLY*, *EVENING_AND_NIGHT*
- **Heure dernier rapport** et **Heure prochain départ** les valeurs sont des timestamp en milliseconde (pour une utilisation plus facile dans un scénario) et seront affichées au format date/heure sur le widget
- **Restriction programmation** donnant la raison de l'exception sur la programmation normale
- **Code erreur** & **Description erreur** donne le code et la description de l'erreur le cas échéant
- **Durée restante** commande info donnant le temps restant d'activité; valable uniquement lors de l'utilisation des commandes **Démarrage mode manuel** ou **Retour à la base**
- **Démarrage mode manuel** Démarre et tond l'herbe pendant la durée (en minute) donnée en option de la commande
- **Pause**
- **Reprendre** Reprend selon la programmation
- **Retour à la base** Retourne à la base pendant le nombre de minute donnée en option de la commande, reprend la programmation ensuite
- **Annulation et retour à la base** commande action, la tondeuse redémarrera lors de la prochaine tâche
- **Stop et retour à la base** commande action, la tondeuse ne redémarrera pas pour la prochaine tâche
- **Temps utilisation des lames** commande info numérique
- **Cycles de charge** commande info numérique
- **Collisions** commande info numérique
- **Temps total de chargement** commande info numérique
- **Temps total de coupe** commande info numérique
- **Temps total de fonctionnement** commande info numérique
- **Temps total de recherche** commande info numérique

# Widget Positions

Le plugin met à disposition un widget *Positions* à appliquer sur la commande **Positions** des tondeuses Husqvarna (les tondeuses Gardena ne disposent pas encore d'une localisation GPS).

Pour que le widget fonctionne bien vous devez effectuer les configurations suivantes:

1. Dans la configuration avancée de la commande **Positions**, onglet *Affichage*, sélectionnez le widget *Gardena/Positions*:

![Configuration avancée](../images/advance_config.png "Configuration avancée")

2. Prenez une capture de la zone de tonte (sur Google Maps par exemple), nommez le fichier *maison.png* par exemple et ensuite copiez l’image dans le dossier *plugins/gardena/data/* sur votre Jeedom (via l'explorateur de fichier intégré à Jeedom par exemple)
3. Identifiez les coordonnées géographiques (latitude et longitude) du coin inférieur gauche et du coin supérieur droit de la zone correspondante à la capture.
4. Encodez les coordonnées prises ci-dessus dans la liste des Paramètres du widgets: *latMin*, *longMin*, *latMax* et *longMax* sont obligatoires.
Si vous avez nommé votre fichier autrement que *maison.png* ou si vous voulez tester une autre capture, encodez le nom du fichier dans le paramètre *imgFile*
5. Les autres paramètres sont optionnels:

![Configuration widget](../images/config_widget.png "Configuration widget")

Sauvez et vous devriez voir la mini-carte avec l'historique des positions sur la tuile de l'équipement:

![Positions](../images/Positions.png "Positions")

# Annexes

## Description des erreurs pour les valves Gardena Smart System (Water Control ou Irrigation Control)

- *NO_MESSAGE* - pas d'erreur
- *CONCURRENT_LIMIT_REACHED* - Ouverture de la valve impossible, un maximum de 2 valves peuvent être ouverte en même temps
- *NOT_CONNECTED* - Aucune valve connectée
- *VALVE_CURRENT_MAX_EXCEEDED* - La valve a été fermée car elle avait une consommation électrique excessive
- *TOTAL_CURRENT_MAX_EXCEEDED* - La valve a été fermée car la consommation électrique totale était trop importante
- *WATERING_CANCELED* - Arrosage annulé
- *MASTER_VALVE* - La valve principale n'est pas connectée
- *WATERING_DURATION_TOO_SHORT* - Durée d'arrosage trop courte, arrosage annulé
- *VALVE_BROKEN* - La connexion électrique avec la valve est interrompue
- *FROST_PREVENTS_STARTING* - Le givre empêche l'ouverture de la valve
- *LOW_BATTERY_PREVENTS_STARTING* - Batterie faible, impossible d'ouvrir la valve
- *VALVE_POWER_SUPPLY_FAILED* - Problème d'alimentation électrique, impossible d'ouvrir la valve
- *UNKNOWN* - Inconnu

## Description des erreurs du Gardena Smart Mower

- *NO_MESSAGE* - pas d'erreur
- *OUTSIDE_WORKING_AREA* - En dehors de la zone de travail
- *NO_LOOP_SIGNAL* - Pas de signal du câble périphérique
- *WRONG_LOOP_SIGNAL* - Mauvais signal du câble périphérique
- *LOOP_SENSOR_PROBLEM_FRONT* - Problème sur le capteur de câble avant
- *LOOP_SENSOR_PROBLEM_REAR* - Problème sur le capteur de câble arrière
- *LOOP_SENSOR_PROBLEM_LEFT* - Problème sur le capteur de câble gauche
- *LOOP_SENSOR_PROBLEM_RIGHT* - Problème sur le capteur de câble droit
- *WRONG_PIN_CODE* - Mauvais code PIN
- *TRAPPED* - Coincé
- *UPSIDE_DOWN* - Retourné.
- *EMPTY_BATTERY* - Batterie vide
- *NO_DRIVE* - Pas de câble guide
- *TEMPORARILY_LIFTED* - Tondeuse soulevée
- *LIFTED* - Soulevé
- *STUCK_IN_CHARGING_STATION* - Coincé dans la station de chargement
- *CHARGING_STATION_BLOCKED* - Station de chargement bloquée
- *COLLISION_SENSOR_PROBLEM_REAR* - Problème sur le capteur de collision arrière
- *COLLISION_SENSOR_PROBLEM_FRONT* - Problème sur le capteur de collision avant
- *WHEEL_MOTOR_BLOCKED_RIGHT* - Roue moteur droite bloquée
- *WHEEL_MOTOR_BLOCKED_LEFT* - Roue moteur gauche bloquée
- *WHEEL_DRIVE_PROBLEM_RIGHT* - Problème sur la roue de direction droite
- *WHEEL_DRIVE_PROBLEM_LEFT* - Problème sur la roue de direction gauche
- *CUTTING_MOTOR_DRIVE_DEFECT* - Motorisation du système de coupe défectueux
- *CUTTING_SYSTEM_BLOCKED* - Système de coupe bloqué
- *INVALID_SUB_DEVICE_COMBINATION* -
- *MEMORY_CIRCUIT_PROBLEM* - Problème avec le circuit mémoire
- *CHARGING_SYSTEM_PROBLEM* - Problème avec le système de chargement
- *STOP_BUTTON_PROBLEM* - Problème avec le bouton STOP
- *TILT_SENSOR_PROBLEM* - Problème avec le capteur d'inclinaison
- *MOWER_TILTED* - Tondeuse inclinée
- *WHEEL_MOTOR_OVERLOADED_RIGHT* -
- *WHEEL_MOTOR_OVERLOADED_LEFT* -
- *CHARGING_CURRENT_TOO_HIGH* -
- *ELECTRONIC_PROBLEM* - Problème électronique.
- *CUTTING_MOTOR_PROBLEM* -
- *LIMITED_CUTTING_HEIGHT_RANGE* -
- *CUTTING_HEIGHT_PROBLEM_DRIVE* -
- *CUTTING_HEIGHT_PROBLEM_CURR* -
- *CUTTING_HEIGHT_PROBLEM_DIR* -
- *CUTTING_HEIGHT_BLOCKED* -
- *CUTTING_HEIGHT_PROBLEM* -
- *BATTERY_PROBLEM* - Problème batterie
- *TOO_MANY_BATTERIES* - Trop de batteries
- *ALARM_MOWER_SWITCHED_OFF* - Alarme, tondeuse éteinte
- *ALARM_MOWER_STOPPED* - Alarme, tondeuse arrêtée
- *ALARM_MOWER_LIFTED* - Alarme, tondeuse soulevée
- *ALARM_MOWER_TILTED* - Alarme, tondeuse inclinée
- *ALARM_MOWER_IN_MOTION* - Alarme, tondeuse en mouvement
- *ALARM_OUTSIDE_GEOFENCE* - Alarme, tondeuse en dehors de la barrière virtuelle
- *SLIPPED* - La tondeuse a dérapé
- *INVALID_BATTERY_COMBINATION* - Combinaison de batterie de différent type invalide
- *UNINITIALISED* - Statut de la tondeuse inconnu
- *WAIT_UPDATING* - Tondeuse en attente d'installation du firmware
- *WAIT_POWER_UP* - Tondeuse s'allume
- *OFF_DISABLED* - Tondeuse désactivée via l'interrupteur principal
- *OFF_HATCH_OPEN* - Tondeuse en attente avec son capot ouvert
- *OFF_HATCH_CLOSED* - Tondeuse en attente avec son capot fermé
- *PARKED_DAILY_LIMIT_REACHED* - Tondeuse parquée, limite de coupe journalière atteinte

## Description des erreurs du Gardena Smart Irrigation Control

- *NO_MESSAGE* - pas d'erreur
- *VOLTAGE_DROP* - Baisse de tension détectée sur l'alimentation électrique (VDD_IN)
- *WRONG_POWER_SUPPLY* - Alimentation électrique incorrecte
- *NO_MCU_CONNECTION* - Problème de communication avec le MCU secondaire
- *UNKNOWN* - Inconnu

## Description des modes Husqvarna Automower

- *MAIN_AREA* - La tondeuse va tondre, rentrer à la base pour se charger selon son programme.
- *DEMO* - Identique à *MAIN_AREA* mais moins longtemps. Pas d'activité des lames.
- *SECONDARY_AREA* - Pas de programmation, la tondeuse est en mode manuel.
- *HOME* - La tondeuse est sur sa base et la programmation n'est pas appliquée.
- *UNKNOWN* - Inconnu.

## Description des états Husqvarna Automower

- *PAUSED* - La tondeuse est en pause.
- *IN_OPERATION* - En opération, voir la valeur **Activité**.
- *WAIT_UPDATING* - La tondeuse télécharge et met à jour le firmware.
- *WAIT_POWER_UP* - La tondeuse s'allume.
- *RESTRICTED* - la tondeuse ne peut pas tondre dû à la programmation ou un stop manuel.
- *OFF* - La tondeuse est éteinte.
- *STOPPED* - La tondeuse est arrêtée et demande une intervention manuelle.
- *ERROR*, *FATAL_ERROR*, *ERROR_AT_POWER_UP* - Une erreur s'est produite, voir la valeur de **Erreur**. La tondeuse demande une intervention manuelle.
- *NOT_APPLICABLE* - Pas applicable.
- *UNKNOWN* - Inconnu.

## Description des activités Husqvarna Automower

- *MOWING* - Tonte en cours
- *GOING_HOME* - Se rend à la base
- *CHARGING* - Sur la base, en chargement.
- *LEAVING* - Quitte la base.
- *PARKED_IN_CS* - Sur la base.
- *STOPPED_IN_GARDEN* - Tondeuse arrêtée dans le jardin. Action manuelle nécessaire.
- *NOT_APPLICABLE* - Action manuelle nécessaire.
- *UNKNOWN* - Inconnu.

# Changelog

[Voir le changelog](./changelog)

# Support

Si vous avez un problème, commencez par lire les derniers sujets en rapport avec le plugin sur [community]({{site.forum}}/tag/plugin-{{page.pluginId}}).

Si malgré tout vous ne trouvez pas de réponse à votre question, n'hésitez pas à créer un nouveau sujet en n'oubliant pas de mettre le tag du plugin ([plugin-{{page.pluginId}}]({{site.forum}}/tag/plugin-{{page.pluginId}})).

Il faudra au minimum fournir:

- une capture d'écran de la page santé Jeedom
- tous les logs disponibles du plugin
- selon les cas, une capture d'écran de l'erreur rencontrée, une capture d'écran de la configuration posant problème...
