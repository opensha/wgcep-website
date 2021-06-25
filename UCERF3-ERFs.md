UCERF3 is a complex model comprised of many logic tree branches. Multiple ERFs are implemented in OpenSHA allowing users to access either a single logic tree branch or a mean model. This page describes the different ERFs available in OpenSHA and their uses/caveats.

## Fault System Solution ERF

Class name: scratch.UCERF3.erf.FaultSystemSolutionERF

This is the base class of all UCERF3 related ERFs, although it is also applicable to any [FaultSystemSolution](https://opensha.org/Legacy-Fault-System-Solution). It allows you to browse for a solution zip file. Available solutions are [described here](UCERF3-Fault-System-Solutions).

## UCERF3 Single Branch ERF

Class name: scratch.UCERF3.erf.UCERF3_CompoundSol_ERF

This ERF allows you to select a single logic tree branch from the 1440 time independent UCERF3 logic tree branches for calculations. It will download the full UCERF3 compound fault system solution which contains results from each individual logic tree branch ([described here](https://opensha.org/Legacy-Fault-System-Solution#compound-fault-system-solution-files), can be [downloaded ​here](http://opensha.usc.edu/ftp/ucerf3_erf/full_ucerf3_compound_sol.zip)). This can take some time (as it is an 810 MB file), so the file is cached in `~/.opensha/ucerf3_erf` where `~/` is the users home directory. This location can be changed by setting the "uc3.store" property at runtime.

## MeanUCERF3 ERF

Class name: scratch.UCERF3.erf.mean.MeanUCERF3

This is a full "true mean" fault system solution. It is similar to the branch averaged fault system solution described above, but instead uses duplicate versions of each rupture whenever a key property (rake, magnitude, area) changes. This retains all variability allowing for quick reproduction of mean UCERF3 results with a minimum set of ruptures. It also allows for the user to, optionally, apply certain approximations to reduce the rupture count (and thus hazard curve compute time) at the expense of accuracy. These approximations are described below. Like the UCERF3 Single Branch ERF, it downloads and caches files in "~/.opensha/ucerf3_erf".

Tests with various settings of the below parameters can be [found ​here](http://opensha.usc.edu/ftp/ucerf3_erf/averaging_diffs.xls). This shows the min/max/mean variation from true mean hazard curves across all NEHRP sites in California.

### Upper Depth Tolerance

Some sections have varying upper depths on different branches due to variable aseismicity values. This parameter combines upper depths within the given tolerance to reduce the subsection (and thus rupture) count. The "Use Mean Upper Depth" parameter allows you to use the average upper depth (default uses the shallower depth).

**Note with time dependence:** Time dependent UCERF3 is incompatible certain settings of this parameter. It must be set sufficiently high (e.g. 10 km) in order to prevent multiple instances of a subsection (and thus incorrect recurrence intervals). This means that it is impossible to perfectly reproduce mean time dependent UCERF3 results with this ERF, but you can get close.

### Magnitude Tolerance

Ruptures have varying magnitudes on different branches due to different scaling relationships and even variable aseismicity values. This parameter averages magnitudes within the given tolerance to reduce the ruptures substantially.

**Note:** enabling aleatory magnitude variability will first average magnitudes for each rupture!

### Rake Combining

Each Deformation Model supplies its own rakes. You can either use the DM specific rakes for each rupture, or combine otherwise identical ruptures. In this case you can use the weighted averaged rake or the rakes from a specific deformation model.
