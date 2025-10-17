# Checklist de suivi par séance

## **Séance 1 (4h) — Installation & préparation**

### Groupe 1 (Hotspot Wi-Fi \+ DHCP)

- [x] Flasher carte SD, installer Raspberry Pi OS  
- [x] Mise à jour système (`apt update && upgrade`)  
- [x] Installer `hostapd`, `dnsmasq`, `iptables`  
- [x] Configurer adresse IP fixe pour wlan0  
- [x] Éditer `hostapd.conf` (SSID, canal, WPA2)  
- [x] Configurer `dnsmasq.conf` pour DHCP  
- [x] Tester la diffusion du hotspot (SSID visible)

---

## **Séance 2 (3h) — Configuration avancée & tests**

### Groupe 1 (NAT et sécurisation)

- [x] Configurer le partage de connexion (iptables, NAT)  
- [x] Activer forwarding IPv4  
- [x] Tester accès Internet depuis clients connectés au hotspot  
- [x] Valider sécurité WPA2

---

## **Séance 3 (4h) — Tests croisés, automatisation et documentation**

### Tous groupes

- [x] Monter NAS de RPi2 sur RPi3 (backup BDD, logs)  
- [x] Tester accès BDD depuis RPi2 et autres clients  
- [x] Tester stabilité et accès Internet sur tous les RPi  
- [x] Écrire scripts bash d’installation/configuration automatisée  
- [x] Documenter schémas réseau, commandes clés, résultats tests  
- [x] Rédiger fiche recette (tests fonctionnels \+ validation)  
- [x] Préparer diaporama et démonstration finale

---

## **Séance 4 (3h) — Revue & présentation**

- [x] Corriger éventuels bugs restants  
- [x] Finaliser documentation  
- [x] Répéter la présentation orale  
- [x] Valider la conformité fonctionnelle globale  
- [x] Présentation orale et démo

