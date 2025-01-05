# Partie Théorique

## 1. Adressage IP et Réseaux

### 1.1 Définition d'une Adresse IP
- Identifiant numérique unique attribué à chaque équipement réseau

- Format IPv4 : 4 octets séparés par des points (ex: 192.168.1.1)

- Notation CIDR (Classless Inter-Domain Routing)
  * Exemple : 192.168.1.0/24 où /24 indique que les 24 premiers bits sont la partie réseau
  * Remplace l'ancien système de classes (A, B, C)

### 1.2 Structure d'un Plan d'Adressage

Pour chaque réseau, on distingue :

- **Adresse réseau** : Première adresse, identifie le réseau (tous les bits hôtes à 0)

- **Plage d'adresses utilisables** : Adresses attribuables aux équipements

- **Adresse de broadcast** : Dernière adresse, permet la diffusion (tous les bits hôtes à 1)

### 1.3 Exemple de Plan d'Adressage

Réseau 192.168.1.0/24 (masque 255.255.255.0)

| Type d'information       | Valeur                  |
|-------------------------|------------------------|
| Adresse réseau          | 192.168.1.0            |
| Plage utilisable        | 192.168.1.1 à 192.168.1.254 |
| Adresse de diffusion    | 192.168.1.255          |

## 2. Adresses Publiques vs Privées

### 2.1 Différences Principales
- **Adresses Publiques** :
  * Routables sur Internet
  * Uniques mondialement
  * Attribuées par les registres Internet régionaux (RIR)

- **Adresses Privées** :
  * Utilisées dans les réseaux locaux
  * Non routables sur Internet
  * Nécessitent du NAT pour accéder à Internet

### 2.2 Plages d'Adresses Privées (RFC 1918)
- Classe A : 10.0.0.0 à 10.255.255.255 (/8)

- Classe B : 172.16.0.0 à 172.31.255.255 (/12)

- Classe C : 192.168.0.0 à 192.168.255.255 (/16)

## 3. DHCP (Dynamic Host Configuration Protocol)

### 3.1 Principe
- Service automatisant l'attribution des configurations IP
- Évite la configuration manuelle des postes clients
- Gestion centralisée des adresses IP

### 3.2 Configuration d'un Serveur DHCP
1. **Éléments à configurer** :
   - Plage d'adresses à distribuer (pool)
   - Masque de sous-réseau
   - Passerelle par défaut
   - Serveurs DNS
   - Durée du bail (lease time)

2. **Processus DORA** :
   - Discover (client)
   - Offer (serveur)
   - Request (client)
   - Acknowledge (serveur)

## 4. Routage

### 4.1 Définition d'une Route
- Chemin qu'empruntent les paquets pour atteindre leur destination
- Composée de : Réseau de destination, Masque, Interface de sortie/Next-hop

### 4.2 Types de Routes
1. **Routes Statiques**
   - Configurées manuellement
   - Stables mais peu flexibles
   - Exemple de configuration CLI :
     ```
     ip route [réseau_dest] [masque] [next-hop/interface]
     ```

2. **Routes Dynamiques**
   - Apprises automatiquement via protocoles de routage
   - S'adaptent aux changements du réseau
   - Protocoles : RIP, OSPF, BGP...

3. **Route par Défaut**
   - Utilisée quand aucune route plus spécifique n'existe
   - Configuration CLI : 
     ```
     ip route 0.0.0.0 0.0.0.0 [next-hop/interface]
     ```

## 5. Diagnostic Réseau

### 5.1 Commandes Principales
1. **ipconfig**
   - Affiche la configuration IP
   - Options utiles :
     * /all : configuration détaillée
     * /release : libère le bail DHCP
     * /renew : renouvelle le bail DHCP

2. **ping**
   - Teste la connectivité
   - Utilise le protocole ICMP
   - Exemple : `ping 192.168.1.1`

3. **tracert**
   - Affiche le chemin vers une destination
   - Montre les routeurs intermédiaires
   - Exemple : `tracert www.google.com`

4. **show** (sur équipements réseau)
   - `show ip route` : table de routage
   - `show interfaces` : état des interfaces
   - `show running-config` : configuration active

### 5.2 Messages ICMP Courants
- **Destination unreachable** : hôte ou réseau inaccessible
- **Time exceeded** : TTL expiré en transit
- **Request timed out** : pas de réponse dans le délai
- **Network unreachable** : pas de route vers le réseau
- **Host unreachable** : hôte non joignable sur le réseau