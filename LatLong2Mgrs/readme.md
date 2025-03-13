# Lat-Lon to MGRS Converter (PowerShell)

This repository contains a PowerShell script that converts geographic coordinates (latitude/longitude) into Military Grid Reference System (MGRS) coordinates. The script supports multiple input methods (manual entry, CSV file, and TXT file) and includes an option to save the output in the same format as the input.

## Table of Contents
- [Overview](#overview)
- [Features](#features)
- [Installation](#installation)
- [Usage](#usage)
  - [Manual Input](#manual-input)
  - [CSV File Input](#csv-file-input)
  - [TXT File Input](#txt-file-input)
- [Technical Details](#technical-details)
  - [MGRS Conversion Process](#mgrs-conversion-process)
  - [Code Structure](#code-structure)
- [Requirements](#requirements)
- [Contributing](#contributing)
- [License](#license)
- [Acknowledgements](#acknowledgements)
- [Contact](#contact)

## Overview
The Lat-Lon to MGRS Converter is a comprehensive PowerShell script that converts latitude and longitude values into MGRS coordinates. It uses UTM conversion techniques combined with grid square calculations to ensure an accurate transformation. This script is ideal for users in geospatial fields, military applications, or anyone needing to convert geographic coordinates to a standardized grid reference.

## Features
- **Multiple Input Methods:**  
  - **Manual Input:** Directly enter latitude and longitude values via the console.
  - **CSV File Input:** Process CSV files containing coordinate data by specifying the column names.
  - **TXT File Input:** Process TXT files with delimiter-separated values by specifying column indices and the delimiter.
- **Output Saving:**  
  Offers the option to save the converted output back to a file (CSV or TXT) in the same format as the original input.
- **Accurate Conversion:**  
  Combines UTM coordinate conversion and grid square identification for precise MGRS calculation.
- **Error Handling:**  
  Includes robust error handling for invalid inputs, missing data, and file read/write operations.

## Installation
1. **Clone the Repository:**
   ```bash
   git clone https://github.com/yourusername/latlon-to-mgrs.git
   ```
2. **Navigate to the Repository:**
   ```bash
   cd latlon-to-mgrs
   ```
3. **Run the Script:**
   - Ensure you are using Windows PowerShell 5.1 (or later) or PowerShell Core.
   - Execute the script with:
     ```powershell
     powershell -ExecutionPolicy Bypass -File LatLonToMGRS.ps1
     ```

## Usage
When you run the script, you will be prompted to choose one of three input methods:

### Manual Input
- **Step 1:** Select option **1**.
- **Step 2:** Enter the latitude and longitude when prompted.
- **Step 3:** The script converts the coordinates and displays the corresponding MGRS coordinate in the console.

### CSV File Input
- **Step 1:** Select option **2**.
- **Step 2:** Provide the full path to your CSV file.
- **Step 3:** Enter the column names for latitude and longitude.
- **Step 4:** The script processes each row, converts the coordinates, and displays the MGRS output.
- **Step 5:** You will be prompted to save the results to a new CSV file.

**Example CSV Format:**
```csv
Latitude,Longitude
34.052235,-118.243683
40.712776,-74.005974
```

### TXT File Input
- **Step 1:** Select option **3**.
- **Step 2:** Provide the full path to your TXT file.
- **Step 3:** Enter the column indices (starting from 0) for latitude and longitude.
- **Step 4:** Enter the delimiter used in the file (for example: `,`, `\t`, or a space).
- **Step 5:** The script processes each line, converts the coordinates, and displays the MGRS output.
- **Step 6:** You will be prompted to save the results to a new TXT file.

**Example TXT Format:**
```
ID,Latitude,Longitude,OtherData
1,34.052235,-118.243683,Data
2,40.712776,-74.005974,Data
```

## Technical Details

### MGRS Conversion Process
The conversion from latitude/longitude to MGRS is achieved through a series of steps:
1. **UTM Conversion:**  
   The `LLtoUTM` function converts geographic coordinates into UTM coordinates. Special cases (e.g., specific zones for Norway and Svalbard) are handled, and a false northing is added for locations in the southern hemisphere.
2. **100,000-Meter Grid Square Calculation:**  
   Functions such as `Get100kID` and `GetLetter100kID` calculate the grid square identifier based on the UTM easting and northing.
3. **MGRS Encoding:**  
   The `Encode` function assembles the full MGRS string, combining the UTM zone, latitude band (determined by `GetLetterDesignator`), grid square, and the residual easting and northing values.

### Code Structure
- **Constants and Helper Functions:**  
  Define necessary constants (e.g., ASCII codes) and helper functions for conversion between characters and code points as well as degree/radian conversion.
- **UTM and MGRS Functions:**  
  Core functions such as `LLtoUTM`, `LLtoMGRS`, `GetLetterDesignator`, and grid square functions handle the main conversion logic.
- **User Input & Output Handling:**  
  The main script section provides a menu-driven interface for selecting the input method, processing the data, and optionally saving the results.

## Requirements
- **PowerShell Version:**  
  Windows PowerShell 5.1 or later / PowerShell Core.
- **File Access:**  
  Ensure you have appropriate permissions to read input files and write output files in your environment.

## Contributing
Contributions are highly welcome! If you have suggestions, bug fixes, or new features, please follow these steps:
1. Fork the repository.
2. Create a new branch for your changes.
3. Submit a pull request detailing your improvements.
4. Open an issue if you encounter any problems.

