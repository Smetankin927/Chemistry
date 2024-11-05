The optimisation of geometry was done in two steps:

1. optimisation, ussing Avogadro openbabel tool (without this step mopac performs badly)

2. using mopac package and PM7 EF GNORM=0.01 GRAPHF ESP command, where GNORM reponsible for gradient norm dropping below 0.01 kcal/mol/Ångstrom during geometry optimization.

The output of Avogadro editor is contained in ```job.mop file```. The opimised geometry we obtain in ```job.arc``` file. Then new geometry was used for FORCE calculation in file ```job_force.mop```. But we have a problem: 

$$
ZERO POINT ENERGY      72.854 KCAL/MOL
NOTE: SYSTEM IS NOT A GROUND STATE, THEREFORE ZERO POINT
ENERGY IS NOT MEANINGFULL. ZERO POINT ENERGY PRINTED
DOES NOT INCLUDE THE  1 IMAGINARY FREQUENCIES
$$
