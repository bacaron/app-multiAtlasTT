# app-multiAtlasTT

<!-- brainlife-app:begin (generated from the App manifest; edit the manifest, not this block) -->

> **Maps a chosen cortical atlas (Schaefer, Gordon, Yeo, HCP-MMP, AAL and others) onto a subject's FreeSurfer surfaces with maTT2 GCS classifiers and outputs volumetric and surface parcellations.**

Implements maTT2 from the multi-atlas transfer tools: atlas GCS files trained on Mindboggle-101 are applied with FreeSurfer to the subject's recon-all output, then the labels are remapped to consecutive integers and written as a volume in the subject T1w space, as GIfTI surface labels and as a brain mask. Use it to get an atlas parcellation (with 14 FreeSurfer subcortical regions) for connectivity or ROI analyses. Needs a completed FreeSurfer recon-all directory and a FreeSurfer license.

| | |
|---|---|
| 📥 **Inputs** | `neuro/freesurfer` |
| 📤 **Outputs** | `neuro/parcellation/volume` · `neuro/surface/vertices` · `neuro/surface/data` · `neuro/mask` |
| 🐳 **Container** | `faskowit/app-multiatlastt:0.0.8` |
| ⚙️ **Resources** | 1 CPUs · 8 GB memory · 2 h walltime |
| 🔑 **Requires** | `FREESURFER_LICENSE` |
| 🔗 **Run it** | [doi.org/10.25663/brainlife.app.470](https://doi.org/10.25663/brainlife.app.470) |

#### 📥 Inputs

| Input | Datatype | Required | Description |
|---|---|---|---|
| `fsin` | `neuro/freesurfer` | yes | Completed FreeSurfer recon-all subject directory. |

#### 📤 Outputs

| Output | Datatype | Description |
|---|---|---|
| `parc-vol` | `neuro/parcellation/volume` | Volumetric parcellation (parc.nii.gz) in subject space with key.txt and label.json. |
| `parc-surf-verts` | `neuro/surface/vertices` | Left and right white, pial and inflated surfaces (GIfTI). |
| `parc-surf-data` | `neuro/surface/data` | Atlas labels on the left and right surfaces (GIfTI) with key and label files. |
| `mask` | `neuro/mask` | Brain mask derived from the FreeSurfer aparc+aseg. |

<details>
<summary><b>⚙️ Parameters</b> (1)</summary>

| Parameter | Type | Default | Description |
|---|---|---|---|
| `atlas` | enum |  | Atlas to map onto the subject's cortex. Options: `gordon333dil`, `yeo17dil`, `hcp-mmp-b`, `schaefer100-yeo17`, `schaefer200-yeo17`, `schaefer400-yeo17 `, `schaefer500-yeo17`, `schaefer300-yeo17`, `shen268cort`, `baldassano`, `arslan`, `aal`, `nspn500`, `aicha`, `ica`. |

</details>

📚 **References used by this App:**
- Fischl B, et al. Automatically parcellating the human cerebral cortex. Cereb Cortex 14:11-22 (2004).

<!-- brainlife-app:end -->

0.0.9 branch 

[brainlife.io](https://brainlife.io/) version of multi atlas transfer tools (maTT). This app takes in a completed `recon-all` FreeSurfer directory, and outputs a volumetric parcellation in the indiviual's T1w space. These tools warp the parcellations to the subject space using the warp information provided by FreeSurfer. This is an implemenation of maTT2, which uses the gcs files trained on the [mindboggle-101](https://mindboggle.info/data) data. The GCS files are automatically pulled from the [maTT fishare directory](https://figshare.com/articles/multiAtlasTT_data/5998583/1) if not present locally. 

Check out the [maTT github repo](https://github.com/faskowit/multiAtlasTT) for more info and the latest version of maTT.  

### Authors
- [Josh Faskowitz](jfaskowi@iu.edu)

### Contributors
- [Soichi Hayashi](hayashis@iu.edu)

### Funding Acknowledgement
brainlife.io is publicly funded and for the sustainability of the project it is helpful to Acknowledge the use of the platform. We kindly ask that you acknowledge the funding below in your publications and code reusing this code.

[![NSF-GRFP-1342962](https://img.shields.io/badge/NSF_GRFP-1342962-blue.svg)](https://www.nsf.gov/awardsearch/showAward?AWD_ID=1342962)
[![NSF-BCS-1734853](https://img.shields.io/badge/NSF_BCS-1734853-blue.svg)](https://nsf.gov/awardsearch/showAward?AWD_ID=1734853)
[![NSF-BCS-1636893](https://img.shields.io/badge/NSF_BCS-1636893-blue.svg)](https://nsf.gov/awardsearch/showAward?AWD_ID=1636893)
[![NSF-ACI-1916518](https://img.shields.io/badge/NSF_ACI-1916518-blue.svg)](https://nsf.gov/awardsearch/showAward?AWD_ID=1916518)
[![NSF-IIS-1912270](https://img.shields.io/badge/NSF_IIS-1912270-blue.svg)](https://nsf.gov/awardsearch/showAward?AWD_ID=1912270)
[![NIH-NIBIB-R01EB029272](https://img.shields.io/badge/NIH_NIBIB-R01EB029272-green.svg)](https://grantome.com/grant/NIH/R01-EB029272-01)

### Citations
We we think you should cite the following when code using this code. 

1. Fischl, B. et al. Automatically parcellating the human cerebral cortex. Cereb. Cortex 14, 11–22 (2004)
2. The doi on the brainlife platform: http://doi.org/10.25663/bl.app.23
3. An acknowledgement to this github page, or the other [maTT github repo](https://github.com/faskowit/multiAtlasTT) would be appreciated.

## Running the App 

### On Brainlife.io

You can submit this App online at [http://doi.org/10.25663/bl.app.23](http://doi.org/10.25663/bl.app.23) via the "Execute" tab.

### Running Locally (on your machine)

1. git clone this repo.
2. Inside the cloned directory, create `config.json` with something like the following content with paths to your input files.

```json
{
        "fsin": "./path/to/freesurferdir/",
        "atlas": "atlasname"
}
```

*Note: the atlasname should be the name of one of the available atlases provided in the figsshare repo.*

3. Launch the App by executing `main`

```bash
./main
```

## Output

All output files will be generated under the current working directory (pwd), in directories called `parc-vol`, `parc-surf`, and `mask`. 

Inside `parc-vol` there will be:
```
parc.nii.gz
key.txt
label.json
```

Inside `parc-surf` there will be:
```
?h.parc.inflated.gii
?h.parc.pial.gii
?h.parc.white.gii
?h.parc.annot.gii
key.txt
label.json
```

Also, there is a volumetric mask in the `mask` directory. 

### Dependencies

This App uses [singularity](https://www.sylabs.io/singularity/) to run. If you don't have singularity, you can run this script in a unix enviroment with:  

  - FreeSurfer: https://surfer.nmr.mgh.harvard.edu/
  - jq: https://stedolan.github.io/jq/
  - python3 with nibabel: https://nipy.org/nibabel/

#### MIT Copyright (c) Josh Faskowitz

<sub> This material is based upon work supported by the National Science Foundation Graduate Research Fellowship under Grant No. 1342962. Any opinion, findings, and conclusions or recommendations expressed in this material are those of the authors(s) and do not necessarily reflect the views of the National Science Foundation. </sub>

