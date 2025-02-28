# SciAnalysis-wsy94

## Author : Kevin G. Yager
## Ported to git by : Julien Lhermitte
## Contributors: Ruipeng Li, Esther Tsai, Yugang Zhang

SciAnalysis is a set of Python scripts for batch processing of image data,
including x-ray scattering detector images. The code was written primarily by
Kevin Yager.

http://gisaxs.com/index.php/SciAnalysis

An under-developing GPT-based Agent for answering questions on SciAnalysis (Siyu Wu):

https://chatgpt.com/g/g-67b88a7cbd9c81919e3141a64d11cf5f-scianalysis-agent

INSTALL: 

 * python setup.py develop
 
 OR, simply download the package and see examples/beamlines/NSLSII_11BM_CMS/UShell/SciAnalysis_jn.ipynb for tutorial.


---# 

# SciAnalysis

## Overview

SciAnalysis is a Python-based framework for batch processing of X-ray scattering data and other image-based scientific analyses. Developed primarily by Kevin G. Yager and maintained by the Center for Functional Nanomaterials at Brookhaven National Laboratory, SciAnalysis provides tools for automated data reduction, calibration, and visualization.

### Key FeaturesMy 

- **Supports multiple data formats** including `.tiff`, `.h5`, and other standard scientific formats.
- **Built-in protocols for data analysis** such as circular averaging, sector averaging, and line cuts.
- **Calibration tools** for detector alignment, beam center correction, and energy calibration.
- **Customizable processing pipelines** to extend analysis for specific experiments.
- **Integration with beamline workflows** for automated processing of large datasets.

## Installation Guide

### 1. Install Python

- Download and install Python from [python.org](https://www.python.org/downloads/).
- Ensure you check **'Add Python to PATH'** during installation.
- Verify installation:
  ```sh
  python --version
  ```

### 2. Install Git

- Download and install Git from [gitforwindows.org](https://gitforwindows.org/).
- Verify installation:
  ```sh
  git --version
  ```

### 3. Clone SciAnalysis Repository

```sh
cd Desktop
git clone https://github.com/CFN-SoftBio/SciAnalysis.git
cd SciAnalysis
```

### 4. Install Dependencies

```sh
pip install -r requirements.txt
python setup.py install
```

### 5. Verify Installation

```sh
python -c "import SciAnalysis; print(SciAnalysis.__version__)"
```

## Codebase Structure

SciAnalysis is organized into several modules:

```
SciAnalysis/
├── Base.py            # Core utilities
├── Data.py            # Data processing classes
├── Fit.py             # Curve fitting utilities
├── IO_HDF.py          # HDF5 file I/O handling
├── XSAnalysis/        # X-ray scattering analysis
│   ├── Data.py        # Handles scattering image data
│   ├── Protocols.py   # Analysis protocols
│   ├── masks/         # Detector masks
└── examples/          # Sample scripts for running analyses
```

## Core Functions and Classes

### 1. Data Handling

#### `DataLine` (SciAnalysis.XSAnalysis.Data)

- Handles 1D data such as line cuts.
- Example usage:
  ```python
  from SciAnalysis.XSAnalysis.Data import DataLine
  data = DataLine.load('datafile.dat')
  ```

#### `Data2DScattering` (SciAnalysis.XSAnalysis.Data)

- Processes 2D scattering images.
- Example:
  ```python
  from SciAnalysis.XSAnalysis.Data import Data2DScattering
  image_data = Data2DScattering('sample.tiff')
  ```

### 2. Calibration

#### `Calibration` (SciAnalysis.XSAnalysis.Tools)

- Used for setting beam center, detector distance, and masking.
- Example:
  ```python
  from SciAnalysis.XSAnalysis.Tools import Calibration
  calib = Calibration(wavelength_A=0.770088)
  calib.set_image_size(981, height=1043)
  calib.set_pixel_size(pixel_size_um=172.0)
  calib.set_beam_position(391, 549)
  ```

### 3. Protocols

#### `Protocols` (SciAnalysis.XSAnalysis.Protocols)

- Defines analysis routines for scattering experiments.
- Example:
  ```python
  from SciAnalysis.XSAnalysis import Protocols

  load_args = {'calibration': calib, 'mask': mask}
  run_args = {'verbosity': 3}
  process = Protocols.ProcessorXS(load_args=load_args, run_args=run_args)

  image_data = process.load('sample.tiff')
  process.run([image_data], [Protocols.circular_average()], output_dir='output/')
  ```

## Basic Usage with Examples

### 1. Loading Data

```python
from SciAnalysis.XSAnalysis.Data import Data2DScattering
image_data = Data2DScattering('sample.tiff')
image_data.plot(show=True)
```

### 2. Performing Calibration

```python
from SciAnalysis.XSAnalysis.Tools import Calibration
calib = Calibration(wavelength_A=0.770088)
calib.set_image_size(981, height=1043)
calib.set_pixel_size(pixel_size_um=172.0)
calib.set_beam_position(391, 549)
```

### 3. Running a Protocol

```python
from SciAnalysis.XSAnalysis import Protocols

load_args = {'calibration': calib, 'mask': mask}
run_args = {'verbosity': 3}
process = Protocols.ProcessorXS(load_args=load_args, run_args=run_args)

image_data = process.load('sample.tiff')
process.run([image_data], [Protocols.circular_average()], output_dir='output/')
```

## Expected Outputs & Troubleshooting

### 1. Output Files

- `.png`: Plots of processed data
- `.dat`: Data tables of extracted results
- `.xml`: Metadata and fitted parameters

### 2. Common Errors

| Error                                                | Solution                                                               |
| ---------------------------------------------------- | ---------------------------------------------------------------------- |
| `ModuleNotFoundError: No module named 'SciAnalysis'` | Ensure installation was successful and SciAnalysis is in `PYTHONPATH`. |
| `ImportError: No module named 'matplotlib'`          | Run `pip install matplotlib`.                                          |
| `FileNotFoundError: No such file or directory`       | Check the path of input files.                                         |

## Contributing

- Fork the repository on GitHub.
- Make changes and submit a pull request.
- Follow PEP8 style guidelines.

## License

SciAnalysis is open-source and licensed under Brookhaven Science Associates License.

## Disclaimer

This README file was generated by GPT models. While efforts have been made to ensure accuracy, ChatGPT can make mistakes. Please verify important information and refer to official SciAnalysis documentation or consult experts for critical use cases.

## Contact

For issues, contact the maintainers via [GitHub Issues](https://github.com/CFN-SoftBio/SciAnalysis/issues).

