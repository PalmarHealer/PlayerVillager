# Resource Pack Configuration Summary

This resource pack has been configured to only apply custom villager models and textures to villagers named "Wache".

## Requirements
- **Entity Texture Features (ETF)** mod must be installed: https://modrinth.com/mod/entitytexturefeatures
- OptiFine or a compatible mod (like ETF)

## What Was Changed

### 1. Removed ALL Base Textures
- Deleted all files from `textures/entity/villager/` that would apply to ALL villagers
- This includes: villager.png, profession/*.png, profession_level/*.png, type/*.png
- Now ONLY random textures with name filters are used

### 2. CEM Model Filtering
- Created `villager.jem.properties` with `name=Wache` filter
- The custom entity model (villager.jem) will ONLY apply to villagers named "Wache"

### 3. Texture Filtering
All random entity texture properties files have been updated with `name.X=Wache` filters:
- Main villager textures (175+ variants)
- Profession-specific textures (farmer, librarian, cleric, etc.)
- Type-specific textures (plains, desert, jungle, snow, savanna, swamp, taiga)
- Profession level textures (tools for different levels)

### 4. Files Modified
- `pack.mcmeta` - Updated description
- `villager.jem.properties` - CEM name filter
- `villager.properties` - Added name filters
- All profession/*.properties files - Added name filters
- All type/*.properties files - Added name filters
- `profession_level/villager_tool.properties` - Added name filters

### 5. Files Removed
- All base texture files that would apply to every villager
- This ensures normal villagers remain completely vanilla

## How to Use
1. Install Entity Texture Features mod
2. Enable this resource pack in your game
3. Reload resources (F3+T)
4. Use a name tag to name a villager exactly "**Wache**"
5. Only that villager will have the custom player-like model and textures
6. All other villagers will remain completely vanilla

## Testing
To test if it's working:
1. Name a villager "Wache" using a name tag
2. The villager should have a custom player-like model with custom textures
3. Create another villager without the name - it should be completely normal/vanilla
4. If normal villagers still show custom textures, press F3+T to reload resources

## Troubleshooting
- If it's not working at all: Make sure ETF mod is installed
- If normal villagers have custom textures: Press F3+T to reload the resource pack
- If "Wache" villagers don't have custom model: Check that the name is exactly "Wache" (case sensitive)
