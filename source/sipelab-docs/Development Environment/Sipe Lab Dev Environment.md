
Install software:

1. [Anaconda](https://www.anaconda.com/download/success)
2. [Git](https://git-scm.com/downloads) and [Github Desktop](https://desktop.github.com/download/)
3. [Visual Studio Code](https://code.visualstudio.com/)

Anaconda will manage virtual environments for Python projects. Python projects usually import third-party modules created by other developers to streamline project development; **Anaconda is the virtual warehouse** that keeps imported modules and libraries orderly and accessible when working on a computer that may have multiple python projects requiring the same module (eg. `numpy` or `pandas`) or allowing several versions of Python to run on the same computer without interference.

Git provides version management for codebases. Similar to Google Docs or Onedrive, Git keeps history of all edits and changes to code in a memory-efficient manner. Git, therefore, allows us to safely make edits and additions to our code without losing our previous progress if we break something (which is inevitable). Github desktop provides a platform to host our code Repositories on the web and update them with an intuitive software solution (though, the git command line interface is always still available). It is useful to note that Github is a platform built atop Git--they are not the same. A Git installation is required for Github. Your Github account will allow you to host your code on the web at github.com for others to see. 

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

Below is a brief tutorial on how to set up a Python environment in VS Code, install mesofield, and run the [mesofield](vscode-file://vscode-app/c:/Users/cakei/AppData/Local/Programs/Microsoft%20VS%20Code/resources/app/out/vs/code/electron-sandbox/workbench/workbench.html) CLI.

## 1. Clone and Open in VS Code

1. Clone this repository (or download it) to your local machine.
2. Open the folder in Visual Studio Code.

## 2. Create a Virtual Environment

Open VS Code’s integrated terminal and create a virtual environment:

python -m venv .venv

Activate it:

- On Windows:

.venv\Scripts\activate

- On macOS/Linux:

source .venv/bin/activate

## 3. Install Dependencies

Install the required dependencies using [requirements.txt](vscode-file://vscode-app/c:/Users/cakei/AppData/Local/Programs/Microsoft%20VS%20Code/resources/app/out/vs/code/electron-sandbox/workbench/workbench.html):

pip install -r requirements.txt

Optionally, you can install directly from [setup.py](vscode-file://vscode-app/c:/Users/cakei/AppData/Local/Programs/Microsoft%20VS%20Code/resources/app/out/vs/code/electron-sandbox/workbench/workbench.html):

pip install .

## 4. Launch Mesofield

Run the mesofield module in development mode from [mesofield.__main__](vscode-file://vscode-app/c:/Users/cakei/AppData/Local/Programs/Microsoft%20VS%20Code/resources/app/out/vs/code/electron-sandbox/workbench/workbench.html):

python -m mesofield launch --dev True

That’s it! This will open the main Mesofield GUI and set it up with simulated hardware for development.