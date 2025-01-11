# lammps_to_mace.ipynb

# LAMMPS to MACE Extended XYZ Converter

This tool converts LAMMPS trajectory data to the extended XYZ format required for MACE force field training.

## Description
The script processes LAMMPS trajectory files containing atomic positions and forces, combines them with energy data, and generates an extended XYZ file in the format required for MACE training.

## Requirements
- Python 3.x
- NumPy
- ASE (Atomic Simulation Environment)

## Input Files Required
1. `trajectory.dump` - LAMMPS trajectory file containing:
  - Atomic positions
  - Forces
  - Atom types (1=O, 2=H for water)
  - Must be generated using LAMMPS dump command:
    ```
    dump 1 all custom 1000 trajectory.dump id type x y z fx fy fz
    dump_modify 1 sort id
    ```

2. `energy.dat` - File containing potential energies:
  - One value per frame
  - Generated using LAMMPS command:
    ```
    variable pe equal pe
    fix saveEnergy all print 1000 "${pe}" file energy.dat screen no
    ```

## Output
- `traj1.extxyz` - Extended XYZ file containing:
 - Number of atoms
 - Energy and lattice information
 - Atomic positions
 - Forces
 - Atom types and atomic numbers

## Usage
```python
from ase.io import read
import numpy as np

# Import the conversion script
# Run the converter
python lammps_to_mace.py
