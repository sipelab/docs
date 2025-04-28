---
sources: https://forum.image.sc/t/loading-processing-and-writing-imagej-compatible-image-stacks-one-frame-at-a-time-with-tifffile-to-reduce-memory-usage/98575/5
relatives:
  - "[[Resources/Scientific Image Acquisition/Image Data/OME Data Model]]"
---

```python
from tifffile import TiffFile, TiffWriter, memmap

# if input is memory-mappable ImageJ hyperstack format
src = memmap('input.tif', mode='r')
dst = memmap('output1.tif', shape=src.shape, dtype=src.dtype, imagej=True)
for frame in range(src.shape[0]):
    dst[frame] = src[frame] + 0  # processing
del dst
del src

# iterate through multi-page TIFF
with TiffFile('input.tif') as src:
    assert src.is_imagej
    metadata = src.imagej_metadata
    with TiffWriter('output2.tif', imagej=True) as dst:
        for page in src.series[0].pages:
            frame = page.asarray()
            frame += 0  # processing
            dst.write(
                frame,
                contiguous=True,
                photometric=page.photometric,
                colormap=page.colormap,
                resolution=page.resolution,
                resolutionunit=page.resolutionunit,
                metadata=metadata,
            )
            metadata = None
```
