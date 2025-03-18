---
created: 2025-02-28
---

## Creating a Component Registry System

Registry mapping for configuration attributes/devices to UI components:

1. Components are created only when relevant features exist in the configuration
2. You can easily add new types of components by adding factory methods
3. The UI updates dynamically when the configuration changes
4. The code is more maintainable with clear separation of component creation logic

```python
class ConfigController(QWidget):

    # ...existing signals...

    def __init__(self, cfg: 'ExperimentConfig'):
        super().__init__()
        self.config = cfg
        self.mmcores = cfg._cores

        # Initialize device-specific components registry
        self._component_registry = {
            # Maps device/feature -> (creation_method, layout_section)
            'led_control': (self._create_led_controls, 'buttons'),
            'camera_snap': (self._create_snap_control, 'buttons'),
            'psychopy': (self._create_psychopy_controls, 'buttons'),
            # Add more mappings as needed
        }

        # Initialize layouts dictionary to hold different layout sections
        self._layouts = {}
        self._setup_base_layout()
        self._setup_dynamic_components()
        self._refresh_config_table()

```

## 2. Create Base Layout Method
```python
def _setup_base_layout(self):
    """Create the base layout structure that will contain dynamic components."""

    main_layout = QVBoxLayout(self)

    self.setFixedWidth(500)

    # Directory selection section
    dir_layout = QHBoxLayout()
    self.directory_label = QLabel('Select Save Directory:')
    self.directory_line_edit = QLineEdit()
    self.directory_line_edit.setReadOnly(True)
    self.directory_button = QPushButton('Browse')
    dir_layout.addWidget(self.directory_label)
    dir_layout.addWidget(self.directory_line_edit)
    dir_layout.addWidget(self.directory_button)
    main_layout.addLayout(dir_layout)

    # JSON dropdown section
    json_layout = QHBoxLayout()
    self.json_dropdown_label = QLabel('Select JSON Config:')
    self.json_dropdown = QComboBox()
    json_layout.addWidget(self.json_dropdown_label)
    json_layout.addWidget(self.json_dropdown)
    main_layout.addLayout(json_layout)

    # Configuration table
    main_layout.addWidget(QLabel('Experiment Config:'))
    self.config_table = QTableWidget()
    self.config_table.setEditTriggers(QTableWidget.AllEditTriggers)
    self.config_table.horizontalHeader().setSectionResizeMode(QHeaderView.Stretch)
    main_layout.addWidget(self.config_table)

    # Create a layout for buttons that will be added dynamically
    buttons_layout = QVBoxLayout()
    main_layout.addLayout(buttons_layout)
    self._layouts['buttons'] = buttons_layout

    # Always add record button
    self.record_button = QPushButton('Record')
    buttons_layout.addWidget(self.record_button)
    self.record_button.clicked.connect(self.record)

    # Connect base signals
    self.directory_button.clicked.connect(self._select_directory)
    self.json_dropdown.currentIndexChanged.connect(self._update_config)
    self.config_table.cellChanged.connect(self._on_table_edit)
```


## 3. Create Component Factory Methods

```python

def _create_led_controls(self):
    """Factory method to create LED control buttons."""
    widgets = []

    # Test LED button
    test_led_button = QPushButton("Test LED")
    test_led_button.clicked.connect(self._test_led)
    widgets.append(test_led_button)

    # Stop LED button
    stop_led_button = QPushButton("Stop LED")
    stop_led_button.clicked.connect(self._stop_led)
    widgets.append(stop_led_button)

    return widgets

def _create_snap_control(self):
    """Factory method to create camera snap control."""

    widgets = []

    # Snap image button
    snap_button = QPushButton("Snap Image")

    # Determine which camera to use based on configuration
    if len(self.mmcores) >= 1:
        camera = self._mmc1 if hasattr(self, '_mmc1') else self._mmc
        snap_button.clicked.connect(lambda: self._save_snapshot(camera.snap()))
    widgets.append(snap_button)

    return widgets

def _create_psychopy_controls(self):
    """Factory method to create PsychoPy related controls."""
    widgets = []

    # Add Note button (typically used during PsychoPy experiments)
    add_note_button = QPushButton("Add Note")
    add_note_button.clicked.connect(self._add_note)
    widgets.append(add_note_button)

    return widgets
```


## 4. Setup Dynamic Components Method

```python

def _setup_dynamic_components(self):
    """Dynamically create UI components based on config attributes."""
    # Check for LED control capability
    has_led_control = hasattr(self.config.hardware, 'Dhyana') and hasattr(self, '_mmc1')
    # Check for camera with snap capability
    has_camera_snap = len(self.mmcores) > 0
    # Check for PsychoPy capability
    has_psychopy = hasattr(self.config, 'start_on_trigger')
    # Dictionary of features and their availability
    available_features = {
        'led_control': has_led_control,
        'camera_snap': has_camera_snap,
        'psychopy': has_psychopy,
        # Add more feature checks as needed
    }
    # Create components for available features
    for feature, available in available_features.items():
        if available and feature in self._component_registry:
            creator_method, layout_section = self._component_registry[feature]
            widgets = creator_method()
            for widget in widgets:
                self._layouts[layout_section].addWidget(widget)
```

## 5. Implement Update Method for Dynamic Reconfiguration
```python

def update_dynamic_components(self):
    """Update dynamic components based on current configuration."""

    # Clear existing dynamic components
    for layout_name, layout in self._layouts.items():
        if layout_name != 'buttons':  # Don't clear the record button
            continue

        # Remove all widgets from the layout except the record button
        while layout.count() > 1:
            item = layout.takeAt(1)
            if item.widget():
                item.widget().deleteLater()

    # Re-setup dynamic components
    self._setup_dynamic_components()

## Usage in Configuration Update Method
def _update_config(self, index):
    """Update the experiment configuration from a new JSON file."""

    json_path_input = self.json_dropdown.currentText()
    if json_path_input and os.path.isfile(json_path_input):
        try:
            self.config.load_parameters(json_path_input)
            # Refresh the GUI table
            self._refresh_config_table()
            # Update dynamic components based on new config
            self.update_dynamic_components()
        except Exception as e:
            print(f"Trouble updating ExperimentConfig from AcquisitionEngine:\n{json_path_input}\nConfiguration not updated.")
            print(e)

```




