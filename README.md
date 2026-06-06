# color-names

## Project Overview
A utility project to map and format color names and their corresponding hex codes or RGB values.

## What is this Project?
This repository contains tools to process color data, likely acting as a dictionary or a utility script to map generic color names to precise color codes.

## How it was done
The project uses a structured `makefile` and a formatting script (`format-colors`) to process input files from the `input` directory and generate processed color data in the `output` directory.

## Why it was done
To provide a standardized dataset or utility for handling color naming and parsing in design or development workflows.

## Tech Stack
- Make / Shell scripting
- Data formatting utilities

## Key Features
- Automated processing using Makefiles.
- Standardized input and output directories for data management.
- Formatting capabilities for parsing color representations.

## File Structure
- `format-colors`: Script/executable for processing color data.
- `makefile`: Build script to automate formatting tasks.
- `input/`: Directory for raw color data.
- `output/`: Directory for processed color data.
- `license.txt`: Project license information.

## Local Setup (if applicable)
1. Clone the repository.
2. Run `make` in the root directory to process the input files into the output directory.