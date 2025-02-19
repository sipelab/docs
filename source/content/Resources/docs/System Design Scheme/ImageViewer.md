
A PyQt widget that displays images from a `CMMCorePlus` instance (pymmcore-plus).

This widget displays images from a single `CMMCorePlus` instance,
updating the display in real-time as new images are captured.

The image is displayed using PyQt's `QLabel` and `QPixmap`, allowing for efficient
rendering without external dependencies like VisPy.

**Parameters**
----------
parent : QWidget, optional
	The parent widget. Defaults to `None`.
mmcore : CMMCorePlus
	The `CMMCorePlus` instance from which images will be displayed.
	Represents the microscope control core.
use_with_mda : bool, optional
	If `True`, the widget will update during Multi-Dimensional Acquisitions (MDA).
	If `False`, the widget will not update during MDA. Defaults to `True`.

**Attributes**
---
clims : Union[Tuple[float, float], Literal["auto"]]
	The contrast limits for the image display. If set to `"auto"`, the widget will
	automatically adjust the contrast limits based on the image data.
cmap : str
	The colormap to use for the image display. Currently set to `"grayscale"`.

**Notes**
---
- **Image Display**: Uses a `QLabel` widget to display the image.
  The image is set to scale to fit the label size (`setScaledContents(True)`).

- **Image Conversion**: Converts images from the `CMMCorePlus` instance to `uint8`
  and scales them appropriately for display using `QImage` and `QPixmap`.

- **Event Handling**: Connects to various events emitted by the `CMMCorePlus` instance:
	- `imageSnapped`: Emitted when a new image is snapped.
	- `continuousSequenceAcquisitionStarted` and `sequenceAcquisitionStarted`: Emitted when
	  a sequence acquisition starts.
	- `sequenceAcquisitionStopped`: Emitted when a sequence acquisition stops.
	- `exposureChanged`: Emitted when the exposure time changes.
	- `frameReady` (MDA): Emitted when a new frame is ready during MDA.

- **Thread Safety**: Uses a threading lock (`Lock`) to ensure thread-safe access to
  shared resources, such as the current frame. UI updates are performed in the main
  thread using Qt's signals and slots mechanism, ensuring thread safety.

- **Timer for Updates**: A `QTimer` is used to periodically update the image
  from the core. The timer interval can be adjusted based on the exposure time,
  ensuring that updates occur at appropriate intervals.

- **Contrast Limits and Colormap**: Allows setting contrast limits (`clims`) and
  colormap (`cmap`) for the image. Currently, only grayscale images are supported.
  The `clims` can be set to a tuple `(min, max)` or `"auto"` for automatic adjustment.

- **Usage with MDA**: The `use_with_mda` parameter determines whether the widget updates
  during Multi-Dimensional Acquisitions. If set to `False`, the widget will not update
  during MDA runs.

**Examples**
--------
```python
from pymmcore_plus import CMMCorePlus
from PyQt6.QtWidgets import QApplication, QVBoxLayout, QWidget

# Initialize a CMMCorePlus instance
mmc = CMMCorePlus()

# Set up the application and main window
app = QApplication([])
window = QWidget()
layout = QVBoxLayout(window)

# Create the ImagePreview widget
image_preview = ImagePreview(mmcore=mmc)

# Add the widget to the layout
layout.addWidget(image_preview)
window.show()

# Start the Qt event loop
app.exec()
```

**Private Methods**
----------------
These methods handle internal functionality:

- `_disconnect()`: Disconnects all connected signals from the `CMMCorePlus` instance.
- `_on_streaming_start()`: Starts the streaming timer when a sequence acquisition starts.
- `_on_streaming_stop()`: Stops the streaming timer when the sequence acquisition stops.
- `_on_exposure_changed(device, value)`: Adjusts the timer interval when the exposure changes.
- `_on_streaming_timeout()`: Called periodically by the timer to fetch and display new images.
- `_on_image_snapped(img)`: Handles new images snapped outside of sequences.
- `_on_frame_ready(event)`: Handles new frames ready during MDA.
- `_display_image(img)`: Converts and displays the image in the label.
- `_adjust_image_data(img)`: Scales image data to `uint8` for display.
- `_convert_to_qimage(img)`: Converts a NumPy array to a `QImage` for display.

**Performance Considerations**
--------------------------
- **Frame Rate**: The default timer interval is set to 10 milliseconds. Adjust the interval based on your performance needs.
- **Resource Management**: Disconnect signals properly by ensuring the `_disconnect()` method is called when the widget is destroyed.


## Converting Images to QImage

- This is the GPU intensive component of this viewer, and is where any optimization to performance might be done. Images must be scaled to uint8 for QT display. 

```python
def _convert_to_qimage(self, img: np.ndarray) -> QImage:
	"""Convert a NumPy array to QImage."""

	if img is None:
		return None
	img = self._adjust_image_data(img)
	img = np.ascontiguousarray(img)
	height, width = img.shape[:2]

	if img.ndim == 2:
		# Grayscale image
		bytes_per_line = width
		qimage = QImage(img.data, width, height, bytes_per_line, QImage.Format.Format_Grayscale8)
	else:
		# Handle other image formats if needed
		return None

	return qimage
```

This function is called during the _convert_to_qimage_( )  method above. Here, the Contrast Limits (Clims) are set
```python
def _adjust_image_data(self, img: np.ndarray) -> np.ndarray:
	# NOTE: This is the default implementation for grayscale images
	# NOTE: This is the most processor-intensive part of this widget
	
	# Ensure the image is in float format for scaling
	img = img.astype(np.float32, copy=False)

	# Apply contrast limits
	if self._clims == "auto":
		min_val, max_val = np.min(img), np.max(img)
	else:
		min_val, max_val = self._clims

	# Avoid division by zero
	scale = 255.0 / (max_val - min_val) if max_val != min_val else 255.0

	# Scale to 0-255
	img = np.clip((img - min_val) * scale, 0, 255).astype(np.uint8, copy=False)

	return img
```