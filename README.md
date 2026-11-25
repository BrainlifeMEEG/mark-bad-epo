# Mark bad segments and channels

<!-- brainlife-app:begin (generated from the App manifest; edit the manifest, not this block) -->

> **Marks bad channels and annotates bad time segments by hand in MNE-Python epoched MEG/EEG data, saving the updated epochs.**

Appends the listed channel names to epo.info['bads'] and, if given, parses the multiline annotations text (onset, duration, description[, channels]) into mne.Annotations that replace existing annotations. Use it to record manual QC decisions before later processing. Channel names are not validated; as committed, the channel check for channel-specific annotations refers to an undefined variable, so such annotations will fail.

| | |
|---|---|
| 📥 **Inputs** | `neuro/meeg/mne/epochs` |
| 📤 **Outputs** | `neuro/meeg/mne/epochs` |
| 🐳 **Container** | `brainlife/mne:1.2.1` |
| ⚙️ **Resources** | 1 CPUs |
| 🔗 **Run it** | [doi.org/10.25663/brainlife.app.815](https://doi.org/10.25663/brainlife.app.815) |

#### 📥 Inputs

| Input | Datatype | Required | Description |
|---|---|---|---|
| `epo` | `neuro/meeg/mne/epochs` | yes | Epoched MEG/EEG data (MNE epochs FIF). |

#### 📤 Outputs

| Output | Datatype | Description |
|---|---|---|
| `out_dir` | `neuro/meeg/mne/epochs` | The input epochs with updated bad channels and annotations (meg-epo.fif). |

<details>
<summary><b>⚙️ Parameters</b> (2)</summary>

| Parameter | Type | Default | Description |
|---|---|---|---|
| `bads` | string |  | Comma-separated channels to reject (e.g. "MEG2422,MEG2321"). |
| `annotations` | string |  | A multiline text describing segments to discard, following a format compatible with mne.Annotations: "start, duration, description[, channels]" |

</details>

📚 **References used by this App:**
- Hayashi S, Caron BA, Heinsfeld AS et al. brainlife.io: a decentralized and open-source cloud platform to support neuroscience research. Nat Methods 21:809-813 (2024). [doi:10.1038/s41592-024-02237-2](https://doi.org/10.1038/s41592-024-02237-2)
- Gramfort A et al. MEG and EEG data analysis with MNE-Python. Frontiers in Neuroscience 7:267 (2013). [doi:10.3389/fnins.2013.00267](https://doi.org/10.3389/fnins.2013.00267)

<!-- brainlife-app:end -->

Brainlife App to reject bad data segments and/or channels MNE-Python [epo.info['bads']](https://mne.tools/stable/auto_tutorials/preprocessing/15_handling_bad_channels.html), and [mne.Annotations](https://mne.tools/stable/generated/mne.Annotations.html#mne-annotations).

# Documentation

#### Input files are:
* a MEG/EEG epochs file in fif format (mne/Epochs).

#### Input parameters are:
* ` Bads `:  str ,  The comma-separated channels to reject (e.g. "MEG2422,MEG2321").
* ` annotations `:  str , A multiline text describing segments to discard, following a format compatible with mne.Annotations:
    "start, duration, description[, channels]"

    For instance:
      
      2, 1, bad_segment
      5, 1, more_selective, MEG2422, MEG2321
      
    will create two annotations, one named "bad_segment" starting at 2s, with duration 1s, and second one named "more_selective" focused on channels MEG2422 and MEG2321, starting at 5s, with duration 1s.

#### Ouput files are:
  * the updated MEG/EEG file in fif format (mne/Epochs), where `epo.info['bads']` has been updated, and with added `epo.annotations`.

## Authors
- [Maximilien Chaumon](maximilien.chaumon@icm-institute.org)

## Contributors
- [Kamilya Salibayeva](ksalibay@iu.edu)


### Funding Acknowledgement
brainlife.io is publicly funded and for the sustainability of the project it is helpful to Acknowledge the use of the platform. We kindly ask that you acknowledge the funding below in your code and publications. Copy and past the following lines into your repository when using this code.

[![NSF-BCS-1734853](https://img.shields.io/badge/NSF_BCS-1734853-blue.svg)](https://nsf.gov/awardsearch/showAward?AWD_ID=1734853)
[![NSF-BCS-1636893](https://img.shields.io/badge/NSF_BCS-1636893-blue.svg)](https://nsf.gov/awardsearch/showAward?AWD_ID=1636893)
[![NSF-ACI-1916518](https://img.shields.io/badge/NSF_ACI-1916518-blue.svg)](https://nsf.gov/awardsearch/showAward?AWD_ID=1916518)
[![NSF-IIS-1912270](https://img.shields.io/badge/NSF_IIS-1912270-blue.svg)](https://nsf.gov/awardsearch/showAward?AWD_ID=1912270)
[![NIH-NIBIB-R01EB029272](https://img.shields.io/badge/NIH_NIBIB-R01EB029272-green.svg)](https://grantome.com/grant/NIH/R01-EB029272-01)

### Citations
1. Avesani, P., McPherson, B., Hayashi, S. et al. The open diffusion data derivatives, brain data upcycling via integrated publishing of derivatives and reproducible open cloud services. Sci Data 6, 69 (2019). [https://doi.org/10.1038/s41597-019-0073-y](https://doi.org/10.1038/s41597-019-0073-y)

