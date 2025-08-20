# OpenTTD Tech Stack

## Build System
- **Primary:** CMake (minimum version 3.17)
- **Languages:** C++20 (standard required, extensions disabled)
- **Package Manager:** vcpkg for dependencies

## Core Dependencies
### Required/Encouraged Libraries
- **breakpad:** Creates minidumps on crash (not on ARM Windows)
- **zlib:** (De)compressing old savegames, content downloads, heightmaps
- **liblzma:** (De)compressing savegames (1.1.0 and later)
- **libpng:** Making screenshots and loading heightmaps
- **liblzo2:** (De)compressing very old savegames (optional)

### Linux-Specific Dependencies
- **libcurl:** Content downloads (with HTTP2 support)
- **libSDL2:** Hardware access (video, sound, mouse)
- **libfreetype:** Loading and rendering fonts
- **libfontconfig:** Font searching and resolution
- **harfbuzz:** Right-to-left script handling (Arabic, Persian)
- **libicu:** Right-to-left scripts and natural string sorting
- **dbus:** System integration (default features disabled)

### 3rd Party Libraries (bundled)
- **squirrel:** Scripting (Zlib license)
- **md5:** Hash implementation (Zlib license)
- **fmt:** String formatting (MIT license)
- **nlohmann json:** JSON parsing (MIT license)
- **OpenGL API:** Graphics (MIT license)
- **catch2:** Testing framework (Boost license)
- **icu scriptrun:** Text processing (Unicode license)
- **monocypher:** Cryptography (2-clause BSD/CC-0)
- **OpenTTD Social Integration API:** Platform integration (MIT license)

## Compiler Requirements
- **Windows:** Microsoft Visual Studio 2022 or newer
- **Linux/macOS:** C++20 compatible compiler