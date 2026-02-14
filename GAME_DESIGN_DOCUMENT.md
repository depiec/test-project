# Game Design Document: Overlord-inspired 2D Action RPG

## Executive Summary

**Project Title**: DYNASTY OF SOULS

**Genre**: 2D Action RPG / Dungeon Management

**Platform**: PC (Godot 4.6+)

**Core Concept**: An action RPG where players guide an undead skeleton lord as they build their dungeon fortress, gather armies, conquer territories, and navigate a world filled with complex societies and conflicts.

## Target Audience

- Fans of action RPGs and dungeon management games
- Fans of dark fantasy and medieval settings
- Players who enjoy deep progression systems and character customization
- Fans of the Overlord series seeking a similar experience in 2D format

## Unique Selling Points

1. **Skeletal Undead Protagonist with Strategic Depth**
2. **Grid-based Dungeon Builder with Resource Management**
3. **Action Combat with Dual-stance System**
4. **NPC-driven Guild Quest System**
5. **Tactical Army Conquest Mode**
6. **Deep Economy and Trade Systems**

---

## 1. WORLD BUILDING

### 1.1 World Geography and Locations

The world of **Aethelgard** spans several distinct regions, each with unique ecosystems, cultures, and power dynamics:

#### The Living World

1. **Kronos Kingdom** (Capital Region)
   - Human-dominated kingdom with centralized monarchy
   - Powerful nobles and wealthy merchant guilds
   - Known for advanced architecture and organized military
   - Home to the Adventurer's Guild chapter (where protagonist initially serves)
   - Features: Grand castle, marble palaces, bustling trade districts

2. **Frostfen Wastes**
   - Harsh northern region inhabited by hardened survivors
   - Nords tribe people with shamanistic traditions
   - Resource-rich: minerals, rare herbs, rare wood types
   - Dangerous ice monsters and frost giants
   - Home to ancient ruins of previous civilizations

3. **Weeping Marshlands**
   - Toxic swamplands with diverse wildlife
   - Nomadic people with tribal social structures
   - Alchemical knowledge and herbal medicine
   - Mutant creatures and water-based hazards
   - Overgrown ancient temples and catacombs

4. **Scarlet Peaks**
   - Volcanic mountain range
   - Dwarf communities with advanced smithing arts
   - Fire-resistant settlements, mining operations
   - Elemental creatures and lava-based threats
   - Source of rare elemental crystals

5. **Whispering Forests**
   - Ancient magical forest with sentient plants
   - Elven enclaves, druids, nature guardians
   - Powerful magical creatures and nature elementals
   - Dense canopy, hidden ruins, ley lines
   - Sacred groves and ancient tree guardians

6. **Sunken Cities**
   - Underwater or flooded coastal regions
   - Ancient civilizations with advanced technologies
   - Pirate settlements, fish-people tribes
   - Sunken temples, underwater ruins
   - Treasure-rich but dangerous

#### The Undead Realm

1. **Graveheart Citadel** (Player's Base/Dungeon)
   - Multi-story dungeon with unique architectural style
   - Underground chambers, torture chambers, libraries
   - Ancient necromancy rituals and forbidden knowledge
   - Summoning circles, soul stones, dark altars
   - Player creates custom dungeon layouts

2. **Bonefort Plains**
   - Wide plains inhabited by lesser undead
   - Simple villages, resource production
   - Graveyard domains, death knights' territories
   - Scattered bones, skeletal remains
   - Training grounds and ambush points

3. **Soulweaver Sanctum**
   - Domain of powerful necromancers
   - Advanced soul manipulation capabilities
   - Soul collection facilities, ritual chambers
   - Elite undead armies, ghostly phenomena
   - Source of magical corruption and power

4. **Ashen Valley**
   - Battlefield ruins and mass graves
   - Powerful undead warlords and champions
   - Armored skeletons, magical constructs
   - Remnants of epic battles, scattered equipment
   - Stronghold of the undead elite

### 1.2 Factions and Organizations

#### Human Factions

1. **The Order of Light**
   - Religious organization, zealous warrior monks
   - Holy knights, paladins, divine spellcasters
   - Dedicated to hunting demons, undead, and heretics
   - Extensive network of churches and temples
   - Seeks to banish evil from Aethelgard

2. **Merchant's Alliance**
   - International trade organization
   - Wealthy merchant houses and guilds
   - Controls major trade routes and ports
   - Diplomatic and economic influence
   - Protects merchants with armed convoys

3. **Wandering Swordsmen Guild**
   - Independent adventuring organization
   - Mercenary companies, bounty hunters
   - Various skills and specializations
   - Operates across multiple kingdoms
   - Can be hired as NPCs and armies

4. **The Shadow Council**
   - Secretive criminal organization
   - Assassins, spies, information brokers
   - Operates in shadows of society
   - Powerful influence on dark dealings
   - Has deep underworld connections

#### Non-Human Factions

1. **High Council of Elves**
   - Ruling elven organization
   - Ancient, wise mages and scholars
   - Magic research and preservation
   - Elven nobility and elite warriors
   - Guarded by powerful spellcasters and rangers

2. **Dwarven Ironborn Clan**
   - Traditional dwarf families and guilds
   - Master craftsmen, weapon makers, armor smiths
   - Clan rivalry and internal politics
   - Strong defensive fortifications
   - Known for superior armor and weapons

3. **Frostnord Tribes**
   - Nords tribes with shamanistic traditions
   - Tribal chieftains and shaman elders
   - Blood magic and nature worship
   - Clan loyalty and honor codes
   - Known for berserker combat style

#### Undead Factions

1. **Lichdom Ruling Council**
   - Supreme necromancers, master spellcasters
   - Ancient beings of extreme power
   - Control over death magic and necromancy
   - Gather souls and magical knowledge
   - Rare meetings with high stakes

2. **Death Knight Order**
   - Elite undead warriors, former paladins
   - Powerful combatants with dark armor
   - Loyal to necromancers, protectors of undead
   - Known for their fearsome abilities
   - Serve as dungeon protectors and lieutenants

3. **Soul Collectors Guild**
   - Undead specialized in soul harvesting
   - Collect souls for necromantic purposes
   - Operate in populated areas
   - Controlled by powerful liches
   - Essential for undead progression

4. **Gravekeepers**
   - Loyal undead, maintain death world
   - Ancient, wise undead souls
   - Care for the dead, maintain graveyards
   - Knowledge of ancient rituals
   - Groundskeepers and guards

### 1.3 Economy and Trade Systems

#### Currency

1. **Gold Currency**
   - Main currency used across Aethelgard
   - Minted by various kingdoms and banks
   - Coins: Gold, Silver, Copper
   - Gold coins are the standard of wealth

2. **Trade Currency**
   - Rare gems, precious metals used in trade
   - Valued by wealthy collectors and merchants
   - Used for expensive magical items
   - Source of prestige and high-level barter

3. **Soul Gems**
   - Magical currency for undead
   - Contain captured souls
   - Used to power magical items and rituals
   - Valued in underworld transactions

4. **Knowledge Currency**
   - Rare spells, magical texts
   - Valued by powerful mages
   - Used for learning abilities
   - Source of power for spellcasters

#### Trade Systems

1. **Trade Routes**
   - Major road networks connecting regions
   - Controlled by merchant guilds
   - Protected convoys and trading posts
   - Port cities with sea routes

2. **Trading Post Mechanic**
   - Set up trade relations with factions
   - Exchange resources for gold, items, information
   - NPC caravans operate between settlements
   - Diplomatic relations affect trade benefits

3. **Resource Production**
   - Farms, mines, lumber camps
   - Different quality levels based on management
   - Resource scarcity affects prices
   - Over-collection leads to resource depletion

4. **Market Fluctuations**
   - Dynamic pricing based on supply and demand
   - Seasonal changes affecting crop prices
   - War events impact resource costs
   - Black market alternative for expensive items

5. **Black Market**
   - Illegal trade operations
   - Stolen goods, contraband, illegal magic items
   - Illegal mercenaries and assassins
   - Underground connections

### 1.4 Magic and Power Systems

#### Magic Types

1. **Necromancy**
   - Soul manipulation, death magic
   - Undead creation and control
   - Life essence and spiritual energy
   - Advanced by liches and necromancers

2. **Elemental Magic**
   - Fire, ice, lightning, earth, water
   - Used by various mages and casters
   - Combat and environmental applications
   - Powerful spell combinations

3. **Shadow Magic**
   - Darkness, illusions, stealth
   - Assassin magic and spy spells
   - Soul stealing and manipulation
   - Darker applications of magic

4. **Divine Magic**
   - Holy light, healing, purification
   - Used by paladins and clerics
   - Anti-undead capabilities
   - Blessings and curses

5. **Nature Magic**
   - Plant growth, animal control
   - Druidic magic and shapeshifting
   - Forest protection and regeneration
   - Healing and restoration

#### Mana System

1. **Magic Power**
   - Mana bar used for spellcasting
   - Regenerates over time and through resting
   - Depletes when casting spells
   - Recovering requires rest and recovery

2. **Soul Power**
   - Undead-specific magic power
   - Gained from enemies and souls
   - Powers over death spells
   - Increases with undead status

3. **Magic Energy Sources**
   - Soul crystals and mana stones
   - Rare magical items used for power
   - Ritual sacrifices provide temporary power
   - Dark altars connect to magical ley lines

4. **Magic Development**
   - Spells unlock through progression
   - Mana efficiency improves with level
   - Combat experience enhances spell power
   - Specialization in particular magic schools

#### Magic Levels

1. **Novice Spells**
   - Basic combat and utility spells
   - Small mana cost
   - Limited power and effects
   - Accessible early in game

2. **Adept Spells**
   - Moderate mana cost, greater effects
   - More complex spell mechanics
   - Some tactical applications
   - Unlock around mid-game

3. **Master Spells**
   - High mana cost, powerful effects
   - Rare and advanced knowledge
   - Complex ritual requirements
   - Unlock at higher levels

4. **Grandmaster Spells**
   - Ultimate abilities, world-changing effects
   - Require preparation and resources
   - Limited usage, great consequences
   - Unlock only at high levels with mastery

### 1.5 Undead Culture and Beliefs

#### Undead Philosophy

1. **Purpose of Death**
   - Undead view life as temporary state
   - Death is continuation of existence
   - Soul persists beyond physical form
   - Power comes from understanding death

2. **Hierarchy of Souls**
   - Living souls are weaker and limited
   - Undead souls gain power through accumulation
   - Ancient souls become wiser and stronger
   - Lich souls become almost divine

3. **Power Philosophy**
   - Strength is necessary for survival
   - Respect only those who can challenge you
   - Power justifies control and rule
   - Weakness is weakness

4. **Necromantic Ethics**
   - Respecting dead and their remains
   - Using souls responsibly
   - Building from death rather than wasteful destruction
   - Wisdom from death knowledge

#### Undead Social Structure

1. **Lich Class**
   - Highest undead authority
   - Magical power, wisdom, immortality
   - Lead undead nations and organizations
   - Source of necromantic knowledge

2. **Death Knight Class**
   - Elite undead warriors
   - Strong combat capabilities
   - Loyal to liches and powerful overlords
   - Military leaders and dungeon guardians

3. **Undead NPC Classes**
   - Different undead types with specific roles
   - Guards, scholars, workers, soldiers
   - Each with unique abilities and skills
   - Loyal to their necromancer lord

4. **Undead Communities**
   - Necromantic societies and settlements
   - Organized undead populations
   - Various undead roles and functions
   - Self-sustaining death communities

#### Undead Religious Beliefs

1. **Death Deities**
   - Ancient gods of death and decay
   - Worshiped in underground temples
   - Granting power and favor to undead
   - Control over death domains

2. **Soul Afterlife**
   - Souls trapped in undead bodies
   - Continue existence after death
   - Soul journeys lead to greater power
   - Finality not part of undead belief

3. **Power of Death**
   - Death as tool and instrument
   - Death and life in balance
   - Understanding death necessary for power
   - Death is not an end but transformation

4. **Undead Ascension**
   - Goal to become nearly immortal
   - Power accumulation as path to divinity
   - Transcending human limitations
   - Undead evolution through power

### 1.6 Monster Ecosystems

#### Undead Monsters

1. **Skeleton Warriors**
   - Basic undead soldiers
   - Melee combatants with weapons
   - Low intelligence, loyal to orders
   - Foundation of undead armies

2. **Zombie Hordes**
   - Large numbers of mindless undead
   - overwhelming force capability
   - Weak individually but strong in numbers
   - Used for mass attacks

3. **Wraiths**
   - Ghostly undead combatants
   - Air elemental form, intangible
   - Can possess enemies and objects
   - Source of fear and chaos

4. **Skeleton Bosses**
   - Enhanced skeletal minions
   - More powerful and intelligent
   - Unique abilities and weapons
   - Dungeon guardians and lieutenants

5. **Necromancer Minions**
   - Undead with magical abilities
   - Spellcasting skeletons and zombies
   - Summoned for diverse attack scenarios
   - Support and combat roles

#### Living Monsters

1. **Wild Animals**
   - Deer, wolves, bears, etc.
   - Basic hunting and food source
   - Low intelligence and simple behavior
   - Weak but common

2. **Beasts**
   - Large creatures like lions, tigers
   - Superior strength and combat skills
   - Territorial and dangerous
   - Prey for stronger monsters

3. **Dragons**
   - Massive magical creatures
   - Fire breath, flight, immense strength
   - Ancient and intelligent
   - Rare and powerful bosses

4. **Elementals**
   - Fire, ice, lightning, earth, water spirits
   - Pure energy beings with magical abilities
   - Immune to natural weapons
   - Challenge for powerful adventurers

5. **Demons**
   - Creatures of darkness and chaos
   - Immense power and destructive abilities
   - Spawn from dark realms
   - Threat to all living creatures

#### Monster Types by Region

1. **Kronus Monster Types**
   - Wolves, bears, goblins
   - Common small enemies
   - Adventurer quest targets
   - Resource gathering

2. **Frostfen Monsters**
   - Ice wolves, frost giants
   - Polar animals and cold creatures
   - Dangerous ice hazards
   - Hard survival challenges

3. **Weeping Monsters**
   - Swamp creatures, hydra variants
   - Poisonous beasts and toxic monsters
   - Alchemical components from monsters
   - Hazardous environment

4. **Rock Monsters**
   - Fire breathing dragons, lava elementals
   - Volcanic creatures and molten entities
   - Extreme environment danger
   - Elite combat challenges

5. **Forest Monsters**
   - Treants, nature spirits
   - Plant-based creatures and guardians
   - Magical forest creatures
   - Druidic challenges

### 1.7 NPC Factions and Social Structure

#### NPC Social Hierarchy

1. **Nobility and Aristocracy**
   - Kings, queens, princes
   - Land and power holders
   - Political influence
   - Military leaders

2. **Merchant Class**
   - Shopkeepers, merchants, traders
   - Wealth and business management
   - Knowledge of trade routes
   - Economic power

3. **Scholars and Mages**
   - Scholars, mages, wizards
   - Knowledge and magical research
   - Rare skills and abilities
   - Intellect and power

4. **Warriors and Adventurers**
   - Knights, warriors, adventurers
   - Combat and exploration skills
   - Dangerous jobs, better pay
   - Social respect and power

5. **Common People**
   - Farmers, laborers, commoners
   - Basic needs and survival
   - Community and social ties
   - Basic rights and responsibilities

#### NPC Social Roles

1. **Quest Givers**
   - NPCs who provide missions and tasks
   - Various types: battles, investigations, trades
   - Rewards for completion
   - Story progression

2. **Shopkeepers and Merchants**
   - NPCs who trade items and services
   - Different shops by region
   - Inventory management
   - Economic interactions

3. **Informants and Spies**
   - NPCs who provide information
   - Quest help and exploration aid
   - Hidden knowledge and secrets
   - Intelligence gathering

4. **Quest Completion NPCs**
   - NPCs who complete player-issued tasks
   - Guild quests and missions
   - Character advancement
   - Guild relationships

5. **Guild Members and Officers**
   - NPCs within guild organizations
   - Leaders and sub-leaders
   - Training and skill improvement
   - Guild politics and conflicts

### 1.8 Unique Lore Around Skeletons/Undead

#### Ancient Skeleton Origins

1. **Bone Wars Era**
   - Ancient war between living and undead
   - Massive battles that shaped world
   - Ancient skeletons from this era
   - Powerful fallen champions

2. **Necromantic Renaissance**
   - Period of undead learning and power
   - Development of necromancy practices
   - Creation of ancient undead artifacts
   - Foundation of undead magic

3. **Undead Rebirth**
   - Return of powerful undead overlords
   - Resurrection of ancient skeletal heroes
   - New undead kingdoms established
   - Undead political realignments

#### Undead Creation Myths

1. **Soul Binding**
   - Undead creation through soul binding
   - Trapped souls form body structure
   - Necromantic rituals enable resurrection
   - Ancient spells preserve undead forms

2. **Bone Binding**
   - Use of original bones for undead construction
   - Enhanced with magical reinforcement
   - Unique and powerful undead
   - Traditional method of undead creation

3. **Magic Conversion**
   - Conversion through strong necromantic magic
   - Transformed living beings into undead
   - Preserving life force but changing nature
   - More powerful and potentially superior

#### Undead Culture and Traditions

1. **Death Festivals**
   - Annual rituals marking death anniversaries
   - Soul offerings to dead ancestors
   - Community and spiritual gatherings
   - Important cultural events

2. **Undead Funerals**
   - Death and remains important for undead
   - Proper burial of skeletons and remains
   - Respect for dead even among undead
   - Understanding of connection to life

3. **Ancestral Veneration**
   - Worship of powerful undead ancestors
   - Seeking guidance from skeletal heroes
   - Remembering ancient necromancers
   - Source of spiritual power

4. **Soul Preservation**
   - Sacred duty to preserve souls
   - Soul stones and soul containers
   - Preventing soul deterioration
   - Essential necromantic study

5. **Bone Collection**
   - Respects for bones and remains
   - Building collections for power
   - Proper handling of bones
   - Historical importance

---

## 2. GAME PLAY MECHANICS

### 2.1 Core Mechanics Breakdown

#### Player Movement and Controls

1. **Movement System**
   - WASD controls for character movement
   - Smooth, responsive movement
   - Character speed and acceleration
   - Movement types: walking, running, sprinting

2. **Mouse Controls**
   - Mouse for camera rotation and aim
   - Mouse click for combat and targeting
   - Right-click for interaction and selection
   - Scroll wheel for inventory and ability selection

3. **Camera System**
   - Third-person top-down camera
   - Camera follows player smoothly
   - Adjustable camera distance
   - Camera rotation based on mouse

4. **Dual-stance System**
   - Caster stance: Magic-based combat
   - Warrior stance: Melee combat with weapons
   - Switch between stances for strategic advantage
   - Each stance has unique abilities and playstyle

5. **Combat System**
   - Action combat with real-time combat
   - Attacks, blocks, dodges, counterattacks
   - Stamina resource management
   - Combat skills and abilities

#### Core Game Systems

1. **Level and Experience System**
   - Character level increases from 1 to 100
   - Kill enemies, complete quests, explore
   - Experience points for progression
   - Required experience scales with level

2. **Character Stats**
   - Strength, Dexterity, Intelligence, Wisdom, Vitality, Charisma
   - Stat points from level upgrades
   - Stats affect combat, magic, and exploration
   - Different builds for different playstyles

3. **Skills and Abilities**
   - Combat skills, magic spells, utility skills
   - Unlocked through progression and training
   - Different skill tree paths
   - Skill cooldowns and mana costs

4. **Quest and Mission System**
   - Main story quests and side quests
   - Faction quests and reputation
   - Personal missions and objectives
   - Quest tracking and rewards

### 2.2 Combat System Details

#### Combat Mechanics

1. **Real-time Action Combat**
   - Real-time combat with fast-paced action
   - Melee combat with weapons
   - Ranged combat with ranged abilities
   - Magic combat with spells and abilities

2. **Dual-stance Combat**
   - Caster stance:
     - Magic-based abilities
     - Range combat from distance
     - AOE spells and crowd control
     - Lower defense but high damage potential
   - Warrior stance:
     - Melee combat with weapons
     - Physical attacks and combos
     - High defense and survivability
     - Strong close combat abilities

3. **Attack and Defense Mechanics**
   - Basic attacks with weapons
   - Combo system and combos
   - Block and parry mechanics
   - Dodging and evading attacks
   - Counterattack opportunities

4. **Stamina and Resource Management**
   - Stamina for combat actions
   - Mana for spellcasting
   - Energy for special abilities
   - Resource recovery and management

5. **Combat Skills and Abilities**
   - Unlockable combat abilities
   - Different skill tree paths
   - Ability cooldowns
   - Mana and stamina costs
   - Specializations in combat styles

#### Combat Flow

1. **Pre-combat Phase**
   - Assess target and approach
   - Choose stance based on situation
   - Use skills for advantage
   - Positioning and placement

2. **Combat Phase**
   - Engage enemy in combat
   - Use combination of attacks and abilities
   - Manage resources between enemies
   - Defensive maneuvers as needed

3. **Post-combat Phase**
   - Loot and recover resources
   - Assess next enemy and plan
   - Use consumable items
   - Continue combat or retreat

#### Combat Scenarios

1. **Solo Combat**
   - Player vs. single enemy
   - Classic combat challenge
   - Skill testing and progression
   - Single target elimination

2. **Group Combat**
   - Player vs. multiple enemies
   - Crowd control and AOE abilities
   - Tactical positioning and strategy
   - Managing multiple combatants

3. **Boss Combat**
   - Large powerful enemies
   - Unique boss abilities and mechanics
   - Challenge and reward
   - Strategic combat planning

4. **Dungeon Combat**
   - Combat within dungeon environment
   - Environmental hazards and traps
   - Combat positioning considerations
   - Dungeon challenge and exploration

### 2.3 Character Progression System

#### Progression from Level 1 to 100

1. **Early Game (Levels 1-20)**
   - Basic skills and abilities
   - Acquire combat and gathering skills
   - Basic dungeon exploration
   - Initial character customization
   - Character building begins

2. **Mid Game (Levels 21-50)**
   - More advanced skills and abilities
   - Dungeon expansion and complexity
   - Faction quests and reputation
   - Guild member progression
   - Skill specialization opportunities

3. **Late Game (Levels 51-80)**
   - Legendary and epic abilities
   - Advanced dungeons and bosses
   - Large-scale conquest and army building
   - Powerful weapons and armor
   - Endgame content and challenges

4. **Endgame (Levels 81-100)**
   - Ultimate and divine abilities
   - World domination and conquest
   - Necromantic power maximum
   - Complete character power potential
   - Final dungeon and boss fight

#### Experience and Growth

1. **Experience Points**
   - Gain XP from defeating enemies
   - XP from quest completion
   - XP from exploration and discovery
   - XP from crafting and gathering

2. **Level Up Rewards**
   - Character stat increases
   - Skill points for skill development
   - Ability upgrades
   - Equipment slots

3. **Specialization System**
   - Combat specialization: warrior or caster
   - Ranged specialization with bows, spells
   - Stealth and combat specialization
   - Magic specialization
   - Choose specialization path

#### Character Classes and Specializations

1. **Undead Warrior**
   - Strong physical combat capability
   - High defense and survivability
   - Melee weapon mastery
   - Warrior stance specialization
   - Dark combat skills

2. **Undead Caster**
   - Powerful necromantic and magical abilities
   - Strong ranged attack capability
   - Magic mastery and spell power
   - Caster stance specialization
   - Necromantic spell specialization

3. **Undead Ranger**
   - Ranged combat specialist, ranged skills
   - Stealth and tactical abilities
   - Bow and weapon skills
   - Combat and survival specialization
   - Assassin and ranger skills

4. **Undead Mage**
   - Generalist magical abilities
   - Combat and support magic
   - Versatile skill set
   - Magic specialization
   - Elemental and necromantic spells

5. **Undead Berserker**
   - High damage dealing combatant
   - Rage and intensity based combat
   - Melee and combat abilities
   - Overwhelming offensive capability
   - Close combat specialization

#### Skill and Ability Development

1. **Combat Skills**
   - Melee combat skills: axes, swords, spears
   - Ranged combat skills: bows, crossbows
   - Magic combat skills: various spell schools
   - Defensive combat skills: blocks, parries, dodges

2. **Gathering Skills**
   - Mining, herbalism, harvesting
   - Resource gathering abilities
   - Crafting resource collection
   - Exploration skill bonuses

3. **Crafting Skills**
   - Weapon crafting skills
   - Armor crafting skills
   - Magic item crafting
   - Consumable creation skills

4. **Knowledge Skills**
   - Information gathering and research
   - Language skills for NPC interactions
   - Exploration and discovery skills
   - Quest and mission intelligence

5. **Undead Skills**
   - Necromantic abilities
   - Skeleton summoning skills
   - Soul manipulation abilities
   - Death magic spells

### 2.4 Inventory and Crafting System

#### Inventory System

1. **Diablo-Style Inventory**
   - Grid-based inventory with slots
   - Item categories organized
   - Quality tiers and item levels
   - Different item rarities and importance

2. **Item Categories**
   - Weapons category: swords, axes, bows, etc.
   - Armor category: helmets, chest armor, gloves, etc.
   - Clothing category: shirts, pants, boots, etc.
   - Consumable category: potions, foods, etc.
   - Material category: ores, gems, herbs, etc.

3. **Item Quality and Level**
   - Common items: basic equipment
   - Uncommon items: slightly better
   - Rare items: exceptional quality
   - Epic items: powerful and rare
   - Legendary items: powerful and very rare

4. **Equipment Slots**
   - Main hand weapon slot
   - Off-hand weapon slot or shield
   - Chest armor slot
   - Helmet slot
   - Gloves slot
   - Boots slot
   - Accessory slot for rings/amulets

#### Crafting and Equipment Systems

1. **Crafting System**
   - Weapons crafting skill
   - Armor crafting skill
   - Magic item crafting
   - Consumable creation
   - Equipment enhancement and modification

2. **Purchase and Craft Options**
   - Buy items from shops and vendors
   - Craft items from collected materials
   - Upgrade and modify existing equipment
   - Enchant and enhance items

3. **Loot System**
   - Loot from defeated enemies
   - Loot from dungeons and bosses
   - Loot from chests and containers
   - Treasure and discovery opportunities

4. **Equipment Management**
   - Equipment and item equipping
   - Item removal and customization
   - Equipment stats and bonuses
   - Item management and organization

#### Item Enhancement and Modification

1. **Equipment Enhancement**
   - Add magical properties to equipment
   - Enchant and socket system
   - Quality upgrade options
   - Customization and personalization

2. **Socket System**
   - Socketed items with magical gem slots
   - Gem-based equipment enhancement
   - Socket placement for specific bonuses
   - Gem management and trading

3. **Item Customization**
   - Personalize equipment appearance
   - Color and design customization
   - Equipment upgrades and modifications
   - Status effect and effect customization

4. **Item Upgrades**
   - Quality upgrades for existing items
   - Upgrade materials and costs
   - Upgrade options for specific equipment types
   - Upgrade progression and goals

### 2.5 Dungeon Builder System Mechanics

#### Grid-Based Dungeon Building

1. **Grid System Basis**
   - Grid-based map construction
   - Modular room placement
   - Room connection and layout
   - Dungeon floor planning

2. **Modular Rooms**
   - Basic room types: chambers, corridors, walls
   - Special rooms: torture chambers, libraries, altars
   - Room size and configuration choices
   - Room placement and arrangement

3. **Dungeon Floor Planning**
   - Multi-floor dungeon structure
   - Floor-to-floor connections
   - Dungeon layout and design
   - Dungeon flow and progression

4. **Resource Constraints**
   - Limited resource management
   - Gold and resources for building
   - Resource gathering and production
   - Resource optimization

#### Building Resources

1. **Building Resources**
   - Gold for building components
   - Materials for construction
   - Dungeon resources for upgrades
   - Soul power for special construction

2. **Resource Production**
   - Gold production from dungeons
   - Resource generation systems
   - Dungeon resource income
   - Resource management and optimization

3. **Building Costs**
   - Cost of building rooms and structures
   - Resource cost of upgrades and enhancements
   - Resource distribution and allocation
   - Building budget and planning

4. **Resource Optimization**
   - Efficient dungeon layout
   - Resource collection optimization
   - Building improvement and efficiency
   - Resource waste reduction

#### Dungeon Room Types

1. **Basic Rooms**
   - Chambers: sleeping areas, meeting rooms
   - Corridors: dungeon paths and passages
   - Walls: dungeon boundaries and protection
   - Basic room functionality

2. **Function Rooms**
   - Training rooms: combat training area
   - Research rooms: magic study and discovery
   - Crafting rooms: item creation capabilities
   - Resource rooms: resource gathering and storage

3. **Special Rooms**
   - Torture chambers: enemy and player punishment
   - Libraries: ancient knowledge and spells
   - Altars: necromantic rituals and powers
   - Summoning circles: skeleton and monster summoning

4. **Defensive Rooms**
   - Barracks: skeleton army training
   - Armory: weapons and equipment storage
   - Guard rooms: skeleton guards and sentinels
   - Defensive structures: traps and obstacles

#### Player Home Base Building

1. **Graveheart Citadel (Player Home)**
   - Player's main dungeon fortress
   - Customizable home base and headquarters
   - Home base functions and features
   - Personalization and customization

2. **Home Base Features**
   - Living quarters for NPC undead
   - Library for research and knowledge
   - Altars for necromantic power and rituals
   - Training and weapon crafting areas

#### Dungeon Building Progress

1. **Initial Dungeon**
   - Basic starting dungeon layout
   - Basic rooms and structure
   - Essential dungeon functionality
   - Basic dungeon construction planning

2. **Advanced Dungeon**
   - Expanding and upgrading dungeon
   - Complex dungeon layouts
   - Additional rooms and special areas
   - Advanced dungeon construction

3. **Final Dungeon**
   - Ultimate fortress and dungeon
   - Complete dungeon customization
   - Maximum dungeon capabilities
   - Final dungeon construction goals

### 2.6 Army Management and Tactical View

#### Army Management System

1. **Army Formation**
   - Skeleton army troops organized and structured
   - Army hierarchy and organization
   - Army composition and balance
   - Army command and control

2. **Army Types**
   - Basic skeleton infantry
   - Armored skeleton warriors
   - Skeleton archers and ranged units
   - Skeleton knights and cavalry
   - Special skeleton units and abilities

3. **Army Composition**
   - Mix of different skeleton unit types
   - Army balance based on mission
   - Army size and capability
   - Army customization and specialization

4. **Army Roster and Management**
   - Army tracking and management
   - Army status and condition
   - Army assignment and deployment
   - Army training and development

#### Tactical Army Combat View

1. **Tactical View Mode**
   - Strategic army combat view
   - Strategic battlefield tactical view
   - Tactical deployment and movement
   - Tactical combat planning

2. **Tactical Army View**
   - Top-down tactical view
   - Battle map deployment
   - Army positioning and placement
   - Tactical battlefield control

3. **Army Combat Mechanics**
   - Tactical army combat
   - Army battle simulation
   - Tactical combat scenarios
   - Army combat outcomes

4. **Strategic Deployment**
   - Army deployment strategy
   - Army tactical placement
   - Strategic battle planning
   - Army deployment scenarios

### 2.7 Guild System with NPC-Directed Quest Flow

#### Guild Structure and Ranks

1. **Guild Organization**
   - Guild hierarchy: leader, officers, members
   - Guild structure and organization
   - Guild governance and administration
   - Guild social structure

2. **Guild Ranks**
   - Initiate: Beginning guild membership
   - Member: Full guild membership
   - Veteran: Experienced guild member
   - Officer: Guild leadership role
   - Guildmaster: Guild leader and authority
   - Similar progression to Skyrim guilds

3. **Different Guild Types**
   - Mage Guild: Magic and spell advancement
   - Warrior Guild: Combat skills and martial arts
   - Trade Guild: Business and economy skills
   - Thief/Assassin Guild: Stealth and skill advancement
   - Other specialized guilds and organizations

#### NPC-Driven Quest System

1. **NPC Quest System**
   - NPCs who issue quests and missions
   - Quest types and missions
   - Quest rewards and effects
   - Quest-driven NPC interactions

2. **NPC Quest Givers**
   - Guild NPCs who provide quests
   - Faction NPCs with missions
   - Quest completion NPCs
   - Quest information and tracking

3. **NPC Quest Completion**
   - NPCs complete player-issued tasks
   - NPC task completion mechanics
   - NPC success and failure based on abilities
   - NPC abilities and attributes

4. **NPC Karma and Reputation**
   - NPC character stats: abilities, karma, loyalty
   - NPC performance and success rates
   - NPC karma effects on player relationships
   - NPC karma and quest outcomes

#### Guild Quest Flow

1. **Guild Quest System Overview**
   - NPCs with guild quests and missions
   - Quest issuance and tracking
   - Quest rewards and guild progression
   - Quest-driven guild advancement

2. **NPC Task Issuing**
   - NPCs who issue tasks and missions
   - Different NPC types and their tasks
   - Task difficulty and requirements
   - NPC task issuance logic

3. **NPC Quest Completion Flow**
   - NPCs complete completed tasks
   - NPC success factors: abilities, karma, player support
   - NPC failure possibilities and consequences
   - NPC quest completion system

4. **NPC Karma and Player Effect**
   - NPC karma influences and effects
   - Evil NPC karma and player targeting
   - Good NPC karma and player reputation
   - NPC karma consequences and relationships

#### Guild Progression

1. **Guild Membership Progression**
   - Guild rank progression and advancement
   - Guild mission completion requirements
   - Guild reputation and standing
   - Guild power and influence

2. **Guild Quest Benefits**
   - Quest completion rewards
   - Guild reputation and standing improvements
   - Guild membership privileges and benefits
   - Guild power and influence growth

3. **Guild Mission Rewards**
   - Rewards from completed quest missions
   - Guild progression rewards
   - Guild reputation rewards
   - Guild power and influence rewards

4. **Guild Power and Influence**
   - Guild rank-based power and influence
   - Guild influence on world and NPCs
   - Guild power effects and benefits
   - Guild authority and command

### 2.8 Karma System and Consequences

#### Karma System Basics

1. **Karma Definition**
   - Player karma system: good and evil alignment
   - Karma based on actions and choices
   - Karma influences and consequences
   - Player alignment and moral choices

2. **Karma Sources**
   - NPCs killed and actions taken
   - Quest choices and mission completion
   - Dungeon building and combat actions
   - Party and army interactions

3. **Karma Effects**
   - NPC relationships and reputation
   - Quest outcomes and availability
   - World reactions and faction standing
   - Combat and adventure effects

#### Karma Impacts

1. **NPC Interactions**
   - Good-aligned NPCs positive relationships
   - Evil-aligned NPCs negative relationships
   - NPC quest availability and rewards
   - NPC trust and cooperation

2. **Faction Relationships**
   - Good faction standing for good karma
   - Enemy faction standing for evil karma
   - Faction quest and mission availability
   - Faction power and influence effects

3. **Quest Outcomes**
   - Karma affects mission results
   - Quest completion based on karma alignment
   - Karma-based quest choices and consequences
   - Karma consequences in main story

4. **Player Reputation**
   - Personal reputation in world
   - Player fame and infamy
   - Reputation effects on NPCs and factions
   - Reputation-based rewards and consequences

#### Karma Consequences

1. **Positive Karma Consequences**
   - Good NPC relationships and acceptance
   - Good faction standing and benefits
   - Quest availability and rewards
   - Improved world interactions

2. **Negative Karma Consequences**
   - Evil NPC hostility and attacks
   - Enemy faction standing and dangers
   - Quest difficulties and restrictions
   - World hostility and threats

3. **Karma-Based Combat**
   - Karma effects on combat
   - NPC reaction to combat actions
   - Karma-based enemy behavior
   - Combat and world consequences based on actions

### 2.9 Economy and Trade Systems

#### Trading Mechanics

1. **Trading System**
   - Shop and vendor interactions
   - NPC trading and barter
   - Player-to-player trading
   - Market and trade system

2. **Merchant Interactions**
   - Shopkeeper NPCs with item inventories
   - Different shops and vendors per region
   - Shop upgrades and expansions
   - Merchant relationships and discounts

3. **Market System**
   - Marketplaces and trade centers
   - Player trading and market functionality
   - Global and regional markets
   - Trading economy

4. **Trade Routes**
   - NPC trade routes and caravans
   - Trade between settlements
   - Trade route logistics and management
   - Trade route profitability

#### Resource and Market Systems

1. **Resource Types**
   - Craft materials: ores, gems, herbs, etc.
   - Goods and consumables
   - Equipment and weapons
   - Magical items and special materials

2. **Resource Economy**
   - Resource supply and demand
   - Resource pricing and market values
   - Resource scarcity and value
   - Resource trading and speculation

3. **Market Dynamics**
   - Market fluctuations and dynamics
   - Trading opportunities and advantages
   - Market arbitrage and profit opportunities
   - Economic optimization

4. **Economy System**
   - Overall game economy
   - Money and resource management
   - Economic opportunities
   - Economic influence

### 2.10 Exploration and Travel Systems

#### World Exploration

1. **World Map**
   - World map and region overview
   - Map locations and landmarks
   - Map navigation and exploration
   - World map features and system

2. **Terrain Types**
   - Various terrain: plains, forests, mountains, cities
   - Terrain-specific challenges and benefits
   - Terrain exploration opportunities
   - Terrain-related content and activities

3. **Travel Methods**
   - On-foot exploration
   - Travel between regions
   - Mount usage for faster travel
   - Teleportation options

4. **Exploration Features**
   - Discovery and exploration
   - Hidden locations and secrets
   - World exploration rewards
   - Exploration system and progression

#### Location System

1. **Player Movement**
   - Free character movement
   - Point-to-point travel
   - Character speed and stamina
   - Movement mechanics

2. **Travel Mechanics**
   - Travel between areas
   - Travel time and distance
   - Travel challenges and obstacles
   - Travel system

3. **Dungeon and Town Travel**
   - Dungeon exploration and travel
   - Town and city exploration
   - Location-specific events
   - Location-based content

4. **Travel Rewards and Content**
   - Travel-based rewards and opportunities
   - Exploration rewards and discoveries
   - Travel-related content and challenges
   - Travel system rewards

### 2.11 NPC Management and Leveling

#### NPC Character System

1. **NPC Creation and Management**
   - NPC character names and backstories
   - NPC appearance and appearance customization
   - NPC abilities and skill attributes
   - NPC stats and capabilities

2. **NPC Naming System**
   - Unique NPC names and naming conventions
   - NPC name tracking and uniqueness enforcement
   - Naming rules and naming system
   - Name organization and management

3. **NPC Leveling System**
   - NPC character leveling from 1 to 100
   - NPC experience and progression
   - NPC level growth and rewards
   - NPC advancement and development

4. **NPC Skills and Abilities**
   - NPC skills and abilities
   - NPC skill tree customization
   - NPC ability development and progression
   - NPC specializations and building

#### NPC Relationship and Management

1. **NPC Interaction System**
   - NPC interactions and relationships
   - NPC relationship management
   - NPC behavior and interactions
   - NPC relationship system

2. **NPC Karma and Relationship**
   - NPC karma and relationships
   - NPC relationship tracking
   - NPC relationship effects and consequences
   - Relationship management and optimization

3. **NPC Assignment and Deployment**
   - NPC assignment and deployment
   - NPC use and utilization
   - NPC assignment benefits and effects
   - NPC management and optimization

4. **NPC Management Tools**
   - NPC management interface
   - NPC roster and management tools
   - NPC organization and control
   - NPC management optimization

5. **NPC Backstories and Personalities**
   - NPC unique backstories
   - NPC personality traits
   - NPC personal motives and goals
   - NPC social relationships

---

## 3. ART DIRECTION

### 3.1 Pixel Art Style Guidelines

#### Visual Style Approach

1. **Pixel Art Foundation**
   - Hand-crafted pixel art for all game elements
   - Careful pixel-level design for clear visibility
   - Consistent art style across all game elements
   - Pixel-art aesthetic for visual simplicity and charm

2. **Dark Medieval Fantasy Color Palette**
   - Dark and muted colors with high contrast
   - Atmospheric lighting effects
   - Color-coded regions and environments
   - Consistent tonal approach

3. **Pixel Scale and Resolution**
   - Standard pixel scale for character art
   - Appropriate resolution for game elements
   - Clear visual hierarchy and readability
   - Optimized performance and clarity

#### Art Style Guidelines

1. **Character Art**
   - Detailed but clear character sprite sets
   - Different color palettes for variations
   - Animated idle, walk, and combat animations
   - Clear character distinguishability

2. **Environment Art**
   - Detailed pixel environments and backgrounds
   - Atmospheric dungeon and town environments
   - Dynamic weather and lighting effects
   - Consistent regional artistic style

3. **Particle Effects**
   - Pixel-based particle systems
   - Effective visual feedback for attacks
   - Magic and combat visual effects
   - Impactful and clear particle effects

### 3.2 Character Design Guidelines

#### Player Character Design

1. **Undead Player Character**
   - Skeleton design and appearance
   - Always remain skeleton, never change species
   - Bone structure and skeletal design guidelines
   - Consistent skeletal appearance across forms

2. **Character Customization**
   - Customizable weapons and equipment
   - Customizable armor and clothing
   - Customizable appearance beyond skeletal form
   - Character customization depth and options

3. **Character Customization Details**
   - Armor design customization
   - Clothing and gear customization
   - Weapon appearance customization
   - Item customization options

#### NPC Design Guidelines

1. **NPC Character Design**
   - Unique character designs for NPC types
   - Distinct visual designs for different NPC factions
   - Unique NPC designs and variations
   - Visual variety among NPC types

2. **Undead NPC Design**
   - Undead NPC visual variety
   - Different undead types and appearances
   - Undead character design guidelines
   - Undead appearance customization

3. **Living NPC Design**
   - Living NPC character designs
   - NPC character design diversity and variety
   - Living NPC unique designs
   - Living NPC customization options

### 3.3 Environment Design

#### Dungeon Design

1. **Dungeon Architecture**
   - Dark, atmospheric dungeon environments
   - Detailed dungeon rooms and hallways
   - Atmospheric dungeon lighting and effects
   - Dungeon architectural style consistency

2. **Regional Dungeon Environments**
   - Different dungeon styles per region
   - Regional dungeon design guidelines
   - Unique dungeon environments
   - Regional dungeon variety

3. **Dungeon Decor and Details**
   - Decorative dungeon elements and features
   - Dungeon details and atmospheric elements
   - Dungeon environmental storytelling
   - Dungeon visual depth

#### Town and World Design

1. **Town Environments**
   - Detailed pixel towns and villages
   - Town architectural styles and variety
   - Town interior and exterior environments
   - Town environmental details

2. **World Geography and Landscapes**
   - Detailed world geography
   - Regional environmental design
   - World map and landscape styles
   - Environmental storytelling

3. **Environmental Variety**
   - Regional environmental variety
   - Environmental storytelling and details
   - World exploration and discovery
   - Environmental depth and variety

### 3.4 UI and HUD Design

#### Main Interface

1. **Player Interface**
   - Health and energy display
   - Player status and information
   - Inventory and equipment display
   - Player navigation and movement

2. **Combat Interface**
   - Combat controls and indicators
   - Ability and skill display
   - Target identification system
   - Combat HUD and elements

3. **Quest and Navigation Interface**
   - Quest tracking system
   - Navigation and map system
   - Quest information display
   - Quest and navigation UI elements

#### Dialogue and Interface

1. **Dialogue System**
   - Dialogue interface and design
   - NPC interaction and dialogue system
   - Dialogue choices and options
   - Dialogue visual system

2. **Game Menu System**
   - Character customization menu
   - Inventory management interface
   - Guild and relationship menus
   - Game menu design and layout

3. **Tactical and Army Interface**
   - Tactical army view interface
   - Army management and deployment
   - Tactical interface and design
   - Army control and management screen

### 3.5 Effects and Particle Systems

#### combat Effects

1. **Combat Visual Effects**
   - Combat impact and feedback
   - Attack and ability visual effects
   - Magic spell visual effects
   - Damage and health effects

2. **Magic and Spell Effects**
   - Necromantic magic visual effects
   - Elemental magic spell effects
   - Magic spell visual feedback
   - Magic effect design

3. **Status and Healing Effects**
   - Status effect visual feedback
   - Health recovery and regeneration effects
   - Status effect UI and visual feedback
   - Healing and recovery visual effects

#### Dungeon and Environmental Effects

1. **Dungeon Effects**
   - Dungeon atmosphere and lighting effects
   - Dungeon environmental effects
   - Dungeon visual effects and feedback
   - Dungeon depth and atmosphere

2. **Environmental and Atmospheric Effects**
   - Atmospheric lighting effects
   - Environmental weather effects
   - Environmental particle effects
   - Environmental atmosphere and mood

3. **Impact and Feedback Effects**
   - Damage impact effects
   - Combat and dungeon feedback effects
   - Hit and miss visual effects
   - Impact-based effects and feedback

### 3.6 Sound Design Approach

#### Sound Design Strategy

1. **Audio Style**
   - Dark ambient music and sound effects
   - Atmospheric dungeon and combat audio
   - RPG-style sound design principles
   - Effective audio feedback and information

2. **Music and Audio Design**
   - Musical score and soundtrack
   - Ambient music and environmental sounds
   - Music and sound design consistency
   - Emotional and atmospheric audio

3. **Combat and Magic Sound**
   - Combat and attack sound effects
   - Magic spell and ability sounds
   - Necromantic magic and spell sounds
   - Combat audio system

#### Voice and Audio Effects

1. **Character Voices and Sound Effects**
   - Character sound effects and feedback
   - NPC voices and dialog audio
   - Character voice design
   - Character sound and audio effects

2. **Audio Interface and Feedback**
   - UI sound effects and feedback
   - Audio-based game feedback
   - Interactive audio system
   - Audio feedback for player actions

### 3.7 Color Palette and Lighting

#### Visual Color Design

1. **Dark Fantasy Color Palette**
   - Dark color scheme for dungeon and combat
   - Muted colors with strong contrasts
   - Dark medieval aesthetic colors
   - Atmospheric color and lighting effects

2. **Pixel Art Color Guidelines**
   - Pixel art-specific color design rules
   - Color-based visual information and feedback
   - Pixel art color implementation
   - Color-coded items and effects

#### Lighting and Atmospheric Effects

1. **Dungeon Lighting and Shadows**
   - Atmospheric dungeon lighting and shadows
   - Dark dungeon lighting effects
   - Dungeon lighting and shadow effects
   - Dungeon atmosphere and lighting

2. **Environmental Lighting Effects**
   - Environmental lighting and atmospheric effects
   - Regional lighting styles
   - World and dungeon lighting design
   - Lighting-based atmospheric effects

3. **Magic and Combat Lighting Effects**
   - Magic spell lighting effects
   - Combat lighting and atmosphere
   - Lighting-based combat feedback
   - Magic spell visual and lighting effects

**End of Game Design Document**

---

## DOCUMENT SUMMARY

### Core Game Elements

**Genre**: 2D Action RPG / Dungeon Management

**Main Character**: Undead skeleton, player identity hidden until powerful enough to take over world

**Core Systems**:

1. **Action Combat**: Action ARPG with dual-stance system (Caster/Warrior)
2. **Dungeon Builder**: Grid-based modular dungeon construction with resource constraints
3. **Army Management**: Tactical army combat and conquest mode
4. **Guild System**: NPC-driven guild quests with progression through ranks
5. **Character progression**: Level 1-100 with skills, abilities, and equipment
6. **Karma System**: Good/evil alignment with world interactions

### Key Game Features

- **Single-player campaign/story mode only** (no sandbox or online features)
- **Dark medieval fantasy pixel art** aesthetic
- **Slower, deeper progression** emphasizing effort and dedication
- **Unique character names and locations** throughout the world
- **Character always remains skeletal undead** - no species change

### Development Focus Areas

1. **Combat Feel**: Impactful and strategic combat systems
2. **Progression Depth**: Meaningful progression from level 1-100
3. **Dungeon Builder Complexity**: Deep and complex grid-based construction
4. **Guild Quest Flow**: NPC-driven mission system with tactical progression
5. **World Immersion**: Rich world-building and unique locations
6. **NPC Systems**: Meaningful NPC management and relationships
7. **Visual Style**: Consistent dark medieval fantasy pixel art aesthetic

### Target Release

**Platform**: PC

**Engine**: Godot 4.6+

**Release Platform**: PC distribution (Steam, etc.)

**Estimated Development Time**: Based on scope and complexity estimation based on similar games.