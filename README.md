[![DOI](https://img.shields.io/badge/DOI-10.82901%2Fnemar.nm000360-blue)](https://doi.org/10.82901/nemar.nm000360)

# Interictal epileptiform discharge annotations in sleep iEEG Data

## Dataset Overview
This dataset comprises multichannel intracranial EEG (iEEG) recordings from 25 epilepsy patients during overnight sleep, collected at two medical centers. 
The recordings include 852 annotated interictal epileptiform discharges, primarily from the medial temporal lobe, identified by expert neurologists. 
The data is formatted according to the BIDS (Brain Imaging Data Structure) standard for iEEG recordings.

## Dataset Structure
- participants.tsv: Contains demographic and clinical information for each participant, including:
  - participant_id: Unique identifier for each participant.
  - age: Age at the time of the study (in years).
  - sex: Biological sex (M/F).
  - SOZ: Seizure onset zone.
  - TimeFromSleepOnset: Time from sleep onset (in minutes).
  - SleepScoring: Sleep stages scored according to AASM criteria.
  
- sub-\<subject_id\>/: Contains the iEEG recordings and metadata for each participant.
  - sub-\<subject_id\>_task-sleep_ieeg.edf: The raw iEEG data in EDF format.
  - sub-\<subject_id\>_task-sleep_events.tsv: Event annotations, such as expert-determined IED (interictal epileptiform discharges) timings.
  - sub-\<subject_id\>_electrodes.tsv: Electrode names and MNI coordinates (for select subjects).
  - sub-\<subject_id\>_coordsystem.json: Describes the coordinate system used for electrode localization.

- derivatives/: Contains processed files, such as:
  - sub-\<subject_id\>_task-sleep_events_interpretation.tsv: Interpretation of events for each participant.
  - channels.tsv: Information on channel names


## License and Data Use
The dataset is shared under the CC-BY-NC license. Users are free to use the data for non-commercial purposes with appropriate attribution.

## Citation
If you use this dataset in your research, please cite the following publication:
Falach R, Geva-Sagiv M, Eliashiv D, Goldstein L, Budin O, Gurevitch G, Morris G, Strauss I, Globerson A, Fahoum F, Fried I, Nir Y. Annotated interictal discharges in intracranial EEG sleep data and related machine learning detection scheme. Sci Data. 2024 Dec 18;11(1):1354. doi: 10.1038/s41597-024-04187-y.

---------------------------------------------------------------------------
## Redistribution on NEMAR (added 2026-10-06; everything above this line is the authors' README.txt, unchanged)

### Source
- Figshare: Falach R, Geva-Sagiv M, Eliashiv D, Goldstein L, Budin O, Gurevitch G, Morris G, Strauss I,
  Globerson A, Fahoum F, Fried I, Nir Y (2024). *Annotated interictal epileptiform discharges in intracranial EEG
  (iEEG) sleep data.* figshare. Dataset. https://doi.org/10.6084/m9.figshare.26131978.v3
  (article 26131978, version 3, published 2024-12-30; single file `ieeg_ieds_bids_final.zip`, 272,009,926 bytes,
  MD5 cdf392d5f92ba106b1f6794844147109).
- Data descriptor: Falach R. et al. Annotated interictal discharges in intracranial EEG sleep data and related
  machine learning detection scheme. *Scientific Data* 11, 1354 (2024). https://doi.org/10.1038/s41597-024-04187-y
- Code: https://github.com/NirLab-TAU/iEEG_ied_detection
- The original archive is included unchanged as `sourcedata/ieeg_ieds_bids_final.zip`.

This NEMAR copy is the authors' own BIDS dataset with the minimal changes needed to pass the current BIDS
validator. Every change is listed in `CHANGES` (version 1.0.1). No recording was modified: the 25 EDF files are
byte-identical to the archive (SHA-256 checked). No filtering, resampling, re-referencing or channel removal was
done for this redistribution.

### Licence
Two licence statements exist for this dataset, and they disagree:
1. Figshare record 26131978 v3, licence field: **"CC BY 4.0"** (https://creativecommons.org/licenses/by/4.0/).
2. Inside the archive, `dataset_description.json`: `"License": "CC-BY-NC"`; and the authors' README.txt (above):
   "The dataset is shared under the CC-BY-NC license. Users are free to use the data for non-commercial purposes
   with appropriate attribution."

The archive statement gives no version number. The depositor (Bruno Aristimunha, 2026-10-06) decided to apply
the most restrictive of the stated licences. This redistribution is therefore released under
**CC BY-NC 4.0 (`CC-BY-NC-4.0`)**. The version "4.0" is the depositor's choice: the source states no version,
and 4.0 is the Creative Commons version of the Figshare record. Commercial use is not permitted under this copy.
If the authors clarify the licence, this copy will be updated.

### Ethics (from Falach et al., 2024)
"All patients provided written informed consent to participate in the research study, under the approval of the
Institutional Review Board at the Tel Aviv Sourasky Medical Center (TASMC, 9 patients), or the Medical
Institutional Review Board at the University of California, Los Angeles (UCLA, 16 patients). In their consent,
patients explicitly agreed for anonymized data to be shared and used in future scientific publications. UCLA
Hospital IRB protocol: 10-000973, TLVMC IRB protocol: TLV-008-12."

### Recording facts worth knowing (from the paper and the files)
- 25 patients (sub-01 to sub-09: Tel Aviv Sourasky Medical Center, 50 Hz mains; sub-10 to sub-25: UCLA, 60 Hz
  mains, per `InstitutionName` and `PowerLineFrequency` in each `_ieeg.json`).
- Each EDF is a short sleep excerpt, 61 to 291 s long (total 4,603 s = 76.7 min, matching the paper's
  "76 minutes"), not a whole night.
- The paper reports acquisition with a Blackrock system "referenced to a central scalp electrode and sampled at
  2KHz". The shared EDF files are at 1000 Hz, so the authors resampled the data before sharing. The EDF
  headers carry no filter information (`SoftwareFilters` is "n/a" in the source sidecars).
- Some participants' files also contain bipolar derivations (channel names such as `RA1-RA3`) next to the
  referential channels. The authors added these to help annotation (see the paper). They are kept as provided.
- `events.tsv`: one row per expert-annotated interictal epileptiform discharge (`duration` 0, `trial_type` =
  the neurologist's free-text label, `sample` = onset sample). The 25 files hold 853 rows in total; the paper
  reports 852 IEDs. The rows are kept as provided. `derivatives/` holds the authors' per-event channel
  lists (`*_events_interpretation.tsv`) and the channel-abbreviation table (`channels.tsv`).
- Electrode coordinates (MNI152Lin, mm) are provided by the authors for 18 participants. For the other 7
  (sub-08, sub-10 to sub-15), the archive has no coordinates. `electrodes.tsv` for these lists the referential
  contact names with x/y/z = n/a, and `coordsystem.json` says "Other" with units "n/a". No coordinates were
  invented. The paper's figure used group-average positions for these patients; those values are not in the
  archive.

### RecordingDuration reconciliation
The source sidecars gave `RecordingDuration` values of 60.999 to 290.999 s. The EDF headers give
n_records x record_duration = 61 to 291 s, at 1000 Hz with 1-s records: exactly 0.001 s (one sample) longer
for every file. The source values follow the (n_samples - 1)/fs convention. BIDS defines the field as the length
of the recording, so the sidecars now carry the header value (n_samples/fs). The per-file old and new values are
in `CHANGES`.

### Privacy
The EDF headers were already de-identified by the authors with MNE-BIDS ("X X X" patient field,
"Startdate 01-JAN-1985 X mne-bids_anonymize X"). The times of day were kept and the dates were replaced. The
TSV and JSON files contain participant codes, age in years, sex, seizure-onset zone, minutes from sleep onset and
sleep-stage vectors. They contain no names, dates of birth, record numbers or imaging. A byte-level review was run
before this deposit.

---------------------------------------------------------------------------
## Additional description (lane L metadata enrichment, 2026-10-06; sources: Falach et al. 2024, Sci Data 11:1354, doi:10.1038/s41597-024-04187-y, sections named below)

### Cohort and acquisition (Methods: Participants, EEG Recordings)
- 25 patients with drug-resistant epilepsy, implanted with depth iEEG electrodes for clinical evaluation of seizure
  foci; electrode locations were based solely on clinical criteria. 9 patients from Tel Aviv Sourasky Medical
  Center (TASMC, recruited 2017-2023) and 16 from UCLA (2007-2012, 2017-2021), who volunteered for an overnight
  sleep research recording session.
- Implant type: depth electrodes (SEEG-type), platinum contacts along the shaft. All 980 channels in the shared
  files are depth-electrode channels (typed SEEG), including the authors' bipolar derivations.
- Amplifier: Blackrock system; sampled at 2 kHz, referenced to a central scalp electrode. The shared EDFs are
  1000 Hz (see "Recording facts" above).
- Channel naming: hemisphere letter (R/L) + 1-3 region letters (e.g. A amygdala, EC entorhinal cortex, AH
  anterior hippocampus; full list in derivatives/channels.tsv) + contact number from 1 (most mesial) increasing
  laterally. Channel selection was based on availability, without regard to IED presence.
- In 15 patients, sleep scoring also used scalp polysomnography (C3, C4, Pz, EOG, chin EMG). These scalp
  channels are not part of the shared EDF files.

### Sleep staging (Methods: Sleep staging)
Manual scoring per AASM guidelines with the Visbrain sleep module (data resampled to 250 Hz, 30-s epochs, with
EOG and optionally EMG). Where only iEEG was available, a validated automatic algorithm detected NREM from
neocortical slow waves and spindles, and all other epochs were marked "wake/REM". The per-subject sleep-scoring
vector (30-s resolution, 15 patients) and time from sleep onset (22 patients) are in participants.tsv.

### Annotation procedure (Methods: Manual annotations)
Two neurologists annotated the data (D.E.: full montage of all intracranial channels for 10 UCLA patients; L.G.:
the other 15 patients, montage of the three most medial MTL channels). Annotation used mainly a scalp-reference
montage; for patients with only MTL signals an additional bipolar montage was included. Criteria: IFCN criteria
for interictal epileptiform discharges with intracerebral considerations (Frauscher et al.). Annotators were
blinded to the clinical profile and used Nicolet Reader (Natus) or Persyst. Each tag has a timestamp and the
brain location of the abnormal activity; tags were then converted into channel lists
(derivatives/*_events_interpretation.tsv). Inter-rater agreement on 6 patients: Cohen's kappa 0.63 +/- 0.23
(1-s resolution).

### Files
- sub-XX/ieeg/*_ieeg.edf: EDF, 1000 Hz, microvolts, referential (and some bipolar) depth channels.
- *_ieeg.json: site, power line frequency, recording duration, channel counts, reference.
- *_channels.tsv: channel type/units/cutoffs plus side (L/R) and soz_region (1 = in the seizure-onset zone).
- *_events.tsv: one row per annotated IED (onset s, duration 0, trial_type = neurologist's free-text label,
  sample = onset x 1000).
- *_electrodes.tsv / *_coordsystem.json: MNI152Lin coordinates (mm) for 18 participants; n/a for 7 (see above).
- derivatives/channels.tsv: channel-abbreviation definitions; derivatives/*_events_interpretation.tsv: per-IED
  channel lists (time_in_sec, annotation, chans).
- sourcedata/ieeg_ieds_bids_final.zip: the authors' original archive.

### Preprocessing already applied by the source
Resampling from the 2 kHz acquisition to the shared 1000 Hz (method not stated by the authors); bipolar
derivations added for some patients. The 0.1-500 Hz band-pass and 50/60 Hz notch described in the paper's
"Technical Validation" were applied for the detection model, not to the shared files (SoftwareFilters "n/a" in the
source sidecars).

### How to load
    from mne_bids import BIDSPath, read_raw_bids
    bp = BIDSPath(root="<dataset root>", subject="01", task="sleep", datatype="ieeg", suffix="ieeg", extension=".edf")
    raw = read_raw_bids(bp)   # IED annotations from events.tsv appear in raw.annotations
The authors' detection code: https://github.com/NirLab-TAU/iEEG_ied_detection

### Funding and acknowledgements
See dataset_description.json (Funding, Acknowledgements), copied from the paper's Acknowledgements.
