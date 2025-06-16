# Build Instructions for GTA-5-MOD-MENU

---

## Table of Contents

1. [Prerequisites](#prerequisites)  
2. [Environment Setup](#environment-setup)  
3. [Cloning the Repository](#cloning-the-repository)  
4. [Building with CMake](#building-with-cmake)  
5. [Building on Windows](#building-on-windows)  
6. [Building on Linux](#building-on-linux)  
7. [Building on macOS](#building-on-macos)  
8. [Python Integration (Optional)](#python-integration-optional)  
9. [Common Issues and Troubleshooting](#common-issues-and-troubleshooting)  
10. [Cleaning the Build](#cleaning-the-build)  
11. [Contact and Support](#contact-and-support)  

---

## 1. Prerequisites

Before you begin building the GTA-5-MOD-MENU, ensure you have the following installed:

- **C++ Compiler:**  
  - Windows: Visual Studio 2019/2022 (with C++ workload)  
  - Linux: GCC 9+ or Clang 10+  
  - macOS: Xcode Command Line Tools or Xcode  

- **CMake:** Version 3.18 or higher recommended.

- **Git:** For cloning the repository.

- **Python 3.7+** (optional, for Python scripting support).

- **Ninja (optional):** For faster builds (can be installed via package manager).

---

## 2. Environment Setup

- Ensure your compiler and build tools are added to your system `PATH`.

- On Windows, launch the **Developer Command Prompt** for Visual Studio.

- On Linux/macOS, open your terminal.

---

## 3. Cloning the Repository

Open your terminal/command prompt and run:

```bash
git clone https://github.com/sugarypumpkin822/GTA-5-MOD-MENU.git
cd GTA-5-MOD-MENU
4. Building with CMake
This project uses CMake for cross-platform builds. You will generate native build files for your platform.

5. Building on Windows
Create a build directory:

bash
Copy
Edit
mkdir build
cd build
Generate Visual Studio project files (for VS 2022):

bash
Copy
Edit
cmake .. -G "Visual Studio 17 2022" -A x64
Build the project:

bash
Copy
Edit
cmake --build . --config Release
The built binaries will be located in build/Release/.

6. Building on Linux
Create and enter a build directory:

bash
Copy
Edit
mkdir build && cd build
Generate Makefiles:

bash
Copy
Edit
cmake ..
Build using make:

bash
Copy
Edit
make -j$(nproc)
The output binary will be in the build/ folder.

7. Building on macOS
Create a build directory:

bash
Copy
Edit
mkdir build && cd build
Generate Xcode project files:

bash
Copy
Edit
cmake .. -G Xcode
Build with Xcode command line:

bash
Copy
Edit
xcodebuild -configuration Release
The built app will be in build/Release/.

8. Python Integration (Optional)
If you plan to use the Python scripting interface:

Ensure Python 3.7+ is installed and added to PATH.

During CMake configuration, enable the Python interface:

bash
Copy
Edit
cmake .. -DENABLE_PYTHON=ON
Make sure Python development headers are available (e.g., install python3-dev on Linux).

9. Common Issues and Troubleshooting
CMake not found:
Ensure CMake is installed and in your system PATH. Check with cmake --version.

Compiler errors:
Make sure your compiler supports C++17 or newer.

Missing Python headers:
Install development packages (python3-dev or equivalent).

Permission issues:
Run terminal/command prompt as Administrator or with sudo as necessary.

Git clone errors:
Check your internet connection or GitHub access.

10. Cleaning the Build
To clean build artifacts:

bash
Copy
Edit
rm -rf build/
Or on Windows, delete the build directory manually.

11. Contact and Support
For build issues or questions:

Open an issue on the GitHub repository.

Join the project Discord (link in README).

Check the Wiki or existing issues for known problems.

Happy modding!

yaml
Copy
Edit

---

If you want, I can generate platform-specific scripts (`build.bat`, `build.sh`) or a troubleshooting FAQ next!







