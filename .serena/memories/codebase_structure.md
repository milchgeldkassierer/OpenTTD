# OpenTTD Codebase Structure

## Root Directory Layout
```
OpenTTD/
├── src/                    # Main source code
├── docs/                   # Documentation files
├── cmake/                  # CMake configuration files
├── bin/                    # Binary/executable outputs
├── regression/             # Regression test data
├── os/                     # OS-specific code/configs
├── media/                  # Game media files
├── CMakeLists.txt          # Main build configuration
├── vcpkg.json             # Dependency management
├── README.md              # Project documentation
├── COMPILING.md           # Build instructions
├── CODINGSTYLE.md         # Coding standards
├── CONTRIBUTING.md        # Contribution guidelines
└── COPYING.md             # License information
```

## Source Code Organization (`src/`)
### Core Directories
- **3rdparty/**: Third-party libraries (squirrel, fmt, json, etc.)
- **core/**: Core utility functions and data structures
- **tests/**: Unit tests using Catch2 framework

### Game Systems
- **ai/**: Artificial Intelligence system
- **script/**: Scripting engine and API
- **game/**: Game logic and rules
- **linkgraph/**: Transport network analysis
- **pathfinder/**: Pathfinding algorithms
- **saveload/**: Save/load game functionality
- **timer/**: Game timing and scheduling

### Graphics & UI
- **blitter/**: Graphics rendering backends
- **video/**: Video driver implementations
- **widgets/**: UI widget implementations
- **fontcache/**: Font rendering and caching
- **spriteloader/**: Sprite loading system

### Game Content
- **newgrf/**: NewGRF (mod) system
- **table/**: Game data tables
- **lang/**: Language/localization files
- **music/**: Music system
- **sound/**: Sound system

### Infrastructure
- **network/**: Multiplayer networking
- **os/**: Operating system abstraction
- **misc/**: Miscellaneous utilities

## Build Artifacts
- **Binary name:** `openttd` (configurable via BINARY_NAME)
- **Test binary:** `openttd_test`
- **CMake generates:** Compile commands for IDE integration