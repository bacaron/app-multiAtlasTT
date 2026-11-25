<h1 align="center">Multi-Atlas Transfer Tool</h1>

<p align="center">
  Maps a chosen cortical atlas (Schaefer, Gordon, Yeo, HCP-MMP, AAL and others) onto a subject's FreeSurfer surfaces with maTT2 GCS classifiers and outputs volumetric and surface parcellations.
</p>

<p align="center">
  <a href="https://github.com/brainlife/abcd-spec"><img src="https://img.shields.io/badge/ABCD_Spec-v1.1-green.svg" alt="ABCD Spec v1.1"></a>
  <a href="https://doi.org/10.25663/brainlife.app.470"><img src="https://img.shields.io/badge/Brainlife-brainlife.app.470-blue.svg" alt="Run on brainlife.io"></a>
  <a href="LICENSE"><img src="https://img.shields.io/badge/License-see_LICENSE-lightgrey.svg" alt="License"></a>
</p>

## At a glance

<!-- brainlife-app:begin (generated from the App manifest; edit the manifest, not this block) -->

> **Maps a chosen cortical atlas (Schaefer, Gordon, Yeo, HCP-MMP, AAL and others) onto a subject's FreeSurfer surfaces with maTT2 GCS classifiers and outputs volumetric and surface parcellations.**

Implements maTT2 from the multi-atlas transfer tools: atlas GCS files trained on Mindboggle-101 are applied with FreeSurfer to the subject's recon-all output, then the labels are remapped to consecutive integers and written as a volume in the subject T1w space, as GIfTI surface labels and as a brain mask. Use it to get an atlas parcellation (with 14 FreeSurfer subcortical regions) for connectivity or ROI analyses. Needs a completed FreeSurfer recon-all directory and a FreeSurfer license.

| | |
|---|---|
| **Inputs** | `neuro/freesurfer` |
| **Outputs** | `neuro/parcellation/volume` · `neuro/surface/vertices` · `neuro/surface/data` · `neuro/mask` |
| **Container** | `faskowit/app-multiatlastt:0.0.8` |
| **Resources** | 1 CPUs · 8 GB memory · 2 h walltime |
| **Requires** | `FREESURFER_LICENSE` |
| **Run it** | [doi.org/10.25663/brainlife.app.470](https://doi.org/10.25663/brainlife.app.470) |

#### Inputs

| Input | Datatype | Required | Description |
|---|---|---|---|
| `fsin` | `neuro/freesurfer` | yes | Completed FreeSurfer recon-all subject directory. |

#### Outputs

| Output | Datatype | Description |
|---|---|---|
| `parc-vol` | `neuro/parcellation/volume` | Volumetric parcellation (parc.nii.gz) in subject space with key.txt and label.json. |
| `parc-surf-verts` | `neuro/surface/vertices` | Left and right white, pial and inflated surfaces (GIfTI). |
| `parc-surf-data` | `neuro/surface/data` | Atlas labels on the left and right surfaces (GIfTI) with key and label files. |
| `mask` | `neuro/mask` | Brain mask derived from the FreeSurfer aparc+aseg. |

<details>
<summary><b>Parameters</b> (1)</summary>

| Parameter | Type | Default | Description |
|---|---|---|---|
| `atlas` | enum |  | Atlas to map onto the subject's cortex. Options: `gordon333dil`, `yeo17dil`, `hcp-mmp-b`, `schaefer100-yeo17`, `schaefer200-yeo17`, `schaefer400-yeo17 `, `schaefer500-yeo17`, `schaefer300-yeo17`, `shen268cort`, `baldassano`, `arslan`, `aal`, `nspn500`, `aicha`, `ica`. |

</details>

<!-- brainlife-app:end -->

## Running the App

### On brainlife.io

Open the App at [doi.org/10.25663/brainlife.app.470](https://doi.org/10.25663/brainlife.app.470), choose `neuro/freesurfer` from your project, set the parameters and press **Execute**. The results are saved to your project as `neuro/parcellation/volume`, `neuro/surface/vertices`, `neuro/surface/data`, `neuro/mask`.

### Locally

You need [Singularity/Apptainer](https://apptainer.org/) (the App runs in `faskowit/app-multiatlastt:0.0.8`), [`jq`](https://jqlang.github.io/jq/), `FREESURFER_LICENSE`.

1. Clone this repository.
2. Create `config.json` with the paths to your inputs and the parameters:

   ```json
   {
       "fsin": "/path/to/fsin/fsin",
       "atlas": ""
   }
   ```

3. Run `./main`.

## Citing

If you use this App, please cite it, the software it builds on and brainlife.io:

- Multi-Atlas Transfer Tool. brainlife.io App. [doi:10.25663/brainlife.app.470](https://doi.org/10.25663/brainlife.app.470)
- Fischl B, et al. Automatically parcellating the human cerebral cortex. Cereb Cortex 14:11-22 (2004).
- Fischl, B. et al. Automatically parcellating the human cerebral cortex. Cereb. Cortex 14, 11–22 (2004)
- The doi on the brainlife platform: http://doi.org/10.25663/bl.app.23
- An acknowledgement to this github page, or the other [maTT github repo](https://github.com/faskowit/multiAtlasTT) would be appreciated.
- Fischl. FreeSurfer. *NeuroImage* 62:774-781 (2012). [doi:10.1016/j.neuroimage.2012.01.021](https://doi.org/10.1016/j.neuroimage.2012.01.021)
- Hayashi S, Caron BA, Heinsfeld AS, et al. brainlife.io: a decentralized and open-source cloud platform to support neuroscience research. *Nature Methods* 21:809–813 (2024). [doi:10.1038/s41592-024-02237-2](https://doi.org/10.1038/s41592-024-02237-2)
- Avesani P, McPherson B, Hayashi S, et al. The open diffusion data derivatives, brain data upcycling via integrated publishing of derivatives and reproducible open cloud services. *Scientific Data* 6:69 (2019). [doi:10.1038/s41597-019-0073-y](https://doi.org/10.1038/s41597-019-0073-y)

## Authors

- Josh Faskowitz

**Contributors**

- Soichi Hayashi

## Funding

[![Wellcome-226486/Z/22/Z](https://img.shields.io/badge/Wellcome-226486%2FZ%2F22%2FZ-purple.svg)](https://wellcome.org/)
[![NIH-NINDS-U24NS140384](https://img.shields.io/badge/NIH_NINDS-U24NS140384-green.svg)](https://reporter.nih.gov/project-details/11261037)
[![NIH-NINDS-UM1NS132207](https://img.shields.io/badge/NIH_NINDS-UM1NS132207-green.svg)](https://reporter.nih.gov/project-details/11411328)
[![NIH-NIBIB-R01EB029272](https://img.shields.io/badge/NIH_NIBIB-R01EB029272-green.svg)](https://reporter.nih.gov/project-details/10262925)
[![NIH-NIBIB-R01EB030896](https://img.shields.io/badge/NIH_NIBIB-R01EB030896-green.svg)](https://reporter.nih.gov/project-details/10428625)
[![NIH-NIMH-R01MH126699](https://img.shields.io/badge/NIH_NIMH-R01MH126699-green.svg)](https://reporter.nih.gov/project-details/10460628)
[![NIH-NIDCD-R01DC020088](https://img.shields.io/badge/NIH_NIDCD-R01DC020088-green.svg)](https://reporter.nih.gov/project-details/11140284)
[![NSF-BCS-1734853](https://img.shields.io/badge/NSF_BCS-1734853-blue.svg)](https://www.nsf.gov/awardsearch/showAward?AWD_ID=1734853)
[![NSF-BCS-2203524](https://img.shields.io/badge/NSF_BCS-2203524-blue.svg)](https://www.nsf.gov/awardsearch/showAward?AWD_ID=2203524)
[![NSF-IIS-1636893](https://img.shields.io/badge/NSF_IIS-1636893-blue.svg)](https://www.nsf.gov/awardsearch/showAward?AWD_ID=1636893)
[![NSF-OAC-2148729](https://img.shields.io/badge/NSF_OAC-2148729-blue.svg)](https://www.nsf.gov/awardsearch/showAward?AWD_ID=2148729)
[![NSF-IIS-1912270](https://img.shields.io/badge/NSF_IIS-1912270-blue.svg)](https://www.nsf.gov/awardsearch/showAward?AWD_ID=1912270)
[![NSF-IIS-2148700](https://img.shields.io/badge/NSF_IIS-2148700-blue.svg)](https://www.nsf.gov/awardsearch/showAward?AWD_ID=2148700)
[![NSF-OAC-1916518](https://img.shields.io/badge/NSF_OAC-1916518-blue.svg)](https://www.nsf.gov/awardsearch/showAward?AWD_ID=1916518)

<sub>brainlife.io, which runs this App, is publicly funded by Wellcome, the U.S. National Institutes of Health and the U.S. National Science Foundation; acknowledging that support helps keep it running.</sub>

## License

See [LICENSE](LICENSE).
