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
    1. Change all values to -300, 300
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
