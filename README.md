# 🏙️ Seattle Building Energy & CO₂ Prediction

<p align="center">
  <img src="seattle_logo.png" alt="Seattle logo" width="320">
</p>

<p align="center">
  <b>Projet réalisé dans le cadre du Bootcamp - Maitrisez les algorithmes de machine learning</b><br>
  <b>OpenClassrooms</b>
</p>

<p align="center">
  Prédiction de la consommation énergétique et des émissions de CO₂ des bâtiments non résidentiels de Seattle
</p>

---

## 🚀 Accès rapide

- 📓 **Notebook principal** : [FAYE_Amadou_Lamine_1_notebooks_032026.ipynb](./FAYE_Amadou_Lamine_1_notebooks_032026.ipynb)
- 🌐 **Notebook en HTML** : [FAYE_Amadou_Lamine_3_notebooks_032026.html](./FAYE_Amadou_Lamine_3_notebooks_032026.html)
- 📊 **Présentation** : [FAYE_Amadou_Lamine_2_presentation_032026.pptx](./FAYE_Amadou_Lamine_2_presentation_032026.pptx)
- 🖼️ **Logo Seattle** : [seattle_logo.png](./seattle_logo.png)
- 📝 **README** : [README.md](./README.md)

> La version HTML permet une lecture plus fluide du notebook directement depuis le dépôt, sans nécessiter l’ouverture de Jupyter Notebook.

---

## 📚 Sommaire

- [Contexte](#-contexte)
- [Problématique](#-problématique)
- [Objectifs](#-objectifs)
- [Démarche méthodologique](#-démarche-méthodologique)
- [Résultats principaux](#-résultats-principaux)
- [Enseignements clés](#-enseignements-clés)
- [Variables les plus influentes](#-variables-les-plus-influentes)
- [Limites](#-limites)
- [Pistes d’amélioration](#-pistes-damélioration)
- [Structure du dépôt](#-structure-du-dépôt)
- [Technologies utilisées](#-technologies-utilisées)
- [Source des données](#-source-des-données)
- [Cadre du projet](#-cadre-du-projet)
- [Conclusion](#-conclusion)

---

## ✨ Contexte

Dans ce projet, je me place dans le rôle d’un **Data Scientist travaillant pour la ville de Seattle**.

Dans le cadre de son objectif de **neutralité carbone à l’horizon 2050**, la ville s’intéresse à la **consommation énergétique** et aux **émissions de CO₂** des **bâtiments non destinés à l’habitation**.

Des relevés détaillés ont été réalisés en **2016** par les services municipaux. Ces mesures étant coûteuses à obtenir, l’objectif est de construire des modèles capables de **prédire** :

- la **consommation énergétique totale** : `SiteEnergyUse(kBtu)`
- les **émissions totales de CO₂** : `TotalGHGEmissions`

à partir des seules **caractéristiques structurelles et fonctionnelles des bâtiments**, comme :

- la taille ;
- l’usage principal ;
- l’année de construction ;
- le nombre d’étages ;
- la localisation ;
- et d’autres variables descriptives.

---

## 🎯 Problématique

À partir des relevés déjà disponibles, il s’agit d’estimer la consommation énergétique et les émissions de CO₂ de bâtiments non résidentiels **pour lesquels ces mesures n’ont pas encore été réalisées**.

Le projet répond ainsi à trois attentes principales :

- mener une **analyse exploratoire courte mais pertinente** ;
- comparer plusieurs **modèles supervisés de régression** ;
- identifier les **facteurs principaux** qui influencent les performances du ou des modèles retenus.

---

## 🎯 Objectifs

Ce projet vise à :

- comprendre la structure des données de benchmarking énergétique de Seattle ;
- nettoyer le dataset et définir un périmètre d’étude cohérent ;
- comparer plusieurs familles de modèles de régression ;
- étudier l’impact de la **transformation logarithmique** des cibles ;
- tester une approche **multi-output** pour prédire simultanément l’énergie et le CO₂ ;
- optimiser les meilleurs modèles retenus ;
- interpréter les résultats et les variables les plus influentes.

---

## 🧠 Démarche méthodologique

Le notebook suit une démarche complète de data science, cohérente avec sa structure générale.

### 1. Préparation des données
- chargement et inspection du jeu de données ;
- sélection du périmètre des bâtiments non résidentiels ;
- traitement des valeurs incohérentes ;
- gestion des valeurs manquantes ;
- suppression de certaines observations atypiques.

### 2. Analyse exploratoire
- distributions univariées des deux cibles ;
- boxplots et histogrammes ;
- comparaison visuelle de `SiteEnergyUse(kBtu)` et `TotalGHGEmissions` ;
- étude des corrélations ;
- analyse spatiale dans Seattle.

### 3. Feature engineering
Création de variables utiles pour améliorer la modélisation, notamment :
- `BuildingAge`
- `GFA_per_floor`
- `LogPropertyGFATotal`
- `LogLargestPropertyUseTypeGFA`
- transformations `log1p` sur certaines variables et sur les cibles

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
- la stabilité de l’apprentissage ;
- la hiérarchie des modèles ;
- les performances de prédiction.

### 6. Modélisation multi-output
Construction d’un modèle unique capable de prédire simultanément :
- `SiteEnergyUse(kBtu)`
- `TotalGHGEmissions`

### 7. Optimisation et interprétation
- `GridSearchCV` de petite taille sur les meilleurs modèles retenus ;
- `Permutation Importance` pour les modèles non basés sur les arbres ;
- `feature_importances_` pour les modèles à arbres.

---

## 🏆 Résultats principaux

### 🔋 Prédiction de `SiteEnergyUse(kBtu)`
Le meilleur modèle retenu est :

**`LinearRegression` sur `log1p(SiteEnergyUse(kBtu))`**

Ce résultat montre qu’après réduction de l’asymétrie de la cible, une structure globalement linéaire permet déjà d’obtenir de très bonnes performances.

### 🌍 Prédiction de `TotalGHGEmissions`
Le meilleur modèle retenu est :

**`ExtraTreesRegressor` optimisé sur la cible brute**

L’optimisation améliore nettement les performances du modèle, ce qui confirme que la prédiction des émissions de CO₂ bénéficie ici d’un modèle flexible capable de capturer des relations non linéaires plus complexes.

### 🔗 Modélisation multi-output
Le meilleur modèle conjoint retenu est :

**`LinearRegression` sur les deux cibles transformées par `log1p`**

Cette approche permet de prédire simultanément la consommation énergétique et les émissions de CO₂ avec un modèle simple, stable et interprétable.

---

## 📈 Enseignements clés

Les principaux enseignements du projet sont les suivants :

- les deux cibles présentent une **forte asymétrie à droite** ;
- la transformation logarithmique est **très bénéfique** pour la modélisation de `SiteEnergyUse(kBtu)` ;
- pour `TotalGHGEmissions`, l’effet du logarithme est plus **nuancé** et dépend du modèle considéré ;
- dans le cadre multi-output, la transformation logarithmique des deux cibles améliore nettement la qualité prédictive globale ;
- la **taille du bâtiment** constitue un facteur explicatif majeur ;
- le **type de bâtiment / type de propriété** est très structurant ;
- `ENERGYSTARScore` apporte également une information utile.

---

## 📊 Variables les plus influentes

Les analyses d’importance mettent en évidence le rôle central de variables liées :

- à la **surface totale du bâtiment** ;
- à la **surface associée à l’usage principal** ;
- au **type de propriété** (`PrimaryPropertyType`) ;
- à la **performance énergétique** (`ENERGYSTARScore`) ;
- et, dans certains cas, à la **localisation**.

Pour `SiteEnergyUse(kBtu)`, la permutation importance montre notamment l’importance de :
- `LogPropertyGFATotal`
- `PrimaryPropertyType`
- `ENERGYSTARScore`
- `LogLargestPropertyUseTypeGFA`

Pour `TotalGHGEmissions`, les `feature importances` du modèle optimisé mettent aussi en avant certaines catégories particulières, comme les bâtiments de type **Hospital**, ainsi que les variables liées à la taille et à l’usage principal.

Dans le cadre multi-output, la permutation importance confirme à nouveau la domination de :
- `LogPropertyGFATotal`
- `PrimaryPropertyType`
- `ENERGYSTARScore`

---

## ⚠️ Limites

Ce projet présente plusieurs limites :

- certaines variables, comme `ENERGYSTARScore`, comportent de nombreuses valeurs manquantes ;
- plusieurs variables explicatives restent corrélées entre elles ;
- les résultats dépendent du choix de l’échelle de travail ;
- les mesures d’importance ne doivent pas être interprétées comme des relations causales ;
- les performances restent conditionnées par les variables disponibles dans le dataset.

---

## 🚀 Pistes d’amélioration

Plusieurs prolongements pourraient être envisagés :

- affiner la sélection de variables pour limiter les redondances ;
- tester des méthodes d’interprétation plus avancées, comme **SHAP** ;
- approfondir l’optimisation d’autres modèles, notamment en multi-output ;
- explorer d’autres approches d’ensemble ;
- enrichir le jeu de données avec des variables contextuelles complémentaires si elles deviennent disponibles.

---

## 🗂️ Structure du dépôt

```text
prediction-energie-co2-seattle/
├── 2016_Building_Energy_Benchmarking.csv
├── FAYE_Amadou_Lamine_1_notebooks_032026.ipynb
├── FAYE_Amadou_Lamine_3_notebooks_032026.html
├── FAYE_Amadou_Lamine_2_presentation_032026.pptx
├── README.md
├── seattle_logo.png
├── .gitignore
└── .gitattributes

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

Source :  
https://data.seattle.gov/Built-Environment/Building-Energy-Benchmarking-Data-2015-Present/teqw-tu6e/about_data

---

## 👨‍💻 Auteur

**Amadou Lamine Faye**

---

## 📌 Cadre du projet

Ce projet a été réalisé dans le cadre du **Bootcamp - Maitrisez les algorithmes de machine learning** proposé par **OpenClassrooms**.

Il s’inscrit dans une logique de progression sur :

- l’analyse exploratoire de données réelles ;
- la modélisation supervisée ;
- la comparaison méthodique de modèles ;
- l’interprétation des résultats ;
- et l’optimisation raisonnée de modèles de machine learning.

---

## 📜 Licence

Projet académique à visée pédagogique.

---

## ✅ Conclusion

Ce projet montre qu’une démarche méthodique permet de construire des modèles **cohérents, performants et interprétables** pour une problématique environnementale concrète.

Le bilan global des modèles retenus est le suivant :

- pour `SiteEnergyUse(kBtu)` : **`LinearRegression` sur `log1p(SiteEnergyUse(kBtu))`**
- pour `TotalGHGEmissions` : **`ExtraTreesRegressor` optimisé sur la cible brute**
- pour une approche conjointe : **`LinearRegression` multi-output sur les deux cibles transformées par `log1p`**

Ainsi, l’objectif initial du projet est atteint : il est possible de prédire de manière satisfaisante la consommation énergétique et les émissions de CO₂ à partir des caractéristiques structurelles et fonctionnelles des bâtiments.
