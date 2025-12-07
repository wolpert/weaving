# Loom Pattern Designer

An interactive web-based tool for designing weaving patterns on a multi-shaft loom. Create, visualize, and export weaving drafts with customizable threading, tie-up, treadling, and thread colors.

## Live Demo

**🚀 [Launch Loom Pattern Designer](https://wolpert.github.io/weaving/)**

The application is hosted on GitHub Pages and can be accessed at:
- https://wolpert.github.io/weaving/

Or view the repository at: https://github.com/wolpert/weaving

## Features

- **Multi-shaft loom support**: Configure 4-16 shafts (default: 8)
- **Flexible grid sizes**: Adjust warp threads (4-64), treadles (4-16), and picks (4-64)
- **Pattern presets**:
  - Threading patterns: Straight Draw, Point Twill, Reverse
  - Treadling patterns: Straight, Reverse, Point
  - Color patterns: Solid, Alternating (2 colors), Rainbow
- **Interactive grids**: Click to set threading, tie-up, and treadling
- **Custom thread colors**: Individual color control for each warp thread and weft pick
- **Real-time drawdown**: See your weave pattern update automatically as you design
- **Export/Import**: Save and load your patterns as JSON files

## How to Use

### Getting Started

1. **Open the HTML file**: Simply open `loom-designer.html` in any modern web browser
2. **Configure your loom**: Set the number of shafts, warp threads, treadles, and picks
3. **Design your pattern**: Use the interactive grids or preset patterns

### Basic Workflow

#### 1. Set Loom Configuration
- **Shafts**: Number of heddles (4-16, default: 8)
- **Warp Threads**: Number of vertical threads (4-64, default: 32)
- **Treadles**: Number of foot pedals (4-16, default: 8)
- **Picks**: Number of weft rows (4-64, default: 32)

#### 2. Apply Threading Pattern
Use the **Threading Pattern** dropdown to apply a preset:
- **Straight Draw**: Sequential pattern (1→2→3→4→1→2...)
- **Point Twill**: Reversing pattern (1→2→3→4→3→2→1...)
- **Reverse**: Backward sequential (4→3→2→1→4→3...)

Or click cells in the threading grid to manually assign threads to shafts.

#### 3. Set Up Tie-Up
Click cells in the tie-up grid to connect treadles to shafts. When you press a treadle (in the treadling), all connected shafts will lift.

#### 4. Apply Treadling Pattern
Use the **Treadling Pattern** dropdown to apply a preset:
- **Straight**: Sequential treadle presses (1→2→3→4→1→2...)
- **Reverse**: Backward sequence (4→3→2→1→4→3...)
- **Point**: Reversing sequence (1→2→3→4→3→2→1...)

Or click cells in the treadling grid to manually set the treadle sequence.

#### 5. Customize Thread Colors
- **Warp Colors**: Click the colored squares above the threading grid
- **Weft Colors**: Click the colored squares beside the treadling grid

Use the color pattern dropdowns for quick setup:
- **Solid Color**: All threads one color
- **Alternating**: Alternates between two selected colors
- **Rainbow**: Full spectrum gradient

#### 6. View the Drawdown
The drawdown (center grid) automatically shows your weave pattern:
- Each cell displays the color of the thread that appears on top
- Warp colors show when warp threads are lifted
- Weft colors show when warp threads are down

### Saving and Loading

- **Export Pattern**: Click to download your design as a JSON file
  - Includes all settings, threading, tie-up, treadling, and colors
  - Filename format: `loom-pattern-YYYY-MM-DD.json`

- **Import Pattern**: Click to load a previously saved pattern
  - Automatically restores all settings and configurations

### Tips

- Start with a preset pattern and customize from there
- Use "Load Sample Pattern" to see an example
- Click "Clear All" to reset and start over
- Colors are saved with your pattern export
- You can manually adjust any preset pattern by clicking individual cells

## Technical Details

- **Technology**: Pure HTML, CSS, and JavaScript (no dependencies)
- **Browser Support**: All modern browsers (Chrome, Firefox, Safari, Edge)
- **File Format**: JSON for pattern export/import
- **Offline Capable**: Works completely offline once downloaded

## Installation

### Option 1: Direct Use
1. Download `loom-designer.html`
2. Open it in your web browser
3. Start designing!

### Option 2: GitHub Pages
1. Fork the repository at https://github.com/wolpert/weaving
2. In your fork, go to Settings → Pages
3. Set source to "main" branch
4. Access at `https://[your-username].github.io/weaving/`

### Option 3: Local Development
```bash
# Clone the repository
git clone https://github.com/wolpert/weaving.git

# Navigate to the directory
cd weaving

# Open the file
# On macOS:
open loom-designer.html
# On Linux:
xdg-open loom-designer.html
# On Windows:
start loom-designer.html
```

## Weaving Terminology

- **Warp**: The vertical threads on the loom
- **Weft**: The horizontal threads woven through the warp
- **Shaft/Heddle**: The frame that raises/lowers groups of warp threads
- **Treadle**: The foot pedal that controls which shafts lift
- **Threading**: Which shaft each warp thread passes through
- **Tie-Up**: Which shafts are lifted by each treadle
- **Treadling**: The sequence of treadle presses (weaving sequence)
- **Drawdown**: The visual representation of the woven cloth
- **Pick**: One row of weft thread

## Contributing

Contributions are welcome! Please feel free to submit issues or pull requests.

## License

This project is open source and available under the [Apache License 2.0](LICENSE).

Copyright 2025 Loom Pattern Designer Contributors

Licensed under the Apache License, Version 2.0 (the "License");
you may not use this file except in compliance with the License.
You may obtain a copy of the License at

    http://www.apache.org/licenses/LICENSE-2.0

Unless required by applicable law or agreed to in writing, software
distributed under the License is distributed on an "AS IS" BASIS,
WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
See the License for the specific language governing permissions and
limitations under the License.

## Acknowledgments

Created as a tool for weavers to design and visualize multi-shaft weaving patterns before starting work on the loom.
