# Agents Guide

## Build, Run, and Test Commands

For Godot 4.6+ 2D games:

```bash
# Run the game in editor or export
godot --path . --run

# Export game
godot --headless --export-release "res://export.pck" output_release

# Run with debug mode
godot --path . --debug

# Run in headless mode for testing
godot --headless --path .

# Run with logging
godot --log-file=game.log --path .
```

## GDScript Coding Standards

### Naming Conventions
- **Scenes**: PascalCase (`player.tscn`, `platform.gd`)
- **Nodes**: PascalCase (preferred for scenes/nodes)
- **Scripts**: PascalCase (`PlayerController.gd`, `GameManager.gd`)
- **Variables**: camelCase (`playerVelocity`, `maxSpeed`)
- **Constants**: UPPER_SNAKE_CASE (`MAX_HEALTH`, `DEFAULT_GRAVITY`)
- **Signals**: snake_case (e.g., `player_died`, `enemy_hurt`)
- **Export**: snake_case or camelCase with underscore prefix

### Type Hints
```gdscript
var player_name: String = "Hero"
var health_points: float = 100.0
@export var max_speed: float = 200.0
@export_category("Combat")
@export var damage: int = 10
```

### Export Variables
```gdscript
@export var weapon_type: String = "rifle"
@export_range(1, 100) var armor_value: int = 50
@export_group("Player Stats")
@export var move_speed: float = 300.0
@export var jump_force: float = 400.0
@export_flag("Can Jump", "Can Dash") var abilities: int = 1
@export_multiline var quest_description: String
@export_directory var level_path: String
@export_file var prefab_path: String
```

### Signals
```gdscript
signal health_changed(new_health: float)
signal player_died
signal enemy_spawned(enemy: Enemy)

func _on_player_died() -> void:
    pass

func take_damage(amount: float) -> void:
    health -= amount
    health_changed.emit(health)
```

### Classes and Inheritance
```gdscript
class_name Actor extends Node2D

extends Node2D

@export var is_player: bool = false

func _ready() -> void:
    set_physics_process(true)

func _physics_process(delta: float) -> void:
    pass
```

### Signals Connection
```gdscript
func _ready() -> void:
    player.take_damage.connect(_on_player_take_damage)

func _exit_tree() -> void:
    if player:
        player.take_damage.disconnect(_on_player_take_damage)
```

### Godot Node Patterns
```gdscript
# Main Game Controller
extends Node2D

var game_state: GameData = null

func _ready() -> void:
    var save_data = load_game_data()
    game_state = GameData.new_from_dict(save_data)

# State Manager
class_name GameManager

signal state_changed(old_state: GameState, new_state: GameState)

enum GameState { MENU, PLAYING, PAUSED, GAME_OVER }

var current_state: GameState = GameState.MENU

# Entity Pattern
class_name Actor extends CharacterBody2D

var stats: ActorStats

var is_active: bool = true

func take_damage(amount: float) -> void:
    if not is_active: return
    # Handle damage

# Collision Handling
func _physics_process(delta: float) -> void:
    move_and_slide()

func _on_area_collision_entered(area: Area2D) -> void:
    pass

func _on_body_entered(body: Node2D) -> void:
    if body is Obstacle:
        handle_collision(body)
```

### Best Practices

#### Organize by Category
- **Audio/** - Sound effects, music
- **Enemies/** - Enemy scenes and scripts
- **Items/** - Power-ups, collectibles
- **Levels/** - Scene files
- **Managers/** - Global managers
- **Player/** - Player-related resources
- **UI/** - User interface scenes
- **VFX/** - Visual effects, particles
- **Resources/** - Item data, enemy stats, etc.

#### Resource and Scene Structure
```gdscript
# Resource structure (resources/)
# - ItemData.gd, EnemyData.gd, LevelData.gd
# - Each represents typed data with @export for editor use

# Scene structure
# - Player.tscn (with Player.gd script)
# - Enemy.tscn (with Enemy.gd script)
# - Level.tscn
```

#### Error Handling
```gdscript
func load_resource(path: String) -> Resource:
    var file = FileAccess.open(path, FileAccess.READ)
    if file == null:
        push_error("Failed to open: " + path)
        return null

    var data = decode_json(file.get_as_text())
    file.close()

    return Resource.new_from_dict(data)

# Use assertion and error handling in game logic
assert(level_count > 0, "Level count must be greater than 0")

# Console.log for debug, push_error for errors in editor
```

#### Constants and Config
```gdscript
const DEFAULT_GRAVITY: float = 980.0
const TERMINAL_VELOCITY: float = 1000.0
const TILE_SIZE: int = 64
const SAVE_FILE_PATH: String = "user://savegame.save"

# Or use config files for settings
# - options.cfg or settings.json
```

### Scene and Node Best Practices
- Use `Node2D` for 2D scenes, not `Node`
- Organize nodes with `Control` or containers for UI
- Keep inheritance shallow (prefer composition over deep inheritance)
- Use `_ready()` for initialization, not `_init()`
- Use `_physics_process()` for physics calculations
- Use `_process()` for general updates (unless physics is needed)

### Performance Tips
- Optimize collision layers and masks
- Use `Area2D` instead of `CollisionShape2D` for non-static objects
- Limit physics updates where possible
- Pool particle systems
- Use `@export` with `@export_range` for tuning values
- Disable `process` and `physics_process` when not needed using `set_process()` or `set_physics_process()`

### Code Comments
```gdscript
## Player entity that can move and jump
class_name Player extends CharacterBody2D

## Maximum horizontal speed in pixels/second
@export var max_speed: float = 300.0

func calculate_movement(delta: float) -> void:
    # Apply gravity
    velocity.y += gravity * delta

## Handle user input and movement logic
func get_input_direction() -> Vector2:
    return Vector2(
        Input.is_action_pressed("move_right") - Input.is_action_pressed("move_left"),
        Input.is_action_pressed("move_down") - Input.is_action_pressed("move_up")
    )
```

### File Naming
- Scenes: `player.tscn`, `enemy.gd`, `ui_start_menu.tscn`
- Scripts: `Player.gd`, `EnemyController.gd`, `GameManager.gd`
- Resources: `item_data.gd`, `enemy_data.gd`
- Constants/Enums: In main script or separate constants file

### Export Configuration
- Export project settings in `project.godot`
- Don't commit `local.settings` or player preferences
- Use `user://` for save files
- Document important project setting changes

### Testing
- Test physics interactions with `test_scene.tscn`
- Verify state transitions in game manager
- Test collision masks
- Validate save/load functionality

## Git Workflow Rules

This document outlines the git workflow conventions and rules for this project.

### Branch Naming Conventions

#### Main Branches
- `main` - The primary branch for stable, production-ready code
- `develop` - The primary development branch (if used)

#### Feature Branches
Use the following prefix followed by a descriptive name:
- `feature/` - New features (e.g., `feature/add-user-authentication`)
- `fix/` - Bug fixes (e.g., `fix/resolve-login-error`)
- `hotfix/` - Critical production fixes (e.g., `hotfix/security-vulnerability`)
- `docs/` - Documentation updates (e.g., `docs/update-readme`)
- `refactor/` - Code refactoring (e.g., `refactor/optimize-database-queries`)
- `test/` - Adding or updating tests (e.g., `test/add-unit-tests`)
- `chore/` - Maintenance tasks (e.g., `chore/update-dependencies`)

#### Branch Structure Example
```
main → develop
  ↓
feature/your-feature-name
  ↓
develop → main (after review and merge)
```

### Commit Message Format

Use the **Conventional Commits** format:

```
<type>(<scope>): <subject>

<body>

<footer>
```

#### Commit Types
- `feat`: A new feature
- `fix`: A bug fix
- `docs`: Documentation only changes
- `style`: Code style changes (formatting, semicolons, etc.)
- `refactor`: Code refactoring (no functional changes)
- `test`: Adding or updating tests
- `chore`: Maintenance tasks or dependency updates
- `perf`: Performance improvements
- `ci`: CI/CD configuration changes

#### Examples
```
feat(auth): add user login functionality

- Implement JWT authentication
- Add login and logout endpoints
- Create authentication middleware
- Update user model with login tracking

Closes #123
```

```
fix(api): resolve timeout in database queries

- Add connection pooling configuration
- Optimize query execution time
- Add error handling for database failures

Fixes #456
```

### Workflow Steps

#### 1. Fork and Setup
1. Clone the repository
2. Create a feature branch from the appropriate base branch
3. Make your changes

#### 2. Committing Changes
1. Write clear, descriptive commit messages following the format above
2. Use meaningful commit messages (explain the "why", not just the "what")
3. Ensure commits are atomic and focused on a single change

#### 3. Pull Request Process
1. Push your feature branch to the remote repository
2. Create a pull request with:
   - Clear title following `type(scope): description` format
   - Detailed description of changes
   - Related issues/commit references
   - Checklist for completeness (if applicable)
3. Wait for code review
4. Address review comments and feedback
5. Once approved, merge to the appropriate branch

#### 4. Merging
- Main branch: Only allow merges from Pull Requests
- Use "Squash and merge" for feature branches to keep commit history clean
- Use "Rebase and merge" only when maintaining a linear history is critical

#### 5. Release Process
1. Update version numbers in relevant files
2. Create a release branch if needed
3. Create a tag for the release
4. Merge release branch to main

### Code Review Guidelines

#### Before Creating a PR
- [ ] Write tests for new features or bug fixes
- [ ] Ensure all tests pass
- [ ] Code follows project style guidelines
- [ ] Update documentation if needed
- [ ] No console logs or debug code in production

#### During Code Review
- [ ] Review for clarity and readability
- [ ] Check for potential bugs or edge cases
- [ ] Verify performance implications
- [ ] Ensure proper error handling
- [ ] Confirm security best practices

### Branch Management

#### Keeping Branches Up to Date
- Before creating a PR, rebase your branch against the latest base branch
- If conflicts occur, resolve them and update your commit history

#### Branch Cleanup
- Delete feature branches after merging (local and remote)
- Keep release branches until the release is stable
- Archive branches for historical reference if needed

### Conflict Resolution

When conflicts occur during merge:
1. Pull the latest changes from the target branch
2. Resolve conflicts locally
3. Commit the resolution
4. Push and create/update the pull request

### Remote Repository

#### Branch Protection Rules (recommended)
- Require pull request reviews before merging
- Require status checks to pass
- Require branches to be up to date before merging
- Disable direct commits to protected branches

### Best Practices

1. **Commit frequently**: Small, frequent commits are easier to review
2. **Write good commit messages**: They tell the story of your changes
3. **Keep PRs focused**: One logical change per PR
4. **Test locally**: Ensure everything works before pushing
5. **Document complex changes**: Explain the rationale and approach
6. **Use descriptive branch names**: Make it clear what the branch contains
7. **Be respectful**: Code reviews should be constructive and helpful

### Additional Resources

- [Conventional Commits](https://www.conventionalcommits.org/)
- [Pro Git Handbook](https://git-scm.com/book/en/v2)
- [GitHub Flow](https://docs.github.com/en/get-started/quickstart/github-flow)

## Godot-Specific Examples for Git Commits

Follow Conventional Commits with GDScript context:

```
feat(gdscript): add player jump mechanics

- Implement double jump capability
- Add coyote time for better jump consistency
- Adjust gravity parameters for smoother movement

Closes #7
```

```
fix(godot): resolve collision detection overlap

- Change collision shape from CircleShape2D to CapsuleShape2D
- Reduce physics frames from 64 to 32 for better performance
- Update collision layer masks

Fixes #5
```

```
refactor(actor): consolidate player and enemy movement

- Extract common movement logic into Actor base class
- Use @export variables for tuning parameters
- Improve code reusability across entities

Closes #12
```

```
test(physics): add unit tests for collision resolution

- Create test scene with various collision shapes
- Verify player can pass through platforms correctly
- Test edge cases for narrow collision detection

Closes #13
```

```
chore(godot): update physics engine settings

- Increase max FPS cap to 60 for smoother gameplay
- Adjust simulation precision in project.godot
- Enable GPU acceleration for particle systems

```

Feature branches follow: `feature/description`