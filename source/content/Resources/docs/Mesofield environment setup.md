

1. Install [[MicroManager]] from [[MicroManager#^963752|here]]
	- Note the installation path somewhere C:/Program Files/Micro-Manager-2.0
2. Install the [[Dhyana 400BSI V2]]  driver for MicroManager from [[Dhyana 400BSI V2#^65d0c1|here]]
	- Follow the Tuscan camera [[Dhyana 400BSI V2#^5c9057|user guide]] for importing the driver files into the MicroManager program file folder noted above


Installation of [[Napari]]

Initialize `conda` environment named `sipefield` with `Python 3.10`

``` bash
conda create -y -n sipefield -c conda-forge python=3.10
```

- for [[MicroManager]] adaptors:
```bash
mmcore install
```


# Setting Up Mesofield in Visual Studio Code

Below is a brief tutorial on how to set up a Python environment in VS Code, install mesofield, and run the [mesofield](vscode-file://vscode-app/c:/Users/cakei/AppData/Local/Programs/Microsoft%20VS%20Code/resources/app/out/vs/code/electron-sandbox/workbench/workbench.html) CLI.

1. Install [[MicroManager]] from [[MicroManager#^963752|here]]
	- Note the installation path somewhere C:/Program Files/Micro-Manager-2.0
2. Install the [[Dhyana 400BSI V2]]  driver for MicroManager from [[Dhyana 400BSI V2#^65d0c1|here]]
	- Follow the Tuscan camera [[Dhyana 400BSI V2#^5c9057|user guide]] for importing the driver files into the MicroManager program file folder noted above
## 1. Clone and Open in VS Code

1. Clone this repository (or download it) to your local machine.
2. Open the folder in Visual Studio Code.

## 2. Create a Virtual Environment
*This uses a python virtual environment, not conda. This is to demonstrate this avenue of building a virtual environment, and allows following this tutorial without having installed conda. However, conda environments are much easier to manage.*

Open VS Code’s integrated terminal and create a Python virtual environment:

```bash
python -m venv .venv
```


Activate it:

- On Windows:

``` bash
.venv\Scripts\activate
```

- On macOS/Linux:

```bash
source .venv/bin/activate
```

## 3. Install Dependencies

Install the required dependencies using [requirements.txt](vscode-file://vscode-app/c:/Users/cakei/AppData/Local/Programs/Microsoft%20VS%20Code/resources/app/out/vs/code/electron-sandbox/workbench/workbench.html):

```
pip install -r requirements.txt
```

Optionally, you can install directly from [setup.py](vscode-file://vscode-app/c:/Users/cakei/AppData/Local/Programs/Microsoft%20VS%20Code/resources/app/out/vs/code/electron-sandbox/workbench/workbench.html):

```
pip install .
```

## 4. Launch Mesofield

Run the mesofield module in development mode from [mesofield.__main__](vscode-file://vscode-app/c:/Users/cakei/AppData/Local/Programs/Microsoft%20VS%20Code/resources/app/out/vs/code/electron-sandbox/workbench/workbench.html):

```
python -m mesofield launch --dev True
```

That’s it! This will open the main Mesofield GUI and set it up with simulated hardware for development.