# Soutenance de thèse
Repository containing the source files for the PhD oral defense

<video src="videos/part_4_applications/types_mires_assemblage.gif" width="512" height="512" controls autoplay loop></video>

![](videos/part_4_applications/types_mires_assemblage.gif)

## Plan

### Introduction - 2 slides
Avant de commencer je tiens à remercier les membres du jury pour leur présence aujourd’hui, que ce soit en présentiel ou à distance ainsi que mes directeurs de thèse pour leur accompagnement et leur soutien tout au long de ce doctorat…
Institut FEMTO-ST, laboratoire AS2M

Contexte : microrobotique

1) Introduction
    - Champs applicatifs de la microrobotique variés
    - Pourquoi la vision par ordinateur
    - Contexte : mesure de position à l'échelle microscopique
2) De l’échelle macroscopique à l’échelle microscopique
    - Exemple des difficultés pour la mesure de position en microscopie
    - Distance de travail très courtes
    - Longues focales + objectifs de microscopes
    - Profondeur de champ réduite + difficultés d'illuminer`` correctement la scène
    - DONC Méthodes stéréo vision impossibles à mettre en place + Mesure planaire seulement

Break : Mesure de position difficile en microscopie, maintenant étude des solution existantes

### État de l'art - 3 slides
1) Aperçu des méthodes de mesure de position en microscopie
    - Présenter l'échelle de résolution
    - 3 grandes familles de méthodes
    - Utilisation d'un nombre réduits de pixels qui définissent une région représentative de l'objet observé
    - Meilleure résolution : même méthode mais avec un objet plus structuré
    - Utiliser la totalité de l'image et effectuer une corrélation entre images
    - Structurer complètement la scène avec des marqueurs périodiques
    - Structurer = contrebalancer le rapport signal sur bruit qui diminue
    - Mesure de phase = ultra résolue DONC c'est ce qu'on va faire
Notre cas d'étude = mires périodiques, mais plage de mesure d'une seule période
2) Marqueurs périodiques et mesure de phase
    - 2 méthodes pour étendre la plage de mesure
    - Utiliser deux périodes légèrement différentes pour faire la mesure à l'aide d'une période globale plus grande
    - Insérer un codage absolu sur les points des mires périodiques
3) Verrous actuels – objectifs de recherche
    - Commenter l'image : peu de place disponible, grande plage de mesure souhaitée et grande résolution
    - Présenter les verrous un à un
    - Expliquer les objectifs de ces travaux de recherche

Break : Après avoir vu les verrous de la mesure de pose en microscopie, étudions en quoi les mires périodiques permettent de répondre aux différents objectifs fixés.

### Méthode de mesure de pose - 8 slides
1) Propriété des signaux périodiques 1D continus
    - Signal sinusoïdal continu + représentation en niveaux de gris
    - Transformée de Fourier = Décomposition en fréquences d'un signal spatial
    - Dual : représentation de la fréquences et de l'angle
Break : mesure de la fréquence et de la phase d'un signal en continu OK, mais que se passe-t-il en échantillonnant CAR cas réel des images acquises
2) Propriété des signaux périodiques 1D échantillonnés
    - Même signal, mais échantillonné et quantifié
    - TF mais pas possible d'étudier directement la phase du pic fréquentiel car sinus cardinal + échantillonné DONC pas assez résolu
    - Donc filtrage du pic puis étude de la phase spatiale après transformée inverse
    - Propriétés de cette phase comprise entre -pi et pi avec des sauts de phase toutes les périodes
        - Phase proche de 0 = intensité du signal max DONC on est au centre d'un point
        - Phase proche de +- pi = intensité du signal min DONC on est sur le pourtour d'un point
        - Mesure de la phase du signal possible directement en mesurant la phase en 0 mais pas assez résolu
    - Déroulage de la phase puis régression linéaire sur droite de phase : assure une meilleure résolution car on prend en compte tout le signal
    - Équation de la droite de phase et mesure directe des paramètres du signal (fréquence et phase)

    Break : Mesure des paramètres d'un signal 1D échantillonné OK, maintenant extension aux signaux 2D

3) Propriété des signaux périodiques 2D
    - Processus de création : Extension d'un signal périodique 1D en 2D + angle
    - Représentation du signal en niveaux de gris
    - Multiplication des deux mires 2D à 1 direction 
    - Position des pics fréquentiels
    - Filtrage + TF inverse + déroulage des images de phase PUIS régression linéaire pour obtenir des équations des plans de phase
    - 6 infos qui représentent fréquence de chacune des directions, angles et phase

Break : comment mieux voir en quoi ces 6 paramètres décrivent complètement la pose de la mire

4) Mesure de position des mires périodiques 2D
    - Ce qu'on voit à l'écran : vue 3D mire périodique dans l'espace + Image de la mire sur le capteur caméra + densité spectrale de la mire
    - Montre le lien entre pose de la mire et position des pics fréquentiels. Les 4 coeffs a1, b1, a2, b2 sont liés à ces positions et phi1, phi2 à la phase de la mire

Break : Comment exploiter ces 6 informations indépendantes pour mesurer la pose 3d de la mire ?

5) Quid du 3D ?
    - Explication figure : projection d'une image de mire vers la caméra avec une projection ortho. Puis schéma
    - Pourquoi ce modèle est intéressant
    - lien entre position des pics fréquentiels, coefficients des plans de phase et position spatiale des périodes
    - Comment exploiter ces informations pour mesurer la pose 3D ?
6) Mesure de pose 3D d’une mire 2D
    - Projection des points de la mire vers la caméra avec projection ortho
    - 4 équations non linéaires, 3 inconnues
    - Ambiguïté

Break : comment lever cette ambiguïté ? Utiliser un autre modèle de projection

7) Extension de la plage de mesure
8) Décodage robuste et absolu de la position

**Rajouter conclus sur les méthodes et transitions vers résultats**

### Validation et performances - 5 slides
1) Résolutions planaires atteintes (1/2)
    - Diversité des actionneurs utilisés : translation, rotation, grandement résolu, moins résolu mais grande plage etc.
    - limite = environnement, pas la méthode
2) Résolutions planaires atteintes (2/2)
3) Résolutions hora-plans atteintes (1/2)
4) Résolutions hora-plans atteintes (2/2)
5) Essais de robustesse à la dégradation des images acquises

### Applications à la microrobotique - 6 slides
1) Développement d’une bibliothèque logicielle polyvalente (1/2)
2) Développement d’une bibliothèque logicielle polyvalente (2/2)
    - Complexité en O(n log(n))
3) Étalonnage de microrobots à articulations souples
4) Étalonnage de microrobots à articulations souples
5) Mesure duale force – déplacement sur fibre végétale
    - Matériaux bio-sourcés
6) Micro-assemblage de puces micro-fluidiques

### Conclusions et perspectives - 7 slides
1) Conclusions (1/2)
2) Conclusions (2/2)
3) Perspectives : la microscopie à holographie numérique (1/4)
4) Perspectives : la microscopie à holographie numérique (2/4)
5) Perspectives : la microscopie à holographie numérique (3/4)
5) Perspectives : la microscopie à holographie numérique (4/4)
    - Applicable surtout dans le cas micro
    - Encombrant
6) Perspectives : Vers des mires non planaires
7) Bilan des publications

### Slides pour questions
- Robustesse de la méthode de décodage
    - Vidéos en boucle sur la robustesse
    - Imagette de phase avec seuils pour déterminer sur ligne codante à `1` ou `0`
- Mesure des angles hors-plan sans ambiguïté
    - vidéo avec balayage beta entre -10 et +10 degrés + images des dérivées successives de la phase