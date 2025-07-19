# Analyse des Transports en Commun Ilevia - Données GTFS

## Description

Ce projet analyse les données de transport en commun du réseau **Ilevia** de la **Métropole Européenne de Lille (MEL)** en utilisant les fichiers **GTFS** (General Transit Feed Specification). L'analyse comprend l'exploration des horaires, des itinéraires, des arrêts et la visualisation cartographique du réseau.

## 📊 Données GTFS utilisées

Le projet utilise les fichiers GTFS standard d'Ilevia :

- **agency.txt** : Informations sur l'agence de transport
- **calendar_dates.txt** : Exceptions de calendrier et dates spéciales
- **routes.txt** : Définition des lignes de transport
- **stop_times.txt** : Horaires de passage aux arrêts
- **stops.txt** : Localisation et informations des arrêts
- **trips.txt** : Voyages programmés sur chaque ligne

## 🗂️ Structure des données

### Agency (Agence)
| Champ | Description |
|-------|-------------|
| `agency_id` | Identifiant unique de l'agence |
| `agency_name` | Nom de l'agence (Ilevia) |
| `agency_url` | Site web officiel |
| `agency_timezone` | Fuseau horaire |
| `agency_lang` | Langue utilisée |
| `agency_phone` | Numéro de téléphone |

### Routes (Lignes)
| Champ | Description |
|-------|-------------|
| `route_id` | Identifiant unique de la ligne |
| `route_short_name` | Nom court (ex: M1, T, 920) |
| `route_long_name` | Nom complet de la ligne |
| `route_type` | Type de transport (métro, bus, tram) |
| `route_color` | Couleur de la ligne |

### Stops (Arrêts)
| Champ | Description |
|-------|-------------|
| `stop_id` | Identifiant unique de l'arrêt |
| `stop_name` | Nom de l'arrêt |
| `stop_lat` | Latitude |
| `stop_lon` | Longitude |
| `wheelchair_boarding` | Accessibilité PMR |

### Stop Times (Horaires)
| Champ | Description |
|-------|-------------|
| `trip_id` | Identifiant du voyage |
| `arrival_time` | Heure d'arrivée |
| `departure_time` | Heure de départ |
| `stop_id` | Identifiant de l'arrêt |
| `stop_sequence` | Ordre dans le trajet |

## 🛠️ Technologies utilisées

### Bibliothèques Python
```python
import pandas as pd      # Manipulation des données
import folium           # Cartographie interactive
import matplotlib.pyplot as plt  # Graphiques
import seaborn as sns   # Visualisations statistiques
import requests         # Requêtes API
```

### APIs externes
- **API Adresse** (data.gouv.fr) : Géocodage d'adresses françaises

```python
# Exemple d'utilisation de l'API Adresse
link = 'https://api-adresse.data.gouv.fr/search/?q=728+Route+de+Villerest&postcode=42155'
r = requests.get(link).json()
```

## 📋 Structure du projet

```
ilevia-gtfs-analysis/
├── data/
│   ├── gtfs/
│   │   ├── agency.txt
│   │   ├── calendar_dates.txt
│   │   ├── routes.txt
│   │   ├── stop_times.txt
│   │   ├── stops.txt
│   │   └── trips.txt
│   └── processed/        # Données traitées
├── notebooks/
│   └── transport_ilevia.ipynb  # Notebook principal
├── scripts/
│   ├── data_loader.py    # Chargement des données GTFS
│   ├── geocoding.py      # Fonctions de géocodage
│   └── visualizations.py # Cartes et graphiques
├── maps/                 # Cartes générées
└── README.md
```

## 🚀 Installation et utilisation

### Prérequis
```bash
pip install pandas folium matplotlib seaborn requests
```

### Chargement des données
```python
# Chargement des fichiers GTFS
df_agency = pd.read_csv('data/gtfs/agency.txt')
df_calendar = pd.read_csv('data/gtfs/calendar_dates.txt')
df_routes = pd.read_csv('data/gtfs/routes.txt')
df_stop_times = pd.read_csv('data/gtfs/stop_times.txt')
df_stops = pd.read_csv('data/gtfs/stops.txt')
df_trips = pd.read_csv('data/gtfs/trips.txt')
```

### Lancement de l'analyse
1. Ouvrir le notebook `transport_ilevia.ipynb`
2. Exécuter les cellules dans l'ordre
3. Les visualisations et cartes seront générées automatiquement

## 📈 Analyses disponibles

### Exploration des données
- **Nombre de lignes** par type de transport
- **Répartition des arrêts** sur le territoire
- **Fréquences de passage** par ligne
- **Couverture géographique** du réseau

### Visualisations cartographiques
- **Carte interactive** des arrêts avec Folium
- **Tracé des lignes** de transport
- **Zones de desserte** et accessibilité
- **Heatmap** de la densité d'arrêts

### Analyses temporelles
- **Horaires de pointe** et creuses
- **Fréquences** par ligne et par période
- **Exceptions de service** (jours fériés, travaux)

## 🗺️ Géocodage avec l'API Adresse

Le projet utilise l'API Adresse du gouvernement français pour :
- Convertir les adresses en coordonnées GPS
- Valider les localisations des arrêts
- Enrichir les données géographiques

```python
def geocode_address(address, postcode):
    """Géocode une adresse avec l'API Adresse"""
    url = f"https://api-adresse.data.gouv.fr/search/?q={address}&postcode={postcode}"
    response = requests.get(url).json()
    if response['features']:
        coords = response['features'][0]['geometry']['coordinates']
        return coords[1], coords[0]  # lat, lon
    return None, None
```

## 📊 Indicateurs clés

### Performance du réseau
- **Nombre total d'arrêts** : À calculer depuis stops.txt
- **Nombre de lignes actives** : À calculer depuis routes.txt
- **Fréquence moyenne** : Basée sur stop_times.txt
- **Couverture territoriale** : Surface desservie

### Accessibilité
- **Arrêts PMR** : wheelchair_boarding = 1
- **Desserte par commune** : Agrégation par zone
- **Temps d'accès moyen** : Distance entre arrêts

## 🔄 Format GTFS

Le **General Transit Feed Specification (GTFS)** est un standard international pour les données de transport public. Il permet :

- **Interopérabilité** entre systèmes
- **Planification d'itinéraires** multi-modaux
- **Analyse comparative** entre réseaux
- **Applications tierces** (Google Maps, Citymapper)

## 📝 Notes techniques

### Gestion des types de données
```python
# Attention aux types mixtes dans stop_times.txt
df_stop_times = pd.read_csv('stop_times.txt', low_memory=False)
```

### Jointures importantes
```python
# Joindre les arrêts avec leurs horaires
stops_with_times = df_stops.merge(df_stop_times, on='stop_id')

# Joindre les voyages avec leurs lignes
trips_with_routes = df_trips.merge(df_routes, on='route_id')
```

## 🤝 Contribution

Les contributions sont bienvenues ! Zones d'amélioration :

1. **Optimisation des performances** pour les gros datasets
2. **Nouvelles visualisations** (3D, animations temporelles)
3. **Analyses prédictives** (retards, affluence)
4. **Export** vers d'autres formats (GeoJSON, KML)

## 📞 Contact

- **Projet** : Analyse GTFS Ilevia MEL
- **Source des données** : [Open Data Ilevia](https://opendata.ilevia.fr/)
- **API Adresse** : [api-adresse.data.gouv.fr](https://api-adresse.data.gouv.fr/)

## 🔗 Ressources utiles

- [Spécification GTFS](https://gtfs.org/)
- [Open Data Ilevia](https://opendata.ilevia.fr/)
- [API Adresse Documentation](https://adresse.data.gouv.fr/api-doc/)
- [Folium Documentation](https://python-visualization.github.io/folium/)
- [Pandas GTFS](https://gtfs.org/schedule/examples/sample-feeds/)

---

*Dernière mise à jour : [19/07/25]
