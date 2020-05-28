Output
======

The output of *lnifmri_prep* is organized in subfolders of **outputfolder**:

* **logs**: log files for main stages of the pipeline.
* **qc**: contains quality control reports and input files for group-level analysis;
* **sub-XX**: contains subject-related output files;

The box below illustrates the hierarchy of files produced by *lnifmri_prep*

.. admonition:: *lnifmri_prep* Output Structure

	|	\|__ **dcmcontainer**/
	|		\|__ any_dcm_folder_name/
	|    				\:
	|	\:
	|	\|
	|	\|__ **outputfolder**/
	|		\|__ **logs**
	|			\|__ lnifmri_prep00_organize.txt
	|		 			\:
	|			\|__ lnifmri_prep05_qc.txt
	|		\:
	|		\|__ **qc**/
	|			\|__ lnifmri_prep_qcfiles/
	|			\|__ lnifmri_preproc_func2std_QC/
	|			\|__ lnifmri_preproc_func2struc_QC/
	|			\|__ filelist_[*fmp,tup,unc*]_[*other software*].txt
	|			\|__ lnifmri_preproc_motion_QC.png
	|			\|__ lnifmri_preproc_pspec_QC.png
	|		\:
	|		\|__ **sub-01**/
	|			\|__ *anat*/
	|			\|__ *dwi*/
	|			\|__ *func*/
	|				\|__ lnifmri_prep_files
	|				\|__ [sdc_fmp/]
	|					\|__ lnifmri_prep_files
	|					\|__ [sub-01_bold_rest-smooth.ica]
	|					\|__ sub-01_bold_[rest,task]-[space]-[smooth].nii.gz	
	|			 				\:	
	|				\|__ [sdc_tup/]
	|			 		\|__ lnifmri_prep_files
	|					\|__ [sub-01_bold_rest-smooth.ica]	
	|					\|__ sub-01_bold_[rest,task]-[space]-[smooth].nii.gz		
	|			 				\:	
	|				\|__ sdc_unc/
	|					\|__ lnifmri_prep_files
	|					\|__ [sub-01_bold_rest-smooth.ica]	
	|					\|__ sub-01_[rest,task]-[space]-[smooth].nii.gz	
	|							\:	
	|				\|__ sub-01_filelist.txt
	|			\:
	|			\|__ *misc*/
	|			\|__ *sdc*/
	|			\|__ *sub-01_ses-YY_T[1,2]w.anat*/
	|		\:
	|		\|__ **sub-XX**/
	|		\:
	|		\|__ **sub-ZZ**/
	|

Subject-specific output
-----------------------

Structural data
^^^^^^^^^^^^^^^

* **sub-XX/anat**: Full resolution anatomical data are stored here. You will find **untouched** nifti files and json sidecars for higher level analysis (e.g. Freesurfer's *recon-all* or voxel-based morphometry).

* **sub-XX/sub-XX_ses-YY.anat**: This folder stores resampled, bias-field corrected and brain-extracted version of structural images, tissue class segmentation, binary masks for GM, WM and CSF, linear and nonlinear matrices for forward and backward registration to standard space (MNI152) brain template. 

* **sub-XX/dwi**: Contains diffusion weighted images (no preprocessing of DWI data is available at this stage)

Functional data
^^^^^^^^^^^^^^^

* **sub-XX/func**: Stores functional timeseries for both resting state and task based protocols.

	* **sub-XX/func/lnifmri_prep_files**: Contains intermediate processing steps and utility files used at various stages of the workflow.

	* **sub-XX/func/sdc_XXX**: This set of folders contain the main output, one folder per SDC method:
	
		 * *fmp*: fieldmap;
		 * *tup*: reversed phase encoding;
		 * *unc*: no SDC, only nonlinear registration.

	will be present, each of them containing a preprocessed functional timeseries along with its normalized and smoothed version. It contains also a power-spectrum plot and the text file used to generate the plot. An ICA output folder, if not skipped at setup, is stored here as well.
	
		* **sub-XX/func/sdc_XXX/lnifmri_prep_files**: As for the top-level folder, intermediate processing steps and utility files used at various stages of the SDC-specific workflow are stored here.

SDC data
^^^^^^^^

* **sub-XX/sdc**: Fieldmaps and/or reversed phase encoding (AP/PA, blip up/down) data are stored and processed in this folder.


Global output
-------------

* **qc**: Contains utility files and images for visual quality control of datasets.

* **logs**: This folder contains logfiles filled by *lnifmri_prep*. Runtime errors are displayed in realtime in the terminal window. 

* **filelist_*.txt**: list of dataset to be used as input for group-ICA (One for SDC method) or VBM group analysis.

* **lnifmri_prep_report.html**: HTML report of preprocessed data.

