# Temple of Echoes

A third-person action-adventure game built with Unreal Engine.

## Project status

**Current development branch:** `feature/health-system`

The repository contains the Unreal project and the imported Universal
Health System from Fab. The project also contains Unreal's template
variants that we plan to combine into the main third-person experience.

### Current template content

-   `Characters`
-   `Input`
-   `Level Prototype`
-   `ThirdPerson`
-   `Variant_Combat`
-   `Variant_Platforming`
-   `Variant_SideScroller`
-   `UniversalHealthSystem`

## Game direction

Temple of Echoes is being developed as a third-person game that
combines:

-   Third-person exploration and movement
-   Combat
-   Platforming
-   Side-scroller sections
-   Universal player/enemy health
-   Damage and healing
-   Enemy encounters
-   HUD and gameplay UI
-   Multiple levels
-   Android/mobile support

The goal is to integrate these systems into one consistent player
experience rather than maintaining separate player implementations for
each template variant.

## Core development principle

Use existing Unreal Engine template systems and the imported Universal
Health System where practical.

Avoid creating duplicate:

-   Player characters
-   Health systems
-   Damage systems
-   Movement systems
-   HUD systems

unless the existing systems cannot satisfy a required feature.

## Repository structure

``` text
TempleofEchoes/
├── Config/
├── Content/
│   ├── Characters/
│   ├── Input/
│   ├── Level Prototype/
│   ├── ThirdPerson/
│   ├── Variant_Combat/
│   ├── Variant_Platforming/
│   ├── Variant_SideScroller/
│   └── UniversalHealthSystem/
├── Documentation/
├── .gitattributes
├── .gitignore
└── TempleofEchoes.uproject
```

## Universal Health System

The imported health system currently includes assets such as:

-   `BP_PlayerCharacter`
-   `BP_Stats_Component`
-   `BP_HP_Potion`
-   `BP_Items_Master`
-   `BP_ItemsSpawner`
-   `BP_SaveGame`
-   `W_MainWidget`
-   `W_PlayerStats_Widget`
-   `W_StatsPanel_1`
-   `W_StatsPanel_2`
-   `Showcase.umap`

The system should be inspected and integrated into the existing
third-person player rather than blindly replacing the template player.

## Development workflow

Work on feature branches.

``` text
main
└── develop
    └── feature/<feature-name>
```

Current feature:

``` text
feature/health-system
```

For every major feature:

1.  Make a small change.
2.  Compile in Unreal Engine.
3.  Play-test.
4.  Fix errors.
5.  Save the project.
6.  Commit the working state.
7.  Push to GitHub.
8.  Continue to the next feature.

## Unreal generated files

Generated folders such as `Saved/`, `Intermediate/`,
`DerivedDataCache/`, `Binaries/`, and build output should remain ignored
by Git.

Large Unreal binary assets such as `.uasset` and `.umap` are intended to
use Git LFS.

## Current next milestone

Integrate and test the Universal Health System with the existing
third-person player.

See:

-   [Development Guide](docs/DEVELOPMENT.md)
-   [Architecture](docs/ARCHITECTURE.md)
-   [Git Workflow](docs/GIT-WORKFLOW.md)
