# Player Villagers Resource Pack

## What This Pack Does

This resource pack allows you to give Minecraft villagers **custom player-like models** by naming them with specific name tags. 

- **Named Villagers** ("Guard" or "Wache") → Custom player-like model with custom texture
- **Unnamed Villagers** → Normal vanilla Minecraft villagers (unaffected)

---

## Requirements

- **OptiFine** OR **Entity Model Features (EMF)** mod
- Minecraft 1.14+

---

## How to Use

### Step 1: Name a Villager
1. Get a name tag
2. Rename it at an anvil to: **"Guard"** or **"Wache"**
3. Right-click on a villager with the name tag
4. The villager will now have a custom player-like model!

### Step 2: Reload Resources
Press **F3 + T** in-game to reload resources after applying name tags.

---

## How It Works (Technical)

The pack uses **OptiFine's Custom Entity Models (CEM)** to replace villager models based on name tags.

### File Structure
```
assets/minecraft/
├── optifine/cem/
│   ├── villager.properties      # Model selection rules
│   └── villager2.jem           # Custom player-like model
└── textures/entity/villager/
    └── guard.png                # Custom texture for the model
```

### villager.properties (Model Selection)
```properties
# When a villager is named "Guard", use model 2 (villager2.jem)
models.2=2
name.2=regex:Guard|.*\\(Guard\\)|\\(Guard\\).*

# When a villager is named "Wache", use model 2 (villager2.jem)
models.3=2
name.3=regex:Wache|.*\\(Wache\\)|\\(Wache\\).*
```

**Key Point:** Model 1 is NOT defined (no `models.1=...`), so unnamed villagers automatically use the vanilla model.

### villager2.jem (Custom Model)
The model file defines a player-like structure with:
- Player-style head, body, arms, and legs
- Direct texture reference: `"texture": "textures/entity/villager/guard.png"`
- Animations for walking and idle movement

---

## Adding More Custom Villagers

### Option 1: Add More Names (Same Model & Texture)

Edit `villager.properties` to add more names:

```properties
# Existing entries
models.2=2
name.2=regex:Guard|.*\\(Guard\\)|\\(Guard\\).*

models.3=2
name.3=regex:Wache|.*\\(Wache\\)|\\(Wache\\).*

# Add new names (uses same model)
models.4=2
name.4=regex:Soldier|.*\\(Soldier\\)|\\(Soldier\\).*

models.5=2
name.5=regex:Knight|.*\\(Knight\\)|\\(Knight\\).*
```

Now villagers named "Soldier" or "Knight" will also use the same custom model and texture.

---

### Option 2: Add Different Model/Texture for Different Names

#### Step 1: Create New Model File
Copy `villager2.jem` to `villager3.jem` and modify as needed.

#### Step 2: Create New Texture
Add your new texture: `textures/entity/villager/merchant.png`

#### Step 3: Update villager3.jem
Edit the texture reference in `villager3.jem`:
```json
{
	"texture": "textures/entity/villager/merchant.png",
	"textureSize": [64, 64],
	"models": [ ... ]
}
```

#### Step 4: Add Model Rule
Add to `villager.properties`:
```properties
# Merchant uses model 3 (villager3.jem with merchant.png)
models.6=3
name.6=regex:Merchant|.*\\(Merchant\\)|\\(Merchant\\).*
```

---

## Custom Sounds

### Removing Villager Sounds

Custom model villagers (Guard, Wache) have their sounds removed by default. This is configured in:
```
assets/minecraft/optifine/random/entity/villager/villager.properties
```

All villager sounds are set to `none`:
- Ambient (idle sounds)
- Trade sounds
- Yes/No sounds
- Death sounds
- Hurt sounds
- Work sounds (all professions)

### Adding Custom Sounds

If you want custom sounds instead of silence:

#### Step 1: Create Sound Files
Place your sound files in:
```
assets/minecraft/sounds/entity/villager/custom/
```

Sound files must be `.ogg` format (Minecraft requirement).

#### Step 2: Create sounds.json
Create `assets/minecraft/sounds.json`:
```json
{
  "entity.villager.custom.ambient": {
    "sounds": ["entity/villager/custom/ambient1"]
  },
  "entity.villager.custom.hurt": {
    "sounds": ["entity/villager/custom/hurt1"]
  },
  "entity.villager.custom.death": {
    "sounds": ["entity/villager/custom/death1"]
  }
}
```

#### Step 3: Update villager.properties
Change `none` to your custom sound:
```properties
sounds.ambient.1=entity.villager.custom.ambient
sounds.hurt.1=entity.villager.custom.hurt
sounds.death.1=entity.villager.custom.death
name.1=iregex:guard|wache|...
```

### Using Player Sounds

To make custom villagers sound like players:
```properties
sounds.ambient.1=none
sounds.hurt.1=entity.player.hurt
sounds.death.1=entity.player.death
name.1=iregex:guard|wache|...
```

---

## Creating Custom Textures

### Texture Requirements
- **Size:** 64x64 pixels
- **Format:** PNG
- **Layout:** Standard Minecraft villager texture layout

### Texture Location
Place your texture in:
```
assets/minecraft/textures/entity/villager/your_texture_name.png
```

### Reference in .jem
In your model file (e.g., `villager2.jem`):
```json
{
	"texture": "textures/entity/villager/your_texture_name.png",
	...
}
```

### Texture Tools
- **Paint.NET** - Free, easy to use
- **GIMP** - Free, more advanced
- **Photoshop** - Professional
- **Blockbench** - For 3D model editing and texturing

---

## Creating Custom Models

### Using Blockbench (Recommended)
1. Download **Blockbench**: https://www.blockbench.net/
2. Open `villager2.jem` in Blockbench
3. Modify the model (change proportions, add elements, etc.)
4. Export as `.jem` format
5. Save as a new file (e.g., `villager3.jem`)

### Model Requirements
- **Format:** JSON Entity Model (.jem)
- **Compatible with:** OptiFine CEM, Entity Model Features (EMF)

---

## Name Matching Patterns

The pack uses **regex patterns** to match villager names flexibly:

### Pattern Explanation
```properties
name.2=regex:Guard|.*\\(Guard\\)|\\(Guard\\).*
```

This matches:
- `Guard` - Exact name
- `My Pet (Guard)` - Name with prefix in parentheses
- `(Guard) Level 5` - Name with suffix
- `Town (Guard)` - Name with parentheses anywhere

### Case-Insensitive Matching
To match both "Guard" and "guard":
```properties
name.2=iregex:guard|.*\\(guard\\)|\\(guard\\).*
```

### Simple Exact Match
For exact name only (no variations):
```properties
name.2=pattern:Guard
```

---

## Current Configuration

### Active Names
- **"Guard"** → Custom player model + guard.png
- **"Wache"** → Custom player model + guard.png (same as Guard)

### Files
- `villager.properties` - Model selection rules
- `villager2.jem` - Custom player-like model
- `guard.png` - Custom texture (currently armorer placeholder)

### Vanilla Villagers
All villagers **without** matching name tags remain completely vanilla (normal Minecraft appearance).

---

## Troubleshooting

### Custom model not showing
1. Check name tag spelling (case-sensitive: "Guard" not "guard")
2. Press **F3 + T** to reload resources
3. Make sure OptiFine or EMF is installed
4. Verify resource pack is enabled in game settings

### Texture not loading
1. Check texture path in `.jem` file matches actual file location
2. Texture must be 64x64 PNG format
3. Press **F3 + T** after changing textures

### Model looks wrong
1. Verify `.jem` file is valid JSON (use JSON validator)
2. Check texture UV mapping matches texture layout
3. Use Blockbench to preview/edit the model

---

## Quick Reference

### Add a New Named Villager Type

1. **Same model, same texture:**
   - Add entry in `villager.properties`:
   ```properties
   models.X=2
   name.X=regex:YourName|.*\\(YourName\\)|\\(YourName\\).*
   ```

2. **Different model/texture:**
   - Copy `villager2.jem` → `villagerX.jem`
   - Create `your_texture.png` in `textures/entity/villager/`
   - Edit `villagerX.jem` texture reference
   - Add to `villager.properties`:
   ```properties
   models.X=X
   name.X=regex:YourName|.*\\(YourName\\)|\\(YourName\\).*
   ```

3. **Reload resources:** F3 + T

---

## Example: Adding a "Soldier" Villager

### Using Same Model (Quick)
Edit `villager.properties`:
```properties
models.4=2
name.4=regex:Soldier|.*\\(Soldier\\)|\\(Soldier\\).*
```
Done! "Soldier" villagers now use the same guard model/texture.

### Using Different Texture
1. Create `soldier.png` (64x64) → `textures/entity/villager/soldier.png`
2. Copy `villager2.jem` → `villager3.jem`
3. Edit `villager3.jem`:
   ```json
   {
       "texture": "textures/entity/villager/soldier.png",
       ...
   }
   ```
4. Edit `villager.properties`:
   ```properties
   models.4=3
   name.4=regex:Soldier|.*\\(Soldier\\)|\\(Soldier\\).*
   ```
5. Press F3+T in game

---

## Credits & License

- Based on "Player Villagers" concept
- Uses OptiFine Custom Entity Models (CEM)
- Compatible with Entity Model Features (EMF)

Feel free to modify and extend this pack for your own use!

---

**Version:** 2.1  
**Last Updated:** 2025-11-17  
**Minecraft Version:** 1.14+
