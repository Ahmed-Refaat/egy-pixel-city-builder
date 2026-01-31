# 🏙️ Egyptian Pixel City Builder

[![License](https://img.shields.io/badge/License-Apache%202.0-blue.svg)](https://opensource.org/licenses/Apache-2.0)
![Python](https://img.shields.io/badge/Python-3.11+-blue)
![React](https://img.shields.io/badge/React-18+-blue)

> **AI-powered isometric pixel-art city map generator - Create nostalgic SimCity-style 3D visualizations of Egyptian cities**

---

## 📖 Table of Contents

- [About](#about)
- [Features](#features)
- [Demo](#demo)
- [Technology Stack](#technology-stack)
- [Quick Start](#quick-start)
- [Project Structure](#project-structure)
- [How It Works](#how-it-works)
- [Usage Guide](#usage-guide)
- [Configuration](#configuration)
- [Development](#development)
- [API Reference](#api-reference)
- [Contributing](#contributing)
- [License](#license)
- [About the Creator](#about-the-creator)

---

## 🎯 About

**Egyptian Pixel City Builder** is an AI-powered tool that generates beautiful isometric pixel-art maps of cities in the nostalgic style of classic games like SimCity 2000 and RollerCoaster Tycoon. 

### What This Tool Does

This project combines:
- 🗺️ **Real Geographic Data** - OpenStreetMap building footprints
- 🤖 **AI Image Generation** - Create pixel-art building sprites
- 🎨 **Isometric Rendering** - Transform 2D into nostalgic 3D views
- 🌐 **Interactive Web Viewer** - Explore the generated city maps
- 🏗️ **3D Visualization** - Optional Three.js rendering

### The Vision

Inspired by classic 90s/2000s city-building games, this tool brings that nostalgic pixel-art aesthetic to real-world cities. Starting with Egyptian cities like Cairo, it can generate massive isometric maps that capture the charm of retro gaming.

---

## ✨ Features

### Core Features

✅ **Automated City Generation**
- Import building data from OpenStreetMap
- AI-generated pixel-art building sprites
- Automatic isometric tile creation
- Large-scale map assembly

✅ **Multiple Rendering Styles**
- Classic 2D isometric view
- 3D interactive visualization (Three.js)
- Water shader effects
- Custom tile layers

✅ **Interactive Web Viewer**
- Zoom and pan controls
- Building information overlay
- OpenSeaDragon integration
- Smooth tile loading

✅ **Flexible Data Pipeline**
- SQLite database for buildings
- Cloudflare R2 storage support
- Local file system option
- Efficient tile caching

### Advanced Features

🎨 **AI-Powered Generation**
- Style-consistent building sprites
- Multiple building types (residential, commercial, industrial)
- Automatic sprite variations
- Custom prompting system

🗺️ **Geographic Processing**
- UTM coordinate system support
- Automatic bounds calculation
- Tile grid generation
- Spatial indexing

📊 **Data Management**
- Building database (SQLite)
- Metadata tracking
- Generation history
- Progress monitoring

---

## 🎮 Demo

### Example Output

The tool generates:
- **Isometric Tiles**: Individual PNG tiles for web display
- **3D Data**: JSON files for Three.js rendering
- **Interactive Map**: Full web application for exploration

### Sample Cities

Currently focused on Egyptian cities:
- **Cairo** - Egypt's bustling capital
- **Alexandria** - Historic Mediterranean port
- **Giza** - Home to the pyramids
- *More cities coming soon*

---

## 🛠️ Technology Stack

### Backend (Python)

- **Python 3.11+** - Core language
- **SQLite** - Building database
- **Shapely** - Geometric operations
- **Pillow** - Image processing
- **httpx** - Async HTTP client
- **Replicate** - AI model API
- **uv** - Package management

### Frontend (Web Viewer)

- **React 18** - UI framework
- **TypeScript** - Type safety
- **OpenSeaDragon** - Tile viewer
- **Three.js** - 3D rendering
- **Bun** - JavaScript runtime
- **Vite** - Build tool

### Infrastructure

- **Cloudflare R2** - Object storage
- **OpenStreetMap** - Geographic data
- **Replicate API** - AI generation

---

## 🚀 Quick Start

### Prerequisites

**System Requirements:**
- Python 3.11 or higher
- Node.js 18+ (or Bun)
- 8GB+ RAM recommended
- 10GB+ disk space for data

**API Keys (Optional):**
- Replicate API key (for AI generation)
- Cloudflare R2 credentials (for cloud storage)

### Installation

1. **Clone Repository**
   ```bash
   git clone https://github.com/Ahmed-Refaat/egy-pixel-city-builder.git
   cd egy-pixel-city-builder
   ```

2. **Install Python Dependencies**
   ```bash
   # Using uv (recommended)
   uv sync
   
   # Or using pip
   pip install -r requirements.txt
   ```

3. **Install Frontend Dependencies**
   ```bash
   cd src/app
   bun install  # or npm install
   ```

4. **Setup Environment**
   ```bash
   cp .env.example .env
   # Edit .env with your API keys
   ```

### Running the Web Viewer

**With Production Data (R2):**
```bash
cd src/app
bun run dev
```

**With Local Data:**
```bash
cd src/app
bun run dev:local
```

Visit `http://localhost:3000` to view the map!

---

## 📁 Project Structure

```
egy-pixel-city-builder/
├── src/
│   ├── app/                      # React web viewer
│   │   ├── src/
│   │   │   ├── components/       # React components
│   │   │   ├── hooks/            # Custom hooks
│   │   │   └── App.tsx           # Main app
│   │   └── package.json
│   │
│   ├── isometric_nyc/            # Core Python library
│   │   ├── buildings/            # Building data management
│   │   ├── generation/           # AI sprite generation
│   │   ├── geometry/             # Geometric operations
│   │   ├── layers/               # Tile layer creation
│   │   ├── rendering/            # Isometric rendering
│   │   └── workflows/            # End-to-end pipelines
│   │
│   ├── web/                      # 3D viewer (Three.js)
│   │   └── src/
│   │       ├── loaders/          # Data loaders
│   │       ├── materials/        # Custom shaders
│   │       └── scene/            # 3D scene setup
│   │
│   └── demos/                    # Feature demos
│       └── water_shader/         # Water effect demo
│
├── geo_data/                     # Geographic data
│   └── boundaries/               # City boundaries
│
├── generations/                  # Generated sprites
│   └── buildings/                # Building sprites
│
├── layers/                       # Generated tile layers
│   └── buildings/                # Building tiles
│
├── synthetic_data/               # Test data
│
├── tests/                        # Unit tests
│
├── buildings.db                  # SQLite database
├── pyproject.toml               # Python config
└── uv.lock                      # Dependency lock
```

---

## 🔍 How It Works

### Step 1: Import Building Data

```python
from isometric_nyc.buildings import import_buildings

# Import buildings from OpenStreetMap
bounds = {
    'north': 30.1,
    'south': 30.0,
    'east': 31.3,
    'west': 31.2
}

import_buildings(bounds, output_db='buildings.db')
```

### Step 2: Generate Building Sprites (AI)

```python
from isometric_nyc.generation import generate_sprites

# Generate pixel-art sprites for each building type
generate_sprites(
    building_types=['residential', 'commercial', 'industrial'],
    style='simcity_2000',
    num_variations=5
)
```

### Step 3: Create Isometric Tiles

```python
from isometric_nyc.rendering import create_isometric_tiles

# Render buildings onto isometric tile grid
create_isometric_tiles(
    buildings_db='buildings.db',
    sprites_dir='generations/buildings/',
    output_dir='layers/buildings/',
    tile_size=256
)
```

### Step 4: View in Browser

```bash
cd src/app
bun run dev
```

The web viewer will load tiles and display your city!

---

## 📚 Usage Guide

### Generating Your Own City

**1. Define Your Area**
```python
# Create a config file: config.yaml
city: "Cairo"
bounds:
  north: 30.1
  south: 30.0
  east: 31.3
  west: 31.2
tile_size: 256
```

**2. Run the Pipeline**
```bash
uv run python -m isometric_nyc.workflows.full_pipeline --config config.yaml
```

**3. View Results**
```bash
cd src/app
bun run dev:local
```

### Customizing Building Styles

**Edit Prompts:**
```python
# src/isometric_nyc/generation/prompts.py

BUILDING_PROMPTS = {
    'residential': 'Isometric pixel art building, residential apartment, SimCity 2000 style...',
    'commercial': 'Isometric pixel art building, modern office, retro gaming aesthetic...',
    'industrial': 'Isometric pixel art factory, smokestacks, vintage game graphics...'
}
```

### Working with Custom Data

**Import Your Own Buildings:**
```python
import sqlite3
import json

# Create buildings database
conn = sqlite3.connect('my_buildings.db')
cursor = conn.cursor()

cursor.execute('''
    CREATE TABLE buildings (
        id TEXT PRIMARY KEY,
        geometry TEXT,  # GeoJSON
        type TEXT,
        height REAL
    )
''')

# Insert buildings
cursor.execute('''
    INSERT INTO buildings VALUES (?, ?, ?, ?)
''', ('building_1', json.dumps(geometry), 'residential', 15.0))

conn.commit()
```

---

## ⚙️ Configuration

### Environment Variables

Create `.env` file:
```bash
# AI Generation
REPLICATE_API_TOKEN=your_replicate_token

# Storage (Optional)
R2_ACCOUNT_ID=your_r2_account
R2_ACCESS_KEY_ID=your_access_key
R2_SECRET_ACCESS_KEY=your_secret_key
R2_BUCKET_NAME=your_bucket

# Database
DATABASE_URL=sqlite:///buildings.db

# Rendering
TILE_SIZE=256
ZOOM_LEVELS=5
```

### Configuration Files

**pyproject.toml** - Python dependencies
```toml
[project]
name = "egy-pixel-city-builder"
version = "1.0.0"
requires-python = ">=3.11"
```

**src/app/package.json** - Frontend dependencies
```json
{
  "name": "egy-city-viewer",
  "version": "1.0.0",
  "type": "module"
}
```

---

## 🔨 Development

### Running Tests

```bash
# Run all tests
uv run pytest

# Run specific test
uv run pytest tests/test_buildings.py

# With coverage
uv run pytest --cov=src
```

### Code Quality

```bash
# Format code
uv run ruff format .

# Lint code
uv run ruff check .

# Type checking
uv run mypy src/
```

### Building for Production

**Web App:**
```bash
cd src/app
bun run build
# Output in dist/
```

**Python Package:**
```bash
uv build
# Output in dist/
```

---

## 📖 API Reference

### Core Classes

#### BuildingsDatabase
```python
from isometric_nyc.buildings import BuildingsDatabase

db = BuildingsDatabase('buildings.db')

# Query buildings
buildings = db.get_buildings_in_bounds(north, south, east, west)

# Add building
db.add_building(id, geometry, type, height)
```

#### IsometricRenderer
```python
from isometric_nyc.rendering import IsometricRenderer

renderer = IsometricRenderer(tile_size=256)

# Render tile
tile_image = renderer.render_tile(buildings, x, y)

# Save tile
tile_image.save('tile_0_0.png')
```

#### SpriteGenerator
```python
from isometric_nyc.generation import SpriteGenerator

generator = SpriteGenerator(api_key='your_key')

# Generate sprite
sprite = generator.generate(
    prompt='isometric pixel art building',
    style='simcity'
)
```

---

## 🤝 Contributing

Contributions welcome! Here's how you can help:

### Ways to Contribute

1. **Add New Cities**
   - Create city boundary files
   - Test import process
   - Share results

2. **Improve AI Prompts**
   - Better building descriptions
   - Style variations
   - Consistency improvements

3. **Enhance Rendering**
   - New tile effects
   - Performance optimizations
   - 3D features

4. **Fix Bugs**
   - Report issues
   - Submit fixes
   - Improve tests

### Development Setup

```bash
# Fork and clone
git clone https://github.com/yourusername/egy-pixel-city-builder.git

# Create branch
git checkout -b feature/your-feature

# Make changes and test
uv run pytest

# Commit and push
git commit -m "Add your feature"
git push origin feature/your-feature

# Open pull request
```

---

## 📄 License

This project is licensed under the **Apache License 2.0** - see the [LICENSE](LICENSE) file for details.

**Copyright 2026 Ahmed Refaat**

---

## 👤 About the Creator

**Ahmed Refaat**

Geospatial developer and creative technologist specializing in maps, data visualization, and generative AI. Passionate about combining geographic data with nostalgic aesthetics to create unique digital experiences.

### Expertise

- 🗺️ **Geospatial Technology**: GIS, mapping, OpenStreetMap
- 🎨 **Generative AI**: Stable Diffusion, custom prompting, style transfer
- 🌐 **Web Development**: React, Three.js, interactive visualizations
- 🐍 **Python Development**: Data processing, automation, APIs
- 🛰️ **Satellite Data**: Earth Engine, remote sensing
- 📊 **Data Visualization**: Charts, maps, 3D graphics

### Featured Projects

- **[Earth Data Hub](https://github.com/Ahmed-Refaat/earth-data-hub)** - *Your Gateway to Global Geospatial Intelligence*
- **[Geo-Parquet Toolkit](https://github.com/Ahmed-Refaat/geo-parquet-toolkit)** - *Efficient geospatial data storage*
- **[Egyptian Positioning Suite](https://github.com/Ahmed-Refaat/egy-positioning-suite)** - *GNSS measurement tools*
- **[Egyptian Pixel City Builder](https://github.com/Ahmed-Refaat/egy-pixel-city-builder)** - *Nostalgic city visualizations*

### Connect

- **GitHub**: [@Ahmed-Refaat](https://github.com/Ahmed-Refaat)
- **Repository**: [egy-pixel-city-builder](https://github.com/Ahmed-Refaat/egy-pixel-city-builder)

---

## 🌟 Show Your Support

If you find this project interesting:

- ⭐ **Star this repository**
- 🔗 **Share with others**
- 🐛 **Report bugs**
- 💡 **Suggest features**
- 🤝 **Contribute code**

---

**Bringing nostalgic pixel-art aesthetics to real-world cities** 🏙️✨

*Egyptian Pixel City Builder - Where retro gaming meets modern mapping*

*Last Updated: January 2026*
