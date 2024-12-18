# OpenGL Game Engine Boilerplate

Tired of wrestling with Visual Studio's bloat just to write OpenGL code? This boilerplate lets you use VS Code (or your preferred editor) with modern C++ and OpenGL, without the overhead of full Visual Studio. It handles all the painful parts of C++ development - linking libraries, configuring build systems, and setting up intellisense - so you can focus on writing code.

Features:
- Modern OpenGL setup with GLFW and GLAD
- CMake-based build system that just works
- Full intellisense support via clangd
- Clean rebuild system for dependency management
- Minimal configuration needed - clone and code
- Works with any editor that supports Language Server Protocol
- No Visual Studio IDE required - just the build tools

## Prerequisites

- Visual Studio 2022 Build Tools
- CMake (3.10 or higher)
- Visual Studio Code
- Git

## Development Environment Setup

### Required Build Tools

1. Visual Studio Build Tools 2022
   - Download from: [Visual Studio Downloads](https://visualstudio.microsoft.com/downloads/)
   - Choose "Build Tools for Visual Studio 2022"
   - In the installer, select:
     - MSVC v143 build tools (x64/x86)
     - Windows 10/11 SDK
     - C++ CMake tools
   - Default installation path: `C:\Program Files (x86)\Microsoft Visual Studio\2022\BuildTools`
   - Ensure the following is in your system PATH:
     ```
     C:\Program Files (x86)\Microsoft Visual Studio\2022\BuildTools\MSBuild\Current\Bin
     ```

### Required VS Code Extensions

1. [CMake Tools](https://marketplace.visualstudio.com/items?itemName=ms-vscode.cmake-tools)

   - Primary CMake integration
   - Provides build/configure commands
   - Handles kit selection
   - Use `Clean Rebuild` from CMake Tools commands for clean builds

2. [clangd](https://marketplace.visualstudio.com/items?itemName=llvm-vs-code-extensions.vscode-clangd)

   - Primary C++ language server
   - Provides intelligent code completion
   - Shows function signatures and documentation
   - Handles code navigation

3. [C/C++ Extension Pack](https://marketplace.visualstudio.com/items?itemName=ms-vscode.cpptools-extension-pack)

   - Includes Microsoft C/C++ extension
   - Provides debugging support
   - Keep IntelliSense disabled (we use clangd)
   - Includes CMake and CMake Tools

4. [Include Autocomplete](https://marketplace.visualstudio.com/items?itemName=ajshort.include-autocomplete)
   - Better README.md editing
   - Preview support

### Verifying Build Tools Installation

1. Check MSBuild Installation:
```bash
where msbuild
```
Should show: `C:\Program Files (x86)\Microsoft Visual Studio\2022\BuildTools\MSBuild\Current\Bin\MSBuild.exe`

2. Check Visual Studio Build Tools:
```bash
"C:\Program Files (x86)\Microsoft Visual Studio\2022\BuildTools\VC\Auxiliary\Build\vcvarsall.bat" x64
```
Should initialize the environment for x64 builds

3. Verify CMake can find the compiler:
```bash
cmake --version
cmake -G "Visual Studio 17 2022" -A x64 -B build
```

### Troubleshooting Build Tools

If build tools aren't found:
1. Verify installation path:
   ```
   C:\Program Files (x86)\Microsoft Visual Studio\2022\BuildTools
   ```
2. Add to PATH if needed:
   - Open System Properties > Advanced > Environment Variables
   - Add to System PATH:
     ```
     C:\Program Files (x86)\Microsoft Visual Studio\2022\BuildTools\MSBuild\Current\Bin
     ```
3. Restart VS Code and terminal after PATH changes

## Project Structure

```
shader_prac/
├── include/           # Header files
├── libs/              # External libraries
│   ├── GLFW/          # GLFW library files
│   └── glad/          # GLAD library files
├── src/               # Source files
├── .clangd            # Clangd configuration
├── .vscode/           # VS Code settings
├── CMakeLists.txt     # CMake build configuration
└── README.md          # This file
```

## Quick Start

1. Clone this repository:
```bash
git clone https://github.com/crushr3sist/gamengine_boilerplate.git
cd gamengine_boilerplate
```

2. Open in VS Code and:
   - Install recommended extensions when prompted
   - Select Visual Studio Build Tools 2022 - amd64 kit
   - Use CMake: Clean Rebuild for clean builds
   - Or use CMake: Build for incremental builds

## Clean Rebuild

The project includes a clean rebuild feature that ensures a fresh build:

1. Via CMake Tools UI:
   - Click on the CMake icon in the sidebar
   - Select "Clean Rebuild" from the build variants

2. Via Command Palette:
   - Press Ctrl+Shift+P
   - Type "CMake: Clean Rebuild"
   - This will clear the build directory and rebuild

3. Manual clean rebuild:
```bash
rm -rf build/
mkdir build
cd build
cmake -G "Visual Studio 17 2022" -A x64 ..
cmake --build . --config Debug
```

## Troubleshooting

### Intellisense Not Working
If intellisense stops working:
1. Delete the build directory
2. Delete .cache directory if it exists
3. Restart VS Code
4. Let CMake reconfigure
5. Restart the Clangd language server (Ctrl+Shift+P -> "Restart Language Server")

### Build Errors
Make sure you're using the correct toolchain:
- Check CMAKE_GENERATOR_TOOLSET in CMakeLists.txt matches your VS version
- Ensure Visual Studio 2022 Build Tools are properly installed
- Verify GLFW and GLAD libraries are present in the libs directory

## OpenGL Setup Details

The boilerplate includes:
- GLFW for window management and OpenGL context creation
- GLAD for OpenGL function loading
- Example triangle rendering with color attributes
- Shader compilation and linking
- Basic error handling

## Project Configuration Files

### CMakeLists.txt
- Configures build settings
- Sets up dependencies
- Handles library linking
- Generates compile_commands.json for intellisense

### .clangd
- Configures clangd language server
- Sets include paths
- Configures diagnostics

### settings.json
- VS Code workspace settings
- CMake configuration
- Clangd settings

## Adding New Files

1. Create .cpp files in src/
2. Create .hpp files in include/ or in src/, they're grabbed nested as well
3. CMake will automatically detect new files (using GLOB)
4. Rebuild project

## Common Operations

### Building
```bash
cmake --build build --config Debug
```

### Running
```bash
./build/Debug/gamengine_boilerplate
```

### Cleaning
```bash
rm -rf build/
```

