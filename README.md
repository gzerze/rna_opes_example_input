# rna_opes_example_input by Gul Zerze, December 16, 2022

# To run this set of files (the contents in the zip file), one can submit a job script with following:

# Define number of replicas
ng=8
# Which set?
s=1
# Full path to application + application name
application="/home/hzerze/PROGRAMS/gromacs-2020.5/exec/bin/gmx_2020.5_plumed mdrun"
# Define variables related to protein and ff
proot="rna"
ff="desres"
fileroot="${proot}_${ff}"
this="mcmu"

mkdir cpts

nm=$(echo "$ng - 1" | bc)
dirs=0

dirs=${dirs}" "${i}
done

options="-maxh 145 -multidir $dirs \
-v -s ${fileroot}_${this}_nd.tpr \
-x ${fileroot}_${this}_nd.xtc \
-o ${fileroot}_${this}_nd.trr \
-c ${fileroot}_${this}_nd.gro \
-e ${fileroot}_${this}_nd.edr \
-g ${fileroot}_${this}_nd.log \
-plumed plumed.dat \
-cpo ${fileroot}_${this}_nd.cpt \
-cpi ${fileroot}_${this}_nd.cpt -noappend"

echo Running on host `hostname`
echo Time is `date`
echo Directory is `pwd`

# Launch the MPI executable

srun $application $options > outfile_${proot} 2>&1

echo Time is `date`
