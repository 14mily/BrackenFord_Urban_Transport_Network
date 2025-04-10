# 🧠 Rapport Technique – Projet Java : Réseau de Transport Urbain de Brackenford (BUTN)

---

## 📑 Sommaire

1. [📚 Description du projet](#-description-du-projet)
2. [🎯 Objectifs pédagogiques et techniques](#-objectifs-pédagogiques-et-techniques)
3. [⚙️ Spécifications](#-spécifications)
4. [🧪 Méthodologie de développement](#-méthodologie-de-développement)
5. [📦 Choix des classes et énumérations](#-choix-des-classes-et-énumérations)
6. [📊 Choix des structures de données](#-choix-des-structures-de-données)
7. [🧮 Choix des algorithmes](#-choix-des-algorithmes)
8. [✅ Résultats](#-résultats)
9. [🚀 Instructions de compilation et exécution](#-instructions-de-compilation-et-exécution)

---

## 📚 Description du projet

Ce projet est une preuve de concept (POC) pour un système d'information permettant de gérer les transports publics urbains de la ville fictive de Brackenford. Les usagers peuvent consulter les lignes, stations, planifier un itinéraire, estimer le temps de trajet, la distance parcourue, le coût, tout en tenant compte de leur profil (étudiant, senior, handicapé…).
---

## 🎯 Objectifs pédagogiques et techniques

- Structurer un projet orienté objet de A à Z.
- Implémenter une logique tarifaire multi-critères.
- Prendre en compte la distance réelle et l’accessibilité.
- Produire un système extensible, en vue de l'intégration d’algorithmes comme Dijkstra.

---

## ⚙️ Spécifications

Le système est 100% en Java, sans interface graphique, en ligne de commande. Il prend en charge :

- 26 stations (A à Z)
- 3 modes de transport (metro, tramway et bus)
- 4 types de passagers (normal, étudiant, senior et handicapé)
- Un tarif basé sur la distance et le profil
- Les stations non accessibles pour certains types d'usagers

---

## 🧪 Méthodologie de développement

Le projet a été découpé en 10 étapes successives, chacune validant une fonctionnalité. Un `main()` de test permet de valider chaque composant en isolation. Ces étapes sont les suivantes :

 1. Lister les stations en ordre alphabétique (inverse)
 2. Information sur chaque ligne
 3. Information détaillée sur chaque station
 4. calculer et afficher un itinéraire
 5. Afficher un itinéraire en détail
 6. itinéraire doit prendre en compte type de passager
 7. itinéraire doit prendre en compte réglage (plus vite, plus court, moins cher, …)
 8. itinéraire doit prendre en compte des passagers handicapées
 9. calculer distances entre stations
 10. ajouter autre fonctionnalité nécessaire

---

## 📦 Choix des classes et énumérations

### 🎓 Exemple : Enumération `TransportType`

```java
public enum TransportType {
    METRO(0.40, 1.2, 500),
    TRAM(0.30, 1.0, 400),
    BUS(0.20, 0.8, 300);
}
```

### 📍 Exemple : Classe `Station`

```java
public class Station {
    private final String nom;
    private final double latitude;
    private final double longitude;
    private final boolean accessible;
}
```

---

## 📊 Choix des structures de données

- `TreeMap<String, Station>` pour classer les stations par ordre alphabétique.
- `ArrayList<Station>` dans les lignes, pour l'ordre des stations.
- `HashSet<String>` pour les services, sans doublon.
- Des structures comme `PriorityQueue` sont prévues pour des algorithmes futurs (Dijkstra).

### 🧠 Exemple : tri alphabétique inverse

```java
public List<Station> getStationsAlphabetInverse() {
    List<Station> liste = new ArrayList<>(stations.values());
    liste.sort((a, b) -> b.getNom().compareTo(a.getNom()));
    return liste;
}
```

---

## 🧮 Choix des algorithmes

### 📏 Distance avec Haversine

```java
public static double calculerDistance(Station depart, Station arrivee) {
    double a = Math.pow(Math.sin(deltaLat / 2), 2) +
               Math.cos(lat1) * Math.cos(lat2) * Math.pow(Math.sin(deltaLong / 2), 2);
    return RAYON_TERRE_METRES * 2 * Math.atan2(Math.sqrt(a), Math.sqrt(1 - a));
}
```

### 💸 Coût avec profil passager

```java
double cout = 1.5 + (distance / 1000.0 * transport.multiplicateurTarifaire);
cout *= voyageur.getTypePassager().reduction;
```

---

### 🛠️ Problèmes rencontrés et solutions

| Problème                  | Solution                                   |
| ------------------------- | ------------------------------------------ |
| Stations non accessibles  | Vérification dans `Voyageur.peutAcceder()` |
| Tarification floue        | Regroupement logique dans `TransportType`  |
| Tri des noms non accentué | Encodage UTF-8 + `TreeMap`                 |

---

## ✅ Résultats 

Le système :

- Affiche toutes les stations en ordre inverse
- Affiche les lignes et leurs stations
- Simule un voyage avec distance, temps, coût, accessibilité
  
---

## 🚀 Instructions de compilation et exécution

### 1. Compilation

```bash
javac *.java
```

### 2. Exécution

```bash
java Main
```

### 3. Exemple de sortie

```bash
Départ : Ashford Road (Non-accessible)
Arrivée : Castle Hill (Accessible)
Mode de transport : BUS
Type de passager : SENIOR
Distance : 1234.56 mètres
Temps estimé : 124.56 secondes
Coût total : 1.92 €
Itinéraire accessible.
```

---

 Par Emilie Koboyo GNASSINGBE [14mily](https://github.com/14mily/)
