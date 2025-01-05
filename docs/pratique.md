# Partie Pratique

## 1. Diagnostic du problème de connectivité

### 1.1 Problème identifié
- L'équipe communication (réseau 10.0.0.0/24) ne peut pas accéder au Wiki (10.0.2.223)
- Message d'erreur lors du ping : "destination host unreachable"

### 1.2 Analyse du réseau
- Équipe communication : 10.0.0.0/24
- Réseau du Wiki : 10.0.2.0/24
- Le routeur de communication (Router_Com) n'a pas de route vers le réseau du Wiki

## 2. Solution mise en place

### 2.1 Configuration du routeur jaune (Router_Com)
1. Ajout de la route manquante :
   ```
   ip route 10.0.2.0 255.255.255.0 10.1.0.2    # Route vers le réseau des serveurs (Wiki)
   ```

## 3. Validation
1. Test de ping depuis PC communication vers Wiki :
   ```
   ping 10.0.2.223
   ```
2. Test de traceroute pour vérifier le chemin :
   ```
   tracert 10.0.2.223
   ```

## 4. Optimisation du plan d'adressage (Problème secondaire)
- Actuel : Les réseaux utilisent des masques /24 (254 adresses disponibles)
- Proposition d'optimisation pour le réseau communication :
  - 8 personnes → besoin de 16 adresses → masque /28 suffisant
  - Nouvelle configuration : 10.0.0.0/28
