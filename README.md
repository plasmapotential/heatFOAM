# heatFOAM:
This repo contians the heatFOAM solver, which is a custom solver for openFOAM.  The heatFOAM solver solves the thermal diffusion equation in 3D for a solid material with temperature dependent thermal properties.  The heat flux is applied as a Neumann boundary condition, and temperature is solved throughout the bulk material.

This code is meant to be utilized with the Heat flux Engineering Analysis Toolkit (HEAT), which can be found here: https://github.com/plasmapotential/HEAT

HEAT calculates the heat flux on plasma facing component (PFC) surfaces (ie on an STL mesh).  HEAT then calls a series of openFOAM scripts to generate a volume mesh from the STL mesh.  TimeVaryingMappedFixedValue is used to interpolate this heat flux point cloud (from the STL) onto the volume mesh boundary patch, which is called STLpatch.  Then the heatFOAM solver solves for the time varying thermal diffusion throughout the PFC bulk material.

There are two directories in this repo, and each will be described below.

## source
The source directory contains source code for openFOAM.  This is a custom solver that should be placed in the following directory:

openFOAMpath/applications/solvers/custom/heatFoam

where openFOAMpath is the location of the openFOAM source code on your local machine

## heatFoamTemplate
