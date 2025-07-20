# CTX Polar CRS Toolbox QGIS Plugin

**Version:** 0.2<br>
**Author:** Quentin Betton<br>
**Contact:** quentin.btn45@gmail.com<br>
**License:** GNU General Public License v2 or later<br>
**Last Update:** 2025-07-19<br>

## Overview

CTX Polar CRS Toolbox is a QGIS plugin designed for Mars researchers and GIS specialists working with data from the Mars Reconnaissance Orbiter (MRO) Context Camera (CTX). It provides automated correction of custom Polar Stereographic CRS (Coordinate Reference Systems) associated with CTX images, specifically addressing consistent errors in the “scale factor at natural origin” parameter present in original datasets.

The plugin’s primary goal is to automatically detect, correct, and manage custom Mars polar projections when CTX rasters are loaded into QGIS, ensuring spatial accuracy and streamlined Mars data processing.

## Features

- **Automatic CRS Correction:**
On importing a raster with a CRS named “PolarStereographic mars”, the plugin automatically patches the CRS’s scale factor to a scientifically correct value, solving recurring georeferencing errors in CTX data.
- **Processing Toolbox Integration:**
Includes a QGIS Processing Algorithm that scans all raster layers in the project and allows batch-correction of CRS scale factors on Mars polar images.
- **Background Monitoring:**
Listens for newly added raster layers and applies corrections in real-time, without user intervention.
- **Customizable and Extensible:**
Codebase is modular, enabling easy updates or extensions to support more planetary coordinate systems.


## Installation

1. **Prerequisites:**
    - QGIS 3.x (minimum version: 3.0)
    - Basic familiarity with adding plugins from directories
2. **Copy/Symlink the Plugin Folder:**
    - Place or symlink the `ctx_polar_crs_toolbox` directory into your QGIS plugins directory
(e.g., `~/.local/share/QGIS/QGIS3/profiles/default/python/plugins/` on Linux).
3. **Restart QGIS:**
    - Open QGIS and activate the plugin via the Plugin Manager.
4. **Optional:**
    - Run tests in the `test/` subfolder for verification before large batch corrections.

## Usage Instructions

### Automatic Correction

- When a raster with the custom CRS (`PolarStereographic mars`) is imported, the plugin:
    - Detects the CRS.
    - Modifies the CRS’s scale factor parameter (`k₀`) from 0 (or the original, erroneous value) to a scientifically correct value (default: 1.0).
    - Applies this fixed CRS directly to the raster in the QGIS session.


### Processing Toolbox

- Launch the “Polar CRS tool” algorithm from the Processing Toolbox group “All layer processing”.
    - The tool will scan all loaded raster layers.
    - Any layer with the target CRS will have its projection string updated.
    - A summary message reports the number of layers modified.


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
Ensure QGIS version ≥ 3.0. Check for correct placement in the plugins directory and verify there are no syntax or indentation errors in custom files.
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


## License

CTX Polar CRS Toolbox is free software, licensed under GNU GPL v2 or later. See the source files for details.
