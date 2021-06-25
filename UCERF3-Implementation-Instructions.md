## Overview

All UCERF3 materials, from inversions to solutions to earthquake rupture forecasts, were created using OpenSHA. This page provides support for those looking to use the UCERF3 model, both from within OpenSHA and without. 

## UCERF3 Fault System Solutions

This is the appropriate starting point for those wishing to use the UCERF3 model outside OpenSHA. A [Fault System Solution](UCERF3-Fault-System-Solutions) is a ZIP file that contains all information relevant to using UCERF3 as an earthquake source model. When using these files it is important to be aware of the following:

* It is often easier to work initially with "branch-averaged" solutions.
* Gridded seismicity (or background) sources are composed of up to two Magnitude frequency distributions (MFDs) at each 0.1° x 0.1° spaced grid node. One is "associated" (as in small earthquake associated with any faults in a grid cell) and the other is "unassociated" (as in independent of any faults). These two MFDs must be added to obtain the total off-fault, gridded, or background seismicity source rate.
* All rupture rates in a UCERF3 solution file are NOT declustered rates. To obtain declustered rates, all supra-seismogenic ruptures (those defined as finite faults) must be scaled by 3%. Gridded or background source rates must be scaled in a magnitude dependent manner according to the OpenSHA ​GardnerKnopoffAftershockFilter. 
* 3D finite representations of ruptures may be created from the individual fault sections defined in a solution file. For details on how to stitch the sections together in order see the OpenSHA implementation of a ​[Compound Fault Surface](https://opensha.org/Legacy-Fault-System-Solution#compound-fault-system-solution-files). Also see the [OpenSHA ​Simple Fault Geometry](https://opensha.org/Glossary#simple-fault) page for more details on constructing a 3D finite fault surface. 
* Details on the [fault system solution file format](https://opensha.org/Legacy-Fault-System-Solution).

Following the above guidelines will ensure consistency with hazard calculations performed by the USGS for the 2014 update to the National Seismic Hazard Map (NSHM).

## UCERF3 ERFs

[This page](UCERF3-ERFs) provides details on using UCERF3 solutions within the OpenSHA framework as earthquake rupture forecasts (ERFs). 

## UCERF3 Time Dependent Rate Calculator

[This page](UCERF3-Time-Dependent-Rate-Calculator) provides a tool which can be used to calculate UCERF3-TD probabilities and equivalent annualized rates for a [UCERF3 Fault System Solution](UCERF3-Fault-System-Solutions).

## Running UCERF3 Inversions

See [this page](Running-UCERF3-Inversions) if you are interested in running UCERF3 inversions. Most users will opt to use the already computed [UCERF3 Fault System Solutions](UCERF3-Fault-System-Solutions).