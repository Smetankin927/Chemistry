## Geometry optimisation
The optimisation of geometry was done in two steps:

1. optimisation, ussing Avogadro openbabel tool (without this step mopac performs badly)

2. using mopac package and *PM7 EF GNORM=0.01 GRAPHF ESP* command, where *GNORM* reponsible for gradient norm dropping below 0.01 kcal/mol/Ångstrom during geometry optimization.

The output of Avogadro editor is contained in ``job.mop file``. The opimised geometry we obtain in ```job.arc``` file.
Then new geometry was used for *FORCE* calculation in file ```job_force.mop```. But we have a problem: in ```job_force.out``` file

```
ZERO POINT ENERGY      72.854 KCAL/MOL

NOTE: SYSTEM IS NOT A GROUND STATE, THEREFORE ZERO POINT
ENERGY IS NOT MEANINGFULL. ZERO POINT ENERGY PRINTED
DOES NOT INCLUDE THE  1 IMAGINARY FREQUENCIES
```

according to [link](https://www.sparkle.pro.br/tutorial/geometry) it means that our geometry not in true ground state. We should use we must use the keyword *IRC=1**.

Creating another file ```job_force_isr.mop``` and adding *IRC=1** key, we obtain ```job_force_isr.xyz``` file with a series of geometries distorted to either side of the maximum. 
We choose 1st and last ~~just because~~ and create files ```job_force_afterIRC_first.mop``` and ```job_force_afterIRC_last.mop```, and reoptimize geometry for both (files ```.arc```). 

Then calculate *FORCE* for both using their ```.arc``` files 
1. ```job_force_afterIRC_first_opt_force.mop```
2.  ```job_force_afterIRC_last_opt_force.mop``` 

 Output ```job_force_afterIRC_last_opt_force.out```

```
HEAT OF FORMATION =      19.978696 KCALS/MOLE

ZERO POINT ENERGY      72.959 KCAL/MOL


NORMAL COORDINATE ANALYSIS (Total motion = 1 Angstrom)
```
And below we can see that all frequences are positive

```
    Root No.       1         2         3         4         5         6         7         8

                 1 B3u     1 B2g     1 Au      1 Ag      1 B3g     2 B3u     1 B1g     1 B1u 

                  65.0     339.4     346.4     514.8     567.4     720.3     818.5     870.6
```

shows us that we reach the minimum. Another output contain imaginary frequency again. 

Lets visualise our optimised geometry ```job_opt_min.mop``` (data is taken from the *job_force_afterIRC_last_opt_force* file.)


<img src="https://raw.githubusercontent.com/Smetankin927/Chemistry/refs/heads/main/first_lab/job_opt_min.jpg" width="250">

## HOMO-LUMO

For this section use Jmol and ``````job_opt_min.mgf`````` file. Useful [link](https://youtu.be/RVSUvm19qPI?si=0ia_mrCdISK7dBuR)

HOMO: -9.1596 eV

LUMO: 1.1796 eV

GAP: 10.3392 eV

<div>
<img src="https://raw.githubusercontent.com/Smetankin927/Chemistry/refs/heads/main/first_lab/HOMO.jpg" width="500">
<img src="https://raw.githubusercontent.com/Smetankin927/Chemistry/refs/heads/main/first_lab/LUMO.jpg" width="500">
</div>

## Localized Molecular orbitals

Copy ```job_opt_min.opt``` to the new ```job_localized.mop``` and add *LOCALIZE ALLVEC* keywords.

The output in Jmol shows that there 32 molecular orbitals, 1-16 are occuped, 17-32 are empty.

But there 4 types of occuped:
1. &sigma;  in double C-C bound  -20.6529 eV
2. &sigma;  in single C-C bound  -17.8685 eV
3. &sigma;  in single C-H bound  -17.3245 eV
4. &sigma;  in single C-H bound where two H atoms  -16.6449 eV
5. &pi;  in double C-C bound  -10.5791 eV

   You can find them in *job_localized_number.jpg*

## Triplet state

