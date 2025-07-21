# CTX Polar CRS Toolbox

**CTX Polar CRS Toolbox** is a QGIS plugin designed to automatically **correct a built-in incompatibility in the custom Polar CRS used for Mars Reconnaissance Orbiter (MRO) Context Camera (CTX) images**. The plugin edits the *PolarStereographic mars* CRS of CTX raster layers on import or on demand, ensuring the proper scale factor is always set.

<<<<<<< HEAD
---

## Features

- **Automatic detection and correction** of the scale factor in imported *PolarStereographic mars* raster layers.
- Provides a **Processing algorithm** ("CRS checker") to batch-correct all applicable rasters in the current project.
- Adds a menu action: quickly run “CRS Checker” from the Plugins menu and see the number of corrected layers.
- Runs silently in the background, correcting CRS issues as CTX rasters are added, or on user demand.
=======
## Overview

CTX Polar CRS Toolbox is a QGIS plugin designed for Mars researchers and GIS specialists working with data from the Mars Reconnaissance Orbiter (MRO) Context Camera (CTX). It provides automated correction of custom Polar Stereographic CRS (Coordinate Reference Systems) associated with CTX images, specifically addressing consistent incompatibilitys in the “scale factor at natural origin” parameter present in original datasets.

The plugin’s primary goal is to automatically detect, correct, and manage custom Mars polar projections when CTX rasters are loaded into QGIS, ensuring spatial accuracy and streamlined Mars data processing.

## Features

- **Automatic CRS Correction:**
On importing a raster with a CRS named “PolarStereographic mars”, the plugin automatically patches the CRS’s scale factor to a scientifically correct value, solving recurring georeferencing incompatibilitys in CTX data.
- **Processing Toolbox Integration:**
Includes a QGIS Processing Algorithm that scans all raster layers in the project and allows batch-correction of CRS scale factors on Mars polar images.
- **Background Monitoring:**
Listens for newly added raster layers and applies corrections in real-time, without user intervention.
- **Customizable and Extensible:**
Codebase is modular, enabling easy updates or extensions to support more planetary coordinate systems.
>>>>>>> dbd4a8e (ReadME files and metadata updates)

---

## Plugin Details

| Key Info          | Value                                                                 |
|-------------------|-----------------------------------------------------------------------|
| **Name**          | CTX Polar CRS Toolbox                                                 |
| **Author**        | Quentin Betton                                                        |
| **Email**         | quentin.btn45@gmail.com                                               |
| **Minimum QGIS**  | 3.0                                                                   |
| **Version**       | 0.2                                                                   |
| **Category**      | Analysis                                                              |
| **Tags**          | python, CRS, raster, Mars, CTX                                        |
| **Experimental**  | Yes                                                                   |
| **Homepage**      | https://github.com/krockdurr/CTX_CRS_Toolbox                          |
| **Tracker**       | https://github.com/krockdurr/CTX_CRS_Toolbox/issues                   |

---

## Motivation

Mars CTX images often contain an incorrect CRS definition that results in an invalid or non-optimal scale factor parameter (`+k` or `+k_0`), impacting spatial accuracy. This plugin ensures that all rasters using the *PolarStereographic mars* CRS have their **scale factor set to 1.0**, as required.

---

## How It Works

- **Real-time Correction**: When you import a raster layer with the *PolarStereographic mars* CRS, the plugin automatically checks for incorrect scale factor values and updates them to `+k=1.0` or `+k_0=1.0` as required.
- **Manual Correction**: Use the **Plugins > CTX Polar CRS Toolbox > Run CRS Checker** menu action to scan all raster layers in the current project for this issue. Layers found with improper scale factors will be updated automatically.
- **Processing Provider**: The plugin registers a processing provider and algorithm, so you can use it in QGIS's Processing Toolbox or models.

---

## Installation

1. Download the plugin ZIP from the [GitHub repository](https://github.com/krockdurr/CTX_CRS_Toolbox).
2. In QGIS, use **Plugins > Manage and Install Plugins > Install from ZIP** and select the downloaded plugin archive.
3. Enable **CTX Polar CRS Toolbox** from the plugin manager.

---

## Usage

- **Automatic usage**: Just add CTX raster images to your QGIS project. The plugin will check and, if needed, fix the Polar CRS in the background.
- **Manual usage**: Go to **Plugins > CTX Polar CRS Toolbox > Run CRS Checker** to batch-correct all layers.

You will see a notification in QGIS's message bar indicating how many layers were modified.

---

## Algorithm Details

- Searches all raster layers for the CRS named *PolarStereographic mars*.
- Parses the `+k` or `+k_0` parameter in the PROJ string.
- If not set to `1.0`, creates and assigns a corrected CRS to the raster layer.
- Provides feedback about which layers were found and fixed.

<<<<<<< HEAD
---
=======
### Customization

- The correction value for the scale factor is 1.0 by default.
- To change this, modify the relevant value in:
    - `RasterCrsListener.set_crs_scale_factor(...)` for background-auto mode.
    - The algorithm code inside `processAlgorithm()` for batch adjustment.


## File Structure

```plaintext
ctx_polar_crs_toolbox_algorithm.py   # Main Processing algorithm logic
ctx_polar_crs_toolbox_provider.py    # Registers algorithms to QGIS
ctx_polar_crs_toolbox.py             # Plugin entry, background monitor
__init__.py                          # QGIS plugin bootstrap
metadata.txt                         # Plugin metadata
test/                                # Unit/integration tests
help/                                # Sphinx-based documentation templates
scripts/                             # Development scripts
README.txt / README.html             # Human-readable plugin info
```


## Troubleshooting

- **Plugin Not Loading:**
Ensure QGIS version ≥ 3.0. Check for correct placement in the plugins directory and verify there are no syntax or indentation incompatibilitys in custom files.
- **No CRS Correction Applied:**
Check that the raster CRS description is exactly “PolarStereographic mars”. The name is case-sensitive and must match what your data uses.
- **Console Output:**
For detailed logging, start QGIS from a terminal. Correction actions are reported in the console; for GUI user messages, consider adding message bar notifications.


## Development \& Customization

- **Extending Correction Logic:**
Modify CRS detection or patching functions in `RasterCrsListener` or the processing algorithm for more custom cases or to support additional Mars projections.
- **Adding Parameters:**
To allow users to specify the scale factor interactively, define a `QgsProcessingParameterNumber` in `initAlgorithm()`.
- **Testing:**
Unit and integration tests are provided in the `test/` folder. Run with pytest or your test runner of choice.
- **Contributing:**
Contributions are welcome! Please use the GitHub issues and pull request system.


## Contact \& Support

- Author: Quentin Betton
- Email: quentin.btn45@gmail.com
- GitHub: [krockdurr/CTX_CRS_Toolbox](https://github.com/krockdurr/CTX_CRS_Toolbox)
- Issue Tracker: [krockdurr/CTX_CRS_Toolbox/issues](https://github.com/krockdurr/CTX_CRS_Toolbox/issues)

>>>>>>> dbd4a8e (ReadME files and metadata updates)

## License

This plugin is free software: you can redistribute it and/or modify it under the terms of the **GNU General Public License** as published by the Free Software Foundation, either version 2 of the License or (at your option) any later version.

---

## Support and Issues

- Report bugs or request features on the [GitHub Issue Tracker](https://github.com/krockdurr/CTX_CRS_Toolbox/issues).
- Contact: **quentin.btn45@gmail.com**

---

## Related

- Designed for Mars remote sensing and planetary geospatial analysis.
- Useful for anyone working with CTX images in QGIS and needing robust, correct spatial referencing.

---

*Developed by Quentin Betton, 2025.*
