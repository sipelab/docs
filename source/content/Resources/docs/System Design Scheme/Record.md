---
parent: "[[ConfigController]]"
signals: "[[recordStarted]]"
controls:
  - "[[Arduino]]"
  - "[[Dhyana 400BSI V2]]"
  - "[[Thorlabs CS165 MU]]"
---
```python
def record(self):
	"""Run MDA sequence with the global Config object parameters loaded from JSON."""
	from mesofield.io import CustomWriter
	import threading

	thread1 = threading.Thread(target=self._mmc1.run_mda, 
				args=(self.config.meso_sequence,), 
				kwargs={'output': CustomWriter(self.config.meso_file_path)})
	thread2 = threading.Thread(target=self._mmc2.run_mda, 
				args=(self.config.pupil_sequence,), 
				kwargs={'output': CustomWriter(self.config.pupil_file_path)})

	# Wait for spacebar press if start_on_trigger is True
	wait_for_trigger = self.config.start_on_trigger
	if wait_for_trigger == True:
		self.launch_psychopy()
		self.show_popup()

	thread1.start()
	thread2.start()
	self.config.encoder.start()
	self.recordStarted.emit() # Signals to start the MDA sequence
```