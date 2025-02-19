---
parent: "[[ConfigController]]"
controls:
  - "[[ExperimentConfig]]"
---
```python
class ConfigController(QWidget):

    def __init__(self, cfg: 'ExperimentConfig'):
        super().__init__()
        self.config = cfg
...
...
...

def _add_note(self):
	"""
	Open dialog to get note from the user,save it to the ExperimentConfig.notes[] List
	"""

	time = datetime.datetime.now().strftime("%Y-%m-%d %H:%M:%S")
	text, ok = QInputDialog.getText(self, 'Add Note', 'Enter your note:')
	if ok and text:
		note_with_timestamp = f"{time}: {text}"
		self.config.notes.append(note_with_timestamp)
```