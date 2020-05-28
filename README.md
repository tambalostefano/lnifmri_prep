# lnifmri_prep

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

[dcm2niix](https://github.com/rordenlab/dcm2niix/releases)

[FSL](https://fsl.fmrib.ox.ac.uk/fsl/fslwiki/FSL)

## Usage example

```bash
user@host:dcmrawdata$ lnifmri_prep
```

## Release History

* 0.0.1
    * Work in progress

## Meta

Stefano Tambalo – {name}.{surname}@unitn.it

See ``LICENSE`` for more information.

<!-- Markdown link & img dfn's -->
[dcm2niix]: https://img.shields.io/npm/v/datadog-metrics.svg?style=flat-square
[fsl]: https://npmjs.org/package/datadog-metrics

