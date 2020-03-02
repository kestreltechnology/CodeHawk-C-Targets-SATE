# CodeHawk-C-Targets-SATE
NIST SATE test cases prepared for analysis by the
[CodeHawk-C analyzer](https://github.com/kestreltechnology/CodeHawk-C)

## Contents
- [Description](#description)
- [Access from the CodeHawk-C analyzer](#access-from-the-codehawk-c-analyzer)
- [Applications](#applications)
  - [lighttpd](#lighttpd)
  - [nagios](#nagios)

## Description
This repository contains six of the benchmark programs used in the
2008, 2009, and 2010 SATE (Static Analysis Tool Exposition)
expositions organized by NIST. The applications have been pre-parsed
(on linux) and are ready for analysis with the CodeHawk C Analyzer.
The reason to provide a pre-parsed
version of the application is that all analyses will be
comparable. Local configuration and versions of standard
library header files may affect the proof obligations generated
and thus result in different analysis results for different
computers.

## Access from the CodeHawk-C analyzer

Add the following line to your chc/util/ConfigLocal.py file (if not
present, copy from chc/util/ConfigLocal.template):
```
    satetargets_home = os.path.expanduser('~')
    config.targets = {
    "sate": os.path.join(satetargets_home,'CodeHawk-C-Targets-SATE/targets/sate.json')
        }
```
(modify satetargets_home to hold your local path to the
CodeHawk-C-Targets-SATE directory, if necessary).
When registered in this way the
path
to the project can be specified with **sate:** followed by the name
of the project, e.g., **sate:lighttpd**, in every
script in the chc/cmdline/c-project directory. For example, to analyze
the **lighttpd** project listed below:
```
> export PYTHONPATH=$HOME/CodeHawk-C
> python chc_analyze_project.py sate:lighttpd --verbose
```
and to view the results when analysis is completed
```
> python chc_report_project.py sate:lighttpd
```
More scripts are available in the
[CodeHawk-C repository](https://github.com/kestreltechnology/CodeHawk-C/blob/master/chc/cmdline/c-project)


## Applications

### lighttpd

- *description*: version 1.4.18 of the
  [lighttpd](https://www.lighttpd.net) open-source webserver, used as
  benchmark application in
  [SATE 2008](https://samate.nist.gov/SATE2008.html)
- *size*: 89 .c files, 941 functions, 51,161 LOC
- *semantic size*: 18,528 statments, 7481 calls, 10,097 assignments
  ([more detailed statistics](targets/2008/lighttpd/latestresults/projectstats.txt))
- *primary proof obligations (ppo's)*: 242,231
- *current analysis status*: 175,011 ppo's (72.2%) proven safe or
  delegated, 67,332 ppo's (27.8%) not yet proven
  ([more detailed results](targets/2008/lighttpd/latestresults/summaryresults.txt)
  broken down by source file and proof obligation kind).
- *contract conditions*: 112 preconditions, 350 postconditions
- *analysis time*: approximately 3 hrs (single core), or 1 hr 15 mins
  (4 cores), or 35 mins (10 cores).


### nagios

- *description*: version 2.10 of the [nagios](https://www.nagios.org)
  open-source infrastructure monitoring application, used as benchmark
  application in [SATE 2008](https://samate.nist.gov/SATE2008.html)
- *size*: 25 .c files, 602 functions, 48,452 LOC
- *semantic size*: 20,163 statements, 8091 calls, 7999 assignments
  ([more detailed statistics](targets/2008/nagios/base/latestresults/projectstats.txt))
- *primary proof obligations (ppo's)*: 204,533
- *current analysis status*: 153,573 ppo's (75.1%) proven safe or
  delegated, 50,960 (24.9%) not yet proven
  ([more detailed results](targets/2008/nagios/base/latestresults/summaryresults.txt))
  broken down by source file and proof obligation kind
- *analysis time*: approximately 42 mins (4 cores)
