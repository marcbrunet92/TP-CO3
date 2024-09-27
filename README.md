# __Compte rendu du TP de physique chimie n°3__

Quelle relation exitste-t-il entre la couleur de la solution et la presence d'éspèces chimiques colorantes dissoutes ?

## __Objectif__

- Explorer les propriété des filtres
- Explorer les propriété des solutions colorées
- Début d'une réfléxion sur le moyen d'analyser une solution avec la spectrophotométrie et la mesure de l'absorbance

## __Moyens__

- 1 jeu de filtres primaire (RVB)

- 1 jeu de filtres secondaires (CMJ)

- 1 source LED de lumière blanche

- 1 spectrophotomètre USB avec fibre optique + cuve + syseme porte cuve

- 5 cuves de spectrophotométrie + porte cuve

- 1 fiole jaugée de 50mL avec bouchon

- 2 bechers de 50mL

- 3 erlenmeyers de 50mL

- du papier d'essuyage

- 1 verre à pied

- 10 pipette compte-goutte

- 1 pisette d'eau déminéralisé

- 1 flacon de 60mL avec bleu patenté (E133) à la concentration de $1.0*10^-5$ mol/L

- 1 flacon de 60mL avec jaune de tartrazine (E102) à la concentration de $1.0*10^-4$ mol/L

- 1 ordinateur (avec un logiciel de spectromètre et un logiciel d'observation)

- 1 webcam

## __Méthodes__

Pour ce tp on realise trois montages :

- schema du pemier montage avec la lumiere, les filtres, la fibre et le spectrophotomètre 
  
  ![a](schema%201.jpg)

- schema d'une camera qui observe des schema à travers un filtre.
  
  ![aa](schema%202.jpg)

- schema de flacon avec des colorants de differentes concentrations.
  
  ![aa](schéma%203.jpg)

On obtient les données avec le spectrophotomètre relié a l'ordinateur et la caméra. On obtient une photo et un schéma de l'intensité lumineuse en fontion de la longueur d'onde.

Dans ce TP on considère la lumière comme étant une onde.    

__Protocole pour obtenir de la lumière filtré :__

- Aligner la lampe, le systeme porte filtre et la fibre optique.

- Mettre l'autre côté de la fibre optique dans le spectrophotomètre.

- étalonner le logiciel du spectrophtomètre avec une lumiere blanche 

- Realiser un spectre avec differents filtres coloré : 
  
  - les trois primaires
  
  - les trois secondaires
  
  - rouge + tous les autres 
  
  - magenta et cyan ensemble
  
  - magenta et jaune ensemble

__Protocole pour obtenir une image avec un filtre:__

- Relier la caméra à l'ordinateur

- Aligner la camera un filtre et une image

__Protocole pour obtenir des solutions colorées de concentration 5 fois inferieures à la solution mère__

- mettre environ 20 mL de solution mère dans un becher 

- en prélever 10 mL dans une pipette gradué

- La vider dans une fiole jaugé de 50 mL 

- Compléter la fiole jusqu'au trait de jauge.

- Remplir une cuve de spectrophotométrie avec la solution fille 

__Protocole pour obtenir une solution fille a partir de deux solutions mères et d'un solvant__

- Mettre environ 20 mL de chacune des solutions mères dans un becher distinct

- Prelever 10 mL de la première solution mère dans une pipette jaugée

- La verser dans la fiole jaugée

- Prelever 10 mL de la seconde solution mère dans une pipette jaugée

- La verser dans la fiole jaugée

- Compléter la fiole jusqu'au trait de jauge 

- mélanger 

- Remplir une cuve de spectrophotométrie avec la solution fille

__Protocole pour obtenir une photo filtrée numériquement__

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

## __Observations__

__Filtrage de la lumière par des filtres colorés :__

![Image](spectre%20filtre.png)

__Filtrage d'une imege avec un filtre__
