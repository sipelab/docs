# Goal:
ExperimentConfig Base class that defines the abstract methods and attributes that should be inherited by any subclass. I would like to standardize the features of the ExperimentConfig; parameters load from a JSON, however, they are only useful if I create a @property function for them. I would like any ExperimentConfig to gracefully load all JSON parameters in such a way that they can be called and used across a GUI software, even edited, while still retaining some form of immutability


```python
import os
import json
import pandas as pd
from abc import ABC, abstractmethod

class ExperimentConfigBase(ABC):
    """
    A base class for ExperimentConfig implementations.

    Features:
    - Gracefully loads parameters from a JSON file.
    - Provides read-only access to parameters outside the class.
    - Defines abstract methods for saving configuration, which must be implemented by subclasses.
    - Facilitates GUI usage by offering methods to convert parameters to a DataFrame.
    
    Note:
    While parameters can be updated via update_parameter, the parameters property returns a copy to
    help preserve immutability outside the class.
    """
    def __init__(self, path: str):
        self._parameters: dict = {}
        self._json_file_path: str = ""
        self._save_dir: str = os.path.abspath(path)
        self.notes: list[str] = []

    def load_parameters(self, json_file_path: str) -> None:
        """
        Loads parameters from a JSON file.
        The loaded parameters are stored in a private dictionary.
        """
        try:
            with open(json_file_path, 'r') as f:
                self._parameters = json.load(f)
                self._json_file_path = json_file_path
        except FileNotFoundError:
            print(f"File not found: {json_file_path}")
        except json.JSONDecodeError as e:
            print(f"Error decoding JSON: {e}")

    def update_parameter(self, key, value) -> None:
        """
        Updates a configuration parameter.
        Override this method in subclasses if you want to enforce stricter immutability.
        """
        self._parameters[key] = value

    @property
    def parameters(self) -> dict:
        """
        Returns an immutable copy of the parameters.
        This prevents external code from directly modifying the configuration.
        """
        return self._parameters.copy()

    def to_dataframe(self) -> pd.DataFrame:
        """
        Converts the configuration parameters to a pandas DataFrame,
        useful for displaying in GUI tables or exporting.
        """
        data = {
            'Parameter': list(self._parameters.keys()),
            'Value': list(self._parameters.values())
        }
        return pd.DataFrame(data)

    @abstractmethod
    def save_configuration(self) -> None:
        """
        Save the configuration parameters and any associated notes/data.
        Subclasses must implement the file saving routines.
        """
        pass
        
```