# OpenTTD Development Commands

## Build System (CMake)
```bash
# Create build directory and configure
mkdir build && cd build
cmake ..

# Build the project
cmake --build .

# Build specific target
cmake --build . --target openttd
cmake --build . --target openttd_test

# Debug build (default)
cmake -DCMAKE_BUILD_TYPE=Debug ..

# Release build
cmake -DCMAKE_BUILD_TYPE=Release ..

# Build with specific binary name
cmake -DBINARY_NAME=my_openttd ..
```

## Testing
```bash
# Build and run tests
cmake --build . --target openttd_test
./openttd_test

# Run tests with CTest
ctest

# Run specific test
ctest -R test_name
```

## Dependencies (vcpkg)
```bash
# Install vcpkg dependencies (if using vcpkg)
vcpkg install

# Update dependencies
vcpkg update
```

## Development Utilities
```bash
# Generate compile commands for IDE
cmake -DCMAKE_EXPORT_COMPILE_COMMANDS=YES ..

# Clean build
cmake --build . --target clean

# Install (system-wide)
cmake --build . --target install
```

## Git Commands (Standard)
```bash
# Clone repository
git clone https://github.com/OpenTTD/OpenTTD.git

# Standard git workflow
git status
git add .
git commit -m "message"
git push
git pull
```

## Regression Testing
```bash
# Run regression tests (if available)
# Check regression/ directory for test data
```

## Platform-Specific Notes
- **Windows:** Use Visual Studio 2022+ or MSBuild
- **Linux:** Standard make/cmake workflow
- **macOS:** Use Xcode or command line tools

## Code Quality
Note: No specific linting/formatting tools were found in the configuration.
Standard C++ best practices apply as per CODINGSTYLE.md.