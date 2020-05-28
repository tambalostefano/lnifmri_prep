LNiF MRI Preprocessing Workflow
================================

*lnifmri_prep* is a set of plain bash scripts to automate preprocessing of MRI data.

It requires minimal user interaction and provide easily interpretable output along with quality control reporting. It implements a generic set of preprocessing steps on structural and functional MRI data in NIFTI format, including: tissue class segmentation, bias field correction, brain extraction, motion correction, susceptibility distortion correction (SDC), within-subject coregistration and normalization to standard space template, nuisance regression, bandpass filtering, ICA decomposition and QC reporting. It also provide outputs that can be easily submitted to a variety of group level analyses (e.g. independent component analysis, voxel-based morphometry, surface-based analysis, etc.)

The package requires a working installation of `FSL <https://fsl.fmrib.ox.ac.uk/fsl/fslwiki/FSL>`_, so be sure to have it properly installed on your system. Although not strictly required, a working installation of `DCM2NIIX <https://github.com/rordenlab/dcm2niix/releases>`_ is highly recommended to handle DICOM to NIFTI conversion, as its output is perfectly integrated in *lnifmri_prep*.

Quick overview
--------------

*lnifmri_prep* workflow can be summarized as follow:

* DCM to NII conversion;
* Creation of output directory structure;
* Anatomical preprocessing (segmentation, bias field correction, brain extraction, normalization to standard space template);
* Realignment of functional timeseries and estimation of motion parameters;
* Unwarping of functional data based on fieldmap o reverse-phase encoding data (see Limitations_);
* Registration of unwarped functional data to subject structural image and standard space template;
* Nuisance regression (WM, CSF, motion parameters, temporal masking);
* Bandpass filtering;
* Single subject ICA (for quality control purposes);
* QC reporting (coregistration, normalization, motion, power spectrum);
* Generation of input lists for group level analysis.

Limitations
-----------

| **Filenames**
| *lnifmri_prep*'s interfaces for I/O of raw (e.g. DICOM folder) and processed data follow the naming convention in use at CIMeC LNiF MRI Lab of University of Trento. If your data come from a different source, then minor tweaking of keyword-based filters implemented in the source code is needed. To do so, please refer to the inline comments of individual shell scripts.

| **Multiple structural images**
| More than one anatomical scan can be acquired for a subject. In this case, the structural pipeline will correctly process and store all the datasets in the appropriate folder, but only a single T1w image will be used as a reference for subsequent processing of functional data.

| **Susceptibility Distortion Correction**
| If no susceptibility data are available (e.g. fieldmap or blip up/down reference scans), unwarping of functional data will be performed only by nonlinear registration to structural T1 and standard space template.

| **User Interaction**
| *lnifmri_prep* is designed to minimize user interaction. Please refer to `Workflow Setup <workflow.html>`__ for information on how to prepare the data environment.
