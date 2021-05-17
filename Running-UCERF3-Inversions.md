## Getting and running the code

The UCERF3 inversion can be run with Java 6 and OpenSHA. First, you must either obtain OpenSHA source code and build yourself ([see here](https://opensha.org/Developers)) or you can download the latest complete distribution jar file from here: ​https://github.com/opensha/opensha-ucerf3/releases

You then must run the following java class with all required arguments: scratch.UCERF3.inversion.CommandLineInversionRunner?. The inversion is extremely memory intensive and at least 8 GB of memory are recommended. For example, to run the UCERF3 reference branch with results written to temp from a jar file:

```
java -Xmx8G -Xms8G -cp /path/to/opensha-ucerf3-all.jar scratch.UCERF3.inversion.CommandLineInversionRunner --completion-time 5h --sub-completion 1s --cool FAST_SA --nonneg LIMIT_ZERO_RATES --num-threads 100% --branch-prefix FM3_1_ZENGBB_Shaw09Mod_DsrTap_CharConst_M5Rate7.9_MMaxOff7.6_NoFix_SpatSeisU3 --directory /tmp
```

## Command Line Inversion Runner usage

The following arguments are required for any inversion:

| option  | typical value  | description |
| --- | --- | --- |
| -s,--sub-completion | 1s | This is the length of time or interations between synchronization between threads in the parallel simulated annealing framework. Append 's' for secionds, 'm' for minutes, 'h' for hours (default is millis). Typical values are 1s (1 second) |
| -time,--completion-time | 5h | This is the total length of time for the inversion. Append 's' for secionds, 'm' for minutes, 'h' for hours (default is millis). Typical values are 5h (5 hours) to ensure good convergence, although shorter times can converge quite well. |
| -t,--num-threads | 100% | number of threads (percentage of available can also be specified, for example, '50%') |
| -branch,--branch-prefix |  | Logic tree branch, for example: FM3_1_ZENGBB_Shaw09Mod_DsrTap_CharConst_M5Rate7.9_MMaxOff7.6_NoFix_SpatSeisU3. See Logic Tree Branch names below |
| -dir,--directory |  | Directory where inversion results and plots should be written |

Other optional arguments:

| option  | typical value  | description |
| --- | --- | --- |
| -cool,--cooling-schedule | FAST_SA | Simulated annealing cooling schedule. One of: CLASSICAL_SA,FAST_SA,VERYFAST_SA,LINEAR. Default: FAST_SA |
| -i,--initial-state-file |  | An initial state for the inversion can be supplied (default is all zeros). It must have already had any waterlevel subtracted. |
| -inigr,--initial-gr | (n/a) | Flag for using a GR starting model. |
| -light,--lightweight | (n/a) | Only write out a bin file for the solution. Leave the rup set file if the prefix indicates run 0. |
| -nonneg,--nonnegativity-const | LIMIT_ZERO_RATES | Nonnegativity constraint. One of: TRY_ZERO_RATES_OFTEN,LIMIT_ZERO_RATES,PREVENT_ZERO _RATES. Default: LIMIT_ZERO_RATES |
| -noplots,--no-plots | (n/a) | Flag for disabling any post inversion plot generation. |
| -perturb,--perturbation-function | UNIFORM_NO_TEMP_DEPENDENCE | Perturbation function. One of: UNIFORM_NO_TEMP_DEPENDENCE,VARIABLE_NO_TEMP_DEPENDENCE,GAUSSIAN,TANGENT,POWER_LAW,EXPONENTIAL. Default: UNIFORM_NO_TEMP_DEPENDENCE |
| -serial,--force-serial | (n/a) | Force serial (classical) simulated annealing that doesn't use multiple threads. |

Additional arguments for tweaking inversion weights and other non-production changes are described at the start of the CommandLineInversionRunner? class.

## Logic Tree Branch Names

You must specify a full logic tree branch prefix for each inversion run. This is a concatenation of one choice from each of the following logic tree branch nodes, separated by underscores. Default (reference) choices are in bold.

For example, the reference branch (bold below) would be: FM3_1_ZENGBB_Shaw09Mod_DsrTap_CharConst_M5Rate7.9_MMaxOff7.6_NoFix_SpatSeisU3

### Fault Models

| Prefix  | Description |
| --- | --- |
| FM3_1 | Fault Model 3.1 |
| FM3_2 | Fault Model 3.2 |

### Deformation Models

| Prefix  | Description |
| --- | --- |
| ABM | Average Block Model |
| NEOK | Neokinema |
| ZENGBB | Zeng B-Fault Bounded |
| GEOL | Geologic |

### Scaling Relationships

| Prefix  | Description |
| --- | --- |
| Shaw09Mod | Shaw (2009) Modified |
| HB08 | Hanks & Bakun (2008) |
| EllB | Ellsworth B |
| EllBsqrtLen | EllB M(A) & Shaw12 Sqrt Length D(L) |
| ShConStrDrp | Shaw09 M(A) & Shaw12 Const Stress Drop D(L) |

### Slip Along Rupture Models

| Prefix  | Description |
| --- | --- |
| DsrUni | Uniform |
| DsrTap | Tapered Ends |

### Inversion Models

| Prefix  | Description |
| --- | --- |
| CharConst | Characteristic (Constrained) |

### Total Mag 5 Rate

| Prefix  | Description |
| --- | --- |
| M5Rate6.5 | 6.5 |
| M5Rate7.9 | 7.9 |
| M5Rate9.6 | 9.6 |

### Max Mag Off Fault

| Prefix  | Description |
| --- | --- |
| MMaxOff7.3 | 7.3 |
| MMaxOff7.6 | 7.6 |
| MMaxOff7.9 | 7.9 |

### Moment Rate Fixes

| Prefix  | Description |
| --- | --- |
| NoFix | No Moment Rate Fixes |

### Spatial Seismicity PDF

| Prefix  | Description |
| --- | --- |
| SpatSeisU2 | UCERF2 |
| SpatSeisU3 | UCERF3 |