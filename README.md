# Compte rendu du TP de physique chimie n°3

Quelle relation existe-t-il entre la couleur de la solution et la présence d'espèces chimiques colorantes dissoutes ?

## Objectif

- Explorer les propriété des filtres
- Explorer les propriété des solutions colorées
- Début d'une réflexion sur le moyen d'analyser une solution avec la spectrophotométrie et la mesure de l'absorbance

## Moyens

- 1 jeu de filtres primaire (RVB)

- 1 jeu de filtres secondaires (CMJ)

- 1 source LED de lumière blanche

- 1 spectrophotomètre USB avec fibre optique + cuve + système porte cuve

- 5 cuves de spectrophotométrie + porte cuve

- 1 fiole jaugée de 50mL avec bouchon

- 2 béchers de 50mL

- 3 erlenmeyers de 50mL

- du papier d'essuyage

- 1 verre à pied

- 10 pipette compte-goutte

- 1 pissette d'eau déminéralisé

- 1 flacon de 60mL avec bleu patenté (E133) à la concentration de $1.0*10^-5$ mol/L

- 1 flacon de 60mL avec jaune de tartrazine (E102) à la concentration de $1.0*10^-4$ mol/L

- 1 ordinateur (avec un logiciel de spectromètre et un logiciel d'observation)

- 1 webcam

## Méthodes

Pour ce TP on réalise trois montages :

- schéma du premier montage avec la lumiere, les filtres, la fibre et le spectrophotomètre 
  
  ![a](schema%201.jpg)

- schéma d'une caméra qui observe des schéma à travers un filtre.
  
  ![aa](schema%202.jpg)

- schéma de flacon avec des colorants de différentes concentrations.
  
  ![aa](schéma%203.jpg)

On obtient les données avec le spectrophotomètre relié à l'ordinateur et la caméra. On obtient une photo et un schéma de l'intensité lumineuse en fonction de la longueur d'onde.

Dans ce TP on considère la lumière comme étant une onde.    

###### Protocole pour obtenir de la lumière filtré :

- Aligner la lampe, le système porte filtre et la fibre optique.

- Mettre l'autre côté de la fibre optique dans le spectrophotomètre.

- étalonner le logiciel du spectrophotomètre avec une lumiere blanche 

- Réaliser un spectre avec différents filtres coloré : 
  
  - les trois primaires
  
  - les trois secondaires
  
  - rouge + tous les autres 
  
  - magenta et cyan ensemble
  
  - magenta et jaune ensemble

###### Protocole pour obtenir une image avec un filtre:

- Relier la caméra à l'ordinateur

- Aligner la caméra un filtre et une image

###### Protocole pour obtenir des solutions colorées de concentration 5 fois inférieures à la solution mère

- mettre environ 20 mL de solution mère dans un bécher 

- en prélever 10 mL dans une pipette gradué

- La vider dans une fiole jaugé de 50 mL 

- Compléter la fiole jusqu'au trait de jauge.

- Remplir une cuve de spectrophotométrie avec la solution fille 

###### Protocole pour obtenir une solution fille à partir de deux solutions mères et d'un solvant

- Mettre environ 20 mL de chacune des solutions mères dans un bécher distinct

- Prélever 10 mL de la première solution mère dans une pipette jaugée

- La verser dans la fiole jaugée

- Prélever 10 mL de la seconde solution mère dans une pipette jaugée

- La verser dans la fiole jaugée

- Compléter la fiole jusqu'au trait de jauge 

- mélanger 

- Remplir une cuve de spectrophotométrie avec la solution fille

###### Protocole pour obtenir une photo filtrée numériquement

- soumettre la photo à ce code 

```python
# importation des bibliothèques et modules

import matplotlib.image as mpimg                # ou "import imageio as mpimg"
import matplotlib.pyplot as plt
import numpy as np
import sys
##

# Définition de la fonction filtre_vert

def filtre_vert( image ):
    photo = np.copy(image)                      # copie de l'image à filtrer
    for i in range(photo.shape[0]):             # i indique la ligne sur laquelle se trouve le pixel
        for j in range(photo.shape[1]):         # j indique la colonne sur laquelle se trouve le pixel
            r, v, b = photo[i, j]               # valeurs des composantes rouge, verte et bleue du pixel situé sur la ligne i et la colonne j
            photo[i, j] = (0,v,0)              # conserve la valeur de la composante verte et annule les composantes rouge et bleue
    return photo
##

# Définition de la fonction filtre_rouge

def filtre_rouge( image ):
    photo = np.copy(image)                      # copie de l'image à filtrer
    for i in range(photo.shape[0]):              # i indique la ligne sur laquelle se trouve le pixel
        for j in range(photo.shape[1]):          # j indique la colonne sur laquelle se trouve le pixel
            r, v, b = photo[i, j]               # valeurs des composantes rouge, verte et bleue du pixel situé sur la ligne i et la colonne j
            photo[i, j] = (r,0,0)              # conserve la valeur de la composante rouge et annule les composantes verte et bleue
    return photo
##

# Définition de la fonction filtre_bleu

def filtre_bleu( image ):
    photo = np.copy(image)                      # copie de l'image à filtrer
    for i in range(photo.shape[0]):             # i indique la ligne sur laquelle se trouve le pixel
        for j in range(photo.shape[1]):         # j indique la colonne sur laquelle se trouve le pixel
            r, v, b = photo[i, j]               # valeurs des composantes rouges, vertes et bleues du pixel situé sur la ligne i et la colonne j
            photo[i, j] = (0,0,b)              # conserve la valeur de la composante bleue et annule les composantes rouge et verte
    return photo
##

# programme principal

# Lecture de l'image sous forme d'un tableau de nombres

photoOriginale = mpimg.imread("cercle_chroma_addit.jpg")   # image placée dans le même dossier que le fichier python ou copier le chemin d'accès
#création d'une figure
fig=plt.figure(num="filtrage d'une image", figsize=(16,8))

# Application de la fonction filtre_rouge à la photo choisie

photoFiltreR = filtre_rouge(photoOriginale)

# Application de la fonction filtre_vert à la photo choisie

photoFiltreV = filtre_vert(photoOriginale)

# Application de la fonction filtre_rouge à la photo choisie

photoFiltreB = filtre_bleu(photoOriginale)

# position de l'image originale avec un titre

fig.add_subplot(2, 2, 1) # sous-figures en 2x2 on crée une première sous-figure en (1,1)
plt.imshow(photoOriginale)
plt.title('Photo originale')

# création des photos filtrées avec titre

fig.add_subplot(2, 2, 2) # sous-figures en 2x2 on crée une deuxième sous-figure en (1,2)
plt.imshow(photoFiltreV)
plt.title('Photo avec un filtre vert')
fig.add_subplot(2, 2, 3) # sous-figures en 2x2 on crée une troisième sous-figure en (2,1)
plt.imshow(photoFiltreR)
plt.title('Photo avec un filtre rouge')
fig.add_subplot(2, 2, 4) # sous-figures en 2x2 on crée une quatrième sous-figure en (2,2)
plt.imshow(photoFiltreB)
plt.title('Photo avec un filtre bleu')

# Affichage de la figure

fig.tight_layout() # ajuste les sous-figures les unes par rapport aux autres
plt.savefig("photo_filtree.png")
plt.show()
if sys.platform.startswith('darwin'):
    sys.exit()
```

## Observations

###### Filtrage de la lumière par des filtres colorés :

![Image](spectre%20filtre.png)

| couleur du filtre | longueur d'onde | Intensité |
| ----------------- | --------------- | --------- |
| Rien              | 450.7           | 19.780    |
| Cyan              | 450,7           | 12.308    |
| Bleu              | 450.7           | 8.823     |
| 2 cyan            | 450.7           | 8.182     |
| Bleu + cyan       | 450.7           | 7.106     |
| Rien              | 517             | 17.192    |
| Cyan              | 517             | 12.503    |
| 2 cyan            | 517             | 9.560     |
| Rien              | 650             | 8.181     |
| Rouge             | 650             | 5.812     |
| 2 rouge           | 650             | 4.927     |

###### Filtrage d'une image avec un filtre

<img src="image_carree.jpg" title="" alt="Image" width="546">

###### Filtrage d'une image avec un algorithme

![](photo_filtree.png)

###### Filtrage de la lumière par une solution

![](spectre%20solution.png)

| couleur de la solution | concentration              | longueur d'onde | Absorbance |
| ---------------------- | -------------------------- | --------------- | ---------- |
| eau                    |                            | 420             | 0.000      |
| bleu                   | <p>1.1*10<sup>-4</sup></p> | 420             | 0.000      |
| jaune                  | <p>1.1*10<sup>-4</sup></p> | 420             | 0.988      |
| jaune                  | <p>2.2*10<sup>-5</sup></p> | 420             | 0.518      |
| bleu et jaune          | <p>2.2*10<sup>-5</sup></p> | 420             | 0.358      |
|                        |                            |                 |            |
| eau                    |                            | 629.5           | 0.000      |
| bleu                   | <p>1.1*10<sup>-4</sup></p> | 629.5           | 0.402      |
| bleu                   | <p>2.2*10<sup>-5</sup></p> | 629.5           | 0.049      |
| jaune                  | <p>1.1*10<sup>-4</sup></p> | 629.5           | 0.000      |
| bleu et jaune          | <p>2.2*10<sup>-5</sup></p> | 629.5           | 0.071      |

## Exploitation

###### Filtrage de la lumière avec un filtre

On calcule la transmittance et l'absorbance de chaque filtre pour une longueur d'onde :

$$
T = \frac{I}{I_0} \hspace{1cm}A = -\log_{10} T
$$

Avec T = la transmittance (sans unité)

          I = L'intensité du a lumière transmise
    
         I<sub>0</sub> = l'intensité incidente (celle de la lumiere blanche pour la longueur d'onde)
    
           A = l'absorbance (sans unité)

On obtient :

| couleur du filtre | longueur d'onde | Intensité | Transmittance (%) | Absorbance |
| ----------------- | --------------- | --------- | ----------------- | ---------- |
| Rien              | 450.7           | 19.780    | 100.0             | 0.000      |
| Cyan              | 450.7           | 12.308    | 62.23             | 0.206      |
| Bleu              | 450.7           | 8.823     | 44.62             | 0.353      |
| 2 cyan            | 450.7           | 8.182     | 41.37             | 0.384      |
| Bleu + cyan       | 450.7           | 7.106     | 35.93             | 0.444      |
| Rien              | 517             | 17.192    | 100.0             | 0.000      |
| Cyan              | 517             | 12.503    | 72.72             | 0.136      |
| 2 cyan            | 517             | 9.560     | 55.63             | 0.265      |
| Rien              | 650             | 8.181     | 100.0             | 0.000      |
| Rouge             | 650             | 5.812     | 71.05             | 0.154      |
| 2 rouge           | 650             | 4.927     | 60.22             | 0.219      |

On voit que lorsqu'il y a plusieurs filtre, la transmittance globale est égale au produit des transmittance de chaque filtre :

$$
T_{cyan+cyan} = T_{cyan} \times T_{cyan} = {T_{cyan}}^2
$$

Par exemple, pour les deux filtres cyan on a :

$$
T_{cyan+cyan} = 41.37\%
$$

$$
{T_{cyan}}^2 = 62.23\%^2 = 38.73\%           
$$

Par contre, l’absorbance d'un ensemble de filtre est égale à l'absorbance de chaque filtre.

$$
A_{cyan + cyan} = A_{cyan}+A_{cyan}=2\times A_{cyan}
$$

Par exemple pour le cyan : 

$$
A_{cyan+cyan}= 0.265 \hspace{1 cm} 2\times A_{cyan}=0.136\times2=0.272
$$

la somme est une opération plus simple que le produit donc il est logique de travailler avec l'absorbance. Plus l'épaisseur du filtre est grande et plus l'absorbance est grande. Pour la transmittance, c'est l'inverse.

###### Filtrage d'une image avec un filtre

On voit que sur l'image numérique, le filtre est absolu donc on obtient du noir pour toute les couleurs qui ne contiennent pas la couleur du filtre. Alors que sur l'image filtrée expérimentalement, le filtre laisse passer un peu du reste. Par exemple, sur l'image bleue, on voit que c'est majoritairement gris alors que le découpage devrait être plus franc. On voit aussi que le filtre vert est le meilleur des trois.

Lorsqu’on place un filtre rouge sur le trajet d'un faisceau de lumière blanche, on obtient de la lumière rouge. Or la lumière blanche est composée de lumière rouge, verte et bleue. Donc la lumière bleue et verte ont été absorbée. Le filtrage relève onc de la synthèse soustractive. 

Lorsqu'on parle de la couleur d'un filtre, on parle de la couleur que le filtre laisse passer.

###### Filtrage de la lumière avec une solution

Les cuves de spectrophotométrie font toutes la même largeur. Grace a cela on peut comparer les résultats car la lumiere traverse autant de solutions dans chaque cas. 

La couleur de la solution est la couleur que la solution laisse passer comme dans le cas d'un filtre. Donc lorsqu'on observe la couleur d'une solution rouge à travers un filtre vert cela fait comme si on observe de la lumiere blanche à travers deux filtres, un rouge et un vert. Dans ce cas on voit la solution grise (un noir pas très franc).

Lorsqu'on dilue la solution 5 fois, l'absorbance diminue. En effet la lumière est moins absorbée parce qu'il y a moins de soluté absorbant. Dans le cas de la solution jaune, lorsque la concentration passe de 1.1\*10<sup>-4</sup> mol/L à 2.2*10<sup>-5</sup>, l'absorbance passe de 0,988 à 0,518.

Lorsqu'on mélange les deux solutions il y a une synthèse additive. La solution est donc verte car elle laisse passer le vert. 

Chaque colorant subit une dilution de facteur 5, la solution est donc concentrée pour chaque colorant à 2.2\*10<sup>-5</sup> mol/L.

Lorsqu'on compare différentes solutions, il faut prendre deux longueurs d'onde caractéristiques (comme des valeurs maximales) car il est plus simple de les comparer et de les voir sur un graphique. Ces radiations donnent aussi la couleur de la solution.

Si on cherche à établir un lien de proportionnalité, on peut utiliser les mesures faites sur la solution jaune a la longueur d'onde 420nm : 

| Solution | Concentration              | Absorbance |
| -------- | -------------------------- | ---------- |
| Jaune    | <p>1.1*10<sup>-4</sup></p> | 0.988      |
| Jaune    | <p>2.2*10<sup>-5</sup></p> | 0.518      |

$$
A = C*k \hspace{1cm} k=\frac{1.1*10^-4-2.2*10^-5}{0.988-0518}≈1.87×10^
{−4}
$$

On peut donc constater la présence d'une loi qui relie la concentration et l'absorbance. Cette loi est celle de Beer-Lambert : 

$$
A=k*C
$$

Avec :

- A : L'absorbance (sans unité)

- k : Le coefficient de proportionnalité en L/mol

- C : La concentration en mol/L

## Validation

On constate que le résultat attendu est conforme aux attentes. En effet, on prévoyait le comportement des filtres. On constate que les mesures comportent un certain degré d'incertitudes car la droite obtenue pour la proportionnalité ne croise pas parfaitement tous les points.

Pour l'image que l'on a filmé à travers un filtre, on voit que le filtre numérique est beaucoup plus efficace que le filtre réel qui est imparfait (Il n'est pas centré sur la bonne longueur d'onde)

La loi des Beer-Lambert, que nous avons vérifiée dans la derniere partie de l'exploitation, nous permet de conclure quant à l'existence d'une relation entre la couleur de la solution et sa concentration en colorant.

## Conclusion

Ces travaux ont permis d'explorer les propriétés des filtres, la transmittance et l'absorbance ainsi que les différentes synthèses résultantes de la combinaison de filtres et de lumière.

Ces travaux nous ont montré que l'on pouvait assimiler des solutions colorer a des filtres plus précis car on peut faire varier leur couleur grâce à des colorants.

Ces travaux nous ont permis de commencer une réflexion sur le moyen d'analyser une solution avec une couleur. Maintenant on peut déduire la concentration d'une solution à partir de l'absorbance et vice-versa, si on connait une valeur de référence pour la solution.
