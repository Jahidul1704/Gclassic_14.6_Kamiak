# Gclassis_14.6
# Geos_chem_14.6
# For your cluster, you have to check the availability of GCC or Intel NetCDF, OpenMPI, and CMake modules.
# In Kamiak hpc(WSU hpc) it has built in gcc, intel, openmpi, netcdf and cmake. For compiling geoschem classis it is require to use upgraded netcdf libraries which are not available in Kamiak.
# 1. First step is to install upgraded netcdf in kamiak or just copy this module from other in my case it is in this directory 
/data/lab/meng/jahidul/netcdd
# 2. Then load all the modules GCC or Intel NetCDF, OpenMPI, and CMake modules.
module load intel
module load hdf5
module load netcdf
module load openmpi

# 3. Then follow the guidelines from this website https://geos-chem.readthedocs.io/en/latest/getting-started/quick-start.html
# 4.  Download the source code:
git clone --recurse-submodules https://github.com/geoschem/GCClassic.git GCClassic

cd GCClassic

# 4.Create a run directory
**Navigate to the run/ subdirectory. To create a run directory, run the script ./createRunDir.sh:**

cd run/

./createRunDir.sh
# 5. And then create run directory as your choice
# 6. Go to run directory that created before like
cd /path/to/gc_4x5_merra2_fullchem 
# 7. go to build directory 
 cd build
# 8.Now this is modification for kamiak hpc

export NETCDF_ROOT=data/lab/meng/jahidul/netcdf

export NETCDF_F90_INCLUDE_DIR=data/lab/meng/jahidul/netcdf/include

export NETCDF_C_INCLUDE_DIR=data/lab/meng/jahidul/netcdf/include

export NETCDF_F_LIBRARY=data/lab/meng/jahidul/netcdf/lib/libnetcdff.so

export NETCDF_C_LIBRARY=data/lab/meng/jahidul/netcdf/lib/libnetcdf.so"

# 9. Then do
"cmake ../CodeDir -DRUNDIR=..   -DNETCDF_C_LIBRARY=$NETCDF_C_LIBRARY   -DNETCDF_F_LIBRARY=$NETCDF_F_LIBRARY   -DNETCDF_C_INCLUDE_DIR=$NETCDF_C_INCLUDE_DIR   -DNETCDF_F90_INCLUDE_DIR=$NETCDF_F90_INCLUDE_DIR   -DCMAKE_PREFIX_PATH=$NETCDF_ROOT"
# 10. Then do 
make -j
make install
# 11. Great, now your compilation and installation are completed.
# 12.Now you can download input files by using dryrun simulation that given in geoschem website
# 13. Then make change HEMCO_Config.rc, geoschem_config.yml and HISTORY.rc as like as your wish
# 14. Now you just need to create batch job "geoschem_classic.sh" 
# 15. Then run geoschem_classic.sh by using " sbatch geoschem_classic.sh"
