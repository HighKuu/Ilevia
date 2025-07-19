
# 🚍 API Transports en Commun - Ilevia MEL

## 📘 Description
Ce projet analyse les données de transport en commun du réseau **Ilevia** de la **Métropole Européenne de Lille (MEL)**.  
Il utilise l'API officielle pour récupérer les informations en **temps réel** sur les prochains passages des **bus**, **tramways** et **métros**.

---

## 📊 Données disponibles
L'API fournit des informations détaillées sur :

- **Identifiants des stations** : Codes uniques pour chaque arrêt  
- **Noms des stations** : Dénominations complètes des arrêts  
- **Codes des lignes** : Identifiants des lignes de transport  
- **Directions** : Terminus et sens de circulation  
- **Horaires en temps réel** : Heures estimées de passage  
- **Métadonnées** : Dates de modification, clés de tri  

---

## 🚌 Exemple de données

```json
{
  "@id": "prochains_passages.1264293270",
  "identifiant_station": "ILEVIA:StopPoint:BP:ZON002:LOC",
  "nom_station": "PIERRE BRIZON",
  "code_ligne": "920",
  "sens_ligne": "A. DUMAS",
  "heure_estimee_depart": "2025-05-02T16:51:59.000+00:00",
  "date_modification": "2025-05-02T16:21:59.358+00:00",
  "cle_modification": "SIRI:304559847",
  "cle_tri": "A. DUMAS/PIERRE BRIZON/2025-05-02T16:51:59.000+02:00"
}
```

---

## 🔧 Structure de l'API

### 📦 Format de réponse

- **Format** : JSON  
- **Nombre total de records** : 5399 (exemple)  
- **Encodage** : UTF-8  
- **Fuseau horaire** : Europe/Paris (+02:00)

### 📑 Champs principaux

| Champ                 | Type      | Description                                 |
|----------------------|-----------|---------------------------------------------|
| `@id`                | String    | Identifiant unique du passage               |
| `identifiant_station`| String    | Code technique de la station                |
| `nom_station`        | String    | Nom affiché de la station                   |
| `code_ligne`         | String    | Code de la ligne de transport               |
| `sens_ligne`         | String    | Direction / terminus de la ligne            |
| `heure_estimee_depart`| DateTime | Heure de passage estimée                    |
| `date_modification`  | DateTime  | Dernière mise à jour                        |
| `cle_modification`   | String    | Clé de version SIRI                         |

---

## 🚇 Types de transport

Le réseau Ilevia comprend :

- **Métro** : Lignes `M1` et `M2`  
- **Tramway** : Lignes `T`, `TRAM`  
- **Bus** : Lignes numérotées (ex : `920`, `ATSE`)  
- **Navettes** : Services spéciaux et lignes de proximité  

---

## 🌍 Couverture géographique

- **Territoire** : Métropole Européenne de Lille  
- **Communes desservies** : Lille, Roubaix, Tourcoing, Villeneuve-d'Ascq, et 90 autres communes  
- **Stations principales** :
  - Pierre Brizon  
  - V. d'Ascq 4 Cantons Stade P. Mauroy  
  - Sequedin Centre  

---

## 📈 Cas d’usage

### Analyse des données

- Étude de la fréquentation  
- Analyse des retards et ponctualité  
- Optimisation des parcours  
- Statistiques de performance du réseau  

### Applications possibles

- Application mobile d’horaires  
- Tableau de bord en temps réel  
- Système d'information voyageurs  
- Outils de planification de trajets  

---

## 🛠️ Technologies recommandées

### Langages

- **Python** : `pandas`, `requests`, `matplotlib`  
- **JavaScript** : `Node.js`, `React`  
- **R** : `tidyverse`, `httr`  
- **Java** : `Spring Boot`, `Jackson`

### Bases de données

- **PostgreSQL** : Stockage des données historiques  
- **InfluxDB** : Données de séries temporelles  
- **Redis** : Cache en temps réel  

---

## 📋 Structure du projet

```
ilevia-transport-analysis/
├── data/
│   ├── raw/              # Données brutes de l'API
│   ├── processed/        # Données nettoyées
│   └── exports/          # Exports et rapports
├── scripts/
│   ├── api_client.py     # Client API
│   ├── data_analysis.py  # Analyse des données
│   └── visualizations.py # Graphiques et cartes
├── docs/
│   ├── api_documentation.md
│   └── data_dictionary.md
└── README.md
```

---

## 🚀 Installation et utilisation

```bash
# Cloner le repository
git clone https://github.com/username/ilevia-transport-analysis
cd ilevia-transport-analysis

# Installer les dépendances
pip install -r requirements.txt

# Lancer l’analyse
python scripts/api_client.py
```

---

## 📊 Métriques et KPIs

- **Ponctualité** : % de passages à l’heure  
- **Fréquence** : Intervalles entre passages  
- **Couverture** : Nombre de stations actives  
- **Fiabilité** : Taux de mise à jour des données  

---

## 🤝 Contribution

Les contributions sont les bienvenues !  
Merci de :

1. Fork le projet  
2. Créer une branche `feature`  
3. Commiter vos changements  
4. Pousser vers la branche  
5. Ouvrir une **Pull Request**  

---

## 📝 Licence

Ce projet est sous licence **MIT**.  
Voir le fichier `LICENSE` pour plus de détails.

---

## 📞 Contact

- **Auteur** : Halim  
- **Email** : halim.moulay@gmail.com  
- **Lien du projet** : [[https://github.com/username/ilevia-transport-analysis](https://github.com/username/ilevia-transport-analysis)](https://github.com/HighKuu/Ilevia)

---

## 🔗 Ressources utiles

- [Site officiel Ilevia](https://www.ilevia.fr)  
- [Métropole Européenne de Lille](https://www.lillemetropole.fr)  
- [Documentation API Transports](#)  
- [Spécifications SIRI](https://www.transmodel-cen.eu/siri/)
