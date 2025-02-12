---
github: https://github.com/napari/napari
docs: https://napari.org/stable/
---
https://forum.microlist.org/t/belatedly-announcing-pymmcore-plus-an-ecosystem-of-pure-python-tools-for-running-experiments-with-micro-manager-core/2268

[Installation Guide](https://napari.org/stable/tutorials/fundamentals/installation.html)

[napari-micromanager plugin](https://github.com/pymmcore-plus/napari-micromanager#napari-micromanager) ^293649

```shell
conda install -c conda-forge napari pyqt

conda update napari

napari
```


# Napari-Micromanager environment setup

1. Install [[MicroManager]] from [[MicroManager#^963752|here]]
	- Note the installation path somewhere C:/Program Files/Micro-Manager-2.0
2. Install the [[Dhyana 400BSI V2]]  driver for MicroManager from [[Dhyana 400BSI V2#^65d0c1|here]]
	- Follow the Tuscan camera [[Dhyana 400BSI V2#^5c9057|user guide]] for importing the driver files into the MicroManager program file folder noted above


Installation of [[Python/Napari]]

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
- On [[Napari-Micromanager environment setup]] 
```bash
pip install napari-micromanager
```
- for [[MicroManager]] adaptors:
```bash
mmcore install
```