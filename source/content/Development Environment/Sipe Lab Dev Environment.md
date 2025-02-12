
Install software:

1. [Anaconda](https://www.anaconda.com/download/success)
2. [Git](https://git-scm.com/downloads) and [Github Desktop](https://desktop.github.com/download/)
3. [Visual Studio Code](https://code.visualstudio.com/)

Anaconda will manage virtual environments for Python projects. Python projects usually import third-party modules created by other developers to streamline project development; **Anaconda is the virtual warehouse** that keeps imported modules and libraries orderly and accessible when working on a computer that may have multiple python projects requiring the same module (eg. `numpy` or `pandas`) or allowing several versions of Python to run on the same computer without interference.

Git provides version management for codebases. Similar to Google Docs or Onedrive, Git keeps history of all edits and changes to code in a memory-efficient manner. Git, therefore, allows us to safely make edits and additions to our code without losing our previous progress if we break something (which is inevitable). Github desktop provides a platform to host our code Repositories on the web and update them with an intuitive software solution (though, the git command line interface is always still available). It is useful to note that Github is a platform built atop Git--they are not the same. A [[Github Repository]] installation is required for Github. Your Github account will allow you to host your code on the web at github.com for others to see. 

Visual Studio Code is our Integrated Development Environment (IDE) software. If you have used Matlab before, VSCode is similar in principal. VSCode can be used for developing in many coding languages, but we will be using it for Python. There are many IDEs around all with pros and cons. It is worth looking at others, but VSCode is an open-source product supported by Microsoft which means it will be around for a while, free, and secure. 

## VSCode Extensions

| ![[vscode-python-extensions.png]]![[vscode-datawrangler-ext.png]]![[vscode-jupyter-ext.png]]![[vscode-git-ext.png]] |
| ------------------------------------------------------------------------------------------------------------------- |

---
## Conda and VSCode

![[select-conda-env-vscode.png]]![[conda-env-vscode.png]]

# Git control in VSCode
Microsoft provides a [useful tutorial](https://code.visualstudio.com/docs/sourcecontrol/overview) with screenshots on using the integrated Git source control in a Visual Studio Code environment. Below is a gif of the Source Control tab in VSCode. I have added new summary to the README.md file and saved it. Now, the README.md file appears in the 'Changes' section. We stage it, add a Commit message, Commit, then Push to Github.
![[Code_Wy3cRNN71y.gif]]

# Setting Up Mesofield in Visual Studio Code

# Mesofield

This is a PyQt application that is designed to interface with scientific hardware through serial connections and [[MicroManager]]

The core of the application is the `ExperimentConfig` class (`mesofield.config.ExperimentConfig`) and the corresponding `ConfigController` widget (`mesofield.gui.widgets.ConfigController`)

`ExperimentConfig` loads hardware configurations via the `mesofield.config.HardwareManager` dataclass which loads a `hardware.yaml` file in the module directory

All hardware and GUI components inherit the `ExperimentConfig` providing global state access to parameters defining filename, directories, and experimental settings.

The `ConfigController` loads additional parameters to the `ExperimentConfig` instance by passing a JSON file path to the `ExperimentConfig.load_parameters()` method.

NOTE: This has only been tested on Windows 10/11. Hardware control features rely on [[pymmcore-plus]] and an installation of [[MicroManager]] with specific device drivers.

The GUI components include live views for cameras (with optional pyqtgraph ImageView), encoder velocity pyqtgraphics, buttons for hardware control, and an iPython terminal for access to the backend

# [Setting Up Mesofield in Visual Studio Code](https://github.com/Gronemeyer/mesofield#setting-up-mesofield-in-visual-studio-code)

Below is a brief tutorial on how to set up a Python environment in VS Code, install mesofield, and run the [mesofield] CLI.

## 1. [Clone and Open in VS Code](https://github.com/Gronemeyer/mesofield#1-clone-and-open-in-vs-code)

1. Clone this repository (or download it) to your local machine.
2. Open the folder in Visual Studio Code.

**Clone the Repository:**

```shell
git clone https://github.com/Gronemeyer/mesofield.git
cd mesofield
```

**Create and Activate a Conda Environment:**

```shell
conda create --name mesofield python=3.11
conda activate mesofield
```

**Install Dependencies:**

```shell
pip install -e .
```

Run the CLI:

_You can run the module using:_

```
python -m mesofield launch
```

That’s it! This will open the main Mesofield GUI and set it up with simulated hardware for development.

# Using the Console in Mesofield

The IPython terminal can be launched with the `Toggle Console` button in the top-left menu bar.

The console gives you access to the backend of the application. Type >>locals() into the terminal to see the accesible namespace using dot-notation

`self` provides access to the MainWindow and its attributes `config` provides you access to the ExperimentConfig `mda` provides access to the MDAWidget

The `config` command is the most useful outside of development. Type `config.hardware` to see the loaded hardware, for example. Type `config.` + `tab` to see the available methods and parameters. Test them out, nothing should break in development mode.