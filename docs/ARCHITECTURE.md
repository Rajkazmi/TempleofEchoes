# Temple of Echoes --- Architecture

## Goal

The project should behave as one game even though it contains multiple
Unreal template variants.

## High-level architecture

``` text
                    Temple of Echoes
                           |
             +-------------+-------------+
             |             |             |
          Player         World        UI/Systems
             |             |             |
       +-----+-----+       |       +-----+------+
       |           |       |       |            |
    Movement     Combat   Levels   Health       HUD
       |           |       |       |            |
       +-----------+-------+-------+------------+
                           |
                     Game Rules / Save
```

## Player architecture

The preferred architecture is one main third-person player.

The player should gradually gain:

-   Exploration movement
-   Combat
-   Platforming abilities
-   Required side-scroller behavior
-   Health
-   Damage response
-   Healing
-   UI interaction

Variant-specific behavior should be enabled where required rather than
creating multiple unrelated player characters.

## Health architecture

The imported Universal Health System is the current candidate for the
health/stat authority.

Known assets include:

``` text
UniversalHealthSystem/
└── Blueprints/
    ├── BP_PlayerCharacter
    ├── BP_SaveGame
    ├── BP_ItemsSpawner
    ├── Components/
    │   └── BP_Stats_Component
    ├── Items/
    │   ├── BP_HP_Potion
    │   ├── BP_MP_Potion
    │   ├── BP_EnergyWater
    │   └── BP_Items_Master
    └── UI/
        ├── W_MainWidget
        ├── W_PlayerStats_Widget
        ├── W_StatsPanel_1
        ├── W_StatsPanel_2
        └── W_StatsPanel_2_Slot
```

The exact API and intended integration points must be verified in Unreal
before implementation.

## Combat architecture

Combat should produce a damage request.

Conceptually:

``` text
Attack
  ↓
Hit detection
  ↓
Target validation
  ↓
Damage request
  ↓
Target health/stat system
  ↓
Health changed
  ↓
HUD / reaction / death
```

Combat should not directly maintain a second copy of target health.

## Enemy architecture

Enemies should have:

``` text
Enemy Character
    |
    +-- Movement
    +-- Navigation
    +-- Combat
    +-- Health
    +-- Death
```

AI behavior should be event/state driven where possible.

Do not use continuous Tick logic when an event, timer, AI task or state
transition can perform the same job.

## Level architecture

The three gameplay variants should be treated as gameplay capabilities
and/or level-specific experiences.

A level should define:

-   Gameplay mode
-   Camera behavior
-   Movement rules
-   Enemy encounters
-   Hazards
-   Objectives
-   Checkpoints
-   Transitions

## Save architecture

The imported `BP_SaveGame` should be inspected before adding another
save system.

Save data should eventually cover only the information that needs
persistence, such as:

-   Player progress
-   Health/state when appropriate
-   Inventory
-   Level/checkpoint
-   Objectives
-   Unlocks

## Mobile architecture

Android is a target platform, but mobile optimization should happen
throughout development.

Avoid unnecessarily expensive:

-   Tick logic
-   high-frequency traces
-   excessive particles
-   unnecessary dynamic material updates
-   large texture memory
-   duplicate actors
-   unnecessary AI calculations

## Dependency rule

Before replacing or duplicating a system, document why the existing
system cannot be reused.

This keeps the project maintainable and reduces Blueprint conflicts.
