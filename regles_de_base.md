# 1. Fixation des règles du UNO

- 108 cartes
- 4 couleurs (bleu, jaune, vert et rouge). Pour chaque couleur : 
    - 1 seul 0 ;
    - 2 exemplaire de chaque chiffre de 1 à 9 ;
    - 2 +2 ;
    - 2 Inversion ;
    - 2 Passe ton tour.
    (25 carted par couleur donc 100)
- 4 Jokers (Changement de couleur)
- 4 Super Jokers (+4)

Les effets officiels : 
    - Passe : le joueur suivant passe son tour.
    - Inversion : le sens du jeu change. 
        Subtilité importante : à 2 joueurs, l'Inversion agit comme un Passe, donc on rejoue.
    - +2 : le joueur suivant pioche 2 cartes et passe son tour.
    - Joker : le joueur choisit la couleur suivante.
    - +4 : choix de la couleur, le suivant pioche 4 cartes et passe son tour.
        En théorie, on n’a le droit de le jouer que si on n’a aucune carte de la couleur demandée. Le suivant peut « contester » : si le joueur trichait, c’est lui qui pioche 4 ; sinon, le contestataire pioche 6.
    - Uno : Il faut l'annoncer quand il ne reste plus qu'une carte. Si un autre joueur le remarque avant le tour suivant, l'oubli coûte 2 cartes de pénalité.
    - Pioche : Si on ne peut pas jouer, on pioche 1 carte. Si elle est jouable, on peut la poser tout de suite. Sinon, le tour passe.

Règles maison mais drôle : 
    - Le cumul des +2 et +4.
    - Piocher jusqu'à avoir une carte jouable.
    - Règle du 7-0 : Un 7 permet d'échanger sa main avec un joueur, un 0 fait tourner toutes les mains dans le sens de jeu.
    - Jump-in : poser une strictement identique hors de son tour.

On pourra d'abord ajouter toutes les règles de bases puis d'ajouter peut-être les règles maison sous forme d'option activable au lancement de la partie.

Cas limites à anticiper : 
    - La pioche est vide : on garde la carte du dessus de la défausse, on mélange le reste et cela devient la nouvelle pioche.
    - La toute première carte retournée est une carte spéciale. Officiellement, son effet s'applique au premier joueur, sauf pour un +4, qu'on remet dans le paquet avant d'en retourner une autre.
    - La fin de partie : Quand un joueur a vidé toute sa main, la partie se termine.


# 2. Problème du multijoueur : les mains cachées

On veut du 1v1, 1v1v1 et 1v1v1v1. Pour gérer le 2 à 4 joueurs est plutôt simple côté logique, le problème c'est qui sont ces joueurs. 

Choix à faire niveau implémentation : 
    - Contre des IA
    - Hot-seat
    - En réseau (sockets, client / serveur)

On fera une abstraction au niveau Joueur dont héritent 'JoueurHumain' et 'JoueurIA'. On pourra brancher plus tard comme un nouveau type de joueur 'JoueurDistant'.

# 3. Architecture : séparation entre la logique et l'affichage

Type MVC (Modèle-Vue-Contrôleur) : 
- Le modèle, ie la logique pure, aucun affichage : 
    - 'Couleur (enum), le type ou la valeur de la carte (enum aussi : PASSE, INVERSION, PLUS_DEUX, JOKER, PLUS_QUATRE) et 'Carte'.
    - 'Paquet' (Pioche, 108 cartes, mélange, tirage), 'Defausse', et la main d'un joueur.
    - 'Joueur' et ses sous-types.
    - 'MoteurDeJeu' : Joeur courant, sens, couleur active, application des effets, vérification des coups, détection de victoire.
    - 'OptionPartie' : Règles maison activées.
- La vue, ie l'affichage : dans la console d'abord, l'interface graphique ensuite.
- Le contrôleur fait le lien entre les actions de l'utilisateur et le modèle.

# 4. L'interface graphique 
- Console : à utiliser un premier. Validation de toute la logique.
- Swing : intégré directement au JDK.
- JavaFX : On pourra basculé sur celui-ci, plus moderne et joli.

