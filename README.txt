This is the Transport Matrix Method (TMM) code repository. It includes both 
the core TMM time-stepping driver code (under driver/), as well as various 
biogeochemical models (under models/) adapted to the TMM framework. The driver 
code and interface to models are written using the PETSc framework 
(http://www.mcs.anl.gov/petsc/) but you don't need this code to use the TMM. 
Simply skip to step (3) below. Otherwise keep reading and if you have any 
questions feel free to email: Samar Khatiwala <samar.khatiwala@earth.ox.ac.uk>

If you use the TMM, please cite Khatiwala et al. (2005; https://doi.org/10.1016/j.ocemod.2004.04.002) 
and Khatiwala (2007; https://doi.org/10.1029/2007GB002923). Furthermore, if you use this code 
please also cite Khatiwala (2018; https://doi.org/10.5281/zenodo.1246300). Thank you!

For a quick overview of the TMM and the PETSc driver also have a look at this excellent 
presentation by Iris Kriest: https://ftp.geomar.de/users/ikriest/TMM/MOPS-TMM-2016-June.pdf

Quick-start instructions:

1) Install PETSc (http://www.mcs.anl.gov/petsc/). The TMM driver code is compatible 
with PETSc version 3.6.x.

2) Download Matlab scripts and add to your Matlab path:
http://kelvin.earth.ox.ac.uk/spk/Research/TMM/tmm_matlab_code.tar.gz

3) Download transport matrices and related data for the ocean model of your 
choice: http://kelvin.earth.ox.ac.uk/spk/Research/TMM/TransportMatrixConfigs/
Currently, there are 3 configurations of MITgcm available online (and several 
others based on the UVic Earth System Model that I am happy to make available). 
For each, download the TMs and other associated data (e.g., MITgcm_ECCO.tar). 
Unpack. Make a note of the path to this directory (e.g., /mydisk/somewhere/MITgcm_ECCO). 
We will need it later. For some experiments you may also find it useful to download 
some miscellaneous data here (and adjust paths accordingly in the provided Matlab scripts): 
http://kelvin.earth.ox.ac.uk/spk/Research/TMM/MiscData/

4) Make a local directory and checkout the TMM driver and model codes:
cd $HOME
mkdir TMM
cd TMM/
git clone https://github.com/samarkhatiwala/tmm.git

5) For each model, e.g., tmm/models/current/mops2.0/ there is a Matlab script to generate 
all input data (e.g., mops2.0/matlab/make_input_files_for_mops_model). Change the top-level 
path at the very top of the script (and, depending on the model, some paths to other data 
files), change any other options you want, and execute. It should generate all necessary 
input data. With luck! (If there is missing data email me for it.)

6) Compile code (e.g., for mops2.0):
cd $HOME/TMM/tmm/
mkdir Work/
cd Work
# First copy the driver code ...
cp -p $HOME/TMM/tmm/driver/current/* .
# ... and then the model specific code
cp -p $HOME/TMM/tmm/models/current/mops2.0/src/* .
make mops

7) Copy all input data created in step 5 above and run scripts 
(e.g., $HOME/TMM/tmm/models/current/mops2.0/runscripts) to Work/

8) Execute model using the example run scripts.

9) Load output using the example load_output.m script.
