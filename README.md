# Simulation d'une Succursale Bancaire

## 📋 Description du Projet

Ce projet simule le fonctionnement quotidien d'une succursale bancaire sur une période de 1000 jours. Il modélise les interactions entre deux types de clients (A et B) et deux types d'employés (caissiers de type C et conseillers de type D), en tenant compte des files d'attente, des rendez-vous et des temps de service.

### Objectif

L'objectif principal est d'analyser et d'optimiser la gestion des risques financiers liés aux temps d'attente et à l'allocation des ressources humaines dans une institution bancaire.

## 🏗️ Architecture du Projet

Le projet est structuré selon une architecture orientée objet avec les classes suivantes :

### Classes Principales

- **Client** (classe abstraite)
  - Attributs : `arrivalTime`, `serviceTime`
  
- **ClientA** (hérite de Client)
  - Clients sans rendez-vous
  - Arrivent selon un processus de Poisson
  - Servis par les caissiers et les conseillers (priorité aux caissiers)
  - Temps de service : loi lognormale (μₐ, σₐ)

- **ClientB** (hérite de Client)
  - Clients avec rendez-vous de 30 minutes
  - Servis uniquement par les conseillers
  - Probabilité `p` de ne pas se présenter
  - Retard possible : loi normale (μᵣ, σᵣ)
  - Temps de service : loi lognormale (μᵦ, σᵦ)

- **Caissier**
  - Servent uniquement les clients de type A
  - Nombre variable selon les périodes (n₁, n₂, n₃)

- **Conseiller**
  - Servent les deux types de clients (priorité aux clients B)
  - Gestion de 12 plages horaires de 30 minutes
  - Probabilité `r` d'avoir un rendez-vous par plage

- **Plage**
  - Représente une période de 30 minutes
  - Attributs : `numeroPlage`, `Rv` (rendez-vous)

- **RendezVous**
  - Attributs : `heureRv`, `numeroClientB`

- **Succursale**
  - Classe principale contenant la logique de simulation
  - Gère les événements (arrivées, départs)
  - Collecte les statistiques

## 📊 Fonctionnalités

### Simulation des Événements

- **ArrivalA** : Gestion de l'arrivée des clients de type A
- **DepartureA** : Gestion du départ des clients de type A
- **ArrivalB** : Gestion de l'arrivée des clients de type B
- **DepartureB** : Gestion du départ des clients de type B
- **NextPeriod** : Transition entre les périodes horaires

### Métriques Calculées

- **Pour les clients A** :
  - Temps d'attente moyen (Wₐ)
  - Nombre de clients servis par jour
  - Distribution des temps d'attente

- **Pour les clients B** :
  - Temps d'attente moyen (Wᵦ)
  - Nombre de clients servis par jour
  - Taux de présence aux rendez-vous

## 🚀 Installation et Utilisation

### Prérequis

- Java JDK 8 ou supérieur
- SSJ (Stochastic Simulation in Java) library
- Un IDE Java (Eclipse, IntelliJ IDEA, etc.)

### Compilation

```bash
javac -cp .:ssj.jar stochastique/*.java
```

### Exécution

```bash
java -cp .:ssj.jar stochastique.Succursale
```

## 📈 Résultats de Simulation

### Sur 1000 jours

**Clients A :**
- Nombre de clients reçus : 56 à 114 par jour
- Temps d'attente moyen : ~0.766 secondes
- Variance : 238.149

**Clients B :**
- Nombre de clients servis : 1 à 3 par jour
- Temps d'attente moyen : ~-3.712 secondes (négatif dû aux arrivées anticipées)
- Variance : 968.045

### Visualisation

Le projet génère des histogrammes illustrant :
- Distribution des temps d'attente pour les clients A
- Distribution des temps d'attente pour les clients B

## 🔧 Configuration

Les paramètres de simulation peuvent être ajustés dans un fichier de configuration :

- `λⱼ` : Taux d'arrivée des clients A (processus de Poisson)
- `μₐ, σₐ` : Paramètres de la loi lognormale pour le temps de service des clients A
- `μᵦ, σᵦ` : Paramètres de la loi lognormale pour le temps de service des clients B
- `μᵣ, σᵣ` : Paramètres de la loi normale pour les retards
- `p` : Probabilité d'absence d'un client B
- `r` : Probabilité qu'un rendez-vous soit prévu
- `s` : Seuil de temps avant rendez-vous
- `nⱼ` : Nombre de caissiers par période
- `mⱼ` : Nombre de conseillers par période

## 📁 Structure du Projet

```
stochastique/
├── Client.java
├── ClientA.java
├── ClientB.java
├── Caissier.java
├── Conseiller.java
├── Plage.java
├── RendezVous.java
└── Succursale.java
```

## 📝 Diagramme UML

Le projet inclut un diagramme de classes UML créé avec StarUML, illustrant les relations entre les différentes entités du système.

## 🔍 Méthodologie

### Approche de Simulation

1. **Initialisation** : Configuration des paramètres et création des employés
2. **Génération des événements** : Création des arrivées et rendez-vous
3. **Traitement des événements** : Gestion chronologique des actions
4. **Collecte des statistiques** : Enregistrement des métriques de performance
5. **Analyse** : Génération des rapports et histogrammes

### Gestion des Files d'Attente

- **FIFO** (First In, First Out) pour les clients A
- **Priorité aux rendez-vous** pour les conseillers
- **Temps de service stochastique** basé sur des distributions probabilistes

## 🤝 Contribution

Les contributions sont les bienvenues ! N'hésitez pas à :
- Signaler des bugs
- Proposer de nouvelles fonctionnalités
- Améliorer la documentation

## 📄 Licence

Ce projet a été réalisé dans un cadre académique.

---

**Note** : Pour plus de détails sur l'implémentation, consultez le rapport complet (`Rapport.pdf`) inclus dans le dépôt.
