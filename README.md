# lnifmri_prep

This pipeline is developed for use at the [Center for Mind/Brain Sciences - CIMeC](https://www.cimec.unitn.it/en/176/magnetic-resonance-laboratory-mri-lab) of the University of Trento (IT).

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


## Requirements

DCM to NIFTI converter: [dcm2niix](https://github.com/rordenlab/dcm2niix/releases)

FSL Software suite: [FSL](https://fsl.fmrib.ox.ac.uk/fsl/fslwiki/FSL)

## Usage example

```bash
user@host:dcmrawdata$ lnifmri_prep
```

## Meta

Copyright (C) 2019-2020 Stefano Tambalo, stefano.tambalo@unitn.it>

See ``LICENSE`` for more information.

