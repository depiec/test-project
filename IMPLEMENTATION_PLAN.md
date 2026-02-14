# DYNASTY OF SOULS - Implementation Plan

**Version**: 1.0  
**Date**: February 14, 2026  
**Game Engine**: Godot 4.6+  
**Project Type**: 2D Action RPG / Dungeon Management  
**Genre**: Overlord-inspired Action RPG with strategic elements

---

## TABLE OF CONTENTS

1. [Executive Summary](#1-executive-summary)
2. [Tech Stack & Architecture](#2-tech-stack-architecture)
3. [Project Structure Setup](#3-project-structure-setup)
4. [Asset Requirements & Pipeline](#4-asset-requirements--pipeline)
5. [Implementation Priority Roadmap](#5-implementation-priority-roadmap)
6. [Phase-by-Phase Development Plan](#6-phase-by-phase-development-plan)
7. [Technical Architecture Details](#7-technical-architecture-details)
8. [Database & System Schema](#8-database--system-schema)
9. [Asset Breakdown by System](#9-asset-breakdown-by-system)
10. [Save System Design](#10-save-system-design)
11. [Performance Optimization](#11-performance-optimization)
12. [Balancing & Difficulty](#12-balancing--difficulty)
13. [Testing Strategy](#13-testing-strategy)
14. [Deliverables & Milestones](#14-deliverables--milestones)
15. [Development Timeline Estimates](#15-development-timeline-estimates)

---

## 1. EXECUTIVE SUMMARY

### Game Overview
**DYNASTY OF SOULS** is a 2D Action RPG where players guide an undead skeleton lord as they build a dungeon fortress, gather armies, conquer territories, and navigate complex social systems. The game combines fast-paced combat with strategic dungeon management, featuring deep character progression, tactical army battles, and dynamic NPC interactions.

### Core Game Loop
1. **Exploration** - Travel through world regions, gather resources
2. **Combat** - Engage enemies in action combat, gain experience
3. **Dungeon Building** - Construct and expand your fortress
4. **Army Management** - Train and command undead forces
5. **Progression** - Level up character, unlock abilities, gather loot
6. **Guild Quests** - Complete missions through NPCs and armies
7. **Conquest** - Expand influence through tactical battles

### Development Approach
- Agile methodology with 2-week sprints
- Phased implementation with clear deliverables
- Priority on core gameplay loop first
- Iterative refinement of systems
- Continuous integration and testing

---

## 2. TECH STACK & ARCHITECTURE

### Engine & Tools
- **Game Engine**: Godot 4.6+ (GDScript + C#)
- **Graphics 2D**: Godot's CanvasItem system with Pixel shaders
- **Audio**: Godot's AudioStreamPlayer and Audio buses
- **Physics**: Physics2D system with Raycasting
- **Save System**: Godot SaveFile API
- **UI Framework**: Custom Control nodes with signal-based architecture

### Programming Languages
- **Primary**: GDScript 4.x
- **Performance Critical**: Mixed C# (for complex calculations)
- **Data**: JSON for configuration files
- **Storage**: SQLite for persistent data (optional for PC release)

### Core Framework Patterns

#### State Machine Pattern
```gdscript
# Core state management
enum GameState {
    MENU,           // Main menu, game selection
    WORLD_MAP,      // World exploration
    DUNGEON_VIEW,   // Dungeon building and management
    COMBAT,         // Active combat
    DIALOGUE,       // NPC interactions
    TACTICAL,       // Army battles
    GUILD,          // Quest management
    INVENTORY,      // Item management
    SETTINGS        // Configuration
}
```

#### Entity-Component Pattern
```gdscript
# Core entity architecture
class_name Entity
signal entity_changed(entity: Entity)
signal entity_died(entity: Entity)

var id: int
var type: EntityType
var position: Vector2
var components: Dictionary
var state: EntityState

func add_component(component: Component) -> void
func get_component(type: ComponentType) -> Component
func has_component(type: ComponentType) -> bool
func update(delta: float) -> void
```

#### Signal-Based Communication
```gdscript
# Core event system
class_name EventBus

signal player_died
signal player_respawned
signal enemy_spawned(enemy: Enemy)
signal dungeon_cleared(dungeon: Dungeon)
signal inventory_updated
signal quest_completed
signal army_deployed
signal faction_reputation_changed(faction: Faction, change: float)
```

### System Architecture

#### Core Systems Tree
```
GameRoot
├── StateManager (Game state management)
├── WorldManager (World and locations)
├── PlayerManager (Player entity)
├── CombatSystem (Combat mechanics)
├── DungeonSystem (Dungeon builder)
├── ArmySystem (Army management)
├── GuildSystem (Quest management)
├── InventorySystem (Items and equipment)
├── EconomySystem (Trading and resources)
├── NPCSystem (NPCs and AI)
├── SaveSystem (Persistence)
├── UISystem (UI management)
└── AudioManager (Sound and music)
```

---

## 3. PROJECT STRUCTURE SETUP

### Godot Project Structure
```
dynasty-of-souls/
├── project.godot               # Project configuration
├── README.md                    # Project documentation
├── AGENTS.md                    # Development guidelines
├── IMPLEMENTATION_PLAN.md      # This document
├── assets/                      # Main asset directory
│   ├── sprites/                 # Pixel art sprites
│   │   ├── characters/         # Player and NPC sprites
│   │   ├── enemies/            # Enemy sprites
│   │   ├── items/              # Item icons and sprites
│   │   ├── tiles/              # Map tiles and textures
│   │   └── particles/          # Particle effects
│   ├── sounds/                 # Audio files
│   │   ├── music/              # Background music
│   │   ├── sfx/                # Sound effects
│   │   └── voice/              # Voice actors
│   ├── ui/                     # UI design elements
│   │   ├── sprites/            # UI button icons
│   │   └── layouts/            # UI scene files
│   └── fonts/                  # Font files
├── resources/                   # Script-based resources
│   ├── item_data.gd           # Item data structure
│   ├── enemy_data.gd          # Enemy data structure
│   ├── level_data.gd          # Level configuration
│   ├── ability_data.gd        # Ability templates
│   └── npc_templates.gd       # NPC templates
├── scenes/                      # Godot scenes
│   ├── main/                   # Main game scene
│   │   ├── main_menu.tscn
│   │   ├── world_map.tscn
│   │   └── game_session.tscn
│   ├── player/                 # Player scenes
│   │   ├── player.tscn
│   │   ├── player_controller.gd
│   │   └── player_stats.gd
│   ├── world/                  # World scenes
│   │   ├── world_map.tscn
│   │   ├── region*.tscn
│   │   └── locations/
│   ├── dungeon/                # Dungeon scenes
│   │   ├── dungeon_base.tscn
│   │   ├── dungeon_builder.gd
│   │   └── room_templates/
│   ├── combat/                 # Combat scenes
│   │   ├── enemy.tscn
│   │   ├── combat_system.gd
│   │   └── combat_ui.tscn
│   ├── ui/                     # UI scenes
│   │   ├── character_panel.tscn
│   │   ├── inventory.tscn
│   │   ├── dialogue_box.tscn
│   │   └── guild_panel.tscn
│   └── systems/                # System manager scenes
│       └── system_manager.tscn
├── scripts/                    # Main game scripts
│   ├── core/                   # Core systems
│   │   ├── state_manager.gd
│   │   ├── event_bus.gd
│   │   └── entity.gd
│   ├── systems/                # Game systems
│   │   ├── player_system.gd
│   │   ├── combat_system.gd
│   │   ├── dungeon_system.gd
│   │   ├── army_system.gd
│   │   ├── guild_system.gd
│   │   ├── inventory_system.gd
│   │   ├── economy_system.gd
│   │   └── npc_system.gd
│   └── ui/                     # UI scripts
│       └── ui_manager.gd
└── data/                       # Game data and configuration
    ├── save_data.gd           # Save data structure
    ├── game_config.gd         # Game balance data
    └── world_data.gd          # World content data
```

### Initialization Files

#### project.godot
```toml
config_version=5

[application]
config/name="Dynasty of Souls"
run/main_scene="res://scenes/main/game_session.tscn"
config/features=PackedStringArray("4.6.2", "Godot Engine 4.6.2.stable")
config/icon="res://icon.svg"

[autoload]
Global=$"res://scripts/core/global.gd"
EventBus=$"res://scripts/core/event_bus.gd"
SaveSystem=$"res://scripts/systems/save_system.gd"

[rendering]
quality/driver/fallbacks/discard_enabled=true
quality/driver/alpha_to_coverage_enabled=false
quality/driver/skip_swap_buffers=true
```

---

## 4. ASSET REQUIREMENTS & PIPELINE

### Asset Categories & Priority

#### PRIORITY 1: Core Gameplay Assets (Weeks 1-4)
- **Player Character**
  - Idle animation sprites (8 directions)
  - Walk animation sprites (8 directions)
  - Combat animation sprites (attack, block, dodge)
  - Dual-stance character sprites (caster/warrior)
  - Equipment override sprites
- **Basic Enemies**
  - Skeleton warrior sprites (idle, walk, attack)
  - Basic enemy AI sprites
  - Health bars and damage feedback

#### PRIORITY 2: UI Elements (Weeks 2-5)
- Main menu interface
- Health/energy/stamina HUD
- Inventory grid system
- Character stats panel
- Quest tracking panel
- Dialogue box
- Combat abilities bar

#### PRIORITY 3: World & Environment (Weeks 3-8)
- World map background
- Region distinct backgrounds
- Tile set for dungeon builder
- Floor textures and walls
- Decorative dungeon elements
- Lighting effects and particles

#### PRIORITY 4: Audio (Weeks 2-6)
- Background music tracks for different regions
- Combat sound effects (hits, deaths, spells)
- Menu and UI sounds
- NPC voice samples
- Ambient dungeon sounds

### Asset Pipeline Requirements

#### Graphics Setup
- **Resolution**: 1920x1080 for gameplay, 512x512 for pixel art
- **Format**: PNG (with transparency)
- **Animation Frames**: At least 3-4 frames per animation state
- **Color Palette**: Separate palette files for different character types

#### Audio Structure
- **Music**: OGG format, 2-3 min tracks per region
- **SFX**: WAV or OGG format, short burst sounds
- **Voice**: WAV format, clear and distinct
- **Formats**: Normalize volume levels (±3dB)

### Asset Creation Tools
- **Pixel Art**: Aseprite or Krita
- **Animation**: Aseprite with onion skinning
- **Audio**: Audacity for editing
- **UI Design**: Figma or GIMP
- **Vector Assets**: Inkscape for icons and UI elements

---

## 5. IMPLEMENTATION PRIORITY ROADMAP

### Phased Approach Overview

```
PHASE 1: CORE FOUNDATION (Weeks 1-6) → Prototype + Core Loop
PHASE 2: EXPLORATION & COMBAT (Weeks 4-12) → World + Basic Combat
PHASE 3: DUNGEON BUILDING (Weeks 8-16) → Dungeon Builder System
PHASE 4: ARMY SYSTEM (Weeks 12-20) → Tactical Army Battles
PHASE 5: GUILD & PROGRESSION (Weeks 14-24) → Quests + NPC Systems
PHASE 6: FINAL POLISH (Weeks 20-26) → Content + Optimization
```

### Core Systems Build Order

#### Build Block 1: Core Engine (Week 1-2)
1. Project setup and structure
2. Basic input system (WASD + Mouse)
3. Camera following system (third-person top-down)
4. State machine framework
5. Event bus for component communication

#### Build Block 2: Player Movement (Week 2-3)
6. Character movement implementation
7. Speed and acceleration systems
8. Player stats and HUD
9. Health, stamina, mana systems
10. Basic character animation

#### Build Block 3: Basic Combat (Week 3-5)
11. Enemy AI basic behavior
12. Attack hitboxes and collision
13. Player combat abilities
14. Damage calculation system
15. Combat feedback and visual effects

#### Build Block 4: World Exploration (Week 4-8)
16. World map and region system
17. Location markers and navigation
18. Walking and travel mechanics
19. Basic NPC interaction
20. Quest tracking system

#### Build Block 5: Inventory System (Week 5-9)
21. Item data structure
22. Inventory UI and grid system
23. Equipment slots and stats
24. Item equipping logic
25. Basic loot system

#### Build Block 6: Dungeon Builder (Week 8-16)
26. Grid-based map system
27. Room placement mechanics
28. Building resources
29. Dungeon construction UI
30. Player home base building

#### Build Block 7: Army System (Week 12-20)
31. Army data structure
32. Unit types and stats
33. Army roster management
34. Tactical view interface
35. Basic army combat simulation

#### Build Block 8: Guild System (Week 14-24)
36. NPC quest system
37. Task issuance and tracking
38. NPC abilities and AI
39. Guild quest rewards
40. Faction reputation system

#### Build Block 9: Final Polish (Week 20-26)
41. Advanced combat mechanics
42. Dungeon expansion and upgrades
43. Trading and economy
44. Save/load system
45. Performance optimization
46. Content completion

---

## 6. PHASE-BY-PHASE DEVELOPMENT PLAN

### PHASE 1: CORE ENGINE SETUP & NAVIGATION
**Duration**: 6 weeks  
**Goal**: Functional prototype with movement and basic combat

#### Week 1: Project Foundation
- [ ] Initialize Godot 4.6+ project
- [ ] Create project structure and folders
- [ ] Set up autoload systems (Global, EventBus)
- [ ] Configure input actions (WASD, mouse, escape)
- [ ] Set camera default behavior
- [ ] Create basic test scene

#### Week 2: Player Movement
- [ ] Implement character movement system
- [ ] Add acceleration and speed tuning
- [ ] Camera follow implementation
- [ ] Character animation states
- [ ] Player stats system (HP, stamina, mana)
- [ ] Basic HUD implementation

#### Week 3: Basic Combat - Player Side
- [ ] Attack input handling
- [ ] Hitbox and damage system
- [ ] Combo system foundation
- [ ] Player combat animations
- [ ] Stamina resource management
- [ ] Basic enemy spawner

#### Week 4: Basic Combat - Enemy System
- [ ] Enemy AI basic movement
- [ ] Enemy states (idle, patrol, chase, attack)
- [ ] Enemy health and damage system
- [ ] Combat feedback and visual effects
- [ ] Death animations and particle effects
- [ ] Basic loot drops

#### Week 5: World Map System
- [ ] World map background and design
- [ ] Region system and navigation
- [ ] Location markers and paths
- [ ] Travel cost and time
- [ ] First location implementation (Kronos Kingdom)
- [ ] Basic NPC interaction

#### Week 6: Quest System Core
- [ ] Quest data structure and tracking
- [ ] Quest UI panel
- [ ] Main quest line setup
- [ ] Basic quest rewards
- [ ] Quest state management

**Phase 1 Deliverable**: playable character with movement, camera, basic combat against simple AI, world map navigation, and simple quests

---

### PHASE 2: CHARACTER SYSTEM & COMBAT FOUNDATION
**Duration**: 8 weeks  
**Goal**: Complete combat system, character progression, inventory

#### Week 7-8: Advanced Combat
- [ ] Hit detection and collision precision
- [ ] Block and parry mechanics
- [ ] Dodge and counterattack system
- [ ] Skill system framework
- [ ] Mana management and spells
- [ ] Combat encounter variety

#### Week 9-10: Character Progression
- [ ] Level-up system and XP requirements
- [ ] Stat point system
- [ ] Skill tree UI and implementation
- [ ] Ability unlocks and upgrades
- [ ] Equipment stat bonuses
- [ ] Class specialization paths

#### Week 11-12: Character Stats & Skills
- [ ] Full stat calculation system
- [ ] Character class templates
- [ ] Skill implementation (combat, magic, utility)
- [ ] Skill tree system
- [ ] Ability cooldowns and costs
- [ ] Specialization system

#### Week 13-14: Inventory System
- [ ] Item data structure and types
- [ ] Grid-based inventory UI
- [ ] Equipment slots system
- [ ] Item equipping logic
- [ ] Item requirements (levels, stats)
- [ ] Bag size tuning

**Phase 2 Deliverable**: Complete combat system with combos, skills, block/dodge mechanics, full level-up progression, skill trees, and inventory system with equipment slots

---

### PHASE 3: WORLD MAP & EXPLORATION
**Duration**: 8 weeks  
**Goal**: Full world exploration, multiple regions, quest variety

#### Week 15-16: World Map Construction
- [ ] World map design and layout
- [ ] Region distinct backgrounds
- [ ] Multiple locations per region
- [ ] Travel paths and navigation
- [ ] Location types (towns, dungeons, camps)
- [ ] Hidden locations and secrets

#### Week 17-18: Region Content
- [ ] Kronos Kingdom complete content
- [ ] Frostfen Wastes content
- [ ] Weeping Marshlands content
- [ ] Different monster types per region
- [ ] Regional NPCs and interactions
- [ ] Regional quests

#### Week 19-20: Exploration Features
- [ ] Discovery and exploration points
- [ ] Hidden areas and secrets
- [ ] Resource gathering spots
- [ ] Discovery rewards
- [ ] Map discovery system
- [ ] Map markers and navigation

#### Week 21-22: Trading & Economy
- [ ] Shop and vendor system
- [ ] Merchant inventory management
- [ ] Currency and buying system
- [ ] Sell system implementation
- [ ] Market price fluctuations
- [ ] Trading post mechanics

**Phase 3 Deliverable**: Full open world with multiple regions, towns, dungeons, NPCs, shops, trading, and diverse exploration content

---

### PHASE 4: DUNGEON BUILDING SYSTEM
**Duration**: 12 weeks  
**Goal**: Complete dungeon builder with room types and customization

#### Week 23-24: Grid Map System
- [ ] Grid-based map construction
- [ ] Grid size and tile system
- [ ] Room placement mechanics
- [ ] Map size limits
- [ ] Room connection logic
- [ ] Import/export map feature

#### Week 25-26: Room Templates
- [ ] Basic room types (chambers, corridors)
- [ ] Function rooms (training, research, crafting)
- [ ] Special rooms (torture, library, altars)
- [ ] Defensive rooms (barracks, armory, guard)
- [ ] Room size and decoration variations
- [ ] Room cost calculations

#### Week 27-28: Building Resources
- [ ] Resource types and generation
- [ ] Gold production from dungeons
- [ ] Resource gathering mechanisms
- [ ] Building cost system
- [ ] Resource optimization
- [ ] Production management

#### Week 29-30: Dungeon Construction UI
- [ ] Room placement UI
- [ ] Resource display and management
- [ ] Map preview
- [ ] Dungeon floor selection
- [ ] Blueprint system
- [ ] Advanced construction controls

#### Week 31-32: Player Home Base
- [ ] Home base customization
- [ ] NPC housing system
- [ ] Library functionality
- [ ] Altar and ritual areas
- [ ] Training areas
- [ ] Personalization options

#### Week 33-34: Dungeon Complexity
- [ ] Multi-floor dungeon support
- [ ] Floor planning and layout
- [ ] Floor-to-floor connections
- [ ] Dungeon layout variations
- [ ] Dungeon difficulty scaling
- [ ] Dungeon completion rewards

**Phase 4 Deliverable**: Complete dungeon builder with room construction, resource management, home base customization, and multi-floor dungeons

---

### PHASE 5: ARMY MANAGEMENT & TACTICAL VIEW
**Duration**: 12 weeks  
**Goal**: Tactical army battles and military campaign

#### Week 35-36: Army Data Structure
- [ ] Army unit types (infantry, archer, knight)
- [ ] Unit stats and abilities
- [ ] Army composition system
- [ ] Army roster management
- [ ] Unit training and development
- [ ] Army upgrades

#### Week 37-38: Army System
- [ ] Army management UI
- [ ] Unit deployment interface
- [ ] Army statistics and status
- [ ] Army composition presets
- [ ] Army size limits
- [ ] Army reinforcement

#### Week 39-40: Tactical View Interface
- [ ] Tactical camera mode
- [ ] Tactical battlefield
- [ ] Army placement system
- [ ] Movement rules
- [ ] Army formation setup
- [ ] Tactical overlay UI

#### Week 41-42: Army Combat System
- [ ] Tactical combat mechanics
- [ ] Unit AI behavior in battles
- [ ] Combat calculations
- [ ] Area-of-effect abilities
- [ ] Terrain effects
- [ ] Battle outcomes

#### Week 43-44: Military Campaign
- [ ] Territory system
- [ ] Campaign map interface
- [ ] Army deployment on campaign
- [ ] Conquest objectives
- [ ] Enemy army encounters
- [ ] Victory conditions

#### Week 45-46: Army Special Units
- [ ] Elite unit types
- [ ] Special unit abilities
- [ [ ] Army heroes and commanders
- [ ] Army customization
- [ ] Advanced tactical options

**Phase 5 Deliverable**: Full tactical army battle system with multiple unit types, formations, and military campaign mechanics

---

### PHASE 6: GUILD SYSTEM & NPC SYSTEMS
**Duration**: 12 weeks  
**Goal**: Complete quest system, NPCs, guild management

#### Week 47-48: NPC System Core
- [ ] NPC character data structure
- [ ] NPC AI system
- [ ] NPC behavior states
- [ ] NPC interactions
- [ ] NPC levels and abilities
- [ ] NPC skills and talents

#### Week 49-50: NPC Quest System
- [ ] Quest issuance system
- [ ] Quest types and objectives
- [ ] Quest difficulty scaling
- [ ] Quest requirements
- [ ] Quest reward system
- [ ] Quest tracking UI

#### Week 51-52: Guild System
- [ ] Guild data structure
- [ ] Guild ranks and hierarchy
- [ ] Guild quest flow
- [ ] Guild progression
- [ ] Guild benefits and powers
- [ ] Guild political systems

#### Week 53-54: NPC Karma System
- [ ] Karma calculation system
- [ ] Karma sources and values
- [ ] Karma-based NPC relationships
- [ ] Reactions to player actions
- [ ] Reputation tracking
- [ ] Karma effects on quests

#### Week 55-56: Advanced NPC Systems
- [ ] NPC backstories and personalities
- [ ] NPC emotional states
- [ ] NPC loyalty and trust
- [ ] NPC relationship management
- [ ] NPC personal quests
- [ ] NPC voice and dialogue

#### Week 57-58: Guild Quest Variety
- [ ] Main story guild quests
- [ ] Side guild quests
- [ ] Reputation-based quests
- [ ] Guild quest rewards
- [ ] Guild quest difficulty
- [ ] Quest branching

**Phase 6 Deliverable**: Complete NPC system with rich backstories, advanced AI, guild system with rank progression, karma-based interactions, and diverse quest variety

---

### PHASE 7: FINAL POLISH & CONTENT
**Duration**: 12 weeks  
**Goal**: Content completion, optimization, bug fixes

#### Week 59-60: Content Completion
- [ ] Final story quests
- [ ] Secret quests
- [ ] Hidden content unlock
- [ ] Easter eggs and secrets
- [ ] Endgame content
- [ ] Content testing

#### Week 61-62: Combat Refinements
- [ ] Boss combat mechanics
- [ ] Advanced enemy AI
- [ ] Balance tuning
- [ ] Difficulty options
- [ ] Combat feedback polish
- [ ] Visual effects enhancement

#### Week 63-64: Dungeon Content
- [ ] Advanced dungeon enemies
- [ ] Dungeon boss fights
- [ ] Dungeon special encounters
- [ ] Dungeon treasure and rewards
- [ ] Dungeon replay value
- [ ] Dungeon secrets and puzzles

#### Week 65-66: Economy and Trading
- [ ] Black market
- [ ] Trade route system
- [ ] Price optimization
- [ ] Resource scarcity mechanics
- [ ] Market fluctuations
- [ ] Trading rewards

#### Week 67-68: Save System
- [ ] Complete save/load system
- [ ] Quick save functionality
- [ ] Auto-save system
- [ ] Save file migration
- [ ] Save slots management
- [ ] Save corruption handling

#### Week 69-70: Performance Optimization
- [ ] Profiling and bottleneck identification
- [ ] Particle system optimization
- [ ] Memory management
- [ ] Draw calls reduction
- [ ] Physics optimization
- [ ] Frame rate stability

#### Week 71-72: Final Polish
- [ ] Final bug fixes
- [ ] UI and HUD polish
- [ ] Audio finalization
- [ ] Cinematic sequences
- [ ] Accessibility features
- [ ] Ending cutscenes

**Phase 7 Deliverable**: Complete, polished, and optimized game ready for release

---

## 7. TECHNICAL ARCHITECTURE DETAILS

### Core System Architecture

#### State Management System
```gdscript
# Core state management structure
class_name GameStateManager
extends Node

enum GameState {
    MENU_START,
    MENU_MAIN,
    WORLD_EXPLORATION,
    DUNGEON_BUILDER,
    COMBAT_ARENA,
    TACTICAL_BATTLE,
    DIALOGUE_INTERFACE,
    INVENTORY_MENU,
    GUILD_PANEL,
    PAUSE_MENU,
    LOAD_SCREEN,
    SAVE_SCREEN,
    SETTINGS_MENU,
    GAME_OVER,
    CREDITS
}

var current_state: GameState = GameState.MENU_MAIN
var state_transitions: Dictionary = {}
var state_entry_actions: Dictionary
var state_exit_actions: Dictionary

func switch_state(new_state: GameState) -> void
func enter_state(state: GameState) -> void
func exit_state(state: GameState) -> void
func is_in_state(state: GameState) -> bool
```

### Entity System Architecture

#### Main Entity Class
```gdscript
class_name Entity extends Node2D
extends Resource

signal entity_health_changed(current: float, max: float)
signal entity_died(entity: Entity)
signal entity_level_changed(new_level: int, xp_total: int)

# Entity properties
var entity_id: string
var entity_name: String
var entity_type: EntityType
var position: Vector2
var level: int = 1
var xp: int = 0
var max_xp: int = 100

# Stats
var base_stats: Statistics = Statistics.new()
var current_stats: Statistics = Statistics.new()

# Combat
var health: float = 100.0
var max_health: float = 100.0
var energy: float = 100.0
var max_energy: float = 100.0
var stamina: float = 100.0
var max_stamina: float = 100.0

# Components
var components: Dictionary = {}

# Flags
var is_alive: bool = true
var is_boss: bool = false
var is_quest_target: bool = false

# Components
func add_component(component: Component) -> void
func get_component(type: ComponentType) -> Component
func has_component(type: ComponentType) -> bool
func remove_component(type: ComponentType) -> void

# Core functions
func update(delta: float) -> void
func take_damage(amount: float, attacker: Entity = null) -> void
func heal(amount: float) -> void
func die() -> void
func level_up() -> void
```

#### Component System
```gdscript
# Component architecture for entities
class_name Component extends Resource

var owner: Entity = null
var component_type: ComponentType
var enabled: bool = true

func _init(owner_ref: Entity, type: ComponentType): pass
func update(delta: float) -> void
```

#### Component Subtypes
```gdscript
enum ComponentType {
    MOVEMENT,
    COMBAT,
    MAGIC,
    STATS,
    AI,
    INTERACTION,
    DUNGEON,
    ARMY,
    INVENTORY,
    EQUIPMENT,
    TRADING,
    SKILL
}
```

### Combat System Architecture

#### Combat System Core
```gdscript
class_name CombatSystem
extends Node

signal combat_started(combat: Combat)
signal combat_ended(combat: Combat, winner: Entity)
signal damage_dealt(damage_data: DamageData)
signal damage_taken(damage_data: DamageData)

var entities_in_combat: Dictionary
var active_combats: Dictionary
var combat_manager: Dictionary

# Combat types
enum CombatType { MELEE, RANGE, MAGIC, PET }

# Combat configuration
const COMBAT_COOLDOWN: float = 2.0
const DAMAGE_COOLDOWN: float = 0.5
const MAX_STACKED_COMBATANTS: int = 8

func register_entity(entity: Entity) -> void
func unregister_entity(entity: Entity) -> void
func combat_check_attack(attacker: Entity, attack_type: CombatType) -> bool
func perform_attack(attacker: Entity, target: Entity, attack_type: CombatType) -> void
func calculate_damage(attacker: Entity, target: Entity, base_damage: float) -> float
func apply_damage(damage_data: DamageData) -> void
```

### Dungeon System Architecture

#### Dungeon Builder System
```gdscript
class_name DungeonSystem
extends Node

enum RoomType { BASIC, FUNCTIONAL, SPECIAL, DEFENSIVE }

signal dungeon_built(dungeon: Dungeon)
signal room_added(room: Room)

# Global dungeon configuration
var max_floor: int = 5
var base_floor_size: int = 20
var max_rooms_per_floor: int = 10
var building_resources: Dictionary

# Grid-based map
var grid_map: GridMap
var map_size: Vector2i

# Construction tools
func build_dungeon(floor_number: int) -> void
func place_room(room_type: RoomType, position: Vector2i) -> Room
func connect_rooms(room1: Room, room2: Room) -> void
func clear_dungeon(floor_number: int) -> void
func get_room_at_position(position: Vector2i) -> Room
```

### Inventory System Architecture

#### Item & Equipment System
```gdscript
class_name Item extends Resource

enum ItemType {
    WEAPON,
    ARMOR,
    CLOTHING,
    CONSUMABLE,
    MATERIAL,
    QUEST,
    TREASURE
}

enum ItemQuality {
    BASIC,
    UNCOMMON,
    RARE,
    EPIC,
    LEGENDARY
}

var item_id: String
var item_name: String
var item_type: ItemType
var item_quality: ItemQuality
var item_level: int
var required_level: int
var icon_path: String
var description: String
var stack_size: int
var max_stack_size: int = 99

# Stats and bonuses
var stats_bonuses: Dictionary
var requirements: Dictionary

# Properties
var is_equippable: bool = false
var is_stackable: bool = true
var is_unique: bool = false
var is_quest_item: bool = false

# Equipment slots for weapons
var equipment_slot: EquipmentSlot = EquipmentSlot.NONE

func get_weight() -> float
func get_value() -> int
func can_equip(entity: Entity) -> bool
func apply_to_entity(entity: Entity) -> void
func remove_from_entity(entity: Entity) -> void
```

---

## 8. DATABASE & SYSTEM SCHEMA

### Data Organization Structure

#### Core Data Tables

##### Items Table
```sql
CREATE TABLE items (
    item_id TEXT PRIMARY KEY,
    item_name TEXT NOT NULL,
    item_type TEXT NOT NULL,
    item_quality TEXT NOT NULL,
    item_level INTEGER NOT NULL DEFAULT 1,
    required_level INTEGER NOT NULL DEFAULT 1,
    icon_path TEXT,
    description TEXT,
    stack_size INTEGER NOT NULL DEFAULT 1,
    max_stack_size INTEGER NOT NULL,
    stats_bonuses JSON,
    requirements JSON,
    is_equippable INTEGER NOT NULL DEFAULT 0,
    is_stackable INTEGER NOT NULL DEFAULT 1,
    is_unique INTEGER NOT NULL DEFAULT 0,
    is_quest_item INTEGER NOT NULL DEFAULT 0,
    equipment_slot TEXT,
    base_value INTEGER NOT NULL DEFAULT 0,
    weight REAL NOT NULL DEFAULT 0.0
);
```

##### Enemies Table
```sql
CREATE TABLE enemies (
    enemy_id TEXT PRIMARY KEY,
    enemy_name TEXT NOT NULL,
    enemy_type TEXT NOT NULL,
    enemy_level INTEGER NOT NULL DEFAULT 1,
    health INTEGER NOT NULL DEFAULT 100,
    max_health INTEGER NOT NULL,
    damage INTEGER NOT NULL DEFAULT 10,
    defense INTEGER NOT NULL DEFAULT 5,
    speed REAL NOT NULL DEFAULT 1.0,
    experience_reward INTEGER NOT NULL DEFAULT 0,
    loot_tables JSON,
    ai_behavior TEXT NOT NULL,
    is_boss INTEGER NOT NULL DEFAULT 0,
    region_tag TEXT,
    spawn_chance REAL NOT NULL DEFAULT 1.0
);
```

##### Quests Table
```sql
CREATE TABLE quests (
    quest_id TEXT PRIMARY KEY,
    quest_name TEXT NOT NULL,
    quest_description TEXT NOT NULL,
    quest_type TEXT NOT NULL,
    quest_giver_id TEXT NOT NULL,
    quest_location TEXT NOT NULL,
    difficulty_level INTEGER NOT NULL DEFAULT 1,
    required_level INTEGER NOT NULL DEFAULT 1,
    main_quest INTEGER NOT NULL DEFAULT 0,
    available_actions JSON,
    quest_state TEXT NOT NULL DEFAULT "available",
    quest_start_time INTEGER,
    quest_end_time INTEGER,
    time_limit INTEGER NOT NULL,
    rewards JSON
);
```

##### Skills Table
```sql
CREATE TABLE skills (
    skill_id TEXT PRIMARY KEY,
    skill_name TEXT NOT NULL,
    skill_type TEXT NOT NULL,
    skill_category TEXT NOT NULL,
    skill_level INTEGER NOT NULL DEFAULT 1,
    max_skill_level INTEGER NOT NULL,
    required_level INTEGER NOT NULL DEFAULT 1,
    cooldown_seconds REAL NOT NULL DEFAULT 0.0,
    mana_cost INTEGER NOT NULL DEFAULT 0,
    stamina_cost INTEGER NOT NULL DEFAULT 0,
    damage_multiplier REAL NOT NULL DEFAULT 1.0,
    description TEXT NOT NULL,
    icon_path TEXT
);
```

##### Progression Table
```sql
CREATE TABLE progression (
    progression_id TEXT PRIMARY KEY,
    player_id TEXT NOT NULL,
    character_level INTEGER NOT NULL DEFAULT 1,
    current_xp INTEGER NOT NULL DEFAULT 0,
    skill_points INTEGER NOT NULL DEFAULT 0,
    talent_points INTEGER NOT NULL DEFAULT 0,
    total_playtime INTEGER NOT NULL DEFAULT 0,
    last_played INTEGER NOT NULL,
    stats JSON,
    specialization TEXT NOT NULL DEFAULT "warrior"
);
```

##### Save Table
```sql
CREATE TABLE saves (
    save_id TEXT PRIMARY KEY,
    save_name TEXT NOT NULL,
    player_data JSON NOT NULL,
    inventory_data JSON NOT NULL,
    equipment_data JSON NOT NULL,
    dungeon_data JSON NOT NULL,
    army_data JSON NOT NULL,
    quest_progress JSON NOT NULL,
    reputation_data JSON NOT NULL,
    world_state JSON NOT NULL,
    timestamp INTEGER NOT NULL,
    game_mode TEXT NOT NULL,
    difficulty_setting TEXT NOT NULL DEFAULT "normal"
);
```

### Configuration JSON Files

#### Game Config
```json
{
    "game_config": {
        "initial_gold": 100,
        "initial_hp": 100,
        "initial_stamina": 100,
        "initial_mana": 100,
        "max_health_per_level": 20,
        "max_stamina_per_level": 15,
        "max_mana_per_level": 20,
        "xp_to_level": [100, 250, 500, 900, 1500, 2400, 3600],
        "difficulty_settings": {
            "normal": {"enemy_multiplier": 1.0, "gold_multiplier": 1.0},
            "hard": {"enemy_multiplier": 1.5, "gold_multiplier": 1.3},
            "nightmare": {"enemy_multiplier": 2.0, "gold_multiplier": 1.6}
        }
    }
}
```

#### World Config
```json
{
    "world_config": {
        "regions": [
            {
                "region_id": "kronos",
                "region_name": "Kronos Kingdom",
                "region_type": "human",
                "background_path": "res://assets/backgrounds/kronos.png",
                "start_location": "capital_city",
                "default_music": "kronos_theme",
                "monster_types": ["wolf", "bear", "goblin", "adventurer"],
                "npc_faction": "kronos_faction"
            }
        ],
        "locations": [
            {
                "location_id": "capital_city",
                "location_name": "Kronos Capital",
                "location_type": "town",
                "region_id": "kronos",
                "unlockable": true,
                "connections": ["military_outpost", "trade_district"],
                "shops": ["general_store", "weaponsmith", "alchemy_shop"],
                "npc_count": 50,
                "default_music": "kronos_market"
            }
        ]
    }
}
```

---

## 9. ASSET BREAKDOWN BY SYSTEM

### Player System Assets
**Total Assets**: 40+  
**Priority**: Highest

#### Character Sprites (16 assets)
- [x] Player skeleton idle (8 directions) - 16 sprites, 16x16, 32x32
- [x] Player skeleton walk (8 directions) - 16 sprites, 16x16, 32x32
- [x] Player skeleton attack (8 directions) - 16 sprites, 16x16, 32x32
- [x] Player skeleton block (8 directions) - 16 sprites, 16x16, 32x32
- [x] Player skeleton dodge (8 directions) - 16 sprites
- [x] Caster stance idle - 16 sprites
- [x] Caster stance walk - 16 sprites
- [x] Warrior stance idle - 16 sprites
- [x] Warrior stance walk - 16 sprites
- [x] Equipment overrides (helmet, chest, gloves, boots) - 16 sprites
- [x] Equipment glow effects - 16 sprites

#### HUD Elements (12 assets)
- [x] Health bar container and health bar - 4 sprites
- [x] Energy bar container and energy bar - 4 sprites
- [x] Stamina bar container and stamina bar - 4 sprites
- [x] Character portrait - 8x8, 16x16, 32x32 variants

#### UI Panels (8 assets)
- [x] Character stats panel - 4 variations
- [x] Character customization menu - 4 variations

### Combat System Assets
**Total Assets**: 60+  
**Priority**: High

#### Enemy Sprites (30 assets)
- [x] Skeleton warrior idle/walk - 4 animations
- [x] Skeleton warrior attack - 4 animations
- [x] Skeleton warrior death - 3 animations + particles
- [x] Orc warrior sprites - 12 animations
- [x] Goblin sprites - 12 animations
- [x] Boss sprites - 8 animations each

#### Combat Effects (15 assets)
- [x] Hit effects (8 directions, 3 sizes) - 24 sprites
- [x] Blood effects - 8 sprites
- [x] Magic spell effects - 12 sprites
- [x] Skill effect trails - 8 sprites
- [x] Dodge effects - 4 sprites
- [x] Block effects - 4 sprites
- [x] Critical hit effects - 4 sprites

#### Combat UI (7 assets)
- [x] Combat targeting reticle - 8 variants
- [x] Attack combos display - 8 variants
- [x] Skill cooldown indicators - 8 variants

### Dungeon System Assets
**Total Assets**: 100+  
**Priority**: Medium

#### Tile Set (16 assets)
- [x] Floor tiles (16 variations) - 16x16 each
- [x] Wall tiles (16 variations) - 16x16 each
- [x] Ceiling tiles (16 variations) - 16x16 each
- [x] Border tiles (16 variations)

#### Room Templates (20 assets)
- [x] Basic chamber - 8 variations
- [x] Corridor pieces - 12 variations
- [x] Training room - 4 variations
- [x] Research room - 4 variations
- [x] Crafting room - 4 variations
- [x] Torture chamber - 4 variations
- [x] Library - 4 variations
- [x] Altar - 4 variations
- [x] Summoning circle - 4 variations
- [x] Barracks - 4 variations
- [x] Armory - 4 variations
- [x] Guard room - 4 variations

#### Decorative Items (20 assets)
- [x] Torches - 8 sprites
- [x] Chains - 8 sprites
- [x] Bones and skulls - 8 sprites
- [x] Pillars - 8 sprites
- [x] Altar items - 8 sprites
- [x] Bookshelves - 8 sprites

### UI System Assets
**Total Assets**: 40+  
**Priority**: High

#### Main Menu (8 assets)
- [x] Main menu background - 4 variations
- [x] Menu buttons (start, continue, settings) - 8 variants
- [x] Title screen - 1 large image
- [x] Version information

#### HUD Elements (20 assets)
- [x] Compass/mini-map - 4 variations
- [x] Quest tracking panel - 4 variations
- [x] Dialog box - 4 variations
- [x] Inventory grid slots - 4 variations
- [x] Guild panel - 4 variations
- [x] Status effects icons - 8 variants

#### Inventory Icons (20 assets)
- [x] Weapon icons (16 types) - 16x16
- [x] Armor icons (16 types) - 16x16
- [x] Consumable icons (8 types) - 16x16
- [x] Material icons (16 types) - 16x16

### World System Assets
**Total Assets**: 80+  
**Priority**: Medium

#### World Map (8 assets)
- [x] World map background - 4 variations
- [x] Location markers - 8 variants
- [x] Region borders - 8 variants
- [x] Fog of war effects - 4 variants

#### Region Backgrounds (8 assets)
- [x] Kronos Kingdom - 1 variation
- [x] Frostfen Wastes - 1 variation
- [x] Weeping Marshlands - 1 variation
- [x] Scarlet Peaks - 1 variation
- [x] Whispering Forests - 1 variation
- [x] Sunken Cities - 1 variation

#### Terrain Elements (32 assets)
- [x] Plain tiles (16 variations) - 16x16
- [x] Mountain tiles (16 variations)
- [x] Forest tiles (16 variations)
- [x] Water tiles (16 variations)

### NPC System Assets
**Total Assets**: 50+  
**Priority**: Medium

#### NPC Sprites (24 assets)
- [x] Human NPCs (8 types) - 12 animations each
- [x] Undead NPCs (8 types) - 12 animations each
- [x] Elven NPCs (4 types) - 12 animations each
- [x] Dwarf NPCs (4 types) - 12 animations each

#### NPC Portraits (20 assets)
- [x] Human NPCs (8 portraits)
- [x] Undead NPCs (8 portraits)
- [x] Other species (4 portraits)

### Audio System Assets
**Total Assets**: 30+  
**Priority**: High

#### Music (8 assets)
- [x] MainMenu - 1 track
- [x] Kronos Kingdom - 1 track
- [x] Frostfen Wastes - 1 track
- [x] Weeping Marshlands - 1 track
- [x] Combat - 1 track
- [x] Combat Epic - 1 track
- [x] Dungeon - 1 track
- [x] Victory - 1 track

#### Sound Effects (12 assets)
- [x] footsteps - 8 variations (different surfaces)
- [x] combat sounds - 8 variations (sword hits, spells, etc.)
- [x] UI sounds - 8 variations (buttons, clicks, etc.)
- [x] NPC speech - 4 variations (different lines)

---

## 10. SAVE SYSTEM DESIGN

### Save System Architecture

#### SaveData Structure
```gdscript
class_name SaveData
extends Resource

var save_id: String = ""
var save_name: String = ""
var timestamp: int = 0
var last_played_location: String = ""
var game_mode: String = "normal"
var difficulty_level: int = 5

# Player progression
var player_level: int = 1
var current_xp: int = 0
var skill_points: int = 0
var total_playtime: int = 0
var specialization: String = "warrior"

# Character stats
var current_hp: float = 100.0
var max_hp: float = 100.0
var energy: float = 100.0
var max_energy: float = 100.0
var stamina: float = 100.0
var max_stamina: float = 100.0
var gold: int = 100

# Inventory and equipment
var inventory: Array = []
var equipment: Dictionary = {}

# Dungeon
var dungeon_build: Dictionary = {}
var current_dungeon_floor: int = 1

# Quests
var quest_progress: Dictionary = {}
var completed_quests: Array = []

# AI and reputation
var reputation: Dictionary = {}
var karma: float = 0.0

# World state
var discovered_locations: Array = []
var completed_objectives: Array = []
```

#### Save Slots System
```gdscript
class_name SaveManager
extends Node

const SAVE_PATH = "user://saves/"
const SAVE_FILE_PREFIX = "dynasty_save_"

signal save_created(save_id: String)
signal save_loaded(save_id: String)
signal save_deleted(save_id: String)

var save_slots: Dictionary = {}

func create_save_slot(slot_index: int, save_data: SaveData) -> void
func load_save_slot(slot_index: int) -> SaveData
func delete_save_slot(slot_index: int) -> void
func list_save_slots() -> void
func quick_save() -> void
func quick_load() -> void
```

#### Save File Formats
```json
{
    "save_data": {
        "save_id": "save_001",
        "save_name": "Playthrough 1",
        "timestamp": 1707907200,
        "last_played_location": "capital_city",
        "game_mode": "normal",
        "difficulty_level": 5,
        "player_level": 15,
        "current_xp": 2300,
        "skill_points": 3,
        "total_playtime": 3600,
        "specialization": "warrior",
        "current_hp": 85.0,
        "max_hp": 200.0,
        "energy": 50.0,
        "max_energy": 100.0,
        "stamina": 75.0,
        "max_stamina": 150.0,
        "gold": 450,
        "inventory": [
            {"item_id": "sword_normal", "stack_count": 1},
            {"item_id": "health_potion", "stack_count": 5}
        ],
        "equipment": {
            "weapon": "sword_normal",
            "chest": "armor_heavy",
            "helmet": "helmet_iron",
            "boots": "boots_iron"
        },
        "quest_progress": {
            "quest_001": "in_progress",
            "quest_002": "started"
        },
        "completed_quests": ["quest_000"],
        "reputation": {
            "kronos_faction": 25.0,
            "merchant_guild": 10.0
        },
        "karma": 15.0,
        "discovered_locations": ["capital_city", "military_outpost"],
        "dungeon_build": {
            "floor_1": {
                "room_1": "chamber_main",
                "room_2": "training_area"
            }
        }
    }
}
```

### Auto-Save System
```gdscript
const AUTO_SAVE_DELAY = 600  # 10 minutes
const QUICK_SAVE_DELAY = 30  # 30 seconds

signal auto_save_completed

var auto_save_timer: int = 0
var quick_save_active: bool = false

func _process(delta: float) -> void:
    if player_system.is_alive:
        auto_save_timer += delta
        if auto_save_timer >= AUTO_SAVE_DELAY:
            auto_save_timer = 0
            perform_auto_save()

func perform_auto_save() -> void:
    var save_data = Global.save_system.create_save_data()
    Global.save_system.save_to_slot(1, save_data)
    auto_save_timer = 1 # Immediate next save

func perform_quick_save() -> void:
    var save_data = Global.save_system.create_save_data()
    Global.save_system.save_to_slot(8, save_data)
    quick_save_active = true
```

---

## 11. PERFORMANCE OPTIMIZATION

### Optimization Strategy

#### Rendering Optimization
1. **Sprite Pools**
   - Pool sprite instances for frequently used sprites
   - Reduce Sprite2D node creation overhead
   - Implement object reuse for particles

2. **Draw Calls Reduction**
   - Group by texture/material
   - Batch draw calls where possible
   - Use AtlasTexture for sprite batching

3. **LOD System**
   - Level of Detail for distant objects
   - Simplified sprites for background elements
   - Distance-based rendering decisions

4. **Canvas Optimization**
   - Minimize Node2D overhead
   - Use CanvasLayer for UI optimization
   - Cache UI layouts and calculations

#### Physics Optimization
1. **Collision Optimization**
   - Use appropriate collision shapes (Capsule vs Rectangle)
   - Disable collisions for invisible objects
   - Use collision layer/mask optimization
   - Spatial hashing for large-scale physics

2. **Movement Optimization**
   - Smooth movement with fixed steps
   - Avoid per-frame position recalculation
   - Use physics interpolation where appropriate

3. **AI Optimization**
   - Simple pathfinding for most NPCs
   - Spatial partitioning for AI queries
   - AI state batching
   - Object pooling for AI entities

#### Memory Optimization
1. **Resource Management**
   - Preload only necessary resources
   - Unload unused resources
   - Implement asset reference counting
   - Use ResourceLoader with caching strategy

2. **Data Structure Optimization**
   - Use efficient data structures for large collections
   - Implement data compression for save files
   - Use JSON for quick save/load

3. **Texture Optimization**
   - Use compressed texture formats (ASTC)
   - Reduce texture resolution for distant objects
   - Implement texture atlases

#### System Performance
```gdscript
# Performance monitoring system
class_name PerformanceMonitor
extends Node

const MAX_FRAMES_TO_TRACK = 60
var frame_times: Array = []

var current_fps: int = 0
var average_frame_time: float = 0.0
var performance_score: float = 100.0

func _process(delta: float) -> void:
    update_metric()

func update_metric() -> void:
    var frame_time = delta
    frame_times.append(frame_time)
    if frame_times.size() > MAX_FRAMES_TO_TRACK:
        frame_times.pop_front()

    current_fps = int(1.0 / delta)
    average_frame_time = frame_times.reduce( func(accum, time): return accum + time, 0.0 ) / frame_times.size()
    
    calculate_performance_score()

func calculate_performance_score() -> void:
    if avg_frame_time < 0.01666:  # Below 60 FPS
        performance_score = 95.0
    elif avg_frame_time < 0.03333:  # Below 30 FPS
        performance_score = 75.0
    elif avg_frame_time < 0.05:  # Below 20 FPS
        performance_score = 50.0
    elif avg_frame_time < 0.1:  # Below 10 FPS
        performance_score = 25.0
    else:
        performance_score = 100.0 - ((avg_frame_time - 0.01666) * 2000.0)
        performance_score = clamp(performance_score, 0.0, 100.0)

func optimize_systems() -> void:
    # Call various optimization systems
    optimize_particle_system()
    optimize_collision_system()
    optimize_memory_system()
```

---

## 12. BALANCING & DIFFICULTY

### Balance Strategy

#### Combat Balance Guidelines

**Player Stats Curve**
```gdscript
# Base stats per level
const BASE_STATS = {
    "strength": 5,
    "dexterity": 5,
    "intelligence": 5,
    "vitality": 5,
    "wisdom": 5,
    "charisma": 5
}

# Stat growth per level
const STATS_GROWTH = {
    "strength": 1.0,
    "dexterity": 1.0,
    "intelligence": 1.0,
    "vitality": 1.5,
    "wisdom": 1.0,
    "charisma": 0.5
}

# XP requirements for each level
const XP_REQUIREMENTS = {
    1: 0,
    2: 100,
    3: 250,
    4: 500,
    5: 900,
    6: 1500,
    7: 2400,
    8: 3600,
    9: 5200,
    10: 7000,
    11: 9200,
    12: 11800,
    13: 14800,
    14: 18200,
    15: 22000,
    16: 26200,
    17: 30800,
    18: 35800,
    19: 41200,
    20: 47000
    // Add values to level 100
}
```

**Enemy Scaling**
```gdscript
# Enemy difficulty calculation
var enemy_difficulty_factor = {}

func calculate_enemy_difficulty(level: int, enemy_type: int, region: int) -> float:
    var base_difficulty = get_base_difficulty(enemy_type)
    var level_factor = 1.0 + (level - 1) * 0.1
    var region_bonus = get_region_bonus(region)
    
    var difficulty = base_difficulty * level_factor * region_bonus
    return clamp(difficulty, 0.5, 5.0)

func get_base_difficulty(enemy_type: int) -> float:
    return {
        1: 1.0,  # Basic skeleton
        2: 1.2,  # Skeleton warrior
        3: 1.5,  # Orc warrior
        4: 2.0,  # Goblin
        5: 3.0,  # Boss
        6: 1.0   # Elite
    }.get(enemy_type, 1.0)

func get_region_bonus(region: int) -> float:
    return {
        1: 1.0,  # Normal
        2: 1.3,  # Hard
        3: 1.6   # Nightmare
    }.get(region, 1.0)
```

### Difficulty Systems

#### Game Modes

**Normal Mode**
- Enemy difficulty: 100%
- Quest rewards: 100%
- Gold rewards: 100%
- Difficulty: Recommended for first playthrough

**Hard Mode**
- Enemy difficulty: 150%
- Quest rewards: 130%
- Gold rewards: 130%
- Recommended for experienced players

**Nightmare Mode**
- Enemy difficulty: 200%
- Quest rewards: 160%
- Gold rewards: 160%
- New mechanics and challenges

#### Difficulty Settings
```gdscript
class_name DifficultyManager
extends Node

enum Difficulty {
    NORMAL,
    HARD,
    NIGHTMARE,
    CUSTOM
}

var current_difficulty: Difficulty = Difficulty.NORMAL
var difficulty_settings = {}

const DIFFICULTY_PRESETS = {
    Difficulty.NORMAL: {
        "enemy_multiplier": 1.0,
        "gold_multiplier": 1.0,
        "quest_multiplier": 1.0,
        "xp_multiplier": 1.0,
        "enemy_knockback": 0.5
    },
    Difficulty.HARD: {
        "enemy_multiplier": 1.5,
        "gold_multiplier": 1.3,
        "quest_multiplier": 1.3,
        "xp_multiplier": 1.2,
        "enemy_knockback": 0.7
    },
    Difficulty.NIGHTMARE: {
        "enemy_multiplier": 2.0,
        "gold_multiplier": 1.6,
        "quest_multiplier": 1.6,
        "xp_multiplier": 1.4,
        "enemy_knockback": 1.0
    }
}

func apply_difficulty_settings() -> void:
    var settings = DIFFICULTY_PRESETS[current_difficulty]
    Global.combat_system.apply_difficulty_multiplier(settings["enemy_multiplier"])
    Global.economy_system.apply_difficulty_multiplier(settings["gold_multiplier"])
```

---

## 13. TESTING STRATEGY

### Test Structure

#### Unit Testing
**Scope**: Core systems and individual components

```gdscript
# Core systems to test
- PlayerMovementSystem: Movement accuracy, speed, control responsiveness
- CombatSystem: Damage calculation, hit detection, cooldowns
- InventorySystem: Item handling, equip/unequip logic, stacking
- SaveSystem: Save/load verification, data integrity
- QuestSystem: Quest state management, progression tracking
```

#### Integration Testing
**Scope**: System interactions and workflows

| System | Tests |
|--------|-------|
| World & Navigation | Travel between locations, map discovery, navigation UI |
| Combat & Progression | XP gain from combat, level-up system, stat allocation |
| Inventory | Equipment system, stat bonuses, item stacking |
| Dungeon Building | Room placement, resource management, build validation |
| Army System | Unit deployment, tactical combat, conquest mechanics |
| Guild & Quest | NPC quest interactions, quest completion tracking, rewards |

#### System Integration Tests

**Combat Flow Test**
1. Spawn player and enemy in combat zone
2. Player enters combat stance
3. Player attacks enemy
4. Damage dealt and HP reduced
5. Enemy dies, XP award
6. Loot drops collected
7. Quest progress updated

**Dungeon Build Flow Test**
1. Select floor number
2. Place basic room
3. Place specialized room
4. Connect rooms
5. Verify build cost
6. Build complete
7. Save dungeon configuration

**Quest Complete Flow Test**
1. NPC offers quest
2. Player accepts quest
3. Player completes objectives
4. Return to NPC
5. Quest progress updated
6. Quest completed
7. Reward collected

**Save/Load Test**
1. Create save with player data
2. Save to slot
3. Verify save created
4. Load save from slot
5. Verify data integrity
6. Continue gameplay
7. Save again
8. Save files work together

#### Game Loop Testing

**Full Playthrough Tests**
- **Level 1-5**: Basic movement, combat, quests
- **Level 6-15**: Skills, inventory, world exploration
- **Level 16-30**: Advanced combat, dungeon building
- **Level 31-50**: Army management, tactical battles
- **Level 51-80**: Endgame content, guild quests
- **Level 81-100**: Final boss, completion

#### Performance Testing

**Frame Rate Stability Test**
- [ ] Test with 10 concurrent entities
- [ ] Test with 50 concurrent entities
- [ ] Test with 100 concurrent entities
- [ ] Test with max concurrent entities
- [ ] Test particle systems
- [ ] Test save/load operations

**Memory Usage Test**
- [ ] Track memory over time
- [ ] Test large dungeon builds
- [ ] Test large inventories
- [ ] Test save/load cycles
- [ ] Identify memory leaks

---

## 14. DELIVERABLES & MILESTONES

### MVP (Minimum Viable Product) - Week 6
**Definition**: Basic playable prototype

**Features Delivered**
- [x] Player movement and camera system
- [x] Basic combat with enemies
- [x] World map navigation
- [x] Basic inventory system
- [x] Level-up progression
- [x] Simple quests

**Acceptance Criteria**
- Player can move and attack
- Enemies spawn and can be defeated
- Player gains XP and levels up
- Inventory can hold items and equipment
- World map allows travel between locations
- Save/load system works

### Alpha Version - Week 12
**Definition**: Feature-complete base game

**Features Delivered**
- [x] Complete character creation
- [x] Full world with all regions
- [x] Complete combat system
- [x] Full inventory and equipment
- [x] Skill system
- [x] Basic dungeon builder
- [x] Quest system foundation

**Acceptance Criteria**
- All core gameplay mechanics work
- World is fully explorable
- Combat is responsive and balanced
- Inventory management works
- Progression feels rewarding
- Dungeon builder can build functional dungeons

### Beta Version - Week 20
**Definition**: Feature-complete game ready for testing

**Features Delivered**
- [x] Army management system
- [x] Tactical battle mechanics
- [x] Guild system
- [x] Advanced NPC system
- [x] Economy and trading
- [x] Save/load system
- [x] Multiple difficulty settings

**Acceptance Criteria**
- Army system functions
- Tactical battles work
- Guild quests complete system
- NPCs interact properly
- Trading works
- Save system reliable
- Multiple playthroughs supported

### Release Candidate - Week 24
**Definition**: Production-ready game

**Features Delivered**
- [x] Final content polish
- [x] Audio and music
- [x] Visual polish
- [x] Final bug fixes
- [x] Performance optimization
- [x] Tutorial system
- [x] Accessibility options

**Acceptance Criteria**
- No critical bugs
- All content complete
- Good performance on target hardware
- Tutorial teaches core mechanics
- Game is accessible to intended audience
- Save system stable

### Final Release - Week 26
**Definition**: Official game release

**Deliverables**
- [x] Production build
- [x] Installation package (Windows)
- [x] Game documentation
- [x] Launch trailer
- [x] System requirements
- [x] Support website

---

## 15. DEVELOPMENT TIMELINE ESTIMATES

### Overall Timeline: 26 Weeks (6 Months)

### Weekly Breakdown

**Weeks 1-6: MVP Development**
- Days 1-7: Project setup, core engine
- Days 8-14: Player movement, combat basics
- Days 15-21: World exploration, quests
- Days 22-28: Finish MVP, testing

**Weeks 7-12: Alpha Version**
- Days 29-35: Combat system completion
- Days 36-42: Inventory and equipment
- Days 43-49: Progression system
- Days 50-56: World content completion

**Weeks 13-18: Beta Version Alpha**
- Days 57-63: Dungeon builder core
- Days 64-70: Dungeon system expansion
- Days 71-77: Army management basics
- Days 78-84: Tactical combat

**Weeks 19-22: Beta Version Beta**
- Days 85-91: Guild system
- Days 92-98: NPC system
- Days 99-105: Economy and trading
- Days 106-112: Final beta features

**Weeks 23-26: Production**
- Days 113-119: Content polish
- Days 120-126: Audio and visual polish
- Days 127-133: Performance optimization
- Days 134-140: Final release preparation

### Team Structure (Recommended)

#### Core Development Team (4-6 people)

**Lead Designer**
- Game design implementation
- Balance tuning
- Feature prioritization

**Game Programmers (2-3)**
- Core systems implementation
- Gameplay programming
- Performance optimization

**Artist (1)**
- Pixel art production
- Asset creation
- UI design

**Technical Artist (1)**
- Sprite optimization
- Color palettes
- Texture management

**QA Testers (1-2)**
- Testing implementation
- Bug tracking
- Quality assurance

### Risk Assessment

**High Risk Areas**
1. **Pixel Art Requirements** - 2-3 weeks behind if artist falls behind schedule. Mitigation: Use placeholder art initially, prioritize core gameplay first

2. **Complex AI Systems** - Army combat and NPC behavior can be complex. Mitigation: Start with simple implementations, incrementally add complexity

3. **Dungeon Builder Complexity** - Grid-based building system can be complex to implement robustly. Mitigation: Build on proven patterns, test thoroughly during development

**Medium Risk Areas**
1. **Save System Issues** - Corruption or compatibility can be problematic. Mitigation: Extensive testing, save file versioning

2. **Performance on Low-End Hardware** - Can reduce player base. Mitigation: Continuous optimization testing

3. **Content Volume** - Large game requires significant content creation. Mitigation: Build core mechanics first, expand content later

---

## APPENDICES

### Appendix A: Technical Specifications

**Target System Requirements**

**Minimum Requirements**
- CPU: Intel Core i3 or equivalent
- RAM: 4GB RAM
- GPU: DirectX 11 compatible with 1GB VRAM
- Storage: 5GB free space

**Recommended Requirements**
- CPU: Intel Core i5 or equivalent
- RAM: 8GB RAM
- GPU: DirectX 11 compatible with 4GB VRAM
- Storage: 10GB SSD recommended

**Graphics Performance**
- Target resolution: 1920x1080
- Recommended resolution: 1920x1080
- Frame rate target: 60 FPS
- Frame time target: <16.67ms

### Appendix B: Development Tools List

**Development Tools**
- Godot 4.6.2+
- Visual Studio Code (or similar IDE)
- Git/GitHub for version control
- Issue tracker (GitHub Issues or similar)

**Art Tools**
- Aseprite (pixel art)
- Krita (digital painting)
- GIMP (image editing)
- Audacity (audio editing)

**Testing Tools**
- Godot test runner
- Performance profiling tools
- Memory monitoring tools

### Appendix C: File Naming Conventions

**Scene Files**
- `scene_name.tscn` - Standard scene file
- `scene_name_1.tscn` - Variant scene
- `scene_name_backup.tscn` - Backup scene

**Sprite Files**
- `player_idle_00.png` - Player idle sprite frame
- `enemy_skeleton_01.png` - Enemy sprite
- `ui_button_normal.png` - UI button

**Audio Files**
- `music_ambient_01.ogg` - Ambient music
- `sfx_sword_hit.wav` - Sound effect
- `voice_npc_001.wav` - Voice line

### Appendix D: Contact & Resources

**Documentation References**
- Godot Engine Documentation
- GDD (Game Design Document)
- AGENTS.md (Development Guidelines)

**Version Control**
- Main branch: `main`
- Development branch: `develop`
- Feature branches: `feature/`
- Bug fix branches: `fix/`

**Issue Tracking**
- Bug reports: GitHub Issues
- Feature requests: GitHub Projects
- Priority: Bug fixes > Features > Polish

---

**Document Version**: 1.0  
**Last Updated**: February 14, 2026  
**Next Review**: After Alpha Version completion

---

*This implementation plan is a living document and will be updated as development progresses or new requirements emerge.*