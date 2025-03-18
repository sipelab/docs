# Goal: 

Pass the ExperimentConfig class object to a [[Resources/Software/PsychoPy]] subprocess

# Purpose:

Providing a Psychopy subprocess with access to the state of the parent process' ExperimentConfig class allowing for access to experimental parameters for data output, etc.

# Current Progress:

### Psychopy QProcess
```python
from PyQt6.QtCore import QProcess

from typing import TYPE_CHECKING
if TYPE_CHECKING:
    from mesofield.config import ExperimentConfig

def launch(config: 'ExperimentConfig', parent=None):
    """Launches a PsychoPy experiment as a subprocess with the given ExperimentConfig parameters."""

    # Build the command arguments
    args = [
        "C:\\Program Files\\PsychoPy\\python.exe",
        f'{config.psychopy_path}',
        f'{config.subject}',
        f'{config.session}',
        f'{config.save_dir}',
        f'{config.num_trials}',
        f'{config.psychopy_save_path}'
    ]

    # Create and start the QProcess
    psychopy_process = QProcess(parent)
    psychopy_process.finished.connect(parent._handle_process_finished)
    psychopy_process.start(args[0], args[1:])
    return psychopy_process
```

### ExperimentConfig Head
```Python
class ExperimentConfig:

    def __init__(self, path: str):
        self._parameters: dict = {}
        self._json_file_path = ''
        self._output_path = ''
        self._save_dir = ''
        self.hardware = HardwareManager(path)
        self.notes: list = []
```


# Notes

Using Python's `pickle` versus `dill` for serializing the object

- `dill` handles more complex objects, such as the [[ExperimentConfig]]

Some attributes cannot be pickled, such as [[pymmcore-plus]] CMMCore objects.

- Pickling uses the object's `__getstate__` and `__setstate__` methods; you can override them and ignore the fields you want. [source](https://stackoverflow.com/questions/2345944/exclude-objects-field-from-pickling-in-python)
- https://docs.python.org/3/library/pickle.html#handling-stateful-objects

## Potential Solutions:

https://oegedijk.github.io/blog/pickle/dill/python/2020/11/10/serializing-dill-references.html

# Attempts:

```python
def launch(config: 'ExperimentConfig', parent=None):

    """Launches a PsychoPy experiment as a subprocess with the given ExperimentConfig parameters."""
    
    serialized_config = dill.dumps(config, byref=True) 
    #dill handles complex objects, pickle does not

    b64_serialized_config = base64.b64encode(serialized_config).decode('ascii') 
    # Qprocesses require strings

    # Create and start the QProcess
    psychopy_process = QProcess(parent)

    psychopy_process.readyReadStandardOutput.connect(lambda: print(psychopy_process.readAllStandardOutput().data().decode()))

    psychopy_process.readyReadStandardError.connect(lambda: print(psychopy_process.readAllStandardError().data().decode()))

    psychopy_process.start(r"C:/Program Files/PsychoPy/python.exe", [r"D:\Experiment Types\Checkerboard Experiment\CheckerBar_vis_build-v0.8.py", b64_serialized_config])
```