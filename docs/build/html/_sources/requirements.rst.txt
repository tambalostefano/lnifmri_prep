System Requirements
===================

Operating system
----------------

*lnifmri_prep* runs on \*nix-based operating systems (Linux, macOS and win-virtualized Linux OS) exclusively via command-line interface.

Software dependencies
---------------------

The package requires a working installation of *dcm2niix* and *FSL*. To succesfully run the workflow, the following packages are mandatory:

* `DCM2NIIX <https://github.com/rordenlab/dcm2niix/releases>`_
* `FSL <https://fsl.fmrib.ox.ac.uk/fsl/fslwiki/FSL>`_

Please refer to package specific documentation pages on how to install them on your system.
They may require administrative privileges to be installed.

Computing resources
-------------------

Processing a single subject will take about 45 minutes for a few fmri volumes (50-100), to more than 150 minutes for longer scans, depending on the size of raw data and CPU speed of your machine. At least 8GB of RAM are required to temporarily store all the intermediate steps of the process.
Since parallel computing and GPU acceleration are not supported by the vast majority of tools included in FSL, a simple way to speed up the processing and save time is to run several instances of *lnifmri_prep* on different subsets of your data. Please notice that the number of instances that can be run in parallel is limited by the amount of RAM available on your PC or laptop.