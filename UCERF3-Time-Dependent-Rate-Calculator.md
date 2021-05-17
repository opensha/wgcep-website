This is a command line utility for extracting time dependent probabilities and equivalent annualized rates from a UCERF3 Fault System Solution. You must have the Java Runtime Environment version 6 or greater installed on your machine and in your system path.

For more information on the UCERF3 Time Dependent model, see the ​[Main Report (2015, BSSA)](http://bssa.geoscienceworld.org/content/early/2015/03/05/0120140093.abstract) and ​[Electronic Supplements](http://opensha.usc.edu/ftp/UCERF3-TimeDependentSupplements/).

**NOTE:** This is only applicable to UCERF3 single branch or branch averaged solutions. It is **not applicable to any "true mean" solutions** that include alternative geometries for the same faults. Older versions of the branch averaged solutions files do not contain the necessary date of last event data built in and replacements should be downloaded [from here](UCERF3-Fault-System-Solutions). An error message will be displayed and the program will exit if one of these older files is used.

**WARNING:** This is provided as a service and is not exhaustively tested. No warranty is expressed or implied and by downloading this software you agree to the ​[OpenSHA license/disclaimer](https://opensha.org/License-Disclaimer).

**[Download Here](http://opensha.usc.edu/apps/opensha/UCERF3_TD_Extract/UCERF3_TD_Extract-1.3.1-10997-2015_06_05.jar)**

### Command Line Arguments

| Short  | Long  | Required?  | Description |
| --- | --- | --- | --- |
| -d <arg> | --duration <arg> | **yes** | Forecast duration in years. |
| -y <arg> | --start-year <arg> | no | Forecast start year. Default: 2014 |
| -h <arg> | --hist-open-interval-basis <arg> | no | Year basis for historical openinterval. Default: 1875 |
| -p <arg> | --prob-model <arg> | **yes** | Probability model. One or more of U3_PREF_BLEND,POISSON,BPT_LOW,BPT_MID,BPT_HIGH. Multiple entries can be comma separated. |
| -s <arg> | --solution <arg> | **yes** | Input Fault System Solution zip file |
| -o <arg> | --output-file <arg> | **yes** | Output file name |
| -b | --binary | no | Output equivalent annualized rates binary file in FSS rates.bin format. Otherwise CSV format. |
| -a | --filter-aftershocks | no | Apply aftershock filter |
| -i | --ignore-no-date-last | no | Skips check that ensures date of last event data is set on at least some fault sections. Can be used to calculate time dependent probabilities using only the historical open interval. |

### Examples

To create a CSV file with probabilities and equivalent annualized rates for for each probability model and a 5 year duration:

```
java -jar ProbDist-1.2.3-10437-2013_11_16.jar --duration 5 --start-year 2014 --solution /path/to/sol.zip --hist-open-interval-basis 1875 --prob-model  U3_PREF_BLEND,POISSON,BPT_LOW,BPT_MID,BPT_HIGH --output-file /path/to/output.csv
```

If you see any error messages that mention java heap space such as an "OutOfMemoryError?" then re-run the command with the -Xmx<MEMORY>G option directly after "java" above, replacing <MEMORY> with the amount of memory in gigabytes that is needed. "-Xmx4G" should be more than adequate if you run into problems. 

### Output

The default output is in CSV format. A truncated example is shown below:

| FSS Index | FSS Rate (1/yr) | U3_PREF_BLEND 5yr Prob | U3_PREF_BLEND Equiv Annual Rate (1/yr) | POISSON 5yr Prob | POISSON Equiv Annual Rate (1/yr) |
| --- | --- | --- | --- | --- | --- |
| 0 | 3.467132332031594E-5 | 1.793458612422435E-4 | 3.58723891268711E-5 | 1.7334159121162873E-4 | 3.4671323320325144E-5 |
| 1 | 1.581459767253252E-5 | 8.183057338995742E-5 | 1.6366784338797184E-5 | 7.906986217631751E-5 | 1.581459767253246E-5 |
| 2 | 1.1240237590986677E-5 | 5.818032401879599E-5 | 1.1636403311906143E-5 | 5.619960869773788E-5 | 1.1240237590983228E-5 |

Alternatively, if the "--binary" flag is supplied, the only equivalent annualized rates will be output in the [Double Array Binary File Format](Fault-System-Solution#double-array-binary-file). If multiple probability models are supplied, individual files will be output with the probability model name appended. 