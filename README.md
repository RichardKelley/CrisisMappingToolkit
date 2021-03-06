# NASA Ames Crisis Mapping Toolkit

The Crisis Mapping Toolkit is a collection of algorithms and utilities for creating maps in response to crisis.
The CMT relies on [Google Earth Engine (EE)](https://earthengine.google.org/) for much of its data processing.
The CMT is released under the Apache 2 license.

The CMT is developed by the NASA Ames Intelligent Robotics Group, with generous support from the Google Crisis
Response Team and the Google Earth Engine Team.

The CMT currently provides:

- Algorithms to determine **flood extent from MODIS data**, such as
  multiple thresholding techniques, learned approaches, Dynamic Nearest
  Neighbor Search, and more.
- Algorithms to determine **flood extent from SAR data**, such as
  histogram thresholding and active contour.
- Various helpful utilities, such as:
    - An **improved visualization UI**, with a drop down menu of layers
      similar to the EE javascript playground.
    - **Local EE image download** and processing, for the occasional operation
      that cannot be done efficiently in EE.
    - A **configurable domain specification** to define problem domains and
      data sources in XML.

The CMT is under heavy development, so expect frequent changes and additional features.
Please contact Brian Coltin (brian.j.coltin at nasa dot gov) with any questions.

## Installation

- Follow the instructions for installing [Google Earth Engine for Python](https://developers.google.com/earth-engine/python_install).
- Download the CMT source code from [Github](https://github.com/bcoltin/CrisisMappingToolkit).
- Install PyQt4.
- Install the CMT with 
  ```
  python setup.py install
  ```

## Documentation

Before calling any CMT function, you must initialize EE, either by calling
ee.Initialize, or by using the cmt ee\_authenticate package:

```python
from cmt import ee_authenticate
ee_authenticate.initialize()
```

### Using the CMT UI

To use the CMT UI, replace your import of the EE map client:

```python
from ee.mapclient import centerMap, addToMap
```

with 

```python
from cmt.mapclient_qt import centerMap, addToMap
```

then use the centerMap and addToMap functions exactly as before.
That's it!

### Using the CMT LocalEEImage

See the documentation in local_ee_image.py. When you construct a LocalEEImage,
the image is downloaded from EE with the specified scale and bounding box
using getDownloadURL. You can then access individual pixels or bands as PIL Images.
Images are cached locally so if you are testing on the same image you do not need to
wait to download every time. We recommend using LocalEEImage sparingly, only for
operations which cannot be performed through EE, as downloading the entire image
is expensive in both time and bandwidth.

## Data Access

To use the data sources in the config directory, you must join the
[Crisis Mapping Toolkit Users Google Group](https://groups.google.com/forum/#!forum/crisis-mapping-toolkit-users).
Joining this group will give you the necessary permissions to view our data.

If you use the Sentinel-1 data, you agree to the [Sentinel-1 Data Use Terms and Conditions](https://scihub.esa.int/userguide/).

To access Skybox data, you must join the [Skybox for Good Google Group](https://groups.google.com/forum/#!forum/skyboxforgood).

Unfortunately, all TerraSAR-X data and the Skybox Malawi image cannot be shared.

