# Software System for Calculating ROS Concentration from Probe Concentration Data Based on ISO 24758-1

A software system for calculating the concentration of Reactive Oxygen Species (ROS) based on probe concentration data and reaction rate constants.

E. Lan, S. Liu,  Fine bubble technology — Evaluation method for determining reactive oxygen species in fine‑bubble dispersions — Part 1: Probe‑based kinetic model (ROS_Calculate software), Version 1.0 [online software]. GitHub, 2025 [viewed 2025‑07‑22].

Available at:

https://github.com/ElonLan/ROS_Calculate

## Project Overview

This software is designed to quantitatively determine the concentrations of various types of Reactive Oxygen Species (ROS) using a probe analysis method. By employing a multi-probe co-measurement approach, it overcomes the limitation of traditional methods that cannot simultaneously measure multiple ROS types. The software features a user-friendly graphical interface and a powerful calculation engine.

## Development Background

Reactive Oxygen Species (ROS) play a crucial role in environmental and biological systems. Accurately measuring the concentrations of different ROS types is essential for understanding their mechanisms of action and impact. Traditional methods are typically limited to measuring a single type of ROS, whereas in real-world environments, multiple ROS types often coexist. This software, through mathematical modeling and a multi-probe method, enables the simultaneous determination of multiple ROS types.

## Core Features

- **Simultaneous Measurement of Multiple ROS Concentrations**: Solves for multiple ROS concentrations based on a system of linear equations.
- **Flexible Calculation Methods**: Supports both Standard Analysis and Overdetermined Analysis.
- **Data Management**: Provides functions for importing, editing, and exporting data.
- **Visual Analysis**: Supports chart displays for ROS and probe concentrations.
- **Database Management**: Includes an editable database for ROS types, probes, and reaction rate constants.

## Technical Architecture

### System Architecture

The software is designed using the MVC (Model-View-Controller) architecture:

**Model Layer:**
- Calculation Engine: Implements the core algorithms for ROS concentration calculation.
- Database Management: Manages data for probes, ROS types, and reaction rate constants.

**View Layer:**
- Main Window: Provides the user interaction interface.
- Database Editor: Used for editing and managing database content.
- Result Visualization: Displays calculation results and charts.

**Controller Layer:**
- Coordinates interactions between the Model and the View.
- Handles user input and event responses.

### Requirements
- Windows Operating System

## User Guide

### Basic Workflow

1. **Prepare Data File:**
   - Create a CSV or Excel file containing probe concentration percentages.
   - The file must include a "Time" column and percentage columns for each probe (formatted as "[ProbeID]_percentage").

2. **Configure Database:**
   - View and edit ROS types, probes, and reaction rate constants via the "Database Management" function.

3. **Calculate ROS Concentration:**
   - Load the data file.
   - The software will automatically identify the probe types from the data.
   - Select the ROS types to be calculated.
   - Choose the calculation method (Standard Analysis or Overdetermined Analysis).
   - Click the "Calculate" button to execute the calculation.

4. **View and Export Results:**
   - View detailed calculation results in the results table.
   - Observe ROS concentration change trends in the visualization chart.
   - Export the result data or charts.

## Explanation of Calculation Methods

### Mathematical Model

The software is based on the reaction kinetics equations between probes and ROS, establishing a linear relationship between the rate of change of probe concentration and the ROS concentration.

**Basic Reaction Equation:**

The reaction rate equation for a probe with ROS is:
$-\frac{d[Probe]}{dt} = \sum_i k_i[Probe][ROS_i]$

**Integration Treatment:**

Integrating the equation yields:
$\ln\left(\frac{[Probe]_t}{[Probe]_0}\right) = \sum_i k_i \cdot \int_0^t [ROS_i] dt$

Where $\int_0^t [ROS_i] dt$ represents the cumulative concentration of $ROS_i$ from time 0 to t.

**Matrix Representation:**

A system of linear equations is constructed:
$A \times x = b$

- $A$: The reaction rate constant matrix ($n \times m$)
- $x$: The unknown ROS cumulative concentration vector ($m \times 1$)
- $b$: The probe concentration change vector ($n \times 1$), where each element is $\ln\left(\frac{[Probe]_t}{[Probe]_0}\right)$

### Solution Methods

Based on the relationship between the number of probes ($n$) and the number of ROS types ($m$), the software provides two solution methods:

1. **Standard Analysis ($n = m$):**
   When the number of probes equals the number of ROS types, the system of equations has a unique solution, which can be solved directly via matrix inversion:
   $x = A^{-1} \times b$

2. **Overdetermined Analysis ($n > m$):**
   When the number of probes is greater than the number of ROS types, the solution is found using the least squares method:
   $x = (A^T \times A)^{-1} \times A^T \times b$
   This method can reduce the impact of experimental errors and improve calculation accuracy.

## Software Interface

### Main Window Layout

The main window is divided into three primary areas:

**Left Control Panel:**
- Probe selection list
- ROS type selection list
- Calculation method selection
- Calculation control buttons

**Right Tabbed Pane:**
- Data Tab: Displays and manages input data.
- Results Tab: Shows calculation results.
- Visualization Tab: Displays ROS concentration charts.

**Toolbar and Menu:**
- File Operations: Open, save data and results.
- Database Management: Open the database editor.
- Help: Display help and about information.

### Database Editor

The database editor contains three tabs:

1. **ROS Type Management:**
   - List of ROS types.
   - Add, edit, and delete ROS types.

2. **Probe Management:**
   - List of probes.
   - Add, edit, and delete probes.

3. **Reaction Rate Constant Management:**
   - Reaction rate constant matrix table.
   - Set and modify the reaction rate constants between specific probes and ROS.

## Development Plan

**Current Version (v1.0)**
- [x] Basic user interface
- [x] Basic calculation engine
- [x] Database management system
- [x] Data visualization
- [x] Result export function

**Future Roadmap (v2.0)**
- [ ] Probe selection optimization algorithm
- [ ] Uncertainty analysis and error propagation
- [ ] Advanced statistical analysis functions
- [ ] Interactive 3D visualization
- [ ] Experimental design wizard

## Glossary

- **ROS**: Reactive Oxygen Species
- **Probe**: A specific compound that reacts with ROS
- **Reaction Rate Constant**: The rate constant for the reaction between a probe and an ROS
- **Cumulative Concentration**: The integrated concentration of an ROS over a specific time period
- **Instantaneous Concentration**: The concentration of an ROS at a specific point in time
- **Standard Analysis**: The calculation method where the number of probes equals the number of ROS types
- **Overdetermined Analysis**: The calculation method where the number of probes is greater than the number of ROS types

## How to Use

Download the latest `ROS_Detection.exe` program and the sample probe concentration data sheet in CSV format from Releases. Double-click the .exe file to open the software program. You can directly use the sample CSV data for plotting.

## Created By

**Nanjing Tianqi Advanced Oxidation Technology Co., Ltd.**  
[www.tqcy.top](http://www.tqcy.top)

Software created by 
Elon Lan And Liu Shu

### Contact Me
- lanqq8@gmail.com
- lanqq8@tqcy.top
