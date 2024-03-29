[BSE paper: Hurley, Tout & Pols (2002)](https://ui.adsabs.harvard.edu/abs/2002MNRAS.329..897H/abstract)

Download the [BSE tar file on Jhurley's website](https://astronomy.swin.edu.au/~jhurley/bsedload.html)

************************************************************************

## Information on the BSE package. 

*Created by Jarrod Hurley at the Institute of Astronomy, Cambridge, UK 
in collaboration with Onno Pols and Christopher Tout. 
12th February 2000.* 

**IMPORTANT: This package must be used in conjunction with the SSE package for evolving single stars.**

Information on the BSE package can be found in the paper: 

*"Evolution of binary stars and the effect of tides on binary 
 populations"*
 Hurley J.R., Tout C.A., & Pols O.R., 2002, MNRAS, 329, 897.

and more information on the SSE package can be found in the paper: 

*"Comprehensive analytic formulae for stellar evolution as a function 
 of mass and metallicity"*
 Hurley J.R., Pols O.R., & Tout C.A., 2000, MNRAS, 315, 543. 

Any queries that are not answered by referring to these texts, or by 
reading the comments in the programs, can be addressed to: 
  jhurley@astro.swin.edu.au  

There have been some updates to the code subsequent to the publication 
of the BSE paper and these are documented in the header of the [evolv2.f](./evolv2.f)
routine. 

************************************************************************

Stellar mass range: `0.1` -> `100` Msun 

Metallicity range:  `0.0001` -> `0.03` (`0.02` is solar) 

Period range:       `all` 

Eccentricity Range: `0.0` -> `1.0`

************************************************************************

### The BSE package contains the following FORTRAN files: 

* `bse.f`       - Main routine. Evolves one binary and creates data files. 
* `const_bse.h` - parameter file 
* `evolv2.f`    - routine that controls the evolution of the binary 
* `binary.in`   - input file for bse.f 
* `comenv.f`    - common envelope evolution
* `corerd.f`    - estimates the core radius of a giant-like star
* `deltat.f`    - determines stellar evolution update timestep 
* `dgcore.f`    - determines the outcome when two degenerate cores merge 
* `gntage.f`    - calculates parameters of new star resulting from a merger 
* `hrdiag.f`    - decides which evolution stage the star is
              currently at and then the appropriate luminosity, radius
              and core mass are calculated 
* `instar.f`    - sets the collision matrix
* `kick.f`      - generates supernova kick and adjusts orbital parameters 
* `Makefile`  - f77 compiler. Use command `make bse`
* `mix.f`       - models stellar collisions
* `mlwind.f`    - contains the mass loss prescription 
* `mrenv.f`     - calculates envelope parameters
* `ran3.f`      - random number generator
* `rl.f`        - calculates Roche-lobe radius 
* `star.f`      - derives the landmark timescales and luminosities 
              that divide the various evolution stages. 
* `zcnsts.f`    - sets all the constants of the formulae which depend on 
              metallicity (there is no Z dependence elsewhere) 
* `zdata.h`     - contains all the coefficient values for zcnsts 
* `zfuncs.f`    - all the formulae as a collection of separate functions

************************************************************************

The main routine bse.f contains comments that should (hopefully?)
make everything self-explanatory. It is simply an example to show how 
EVOLV2 should be used. 
Information is also contained in the headers of some routines. In particular, 
see bse.f for an explanation of the input.  

In the case of EVOLV2 being called in a loop over many stars 
be careful to initialise each new star, i.e. 

`mass(i) = mass0(i)`

`kstar(i) = 1`

`epoch(i) = 0.0`

`ospin(i) = 0.0`

`tphys = 0.0`

as well as setting the masses (mass0), period (tb) and eccentricity (ecc). 

However, the routine ZCNSTS only needs to be called each time you change
metallicity.

You may not want to use bse.f at all and instead, for example, prefer to use 
EVOLV2 directly as the main routine. 
Also, you may want to utilise the individual subroutines in different ways. 

**PROBLEMS: if the program stops with a 'FATAL ERROR' then more information should be contained in the fort.99 file. When you have identified the initial conditions that produce the error then please contact me and I may help to fix the bug - assuming it can be reproduced!**

************************************************************************

### Definitions of the evolution types for the stars:

 KW
* 0 - deeply or fully convective low mass MS star
* 1 - Main Sequence star
* 2 - Hertzsprung Gap
* 3 - First Giant Branch
* 4 - Core Helium Burning
* 5 - First Asymptotic Giant Branch
* 6 - Second Asymptotic Giant Branch
* 7 - Main Sequence Naked Helium star
* 8 - Hertzsprung Gap Naked Helium star
* 9 - Giant Branch Naked Helium star
* 10 - Helium White Dwarf
* 11 - Carbon/Oxygen White Dwarf
* 12 - Oxygen/Neon White Dwarf
* 13 - Neutron Star
* 14 - Black Hole
* 15 - Massless Supernova

**Good luck!**

************************************************************************
