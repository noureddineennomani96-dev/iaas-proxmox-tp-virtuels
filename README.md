# ☁️ IaaS Proxmox VE – Plateforme de TP virtuels

Projet de fin d'études : conception, déploiement et validation d'une infrastructure
IaaS open source basée sur **Proxmox VE** pour la gestion des travaux pratiques
virtuels à l'École Supérieure de Technologie d'Ouarzazate (ESTO).

> DUT Gestion des Réseaux & Sécurité – Université Ibn Zohr, Agadir – 2025/2026

## 🎯 Contexte et objectif

Les laboratoires de l'ESTO font face à plusieurs contraintes : parc limité
(20 postes pour 30 étudiants), réinstallation longue après les TP destructifs,
absence d'isolation entre étudiants, coût des licences.

Ce projet fournit une plateforme légère, économique et évolutive où :
- les **enseignants** déploient des environnements standardisés en quelques minutes ;
- les **étudiants** accèdent à leurs VM depuis un navigateur, à l'école ou à domicile ;
- les environnements sont **isolés** et **réinitialisables** via snapshots.

## 🏗️ Architecture

Plateforme mono-nœud centrée sur Proxmox VE (KVM + LXC), avec 5 principes :
simplicité, isolation, accès unifié via le web, réutilisabilité, évolutivité.

| Élément | Détail |
|---|---|
| Hyperviseur | Proxmox VE (basé sur Debian 12) |
| Virtualisation | KVM (VM) et LXC (conteneurs) |
| Environnement de test | VMware Workstation (virtualisation imbriquée) |
| Stockage | LVM local |
| Accès | Interface web HTTPS (port 8006) |

### Comparatif étudié
Proxmox VE a été retenu face à OpenStack, oVirt et Xen pour sa simplicité
d'installation, sa légèreté et son interface web intégrée.

## 🗂️ Organisation des ressources

**Pools :**

| Pool | Usage |
|---|---|
| `Modeles_TP` | Templates réutilisables |
| `TP_Systemes` | TP systèmes d'exploitation |
| `TP_Securite` | TP sécurité (Kali, outils) |
| `TP_Developpement` | TP développement (Debian, code) |

**Rôles personnalisés :**

| Rôle | Droits |
|---|---|
| `Role-Enseignant` | Création, modification, clonage, snapshots, console, démarrage/arrêt |
| `Role-Etudiant` | Visualisation, console, démarrage/arrêt |

**Templates :** Ubuntu 22.04, Debian 12, Kali Linux.

## ✅ Tests de validation

- Un étudiant ne voit que son pool dédié (isolation)
- L'enseignant voit tous les pools et toutes les VM
- Déploiement rapide par clonage de templates
- Réinitialisation via snapshots

## 🚀 Reproduire l'installation

1. Créer une VM (Debian 12 x64) sous VMware Workstation, activer la
   virtualisation imbriquée (VT-x/AMD-V)
2. Installer Proxmox VE depuis l'ISO officielle
3. Configurer une IP statique dans `/etc/network/interfaces`, puis :
```bash
   systemctl restart networking
```
4. Accéder à `https://<IP-PROXMOX>:8006`
5. Créer les pools, rôles et utilisateurs (Datacenter → Pool / Permissions)
6. Téléverser les ISO, créer les VM puis les convertir en templates

## 🔭 Perspectives

- Intégration d'OpenStack
- Portail web étudiant
- Cluster Proxmox multi-nœuds (Ceph/NFS)
- Déploiement réel au sein de l'établissement

## 👥 Auteurs

- **ENNOMANI Noureddine**
- **GAZA Chaymae**
- **GAMGAM Farah**

Encadrant : M. OUKHATAR Ayoub  
École Supérieure de Technologie d'Ouarzazate – Filière GRS

## 📄 Licence

Projet académique (ou choisir une licence, ex. MIT).
