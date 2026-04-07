# 🏙️ Seattle Building Energy & CO₂ Prediction

> Projet réalisé dans le cadre du **Bootcamp - Maitrisez les algorithmes de machine learning** d’**OpenClassrooms**

<p align="center">
  <img src="seattle_logo.png" alt="Seattle" width="320">
</p>

---

## ✨ Contexte

Vous travaillez en tant que **Data Scientist pour la ville de Seattle**.  
Dans le cadre de son objectif de **neutralité carbone à l’horizon 2050**, la ville s’intéresse de près à la consommation énergétique et aux émissions de CO₂ des **bâtiments non résidentiels**.

Des relevés détaillés ont été réalisés en **2016** par les services municipaux. Ces mesures étant coûteuses à obtenir, l’objectif de ce projet est de **prédire** :

- la **consommation énergétique totale** des bâtiments : `SiteEnergyUse(kBtu)` ;
- les **émissions totales de CO₂** : `TotalGHGEmissions`.

Les prédictions reposent uniquement sur des **données structurelles des bâtiments**, comme :

- la taille ;
- l’usage principal ;
- l’année de construction ;
- le nombre d’étages ;
- la localisation ;
- et d’autres caractéristiques descriptives.

---

## 🎯 Problématique

À partir des relevés déjà disponibles, il s’agit de construire des modèles capables d’estimer la consommation énergétique et les émissions de CO₂ de bâtiments non résidentiels **pour lesquels ces mesures n’ont pas encore été réalisées**.

Plus précisément, le projet devait permettre de :

- mener une **analyse exploratoire courte mais pertinente** pour faire ressortir les principaux enseignements sur les bâtiments étudiés ;
- tester **plusieurs modèles supervisés** pour la prédiction de la consommation énergétique et des émissions ;
- identifier les **facteurs les plus influents** dans les performances des modèles retenus.

---

## 🧠 Démarche suivie

Le projet a été mené selon une démarche complète de data science.

### 1. Préparation des données
- sélection du périmètre des bâtiments non résidentiels ;
- nettoyage des données ;
- traitement des valeurs incohérentes ;
- suppression de certaines observations atypiques ;
- gestion des valeurs manquantes.

### 2. Analyse exploratoire
- distributions des variables cibles ;
- histogrammes et boxplots ;
- analyse des asymétries et des outliers ;
- étude des corrélations ;
- visualisations géographiques.

### 3. Feature engineering
Création et enrichissement de plusieurs variables utiles, notamment :
- `BuildingAge`
- `GFA_per_floor`
- variables transformées avec `log1p`
- variables dérivées liées aux surfaces

### 4. Modélisation supervisée
Comparaison de plusieurs modèles :
- `DummyRegressor`
- `LinearRegression`
- `RandomForestRegressor`
- `ExtraTreesRegressor`
- `SVR`
- `KNeighborsRegressor`
- `XGBoostRegressor`

### 5. Étude de la transformation logarithmique
Analyse de l’effet de `log1p` sur :
- la forme des distributions ;
- la stabilité des modèles ;
- les performances de prédiction.

### 6. Modélisation multi-output
Construction d’un modèle unique capable de prédire simultanément :
- `SiteEnergyUse(kBtu)`
- `TotalGHGEmissions`

### 7. Optimisation et interprétation
- `GridSearchCV` sur les meilleurs modèles retenus ;
- `Permutation Importance` pour les modèles non basés sur les arbres ;
- `feature_importances_` pour les modèles à arbres.

---

## 📊 Résultats principaux

### 🔋 Meilleur modèle pour `SiteEnergyUse(kBtu)`
Le meilleur modèle retenu est :

**`LinearRegression` sur `log1p(SiteEnergyUse(kBtu))`**

Ce résultat montre qu’après réduction de l’asymétrie de la cible, une structure globalement linéaire permet déjà d’obtenir de très bonnes performances.

### 🌍 Meilleur modèle pour `TotalGHGEmissions`
Le meilleur modèle retenu est :

**`ExtraTreesRegressor` optimisé sur la cible brute**

L’optimisation améliore nettement les performances du modèle, ce qui confirme que la prédiction des émissions de CO₂ bénéficie ici d’un modèle flexible capable de capturer des relations non linéaires complexes.

### 🔗 Meilleur modèle multi-output
Le meilleur modèle conjoint retenu est :

**`LinearRegression` sur les deux cibles transformées par `log1p`**

Cette approche permet de prédire simultanément l’énergie et le CO₂ avec un modèle simple, stable et interprétable.

---

## 📈 Enseignements clés

Les analyses menées mettent en évidence plusieurs constats importants :

- les deux cibles présentent une **forte asymétrie à droite** ;
- la transformation logarithmique est **très bénéfique** pour la modélisation de `SiteEnergyUse(kBtu)` ;
- pour `TotalGHGEmissions`, l’effet du logarithme est plus **nuancé** selon le modèle ;
- la **taille du bâtiment** joue un rôle majeur dans les prédictions ;
- le **type de bâtiment** est une variable très structurante ;
- `ENERGYSTARScore` apporte une information prédictive utile.

---

## 📌 Variables importantes

Les analyses d’importance de variables montrent que les facteurs les plus influents sont principalement liés :

- à la **surface totale du bâtiment** ;
- à la **surface associée à l’usage principal** ;
- au **type de propriété / type de bâtiment** ;
- à la **performance énergétique** ;
- et, dans certains cas, à la **localisation**.

Pour les émissions de CO₂, certaines catégories particulières, comme les bâtiments de type **Hospital**, ressortent fortement dans le modèle final.

---

## ⚠️ Limites

Comme tout projet de modélisation, ce travail présente plusieurs limites :

- certaines variables comportent un nombre important de valeurs manquantes ;
- plusieurs variables explicatives restent corrélées entre elles ;
- les résultats dépendent du choix de l’échelle de travail ;
- les importances de variables ne doivent pas être interprétées comme des relations causales ;
- les performances restent conditionnées par les variables disponibles dans le dataset.

---

## 🚀 Pistes d’amélioration

Plusieurs prolongements pourraient être envisagés :

- approfondir la sélection de variables ;
- tester des méthodes d’interprétation plus avancées, comme **SHAP** ;
- explorer d’autres modèles ou approches d’ensemble ;
- enrichir le dataset avec des variables contextuelles complémentaires ;
- pousser plus loin l’optimisation en multi-output.

---

## 🗂️ Structure du projet

```text
Prediction_consommation_energetique_et_emissions_CO2_batiments_Seattle_FAYE_Amadou_Lamine/
├── FAYE_Amadou_Lamine_1_notebooks_032026/
├── FAYE_Amadou_Lamine_2_presentation_032026/
└── FAYE_Amadou_Lamine_3_readme_032026/
```

---

## 🛠️ Technologies utilisées

- Python
- Pandas
- NumPy
- Scikit-learn
- XGBoost
- Matplotlib
- Seaborn
- Folium
- Jupyter Notebook

---

## 📚 Source des données

Jeu de données officiel de la ville de Seattle :

**Building Energy Benchmarking Data (2015-Present)**  
Source : `https://data.seattle.gov/Built-Environment/Building-Energy-Benchmarking-Data-2015-Present/teqw-tu6e/about_data`

---

## 👨‍💻 Auteur

**Amadou Lamine Faye**

---

## 📌 Cadre du projet

Ce projet a été réalisé dans le cadre du **Bootcamp - Maitrisez les algorithmes de machine learning** proposé par **OpenClassrooms**.

Le travail s’inscrit dans une logique de montée en compétence progressive sur :

- l’analyse exploratoire de données ;
- la modélisation supervisée ;
- la comparaison méthodique de modèles ;
- l’interprétation des résultats ;
- et l’optimisation raisonnée de modèles de machine learning.

---

## 📜 Licence

Projet académique à visée pédagogique.

---

## ✅ Conclusion

Ce projet montre qu’une démarche méthodique permet de construire des modèles **cohérents, performants et interprétables** pour des problématiques environnementales complexes.

Au-delà des scores obtenus, il met surtout en évidence l’importance :

- du prétraitement ;
- du choix de l’échelle de travail ;
- de la comparaison rigoureuse entre modèles ;
- de l’optimisation ciblée ;
- et de l’interprétation des variables influentes.

Il répond ainsi concrètement à la problématique initiale : **prédire la consommation énergétique et les émissions de CO₂ de bâtiments non résidentiels de Seattle à partir de leurs caractéristiques structurelles**.
