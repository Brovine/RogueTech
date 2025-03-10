this mod allows you next things 
1. Add external animated parts to vehicles
2. Changing chassis terrain interactions
3. Forbids certain mechs/vehicles to spawn on certain biomes
4. Add custom animated hardpoints

main settings in mod.json
	"SortBy": {
		"orderByCbillValue":false,
		"orderByNickname":false,
		"orderByTonnage":false
	},                                        - sorting order settings
	"PartialMovementOnlyWalkByDefault": true, - if true and AllowPartialSprint is not overridden via value in Unaffected section or CUAllowPartialSprint stat value, 
	                                            units allow partial movement only walk not sprint
	"AllowRotateWhileJumpByDefault": true, - if false and player units will not be able to rotate while normal jumping unless overridden by unit CUAllowRotateWhileJump stat value 
												or Unaffected.AllowRotateWhileJump
											if true player unit will be able to rotate while normal jumping  unless overridden by unit CUAllowRotateWhileJump stat value 
												or Unaffected.AllowRotateWhileJump
	"ConvoyRouteBeaconVFX":"vfxPrfPrtl_artillerySmokeSignal_loop", - VFX for convoy route points
	"ConvoyRouteBeaconVFXScale":{"x":1,"y":1,"z":1}, - VFX scale for convoy route points
	"IntelShowMiniMap": false - if true contract details accessible from lance configuration screen will show minimap
	"IntelShowMood": false - if true contract details accessible from lance configuration screen will show contract mood
	"IntelCompanyStatShowMiniMap": "Intel_Show_Minimap" - if this boolean company stat is true contract details accessible from 
	                                                      lance configuration screen will show minimap even if IntelShowMiniMap is false
	"IntelCompanyStatShowMood": "Intel_Show_Mood" - if this boolean company stat is true contract details accessible from 
	                                                      lance configuration screen will show contract mood even if IntelShowMood is false
	"IntelShowMood": false - if true contract details accessible from lance configuration screen will show contract mood
	"timerObjectiveChange": {  - for certain contract types game logic timers can be altered. Timers eg. reinforcements arrival etc.
		"DefendBase":{         - contract type name
			"autoDeployAdvice":1,   - timer change for auto deploy
			"manualDeployAdvice":2  - timer change for manual deploy
		}
	}
	"DeployManual": true, - allowing manual deploy in random contract.
	"DeployManualSpawnProtection": true - if true spawn protection will be used on manual deploy. How is it working:
	                                      on player deploy all units on battle fields gain spawn protection flag
										  this flag is been removed on unit activation end (reserve does not affects this flag).
										  if either attacker either target have this flag attack is always miss
										  So you have deployed your units, AI takes turn - they can't hit you cause both you and AI have flag
										  AI got its turn - yours turn now. Even if AI units choose to act (not reserve) and loose protection flag,
										  you can't hit cause your units have flag but you can move. When you've done AI units chooses to reserve act 
										  and still can't hit cause they have flag. Next round both yours and AI units loose protection flag and can shoot normally
	"DeployAutoSpawnProtection": true - if true on first round begin all units gain spawn protection 
	"AskForDeployManual": true - if true and manual deployment is allowed will ask if player wants to set deploy position. 
	                             if false and manual deployment is allowed - deploy will be manual. 
	"ManualDeployForbidContractTypes": [] - list of contract types names, for listed contract types manual deploy will be forbidden
	"DeployMaxDistanceFromOriginal": 30 - max distance from original deploy position
	"DeployMinDistanceFromEnemy": 300 - min distance form enemy unit
	              NOTE: DeployMaxDistanceFromOriginal and DeployMinDistanceFromEnemy working like OR. Eg. your manual deploy position should be near than <DeployMaxDistanceFromOriginal>
				  from original spawn point OR farer than <DeployMinDistanceFromEnemy> every enemy
				  Also no pathing checking performed - if you deploy your lance to deep water or mountain it will be your own damn fault. 
    "fixWaterHeight":true, - whether or not underwater terrain height should be fixed. If false hovers will not be able to move over water/deep water surface
    "maxWaterSteepness":30, - max underwater terrain steepness - if underwater terrain cell will have steepness grater than this value it will be fixed to 0 and cell will be marked as deep water
                              this needed for two things - hovers should not be affected by water cell steepness and not hovers should not be able to pass through this cell
    "waterFlatDepth":2, - if underwater cell have depth grater than this value x2 it will be lifted up.
    "deepWaterDepth":5  - if underwater cell have depth grater than this it will be marked as deep water. (Note: 5 it is greater than almost game's vehicle height)
    "LancesIcons": [ "one", "two", "three" ], - icons for lance selector 
    "overallDeploySize": 6,  - deploy size for skirmish or without bigger drops 
    "Lances": [ {"size":6,"allow":5,"is_vehicle":false},{"size":4,"allow":3,"is_vehicle":true} ] - lances layout for skirmish or without bigger drops 
    "MaxVehicleRandomPilots": 0, - max vehicles pilots to be autogenerated
    "CanPilotVehicleProbability": 0.0, - chance of random generated pilot to become vehicle pilot
    "CanPilotAlsoMechProbability": 0.0, - chance of vehicle pilot to can also pilot mech
    "ShowVehicleBays": false, - if false user can't access vehicle bays
    "CanPilotVehicleTag": "pilot_vehicle_crew", - name of tag showing pilot can control vehicles
    "CannotPilotMechTag": "pilot_nomech_crew", - name of tag showing pilot CAN NOT control mech
    "BaysCountExternalControl":false - if true mechbays count controlled by external mod via API
    "ArgoBaysFix":1, -               - if BaysCountExternalControl is true and player controls Argo, active bays count is modified by this value.
	"AllowVehiclesEdit": false - if true vehicles allowed to edit and move to/from storage.
    "MechBaySwitchIconMech": "mech" - icon showing mech bays are showed
    "MechBaySwitchIconVehicle":"vehicle" - icon showing vehcile bays are showed
    "MechBaySwitchIconUp":"weapon_up" - icon to scroll bays up
    "MechBaySwitchIconDown":"weapon_down" - icon to scroll bays down
    "ShowActiveAbilitiesIcon": "futuristic", - icons for show/hide abilities buttons. If empty Move/Sprint icons used. 
    "ShowPassiveAbilitiesIcon": "ram",
    "HideActiveAbilitiesIcon": "futuristic",
    "HidePassiveAbilitiesIcon": "ram",
	"PlayerControlConvoyTag": "convoy_player_control" - tag added to lance's spawnEffects to turn on player controllable convoy to mechanic
example from contract override definition:
.............
    "employerTeam" : {
        "encounterLayerData" : {
            "EncounterObjectGuid" : "09a421f4-c536-428b-9c33-711cb45425c6"
        },
        "teamGuid" : "ecc8d4f2-74b4-465d-adf6-84445e5dfc230",
        "teamName" : "EmployerTeam",
        "faction" : "INVALID_UNSET",
        "teamLeaderCastDefId" : "castDef_TeamLeader_Current",
        "lanceOverrideList" : [
            {
                "lanceSpawner" : {
                    "EncounterObjectGuid" : "d3d75b1e-ace5-43e8-b037-79a2dd2b3d4e"
                },
                "name" : "Lance_Friendly_Escort",
                "lanceDefId" : "Tagged",
                "lanceTagSet" : {
                    "items" : [
                        "lance_type_convoy"
                    ],
                    "tagSetSourceFile" : "tags/LanceTags"
                },
                "lanceExcludedTagSet" : {
                    "items" : [],
                    "tagSetSourceFile" : "tags/LanceTags"
                },
                "spawnEffectTags" : {
                    "items" : [ "convoy_player_control" ], <----- there
                    "tagSetSourceFile" : "tags/SpawnEffectTags"
                }, 
.......................................
    "ConvoyMaxDistFromOther": 200, - max distance from other units of convoy allowed
    "ConvoyMaxDistFromPlayer": 300, - max distance from nearest player's unit (if nearest player's unit is farer convoy unit becomes immobilized). 
	                                 Positions far from player units forbidden by pathing also.
    "ConvoyMaxDistFromRoute": 30, - speaking raw it is max distance from route lines allowed by convoy units pathing

MechResizer has been devoured
## Settings

All resize settings are exclusive, so you cannot apply layered resizing i.e. a default of 1.1 will not multiply a tag of 2. Resizing preference is in the following order: vector supplied in `<TYPE>ResizeMultiplierVectors`, tags, `<TYPE>ResizeMultipliers`, prefab, `mod.json`-supplied default, and a hard-coded default of 1.25.

The dimensions for the `*Vectors` settings are measured like: <X> - width (shoulder to shoulder), <Y> - height (toes to head), <Z> - depth (chest to back)

### Tag-Based Resizing
In addition to the settings that follow that are set in `mod.json`, you can also change the size of elements using tags. There are two formats:

1. `mr-resize-N`: `N` can be an integer or decimal number and will resize the given item equally in all dimensions
2. `mr-resize-X-Y-Z`: `X`, `Y`, and `Z` can be an integers or decimal numbers and will scale on that axis

The tags must be put in the following type of file to be applied:

Type | File Type | Tag Location
--- | --- | ---  
Mechs | `data/chassis/chassisdef_<variant>.json` | `ChassisTags`->`items`
Vehicles | `data/vehicle/vehicledef_<variant>.json` | `VehicleTags`->`items`
Turrets | `data/turrets/turretdef_<variant>.json` | `TurretTags`->`items`
Projectiles | `data/weapon/Weapon_<variant>.json` | `ComponentTags`->`items`

### `mod.json` settings
Setting | Type | Default | Description
--- | --- | --- | ---
`debug` | `boolean` | false | enable debug logging
`defaultMechSizeMultiplier` | float | 0.9 | override this to globally change all mech sizes in combat. Vanilla is 1.25
`defaultVehicleSizeMultiplier` | float | 1 | override this to globally change all vehicle sizes in combat. Vanilla is 1
`defaultTurretSizeMultiplier` | float | 1 | override this to globally change all turret sizes in combat. Vanilla is 1
`defaultProjectileSizeMultiplier` | float | 1 | override this to globally change certain weapon (missiles only ATM) projectile sizes in combat. Vanilla is 1
`mechSizePrefabMultipliers` | json hash | {} | change the size of any set of mechs that share a common `PrefabBase` in their chassis definition files. For example, making all highlander variants very large might look like: `"highlander": {"x": 8, "y": 8, "z": 8}`
`vehicleSizePrefabMultipliers` | json hash | {} | change the size of any set of vehicles that share a common `PrefabBase` in their vehicle chassis definition files.
`turretSizePrefabMultipliers` | json hash | {} | change the size of any set of turrets that share a common `PrefabBase` in their turret chassis definition files.
`projectileSizePrefabMultipliers` | json hash | {} | change the size of any set of projectiles that share a common `PrefabBase` in their weapon firing them's weapon definition files.
"MechScaleJRoot": false - if true for while resizing mech MR will try to resize j_Root transform instead of whole game object. Which can help to avoid floating mechs
                          default is false. 

### Deprecated `mod.json` Settings - please use the size change options above i
Setting | Type | Default | Description
--- | --- | --- | ---
`mechResizeMultipliers` _deprecated_ | json hash | {} | change the size of mechs using the format `"chassis string" : multiplier`. A big locust would be like `"chassisdef_locust_LCT-1V": 15`
`mechResizeMultiplierVectors` _deprecated_ | json hash | {} | change mech sizes using three dimensional multipliers with format `"chassis string": { "x": Xmulti, "y": Ymulti, "z": Zmulti }`. A very tall locust might look like `"chassisdef_locust_LCT-1V": {"x": 1,"y": 2, "z": 1}``
`vehicleResizeMultipliers` _deprecated_ | json hash | {} | change the size of vehicles using the format `"chassis string" : multiplier`. A big APC would be like `"vehiclechassisdef_APC_Wheeled": 3`
`vehicleResizeMultiplierVectors` _deprecated_ | json hash | {} | change vehicle sizes using three dimensional multipliers with format `"chassis string": { "x": Xmulti, "y": Ymulti, "z": Zmulti }`. A very long APC might look like `"vehiclechassisdef_APC_Wheeled": {"x": 1,"y": 1, "z": 2}``
`turretResizeMultipliers` _deprecated_ | json hash | {} | change the size of turrets using the format `"chassis string" : multiplier`. 
`turretResizeMultiplierVectors` _deprecated_ | json hash | {} | change turret sizes using three dimensional multipliers with format `"chassis string": { "x": Xmulti, "y": Ymulti, "z": Zmulti }`.
`projectileResizeMultipliers` _deprecated_ | json hash | {} | change the size of projectiles using the format `"weapon id string" : multiplier`.
`projectileResizeMultiplierVectors` _deprecated_ | json hash | {} | change projectile sizes using three dimensional multipliers with format `"weapon id string": { "x": Xmulti, "y": Ymulti, "z": Zmulti }`.
    
    
DesignMask definition
new section 
	"Custom":{
		"CustomMoveCost":{
			"Hover": {    - name of move cost overriden section. You can set same name at chassis definition to override move cost for this chassis and biome
								additive for CAC temp masks. 
								For example radioactive_forest.Hover.moveCost = forest.Hover.moveCost + radioactive.Hover.moveCost - 1.0
				"moveCost":9999.9,
				"SprintMultiplier":9999.9
			}
		}
	}

VehicleChassis/Chassis
"CustomParts":{
    "AlternateRepresentations": [                                       - section where you can define alternate representation for your mech
      {                                                                 
        "PrefabIdentifier": "chrprfmech_vf11lambase-001",               - prefab identifier for alternate representation
        "AdditionalPrefabs": [],                                        - list of additional prefabs for this representation (mostly needed for custom hardpoints)
        "PrefabBase": "vf11lam",                                        - prefab base
        "HardpointDataDef":"hardpointdatadef_vf11lam",                  - hardpoint definition
        "Type": "AirMech",                                              - type (available values: Normal, AirMech)
        "HoveringSoundStart": "jet_start",                              - hover sound start event. Default jet_start
        "HoveringSoundEnd": "jet_end",									- hover sound start event. Default jet_end
		"additionalEncounterTags": [ "unit_vtol" ],                     - encounter tags list will be applied to actor. Note: you should be careful with this option, 
																		  tags in this list should not be equal to tags in contracts definitions otherwise you can break 
																		  objectives logic. 
		"NoJumpjetsBlock": false,                                       - if true mech in airmech mode do not have restriction on jumping regardless flying height 
																		  but it still can't use DFA attack
		"MoveClamp": 0,                                                 - move clamp, same rules as for Unaffected section, but per representation
		                                                                  0 - counted as not set. Example on math: clamp = 0.5, speed = 100
																		  at start unit will be able to move 0-50 distance
																		  if previous turn move distance was 50 it will be able to move 25-75
																		  at maximum speed it will be able to move 50-100
		"MinJumpDistance": 0,                                           - min jump distance. Effective value will be <JumpDistance> * <MinJumpDistance>. 
		                                                                  Unit in this mode can't jump distance less than this. 
																		  Value less or equal 0 or greater or equal 1 counted as unset
        "FlyHeight": 15.0,                                              - Flying height
        "AirMechVerticalJets":[                                         - list of jump jets
          {
            "Prefab":"vf11lam_vjets_left_leg",                          - prefab name
            "Attach":"j_LHeel",                                         - attach bone
            "JetsAttachPoints":["jetAttachPoint"]                       - name of transform where jet stream should be spawned
          },
          {
            "Prefab":"vf11lam_vjets_right_leg",
            "Attach":"j_RHeel",
            "JetsAttachPoints":["jetAttachPoint"]
          },
          {
            "Prefab":"vf11lam_vjets_torso",
            "Attach":"j_Spine2",
            "JetsAttachPoints":["jetAttachPoint"]
          }
        ]
      }
	  NOTE: to switch mech representation to alternate in battle you should create activatable component setting CUAlternateRepresentation statistic value
	  example is in vf11lam/upgrades/Gear_LAMSwitcher
	  CUAlternateRepresentation's value is zero based index of representation from AlternateRepresentations array where 0 is default representation defined in chassis
	  Eg. if you want to show first alternate representation you should set value = 1 to it
	  Unity project is in LAMExample.unitypackage
    ] 
	"SquadInfo": {            - ONLY for mech's chassis 
      "Troopers":5,           - units count in trooper squad, up to 8. If set as 1 no logic changing performed 
      "UnitSize": 0.2,        - unit scale
	  "armorIcon":"VehicleSwarm_Solid",  - custom squad unit icons
	  "outlineIcon":"VehicleSwarm_Outline",
	  "structureIcon":"VehicleSwarm_Lined",
      "DeadUnitToHitMod": 9,  - to-hit mod when last trooper squad remain. Example squad - 4 units, DeadUnitToHitMod - 9. When all 4 units operational modifier = 0
	                            one unit dead modifier = 3, two units dead, modifier = 6, three units dead, modifier = 9. Formula: modifier = <DeadUnitToHitMod> * <dead units> / (<Troopers> - 1)
      "Hardpoints":{          - visual hardpoints mapping. Internally squad it is one mech, each trooper is its location. MechDef reflects this fact.
	                            Visually each trooper is shrinked mech representation. To properly align weapons representation in this sub mechs models this mad is needed.
								In example all energy weapons goes to left arms of troopers etc. Should be made corresponded to base chassis hardpoints definition.
        "Energy": "LeftArm",
        "Missile": "LeftTorso",
        "AntiPersonnel": "RightArm"
      }
    },
	NOTE: squad can have no more than one jumpjet. This means no matter amount of actual jumpjets components you install. 
	If each operational location (squad trooper) have working jumpjet it will be counted as whole squad have one jupmjet in jump distance calculation.
	Squad can't have stability nor heat. 
	Squad can't be legged cause it have no legs internally.
	Squad can be destroyed only all units destroyed.
	Squad will get less AoE damage if some troopers dead
	Squad will get less damage from landmines if some troopers dead.



    "MeleeWeaponOverride":{    - override melee weapon for chassis. If you'll set weapon with non-melee weapon category or weapon than needs ammo, it will be only your fucken problem.
      "DefaultWeapon": "Weapon_MeleeAttackBattleClaw"
    }
    "AOEHeight": 55,  - this value will be added to y-coordinate of current position in AoE damage calculations (weapon/landmines/component's explosions). 
                        Can be altered runtime via CUAOEHeight actor's statistic value (float)
    "FiringArc":60, - if set and > 10 means vehicle firing arc in degrees and vehicle have to rotate toward target to fire. 
                      Working for mechs too, but you should note - direction decal will not been changed. 
    "Unaffected":{  
      "AllowPartialMovement": true - if true partial movement for this unit is allowed. Default value true, corresponding stat name "CUAllowPartialMovement"
	                                 NOTE: partial movement means if you holding left shift while setting move destination point,
									 it will place waypoint this position instead of destination point allowing you set more complicated trajectory
									 i strongly suggest you to forbid partial movement for VTOLs and LAMs in airmech mode
									 NOTE: it would not be able to set new waypoint if you have less than PartialMovementGuardDistance (default 15.0) movepoints left
      "AllowPartialSprint": true - if true partial movement for this unit is allowed while sprinting. Default value <!PartialMovementOnlyWalkByDefault>,
									corresponding stat name "CUAllowPartialSprint".
									NOTE: if AllowPartialSprint is false and AllowPartialMovement is true unit allowed to partial move only while walking
									if AllowPartialSprint is not set and PartialMovementOnlyWalkByDefault is true allowed to partial move only while walking
									if AllowPartialSprint is not set and PartialMovementOnlyWalkByDefault is false allowed to partial move only while walking and sprinting
      "AllowRotateWhileJump": true - if true unit is allowed to rotate while jumping. Default value <AllowRotateWhileJumpByDefault>,
									corresponding stat name "CUAllowRotateWhileJump".
	  "MoveClamp": 0.3,       - this value controls inertia of unit. Unit move distance can't be greater [move distance prev. round] + MoveClamp*Speed 
                                and less [move distance prev. round] - MoveClamp*Speed. Only for AI. For Pathing: true value should be between 0.2 and 0.5. 
                                For Pathing: true default value 0.2. For others  default 0 (mean not apply at all).
      "DesignMasks":"true",   - if true chassis will be unaffected to all terrain design masks effects except move cost. 
								Can be altered runtime via CUDesignMasksUnaffected actor's statistic value (boolean)
								Note! when CUDesignMasksUnaffected becomes true unit looses all design mask sticky effects previously applied
								and its current occupied design mask counted as empty, that is why changing CUDesignMasksUnaffected in design mask is very foolish move
								CUDesignMasksUnaffected becomes false only design mask effects from current position is applied. 
      "Pathing":"true",       - if true chassis will be unaffected by pathing limitations 
							(eg can climb vertical surface, other actors collisions, not cause filmsy objects destruction on impact). 
							If choosed as melee target attacker melee (NOT AP) weapon always miss. Ignore terrain move cost.
              Can be altered runtime via CUPathingUnaffected actor's statistic value (boolean)
      "Fire":"true",         - if true chassis not receive damage passing burning terrain. Can be altered runtime via CUFireActorStatUnaffected actor's statistic value (boolean)
      "Landmines":"true",     - if true chassis not cause landmines to explode (still can receive AoE damage from landmines if explosion triggered by someone else).
                               Can be altered runtime via CULandminesUnaffected actor's statistic value (boolean)
      "MoveCostBiome":true   - if true unaffected by move modify per biome. Can be altered runtime via CUMoveCostBiomeUnaffected actor's statistic value (boolean)
    },
    "MoveCostModPerBiome":{  - dictionary of move cost modify per biome design mask
      "DesignMaskBiomeMartianVacuum":2.0,
      "DesignMaskBiomeLunarVacuum":10.0
    }, 
	"NoIdleAnimations": false - restrict idle animation for chassis. Can be altered runtime using CUNoMoveAnimation statistic value, boolean
	"NoMoveAnimations": false - restrict move animation for chassis. Can be altered runtime using CUNoRandomIdleAnimations statistic value, boolean
    "quadVisualInfo":{            - settings for quad visuals 
      "UseQuadVisuals": true,     - if false quad visuals will not be used
      "FLegsPrefab": "chrPrfMech_kingcrabBase-001",  - prefab for forward legs. 
	                                                   for rear legs chassis PrefabIdentifier value is used
      "BodyLength":7.0,                              - length of the body in meters
      "FLegsPrefabBase": "kingcrab",                 - used for jumpjets and headlight spawning if model has one
      "RLegsPrefabBase": "kingcrab",
      "NotSuppressRenderers":["_left_leg_","_right_leg_"]  - list of front and rear legs model parts which should not be suppressed 
    },
	Please read "AnimationType": "QuadBody" custom part section to get info on quad body setup

	"ArmsCountedAsLegs": false - setting this flag true will cause next consequences
									 1. Side torso crush not lead to attached arm destroy
									 2. Mech will not die if both legs destroyed. It will be destroyed on destruction head, center torso or all four limbs
									 3. Loosing leg do not remove sprint ability. Mech is not counted as legged until two limbs destroyed.
									 4. Arm destruction leads to increase minimum instability even with OnlyPermanentLossFromLegs: true in constants.
									 5. Destruction of arm counts as leg destruction in terms of added instability after attack
									 6. Destruction one leg not force mech to fall. To fall on limb destruction two limbs should be destroyed.
	"FrontLegsDestructedOnSideTorso": false - working only is ArmsCountedAsLegs is true. If set to true it overrides "Side torso crush not lead to attached arm destroy" 
											  to original behavior eg. on side torso nuke, relevant front leg will be nuked too
	"CustomHitTable": "custhittable_experimental" - id of custom hit table. See "custom hit table" section for more info.
													Note! squads are not reacting this setting. They have own hit tables math.
	"LegDestroyedMovePenalty": -1f - move speed penalty on leg destroy. if < 0 or omitted Constants.MoveConstants.LegDestroyedPenalty used
	"LegDamageRedMovePenalty": -1f - move speed penalty on leg penalized. if < 0 or omitted Constants.MoveConstants.LegDamageRedPenalty used
	"LegDamageYellowMovePenalty": -1f - move speed penalty on leg damages. if < 0 or omitted Constants.MoveConstants.LegDamageYellowPenalty used
	"LegDamageRelativeInstability": -1f - leg damage relative instability. if < 0 or omitted Constants.PilotingConstants.LegDamageRelativeInstability used
	"LegDestroyRelativeInstability": 1f - leg destroy relative instability. if < 0 or omitted 1.0 used

	"MoveCost":"Hover",     - move cost per design mask overridence (useless if Unaffected.Pathing is true).
                            Can be altered runtime via CUMoveCost actor's statistic value (string)
    "TieToGroundOnDeath":"true", - if true tied to ground on death (useful if prefab positions is altered by sections below)
	"HighestLOSPosition":{"x":0,"y":60,"z":0}, - offset for targeting
	"TurretAttach":{
		"offset":{"x":-0.6,"y":52.3,"z":5.5}, - offset for turret location, if omitted not touched
		"rotate":{"x":0,"y":0,"z":0} - rotation for turret location, if omitted not touched
	},
	"BodyAttach":{
		"offset":{"x":-0.6,"y":54,"z":0}  - offset for body location, if omitted not touched
	},
    "TurretLOS":{
		"offset":{"x":-0.6,"y":52.3,"z":5.5} - offset for turret line-of-sight location (usually same as TurretAttach), if omitted not touched
	},
	"LeftSideLOS":{
		"offset":{"x":-2,"y":54,"z":0} - offset for left side line-of-sight location, if omitted not touched
	},
	"RightSideLOS":{
		"offset":{"x":2,"y":54,"z":0} - offset for right side line-of-sight location, if omitted not touched
	},
	"leftVFXTransform":{
		"offset":{"x":-2,"y":54,"z":0} - offset for left vfx attach point (usually same as LeftSideLOS), if omitted not touched
	},
	"rightVFXTransform":{
		"offset":{"x":2,"y":54,"z":0} - offset for right vfx attach point (usually same as RightSideLOS), if omitted not touched
	},
	"rearVFXTransform":{
		"offset":{"x":0,"y":54,"z":-7} - offset for rear vfx attach point (usually same as RightSideLOS), if omitted not touched
	},
	"thisTransform":{
		"offset":{"x":0,"y":52,"z":0} - offset for main transform (as far as i can see not used for vehicles), if omitted not touched
	},
	"lightsTransforms":[ - offsets and rotations array for lights (i don't know why y-coordinate have to be doubled this values get from experiments)
		{"offset":{"x":-1.1,"y":103.8,"z":4.7},"rotate":{x:"60","y":0,"z":0}},
		{"offset":{"x":1.2,"y":103.8,"z":4.7},"rotate":{x:"60","y":0,"z":0}}
    ],
		"CustomParts":[  - array for external animated parts for chassis (all prefabs will be requested on loading dependences for chassis)
			{
				"prefab":"warrior_rotor_top_x10_brass", - prefab name
                            !READ NEXT NOTE CAREFULLY IF YOU EXPERIENCED PROBLEMS WITH SPAWNING YOUR PRESITANT OBJEJECTS USING CUSTOM UNITS MOD!
                            To make it work you must follow some rules 
                            1. You can't spawn prefab containing object with your models directly. You have to create empty object, name it as you want it to be referenced,
                            and only than add objects with your models as children for this object. 
                            2. For name of parent object you have to use letters in LOWER case this is some sort of unity/game/modtek limitation.
                            3. You can search at the unity package i'm providing with this mod for examples how to create asset with prefabs engine can successfully load.
				"prefabTransform":{                     - prefab transformations
					"offset":  {"x":0,"y":1.4,"z":0.5},
					"scale":   {"x":1,"y":1,"z":1},
					"rotation":{"x":0, "y":0, "z":0}
				},
        "RequiredUpgrades":["Gear_Actuator_Coventry_Alpha"], - list of upgrades required for this component to spawn. If list empty or omitted part will spawn always. 
                                                                If at least one component from list present, part will spawn.
                                                                For mechs only MechChassisLocation checked. For vehicles all vehicle checked. 
        "RequiredComponents": [                             - list of components required for this component to spawn. If list empty or omitted part will spawn always. 
                                                                If at least one component from list present, part will spawn.
          {
            "MechSearchLocations": [ "LeftArm" ],           - list of locations where component will be searched. If empty or omitted every location is suitable.
            "VehicleSearchLocations": []                    - same but for vehicles.
            "DefId": "Gear_Actuator_Coventry_Alpha"         - definition id. If empty or omitted every component is suitable.
            "CategoryId": ""                                - CustomComponents category id. If empty or omitted every component category is suitable.
          }
        ],
        "VehicleChassisLocation":"Front",               - attach location for vehicles
        "MechChassisLocation":"RightArm",               - attach location for mechs
                                                        NOTE! on location or entire unit destruction all spawned objects removing from game 
                                                        maybe later, i will implement proper physics.
        "MaterialInfo":{
          !READ NEXT NOTE CAREFULLY IF YOU EXPERIENCED PROBJEMS WITH TEXTURING YOUR LOADABLE OBJECTS!
          Some basics: model it is mesh + material. Material is shader + shader's settings relative to this model (textures is part of settings).
          Shader is set of instruction for GPU telling it how draw your model properly. 
          If you try to use standard unity shader for your prefabs - it will work wrong cause it does not know about game rendering features.
          So, to get your models to be textured properly you have next options:
          1. If you experienced enough you can write your own shader than will work correctly in game (but if you can, why are you reading this?)
          Fortunately i've found basic shader developers using to texture objects and its settings are very similar to standard one. 
          2. You can use UABE to replace standard unity's shader to game's one. (You can't import game's shader to your unity project cause absence of shader's source)
             But it needs additional post-production phase for your asset. After every change and reassemble you have to modify your asset to replace shader.
          3. You can include MaterialInfo to your custom part definition. If you do, my code while spawning objects will search through all models in your prefab for materials you point
             and replace their shaders to ones you points (for example i'm providing possibility to replace shader to game's standard one)
          "warrior_top_rotor_0Mat":{                              - name of material in your prefab to search
            "shader": "battletechstandartshader",                 - name of shader object
            "shaderKeyWords":["_DETAIL_OVERLAY","_EMISSION","_METALLICGLOSSMAP","_NORMALMAP"] - list of shader keywords.
          }
        },
        
				"AnimationType":"SimpleRotator",        - animation type
				"AnimationData":{ - data specific for animation type
        "speed":5, - rotor blades rotation speed
        "sound":"AudioEventList_motor_motor_buzzy_start", - sound for rotor 
        "axis":"y" - axis to rotate around (note it is object's axis not world's one it is depends on object's rotation)
        "rotateBone":"saw" - name of transform to rotate.
            Some basics: your prefab can consist of many child objects (models). 
            With SimpleRotator you can rotate whole set or just one of them. Look at king crab's chassis circle saw demo. 
        }  
			},
			{
				"prefab":"warrior_rotor_bottom_x10_brass",
				"prefabTransform":{
					"offset":  {"x":0,"y":1.2,"z":0.5},
					"scale":   {"x":1,"y":1,"z":1},
					"rotation":{"x":0, "y":0, "z":0}
				},
        "VehicleChassisLocation":"Front",
				"AnimationType":"SimpleRotator",
				"AnimationData":{"speed":-5,"axis":"y"}
			},
			{
				"prefab":"warrior_turret_x10_red",
				"prefabTransform":{
					"offset":  {"x":0,"y":0,"z":0},
					"scale":   {"x":20,"y":20,"z":20},
					"rotation":{"x":0, "y":0, "z":0}
				},
        "VehicleChassisLocation":"Turret",       - parent attach point (only have meaning only in visual plane)
        "VehicleChassisLocation":"Turret",       - parent attach point (only have meaning only in visual plane)
				"AnimationType":"Turret",                - turret rotates toward target on fire 
				"AnimationData":{
          "speed":10,                 - in idle state turret rotates +60 <-> - 60 degrees in horizontal plane
          "axis":"y"                  - reserved for future use
          "VehicleLocation": "Front", - all weapons in this location will be attached to with turret and their fire visuals will be played from its barrel
          "barrels":[                 - array of barrel transforms (only first barrel using now)
            {"offset":{"x":0,"y":-3,"z":3}}  - barrel offset/rotate/scale. Parent point is turret center
          ]
        }
        NOTE! You can attach to vehicle as many turrets as you want but they need have different VehicleLocation. Only first turret in each location will be used.
			},
			{
				"prefab":"",
				"prefabTransform":{
					"offset":  {"x":0,"y":0,"z":0},
					"scale":   {"x":1,"y":1,"z":1},
					"rotation":{"x":0, "y":0, "z":0}
				},
        "VehicleChassisLocation":"Left",
				"AnimationType":"WeaponMountPoint",  - weapon mount point animator, just stub. Having barrels as turret but not rotating to target. 
                                               Useful if you want to have different mount points for left and right side of vehicle 
                                               (vanilla have only two attach points turret and body, eg. weapon from left/right/front/rear locations in vanilla will be visually attached to body)
				"AnimationData":{
          "speed":1,                           - not used
          "VehicleLocation": "Left",          - same meaning as for Turret animator
          "barrels":[                         - same meaning as for Turret animator
            {"offset":{"x":0,"y":-3,"z":0}}
          ]
        }
			},
		
        "AnimationType": "MechTurret",
        "AnimationData": {
          "TurnAnimator":"base", - name of game object turn animator attached
          "AttachPoints":[
            {"Location":"LeftTorso", - all custom hardpoints with attach type "Turret" in this location will be attached to turret
				"AttachTo":"WeaponAttachL", - name of game object hardpoints will be attached
				"Animator":"WeaponMountL" - name of game object vertical move animator attached
				},
            {"Location":"RightTorso","AttachTo":"WeaponAttachR","Animator":"WeaponMountR"}
          ]
        },

        "AnimationType": "QuadBody",
        "AnimationData": { 
          "VerticalRotate":"rotate",              - name of quad body model part which is used as vertical rotation axis
          "TurretAttach": "turret_attach",        - attach point for mech turret
          "FrontLegsAttach":"front_legs_attach",  - attach point for front legs model
          "ShowFrontLegsAxis": false,             - show axis (for position purposes)
          "DamageAnimator":"barg_CT_LT_RT_plus_damage_models", - name of object containing body damage animator
          "RTVFXTransform":"RT_vfx_transform",                 - vfx attach point for right torso 
          "LTVFXTransform":"LT_vfx_transform",                 - vfx attach point for left torso 
          "CTVFXTransform":"CT_vfx_transform",                 - vfx attach point for center torso
          "HEADVFXTransform":"HEAD_vfx_transform",             - vfx attach point for head
          "JumpJetsSpawnPoints": ["jumpjet_rear","jumpjet_front","jumpjet_left","jumpjet_right"], - list jump jets spawn points
          "HeadLightSpawnPoints": ["headlight_left","headlight_right"]                            - list of headlight spawn point
        }

	]
}, 

you can control per-biome spawning via vehicle/mech tags
current supported values:
	NoBiome_generic,
	NoBiome_highlandsSpring,
	NoBiome_highlandsFall,
	NoBiome_lowlandsSpring,
	NoBiome_lowlandsFall,
	NoBiome_desertParched,
	NoBiome_badlandsParched,
	NoBiome_lowlandsCoastal,
	NoBiome_lunarVacuum,
	NoBiome_martianVacuum,
	NoBiome_polarFrozen,
	NoBiome_tundraFrozen,
	NoBiome_jungleTropical,
	NoBiome_urbanHighTech,

  
  
CustomHardpoints section  

  "CustomHardpoints": {
    "prefabs": [                                                         - list for avaible prefabs
      {
        "prefab": "chrprfweap_kingcrab_leftarm_laser_eh1",               - prefab name. Should be mentioned in mod.json manifest section, any mod.json, game's engine just should be able to load this prefab 
                                                                           and know which asset contains it. 
                                                                           Some notes on correct prefab creation:
                                                                             your object containing mesh renderer should not be root prefab object. I'm suggesting next prefab structure:
                                                                             chrprfweap_kingcrab_leftarm_laser_eh1 (root object. name should be same with prefab)
                                                                                  |
                                                                                  ---> barrels (object containing Animator component. Animator should be one per prefab, if any, it presents not necessary)
                                                                                         |
                                                                                         -----> barrel_mesh (object containing mesh renderer)
                                                                                                    |
                                                                                                    -----> emitter point (empty object pointing fire vfx start position)
                                                                           Your overall structure can be more complicated - for example you can add some particle vfxes. You should just follow next rules
                                                                           1. Root object should be empty. 
                                                                           2. No more than one animator allowed (count of animations clips are limited only by resource amount and your fantasy)
        "shaderSrc": "chrPrfWeap_kingcrab_leftarm_ac10_bh1",             - game existing prefab used as source of shader. Game's engine have specific settings and default unity's shaders rendering not exactly correct. 
                                                                           Objects becomes very bright. To avoid this, code can replace your shader to game's one. 
                                                                           NOTE: if shaderSrc is not empty and pointing to existing prefab, ALL mesh renderers will be altered, but only mesh renderers will be affected. 
                                                                           Particle system stay untouched. 
        "emitters": [                                                    - list of names. This names points to objects which positions is used to calculate start coordinates for fire effects. 
                                                                           This is very important, cause if you are not set this weapon will fire from wrong positions (fallback positions is 0,0,0 relative to location)
          "fire1",
          "fire2"
        ],
        "preFireAnimation": "prefire"                                    - name of bool variable used by code to make animator know when to start prefire animation. If not empty code will set this variable to true on prefire. 
                                                                           Fire sequence not begins until animation is finished. Code suggesting this animation have 1 sec length. 
                                                                           Modder can control speed of this animation by PrefireAnimationSpeedMod setting per weapon/mode/ammo definitions (multiplicative, default 1). 
                                                                           Before starting animation code will set prefire_speed animator variable accordingly. So animation clip should be setuped to use this variable 
                                                                           as source of speed modifier. 
                                                                           At end of fire sequence this variable will be set to false. Animator should use this as trigger to move to idle state. 
      },
      {
        "prefab": "chrprfweap_kingcrab_leftarm_rotatelaser_eh1",
        "shaderSrc": "chrPrfWeap_kingcrab_leftarm_ac10_bh1",
        "emitters": [
          "fire1",
          "fire2",
          "fire3"
        ],
        "preFireAnimation": "prefire",
        "fireEmitterAnimation": [                                        - names of bool variables controlling fire animations. 
                                                                           On first shoot variable with index 0 will be set to true (if name is not empty). All other to false.
                                                                           On second shoot variable with index 1 will be set to true (if name is not empty). All other to false.
                                                                           And so on.
                                                                           At fire complete all variables set to false. Animator should use this to return animation machine to idle state. 
                                                                           In next example variable with index 0 is empty cause in current model at idle state barrels already in correct position for first shoot, so no animation needed.
                                                                           Fire animation speed can be controlled same way as prefire. FireAnimationSpeedMod setting per ammo/mode/weapon (multiplicative, default 1).
                                                                           "fire_speed" variable should be used in prefab's animation clips. 
          "",
          "fire1",
          "fire2"
        ]
      }
    ],
    "aliases": {                                                        - aliases. This setups link between HardpointData element and prefab. You can setup replacement of one weapon type prefabs to prefabs of another type. 
      "chrPrfWeap_kingcrab_leftarm_laser_eh1":{
        "location": "leftarm",
        "prefab": "chrprfweap_kingcrab_leftarm_laser_eh1"
      },
      "chrPrfWeap_kingcrab_leftarm_rotatelaser_eh1":{
        "location": "leftarm",
        "prefab": "chrprfweap_kingcrab_leftarm_rotatelaser_eh1"
      },
      "chrPrfWeap_kingcrab_leftarm_rotategauss_bh1":{
        "location": "leftarm",
        "prefab": "chrprfweap_kingcrab_leftarm_rotatelaser_eh1"
      }
    }
  }, 
  
!NOTE! With current version even if game can't find prefab for weapon - empty object will be spawned and default weapon representation will be setup. It will have wrong fire position an no mesh but no circle of death. 

Custom hit tables

{
	"Id": "custhittable_experimental", - id for this table, must be same as file name
	"hitTable": {                      - hit table
		"FromFront": {                 - attack direction
			"Head": 10,                - <Armor location name>:<weight>. Armor location can be either mech-style (CenterTorso, LeftTorso etc) 
			                             either vehicle-style (Front, Rear etc). <weight> is integer.
			"CenterTorso": 1,
			"LeftTorso": 1,
			"RightTorso": 1,
			"LeftArm": 1,
			"RightArm": 1,
			"LeftLeg": 1,
			"RightLeg": 1,
			"CenterTorsoRear": 1,
			"LeftTorsoRear": 1,
			"RightTorsoRear": 1
		},
		"FromLeft": {
			"Head": 10,
			"CenterTorso": 1,
			"LeftTorso": 1,
			"RightTorso": 1,
			"LeftArm": 1,
			"RightArm": 1,
			"LeftLeg": 1,
			"RightLeg": 1,
			"CenterTorsoRear": 1,
			"LeftTorsoRear": 1,
			"RightTorsoRear": 1
		},
		"FromRight": {
			"Head": 10,
			"CenterTorso": 1,
			"LeftTorso": 1,
			"RightTorso": 1,
			"LeftArm": 1,
			"RightArm": 1,
			"LeftLeg": 1,
			"RightLeg": 1,
			"CenterTorsoRear": 1,
			"LeftTorsoRear": 1,
			"RightTorsoRear": 1
		},
		"FromBack": {
			"Head": 10,
			"CenterTorso": 1,
			"LeftTorso": 1,
			"RightTorso": 1,
			"LeftArm": 1,
			"RightArm": 1,
			"LeftLeg": 1,
			"RightLeg": 1,
			"CenterTorsoRear": 1,
			"LeftTorsoRear": 1,
			"RightTorsoRear": 1
		},
		"FromTop": {
			"Head": 10,
			"CenterTorso": 1,
			"LeftTorso": 1,
			"RightTorso": 1,
			"LeftArm": 1,
			"RightArm": 1,
			"LeftLeg": 1,
			"RightLeg": 1,
			"CenterTorsoRear": 1,
			"LeftTorsoRear": 1,
			"RightTorsoRear": 1
		},
		"ToProne": {
			"Head": 10,
			"CenterTorso": 1,
			"LeftTorso": 1,
			"RightTorso": 1,
			"LeftArm": 1,
			"RightArm": 1,
			"LeftLeg": 1,
			"RightLeg": 1,
			"CenterTorsoRear": 1,
			"LeftTorsoRear": 1,
			"RightTorsoRear": 1
		},
		"FromArtillery": {
			"Head": 10,
			"CenterTorso": 1,
			"LeftTorso": 1,
			"RightTorso": 1,
			"LeftArm": 1,
			"RightArm": 1,
			"LeftLeg": 1,
			"RightLeg": 1,
			"CenterTorsoRear": 1,
			"LeftTorsoRear": 1,
			"RightTorsoRear": 1
		}
	},
	"adjacentLocations": {                                         - setting for adjacent locations
		"Head": [ "CenterTorso", "LeftTorso", "RightTorso" ],      - <armor location>: <list of nearby locations>. location can be either mech-style (CenterTorso, LeftTorso etc) 
			                                                         either vehicle-style (Front, Rear etc)
		"CenterTorso": [ "LeftTorso", "RightTorso", "Head" ],
		"LeftTorso": [ "CenterTorso", "LeftArm" ],
		"RightTorso": [ "CenterTorso", "RightArm" ],
		"LeftArm": [ "LeftTorso" ],
		"RightArm": [ "RightTorso" ],
		"LeftLeg": [ "LeftTorso" ],
		"RightLeg": [ "RightTorso" ],
		"CenterTorsoRear": [ "LeftTorsoRear", "RightTorsoRear" ],
		"LeftTorsoRear": [ "RightTorsoRear", "CenterTorsoRear" ],
		"RightTorsoRear": [ "LeftTorsoRear", "CenterTorsoRear" ]
	},
	"clusterSpecialLocation": "None"              - special location for cluster hit table generation. 
	                                                for mechs by default it is Head, for vehicles None
													this location. This location is reacting on
													ClusterChanceNeverClusterHead and ClusterChanceNeverMultiplyHead 
													Combat constants
}

  
appendix A. Game's build-in audio events names in format '<name>':<id>
id - just for info purposes
 'AudioEventList_aircraft_aircraft_dropship_gencon_landing':3307102648
 'AudioEventList_aircraft_aircraft_leopard_destruction':556692128
 'AudioEventList_aircraft_aircraft_leopard_landing':1271550741
 'AudioEventList_aircraft_aircraft_leopard_takeoff':199263772
 'AudioEventList_aircraft_aircraft_leopard_touchAndGo':4220346206
 'AudioEventList_aircraft_aircraft_union_destruction':3671973990
 'AudioEventList_aircraft_aircraft_union_landing':3475508787
 'AudioEventList_vehicle_vehicle_explosion_a':3264067355
 'AudioEventList_vehicle_vehicle_explosion_b':3264067352
 'AudioEventList_vehicle_vehicle_gallant_engine_start':4190637255
 'AudioEventList_vehicle_vehicle_gallant_engine_stop':965956205
 'AudioEventList_vehicle_vehicle_gallant_start':1957306428
 'AudioEventList_vehicle_vehicle_gallant_stop':1500812688
 'AudioEventList_vehicle_vehicle_striker_engine_start':1747122798
 'AudioEventList_vehicle_vehicle_striker_engine_stop':661937998
 'AudioEventList_vehicle_vehicle_striker_start':2272730975
 'AudioEventList_vehicle_vehicle_striker_stop':2358986789
 'AudioEventList_vehicle_vehicle_tank_engine_start':335805546
 'AudioEventList_vehicle_vehicle_tank_engine_stop':61446978
 'AudioEventList_vehicle_vehicle_tank_start':1585469955
 'AudioEventList_vehicle_vehicle_tank_stop':423783297
 'AudioEventList_vehicle_vehicle_turret_interrupted':2305709755
 'AudioEventList_vehicle_vehicle_turret_start':1268444341
 'AudioEventList_vehicle_vehicle_turret_stop':843885591
 'AudioEventList_amb_amb_steam_engineeringRoom':2012392099
 'AudioEventList_ambiences_ambiences_start':1596568133
 'AudioEventList_ambiences_ambiences_stop':1987049447
 'AudioEventList_docking_docking_dock':1127131822
 'AudioEventList_docking_docking_release':111588762
 'AudioEventList_jump_jump_end':2752223339
 'AudioEventList_jump_jump_start':3244792144
 'AudioEventList_whoosh_whoosh_argo_large':2571020097
 'AudioEventList_whoosh_whoosh_argo_medium':1086353609
 'AudioEventList_whoosh_whoosh_argo_short':1302843434
 'AudioEventList_whoosh_whoosh_leopard_large':1370841601
 'AudioEventList_whoosh_whoosh_leopard_medium':1713558921
 'AudioEventList_whoosh_whoosh_leopard_small':3573500489
 'AudioEventList_whoosh_whoosh_long_hi':2556949102
 'AudioEventList_whoosh_whoosh_long_lo':2489838548
 'AudioEventList_whoosh_whoosh_long_mix':1301660715
 'AudioEventList_whoosh_whoosh_medium_hi':4184872571
 'AudioEventList_whoosh_whoosh_medium_lo':4117761961
 'AudioEventList_whoosh_whoosh_medium_mix':577441512
 'AudioEventList_whoosh_whoosh_short_hi':418135726
 'AudioEventList_whoosh_whoosh_short_lo':351025172
 'AudioEventList_whoosh_whoosh_short_mix':3722038635
 'AudioEventList_radio_radio_end':4172435892
 'AudioEventList_radio_radio_test01':3051689856
 'AudioEventList_radio_radio_test02':3051689859
 'AudioEventList_radio_radio_test03':3051689858
 'AudioEventList_vo_vo_play_argo_ambient':1697983434
 'AudioEventList_vo_vo_play_argo_group':2419063319
 'AudioEventList_vo_vo_play_argo_simgame':1791954385
 'AudioEventList_vo_vo_play_computer_ai':3491070856
 'AudioEventList_vo_vo_play_missions':3519092509
 'AudioEventList_vo_vo_play_pilot_player_character':2045319018
 'AudioEventList_vo_vo_play_pilots':3651348061
 'AudioEventList_vo_vo_play_procedural_mission':1810496138
 'AudioEventList_vo_vo_play_restoration_mission':662635667
 'AudioEventList_vo_vo_static_start_mission':650213631
 'AudioEventList_vo_vo_static_start_pilot':780605847
 'AudioEventList_vo_vo_static_stop_mission':498061635
 'AudioEventList_vo_vo_static_stop_pilot':236982011
 'AudioEventList_vo_vo_stop_argo_ambient':2960428520
 'AudioEventList_vo_vo_stop_argo_group':1872226985
 'AudioEventList_vo_vo_stop_argo_simgame':2543473511
 'AudioEventList_vo_vo_stop_missions':1531591975
 'AudioEventList_vo_vo_stop_pilots':1280583203
 'AudioEventList_vo_vo_stop_procedural_mission':4139172876
 'AudioEventList_vo_vo_stop_restoration_mission':2757205817
 'AudioEventList_environment_environment_beacon_loop_play':524534697
 'AudioEventList_environment_environment_beacon_loop_stop':2046951631
 'AudioEventList_environment_environment_beacon_pulse':4270851921
 'AudioEventList_environment_environment_dustdevils_loop_start':1564329446
 'AudioEventList_environment_environment_dustdevils_loop_stop':1910069030
 'AudioEventList_play_play_distant_battle_m010':2813920021
 'AudioEventList_play_play_fan':2757069037
 'AudioEventList_play_play_generator':3104499145
 'AudioEventList_play_play_laser_mining_machine':2853477536
 'AudioEventList_play_play_mission060_klaxon':3159316920
 'AudioEventList_play_play_orbital_gun':3135092258
 'AudioEventList_play_play_rubble_electrical':2848102585
 'AudioEventList_play_play_spores':1377559064
 'AudioEventList_play_play_urban_fan':1898457080
 'AudioEventList_play_play_urban_fountain_large':4127992541
 'AudioEventList_play_play_urban_fountain_medium':1401121053
 'AudioEventList_play_play_urban_fountain_small':3779719925
 'AudioEventList_play_play_urban_generator_coolant':2852242899
 'AudioEventList_play_play_urban_generator_electrical':2895017949
 'AudioEventList_play_play_urban_holograms':2004687783
 'AudioEventList_play_play_water_skirt_vent':3553859511
 'AudioEventList_play_play_waterfall_short_narrow':1601871927
 'AudioEventList_play_play_waterfall_short_wide':3075392599
 'AudioEventList_play_play_waterfall_tall_narrow':3485580056
 'AudioEventList_play_play_waterfall_tall_wide':2941377040
 'AudioEventList_play_play_artillery_impact':655314149
 'AudioEventList_play_play_artillery_projectile':1799047542
 'AudioEventList_play_play_dropPod_impact':3657599031
 'AudioEventList_play_play_dropPod_projectile':1023942412
 'AudioEventList_play_play_orbital_ppc':3188235375
 'AudioEventList_stop_stop_distant_battle_m010':319214499
 'AudioEventList_stop_stop_fan':503719263
 'AudioEventList_stop_stop_generator':3985384471
 'AudioEventList_stop_stop_laser_mining_machine':1898163914
 'AudioEventList_stop_stop_rubble_electrical':1587172455
 'AudioEventList_stop_stop_urban_fan':4021683170
 'AudioEventList_stop_stop_urban_fountain_large':1393668887
 'AudioEventList_stop_stop_urban_fountain_medium':2533969139
 'AudioEventList_stop_stop_urban_fountain_small':4141285539
 'AudioEventList_stop_stop_urban_generator_coolant':3265439909
 'AudioEventList_stop_stop_urban_generator_electrical':1245777447
 'AudioEventList_stop_stop_urban_holograms':2263294485
 'AudioEventList_stop_stop_water_skirt_vent':2942943201
 'AudioEventList_crab_crab_close_impact':1474530971
 'AudioEventList_crab_crab_close_move':2887032870
 'AudioEventList_crab_crab_opentoattack':3798826581
 'AudioEventList_crab_crab_opentoready':1934134290
 'AudioEventList_ducking_ducking_on_melee':1646489255
 'AudioEventList_eject_eject_launch':239187470
 'AudioEventList_eject_eject_projectile':3356178986
 'AudioEventList_foley_foley_long':1281966843
 'AudioEventList_foley_foley_medium':279517784
 'AudioEventList_foley_foley_short':2462372597
 'AudioEventList_hatchet_hatchet_latch':3971533133
 'AudioEventList_hatchet_hatchet_move':1016923602
 'AudioEventList_hatchet_hatchet_slide':4111452128
 'AudioEventList_hatchet_hatchet_sparks':728688223
 'AudioEventList_mech_mech_bodyfall':3638155978
 'AudioEventList_mech_mech_bodyfall_heavy':593568874
 'AudioEventList_mech_mech_bodyfall_light':2434904079
 'AudioEventList_mech_mech_bodyfall_medium':4235120740
 'AudioEventList_mech_mech_cockpit_explosion':1589129056
 'AudioEventList_mech_mech_coolant_vent':1007289689
 'AudioEventList_mech_mech_damage_burning_electrical_start':28447346
 'AudioEventList_mech_mech_damage_burning_electrical_stop':2604832682
 'AudioEventList_mech_mech_damage_burning_sparks_start':3786872438
 'AudioEventList_mech_mech_damage_burning_sparks_stop':350931958
 'AudioEventList_mech_mech_damage_bursts_sparks':4201573853
 'AudioEventList_mech_mech_destruction_a':3290458103
 'AudioEventList_mech_mech_destruction_b':3290458100
 'AudioEventList_mech_mech_destruction_c':3290458101
 'AudioEventList_mech_mech_engine_damaged_badly':1285733082
 'AudioEventList_mech_mech_engine_damaged_mildly':3177945601
 'AudioEventList_mech_mech_engine_powerdown':3882980581
 'AudioEventList_mech_mech_engine_powerdown_death':3583119990
 'AudioEventList_mech_mech_engine_powerup':2497018962
 'AudioEventList_mech_mech_engine_start':2535540750
 'AudioEventList_mech_mech_engine_stop':3401536366
 'AudioEventList_mech_mech_fire_large':792342065
 'AudioEventList_mech_mech_fire_medium':3793694553
 'AudioEventList_mech_mech_fire_small':855540089
 'AudioEventList_mech_mech_fire_small_internal':3769906135
 'AudioEventList_mech_mech_fire_stop':1514463188
 'AudioEventList_mech_mech_footstep':2435876175
 'AudioEventList_mech_mech_footstep_idle':4099323152
 'AudioEventList_mech_mech_impact01':1474674966
 'AudioEventList_mech_mech_impact02':1474674965
 'AudioEventList_mech_mech_impact03':1474674964
 'AudioEventList_mech_mech_impact04':1474674963
 'AudioEventList_mech_mech_jumpjets_heavy_start':3438577016
 'AudioEventList_mech_mech_jumpjets_heavy_stop':2763246980
 'AudioEventList_mech_mech_jumpjets_light_start':2671627645
 'AudioEventList_mech_mech_jumpjets_light_stop':2640150271
 'AudioEventList_mech_mech_jumpland':740494746
 'AudioEventList_mech_mech_metal_squeal':940202708
 'AudioEventList_mech_mech_part_break_a':2526891318
 'AudioEventList_mech_mech_part_break_b':2526891317
 'AudioEventList_mech_mech_part_break_c':2526891316
 'AudioEventList_mech_mech_surface_strike':1794745359
 'AudioEventList_mech_mech_water_enter':1431069237
 'AudioEventList_mech_mech_water_exit':1987229737
 'AudioEventList_motor_motor_buzzy_start':2339019304
 'AudioEventList_motor_motor_buzzy_stop':3768317428
 'AudioEventList_motor_motor_clicky_start':803403707
 'AudioEventList_motor_motor_clicky_stop':459470361
 'AudioEventList_motor_motor_sawserver_start':1069869742
 'AudioEventList_motor_motor_sawserver_stop':796140174
 'AudioEventList_move_move_mechanical':98366580
 'AudioEventList_move_move_mechanical_short':325303723
 'AudioEventList_on_on_ground_impact_hit':846702759
 'AudioEventList_on_on_ground_impact_miss':1134680808
 'AudioEventList_on_on_melee_impact':3039888256
 'AudioEventList_torso_torso_rotate_interrupted':2247726887
 'AudioEventList_torso_torso_rotate_start':1210558537
 'AudioEventList_torso_torso_rotate_stop':1356790499
 'AudioEventList_MU_MU_Play_GameplayMusic':441149344
 'AudioEventList_MU_MU_Play_MenuMusic':4039172695
 'AudioEventList_MU_MU_Stop_AllAudioExceptMusic':1917352548
 'AudioEventList_MU_MU_Stop_GameplayMusic':3160555914
 'AudioEventList_activeProbe_activeProbe_play':320379408
 'AudioEventList_activeProbe_activeProbe_priming_off':2099832552
 'AudioEventList_activeProbe_activeProbe_priming_on':2307477490
 'AudioEventList_activeProbe_activeProbe_stop':2963931826
 'AudioEventList_ui_ui_action_generic':1906840602
 'AudioEventList_ui_ui_action_gunnery':1191555991
 'AudioEventList_ui_ui_action_guts':991696128
 'AudioEventList_ui_ui_action_jump':1891400627
 'AudioEventList_ui_ui_action_notavailable':1202227231
 'AudioEventList_ui_ui_action_observation':747158411
 'AudioEventList_ui_ui_action_piloting':4065118337
 'AudioEventList_ui_ui_action_sprint':1398548603
 'AudioEventList_ui_ui_callout_inspired_buff':1400305465
 'AudioEventList_ui_ui_callout_toast':3658236246
 'AudioEventList_ui_ui_ecm_buff_down':1897676388
 'AudioEventList_ui_ui_ecm_buff_up':3808587679
 'AudioEventList_ui_ui_ecm_start':2551148966
 'AudioEventList_ui_ui_ecm_stop':4153254630
 'AudioEventList_ui_ui_esc_menu_hover':2866688670
 'AudioEventList_ui_ui_esc_menu_in':1920893261
 'AudioEventList_ui_ui_esc_menu_out':2402590420
 'AudioEventList_ui_ui_esc_menu_select':4034409072
 'AudioEventList_ui_ui_generic_confirm':390458608
 'AudioEventList_ui_ui_generic_hover':88994342
 'AudioEventList_ui_ui_mech_action_choose_yes':3970896206
 'AudioEventList_ui_ui_mech_action_hover':4247886413
 'AudioEventList_ui_ui_mech_choose_hover':1056171268
 'AudioEventList_ui_ui_mech_choose_off':3666879309
 'AudioEventList_ui_ui_mech_choose_on':4090541825
 'AudioEventList_ui_ui_mech_move':2538919975
 'AudioEventList_ui_ui_mech_move_path':2921029031
 'AudioEventList_ui_ui_mech_move_path_confirm':1156764138
 'AudioEventList_ui_ui_mech_move_rotate_start':3024088466
 'AudioEventList_ui_ui_mech_move_rotate_stop':3255711818
 'AudioEventList_ui_ui_mech_restart':2386294337
 'AudioEventList_ui_ui_mission_done':3192677011
 'AudioEventList_ui_ui_mission_fail':1911186247
 'AudioEventList_ui_ui_mission_popup_off':2686083129
 'AudioEventList_ui_ui_mission_popup_on':1450546573
 'AudioEventList_ui_ui_mission_withdraw':3881139189
 'AudioEventList_ui_ui_mp_chat_alert':879273697
 'AudioEventList_ui_ui_mp_go_to_mech_select':105996637
 'AudioEventList_ui_ui_mp_menu_hover':427470178
 'AudioEventList_ui_ui_mp_select_go':2015535309
 'AudioEventList_ui_ui_mp_select_mech_value_ok':2576795435
 'AudioEventList_ui_ui_mp_select_mech_value_over':3509850199
 'AudioEventList_ui_ui_objective_add':4069001851
 'AudioEventList_ui_ui_objective_done':1663464438
 'AudioEventList_ui_ui_objective_fail':2399597118
 'AudioEventList_ui_ui_overheat_alarm_1':3175092196
 'AudioEventList_ui_ui_overheat_alarm_2':3175092199
 'AudioEventList_ui_ui_overheat_alarm_3':3175092198
 'AudioEventList_ui_ui_overheat_imminent':2078777640
 'AudioEventList_ui_ui_overheat_shutdown_imminent':1337005591
 'AudioEventList_ui_ui_panels_down':2297788666
 'AudioEventList_ui_ui_panels_up':3780452249
 'AudioEventList_ui_ui_phase_1':3039138271
 'AudioEventList_ui_ui_phase_turn_me':958989884
 'AudioEventList_ui_ui_phase_turn_you':835085243
 'AudioEventList_ui_ui_radar_blip_detected':4157967717
 'AudioEventList_ui_ui_radar_blip_moving':2331000673
 'AudioEventList_ui_ui_salvage_received':4267392257
 'AudioEventList_ui_ui_settings_menu_check':1088701156
 'AudioEventList_ui_ui_settings_menu_uncheck':2948342627
 'AudioEventList_ui_ui_sim_back':1667154735
 'AudioEventList_ui_ui_sim_event_popup':2440455941
 'AudioEventList_ui_ui_sim_menu_appear':4029002589
 'AudioEventList_ui_ui_sim_menu_hover':116313428
 'AudioEventList_ui_ui_sim_menu_select':2274902470
 'AudioEventList_ui_ui_sim_object_hover':3103349592
 'AudioEventList_ui_ui_sim_object_select':4106159914
 'AudioEventList_ui_ui_sim_pilot_pic_appear':1878799779
 'AudioEventList_ui_ui_sim_platform_start':3223757106
 'AudioEventList_ui_ui_sim_platform_stop':1826771818
 'AudioEventList_ui_ui_sim_popup_newChassis':2997968017
 'AudioEventList_ui_ui_sim_rewardbox1':1996520511
 'AudioEventList_ui_ui_sim_rewardbox2':1996520508
 'AudioEventList_ui_ui_sim_submenu_appear':317544439
 'AudioEventList_ui_ui_sim_submenu_hover':3211003714
 'AudioEventList_ui_ui_sim_travel_loop_play':4185281064
 'AudioEventList_ui_ui_sim_travel_loop_stop':2267984026
 'AudioEventList_ui_ui_sim_travel_ping_play':2496623122
 'AudioEventList_ui_ui_sim_whoosh_room_change':961970741
 'AudioEventList_ui_ui_sim_whoosh_zoom':3648784138
 'AudioEventList_ui_ui_target_cycling':3846211843
 'AudioEventList_ui_ui_target_lock_bracket':2369329404
 'AudioEventList_ui_ui_target_lock_bracket_last':3689647655
 'AudioEventList_ui_ui_target_lock_hard':3520700967
 'AudioEventList_ui_ui_target_lock_soft':3537318368
 'AudioEventList_ui_ui_target_rotate_start':1279084164
 'AudioEventList_ui_ui_target_rotate_stop':1546761784
 'AudioEventList_ui_ui_target_sensor_lock_hard':796565048
 'AudioEventList_ui_ui_target_sensor_lock_soft':556931275
 'AudioEventList_ui_ui_target_sensor_lock_soft_off':3555642237
 'AudioEventList_ui_ui_target_sensor_sweep_start':884067730
 'AudioEventList_ui_ui_target_sensor_sweep_stop':1182849098
 'AudioEventList_ui_ui_weapon_choose_yes':378852106
 'AudioEventList_ui_ui_weapon_destroyed':4265165438
 'AudioEventList_ui_ui_weapon_disabled':3966917441
 'AudioEventList_ui_ui_weapon_hover':1761074433
 'AudioEventList_breakable_breakable_building_damage':1713355867
 'AudioEventList_breakable_breakable_concrete':2984704776
 'AudioEventList_breakable_breakable_concrete_barrier':3511346272
 'AudioEventList_breakable_breakable_concrete_large':495359612
 'AudioEventList_breakable_breakable_concrete_medium':2611577842
 'AudioEventList_breakable_breakable_concrete_small':2888588100
 'AudioEventList_breakable_breakable_dumpster':1423471327
 'AudioEventList_breakable_breakable_fence':3548602884
 'AudioEventList_breakable_breakable_fence_large':2368537064
 'AudioEventList_breakable_breakable_fence_medium':4169498886
 'AudioEventList_breakable_breakable_fence_small':749351936
 'AudioEventList_breakable_breakable_glass':387806267
 'AudioEventList_breakable_breakable_lightpole':2386213473
 'AudioEventList_breakable_breakable_metal':3490160970
 'AudioEventList_breakable_breakable_metal_large':1400066202
 'AudioEventList_breakable_breakable_metal_medium':2988863460
 'AudioEventList_breakable_breakable_metal_small':974947462
 'AudioEventList_breakable_breakable_radio_tower':1182306552
 'AudioEventList_breakable_breakable_vehicle':1201005715
 'AudioEventList_breakable_breakable_vehicle_fiery':2542997389
 'AudioEventList_collapse_collapse_large':3593681920
 'AudioEventList_collapse_collapse_large_fiery':1217697990
 'AudioEventList_collapse_collapse_large_fiery_tall':2836885728
 'AudioEventList_collapse_collapse_medium':510637070
 'AudioEventList_collapse_collapse_medium_fiery':1049034760
 'AudioEventList_collapse_collapse_short':740736451
 'AudioEventList_collapse_collapse_short_fiery':1962510813
 'AudioEventList_collapse_collapse_tiny':3377052157
 'AudioEventList_collapse_collapse_tiny_fiery':1350155819
 'AudioEventList_ecm_ecm_enter':855028813
 'AudioEventList_ecm_ecm_exit':1702294241
 'AudioEventList_explosion_explosion_coolant':1442258229
 'AudioEventList_explosion_explosion_electrical':2710565687
 'AudioEventList_explosion_explosion_large':2588735442
 'AudioEventList_explosion_explosion_medium':4165830412
 'AudioEventList_explosion_explosion_propane_tank':3916379071
 'AudioEventList_explosion_explosion_small':604083038
 'AudioEventList_fire_fire_large_180seconds':1928250444
 'AudioEventList_fire_fire_large_start':3618729104
 'AudioEventList_fire_fire_large_stop':1112110460
 'AudioEventList_fire_fire_medium_180seconds':160877140
 'AudioEventList_fire_fire_medium_start':211675768
 'AudioEventList_fire_fire_medium_stop':3138909316
 'AudioEventList_fire_fire_small_180seconds':1972692740
 'AudioEventList_fire_fire_small_start':788625640
 'AudioEventList_fire_fire_small_stop':2935850420
 'AudioEventList_impact_impact_weapon':1378694922
 'AudioEventList_small_small_building_collapse_large':1794037989
 'AudioEventList_small_small_building_collapse_med':174697090
 'AudioEventList_small_small_building_collapse_small':2154267453
 'AudioEventList_small_small_building_collapse_tiny':1798116218
 'AudioEventList_ac10_ac10_auto_single':1271390687
 'AudioEventList_ac10_ac10_auto_start':2794484601
 'AudioEventList_ac10_ac10_auto_stop':4142991059
 'AudioEventList_ac10_ac10_cannon':2644713222
 'AudioEventList_ac2_ac2_shot':1450394644
 'AudioEventList_ac20_ac20_auto_single':3029130770
 'AudioEventList_ac20_ac20_auto_start':1587432538
 'AudioEventList_ac20_ac20_auto_stop':1176261874
 'AudioEventList_ac20_ac20_cannon':580791825
 'AudioEventList_ac5_ac5_1stand2ndshot':2549964306
 'AudioEventList_ac5_ac5_3rdshot':1842726030
 'AudioEventList_flamer_flamer_start':328273805
 'AudioEventList_flamer_flamer_stop':2748237391
 'AudioEventList_gauss_gauss_chargeup':2917197164
 'AudioEventList_gauss_gauss_shoot':2452532288
 'AudioEventList_laser_laser_beam_stop_large':3209843651
 'AudioEventList_laser_laser_beam_stop_medium':2599849911
 'AudioEventList_laser_laser_beam_stop_small':3831089487
 'AudioEventList_laser_laser_large':4048453998
 'AudioEventList_laser_laser_medium':136592768
 'AudioEventList_laser_laser_small':3760557578
 'AudioEventList_lrm_lrm_launcher_end':607827825
 'AudioEventList_lrm_lrm_launcher_start':4237551394
 'AudioEventList_lrm_lrm_missile_launch':1647457025
 'AudioEventList_lrm_lrm_missile_launch_last':1762108332
 'AudioEventList_lrm_lrm_projectile_start':3368411099
 'AudioEventList_lrm_lrm_projectile_stop':2665274041
 'AudioEventList_machine_machine_gun_start':3916112878
 'AudioEventList_machine_machine_gun_stop':1663795150
 'AudioEventList_ppc_ppc_shoot':1071375452
 'AudioEventList_pulse_pulse_lrg_chargeup':383447416
 'AudioEventList_pulse_pulse_lrg_shoot':971720980
 'AudioEventList_pulse_pulse_med_chargeup':736367701
 'AudioEventList_pulse_pulse_med_shoot':3438267387
 'AudioEventList_pulse_pulse_sml_chargeup':4041000047
 'AudioEventList_pulse_pulse_sml_shoot':745217
 'AudioEventList_srm_srm_launcher_end':2830936084
 'AudioEventList_srm_srm_launcher_start':2788752519
 'AudioEventList_srm_srm_missile_launch':2876955656
 'AudioEventList_srm_srm_missile_launch_last':732096931
 'AudioEventList_srm_srm_projectile_start':766570538
 'AudioEventList_srm_srm_projectile_stop':2537716994