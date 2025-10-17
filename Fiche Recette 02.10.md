# Fiche de recette - Hotspot Wi-Fi + NAT

**Binôme** : Tom/Enzo  
**Date** : 02/10/2025  
**Version** : 1.1  

---
## 1. Prérequis
| **ID** | **Description**                          | **Validé (✔/✘)** | **Commentaires**          |
|--------|------------------------------------------|------------------|---------------------------|
| PR01   | Raspberry Pi OS à jour                  | ✔                | `sudo apt update && upgrade` |
| PR02   | Paquets `hostapd`, `dnsmasq` installés  | ✔                | Paquets installés, fichiers de préconfigurations trouvés. |
| PR03   | Interface Wi-Fi (`wlan0`) disponible     | ✔                | `ip a`                |

---
## 2. Tests fonctionnels

### 2.1 Configuration du Hotspot
| **ID Test** | **Fonctionnalité**               | **Description**                          | **Méthode/Commande**                     | **Résultat attendu**               | **Résultat obtenu** | **Statut** |
|-------------|-----------------------------------|------------------------------------------|------------------------------------------|------------------------------------|---------------------|------------|
| T01         | Hotspot visible                   | Le SSID "ProjetRPi" est visible          | `ip a` ou recherche Wi-Fi (smartphone/PC) | SSID détecté                     | ✔                   | 🟢 OK      |
| T02         | Connexion possible                | Connexion avec mot de passe WPA2         | Tentative de connexion depuis un client | Connexion établie, IP attribuée   | ✔                   | 🟢 OK      |
| T03         | Adressage IP correct              | Plage DHCP respectée (192.168.4.2-20)    | `ip a` sur le client                     | IP dans la plage DHCP             | 192.168.4.8         | 🟢 OK       | ✔

### 2.2 Partage de connexion (NAT)
| **ID Test** | **Fonctionnalité**               | **Description**                          | **Méthode/Commande**                     | **Résultat attendu**               | **Résultat obtenu** | **Statut** |
|-------------|-----------------------------------|------------------------------------------|------------------------------------------|------------------------------------|---------------------|------------|
| T04         | Accès Internet                    | Ping vers 1.1.1.1 depuis un client      | `ping 1.1.1.1`                           | Réponse ICMP                       | ✔                   | 🟢 OK      |
| T05         | Navigation web                   | Accès à un site web (ex: google.com)     | `curl -I https://google.com`             | Code HTTP 200                      | ✔                   | 🟢 OK      |
| T06         | Règles NAT actives                | Vérification des règles iptables         | `sudo iptables -t nat -L`                 | Règle MASQUERADE présente          | ✔                   | 🟢 OK      |

---
## 3. Tests de robustesse
| **ID Test** | **Fonctionnalité**               | **Description**                          | **Méthode/Commande**                     | **Résultat attendu**               | **Résultat obtenu** | **Statut** |
|-------------|-----------------------------------|------------------------------------------|------------------------------------------|------------------------------------|---------------------|------------|
| T07         | Redémarrage service               | Redémarrage de `hostapd` et `dnsmasq`   | `sudo systemctl restart hostapd dnsmasq`  | Services actifs, hotspot disponible | ✔                   | 🟢 OK      |
| T08         | Reboot RPi                        | Redémarrage complet du RPi               | `sudo reboot`                            | Hotspot disponible après reboot    | ✔                   | 🟢 OK      |
| T09         | Charge réseau                     | 5 clients connectés simultanément        | Connexion de 5 appareils sur le même réseau                 | Hotspot stable, pas de déconnexion |      ✔               | 🟢 OK       |

---
## 4. Tests d’intégration
| **ID Test** | **Fonctionnalité**               | **Description**                          | **Méthode/Commande**                     | **Résultat attendu**               | **Résultat obtenu** | **Statut** |
|-------------|-----------------------------------|------------------------------------------|------------------------------------------|------------------------------------|---------------------|------------|
| T10         | Accès depuis RPi2 (NAS)           | RPi2 se connecte au hotspot              | `ping 192.168.4.1` depuis RPi2           | Réponse ICMP                       | ✔                 |      🟢 OK  |
| T11         | Accès depuis RPi3 (SGBD)          | RPi3 se connecte au hotspot              | `ping 8.8.8.8` depuis RPi3               | Accès Internet fonctionnel         |   ✔                 |    🟢 OK    |

---
## 5. Observations et points d’amélioration
- **Succès** : Le hotspot est stable et le NAT fonctionne correctement.
- **Points à améliorer** :
  - Ajouter un script de monitoring pour surveiller la charge CPU lors de multiples connexions.
  - Documenter la procédure de changement du mot de passe Wi-Fi.

---
## 6. Validation globale
**Statut final** : 🟢 **Terminé**  
**Commentaires** : Tout est terminé. Le système est fonctionnel et stable.

---
