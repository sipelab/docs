```python
import tifffile
import pyqtgraph

tiff_stack = tifffile.memmap(path/to/tiff/stack)
self.acquisition_gui.preview1.setImage(tiff_stack.T)
```


> [!NOTE] 
> For backward compatibility, image data is assumed to be in column-major order (column, row). However, most image data is stored in row-major order (row, column) and will need to be transposed before calling `setImage()`: