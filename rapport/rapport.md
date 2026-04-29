# Rapport final — Cartographie intelligente du risque et du rendement des actions du CAC 40

## 1. Introduction

La finance produit une grande quantité de données : prix des actions, rendements, volatilités, corrélations avec les indices boursiers, etc. Pour un investisseur débutant, il peut être difficile d’identifier rapidement les actions les plus stables, les plus risquées ou les plus proches entre elles.

L’objectif de ce projet est d’utiliser des méthodes simples de Data Science afin d’analyser un ensemble d’actions françaises. Le but n’est pas de prédire le futur, mais de construire une lecture claire du comportement passé des actions à partir de plusieurs indicateurs financiers.

Dans ce projet, nous utilisons notamment l’Analyse en Composantes Principales (ACP), le clustering K-Means et la Classification Ascendante Hiérarchique (CAH). Ces méthodes permettent de représenter les actions dans un espace réduit et de les regrouper selon leur profil de risque et de rendement.

## 2. Problématique

La problématique principale du projet est la suivante :

**Peut-on regrouper automatiquement des actions du CAC 40 selon leur profil de risque et de rendement, à partir de données historiques publiques, sans utiliser de méthodes avancées comme le deep learning ?**

Pour répondre à cette question, nous cherchons à comparer les actions à partir de plusieurs indicateurs simples :

- le rendement moyen annuel ;
- la volatilité annuelle ;
- le rendement minimum journalier ;
- le rendement maximum journalier ;
- la corrélation avec l’indice CAC 40.

Ces indicateurs permettent de décrire à la fois la performance moyenne, le risque et le lien entre chaque action et le marché français.

## 3. Données utilisées

Les données utilisées dans ce projet proviennent de Yahoo Finance grâce à la bibliothèque Python `yfinance`.

Nous avons étudié 15 actions françaises :

- TTE.PA ;
- SU.PA ;
- MC.PA ;
- AI.PA ;
- SAN.PA ;
- AIR.PA ;
- SAF.PA ;
- BNP.PA ;
- OR.PA ;
- CS.PA ;
- DG.PA ;
- EL.PA ;
- RMS.PA ;
- KER.PA ;
- ACA.PA.

L’indice CAC 40, noté `^FCHI`, est utilisé comme référence du marché français. La période étudiée est comprise entre **2020-01-01** et **2025-12-31**.

Les prix des actions sont utilisés pour calculer les rendements journaliers, puis plusieurs indicateurs financiers sont construits à partir de ces rendements.

## 4. Méthodes utilisées

### 4.1 Rendement journalier

Le rendement journalier mesure la variation relative du prix d’une action entre deux jours consécutifs.

Il est calculé de la manière suivante :

```text
rendement journalier = (prix du jour / prix du jour précédent) - 1
```

Cet indicateur permet d’observer les variations quotidiennes d’une action.

### 4.2 Rendement moyen annualisé

Le rendement moyen annualisé donne une estimation de la performance moyenne d’une action sur une année. Il est obtenu à partir du rendement journalier moyen, multiplié par le nombre approximatif de jours de bourse dans une année.

Dans ce projet, on utilise généralement 252 jours de bourse par an.

### 4.3 Volatilité annualisée

La volatilité mesure le niveau de variation des rendements d’une action. Une volatilité élevée signifie que le prix de l’action varie beaucoup, donc que le risque est plus important.

La volatilité annualisée est obtenue à partir de l’écart-type des rendements journaliers.

### 4.4 Rendement minimum et maximum journalier

Le rendement minimum journalier correspond à la plus forte baisse observée sur une journée. Le rendement maximum journalier correspond à la plus forte hausse observée sur une journée.

Ces deux indicateurs permettent de repérer les actions qui ont connu des variations extrêmes.

### 4.5 Corrélation avec le CAC 40

La corrélation avec le CAC 40 mesure le lien entre les variations d’une action et celles de l’indice CAC 40.

Une corrélation élevée signifie que l’action évolue souvent dans le même sens que le marché français. Une corrélation plus faible indique un comportement plus différent du marché.

### 4.6 ACP

L’ACP, ou Analyse en Composantes Principales, permet de réduire le nombre de variables tout en gardant le maximum d’information possible.

Dans ce projet, les 5 indicateurs financiers sont réduits en 2 axes principaux. Cela permet de représenter les actions dans un plan à deux dimensions et de visualiser les similarités entre elles.

Avant d’appliquer l’ACP, les données sont normalisées avec `StandardScaler`, car les variables n’ont pas toutes la même échelle.

### 4.7 K-Means

Le K-Means est une méthode de clustering qui permet de regrouper automatiquement les actions en plusieurs groupes.

Dans ce projet, nous avons choisi **3 clusters** pour obtenir une interprétation simple :

- un groupe avec un bon compromis rendement/risque ;
- un groupe plus risqué ;
- un groupe moins performant ou particulier.

### 4.8 CAH

La CAH, ou Classification Ascendante Hiérarchique, est une autre méthode de regroupement. Elle permet de construire un dendrogramme pour observer progressivement comment les actions se regroupent selon leur proximité.

Plus deux actions se regroupent à une faible distance dans le dendrogramme, plus elles sont similaires selon les indicateurs étudiés.

## 5. Analyse descriptive

L’analyse descriptive permet d’avoir une première vision du comportement des actions avant d’appliquer l’ACP et le clustering.

Les indicateurs calculés pour chaque action sont les suivants :

| Action | Rendement moyen annuel | Volatilité annuelle | Rendement min journalier | Rendement max journalier | Corrélation CAC 40 |
|---|---:|---:|---:|---:|---:|
| TTE.PA | 0.129379 | 0.304387 | -0.166083 | 0.150742 | 0.660793 |
| SU.PA | 0.218439 | 0.299061 | -0.140180 | 0.120130 | 0.768534 |
| MC.PA | 0.131210 | 0.303992 | -0.086779 | 0.128119 | 0.779378 |
| AI.PA | 0.110667 | 0.208582 | -0.111603 | 0.082596 | 0.726724 |
| SAN.PA | 0.052344 | 0.233065 | -0.189329 | 0.084405 | 0.402857 |
| AIR.PA | 0.155409 | 0.396552 | -0.221685 | 0.204633 | 0.730943 |
| SAF.PA | 0.205461 | 0.379744 | -0.228737 | 0.209327 | 0.752658 |
| BNP.PA | 0.184088 | 0.343259 | -0.135203 | 0.179807 | 0.769486 |
| OR.PA | 0.098581 | 0.247306 | -0.075803 | 0.084374 | 0.673341 |
| CS.PA | 0.170059 | 0.268402 | -0.152184 | 0.175640 | 0.788181 |
| DG.PA | 0.106035 | 0.292405 | -0.170744 | 0.188469 | 0.792284 |
| EL.PA | 0.165868 | 0.267639 | -0.103898 | 0.129790 | 0.688707 |
| RMS.PA | 0.235355 | 0.278957 | -0.065414 | 0.091043 | 0.689189 |
| KER.PA | -0.027548 | 0.350136 | -0.123147 | 0.117627 | 0.685656 |
| ACA.PA | 0.158577 | 0.307194 | -0.168638 | 0.136669 | 0.757718 |

On remarque que certaines actions ont un rendement moyen annuel élevé, comme RMS.PA, SU.PA ou SAF.PA. D’autres actions, comme KER.PA, ont un rendement moyen annuel négatif sur la période étudiée.

La volatilité varie aussi selon les actions. Par exemple, AIR.PA, SAF.PA, BNP.PA et KER.PA présentent des volatilités plus élevées. Cela signifie que ces actions ont connu des variations plus importantes.

SAN.PA se distingue par une corrélation plus faible avec le CAC 40. Cela montre que cette action a un comportement plus différent de l’indice de marché par rapport aux autres actions étudiées.

Les graphiques des prix normalisés, des rendements moyens, des volatilités et de la matrice de corrélation permettent de compléter cette analyse visuelle.

## 6. ACP

L’ACP a été appliquée sur les 5 indicateurs financiers après normalisation.

Les deux premiers axes de l’ACP expliquent une grande partie de l’information :

| Axe | Part de variance expliquée |
|---|---:|
| Axe 1 | 0.518253 |
| Axe 2 | 0.266822 |
| Total | 0.785075 |

Les deux premiers axes expliquent donc environ **78,5 %** de l’information totale. Cela signifie que la projection en deux dimensions conserve une grande partie de l’information initiale.

Les contributions des variables aux axes sont les suivantes :

| Variable | Axe 1 | Axe 2 |
|---|---:|---:|
| rendement_moyen_annuel | 0.271357 | 0.573199 |
| volatilite_annuelle | 0.522506 | -0.167942 |
| rendement_min_journalier | -0.408099 | 0.553981 |
| rendement_max_journalier | 0.591927 | -0.090087 |
| correlation_CAC40 | 0.369365 | 0.572911 |

L’axe 1 est fortement influencé par la volatilité annuelle et le rendement maximum journalier. Il permet donc de séparer les actions selon leur niveau de variation et leur potentiel de hausse journalière.

L’axe 2 est surtout influencé par le rendement moyen annuel, le rendement minimum journalier et la corrélation avec le CAC 40. Il apporte donc une information complémentaire sur la performance moyenne et le lien avec le marché.

Sur le graphique ACP, les actions proches ont des comportements financiers similaires. Par exemple, AI.PA et OR.PA sont proches, tout comme MC.PA et EL.PA. SAN.PA apparaît plus isolée, ce qui indique un profil différent.

## 7. Clustering

### 7.1 Résultats du K-Means

Le K-Means a été appliqué avec 3 clusters. Les groupes obtenus sont les suivants :

| Cluster | Actions |
|---|---|
| Cluster 0 | AI.PA, MC.PA, EL.PA, OR.PA, RMS.PA |
| Cluster 1 | AIR.PA, SU.PA, TTE.PA, DG.PA, BNP.PA, SAF.PA, CS.PA, ACA.PA, KER.PA |
| Cluster 2 | SAN.PA |

Le profil moyen de chaque cluster est le suivant :

| Cluster | Rendement moyen annuel | Volatilité annuelle | Rendement min journalier | Rendement max journalier | Corrélation CAC 40 |
|---|---:|---:|---:|---:|---:|
| 0 | 0.148336 | 0.261295 | -0.088699 | 0.103184 | 0.711468 |
| 1 | 0.144433 | 0.326793 | -0.167400 | 0.164783 | 0.745139 |
| 2 | 0.052344 | 0.233065 | -0.189329 | 0.084405 | 0.402857 |

Le cluster 0 présente le meilleur rendement moyen annuel, avec une volatilité modérée. Il représente donc le meilleur compromis entre rendement et risque.

Le cluster 1 possède une volatilité annuelle plus élevée. Son rendement moyen est proche de celui du cluster 0, mais le risque est plus important.

Le cluster 2 contient uniquement SAN.PA. Il présente le rendement moyen annuel le plus faible et une corrélation plus faible avec le CAC 40.

### 7.2 Résultats de la CAH

La CAH a été utilisée pour construire un dendrogramme. Ce graphique montre les distances entre les actions et permet d’observer quels titres sont les plus proches.

On observe plusieurs rapprochements intéressants :

- AIR.PA et SAF.PA sont très proches ;
- AI.PA et OR.PA sont également proches ;
- MC.PA et EL.PA forment un groupe cohérent ;
- SU.PA et ACA.PA sont proches, puis se regroupent avec BNP.PA et TTE.PA.

Si on coupe le dendrogramme autour d’une distance proche de 5, on peut obtenir environ 3 groupes principaux :

| Groupe CAH | Actions |
|---|---|
| Groupe 1 | AIR.PA, SAF.PA, CS.PA, DG.PA, TTE.PA, BNP.PA, SU.PA, ACA.PA |
| Groupe 2 | SAN.PA |
| Groupe 3 | KER.PA, AI.PA, OR.PA, RMS.PA, MC.PA, EL.PA |

La CAH confirme plusieurs éléments observés avec K-Means. En particulier, SAN.PA apparaît comme une action différente des autres. Les actions du luxe et de la consommation comme MC.PA, EL.PA, RMS.PA, OR.PA et AI.PA semblent aussi avoir des profils proches.

## 8. Interprétation des résultats

### Cluster 0 : meilleur compromis rendement / risque

Le cluster 0 regroupe les actions suivantes :

**AI.PA, MC.PA, EL.PA, OR.PA et RMS.PA.**

Ce groupe présente le rendement moyen annuel le plus élevé, avec une volatilité annuelle modérée. Il peut donc être interprété comme le groupe le plus équilibré.

Les entreprises de ce groupe ont un bon niveau de performance tout en gardant un risque raisonnable par rapport au cluster 1.

**Interprétation :** ce cluster représente le meilleur compromis entre rendement et risque.

### Cluster 1 : groupe le plus risqué

Le cluster 1 regroupe les actions suivantes :

**AIR.PA, SU.PA, TTE.PA, DG.PA, BNP.PA, SAF.PA, CS.PA, ACA.PA et KER.PA.**

Ce groupe a une volatilité annuelle moyenne plus élevée que les autres clusters. Cela signifie que les actions de ce groupe ont des variations plus fortes.

Le rendement moyen annuel reste élevé, mais il est accompagné d’un niveau de risque plus important. Le rendement maximum journalier est aussi plus élevé dans ce cluster, ce qui montre que ces actions peuvent connaître de fortes hausses, mais aussi de fortes baisses.

**Interprétation :** ce cluster correspond au groupe le plus risqué.

### Cluster 2 : groupe moins performant et particulier

Le cluster 2 contient uniquement :

**SAN.PA.**

Ce groupe a le rendement moyen annuel le plus faible. Il possède aussi une corrélation plus faible avec le CAC 40, ce qui montre que son comportement est plus différent du marché.

Même si sa volatilité annuelle n’est pas la plus élevée, son rendement moyen reste faible. Comme ce cluster contient une seule action, il faut interpréter ce résultat avec prudence.

**Interprétation :** ce cluster est le moins performant sur la période étudiée et correspond à une action particulière.

### Comparaison entre K-Means et CAH

Les résultats de K-Means et de la CAH sont globalement cohérents. Les deux méthodes montrent que SAN.PA se distingue des autres actions.

La CAH permet aussi de mieux visualiser les proximités entre certaines actions. Par exemple, AIR.PA et SAF.PA sont très proches, tout comme AI.PA et OR.PA.

Cependant, certains regroupements peuvent varier selon la méthode utilisée. Cela est normal, car K-Means et CAH n’utilisent pas exactement la même logique de classification.

## 9. Limites

Ce projet présente plusieurs limites.

Premièrement, il analyse uniquement le passé. Les résultats obtenus ne permettent pas de prévoir avec certitude les performances futures des actions.

Deuxièmement, les résultats dépendent de la période choisie. Une autre période d’analyse pourrait donner des rendements, volatilités et clusters différents.

Troisièmement, le nombre de variables utilisées est limité. Dans ce projet, nous avons utilisé des indicateurs simples comme le rendement, la volatilité et la corrélation. Pour une analyse plus complète, on pourrait ajouter d’autres informations, comme les volumes échangés, les secteurs d’activité, les dividendes ou des indicateurs macroéconomiques.

Quatrièmement, le choix du nombre de clusters influence les résultats. Ici, nous avons choisi 3 clusters pour simplifier l’interprétation, mais un autre nombre de groupes pourrait être testé.

Enfin, ce projet est pédagogique. Il ne constitue pas un conseil financier. Les décisions d’investissement doivent prendre en compte beaucoup d’autres éléments.

## 10. Conclusion

Ce projet montre qu’il est possible d’utiliser des méthodes classiques de Data Science pour analyser et regrouper des actions selon leur profil de risque et de rendement.

L’analyse descriptive permet d’observer les différences entre les actions à partir d’indicateurs simples. L’ACP permet ensuite de réduire les données en deux axes principaux tout en conservant environ 78,5 % de l’information. Cette projection facilite la visualisation des similarités entre les actions.

Le K-Means permet de construire trois groupes d’actions. Le cluster 0 apparaît comme le groupe le plus intéressant, car il combine le meilleur rendement moyen annuel avec une volatilité modérée. Le cluster 1 correspond au groupe le plus risqué, avec une volatilité plus élevée. Le cluster 2, composé uniquement de SAN.PA, est le moins performant sur la période étudiée.

La CAH confirme plusieurs résultats du K-Means, notamment le caractère particulier de SAN.PA et la proximité entre certaines actions comme AIR.PA et SAF.PA, ou encore AI.PA et OR.PA.

En conclusion, ce projet permet de construire une cartographie simple, claire et interprétable du risque et du rendement des actions étudiées. Il montre aussi que des méthodes accessibles comme l’ACP, K-Means et la CAH peuvent être utiles pour mieux comprendre le comportement des actions, même sans utiliser de modèles avancés.
