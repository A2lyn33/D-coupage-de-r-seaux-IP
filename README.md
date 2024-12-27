# D-coupage-de-r-seaux-IP
# Découpage du réseau 172.16.1.0/24

Ce document présente le découpage d'un réseau fictif en 172.16.1.0/24 en deux approches différentes : symétrique et asymétrique, pour satisfaire les besoins de quatre pôles informatiques.

## 1. Découpage Symétrique
Dans cette approche, les sous-réseaux sont égaux pour tous les pôles, même si certains disposent d'équipements moins nombreux. Nous utilisons le préfixe CIDR /26 pour chaque sous-réseau (64 adresses par sous-réseau).

### Calcul
- Nombre total d’adresses pour un réseau en /26 : 2^(32-26) = 64
- Adresses utilisables : 64 - 2 = 62 (réseau + broadcast exclus).

### Répartition des sous-réseaux
| Pôle               | CIDR          | Adresse Réseau  | Adresse de Diffusion | Adresses Utilisables       |
|---------------------|---------------|------------------|-----------------------|----------------------------|
| Informatique        | 172.16.1.0/26 | 172.16.1.0       | 172.16.1.63          | 172.16.1.1 à 172.16.1.62  |
| Développement      | 172.16.1.64/26| 172.16.1.64      | 172.16.1.127         | 172.16.1.65 à 172.16.1.126|
| Administratif       | 172.16.1.128/26| 172.16.1.128    | 172.16.1.191         | 172.16.1.129 à 172.16.1.190|
| Technicien          | 172.16.1.192/26| 172.16.1.192    | 172.16.1.255         | 172.16.1.193 à 172.16.1.254|

### Conclusion Symétrique
Ce découpage assure une allocation uniforme des ressources, mais gaspille de l'espace pour les pôles avec des besoins plus modestes.

## 2. Découpage Asymétrique
Cette approche optimise l’utilisation des adresses en adaptant la taille des sous-réseaux aux besoins réels de chaque pôle.

### Calcul
- **Pôle Informatique :** Besoin de 50 adresses. Taille réseau : /26 (64 adresses, 62 utilisables).
- **Pôle Développement :** Besoin de 12 adresses. Taille réseau : /28 (16 adresses, 14 utilisables).
- **Pôle Administratif :** Besoin de 20 adresses. Taille réseau : /27 (32 adresses, 30 utilisables).
- **Pôle Technicien :** Besoin de 15 adresses. Taille réseau : /28 (16 adresses, 14 utilisables).

### Répartition des sous-réseaux
| Pôle               | CIDR           | Adresse Réseau  | Adresse de Diffusion | Adresses Utilisables        |
|---------------------|----------------|------------------|-----------------------|-----------------------------|
| Informatique        | 172.16.1.0/26  | 172.16.1.0       | 172.16.1.63          | 172.16.1.1 à 172.16.1.62   |
| Développement      | 172.16.1.64/28 | 172.16.1.64      | 172.16.1.79          | 172.16.1.65 à 172.16.1.78  |
| Administratif       | 172.16.1.80/27 | 172.16.1.80      | 172.16.1.111         | 172.16.1.81 à 172.16.1.110 |
| Technicien          | 172.16.1.112/28| 172.16.1.112     | 172.16.1.127         | 172.16.1.113 à 172.16.1.126|

### Conclusion Asymétrique
Ce découpage répond aux besoins précis des pôles tout en maximisant l’utilisation des adresses IP disponibles.

## Synthèse
Le découpage asymétrique est plus efficace car il évite le gaspillage d'adresses tout en couvrant les besoins prévus pour chaque pôle.

