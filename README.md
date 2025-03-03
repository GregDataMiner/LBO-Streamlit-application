# 📌 Business Acquisition Example LBO  
**Modélisation d'un rachat d'entreprise via un LBO (Leverage Buyout) avec Streamlit**  

## 🔗 *[Accéder à l’application en ligne](https://lbo-application.streamlit.app/)*

---

## 📖 Présentation du projet  

Ce projet est une **application web interactive** développée avec **Streamlit**, permettant de modéliser un **LBO (Leverage Buyout)**.  
L'objectif est d'analyser **les effets du financement par dette** sur la rentabilité d'une acquisition d'entreprise en utilisant un modèle dynamique et interactif.

### 🎯 **Fonctionnalités principales**  
✅ **Définition des paramètres d’acquisition** :  
   - Saisie de l'EBITDA, du multiple d’entrée, du pourcentage de financement en equity.  
✅ **Calcul de la structure du capital** :  
   - Décomposition du financement entre equity et dette.  
✅ **Projection des résultats financiers** :  
   - Évolution de l’EBITDA, paiement des intérêts, génération de revenus nets.  
✅ **Tableau d’amortissement de la dette** :  
   - Visualisation des remboursements et de l’évolution du solde de la dette.  
✅ **Analyse de sensibilité** :  
   - Impact des variations du taux d’intérêt, de la croissance et de l’apport en equity sur la rentabilité finale.  
✅ **Visualisation des données** :  
   - Graphiques interactifs générés avec **Plotly**.  

---

## 📂 Structure du projet  

L’application est organisée en plusieurs fichiers :  

```
📁 lbo-streamlit-application
│── 📄 app.py                  # Script principal Streamlit  
│── 📄 Functions.py             # Fonctions de calcul du LBO  
│── 📄 requirements.txt         # Dépendances du projet  
│── 📄 README.md                # Présentation du projet  
```

### 🔍 **Explication des fichiers**  
#### **1️⃣ `app.py` (Application principale)**
Ce fichier contient le **code de l’interface Streamlit**, divisée en plusieurs sections :
- **Entrée des paramètres financiers** (EBITDA, multiple d’entrée, equity, taux d’intérêt, durée du prêt, croissance annuelle).
- **Affichage de la structure du capital** (dette vs equity).
- **Génération du tableau d’amortissement** avec visualisation interactive.
- **Calcul des indicateurs de sortie** (Enterprise Value, MOIC, IRR).
- **Analyse de sensibilité** pour tester différentes hypothèses.

#### **2️⃣ `Functions.py` (Calculs et algorithmes)**
Ce fichier regroupe toutes les fonctions de calcul utilisées par `app.py` :
- `initial_values()` : calcule le prix d'acquisition, la répartition entre dette et equity.
- `amortization_table()` : génère un tableau d’amortissement de la dette sur la durée du prêt.
- `projections()` : **simule l’évolution des flux financiers** (voir détails ci-dessous).
- `capital_structure()` : analyse la part de dette et d’equity dans la capitalisation.
- `exit_indicators()` : calcule la rentabilité finale du LBO (MOIC, IRR).

---

## 📈 **Projection des résultats financiers**  

L’un des éléments les plus importants de l’analyse LBO est la **projection des résultats financiers** sur plusieurs années afin d’anticiper l’évolution des flux de trésorerie, du remboursement de la dette et de la rentabilité.

L'application projette les résultats financiers en utilisant les hypothèses définies par l'utilisateur :
- **Évolution de l’EBITDA sur 5 ans** (taux de croissance annuel).
- **Calcul des intérêts de la dette** à partir du taux d’intérêt et du solde restant.
- **Calcul du résultat net** (Net Income) après paiement des intérêts.

### 🔢 **Détails des calculs**
Chaque année, l'EBITDA évolue en fonction du **taux de croissance annuel (YoY Growth)** :
```python
ebitda = appreciation(growth/100, year) * ltm_ebitda
```
où :
- `growth` est le taux de croissance annuel en pourcentage.
- `ltm_ebitda` est l’EBITDA initial défini par l’utilisateur.
- `appreciation()` est une fonction qui applique la croissance annuelle :
```python
def appreciation(interest_rate, year):
    return (1 + interest_rate) ** year
```

Le **paiement des intérêts** est basé sur le solde de la dette :
```python
interest = df.loc[year, 'Interest'] if year in df.index else 0
```
Puis, le **résultat net (Net Income)** est calculé :
```python
net_income = ebitda - interest
```

L'affichage dans Streamlit se fait sous forme de **tableau dynamique** avec :
- **EBITDA projeté** 📈
- **Paiement des intérêts** 💰
- **Résultat net** 🏦

Exemple de présentation :
```python
st.subheader(f"Year {year}")
st.write(f'${ebitda:,.0f}')
st.write(f'${interest:,.0f}')
st.markdown("---")
st.write(f'${net_income:,.0f}')
```

---

## 📊 Aperçu de l’application  

L’application permet de visualiser l’impact des décisions financières sur un **LBO** à travers :  
📑 **Des tableaux dynamiques** pour comprendre l'évolution des flux financiers.  
📊 **Des graphiques interactifs** pour visualiser les paiements de la dette et la structure du capital.  
🎯 **Une interface claire et intuitive** pour tester différentes hypothèses et affiner l’analyse financière.  

---

## 📧 Contact & Contribution  

🚀 Ce projet est idéal pour les **analystes financiers, investisseurs et étudiants en finance** souhaitant comprendre le fonctionnement d’un LBO.  
Si vous souhaitez **contribuer** ou poser une question, n’hésitez pas à ouvrir une **issue** ou à proposer un **pull request**.  

Si ce projet vous aide, pensez à **starrer ⭐ sur GitHub** pour le soutenir ! 😃  
