UCERF3 data is stored in the [FaultSystemSolution](https://opensha.org/Legacy-Fault-System-Solution) file format. There are a variety of solution files available to users, and different applications require different files. These files can be used with the [UCERF3 ERFs](UCERF3-ERFs).

## Individual Branches - Compound Fault System Solution

If you need results for one or more individual UCERF3 logic tree branches, you must use the UCERF3 Compound Fault System Solution file. This file can be downloaded here:

[http://opensha.usc.edu/ftp/ucerf3_erf/full_ucerf3_compound_sol.zip](http://opensha.usc.edu/ftp/ucerf3_erf/full_ucerf3_compound_sol.zip)

The file format is described [here](https://opensha.org/Legacy-Fault-System-Solution#compound-fault-system-solution-files). It does not contain the grid sources xml file for each branch. If this is needed, you can use the extraction utility described below.

If you need access to individual inversions for a single branch (UCERF3 averages 10 inversion runs per branch), you will need this file which contains rates.bin files for each run:

[http://opensha.usc.edu/ftp/kmilner/ucerf3/2013_05_10-ucerf3p3-production-10runs/2013_05_10-ucerf3p3-production-10runs_COMPOUND_SOL_WITH_IND_RUNS.zip](http://opensha.usc.edu/ftp/kmilner/ucerf3/2013_05_10-ucerf3p3-production-10runs/2013_05_10-ucerf3p3-production-10runs_COMPOUND_SOL_WITH_IND_RUNS.zip)

If you are interested in how the UCERF3 waterlevel affects results, you may also be interested in [this zip file](http://opensha.usc.edu/ftp/kmilner/ucerf3/2013_05_10-ucerf3p3-production-10runs/2013_05_10-ucerf3p3-production-10runs-bins.zip) which contains two files per inversion per branch. The *_run*.bin files contain the rates for each rupture, similar to the previous file. The *_run*_noMinRates.bin files contain the inverted rates before the waterlevel was added back in. To recover the waterlevel, subtract values from *_run*_noMinRates.bin from the *_run*.bin files. These files are in our [double array binary file format](https://opensha.org/Legacy-Fault-System-Solution#double-array-binary-file).

## Single Solution Extraction Utility

A java utility has been provided to aid with the extraction of single logic tree branches from a Compound Fault System Solution. First, you must either obtain OpenSHA source code and build yourself ([learn more here](https://opensha.org/Developers)) or you can download the latest complete UCERF3 jar file from here: https://github.com/opensha/opensha-ucerf3/releases

You then must run the following java class with all required arguments: scratch.UCERF3.utils.CompoundSolBranchExtractor <compound-sol-file> <branch> <output>

Arguments:

* <compound-sol-file> - Path to compound solution zip file downloaded previously
* <branch> - Logic tree branch to extract. Branch choices should be separated by underscores in a single string as described here. Example: FM3_1_ZENGBB_Shaw09Mod_DsrTap_CharConst_M5Rate7.9_MMaxOff7.6_NoFix_SpatSeisU3
* <output> - Path to output directory, or fully qualified file name. If directory is supplied, file name will be generated automatically from branch choices. 

Example to write the reference branch to /tmp:

`java -cp /path/to/opensha-ucerf3-all.jar scratch.UCERF3.utils.CompoundSolBranchExtractor /path/to/full_ucerf3_compound_sol.zip FM3_1_ZENGBB_Shaw09Mod_DsrTap_CharConst_M5Rate7.9_MMaxOff7.6_NoFix_SpatSeisU3 /tmp/`

*Note that with older versions of java this may not work for files greater than 4.1 GB (ZIP64 files). If you see an error relating to an invalid header, this is likely the problem.*

## Branch Averaged Solution

These solutions are an approximate mean model for a single Fault Model. Each rupture rate, magnitude, and rake is the weighted mean of all 720 time independent logic tree branches for that Fault Model. This means that magnitude and rake variability is discarded for a single mean value. Additionally, fault geometries can vary between logic tree branches due to aseismicity factors - this solution uses aseismicity factors derived from branch averaged slip rates. They are useful for quick calculations, but can vary substantially from the true model especially near dipping faults with variable aseismicity among logic tree branches.

Time independent hazard curves calculated with these solutions will differ from true mean (curves that were calculated for each logic tree branch independently then averaged) by 0-7%. Gridded seismicity contained in these solutions is weight averaged and captures the true mean perfectly.

They can be downloaded here:

* Fault Model 3.1: [http://opensha.usc.edu/ftp/kmilner/ucerf3/2013_05_10-ucerf3p3-production-10runs/2013_05_10-ucerf3p3-production-10runs_COMPOUND_SOL_FM3_1_MEAN_BRANCH_AVG_SOL.zip](http://opensha.usc.edu/ftp/kmilner/ucerf3/2013_05_10-ucerf3p3-production-10runs/2013_05_10-ucerf3p3-production-10runs_COMPOUND_SOL_FM3_1_MEAN_BRANCH_AVG_SOL.zip)
* Fault Model 3.2: [http://opensha.usc.edu/ftp/kmilner/ucerf3/2013_05_10-ucerf3p3-production-10runs/2013_05_10-ucerf3p3-production-10runs_COMPOUND_SOL_FM3_2_MEAN_BRANCH_AVG_SOL.zip](http://opensha.usc.edu/ftp/kmilner/ucerf3/2013_05_10-ucerf3p3-production-10runs/2013_05_10-ucerf3p3-production-10runs_COMPOUND_SOL_FM3_2_MEAN_BRANCH_AVG_SOL.zip)

Branch averaged solutions are also available for various subsets of the logic tree:

* Each Fault Model/Deformation Model: [http://opensha.usc.edu/ftp/kmilner/ucerf3/2013_05_10-ucerf3p3-production-10runs_fm_dm_sub_plots/](http://opensha.usc.edu/ftp/kmilner/ucerf3/2013_05_10-ucerf3p3-production-10runs_fm_dm_sub_plots/)
* Each Fault Model/Deformation Model/Scaling Relationship: [http://opensha.usc.edu/ftp/kmilner/ucerf3/2013_05_10-ucerf3p3-production-10runs_fm_dm_scale_sub_plots/](http://opensha.usc.edu/ftp/kmilner/ucerf3/2013_05_10-ucerf3p3-production-10runs_fm_dm_scale_sub_plots/)

## "True Mean" solution

A different type of branch averaged solution, the "true mean" solution, is also available. They are similar to the branch averaged fault system solution described above, but instead use duplicate versions of each rupture whenever a key property (rake, magnitude, area) changes. This retains all variability allowing for quick reproduction of mean UCERF3 results with a minimum set of ruptures. The [MeanUCERF3 ERF](UCERF3-ERFs#meanucerf3-erf) uses this file and also allows the user to apply various approximations to further reduce the rupture count.

Note: These solutions are not compatible with time dependent UCERF3 calculations as multiple instances of each subsection may exist, resulting in rate partitioning between instances and incorrect recurrence intervals for renewal model calculations.

* Both fault models combined: [http://opensha.usc.edu/ftp/ucerf3_erf/mean_ucerf3_sol.zip](http://opensha.usc.edu/ftp/ucerf3_erf/mean_ucerf3_sol.zip)
* FM3.1 only: [http://opensha.usc.edu/ftp/ucerf3_erf/FM3_1_mean_ucerf3_sol.zip](http://opensha.usc.edu/ftp/ucerf3_erf/FM3_1_mean_ucerf3_sol.zip)
* FM3.2 only: [http://opensha.usc.edu/ftp/ucerf3_erf/FM3_2_mean_ucerf3_sol.zip](http://opensha.usc.edu/ftp/ucerf3_erf/FM3_2_mean_ucerf3_sol.zip)