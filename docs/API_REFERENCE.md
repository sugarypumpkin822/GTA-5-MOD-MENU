# GTA 5 Mod Menu API Reference

---

## Table of Contents

1. [Introduction](#introduction)  
2. [Getting Started](#getting-started)  
3. [Initialization and Shutdown](#initialization-and-shutdown)  
4. [Core API Modules](#core-api-modules)  
   - 4.1 [Menu Management](#menu-management)  
   - 4.2 [Player Control](#player-control)  
   - 4.3 [Vehicle Control](#vehicle-control)  
   - 4.4 [World Interaction](#world-interaction)  
   - 4.5 [Memory and Process](#memory-and-process)  
   - 4.6 [Bypass & Anti-Cheat](#bypass--anti-cheat)  
   - 4.7 [Python Interface](#python-interface)  
5. [Events and Callbacks](#events-and-callbacks)  
6. [Error Handling](#error-handling)  
7. [Data Structures](#data-structures)  
8. [Advanced Usage](#advanced-usage)  
9. [Examples](#examples)  
10. [Changelog](#changelog)  
11. [FAQ](#faq)  
12. [Support](#support)  

---

## 1. Introduction

This document describes the complete programming interface for the **GTA 5 Mod Menu**. It provides functions, data structures, and usage patterns to interact programmatically with the mod menu, control gameplay features, and extend functionality.

---

## 2. Getting Started

To use the API:

- Include the header files in your project (`include/` directory).  
- Link against the mod menu core library (`lib/modmenu.lib` or equivalent).  
- Initialize the system with `ModMenu_Init()`.  
- Use provided APIs to manipulate game state or menu behavior.  
- Shutdown cleanly with `ModMenu_Shutdown()`.

---

## 3. Initialization and Shutdown

### `bool ModMenu_Init(void* gameHandle, ModMenuConfig* config);`

Initializes the mod menu system. Must be called before any other API functions.

- **Parameters:**  
  - `gameHandle` - Handle or pointer to the GTA 5 game process (platform-dependent).  
  - `config` - Pointer to configuration structure (see Data Structures).  

- **Returns:**  
  - `true` on successful initialization.  
  - `false` if initialization failed.  

---

### `void ModMenu_Shutdown();`

Shuts down the mod menu, releasing all resources.

---

## 4. Core API Modules

---

### 4.1 Menu Management

#### `bool Menu_Create(const char* title);`

Creates a new mod menu window with the specified title.

- **Parameters:**  
  - `title` - Null-terminated string for menu title.

- **Returns:**  
  - `true` if created successfully.  
  - `false` if creation failed.

---

#### `void Menu_Destroy();`

Destroys the current menu instance.

---

#### `void Menu_AddItem(const MenuItem* item);`

Adds an item to the menu.

- **Parameters:**  
  - `item` - Pointer to a `MenuItem` structure (see Data Structures).

---

#### `void Menu_Show();`

Displays the menu in-game.

---

#### `void Menu_Hide();`

Hides the menu.

---

#### `bool Menu_IsVisible();`

Returns whether the menu is currently visible.

- **Returns:**  
  - `true` if visible, `false` otherwise.

---

### 4.2 Player Control

#### `bool Player_SetHealth(int health);`

Sets the player's health.

- **Parameters:**  
  - `health` - Integer health value (0–100).

- **Returns:**  
  - `true` if successful, `false` otherwise.

---

#### `int Player_GetHealth();`

Returns the current player health.

---

#### `bool Player_SetPosition(float x, float y, float z);`

Sets player position in the world.

- **Parameters:**  
  - `x`, `y`, `z` - Coordinates in world space.

---

#### `void Player_GiveWeapon(int weaponId, int ammoCount);`

Gives the player a weapon.

- **Parameters:**  
  - `weaponId` - Weapon identifier (see Weapon IDs).  
  - `ammoCount` - Number of ammo rounds.

---

### 4.3 Vehicle Control

#### `bool Vehicle_Spawn(int modelHash, float x, float y, float z);`

Spawns a vehicle at given coordinates.

---

#### `void Vehicle_SetSpeed(float speed);`

Sets current vehicle speed.

---

#### `bool Vehicle_SetColor(int colorPrimary, int colorSecondary);`

Sets vehicle paint colors.

---

### 4.4 World Interaction

#### `void World_SetTime(int hour, int minute);`

Changes the in-game time.

---

#### `void World_SpawnNPC(int modelHash, float x, float y, float z);`

Spawns a non-player character.

---

### 4.5 Memory and Process

#### `bool Memory_Write(void* address, const void* buffer, size_t size);`

Writes bytes to a memory address in the game process.

---

#### `bool Memory_Read(void* address, void* buffer, size_t size);`

Reads bytes from a memory address.

---

### 4.6 Bypass & Anti-Cheat

#### `bool Bypass_Init();`

Initializes anti-cheat bypass modules.

---

#### `bool Bypass_IsActive();`

Returns whether bypass is currently active.

---

### 4.7 Python Interface

#### `bool Python_RunScript(const char* scriptPath);`

Executes a Python script in the mod menu context.

---

## 5. Events and Callbacks

### `typedef void (*MenuCallback)(MenuItem* item);`

Function pointer type for menu item callbacks.

---

### `void Menu_SetOnItemSelected(MenuCallback callback);`

Sets a callback invoked when a menu item is selected.

---

### Game Event Hooks

- `OnPlayerDamage`  
- `OnVehicleSpawn`  
- `OnMenuToggle`  

(Events provide hooks to integrate custom behaviors.)

---

## 6. Error Handling

API functions return `bool` or status codes. Use `ModMenu_GetLastError()` to get detailed error information.

---

## 7. Data Structures

### `typedef struct {`

```c
    int id;
    const char* name;
    MenuItemType type;
    union {
        int intValue;
        float floatValue;
        const char* strValue;
        bool boolValue;
    } value;
    MenuCallback callback;
} MenuItem;
typedef struct {
c
Copy
Edit
    bool enableDebug;
    int maxMenuItems;
    const char* defaultScriptPath;
} ModMenuConfig;'''


















8. Advanced Usage
Dynamic menu creation with runtime scripting.

Custom memory patches and detours.

Integration with external Python automation.

9. Examples
Example 1: Initialize and Create Menu
c
Copy
Edit
ModMenuConfig config = {true, 50, "./scripts/default.py"};
if (!ModMenu_Init(gameHandle, &config)) {
    printf("Failed to initialize mod menu\n");
    return -1;
}
Menu_Create("Main Mod Menu");
Menu_Show();
Example 2: Add a Toggle Item
c
Copy
Edit
MenuItem godMode = {
    .id = 1,
    .name = "God Mode",
    .type = MENU_ITEM_TOGGLE,
    .value.boolValue = false,
    .callback = OnGodModeToggle
};
Menu_AddItem(&godMode);
10. Changelog
v1.0 Initial release with core API

v1.1 Added Python interface and vehicle control

v1.2 Enhanced anti-cheat bypass status functions

v1.3 Added event callbacks for menu interactions

# 11. FAQ
Q: How do I extend the menu?
A: Use Menu_AddItem() and callbacks to dynamically add features.

Q: Is online modding supported?
A: Modifying online is risky and not officially supported.

12. Support
Report issues via GitHub issues.

Join the Discord community (link in project README).

Submit pull requests with improvements.

End of API Reference.

yaml
Copy
Edit

---

If you'd like, I can also generate example Python bindings or detailed enum lists for weapons, vehicles, and more! Just ask!
