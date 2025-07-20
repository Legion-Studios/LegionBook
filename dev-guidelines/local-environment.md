# Local Development Environment Setup

Legion Studios enforces a specific development environment setup to ensure consistency and ease of development across all addons. This document outlines the steps to set up your local environment for addon development.

## Steps

- [Prerequisites](#prerequisites)
- [Setting Up the Repository](#setting-up-the-repository)
- [Open the Workspace in Visual Studio Code](#open-the-workspace-in-visual-studio-code)
- [Using HEMTT](#using-hemtt)

## Prerequisites

Before you begin, ensure you have the following installed:

- [Git](https://git-scm.com/downloads) (Version Control System) or some other Git client I.E ([GitHub Desktop](https://desktop.github.com/)) or [GitKraken](https://www.gitkraken.com/)
- [Arma 3 Tools](https://store.steampowered.com/app/233800/Arma_3_Tools/) (available on Steam)
- [Visual Studio Code](https://code.visualstudio.com/) or another code editor of your choice
- [Mikero's Tools](https://mikero.bytex.digital/) (download the AIO)
- [Hemtt](https://github.com/BrettMayson/HEMTT) Install via `winget install BrettMayson.HEMTT`

## Setting Up the Repository

1. **Setup P Drive** (Windows Only)**:
   - Create a folder on your system where you want to store the Legion Studios addons, e.g., `C:\ArmaWorkBench`.
   - Launch the Arma 3 Tools and set the P Drive to point to this folder.
        - Preferences -> Path to your P drive -> Set it to `C:\ArmaWorkBench`
        - Check Mount P Drive on startup if you want it to automatically mount when you start the Arma 3 Tools. This will create a popup whenever you start your machine to mount the P Drive.
        - Click "Mount P Drive" to mount it immediately. This will create a virtual drive (P:) that points to the folder you specified.
        - Ensure that the P Drive is mounted before proceeding with the next steps.

2. **Mikeros P Drive Setup**:
   - In Arma 3 Tools go to `External` -> `Mikero's Tools`.
   - Click on `Arma3P.cmd`
   - In the dialog that appears enter the following parameters:
     - "enter drive to extract to E..Z" - `P`
     - "full extraction including layers, dubbing, and missions (base addons only)? [Y/N]" - `N`

3. **Create a Legion Studios Folder**: Inside your P Drive, create a folder named `ls` to store all Legion Studios addons.

    ```bash
    mkdir P:\ls
    ```

    You can do this using the command line or through your file explorer.

4. **Clone the Repository**: Open a terminal and run the following command to clone the Legion Studios repository into the `ls` folder:

    ````bash
    cd P:\ls
    ````

    ```bash
    git clone https://github.com/Legion-Studios/LegionCore.git core
    ````

    This will create a folder named `core` in your current directory containing the Legion Studios addons.

5. **Submodules**: If the repository contains submodules, initialize and update them by running the following command in the `core` directory:

   ```bash
   cd core
   git submodule update --init --recursive
   ```

   This will only be applicable once the `translations` submodule is added.

## Open the Workspace in Visual Studio Code

1. In file explorer, navigate to the `P:\ls\core` directory.
2. Double click on the `LegionCore.code-workspace` file to open it in Visual Studio Code.
3. When prompted, install the recommended extensions for the workspace. This is highly recommended.

## Using HEMTT

To build the mod using HEMTT, follow these steps:

1. Open a terminal in the `P:\ls\core` directory.
2. Run the following command to build the mod:

   ```bash
   hemtt build
   ```

3. If you want to build a specific addon, you can specify it like this:

   ```bash
    hemtt build --just <folder_name>
    ```
