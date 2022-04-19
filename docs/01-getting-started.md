# Getting Started

## Overview

The VisionEval strategic modeling system allows rapid evaluation of land use and transportation
scenarios to support scenario planning, and to develop strategies to manage transportation system
performance.

Configuring and running VisionEval scenarios is simpler and faster than using traditional travel
demand models, and more flexible and detailed than using traditional spreadsheet sketch models.
While VisionEval outputs are limited in spatial resolution, the system is very detailed in its
analysis of demographics and behavioral responses to a variety of transportation policies and system
improvements (captured in a broad range of computed performance metrics).

More detailed information on how VisionEval works and what it can do is contained in the **[Concepts
Primer](https://github.com/VisionEval/VisionEval/wiki/VisionEval-Primer)**.

The remainder of this document explains the mechanics of VisionEval: how to install it, and what to
do with it after it is installed.

-   [Overview](#overview)
-   [Installation and Setup](#installation)
-   [Workflow](#workflow)
-   [Editing and Running Models](#editrun)
-   [Getting Results](#results)

<a name='installation'>Installation and Setup</a>
-------------------------------------------------

VisionEval runs within the R Statistical Environment on any system for
which R is available. There are two paths to installing VisionEval:

1.  **Install from stand-alone Windows installer**:
    + **[Download a zipped folder](https://visioneval.org/category/download.html)** from the VisionEval website for a specific version of R.

    This is the simplest way to quickly get VisionEval on your computer.
    You will first need to install

    -   [R, at least version 4.0.x](https://cran.r-project.org), and
    -   [RStudio](https://www.rstudio.com/products/rstudio/download/ "Download RStudio")
        (a widely-used platform-independent R Visual Environment)

<br/><br/>

2.  **Copy, clone or 'fork' the system code repository**

  + If you area a Mac/Linux user, or if you are interested in contributing to the development of VisionEval modules, models, framework, or visualizer,
    choose this path.

    The current release is hosted at [VisionEval on **Github](https://VisionEval/VisionEval)**. Development releases are
    available at [VisionEval-dev](https://VisionEval/VisionEval-Dev). Once
    you have downloaded or cloned one of the VisionEval repositories,
    instructions for building a runtime are found in `build/Building.md`
    (or you can locate that file in the repository).

### Install for Windows

#### Pre-requisites

You will need:

   - [R, at least version 4.0.x](https://cran.r-project.org)
   - [RStudio](https://www.rstudio.com/products/rstudio/download/ "Download RStudio")

Once you have R and RStudio installed, you can retrieve the VisionEval
installer itself:

#### Installer

***[Get VisionEval Here](https://github.com/VisionEval/VisionEval-Dev/releases)***

<!-- Eventually: https://github.com/VisionEval/VisionEval/releases/download/v2.0.0/VE-installer-Windows-R4.0.3-latest.zip) -->

*Note: 530 Mb download! Packaged for R 4.0.3*

The link above will download a .zip file containing the following:

  - The VisionEval framework code
  - Sample models including VE-RSPM, VE-RPAT, VE-State and VE-ScenarioViewer
  - All necessary R packages
  - Documentation (this Getting Started document)

[See this page](https://github.com/VisionEval/VisionEval/releases/tag/v2.0.0) for eventually for other R versions
(3.6.1 - 4.0.3) and other operating systems.

#### Completing the Installation

After installing R 4.0.3 (or the version of R corresponding to the
installer you are retrieving) and RStudio, unzip the VisionEval
installer into an empty destination folder of your choice.

To complete the installation and start VisionEval, do this: 1. navigate
to the folder into which you unzipped the installer: 2. Double-click

```
**VisionEval.Rproj**
```

RStudio will start, and the VisionEval will load. You should see this
message:

```
Loading VisionEval for R 4.0.3
Welcome to VisionEval!
```

If the `VisionEval.Rproj` file does not open RStudio when you double-click it,
you can start RStudio directly, then choose `File / Open Project...` and get
to the same place. By default, RStudio remembers the project you last loaded,
so having done that once you should get back to VisionEval each time you start
RStudio (unless you work on a different project).

#### Starting VisionEval Manually<a name='changedir'></a>

If you need to start VisionEval manually for some reason, just start
RStudio (or even plain R), change into your installation folder using
  - RStudio's `Session / Set Working Directory...` menu option, or
  - In plain R, the `File / Change dir...` menu option or `setwd` command.

Then run this instruction to start VisionEval:

    source("VisionEval.R")

<a name='workflow'>Workflow of VisionEval</a>
---------------------------------------------

VisionEval models and the underlying software framework are written in
the [R programming language](https://www.r-project.org) for statistical
computing and graphics. The purpose of the model system and framework is
to enable models be created in a plug-and-play fashion from modules that
are distributed as R packages. A simple R script is used to implement a
model by initializing the model environment and then calling modules
successively. Scenarios are then constructed through a set of files that
provide variant model inputs for evaluation and comparison.

To use VisionEval to evaluate scenarios, there are several elements that
users need to set up:

1.  Select one of the [VisionEval
    models](https://github.com/VisionEval/VisionEval/wiki/VisionEval-Models),
    customizing it as needed:

    -   **[VERSPM](https://github.com/VisionEval/VisionEval-Dev/blob/readme-dev/docs/tutorials/verspm/Main.md)**
        – Regional Strategic Planning Model
    -   **[VERPAT](https://github.com/VisionEval/VisionEval/wiki/VERPAT-Tutorial-Overview)**
        – Rapid Policy Analysis Tool
    -   **[VE-State](https://github.com/VisionEval/VisionEval/wiki/VE-State-Status)**
        – VisionEval State-Level Model

    Instructions and tutorials for configuring these models are
    presented in the **[VisionEval
    Wiki](https://github.com/VisionEval/VisionEval/wiki)**, which is your
    entry point to a wealth of documentation on the VisionEval models. 

    Tutorials for each model are available as well, refer to the [visioneval.org site](https://visioneval.org/category/users.html) for details.

2.  Develop a *Base Scenario* for the region under analysis. The Base
    Scenario specifies:
    -   **Model Geography** (zone structure), reported as Marea
        (metropolitan area), AZones (county-sized), and BZones (census-tract-sized)
    -   **Base and Future Years** to be evaluated for each scenario
        (e.g. 2015 and 2040)
    -   **Local Data Files** describing Base Scenario conditions in the
        region (including both observed base year data, and estimates of
        future year conditions with no scenario policies applied)
3.  Develop variant *Future Actions* and *Scenarios*, by adjusting
    specific input elements for the Future Years. The [`VEScenario`
    sub-system](https://github.com/VisionEval/VisionEval/wiki/VERPAT-Tutorial-Multiple-Scenarios)
    (described for VERPAT, but available for any of the VisionEval
    models) contains functions to help build and run scenarios composed
    of combinations of future actions.
4.  [Run the scenarios](#editrun), either manually, or using the
    `VEScenario` sub-system
5.  [Extract the results](#results) for summarization and further
    analysis in R or export tabular data files to other data analysis
    systems.

<a name='editrun'>Editing and Running Models</a>
------------------------------------------------

As described in the model tutorials [on the
Wiki](https://github.com/VisionEval/VisionEval/wiki), a VisionEval
Scenario contains the following components:

-   The model intialization and description file, `run_model.R`
-   Global parameters in the `/defs` folder
-   Scenario Input data in the `/inputs` folder

The [documentation on the
Wiki](https://github.com/VisionEval/VisionEval/wiki) for each model
describes what needs to go into the input files and configuration
options, which of the default scenario files you need to change for your
model area, and where to obtain the data you need.

### End User Interface

VisionEval includes simple R command-line instructions for running
models and their outputs. Once you have received the
`Welcome to VisionEval!` message, you can perform these operations from the R console (either in R or RStudio):

To list the available models (including those you may create as
described below, provided you put them in the standard place), do this:

``` 
  dir("models") 
```

You'll see a list of available models:

    [1] "VE-State"         "VE-State-Staged"  "VERPAT"           "VERPAT_Scenarios"
    [5] "VERSPM"           "VERSPM_MM"        "VERSPM_Scenarios"

To open a model from that list, just do this (remember to save the
result into an R variable, using the assignment operator `<-` ):

```
  rspm <- openModel("VERSPM")
```

The resulting R object `rspm` now lets you work with the VERSPM model
and its sample scenario. You can customize the inputs to the VERSPM
model (in the "models/VERSPM" directory), or you can use this command to
copy the model and test scenario into a new model directory (which we
are calling `MY-RSPM`):

```
  myrspm <- rspm$copy("MY-RSPM") 
```

After you run that, VisionEval will tell you the directory that contains
the copy of the model and its test scenario (the exact directory will
depend on your Windows user account and where you installed VisionEval):

    "C:/Users/MyVisionEval/Documents/VisionEval/models/MY-RSPM"

You can run the sample scenario like this:

```
  myrspm$run()
```

The model will give you progress updates as it runs:

```
  Running model stage:
  C:/Users/MyVisionEval/Documents/VisionEval/models/MY-RSPM
  run_model.R: script entered
  run_model.R: library visioneval loaded
  [1] "2021-02-04 10:50:20 -- Initializing Model. This may take a while."
  [1] "2021-02-04 10:50:41 -- Model successfully initialized."
  run_model.R: initializeModel completed 
  [1] "2021-02-04 10:50:41 -- Starting module 'CreateHouseholds' for year '2010'."
  [1] "2021-02-04 10:50:44 -- Finish module 'CreateHouseholds' for year '2010'."
  ...
  [... More messages ... ]
  ...
  [1] "2021-02-04 10:56:13 -- Starting module 'CalculatePtranEnergyAndEmissions' for year '2038'."
  [1] "2021-02-04 10:56:15 -- Finish module 'CalculatePtranEnergyAndEmissions' for year '2038'."
  run_model.R: run complete.
  Model stage C:/Users/MyVisionEval/Documents/VisionEval/models/VERSPM complete
  Model Stage: /models/MY-RSPM
  Status: Complete
```

If errors are reported and you would like to see the log, you can open
this file from RStudio's file pane (in the directory in which your model
scenario is located):
 
  "C:/Users/MyVisionEval/Documents/VisionEval/models/MY-RSPM/Log_2021-02-04_10_50_20..txt"

where the `year-day-month_hour_minute_second` will be the date and time that the model run
started (what you see next to the "Initializing Model" message).

<a name='results'>Extracting Model Results</a>
----------------------------------------------

Extracting information from a completed model run should be done with
the VisionEval command line interface. First, make sure your model has
run to completion, for example by doing this:

```
  myrspm <- openModel("MY-RSPM")
  myrspm$status
  [1] "Complete"
```

If it doesn't say "Complete", please review the instructions above for
setting up and running a scenario.

Outputs from VisionEval are saved in the scenario "Datastore", which may be an [HDF5 file](https://www.hdfgroup.org/solutions/hdf5), or a
directory hierarchy containing saved R objects. The default model
scenarios all use R object storage. Both of the output file formats are
complex and difficult to manipulate manually, so you should use the VisionEval command line interface.

The Datastore is organized hierarchically into "Groups" and "Tables", with each Table containing "Fields" (a.k.a. "Datasets"), each of which is a vector of values organized by model geography, household ID or vehicle ID.  You can list the available Groups by doing this:

```
    myrspm$groups
    Group    Stage Selected
    1   2010     1      Yes
    2 Global     1      Yes
    3   2038     1      Yes
```

You can list Tables by doing this:

```
    myrspm$tables
    Group         Table Stage Selected
    1    2010     Azone     1      Yes
    2    2010 Household     1      Yes
    3    2010     Bzone     1      Yes
    4    2010    Worker     1      Yes
    5    2010     Marea     1      Yes
    6    2010   Vehicle     1      Yes
    7    2010    Region     1      Yes
    8  Global    Region     1      Yes
    9  Global     Marea     1      Yes
    10   2038     Azone     1      Yes
    11   2038 Household     1      Yes
    12   2038     Bzone     1      Yes
    13   2038    Worker     1      Yes
    14   2038     Marea     1      Yes
    15   2038   Vehicle     1      Yes
    16   2038    Region     1      Yes
```

You can get the available Fields in all the tables by doing this:

```
    flds <- myrspm$fields
```

We have in this example saved the result (an R `data.frame`) into a variable, since it has a lot of rows (the default RSPM model and scenario geography generates 473 rows). You can inspect that using R data.frame operations, or you can save it out to an external comma-separated values (CSV) file like this:

```
    write.csv(flds, file = "Field-List.csv")
```

Alternatively, you can use the `list` function to filter the list of fields and select appropriate
ones. The following command will get the names of all the fields that have been selected (that is, they are
present in at least one selected group + table):

```
    myrspm$list()
```

But mostly you'll use the list with a pattern, like this:

```
    myrspm$list(pattern="Dvmt")
```

That will show you the names of all the fields that contain "Dvmt".  Then you can select just those fields by doing this:

```
    myrspm$fields <- myrspm$list(pattern="Dvmt")
```

If you want to get a complete view of the fields you now have selected for extraction, you can do this:

```
    myrspm$list(index=TRUE)
```

Once you have figured out which groups, tables and fields you're interested in, you can extract them. Remember that if
you don't select anything, you will get the _entire_ datastore, which might be pretty big!

To extract data from a scenario Datastore, you can execute this instruction:

```
    myrspm$extract()
    Extracting data for Table Azone in Group 2010
    Extracting data for Table Bzone in Group 2010
    Extracting data for Table Household in Group 2010
    Extracting data for Table Marea in Group 2010
    [... More "Extracting Data" messages ...]
    Extracting data for Table Region in Group Global
    Write output file: /models/MY-RSPM/output/Azone_2010_1_2021-02-04_143854.csv
    Write output file: /models/MY-RSPM/output/Bzone_2010_1_2021-02-04_143854.csv
    Write output file: /models/MY-RSPM/output/Household_2010_1_2021-02-04_143854.csv
    [... More "Write output file" messages ...]
    Write output file: /models/MY-RSPM/output/Region_Global_1_2021-02-04_143854.csv
```

That will create a directory called `output` adjacent to the scenario `inputs` folder where it will
write one comma-separated file for each Table, naming the files after the Group, Table and the date
and time at which the model was run (_NOT_ the date and time at which the data was extracted). If
you perform the extract, you can verify that all the expected files are there with this command:

```
    dir("models\\MY-RSPM\\output")
```

And you should see these files:

```
  [1] "Azone_2010_1_2021-02-04_143854.csv"
  [2] "Azone_2038_1_2021-02-04_143854.csv"
  [3] "Bzone_2010_1_2021-02-04_143854.csv"
  [4] "Bzone_2038_1_2021-02-04_143854.csv"
  [5] "Household_2010_1_2021-02-04_143854.csv"
  [6] "Household_2038_1_2021-02-04_143854.csv"
  [7] "Marea_2010_1_2021-02-04_143854.csv"
  [8] "Marea_2038_1_2021-02-04_143854.csv"
  [9] "Marea_Global_1_2021-02-04_143854.csv"
 [10] "Region_2010_1_2021-02-04_143854.csv"
 [11] "Region_2038_1_2021-02-04_143854.csv"
 [12] "Region_Global_1_2021-02-04_143854.csv"
 [13] "Vehicle_2010_1_2021-02-04_143854.csv"
 [14] "Vehicle_2038_1_2021-02-04_143854.csv"
 [15] "Worker_2010_1_2021-02-04_143854.csv"
 [16] "Worker_2038_1_2021-02-04_143854.csv"
```

The default is to extract all Groups and Tables, and all the Fields within them. You can select a
subset just by pushing a list of names into the Groups, Tables or Fields (see the instructions
above). For example, the following commands will generate output files containing only the scenario
years 2010 and 2038 from the sample model, and leaving out the Global group:

```
    myrspm$groups <- c("2010","2038")
```

The groups will now look like this:

```
    myrspm$groups
    Group    Stage Selected
    1   2010     1      Yes
    2 Global     1      No
    3   2038     1      Yes
```

To clear a selection of `groups` (or `tables` or `fields`), you can just push an empty list, like this:

```
    myrspm$groups <- ""
    myrspm$tables <- ""
    myrspm$fields <- ""
```

And then the groups will again have everything selected.

```
    myrspm$groups
    Group    Stage Selected
    1   2010     1      Yes
    2 Global     1      Yes
    3   2038     1      Yes
```

A realistic example might be to select all the fields with 'vmt' in their name, from the Marea table in the
year groups.  So we would do this:

```
   myrspm$groups <- c("2010","2038")
   myrspm$tables <- "Marea"   # or c("Marea")
   myrspm$fields <- myrspm$list(pattern="vmt")
```

And we can confirm that we are going to get what we want by doing this:

```
   myrspm$list(index=TRUE)
```

And finally, we can just extract the results into files, using `myrspm$extract()`.

If you want to manipulate the model results within R, using R functions and packages, you can do the following:

```
    results <- myrspm$extract(saveTo = FALSE)
```

That instruction creates an R list of R data.frames, each of which contains a single Datastore
table, applying whatever selections you made. Be aware that extract loads the entire Datastore into
memory. So if your model is large, you may want to select a subset of groups or tables. Or you can
just save the outputs into files and then load those back into R one at a time for further
processing.

The `saveTo` option can be used to specify an alternate directory, so you can do something like the
following to create an alternate output directory with only selected groups or tables:

```
    myrspm$groups <- c("2010", "2038")
    myrspm$extract(saveTo = "years-only")
```

You will then find a directory called `years-only` next to the model scenario `inputs` containing the extracted subset.

If you try to do a new Datastore extract into an existing folder (`outputs` or whatever),
VisionEval will tell you that the directory already has things in it. You should specify the
`overwrite` parameter like this to replace the existing files:

```
    myrspm$extract(saveTo = "years-only", overwrite = TRUE)
```

If you make changes to your scenario inputs and would like to run the model again, you can clear
the results like this:

```
myrspm$clear()
```

VisionEval will ask you for confirmation, and if you type 'y' and press
`<Enter>`, the output files will be erased. You'll see something this:

```
[1] "/models/MY-RSPM/ModelState.Rda"  
[2] "/models/MY-RSPM/Datastore"  
[3] "/models/MY-RSPM/Log\_2021-02-04\_10\_50\_20.txt"
Clear ALL prior model results? (y/n/c)
y
Model results cleared. 
```

Then you can `run` your scenario again.

### Running Scenarios directly from R

Rather than use the `openModel` command line interface, it is easy to manually run a VisionEval
scenario by [changing to the directory](#changedir) that contains the scenario components and then
`source`'ing the run\_model.R script, with this R command line (or the RStudio `Code / Source
File...` menu option):

    source("run_model.R")

You can use that instruction as the basis for R scripts to automate running a lot of scenarios.

To run a VisionEval model from within an operating system batch or shell script, you should change
to your VisionEval model directory, then use the `Rscript` program to run the model (note the
directory separator will be different on a Macintosh or on Linux):

```
    cd VisionEval\models\MY-RSPM
    Rscript run_model.R
```

### Getting More Information

Up-to-date information on using VisionEval can be found on [the VisionEval
Wiki](https://github.com/VisionEval/VisionEval/wiki), including information on developing data file
inputs, validating the model outputs, and using the outputs to support planning decisions.

## OLD FROM WIKI, NEED TO INTEGRATE
## Overview

The VisionEval software framework is written in the R programming language for statistical computing and graphics.  The purpose of the model system and framework is to enable models be created in a plug-and-play fashion from modules that are also distributed as R packages. A simple R script is used to implement a model by initializing the model environment and then calling modules successively.

**Video Description of Tool installation, setup, and basic usage**

This 45 minute video was recorded during a VisionEval Training at Portland State University in September 
2019:

<iframe src="https://www.youtube.com/embed/-ylFbyLfhbw?t=2203" width="672" height="400px" data-external="1"></iframe>

## Installation and Setup 

There are two paths to getting VisionEval running:

1. **Install from stand-alone Windows installer**Download a zipped folder with all dependencies include, for a specific version of R. This is the simplest way to quickly get VisionEval on your computer. This uses the installers on the [Releases](https://github.com/VisionEval/VisionEval/releases) page and further details are available on the [Downloads page of visioneval.org](https://visioneval.org/category/download.html). This currently is designed for the Windows operating system. This path is described first.

2. **Clone or fork repository** If you area a Mac/Linux user, or if you are interested in contributing to the development of VisionEval modules, models, framework, or visualizer, choose this path.   Instructions for setting up the VisionEval development environment can be found in the <a target="_blank" href="https://github.com/VisionEval/VE-Installer">VE-Installer</a> repository.

**Install for Windows**:**[Get VisionEval Here](https://github.com/VisionEval/VisionEval/releases/download/v1.0.0/VE-installer-Windows-R3.6.1.2019-07-15.zip)**

*Note: 583 Mb download! Packaged for R 3.6.1*

[See this page for other R versions, 3.4.4 - 3.6.0](https://github.com/VisionEval/VisionEval/releases/tag/v1.0.0)

After installing R 3.6.1 and downloading the VE Installer from the link above, unzip the folder to the destination folder of your choice.

The link above will download a .zip file containing the following:
 - The VisionEval framework code
 - VE-RSPM, VE-RPAT, VE-GUI, VE-State and VE-ScenarioViewer 
 - All necessary R packages

To complete the installation and start VisionEval, simply:
   - Double-click **<tt>VisionEval.bat</tt>**

## Running VisionEval 

Once you have been welcomed to VisionEval, you can follow the instructions under "Running VE Models" on the
<a href="https://github.com/VisionEval/VisionEval/wiki/Getting-Started">Getting Started</a> page.
Your destination folder contains everything you need from the VisionEval "sources" folder.

The installation also creates some convenience functions which will run the model test scenarios or start the VE GUI:
 - <tt>vegui()</tt> to start the GUI (navigate to your destination folder to find the scenario run scripts)
 - <tt>verpat()</tt> for the VERPAT test model
 - <tt>verpat(scenarios=TRUE)</tt> to run multiple scenarios in VERPAT
 - <tt>verpat(baseyear=TRUE)</tt> to run the alternate VERPAT sample scenario
 - <tt>verspm()</tt> for the VERSPM test model
 - <tt>verspm(scenarios=TRUE)</tt> to run multiple scenarios in VERSPM

## Requirements 

If the above installation steps did not succeed, ensure that you have downloaded the appropriate version of VisionEval to match the version of R that you have installed.

### R 
The current version of VisionEval is built for the latest version of R, 3.6.1.  If you currently have another version of R installed, you can go to the [GitHub release page](https://github.com/VisionEval/VisionEval/releases) to download VisionEval for R. 

You can find the <a
href="https://cran.r-project.org/bin/windows/base/" target="_blank">R 3.6.1 installer for Windows here</a>.

### RStudio (optional)
Many users find that <a href="https://www.rstudio.com/products/rstudio/#Desktop" target="_blank">RStudio</a> is a more user-friendly version of the
standard R interface.  RStudio is particularly recommended if you plan to clone and explore the
<a target="_blank" href="https://github.com/VisionEval/VE-Installer">Visioneval source code from GitHub</a>.

**See the VERPAT [tutorial](https://github.com/visioneval/VisionEval/wiki/VERPAT-Tutorial-Running-the-Model)** for more information on running models.

### Running VEGUI to then run a model 

After installing from the stand-alone installer (path 1, above), you can run the VEGUI using the helper functions `vegui()`.

### Running Multiple Scenarios of a Model
After installing from the stand-alone installer (path 1, above), you can run the multiple scenarios examples using the helper functions `verpat(scenarios = T)` and `verspm(scenarios = T)`.

After you run the multiple scenarios tests, you can explore the relationship between input scenarios and results using VEScenarioViewer.  You can try the example interactive [VERPAT](http://htmlpreview.github.io/?https://github.com/VisionEval/VisionEval/blob/master/sources/VEScenarioViewer/verpat.html) and [VERSPM](http://htmlpreview.github.io/?https://github.com/VisionEval/VisionEval/blob/master/sources/VEScenarioViewer/verspm.html) scenario viewers (visualizers) online.

See the VERPAT [tutorial](https://github.com/visioneval/VisionEval/wiki/VERPAT-Tutorial-Multiple-Scenarios) for more information regarding the visualizers.
