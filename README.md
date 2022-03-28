# heatFOAM:
This repo contians the heatFOAM solver, which is a custom solver for openFOAM.  The heatFOAM solver solves the thermal diffusion equation in 3D for a solid material with temperature dependent thermal properties.  The heat flux is applied as a Neumann boundary condition, and temperature is solved throughout the bulk material.

This code is meant to be utilized with the Heat flux Engineering Analysis Toolkit (HEAT), which can be found here: https://github.com/plasmapotential/HEAT

HEAT calculates the heat flux on plasma facing component (PFC) surfaces (ie on an STL mesh).  HEAT then calls a series of openFOAM scripts to generate a volume mesh from the STL mesh.  TimeVaryingMappedFixedValue is used to interpolate this heat flux point cloud (from the STL) onto the volume mesh boundary patch, which is called STLpatch.  Then the heatFOAM solver solves for the time varying thermal diffusion throughout the PFC bulk material.

The code was written by Dr. Tom Looby.  Questions can be directed to tlooby@cfs.energy

There are two directories in this repo, and each will be described below.  At the bottom some build notes provide information about building this source code.

## source
The source directory contains source code for openFOAM.  This is a custom solver that should be placed in the following directory:

openFOAMpath/applications/solvers/custom/heatFoam

where openFOAMpath is the location of the openFOAM source code on your local machine.  Once you have placed this code in the correct location, you can compile by using the build_heatFoam script.  Alternatively, if you place the code in the aforementioned directory before building all of openFOAM from source it will also build heatFOAM.  Note that you must have already sourced your OF installation in the terminal before running build_heatFoam.  Also note that you will need the swiss army knife for openFOAM (Swak4FOAM) toolkit.

## heatFoamTemplate


## build notes
To install openfoam, follow these instructions:
https://develop.openfoam.com/Development/openfoam/-/blob/master/doc/Build.md

Make sure that before you compile, you copy the heatfoam dir to the new install so that it compiles that too.  

After compiling, make a new $FOAM_RUN dir:

mkdir -p $FOAM_RUN
cd $FOAM_RUN
cp -r $FOAM_TUTORIALS/incompressible/simpleFoam/pitzDaily .

Navigate to the swak4foam directory.  If you ran this for a previous build of OF, then you need to clean up first:

./Allwclean

Now compile swak4foam (note that you should have already loaded the OF bashrc for the version you want to compile for)

./Allwmake > log.make 2>&1

Instructions:  https://openfoamwiki.net/index.php/Installation/swak4Foam

If that doesn’t work because of libraries failing, you may need to re-download and recompile with the latest version:
https://openfoamwiki.net/index.php/Contrib/swak4Foam

For HEAT appImage you may need to edit the following files:

dashGUI.py
appImageRecipe.yml
.../openfoam/etc/bashrcHEAT
.../openfoam/etc/setupHEAT
<HEATdir>/github/source/appImageRunHEAT
