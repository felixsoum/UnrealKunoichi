# UnrealKunoichi
![UnrealKunoichi](https://user-images.githubusercontent.com/6082364/64686463-b62a1d00-d456-11e9-959e-e380b4975645.png)

## Gfycat Preview
https://gfycat.com/bowedaggressivefritillarybutterfly

## Instructions (en)
1. Show Mixamo example
    1. Trim
    1. In place
    1. No skin
1. Download all assets
    1. Character skeletal mesh
    1. Movement animations
        1. Idle
        1. Walk
        1. Run
    1. Attack animations
        1. Slash
        1. Kick
        1. Throw

### Use Kunoichi character
1. Import skeletal mesh
1. Rename all assets
1. Fix material
1. Change blend mode to opaque
1. Create BP_Kunoichi
1. Pick ThirdPersonCharacter as parent class
1. Change SkeletalMesh to SK_Kunoichi
1. Delete ThirdPersonCharacter in level
1. Add GameMode Override (ThirdPersonGameMode)
1. Change Default Pawn Class to BP_Kunoichi
1. Test in PIE

### Integrate walk/idle/run
1. import all animations
1. Pick Kunoichi for skeleton
1. Rename all assets
1. Organize into folders Combat and Movement
1. Prepare movement blendspace
    1. Create blend space
    1. Change Horizontal Axis name : Right
    1. Change Vertical Axis name : Forward
    1. Change all values to -600, 600
    1. Change Grid division to 12
    1. Add all movement animations into blendspace
1. Create Animation Blueprint with Parent Class AnimInstance and SKEL_Kunoichi skeleton
1. Goto AnimGraph view
1. Add new state machine (Movement)
1. Connect state machien to final animation pose
1. Add new state: Idle_Walk_Run
    1. Add BS_Kunoichi blendspace
    1. Promote Right and Forward variables
1. Goto Event Graph
    1. Use Begin Play node to save reference to BP_Kunoichi
    1. Get relevant vectors from BP_Kunoichi and perform dot product to set correct values for Right and Forward variables
1. Assign ABP_Kunoichi to animation class in BP_Kunoichi
1. Test PIE

### Integrate jump
1. Add and set up states: Jump_Start, Jump_Loop, Jump_End
1. Set up Idle_Walk_Run -> Jump_Start transition
    1. Promote IsInAir variable
1. Set up Jump_Start -> Jump_Loop transition
    1. Use current time ratio node
1. Set up Jump_Loop -> Jump_End transition
    1. Using IsInAir bool
1. Set up Jump_End -> Idle_Walk_Run transition
    1. Use current time ratio node
1. Test using variable details
1. Modify Event Graph to set IsInAir variable using IsFalling node
1. Test PIE

### Add attack
1. Create new input binding
1. Create slash montage
1. Add default slot to AnimGraph
1. Add Attack action event in BP_Kunoichi
1. Test in PIE
1. Add and use IsAttacking bool
1. Import sword mesh and textures
1. Rename assets
1. Fix material
    1. Use texture sample node
1. Add sockets to Kunoichi
    1. Right Shoulder
    1. Right hand
1. Add scene components to new sockets
1. Add static mesh for sword and adjust scene components
1. Scale weapon
1. Test PIE
1. Move weapon to sheated scene component
1. Update BP to move weapon to ready scene component when attacking
1. Test PIE
1. Add delay and test again
1. Replace delay with anim notify
1. Create ReadyWeapon custom event
1. Create AnimNotify_ReadyWeapon in ABP_Kunoichi
    1. Connect it to Ready Weapon event

### Create target dummy
1. Create BP_Dummy actor
1. Replace root with capsule collider
1. Add skeletal mesh and use mannequin SK
1. Set animation to animation asset idle
1. Select collision Presets: Pawn
1. Place dummy in level
1. Add event ActorBeginOverlap -> Print
1. Test PIE
1. Add box collider to sword
1. Test PIE
1. Add CanAttackHit bool to BP_Kunoichi and set it to true at attack start
1. In BP_Dummy cast hit actor to BP_Kunoichi and integrate hit condition
    1. Use AND node to also check IsAttacking

### Improve dummy hit effect
1. Create new material M_Dummy
    1. Use constant3vector
    1. Use linear interpolate
    1. Use scalar parameter
1. Place material in dummy
1. Create dynamic material instance in construction script
    1. Promote the material
1. Try setting the value in the construction script and testing in PIE, then undo
1. Add HitValue float variable in BP_Dummy and use it to change the scalar parameter
1. Increase speed by multiplying with constant

### Extra
1. Create kick combo
    1. Create kick montage
    1. Add bool to determine which attack to use (slash or kick)
        1. Use the select node to select the montage
        1. Add another box collider for kick
    1. Activate and deactive the correct colliders by changing the collision presets
1. Create shuriken projectile
    1. Import and rename assets
    1. Improve shuriken material with fresnel node
    1. Create BP_Shuriken
    1. Add static mesh, box collider and projectile component
1. Create shuriken throw
    1. Create throw montage
    1. Add input binding
    1. Create new upper body slot in throw montage and use it
    1. Update AnimGraph to use pose cache and layed blend per bone
        1. Use Spine as the bone name for the layer
    1. Add anim notify to throw
        1. Use it to spawn a shuriken
        1. Adjust camera angle to improve throw

## Instructions (fr)
1. Montrer l'exemple Mixamo
    1. Trim
    1. Sur place
    1. Pas de skin
1. Télécharger tous les assets
    1. Mesh squelettique du personnage
    1. Animations de mouvement
        1. Idle
        1. Walk
        1. Run
    1. Animations d'attaque
        1. Slash
        1. Kick
        1. Throw

### Utilisez le caractère Kunoichi
1. Importer le mesh squelettique
1. Renommez tous les assets
1. Réparer le matériel
1. Changer le mode de blend en opaque
1. Créez BP_Kunoichi
1. Choisissez ThirdPersonCharacter comme classe parent
1. Changez SkeletalMesh en SK_Kunoichi
1. Supprimez ThirdPersonCharacter dans le niveau
1. Ajouter un remplacement de GameMode (ThirdPersonGameMode)
1. Changez la classe du joueur par défaut en BP_Kunoichi
1. Test en PIE

### Intégrer Idle / Walk / Run
1. Importer toutes les animations
1. Choisissez Kunoichi pour le squelette
1. Renommez tous les assets
1. Organiser dans les dossiers Combat et Mouvement
1. Préparer un blend space
    1. Créer un blend space
    1. Changer le nom de l’axe horizontal: Right
    1. Changer le nom de l’axe vertical: Forward
    1. Modifiez toutes les valeurs en -600, 600
    1. Changer la division de la grille en 12
    1. Ajouter toutes les animations de mouvement dans le blend space
1. Créer un plan d’animation avec la classe parente AnimInstance et le squelette SKEL_Kunoichi
1. Aller à la vue AnimGraph
1. Ajouter une nouvelle state machine (mouvement)
1. Connectez le state machine à la pose finale de l’animation
1. Ajouter un nouvel état: Idle_Walk_Run
    1. Ajouter le blend space BS_Kunoichi
    1. Promouvoir les variables Right et Forward
1. Allez au Event Graph
    1. Utilisez le nœud Begin Play pour enregistrer la référence à BP_Kunoichi.
    1. Obtenez les vecteurs pertinents de BP_Kunoichi et utilisez le produit scalaire pour définir les valeurs correctes pour les variables Droite et Suivante.
1. Affecter ABP_Kunoichi à une classe d'animation dans BP_Kunoichi
1. Test PIE

### Integrate jump
1. Ajouter et configurer des états: Jump_Start, Jump_Loop, Jump_End
1. Configurez la transition Idle_Walk_Run -> Jump_Start
    1. Promouvoir la variable IsInAir
1. Configurer Jump_Start -> transition Jump_Loop
    1. Utiliser le nœud du rapport de temps actuel
1. Configurez la transition Jump_Loop -> Jump_End
    1. Utiliser IsInAir bool
1. Configurez la transition Jump_End -> Idle_Walk_Run
    1. Utiliser le nœud du rapport de temps actuel
1. Testez en utilisant des détails variables
1. Modifier le graphique d’événement pour définir la variable IsInAir à l’aide du noeud IsFalling
1. Test PIE

### Ajouter une attaque
1. Créer une nouvelle input binding
1. Créer un montage slash
1. Ajouter un default slot à AnimGraph
1. Ajouter un événement d'action d'attaque dans BP_Kunoichi
1. Test en PIE
1. Ajouter et utiliser IsAttacking bool
1. Importer le mesh et les textures d'épée
1. Renommer les assets
1. Réparer le matériel
    1. Utiliser un noeud de TextureSample
1. Ajouter des sockets à Kunoichi
    1. Épaule droite
    1. Main droite
1. Ajouter des composants de scène à de nouveaux sockets
1. Ajouter un mesh statique pour l’épée et ajuster les composants de la scène
1. Ajuste l'échelle de l'arme
1. Test PIE
1. Déplacer l'arme vers le composant de la scène
1. Mettre à jour le partenaire pour déplacer l’arme sur le composant de scène prêt à attaquer
1. Test PIE
1. Ajouter un délai et tester à nouveau
1. Remplacer le délai avec anim notify
1. Créer un événement personnalisé ReadyWeapon
1. Créez AnimNotify_ReadyWeapon dans ABP_Kunoichi
    1. Connectez-le à l'événement Ready Weapon

### Créer le mannequin cible
1. Créer un acteur BP_Dummy
1. Remplacez le root par un capsule collider
1. Ajouter le mesh squelettique et utiliser le mannequin SK
1. Définissez l’animation idle sur le mesh.
1. Sélectionnez les préréglages de collision: Pawn
1. Placez le mannequin dans le niveau
1. Ajouter un événement ActorBeginOverlap -> Imprimer
1. Test PIE
1. Ajouter un collisionneur à l'épée
1. Test PIE
1. Ajoutez CanAttackHit bool à BP_Kunoichi et définissez-le sur true au début de l'attaque.
1. Dans BP_Dummy, acteur hit pour BP_Kunoichi et intégration de la condition de hit
    1. Utilisez le noeud AND pour vérifier également IsAttacking

### Améliorer l'effet de frappe factice
1. Créer un nouveau matériau M_Dummy
    1. Utilisez constant3vector
    1. Utiliser interpoler linéaire
    1. Utiliser le paramètre scalaire
1. Placez le matériel dans le mannequin
1. Créer une instance de matériau dynamique dans un script de construction
    1. Promouvoir le matériel
1. Essayez de définir la valeur dans le script de construction et de tester PIE, puis annulez
1. Ajoutez la variable float HitValue dans BP_Dummy et utilisez-la pour modifier le paramètre scalaire.
1. Augmenter la vitesse en multipliant par constante

### Supplémentaire
1. Créer un combo de kick
    1. Créer un montage de kick
    1. Ajoutez bool pour déterminer quelle attaque utiliser (slash ou kick)
        1. Utilisez le nœud de sélection pour sélectionner le montage.
        1. Ajouter un autre collisionneur de boîte pour le coup
    1. Activer et désactiver les collisionneurs corrects en modifiant les préréglages de collision
1. Créer un projectile shuriken
    1. Importer et renommer des actifs
    1. Améliorer le matériel de shuriken avec le noeud de Fresnel
    1. Créer BP_Shuriken
    1. Ajouter un maillage statique, un collisionneur de boîtes et un composant projectile
1. Créer un lancer de shuriken
    1. Créer un montage de projection
    1. Ajouter une liaison d'entrée
    1. Créez une nouvelle fente pour le haut du corps dans le montage de projection et utilisez-la.
    1. Mettez à jour AnimGraph pour utiliser le cache de pose et le mélange pondéré par os.
        1. Utilisez Spine comme nom d'os pour le calque
    1. Ajouter anim notify à jeter
        1. Utilisez-le pour engendrer un shuriken
        1. Ajustez l'angle de la caméra pour améliorer la projection
