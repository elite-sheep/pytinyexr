# pytinyexr

[![Build Status](https://travis-ci.org/syoyo/PyEXR.svg?branch=master)](https://travis-ci.org/syoyo/PyEXR)

Loading OpenEXR (.exr) images using Python.

pytinyexr is a forked version of PyEXR(https://github.com/ialhashim/PyEXR) and maintained by TinyEXR author(s).

It is basically a Python binding for tinyexr. Use CMake to build the module (uses pybind11). Installation script is not there, you can simply copy the resulting python module files. Supports loading functionality, saving can be easily added (pull requests welcome!).

# Usage

In the first example we show how to read an EXR image and display an EXR image with `matplotlib`.  

```python
from tinyexr import PyEXRImage
import matplotlib.pyplot as plt
import numpy as np

# The image in (A)BGR order
img = PyEXRImage('./figures/dwsample.exr')
print(img)

img_np = np.reshape(np.array(img, copy=False), (img.height, img.width, 4))[:,:,1:]

# Re-order the image to RGB 
img_np = img_np[...,::-1]
plt.imshow(img_np)
plt.show()
```



In the following sample we demonstrate how to get access to pixel values and display an EXR image with `PIL`.
```python
from tinyexr import PyEXRImage

# Load an EXR image (tinyexr backend)
img = PyEXRImage('./figures/2by2.exr')

# Print basic details
print(img)

# Pixel values access
r = img.getPixel(x,y,0)
g = img.getPixel(x,y,1)
b = img.getPixel(x,y,2)
a = img.getPixel(x,y,3)

# Numpy:
m = np.array(img, copy = False)
# or
rgb = np.reshape(np.array(rgb_img, copy = False), (rgb_img.height, rgb_img.width, 4))
# a matrix of (height x width x channels)

# Display
from PIL import Image
Image.fromarray(np.clip(np.uint8(rgb*255.0), 0, 255)).show()
```

# PyPI package

PyPI package is registered as pytinyexr: https://pypi.org/project/pytinyexr/

```
$ pip install pytinyexr
```

To install the package from source, just execute the following command in your CMD:  
```
$ pip install .
```

### For developer

For each release, upload source distribution from local.

```
$ rm -rf dist && python setup.py sdist
$ twine upload dist/*.tar.gz
```

## License

Even though original PyEXR has unclear license, I'd like to use MIT license for pytinyexr(only applicable to python binding codes).

### Third party licenses

TinyEXR is licensed under BSD license.


## Notice.

Python2.7 binary wheel is not provided.
