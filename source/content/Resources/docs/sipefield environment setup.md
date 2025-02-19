

1. Install [[MicroManager]] from [[MicroManager#^963752|here]]
	- Note the installation path somewhere C:/Program Files/Micro-Manager-2.0
2. Install the [[Dhyana 400BSI V2]]  driver for MicroManager from [[Dhyana 400BSI V2#^65d0c1|here]]
	- Follow the Tuscan camera [[Dhyana 400BSI V2#^5c9057|user guide]] for importing the driver files into the MicroManager program file folder noted above


Installation of [[Napari]]

Initialize `conda` environment named `sipefield` with `Python 3.10`

``` bash
conda create -y -n sipefield -c conda-forge python=3.10
conda activate napari-env
```

install Napari
```bash
conda install -c conda-forge napari pyqt
```

update Napari
```bash
conda update napari
```

launch Napari
```bash
napari
``` 

Install [[Napari 1#^293649|micromanager plugin]]
- On [[sipefield environment setup]] 
```bash
pip install napari-micromanager
```
- for [[MicroManager]] adaptors:
```bash
mmcore install
```