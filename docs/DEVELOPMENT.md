# Temple of Echoes --- Development Guide

## 1. Development order

The game will be developed in controlled milestones.

### Milestone 1 --- Health

-   Inspect Universal Health System
-   Identify the stats component
-   Connect health to the existing third-person player
-   Display player health
-   Test damage
-   Test healing
-   Test death
-   Test respawn/save behavior where required

### Milestone 2 --- Combat

-   Inspect the existing Combat variant
-   Integrate combat into the main third-person player
-   Connect attacks to damage
-   Connect enemy health to the universal system
-   Add enemy death
-   Test hit detection

### Milestone 3 --- Enemy AI

-   Inspect the existing enemy implementation
-   Establish navigation correctly
-   Implement chase behavior
-   Implement stopping distance
-   Implement attack range
-   Implement attack cooldown
-   Prevent enemies from sinking into the level
-   Test movement before adding more AI complexity

### Milestone 4 --- Healing and pickups

-   Integrate `BP_HP_Potion`
-   Decide whether healing is immediate or inventory-based
-   Connect pickup events to the universal health/stat system
-   Add UI feedback

### Milestone 5 --- Platforming

-   Integrate platforming movement/features into the main player
-   Keep one player architecture
-   Test transitions between exploration, combat and platforming

### Milestone 6 --- Side-scroller sections

-   Integrate side-scroller gameplay as a level/section feature
-   Avoid creating a separate permanent player unless required
-   Define camera and movement rules per level

### Milestone 7 --- Levels

The project currently has three levels/variant areas to develop.

Each level should clearly document:

-   Player start
-   Objective
-   Enemies
-   Pickups
-   Hazards
-   Checkpoints
-   Exit/transition
-   Required systems

### Milestone 8 --- Mobile

Only after the core game is stable:

-   Android input
-   Touch controls
-   UI scaling
-   Performance profiling
-   Texture/material optimization
-   Packaging
-   Device testing

## 2. Blueprint rules

### Rule A --- Inspect before changing

Before creating a Blueprint:

1.  Search the Content Browser.
2.  Check whether Unreal already provides the required system.
3.  Check whether the Fab health system already provides the feature.
4.  Reuse an existing system where practical.

### Rule B --- One source of truth

Health should have one authoritative implementation.

Do not maintain separate:

-   `PlayerHealth`
-   `EnemyHealth`
-   `CombatHealth`
-   `PotionHealth`

variables that can become inconsistent.

Instead, use the Universal Health System as the health/stat authority
after its API is understood.

### Rule C --- Test one system at a time

Do not build several interconnected systems before testing the first
one.

Recommended sequence:

``` text
Health
↓
Damage
↓
Healing
↓
Death
↓
Combat
↓
Enemy AI
↓
HUD
```

### Rule D --- Avoid unnecessary Event Tick

`Event Tick` should not be used for logic that can be event-driven.

Prefer:

-   Events
-   Timers
-   Overlap events
-   Input events
-   Animation notifies
-   AI tasks/services where appropriate

This is especially important for mobile performance.

## 3. Testing checklist

After each major Blueprint change:

-   Compile
-   Save
-   Start PIE
-   Test the intended behavior
-   Test the failure case
-   Check Output Log
-   Check for Blueprint warnings/errors
-   Stop PIE
-   Save again

### Example: health test

``` text
Initial health
      ↓
Take damage
      ↓
Health decreases
      ↓
Take additional damage
      ↓
Health reaches zero
      ↓
Death behavior
      ↓
Heal/revive behavior if supported
```

## 4. Documentation rule

Whenever a system is completed, document:

-   Blueprint name
-   Location
-   Purpose
-   Variables
-   Events
-   Functions
-   Interfaces
-   Dependencies
-   How it is tested
-   Known limitations

This makes the project easier to debug later.
