# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project Overview

This is a single-page web application for designing weaving patterns on multi-shaft looms. The entire application is contained in `loom-designer.html` - a standalone HTML file with embedded CSS and JavaScript (no build process or dependencies).

## Architecture

### State Management
The application uses a single global `state` object that tracks:
- Loom configuration (shafts, warpThreads, treadles, picks)
- Threading: 2D array `[warpThreads][shafts]` - maps each warp thread to a shaft
- Tie-up: 2D array `[treadles][shafts]` - maps treadles to shafts they lift
- Treadling: 2D array `[picks][treadles]` - sequence of treadle presses
- Colors: Arrays for `warpColors[warpThreads]` and `weftColors[picks]`

### Grid Layout Structure
The UI consists of four interconnected grids positioned in standard weaving draft layout:
```
         Threading (horizontal)
         ↓
Tie-Up → [top-right]

Drawdown ← (calculated)

         Treadling (vertical) →
```

**Important**: Color pickers are positioned alongside their respective grids:
- Warp colors: Horizontal bar above threading grid
- Weft colors: Vertical bar beside treadling grid

### Drawdown Calculation
The drawdown is **calculated automatically** from threading × tie-up × treadling:
1. For each pick/thread intersection, check which treadle is active in treadling
2. Look up which shafts that treadle lifts in tie-up
3. Check if the thread's shaft (from threading) is lifted
4. If lifted: display warp color; if down: display weft color

This is handled in `calculateDrawdownCell(pick, thread)` and `updateDrawdown()`.

## Key Functions

### Pattern Application
- `applyThreadingPattern()` - Applies preset threading patterns (straight, point, reverse)
- `applyTreadlingPattern()` - Applies preset treadling sequences
- `applyWarpColorPattern()` / `applyWeftColorPattern()` - Applies color schemes

### Grid Management
- `createGrid()` - Dynamically generates interactive grids with click handlers
- `createColorPickers()` - Generates color selector grids aligned with threading/treadling
- Grid click handlers use **single-selection model**: clicking a cell deselects others in that column/row

### Export/Import
Export format (JSON):
```json
{
  "version": "1.0",
  "settings": { shafts, warpThreads, treadles, picks },
  "threading": [...],
  "tieup": [...],
  "treadling": [...],
  "warpColors": [...],
  "weftColors": [...]
}
```

## Weaving Domain Knowledge

When modifying the application, understand these weaving concepts:
- **Threading**: Assignment of warp threads to shafts (typically each thread on one shaft)
- **Tie-up**: Which shafts lift together when a treadle is pressed
- **Treadling**: The sequence in which treadles are pressed during weaving
- **Drawdown**: The resulting fabric pattern (automatically calculated, never edited directly)

Common patterns:
- **Straight Draw**: Sequential assignment (1,2,3,4,1,2,3,4...)
- **Point Twill**: Up-and-down pattern (1,2,3,4,3,2,1,2,3,4...)
- **Reverse**: Backward sequence (4,3,2,1,4,3,2,1...)

## Testing the Application

Since this is a pure client-side application with no build process:

1. **Open directly in browser**:
   ```bash
   # Linux
   xdg-open loom-designer.html
   # macOS
   open loom-designer.html
   # Windows
   start loom-designer.html
   ```

2. **Test pattern export/import**:
   - Create a pattern
   - Export to JSON
   - Clear all
   - Import the JSON file
   - Verify all grids and colors are restored

3. **Test drawdown calculation**:
   - Set up threading, tie-up, and treadling
   - Verify drawdown updates automatically
   - Change colors and verify drawdown reflects new colors

## Common Modifications

### Adding New Threading/Treadling Patterns
Add options to the select dropdowns and implement the pattern logic in `applyThreadingPattern()` or `applyTreadlingPattern()`. Patterns should handle variable shaft/treadle counts.

### Adding New Color Patterns
Add options to color pattern dropdowns and implement in `applyWarpColorPattern()` or `applyWeftColorPattern()`.

### Changing Grid Constraints
Modify the `min`/`max` attributes on number inputs in the HTML. Update defaults in the `state` object initialization.

## Important Implementation Details

- **Grid coordinates**: `dataset.row` and `dataset.col` are used to identify cells. Row/col meanings vary by grid:
  - Threading: row=shaft, col=thread
  - Tie-up: row=shaft, col=treadle
  - Treadling: row=pick, col=treadle
  - Drawdown: row=pick, col=thread

- **Color picker alignment**: Warp colors use `gridTemplateColumns: repeat(${warpThreads}, 20px)` to match threading width. Weft colors use `gridTemplateRows: repeat(${picks}, 20px)` to match treadling height.

- **Dropdown reset behavior**: Pattern/color dropdowns reset to empty value after applying to allow re-application.

## File Structure

- `loom-designer.html` - Complete application (HTML + CSS + JavaScript)
- `README.md` - User documentation and GitHub Pages deployment instructions
- `LICENSE` - Apache License 2.0
- `CLAUDE.md` - This file

No build tools, package managers, or external dependencies are used.

## License

This project is licensed under the Apache License 2.0. All source files include the Apache license header.
