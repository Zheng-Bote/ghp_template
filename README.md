<div id="top" align="center">
<h1>GH Template with GH-Pages 📂</h1>
<p>cross-platform application to do something</p>

![License](https://img.shields.io/badge/license-MIT-green.svg)
![Platform](https://img.shields.io/badge/platform-Linux%20%7C%20Windows%20%7C%20macOS-lightgrey.svg)
[![GitHub release (latest by date)](https://img.shields.io/github/v/release/Zheng-Bote/ghp_template?logo=GitHub)](https://github.com/Zheng-Bote/ghp_template/releases)
<br/>
[Report Issue](https://github.com/Zheng-Bote/ghp_template/issues) · [Request Feature](https://github.com/Zheng-Bote/ghp_template/pulls)

</div>

<hr>

<!-- START doctoc generated TOC please keep comment here to allow auto update -->
<!-- DON'T EDIT THIS SECTION, INSTEAD RE-RUN doctoc TO UPDATE -->
**Table of Contents**

- [Description](#description)
  - [✨ Key Features](#-key-features)
  - [Status](#status)
- [Documentation & Screenshots](#documentation--screenshots)
- [⚙️ Build](#-build)
  - [Build Instructions](#build-instructions)
  - [Project Structure](#project-structure)
- [🏗️ Architecture](#-architecture)
  - [Component Overview](#component-overview)
  - [Class Diagram](#class-diagram)
  - [Sorting Flow Logic](#sorting-flow-logic)
- [🤝 Contributing](#-contributing)
- [📄 License](#-license)
- [👤 Author](#-author)
  - [Code Contributors](#code-contributors)

<!-- END doctoc generated TOC please keep comment here to allow auto update -->

<hr>

# Description

![QT](https://img.shields.io/badge/Community-6+-41CD52?logo=qt)
![CXX](https://img.shields.io/badge/C++-23-blue?logo=cplusplus)
![Rust](https://img.shields.io/badge/Rust-Rocket-lightgrey?logo=rust)
![Expressif](https://img.shields.io/badge/ESP-32-E7352C?logo=espressif)
![GHA](https://img.shields.io/badge/Github-Action-black?logo=githubactions)
![Node](https://img.shields.io/badge/Node-24-blue?logo=tsnode)
![Angular](https://img.shields.io/badge/Angular-21+-red?logo=angular)
![Vue](https://img.shields.io/badge/Vue-3+-4FC08D?logo=vuedotjs)
![HTML5](https://img.shields.io/badge/HTML-5+-E34F26?logo=html5)
![Typescript](https://img.shields.io/badge/TypeScript-5+-3178C6?logo=typescript)
![Svelte.js](https://img.shields.io/badge/Svelte-5-324FFF?logo=svelte)
![Lit.js](https://img.shields.io/badge/Lit.js-324FFF?logo=lit)
![CSS3](https://img.shields.io/badge/CSS3-663399?logo=css3)
![Platform](https://img.shields.io/badge/platform-Linux%20%7C%20Windows%20%7C%20macOS-lightgrey.svg)
![License](https://img.shields.io/badge/license-MIT-green.svg)

**GH Template with GH-Pages** is a Github README template, especially with Github Pages based on Jekyll.

## ✨ Key Features

- **Real-time updates with zero downtimes:** Uses xyz super features.
- **Bug-Free:** zero bugs and super stable.
- **zero costs:** running in Clouds with zero costs.

## Status

:arrow_right: <mark>:warning: still under construction :warning:</mark> :arrow_left:

![GitHub Created At](https://img.shields.io/github/created-at/Zheng-Bote/ghp_template)
[![GitHub release (latest by date)](https://img.shields.io/github/v/release/Zheng-Bote/ghp_template?logo=GitHub)](https://github.com/Zheng-Bote/ghp_template/releases)
![GitHub Release Date](https://img.shields.io/github/release-date/Zheng-Bote/ghp_template)
![Status](https://img.shields.io/badge/Status-stable-green)

![GitHub Issues](https://img.shields.io/github/issues/Zheng-Bote/ghp_template)
![GitHub Pull Requests](https://img.shields.io/github/issues-pr/Zheng-Bote/ghp_template)

---

# Documentation & Screenshots

_see Github Pages_

# ⚙️ Build

**_Prerequisites_**

- C++ Compiler supporting C++23 (GCC 13+, Clang 16+, MSVC 2022 v17.6+)
- CMake (3.23 or newer)
- Qt 6 (Core, Gui, Widgets, LinguistTools)

## Build Instructions

```Bash
# 1. Clone the repository
git clone [https://github.com/Zheng-Bote/ghp_template.git](https://github.com/Zheng-Bote/ghp_template.git)
cd file-sorter

# 2. Create build directory
mkdir build && cd build

# 3. Configure with CMake
cmake -DCMAKE_BUILD_TYPE=Release ..

# 4. Build
cmake --build . --config Release

# 5. Installer packages (optional, Windows only)
cpack.exe -C Release
# in some cases (if Chocolatey is installed on your system) the complete path to your Qt cpack is needed
& "C:\Qt\Tools\CMake_64\bin\cpack.exe" -C Release
```

## Project Structure

```Plaintext
file-sorter/
├── CMakeLists.txt       # Build configuration
├── resources.qrc        # Resource file (icons, etc.)
├── resources/           # Resource files (icons, logos, for AppImage etc.)
├── include/             # Header files (*.hpp)
├── src/                 # Source files (*.cpp)
├── translations/        # Translation files (*.ts)
└── configure/           # CMake configuration scripts
```

> \[!NOTE]
> You can modify rules while "Automatic Monitoring" is active. The changes will be applied immediately.

---

([back to top](#top))

# 🏗️ Architecture

The application follows a clean separation of concerns, splitting the User Interface (UI) from the business logic.

## Component Overview

1.  **MainWindow (UI):** Handles user interaction, configuration (TableWidget), and displays logs. It manages the application lifecycle and processes optional CLI arguments (QCommandLineParser) to handle minimized starts.
2.  **FileSorter (Logic):** A `QObject` based worker class. It handles:
    - File system monitoring (`QFileSystemWatcher`).
    - Debouncing logic to wait for file write operations.
    - The actual sorting algorithm (Pattern matching & `std::filesystem`/`QDir` operations).
3.  **Config & Resources:**
    - `rz_config.hpp`: Generated by CMake for versioning and metadata.
    - `QSettings`: Stores sorting rules persistently.
    - `Qt Linguist`: Handles translations (`.ts` / `.qm`).

## Class Diagram

```mermaid
classDiagram
    class MainWindow {
        +QTableWidget* m_table
        +QTextEdit* m_logOutput
        +QCheckBox* m_autoSortCheck
        -setupUI()
        -saveSettings()
        -loadSettings()
        -onRulesModified()
    }

    class FileSorter {
        +void sortDownloads(List categories)
        +void setMonitoring(bool enable)
        +void updateRules(List categories)
        -QFileSystemWatcher* m_watcher
        -QTimer* m_debounceTimer
        -onDirectoryChanged()
    }

    class Category {
        +QString folderName
        +QStringList extensions
        +bool useDatePath
    }

    class AboutDialog {
        +AboutDialog(QWidget* parent)
    }

    MainWindow *-- FileSorter : owns
    MainWindow ..> Category : creates
    MainWindow ..> AboutDialog : shows
    FileSorter -- QFileSystemWatcher : uses
    FileSorter -- QTimer : uses
```

## Sorting Flow Logic

When Automatic Monitoring is enabled, the application follows this process:

```mermaid
flowchart TD
    A["Start / New File Detected"] --> B{"Is Debounce Timer Active?"}
    B -- Yes --> C["Reset Timer"]
    B -- No --> D["Start Timer (e.g. 2s)"]
    C --> E["Wait..."]
    D --> E
    E --> F{"Timer Timeout"}
    F --> G["Scan Download Directory"]
    G --> H{"File matches Rule?"}
    H -- No --> I["Skip File"]
    H -- Yes --> J{"Date Sorting Enabled?"}
    J -- Yes --> K["Create Path: Folder/YYYY/MM/DD"]
    J -- No --> L["Create Path: Folder/"]
    K --> M["Move File"]
    L --> M
    M --> N["Log Action"]
```

---

([back to top](#top))

# 🤝 Contributing

Contributions are welcome! Please fork the repository and create a pull request.

1. Fork the Project
2. Create your Feature Branch (git checkout -b feature/AmazingFeature)
3. Commit your Changes (git commit -m 'Add some AmazingFeature')
4. Push to the Branch (git push origin feature/AmazingFeature)
5. Open a Pull Request

# 📄 License

Distributed under the MIT License. See LICENSE for more information.

Copyright (c) 2025 ZHENG Robert

# 👤 Author

[![Zheng Robert - Core Development](https://img.shields.io/badge/Github-Zheng_Robert-black?logo=github)](https://www.github.com/Zheng-Bote)

## Code Contributors

![Contributors](https://img.shields.io/github/contributors/Zheng-Bote/qt-desktop_file_encryption-decryption?color=dark-green)

<hr>
([back to top](#top))

:vulcan_salute:
