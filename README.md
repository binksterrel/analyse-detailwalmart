# Analyse Walmart : Les Promotions Augmentent-elles les Ventes ?

Ce dépôt contient l'analyse complète d'un jeu de données de ventes hebdomadaires de Walmart, fusionné à partir de trois fichiers (`sales`, `stores`, `features`).

L'objectif était de déterminer si les promotions (MarkDown) avaient un impact réel sur les ventes. L'analyse prouve via un **test T que les promotions augmentent les ventes de manière statistiquement significative (p < 0.001)**.

La découverte clé réside dans la nuance : si le *fait* d'activer une promotion est efficace, le *montant* de cette promotion a une **influence positive mais très faible (Corrélation = 0.065)** sur le volume total des ventes.

**Compétences démontrées :** `Python`, `Pandas`, `Seaborn`, `Scipy`, `Analyse de Données`, `Nettoyage de Données`, `EDA (Exploratory Data Analysis)`, `Data Visualization`, `Test Statistique (Test T)`, `Feature Engineering`

---

## 🎯 Problématique

L'objectif initial de ce projet était de répondre à une question business simple et directe : **"Est-ce que les promotions (MarkDown 1 à 5) augmentent significativement les ventes hebdomadaires ?"**

À première vue, la différence des moyennes semblait faible (16 177 $avec promo contre 15 872 $sans). L'enjeu était donc de déterminer si cette différence était statistiquement réelle ou si elle était simplement due au hasard.

---

## 🕵️ Méthodologie et Découvertes Clés

Mon analyse s'est déroulée en trois étapes critiques dans un Jupyter Notebook.

### 1. Préparation et Feature Engineering
Les données brutes étaient réparties sur trois fichiers et les promotions étaient difficiles à analyser car elles contenaient de nombreux `NaN`. Une étape de préparation a été nécessaire pour les rendre exploitables :

* **Fusion :** Les trois fichiers (`sales`, `stores`, `features`) ont été fusionnés en un seul DataFrame principal via Pandas.
* **Nettoyage :** Les `NaN` des colonnes `MarkDown` ont été remplacés par `0`, partant de l'hypothèse qu'un `NaN` signifiait une absence de promotion.
* **Feature Engineering :** Deux variables cruciales ont été créées pour l'analyse :
    1.  `Total_MarkDown` : La somme des 5 types de promotions.
    2.  `Promo_Active` : Une variable booléenne (Vrai/Faux) indiquant si `Total_MarkDown` était supérieur à 0. C'est la variable clé qui a permis l'analyse.

### 2. Analyse Principale (Test T)
L'hypothèse principale a été testée en comparant les ventes des deux groupes (`Promo_Active = True` vs. `Promo_Active = False`) à l'aide d'un test T indépendant de `scipy.stats`.

* **Hypothèse Nulle (H₀) :** Les promotions n'ont **aucun** effet (les moyennes des deux groupes sont statistiquement identiques).
* **Résultat :** Le test a retourné une **p-value de 3.35e-05** (soit 0.0000335).
* **Conclusion :** Cette p-value étant très inférieure au seuil de 0.05, nous rejetons l'hypothèse nulle. La différence est **hautement significative** et n'est pas due au hasard.

### 3. Découverte par Nuance (Analyse de Corrélation)
La première question étant répondue ("Oui, les promos fonctionnent"), une seconde question a été posée : "Est-ce que dépenser *plus* en promotion entraîne *plus* de ventes ?"

* Une analyse de corrélation a été menée entre `Weekly_Sales` (ventes) et `Total_MarkDown` (montant).
* **Résultat :** La corrélation est de **0.065**.
* **Conclusion :** C'est une corrélation positive mais **extrêmement faible**.

---

## 🏁 Conclusion

Ce projet est une démonstration de l'importance de choisir le bon outil statistique pour répondre à la bonne question.

J'ai prouvé que les promotions sont un levier efficace : le simple **fait de les activer** a un impact significatif et prouvé sur l'augmentation des ventes (confirmé par le **Test T**).

Cependant, l'analyse de corrélation apporte une nuance cruciale pour le business : le **montant** dépensé pour ces promotions n'a qu'une très faible influence linéaire sur le volume des ventes. L'efficacité réside dans "l'acte" de promouvoir, pas nécessairement dans "l'intensité" de la promotion.

Ce projet démontre ma capacité à ne pas m'arrêter à une simple moyenne, à utiliser les outils statistiques pour valider une hypothèse, et à affiner l'analyse pour trouver une nuance business importante.

---

## 🚀 Comment l'exécuter

Ce projet est un Jupyter Notebook (`.ipynb`).

**Fichiers dans ce dépôt :**
* `analyseretail.ipynb` : Le notebook contenant l'analyse complète (code et markdown).
* `sales data-set.csv` : Données brutes des ventes.
* `stores data-set.csv` : Données brutes des magasins.
* `Features data set.csv` : Données brutes (météo, promotions, etc.).
* `dashboard_ventes_promo.png` : L'image dashboard résumant les deux visualisations clés.

**Exécution :**
Pour exécuter l'analyse, ouvrez `analyseretail.ipynb` dans un environnement Jupyter (comme Jupyter Lab, VS Code, ou Google Colab) et assurez-vous que les trois fichiers CSV sont dans le même répertoire.
