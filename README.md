# color-names

## Project Overview
A highly versatile Python command-line utility project designed to parse, normalize, and format human-readable color names and their corresponding Hex/RGB values from tabular raw text into a multitude of programming and markup languages.

## What is this Project?
This repository contains a data processing script (`format-colors`) that acts as a universal adapter. It takes tab-separated lists of color names and Hex codes (typically pasted from sources like Wikipedia's "List of Colors") and converts them into standardized machine-readable formats. It can automatically generate boilerplate code, data structures, and configuration files for multiple languages simultaneously.

## How it was done (Deep Technical Details)
- **Data Parsing & Normalization**:
  - Implemented entirely in standard Python.
  - Utilizes `re` (Regular Expressions) to sanitize color names, converting strings like "Alice Blue" into valid C/Python identifiers (e.g., `alice_blue`).
  - Implements custom hex-to-rgb decoding, gracefully handling both shorthand `#FFF` and standard `#FFFFFF` formats while computing integer R, G, B channels via base-16 conversions (`int(hx, 16)`).
- **Format Generators**:
  - Employs a dispatcher dictionary (`FORMATS`) mapping format names to specific serialization functions.
  - **C Code (`ccode`)**: Generates a standard C header/source file containing an `enum Color`, a `typedef struct ColorInfo`, and initializes an array mapping enums to structs natively.
  - **Lisp S-Expressions (`sexp`)**: Generates Lisp-friendly lists.
  - **XML**: Uses `xml.sax.saxutils.escape` to safely encode entities, outputting a standard DOM tree.
  - **JSON**: Outputs highly structured and minified JSON objects mapping color identifiers to metadata.
  - **HTML**: Dynamically generates an HTML document containing a styled data table with visual color swatches using inline CSS (`background-color`).
  - **Conf/CSV**: Supports flat file structures for simple database ingestion.
- **CLI Architecture**:
  - Built using Python's `optparse` (OptionParser) for robust command-line argument handling, allowing customized `-f` (format) and `-o` (output file) directives.
- **Build Automation**:
  - Orchestrated via a `makefile` that batches processing across the `input/` directory and deposits results into the `output/` directory for all supported file types.

## Why it was done
To eliminate the manual labor of hardcoding color palettes into various programming environments. It provides a standardized utility for handling color naming and parsing in multi-language design or development workflows.

## Tech Stack
- `python` (Standard Library: `re`, `sys`, `optparse`, `xml.sax.saxutils`)
- Make (`makefile`)

## Key Features
- **7+ Output Formats**: Supports `ccode`, `conf`, `csv`, `html`, `json`, `sexp`, and `xml`.
- **Robust Hex/RGB Engine**: Translates shorthand colors and calculates accurate byte-level RGB arrays.
- **Auto-Identifier Generation**: Ensures generated variable names conform to syntactic rules (e.g., prefixing identifiers that start with a number).
- **Automated Processing**: End-to-end execution using Makefiles.

## File Structure
- `format-colors`: Main Python executable for processing color data.
- `makefile`: Build script to automate formatting tasks across all formats.
- `input/`: Directory for raw, tab-separated color data (from Wikipedia).
- `output/`: Auto-generated output directory containing parsed data structures.
- `license.txt`: Project license information.

## Local Setup
1. Clone the repository.
2. Ensure you have Python installed.
3. Drop your raw tab-separated color text files into the `input/` directory.
4. Run `make` in the root directory. This will parse all files in `input/` and generate the respective files (.json, .xml, .c, etc.) into the `output/` directory.
5. Alternatively, run `./format-colors -f json -o mycolors.json input/mytext.txt` to execute it manually.