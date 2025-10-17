# **Cahier des Charges – Mini-Projet NAS : Hotspot Wi-Fi**

## **1\. Contexte et objectif**

Ce mini-projet a pour but de mettre en place un hotspot Wi-Fi fonctionnel à l’aide d’un Raspberry Pi 3B+. L’objectif principal est de permettre la création d’un réseau sans fil local, doté d’un adressage IP et d’un partage de connexion Internet via NAT. Ce réseau doit être suffisamment stable pour accueillir plusieurs clients simultanément et doit aussi permettre l’intégration avec d’autres Raspberry Pi comme celui utilisé en tant que NAS ou celui utilisé comme serveur de base de données.

---

## **2\. Périmètre du projet**

Le projet couvre l’installation et la configuration d’un point d’accès Wi-Fi sécurisé, la mise en place d’un serveur DHCP pour distribuer les adresses IP, ainsi que l’activation du NAT pour permettre le partage de la connexion Ethernet sur le Wi-Fi. Il inclut également la vérification de la connectivité interne et externe, la rédaction d’une documentation sur les problèmes rencontrés et les solutions apportées, ainsi que l’intégration du service avec les autres Raspberry Pi utilisés dans le projet global.

---

## **3\. Ressources matérielles**

* Raspberry Pi 3B+

* Carte SD pour le système

* Connexion Ethernet

* Alimentation 5V/2,5A

---

## **4\. Ressources logicielles**

Le système utilisé est Raspberry Pi OS Lite, pour des raisons de performance et de fiabilité. Les paquets nécessaires sont `hostapd` pour la gestion du point d’accès, `dnsmasq` pour le DHCP et le DNS, ainsi que `iptables` pour la gestion du NAT et du partage de connexion. La configuration réseau repose sur l’utilisation de NetworkManager.

---

## **5\. Configuration réseau cible**

* Interface Ethernet (eth0) : DHCP (exemple : 172.16.10.220)

* Interface Wi-Fi (wlan0) : IP fixe 192.168.4.1/24

* Plage DHCP : 192.168.4.2 – 192.168.4.20

* Passerelle et DNS : 192.168.4.1

* SSID : RPi2\_CIEL\_215

* Mot de passe Wi-Fi : \**********

---

## **6\. Contraintes et limites**

L’installation a été réalisée dans un environnement contraint, puisque le réseau du lycée Charles Carnus limite certains accès nécessaires au téléchargement de paquets. Ce problème a été contourné en passant par une autre connexion Internet.

Concernant la gestion des règles NAT, l’utilisation du paquet **iptables-persistent** a permis de conserver la configuration même après un redémarrage, supprimant ainsi le problème de perte d’adresse IP et la nécessité de relancer manuellement les services.

Enfin, le Raspberry Pi 3B+ reste un matériel limité en termes de puissance processeur et de mémoire. Cela impose une certaine prudence quant au nombre d’utilisateurs simultanés connectés au hotspot, ce qui justifie le choix de **Raspberry Pi OS Lite**, une distribution optimisée pour limiter la consommation de ressources.

---

## **7\. Problèmes rencontrés et solutions**

Deux difficultés principales ont été rencontrées. La première concernait l’impossibilité d’installer `iptables` à cause des restrictions du réseau du lycée. La solution a été de passer par un partage de connexion 4G afin d’accéder aux dépôts nécessaires.  
La seconde difficulté venait de la perte de l’adresse IP fixe au redémarrage du Raspberry Pi, en raison de l’absence de lancement automatique de NetworkManager. Ce problème a été résolu par un démarrage manuel du service à l’aide de la commande `systemctl`.

---

## **8\. Recette fonctionnelle**

Les tests réalisés ont confirmé que le hotspot était visible et accessible, que les clients recevaient correctement une adresse IP dans la plage prévue, et que le partage de connexion Internet via NAT était fonctionnel. Les redémarrages des services et du Raspberry Pi n’ont pas compromis le fonctionnement du point d’accès, et plusieurs clients ont pu se connecter en simultané sans perte de stabilité. Enfin, l’intégration avec les autres Raspberry Pi du projet s’est avérée concluante, avec notamment la possibilité pour le RPi NAS et le RPi SGBD de se connecter et d’accéder au réseau.

---

## **9\. Livrables attendus**

Le projet doit fournir un Raspberry Pi configuré et opérationnel en tant que hotspot Wi-Fi. Il doit également inclure une documentation technique détaillant les étapes d’installation, la configuration, ainsi que les procédures de dépannage. Un schéma réseau et une fiche de recette validée complètent les livrables attendus.

---

## **10\. Critères de validation**

La validation du projet repose sur plusieurs critères : la visibilité et l’accessibilité du SSID avec le mot de passe défini, l’attribution correcte d’adresses IP aux clients, l’accès Internet via NAT, le maintien du service après un redémarrage, ainsi que la connexion réussie des Raspberry Pi NAS et SGBD au hotspot.

---

