# UCERF3-TD Known Issues and Corrections

## Subsection Ordering Bug

UCERF3 users Gabriele Coccia and Paolo Bazzurro discovered an issue with subsection ordering in the electronic subplements to the UCERF3-TD model. This also affected a few of the figures from the final BSSA paper.

### Bug summary

Sub section probability CSV data files, posted in the UCERF3-TD electronic supplements (for example: http://opensha.usc.edu/ftp/UCERF3-TimeDependentSupplements/all_5yr/sub_section_probabilities.csv), were originally sorted by name. This led to an incorrect ordering of subsections on faults with 10 or more subsections, for example:

```
Fault x Subsection 1
Fault x Subsection 10
Fault x Subsection 11
Fault x Subsection 2
Fault x Subsection 3
...
Fault x Subsection 9
```

The data, however, was sorted by subsection number (1, 2, 3, etc). All files have been updated, with the original (with the bug) data [preserved here](http://opensha.usc.edu/ftp/TimeDependentPreliminary_nofix_redo/). The corrected files were moved into place to replace the original (with bug) files on 4/12/2017.

### BSSA Figure Updates

The following figures from the UCERF3-TD BSSA figures were sensitive to this bug and have been updated online:

Figure 5:

a) Mean Time Dep Probs:
 * ORIGINAL: http://opensha.usc.edu/ftp/TimeDependentPreliminary_nofix_redo/m6.7_30yr/SubsectionProbabilityMaps/U3_TimeDep_Mean.pdf
 * FIXED: http://opensha.usc.edu/ftp/UCERF3-TimeDependentSupplements/m6.7_30yr/SubsectionProbabilityMaps/U3_TimeDep_Mean.pdf

b) UCERF3-TD Prob Gain
 * ORIGINAL: http://opensha.usc.edu/ftp/TimeDependentPreliminary_nofix_redo/m6.7_30yr/SubsectionProbabilityMaps/U3_Gain.pdf
 * FIXED: http://opensha.usc.edu/ftp/UCERF3-TimeDependentSupplements/m6.7_30yr/SubsectionProbabilityMaps/U3_Gain.pdf

Figure 13 (deformation model branch sensitivity):

* ORIGINAL: http://opensha.usc.edu/ftp/TimeDependentPreliminary_nofix_redo/m6.7_30yr/BranchSensitivityMaps/DeformationModels_combined.pdf
* FIXED: http://opensha.usc.edu/ftp/UCERF3-TimeDependentSupplements/m6.7_30yr/BranchSensitivityMaps/DeformationModels_combined.pdf

Figure 14 (scaling relationship sensitivity)

* ORIGINAL: http://opensha.usc.edu/ftp/TimeDependentPreliminary_nofix_redo/m6.7_30yr/BranchSensitivityMaps/ScalingRelationships_combined.pdf
* FIXED: http://opensha.usc.edu/ftp/UCERF3-TimeDependentSupplements/m6.7_30yr/BranchSensitivityMaps/ScalingRelationships_combined.pdf

Figure 15 (probability model sensitivity)

* ORIGINAL: http://opensha.usc.edu/ftp/TimeDependentPreliminary_nofix_redo/m6.7_30yr/BranchSensitivityMaps/MagDepAperiodicity_combined.pdf
* FIXED: http://opensha.usc.edu/ftp/UCERF3-TimeDependentSupplements/m6.7_30yr/BranchSensitivityMaps/MagDepAperiodicity_combined.pdf