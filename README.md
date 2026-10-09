# Mark Bad Channels and Segments in Epoched MEG/EEG Data

[![Run on Brainlife.io](https://img.shields.io/badge/Brainlife-bl.app.815-blue.svg)](https://doi.org/10.25663/brainlife.app.815)

## Description

This app marks bad channels and annotates bad time segments "by hand" in MNE `Epochs` data, using [`epo.info['bads']`](https://mne.tools/stable/auto_tutorials/preprocessing/15_handling_bad_channels.html) and [`mne.Annotations`](https://mne.tools/stable/generated/mne.Annotations.html#mne-annotations). Channels marked as bad are excluded from downstream analysis, and annotations describe segments of data to be discarded.

The app generates:
- The epochs data with updated `epo.info['bads']` and (optionally) new annotations, saved to `out_dir/meg-epo.fif`

## Inputs

- **`mne`** (`neuro/meeg/mne/epochs`): epoched MEG/EEG data (`meg-epo.fif`) to mark bad channels and segments in (required)

## Outputs

- **`out_dir/meg-epo.fif`** (`neuro/meeg/mne/epochs`, tag `bads_marked`): the input epochs, with `epo.info['bads']` updated and annotations added

## Configuration Parameters

| key | type | default | description |
|---|---|---|---|
| `bads` | string | `""` | Comma-separated channel names to append to `epo.info['bads']` (e.g., `"MEG2422,MEG2321"`). Leading/trailing spaces and empty entries are stripped. |
| `annotations` | string (multiline) | `""` | Multiline text describing segments to discard, one per line: `start, duration, description[, channel1, channel2, ...]`. Parsed into an `mne.Annotations` object and applied via `epo.set_annotations()`, which replaces any annotations already present on the input. |

Example `annotations` value:
```
2, 2, bad_segment
5, 2, more_selective, MEG2422, MEG2321
```
This creates two annotations: `bad_segment` starting at 2s with duration 2s (applies to all channels), and `more_selective` starting at 5s with duration 2s, restricted to channels `MEG2422` and `MEG2321`.

## Usage

### Running on Brainlife.io

1. Select your epoched MEG/EEG dataset (`mne.Epochs`) as the `mne` input.
2. Optionally set `bads` and/or `annotations` in the configuration form.
3. Submit the process.

### Local Testing

```bash
# Edit config.json to point "mne" at a real epo.fif file, then:
singularity exec docker://brainlife/mne:1.2.1 python3 main.py
```

## Technical Details

- **Bad channels**: names listed in `bads` are appended to `epo.info['bads']`; they are not validated against the channel names present in the data.
- **Annotations**: each line of `annotations` is split on `,`, `;`, or `-` into `onset, duration, description[, channels...]`, then assembled into a single `mne.Annotations` object that replaces any annotations already present on the input epochs.

## Authors

- [Maximilien Chaumon](https://github.com/dnacombo), Paris Brain Institute
- [Kami Salibayeva](https://github.com/KSalibay)

## Citations

Hayashi, S., Caron, B.A., Heinsfeld, A.S. et al. brainlife.io: a decentralized and open-source cloud platform to support neuroscience research. Nat Methods 21, 809–813 (2024). https://doi.org/10.1038/s41592-024-02237-2

Gramfort, A. et al. MEG and EEG data analysis with MNE-Python. Front. Neurosci. 7, 267 (2013). https://doi.org/10.3389/fnins.2013.00267

## Funding Acknowledgement

brainlife.io is publicly funded and for the sustainability of the project it is helpful to Acknowledge the use of the platform. We kindly ask that you acknowledge the funding below in your code and publications. Copy and paste the following lines into your repository when using this code.

[![NSF-BCS-1734853](https://img.shields.io/badge/NSF_BCS-1734853-blue.svg)](https://nsf.gov/awardsearch/showAward?AWD_ID=1734853)
[![NSF-BCS-1636893](https://img.shields.io/badge/NSF_BCS-1636893-blue.svg)](https://nsf.gov/awardsearch/showAward?AWD_ID=1636893)
[![NSF-ACI-1916518](https://img.shields.io/badge/NSF_ACI-1916518-blue.svg)](https://nsf.gov/awardsearch/showAward?AWD_ID=1916518)
[![NSF-IIS-1912270](https://img.shields.io/badge/NSF_IIS-1912270-blue.svg)](https://nsf.gov/awardsearch/showAward?AWD_ID=1912270)
[![NIH-NIBIB-R01EB029272](https://img.shields.io/badge/NIH_NIBIB-R01EB029272-green.svg)](https://grantome.com/grant/NIH/R01-EB029272-01)
[![NIH-NIBIB-R01EB030896](https://img.shields.io/badge/NIH_NIBIB-R01EB030896-green.svg)](https://grantome.com/grant/NIH/R01-EB030896-01)

## License

Copyright (c) 2020 brainlife. Licensed under the MIT License, see [LICENSE](LICENSE).
