# Généralités sur le langage R

## Les Variables

### D'un point de vue global 

L’étude des variables est l’objet principal des statistiques descriptives. Il existe plusieurs type de variables que l’on décrit dans le tableau suivant :

<table>
  <tr>
   <td colspan="4" >Variables
   </td>
  </tr>
  <tr>
   <td colspan="2" >Qualitatives
   </td>
   <td colspan="2" >Quantitatives
   </td>
  </tr>
  <tr>
   <td>Nominales
   </td>
   <td>Ordinales
   </td>
   <td>Continues
   </td>
   <td>Discrètes
   </td>
  </tr>
  <tr>
   <td>Une variable qui décrit une caractéristiques qu’il n’est pas possible de trier du plus petit au plus grand.
<p>
Exemple : les couleurs, noms de ville...
   </td>
   <td>Une variables qui décrit une caractéristique qui ne prend qu’un nombre limité de modalités que l’on peut classer par ordre croissant.
<p>
Exemple : une review individuelle sur une produit amazon, une note scolaire numérotée de A à E
   </td>
   <td>Une variable qui décrit une caractéristique mesurée par un nombre réel (pour résumer des nombres à virgule)
<p>
Exemple : Un salaire, une mesure de taux d’oxygène dans l’air, un prix
   </td>
   <td>Une variable qui décrit une caractéristique mesurée par un nombre entier
<p>
Exemple : un âge mesuré en années, un nombre de visites sur un site web
   </td>
  </tr>
</table>

### Les tenseurs

Dans les langages de programmation et notamment pour l'analyse statistique, la manipulation des vecteurs et matrices est fréquente. 
Reprenons leur définition : 

Un tenseur est une généralisation de la notion de vecteur. C'est un objet de dimension *n* contenant des nombres. Pour les petites dimensions :: 0, 1 et 2, on a donné un nom spécifique à ces objets.

Dimension 0 : Scalaire.

```
# Voici un nombre scalaire

2
```

Dimension 1 : Vecteur.

```
# Voici un vecteur

[1,
 2,
 3]
```

Dimension 2 : Matrice.
```
# Voici une matrice

[[1, 2, 3,
  4, 5, 6,
  7, 8, 9]]

```

Au delà de deux dimensions : *tenseur*.

## Les packages (library)
Utiliser des librairies en R

### Qu’est ce qu’une librairie ?

L'utilisation des librairies est possible en R, comme en Python. Par définition une librairie est un module dans lequel il y a plusieurs classes que vous pouvez utiliser quand vous en avez envie/besoin.

Il existe des milliers de libraires sous R, les plus connues sont *data.table* ...


#### Comment importer une librairie ?

```
#Installer une librairie depuis le CRAN
install.packages("devtools")

#Installer une librairie depuis github
library("devtools")
install_github("dgrtwo/broom")
```

C’est tout aussi simple que cela pour importer une librairie. Vous pouvez également le faire directement via votre IDE.

#### Comment utiliser une librairie ?

L'import d'une librairie ne se fait qu'une seule, cependant vous devrez charger votre libraire à chaque fois. Pour cela : 

```
library(dplyr)
```

Une dernière chose à comprendre est qu’il y a plein de librairies différentes et que celles-ci ne fonctionnent pas de la même manière. Il faudra donc se référer à la documentation de la librairie en question pour avoir plus d’informations. 


## Importer / Exporter des données

Pour importer vos données, plusieurs options selon dans quoi est stocké votre dataset. Nous ferons simple dans ce cours, les fichiers seront souvent des CSV :

```
# Le fichier data.txt est lu est stocké dans un nouveau objet R nommé Database 
Database <- read.table("data.txt", header = TRUE) 

library(data.table)
Database <- fread("data.txt")


# Fichier de type CSV depuis un serveur web (ce fichier contient des stats de google webmaster tools pour edutechwiki ...) 
Database_webmaster <- read.csv("http://tecfa.unige.ch/guides/R/data/edutechwiki-fr-gw-oct-6-2014.csv", header = TRUE, sep= ",") 

```

Pour exporter vos données et les enregistrer sur votre ordinateur par exemple : 

```
# Le fichier est enregistré sous nomFichier.csv et le numéro des lignes n’est pas conservé 
 write.csv(nomFichier,file="nomFichier.csv",row.names = FALSE)
```

## Les graphiques

### Les nuages de point

Pour tracer un graphique, un nuage de points où y = f(x) 
```
plot(x,y) 
```

Utilisons un dataset simple : le dataset iris, qui contient les largeurs et longueurs des sépales et pétales de plusieurs fleurs.

```
# La fonction plot() s'utilise d ela manière suivante
plot(iris$Petal.Length, iris$Petal.Width)
```

![](https://drive.google.com/uc?export=view&id=1ECj8a3VoNYOGd9jlMqiFlnSpaUqTm8eY)

Différentes options sont utilisables pour la mise en forme
```
# main pour le titre
plot(iris$Petal.Length, iris$Petal.Width, main="Edgar Anderson's Iris Data")

# col pour changer la couleur 
plot(iris$Petal.Length, iris$Petal.Width,col="red")

# type pour changer le type de point ('l' pour ligne, 'p' pour point, 'b' point-ligne, ...)
plot(iris$Petal.Length, iris$Petal.Width,type="b")

# xlab, ylab pour renommer les axes
plot(iris$Petal.Length, iris$Petal.Width,xlab = "titre de l'axe x",ylab = "axe y") 

# xlim et ylim pour paramétrer les limites
plot(iris$Petal.Length, iris$Petal.Width,xlim=c(0,10),ylim=c(2,5))
```

### Les diagrammes en barre

La fonction barplot() est la plus commune pour les diagrammes en barre, il est possible de les customiser pour obtenir les visuels plus poussés comme des barplot empilé, des barres horizontales ou verticales, ...

```
x = c(1,2,5,2) 
barplot(x)

barplot(table(iris$Species))
```

![](https://drive.google.com/uc?export=view&id=1q6iPmHgLTMRariPRxhatoWjjc3speJ0B)


### Les histogrammes

Tracer un histogramme avec R, c'est à dire visualiser la répartition d'un effectif se fait avec la commande hist().

```
# soit x une liste de données simulées ici 
x <- rnorm(10000,20,3) # A remplacer 
# Tracer l'histogramme 
hist(x) 
``` 

![](https://drive.google.com/uc?export=view&id=1vcpRzaA9D5OgnpaISfum08K4RWnMp-z3)


### Pour aller plus loin

Les packages de visualisations graphiques sont nombreux, les plus connus restent plotly et ggplot2 qui permettent une totale maitrise des graphiques mais aussi un rendu visuel plus sympathique voir dynamique. 



