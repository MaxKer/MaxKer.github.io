---
layout: post
title: Mon serveur domotique Jeedom
uid: 1

---

# Projet WarmDom

## Objectif du projet

L'objectif principale de ce projet est d'optimiser la qualité du chauffage électrique à partir des fils pilotes.

Afin de gérer au mieux le contrôle de mes chauffages électriques, j'ai souhaité mettre en place une box domotique reliée à plusieurs sondes de températures et permettant d'envoyer des ordres à chaque chauffage électrique (4 en tout).

## Schéma fonctionnel

Faire apparaître box domotique, internet, smartphone, autres équipements, chauffages, ...

### Box domotique

Pour ma box domotique j'ai choisi de partir sur une RaspberryPi 3 avec Jeedom 3 installé dessus.
Pour les connecter sondes réparties dans l'appartement, j'ai décider d'utiliser des Raspberry pi Zero, qui ne coûtent qu'une dizaine d'euros et qui proposent le Wi-Fi.

#### Initialisation de la RPi3

J'ai suivi ce **tutoriel**, qui explique comment flasher la dernière version de raspbian (Lite pour ce projet) sur votre carte SD.

Une fois raspbian installé et à jours, j'ai installé Jeedom à partir de ce **tutoriel**. La version 3 s'installe comme un paquet Debian classique grâce à un script d'installation.

#### Sécurité et réseau

Afin de rendre accessible Jeedom de l'extérieur, j'ai choisi d'activer le HTTPS sur le Apache de la RPi, et de configurer LetsEncrypt pour récupérer un certificat TLS Server "trusté" par tous les navigateurs. Cela me permettra par le suite d'accéder à mon interface Jeedom depuis l'extérieur, et donc de piloter mon chauffage même depuis l'extérieur de chez moi.

1) Activer mod_ssl

```a2enmod ssl```

Redémarrer Apache2 

```sudo service apache2 restart```

2) Configurer letsencrypt

3) Modifier le mot de passe admin de Jeedom

Avant de rendre accessible votre Jeedom sur internet, vous devez absolument changer le mot de passe par défaut et mettre un mot de passe robuste.

4) Configurer le NAT sur votre box Internet

Port interne: 443, port externe 443, machine : votre rpi (onglet NAT/PAT)
Je conseille avant d'assigner une IP statique à votre rpi. (onglet DHCP)


#### Intégration de Slack

Incoming WebHooks

-> Permet d'envoyer des messages de Jeedom vers une chan Slack

Outgoing WebHooks

-> Permet d'envoyer des commandes à Jeedom depuis Slack

**Attention**
Il faut bien renseigner la "Destination" dans la commande EnvoiMessage (là où on défini le Webhook, le domaine et l'authentification token)
Ca semble fonctionner sans quand on teste directement via le bouton Tester mais dans un scenario avec ask, il faut bien que la destination soi renseignée


#### Intégration de Telegram

https://www.maison-et-domotique.com/70896-piloter-jeedom-avec-telegram/


### Contrôle des fils pilotes

http://jilks.fr/wordpress/fil-pilote-directement-avec-un-raspberry-et-jeedom

#### Schéma

#### I2C RPi

#### Config Jeedom




### Sondes de température DS18b20

#### Schéma

Insérer la partie du schéma 1-wire avec 1 sonde

-> Ajout de la config avec des sondes sur des raspberry pi zero

#### One Wire
https://jeedom.com/doc_old/documentation/plugins/onewire/fr_FR/onewire

#### Config Jeedom

Config du plugin 1-wire (avec des sondes en remote sur les rpi zero)

### Détecteur de mouvement

#### Schéma

-> Connectique PIR HC-SR501 5-20V DC

#### Config Jeedom

-> Plugin GPIO
-> Plugin Jeelink pour accès aux détecteurs des rpi zero à partir du jeedom master (rpi 3)

### Télé info EDF

http://www.magdiblog.fr/gpio/teleinfo-edf-suivi-conso-de-votre-compteur-electrique/

#### Schéma

#### Config Jeedom
