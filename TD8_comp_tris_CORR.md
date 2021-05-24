---
jupyter:
  jupytext:
    formats: ipynb,md
    text_representation:
      extension: .md
      format_name: markdown
      format_version: '1.3'
      jupytext_version: 1.11.2
  kernelspec:
    display_name: Python 3
    language: python
    name: python3
---

# TD8 Comparateur de tris - CORRECTION


Nous avons étudié la semaine dernière deux algorithmes de tris : 
- le tri par sélection
- le tri par insertion

L'objectif du TD de cette semaine est d'appliquer ces 2 algorithmes sur des exemples de listes et de les comparer avec l'algorithme de tri natif utilisé par Python.


## 1. Tri par sélection :
En vous aidant de l'animation ci-dessous, rappeler le principe de l'algorithme du tri par sélection :
![selection](select_sort.gif)

<!-- #region -->
__1.1. Principe du tri par sélection :__


On __sélectionne__ dans la partie de la liste non triée le plus petit élément  
que l'on échange avec le premier élément dans la partie non triée.  
Il devient le plus grand dans la partie triée.  
On recommence la sélection et l'échange jusqu'à l'avant dernier élément.





__1.2. Récupérer dans le TD de la semaine dernière le script de ce tri et coller le code en dessous :__  
<!-- #endregion -->

```python
#code de la fonction tri par sélection
def tri_par_selection(liste):
    """La fonction prend en argument une liste non vide et
    renvoie la liste triée.
    liste : une liste non vide de nombres ou chaine de caractères"""
    for i in range(len(liste)):
        m=i
        for j in range(i+1,len(liste)):
            if liste[j] < liste[m]:
                m=j
        liste[i],liste[m]=liste[m],liste[i]
    return liste
```

__1.3. Utiliser la liste aléatoire suivante pour tester le tri par sélection__

```python
from random import *
liste=[randint(1,100) for i in range(10)]
print(liste)
#compléter le code ci-dessous pour afficher la liste triée avec le tri par sélection
print(tri_par_selection(liste))
```

## 2. Tri par insertion :
Observer de même l'animation suivante et rappeler le principe de l'alogorithme du tri par insertion :
![insertion](tri_insert_anim.gif)

<!-- #region -->
__2.1. Principe du tri par insertion :__


On __insére__ le premier élément de la partie de la liste non triée à sa place dans la partie triée.  
On recommence l'insertion jusqu'au dernier élément de la liste.





__2.2. Récupérer dans le TD de la semaine dernière le script de ce tri et coller le code en dessous :__  
<!-- #endregion -->

```python
#code de la fonction du tri par insertion
def insertion(liste,rang):
    """La fonction prend en arguments une liste non vide et un indice,
    et insère dans la liste l'élément d'indice rang parmi les éléments d'indice 0 à rang-1.
    liste : une liste non vide de nombres ou chaine de caractères
    rang : un entier."""
    m = liste[rang]
    while rang>0 and m<liste[rang-1]:
        liste[rang] = liste[rang-1]
        rang = rang - 1
    liste[rang] = m
    return liste

def tri_par_insertion(liste):
    """La fonction prend en argument une liste non vide et renvoie la liste triée.
    liste : une liste non vide de nombres ou chaines de caractères
    """
    for i in range(1,len(liste)):
        liste = insertion(liste,i)
    return liste
```

__2.3. Utiliser la liste aléatoire suivante pour tester votre fonction et afficher la liste triée__

```python
liste=[randint(1,100) for i in range(10)]
print(liste)
#Compléter le code ci-dessous pour afficher la liste triée avec le tri par insertion
print(tri_par_insertion(liste))
```

<!-- #region -->
## 3. Observation des tris en activité
Visualiser les 3 vidéos suivantes (__avec le son !__) pour une comparaison visuelle des 2 tris au programme de la NSI.

La troisième vidéo est donnée à titre de curiosité pour vous montrer d'autres types de tris bien plus efficaces (mais aussi plus complexes à coder...)

- video tri par insertion (1min57) :  https://youtu.be/8oJS1BMKE64?list=PLZh3kxyHrVp_AcOanN_jpuQbcMVdXbqei


- video tri par selection (1min22) : https://youtu.be/92BfuxHn2XE?list=PLZh3kxyHrVp_AcOanN_jpuQbcMVdXbqei


- vidéo de comparaison de 15 tris (5min49) :  https://www.youtube.com/watch?v=kPRA0W1kECg)

Le nom du tri apparait en haut à gauche de la vidéo accompagné du nombre de comparaisons, du nombre d'accès aux données et du temps de calcul.
<!-- #endregion -->

## 4. Comparaison des tris du programme
Après cette petite récréation, passons aux choses sérieuses.

Pour comparer les deux tris par insertion et sélection, il sera nécessaire d'utiliser la fonction `time()`inclue dans le package `time`.  
Nous avons déjà utilisé cette fonction dans un TP précédent, revoir ci-nécessaire ce TP pour plus d'explications.

On chargera donc en mémoire le script suivant et on complètera son code.  
Ne pas oublier de relancer les deux fonctions du __1.__ et __2.__ 




```python
import time
#début du décompte du temps
t1 = time.time()
#mettre le code ici
t2 = time.time()
#affichage du temps d'execution 
print("temps d'execution du tri : ", t2-t1)
```

__Travail demandé :__
1. Construire une liste de 3000 entiers pris au hasard entre 1 et 10000.  
Mesurer le temps d'exécution pour les 2 algorithmes et comparer.

_Attention : pensez à reconstruire la liste entre les 2 tris !_

2. Construire cette fois une liste d' entiers __consécutifs__ de 0 à 2999.  
Mesurer le temps d'exécution pour les 2 algorithmes et comparer.

3. Construire enfin une liste de 100000 entiers aléatoires entre 1 et 100000 et mesurer le temps d'execution avec le tri proposé par défaut de Python ( fonction `sort()` )


## Question 1 :

```python
liste=[randint(1,10000) for i in range(3000)]
t1 = time.time()
tri_par_selection(liste)
t2 = time.time()
print("temps d'execution du tri par selection : ", t2-t1)
liste=[randint(1,10000) for i in range(3000)]
t1 = time.time()
tri_par_insertion(liste)
t2 = time.time()
print("temps d'execution du tri par insertion : ", t2-t1)
```

## Question 2 :

```python
liste=[i for i in range(3000)]
t1 = time.time()
tri_par_selection(liste)
t2 = time.time()
print("temps d'execution du tri par selection : ", t2-t1)
liste=[i for i in range(3000)]
t1 = time.time()
tri_par_insertion(liste)
t2 = time.time()
print("temps d'execution du tri par insertion : ", t2-t1)
```

## Question 3 :

```python
liste=[randint(1,100000) for i in range(100000)]
t1 = time.time()
liste.sort()
t2 = time.time()
print("temps d'execution du tri Python : ", t2-t1)
```
