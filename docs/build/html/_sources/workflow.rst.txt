Workflow Setup
==============

The next sections illustrate how to accomplish a complete preprocessing stage.

Setup the environment
---------------------

Prepare a root container for your raw data DICOM folders::

	user@host:home$ mkdir path/to/dcmcontainer

Copy/Move your raw data to *path/to/dcmcontainer*::

	user@host:home$ cp -r path/to/my/dcmfolders/ path/to/dcmcontainer/

.. warning::
	| The automated pipeline works on a keyword-based parsing of filenames.
	|
	| If your functional dataset contains resting-state and task-based timeseries, and these two dataset share a common basename, *lnifmri_prep* will process them **as if they are both resting-state acquisition**. This default behaviour can be tweaked by manually renaming the raw DICOM folder to include the "task" keyword in the folder name. This will disable the bandpass filtering of task-based timeseries.
	|
	| dcmcontainer
	|		\|__ anat1_dcm_folder_name
	|		\|__ func1_dcm_folder_name
	|		\|__ **func2_dcm_folder_name** 		*--> this is the task-based scan*
	|
	| Renamed to:
	|
	| dcmcontainer
	|		\|__ anat1_dcm_folder_name
	|		\|__ func1_dcm_folder_name
	|		\|__ **func2_dcm_task_folder_name** *--> this is the task-based scan*
	|
	| Before launching the workflow, please fix all relevant folders.


Launch *lnifmri_prep*
---------------------

To start the workflow, *cd* to *dcmcontainer* and run *lnifmri_prep*::

	user@host:home$ cd path/to/dcmcontainer
	user@host:dcmcontainer$ lnifmri_prep

A splash screen will appear; you must provide the location to store preprocessed data::

	Enter directory output name [YYYYMMDD_HHMMSS]:

Enter a custom name or accept the default option in square brackets by hitting [ENTER]::

	Enter directory output name [YYYYMMDD_HHMMSS]: outputfolder	

.. note::
	If a directory *outputfolder* already exists in the selected path, a timestamp (YYYYMMDD_HHMMSS) will be prepended to avoid overwriting of existing data.

At this point, you have the option to skip single-subject ICA::

	Run SS-ICA? (y/n) [y]:

by overriding the default answer in square brackets. Make your choice and hit [ENTER].

.. warning::
	Running single-subject ICA can dramatically increase processing time. However, since detailed ICA reports are really useful for visual sanity check of the timeseries, this is the default option.

After a few preliminary steps, a screening of global MR acquisition parameters of functional scans is run to spot potential inconsistencies. Here you have the possibility to exclude zero or more subjects from further processing. A sample summary report will appear at terminal prompt as follows::

	Key to param headers:
	RT    | RepetitionTime
	ET    | EchoTime
	...
	RCAE  | ReceiveCoilActiveElements
	MAF   | MultibandAccelerationFactor

	Code  |	Sub-ID 	| RT | 	ET    | ... | RCAE         | MAF |

	[01]  |	sub-01	| 1  |	0.028 | ... | "HC1-7"      |  8  |

	[02]  |	sub-02	| 1  |  0.028 | ... | "HC1-7;NC1"  |  8  |
	[03]  |	sub-03	| 1  |	0.028 | ... | "HC1-7;NC1"  |  8  |
	[04]  |	sub-04	| 1  |	0.028 | ... | "HC1-7;NC1"  |  8  |
	[06]  |	sub-06	| 1  |	0.028 | ... | "HC1-7;NC1"  |  8  |

	[05]  |	sub-05	| 1 |	0.028 | ... | "HC1-7;NC12" |  8  |

Subjects are sorted and grouped to highlight sub-groups defined by common acquisition parameters. At the prompt you can specify which subjects to exclude or proceed with the entire experimental dataset::

	To exclude one or more subjects from the workflow,
	please enter their code	separated by [space] and hit [ENTER], e.g.:

	Skip subject(s): 01 05

	Or leave the field blank and click [ENTER] to process the entire list.

The program will then show a list of subjects that will be excluded from the analysis and ask for confirmation. The list will show "NONE" if either you will choose to keep all the subjects of if the input list is not valid (e.g.: wrong or non-existent code, missing space between codes, etc...)::

	Skip subject(s): 13 *(or 00, 3, 03-02, 0104, etc...)*

	The following subjects will be EXCLUDED from the analysis:

	NONE

	Continue? (y/n):

In case of partially mispelled codes, the list will show only the valid entries::

	Skip subject(s): 01 5

	The following subjects will be EXCLUDED from the analysis:

	sub-01

	Continue? (y/n):

Here you can accept and continue or repeat the selection. Once you are happy with your choice, confirm with "y" to finalize this step.

| Setup is now complete. Wait a few seconds for the program to start. Progress time will be reported in the terminal window upon successful completion of every step. No further actions are required until the end of the workflow.
|
| The process will run as follows:

	1. DCM to NIFTI conversion (raw DICOM folders will be renamed with a ".sub" suffix);
	2. Creation of output directory tree;
	3. Processing of structural images;
	4. Processing of functional data;
	5. QC reporting.

.. note::
	During DCM to NII conversion, a copy of NIFTI files will be stored in the corresponding DICOM folder. All converted NIFTI are associated to a .json file containing the most relevant metadata extracted from DICOM header.


Check progress
--------------

You can check the status of the pipeline by inspecting files in the *outputfolder/logs*. In a new terminal window, type::

	user@host:~$ cd path/to/dcmcontainer/outputfolder/logs
	user@host:logs$ nano XX_logfile

or::

	user@host:~$ tail -f path/to/dcmcontainer/outputfolder/logs/XX_logfile.txt

to enable real-time monitoring of selected log file.

After completion, processed files will be stored in the appropriate subfolders of *outputfolder*.