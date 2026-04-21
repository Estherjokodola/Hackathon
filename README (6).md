# 🏥 DATICAN Hackathon 6 — DICOM Data Organisation Pipeline

**Author:** Hackathon Team | **Date:** 2025

---

## What This Does

This notebook takes a folder of unorganised DICOM medical imaging files (`.dcm`) and automatically sorts them into a clean folder structure based on three things read from inside each file:

- **Modality** — the type of scan (e.g. MR = MRI, DX = X-ray, MG = Mammogram)
- **Body Part** — what was scanned (e.g. BRAIN, SHOULDER, SPINE)
- **Subject** — the patient ID (e.g. MRN161906, X134)

**Before:**
```
Hackathon_competition_data/
├── 1.dcm
├── 2.dcm
...
└── 50.dcm
```

**After:**
```
organized_dataset/
├── DX/
│   ├── SHOULDER/ → X134/, X254/
│   ├── SINUS/    → X246/, X298/
│   ├── SKULL/    → X265/, X365/
│   ├── TMJ/      → X5494/
│   ├── TSPINE/   → X257/, X381/
│   └── WRIST/    → X263/, X417/
├── MG/
│   └── BREAST/   → 234441../, 247868../
└── MR/
    ├── BRAIN/    → FMRN105577/, FMRN109225/
    ├── CSPINE/   → MRN161906/, MRN175600/
    ├── HEAD/     → MR2823/, MR2918/
    ├── LSPINE/   → MRN135765/, MRN140741/
    ├── NECK/     → UDCS_YAB_18/
    ├── SPINE/    → MR2922/, MR3280/
    └── TLSPINE/  → MRN167313/
```

---

## Our Results

The pipeline was run on the Hackathon competition dataset. Below are the exact outputs produced.

---

### Data Extraction
```
Extraction done ✔️
['Hackathon_competition_data']
```

---

### Libraries
```
Libraries loaded successfully ✅
pydicom version : 3.0.2
pandas  version : 2.2.2
```

---

### Files Located
```
Found 50 DICOM files in '/content/Hackathon_competition_data'
⏱️  Step 1 completed in 0.00s
```

---

### Sample File Inspection
```
Sample file : 1.dcm
Modality    : DX
Body Part   : SHOULDER
Patient ID  : X134
Patient Name: DX_SHOULDER_X134_IBDABC
Study Date  : 20180122
⏱️  Step 2 completed in 0.00s
```

---

### Metadata Extraction
```
Successfully parsed : 50 files
Errors              : 0 files
⏱️  Step 3 completed in 0.18s  (8 parallel threads)
```

---

### Metadata Table (all 50 files)

| # | file | modality | body_part | subject |
|---|---|---|---|---|
| 0 | 1.dcm | DX | SHOULDER | X134 |
| 1 | 10.dcm | DX | SKULL | X265 |
| 2 | 11.dcm | DX | SKULL | X365 |
| 3 | 12.dcm | DX | SKULL | X365 |
| 4 | 13.dcm | DX | TMJ | X5494 |
| 5 | 14.dcm | DX | TMJ | X5494 |
| 6 | 15.dcm | DX | TSPINE | X257 |
| 7 | 16.dcm | DX | TSPINE | X257 |
| 8 | 17.dcm | DX | TSPINE | X381 |
| 9 | 18.dcm | DX | TSPINE | X381 |
| 10 | 19.dcm | DX | WRIST | X263 |
| 11 | 2.dcm | DX | SHOULDER | X134 |
| 12 | 20.dcm | DX | WRIST | X263 |
| 13 | 21.dcm | DX | WRIST | X417 |
| 14 | 22.dcm | DX | WRIST | X417 |
| 15 | 23.dcm | MG | BREAST | 234441.. |
| 16 | 24.dcm | MG | BREAST | 234441.. |
| 17 | 25.dcm | MG | BREAST | 247868.. |
| 18 | 26.dcm | MG | BREAST | 247868.. |
| 19 | 27.dcm | MR | BRAIN | FMRN105577 |
| 20 | 28.dcm | MR | BRAIN | FMRN105577 |
| 21 | 29.dcm | MR | BRAIN | FMRN109225 |
| 22 | 3.dcm | DX | SHOULDER | X254 |
| 23 | 30.dcm | MR | BRAIN | FMRN109225 |
| 24 | 31.dcm | MR | CSPINE | MRN161906 |
| 25 | 32.dcm | MR | CSPINE | MRN161906 |
| 26 | 33.dcm | MR | CSPINE | MRN175600 |
| 27 | 34.dcm | MR | CSPINE | MRN175600 |
| 28 | 35.dcm | MR | HEAD | MR2823 |
| 29 | 36.dcm | MR | HEAD | MR2823 |
| 30 | 37.dcm | MR | HEAD | MR2918 |
| 31 | 38.dcm | MR | HEAD | MR2918 |
| 32 | 39.dcm | MR | LSPINE | MRN135765 |
| 33 | 4.dcm | DX | SHOULDER | X254 |
| 34 | 40.dcm | MR | LSPINE | MRN135765 |
| 35 | 41.dcm | MR | LSPINE | MRN140741 |
| 36 | 42.dcm | MR | LSPINE | MRN140741 |
| 37 | 43.dcm | MR | NECK | UDCS/YAB/18 |
| 38 | 44.dcm | MR | NECK | UDCS/YAB/18 |
| 39 | 45.dcm | MR | SPINE | MR2922 |
| 40 | 46.dcm | MR | SPINE | MR2922 |
| 41 | 47.dcm | MR | SPINE | MR3280 |
| 42 | 48.dcm | MR | SPINE | MR3280 |
| 43 | 49.dcm | MR | TLSPINE | MRN167313 |
| 44 | 5.dcm | DX | SINUS | X246 |
| 45 | 50.dcm | MR | TLSPINE | MRN167313 |
| 46 | 6.dcm | DX | SINUS | X246 |
| 47 | 7.dcm | DX | SINUS | X298 |
| 48 | 8.dcm | DX | SINUS | X298 |
| 49 | 9.dcm | DX | SKULL | X265 |

---

### Distribution Analysis
```
=============================================
  MODALITY DISTRIBUTION
=============================================
modality
MR    24
DX    22
MG     4

=============================================
  BODY PART DISTRIBUTION
=============================================
body_part
SHOULDER    4
SKULL       4
TSPINE      4
WRIST       4
BREAST      4
BRAIN       4
SPINE       4
CSPINE      4
HEAD        4
LSPINE      4
SINUS       4
TMJ         2
NECK        2
TLSPINE     2

=============================================
  SUMMARY STATISTICS
=============================================
  Total files        : 50
  Unique modalities  : 3
  Unique body parts  : 14
  Unique subjects    : 25

⏱️  Step 5 completed in 0.005s
```

---

### Modality × Body Part Cross-tabulation

| modality | BRAIN | BREAST | CSPINE | HEAD | LSPINE | NECK | SHOULDER | SINUS | SKULL | SPINE | TLSPINE | TMJ | TSPINE | WRIST |
|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|
| DX | 0 | 0 | 0 | 0 | 0 | 0 | 4 | 4 | 4 | 0 | 0 | 2 | 4 | 4 |
| MG | 0 | 4 | 0 | 0 | 0 | 0 | 0 | 0 | 0 | 0 | 0 | 0 | 0 | 0 |
| MR | 4 | 0 | 4 | 4 | 4 | 2 | 0 | 0 | 0 | 4 | 2 | 0 | 0 | 0 |

---

### File Organisation
```
Files copied  : 50
Files skipped : 0 (already existed)
Organised dataset root: 'organized_dataset/'
⏱️  Step 6 completed in 0.01s  (8 parallel threads)
```

---

### Validation
```
Total entries in organised dataset : 25
Total DICOM files confirmed        : 50
Validation status                  : ✅ PASS
⏱️  Step 7 completed in 0.005s
```

| modality | body_part | subject | dcm_files |
|---|---|---|---|
| DX | SHOULDER | X134 | 2 |
| DX | SHOULDER | X254 | 2 |
| DX | SINUS | X246 | 2 |
| DX | SINUS | X298 | 2 |
| DX | SKULL | X265 | 2 |
| DX | SKULL | X365 | 2 |
| DX | TMJ | X5494 | 2 |
| DX | TSPINE | X257 | 2 |
| DX | TSPINE | X381 | 2 |
| DX | WRIST | X263 | 2 |
| DX | WRIST | X417 | 2 |
| MG | BREAST | 234441.. | 2 |
| MG | BREAST | 247868.. | 2 |
| MR | BRAIN | FMRN105577 | 2 |
| MR | BRAIN | FMRN109225 | 2 |
| MR | CSPINE | MRN161906 | 2 |
| MR | CSPINE | MRN175600 | 2 |
| MR | HEAD | MR2823 | 2 |
| MR | HEAD | MR2918 | 2 |
| MR | LSPINE | MRN135765 | 2 |
| MR | LSPINE | MRN140741 | 2 |
| MR | NECK | UDCS_YAB_18 | 2 |
| MR | SPINE | MR2922 | 2 |
| MR | SPINE | MR3280 | 2 |
| MR | TLSPINE | MRN167313 | 2 |

---

### Directory Tree
```
organized_dataset/
├── DX/
│   ├── SHOULDER/
│   │   ├── X134/
│   │   │   ├── 1.dcm
│   │   │   └── 2.dcm
│   │   └── X254/
│   │       ├── 3.dcm
│   │       └── 4.dcm
│   ├── SINUS/
│   │   ├── X246/
│   │   │   ├── 5.dcm
│   │   │   └── 6.dcm
│   │   └── X298/
│   │       ├── 7.dcm
│   │       └── 8.dcm
│   ├── SKULL/
│   │   ├── X265/
│   │   │   ├── 10.dcm
│   │   │   └── 9.dcm
│   │   └── X365/
│   │       ├── 11.dcm
│   │       └── 12.dcm
│   ├── TMJ/
│   │   └── X5494/
│   │       ├── 13.dcm
│   │       └── 14.dcm
│   ├── TSPINE/
│   │   ├── X257/
│   │   │   ├── 15.dcm
│   │   │   └── 16.dcm
│   │   └── X381/
│   │       ├── 17.dcm
│   │       └── 18.dcm
│   └── WRIST/
│       ├── X263/
│       │   ├── 19.dcm
│       │   └── 20.dcm
│       └── X417/
│           ├── 21.dcm
│           └── 22.dcm
├── MG/
│   └── BREAST/
│       ├── 234441../
│       │   ├── 23.dcm
│       │   └── 24.dcm
│       └── 247868../
│           ├── 25.dcm
│           └── 26.dcm
└── MR/
    ├── BRAIN/
    │   ├── FMRN105577/
    │   │   ├── 27.dcm
    │   │   └── 28.dcm
    │   └── FMRN109225/
    │       ├── 29.dcm
    │       └── 30.dcm
    ├── CSPINE/
    │   ├── MRN161906/
    │   │   ├── 31.dcm
    │   │   └── 32.dcm
    │   └── MRN175600/
    │       ├── 33.dcm
    │       └── 34.dcm
    ├── HEAD/
    │   ├── MR2823/
    │   │   ├── 35.dcm
    │   │   └── 36.dcm
    │   └── MR2918/
    │       ├── 37.dcm
    │       └── 38.dcm
    ├── LSPINE/
    │   ├── MRN135765/
    │   │   ├── 39.dcm
    │   │   └── 40.dcm
    │   └── MRN140741/
    │       ├── 41.dcm
    │       └── 42.dcm
    ├── NECK/
    │   └── UDCS_YAB_18/
    │       ├── 43.dcm
    │       └── 44.dcm
    ├── SPINE/
    │   ├── MR2922/
    │   │   ├── 45.dcm
    │   │   └── 46.dcm
    │   └── MR3280/
    │       ├── 47.dcm
    │       └── 48.dcm
    └── TLSPINE/
        └── MRN167313/
            ├── 49.dcm
            └── 50.dcm
```

---

### Final Timing Summary
```
==================================================
  ⏱️  PIPELINE TIMING BREAKDOWN
==================================================
  Step 1: Locate files                    0.001s
  Step 2: Inspect sample                  0.005s
  Step 3: Extract metadata (parallel)     0.181s
  Step 5: Distribution analysis           0.005s
  Step 6: Organise files (parallel)       0.013s
  Step 7: Validate output                 0.005s
--------------------------------------------------
  Active compute time  :  0.212s
  Total wall-clock time:   0.42s  (incl. display/idle)
==================================================
  Files processed  : 50
  Modalities       : 3
  Body parts       : 14
  Unique subjects  : 25
==================================================
```

> ⚠️ **Note on timing:** These results were recorded on a Google Colab session on 21 April 2025. Timing will vary depending on your Colab instance, internet speed, and whether files are being read for the first time or from cache. Active compute time should remain well under 1 second for a 50-file dataset, but total wall-clock time may range from 0.3s to several seconds depending on your environment.

---

## How to Run the Notebook

### What you need
- A Google account (free)
- A web browser
- `Hackathon6_DICOM_Pipeline_Local.ipynb` — the notebook
- `Hackathon_competition_data.zip` — your DICOM data

---

### Step 1 — Open Google Colab

Go to [colab.research.google.com](https://colab.research.google.com) and sign in.

---

### Step 2 — Open the Notebook

Click **File → Upload notebook**, then select `Hackathon6_DICOM_Pipeline_Local.ipynb` from your computer. The notebook will open with all cells visible.

---

### Step 3 — Upload Your Data

1. In the left sidebar, click the **folder icon (📁)**
2. Click the **upload button** (page with an upward arrow)
3. Upload `Hackathon_competition_data.zip`
4. Wait until it appears under `/content/` in the sidebar

---

### Step 4 — Run All Cells in Order

> **Always run cells top to bottom. Never skip a cell.**

Use **Shift + Enter** to run one cell at a time, or **Runtime → Run all** to run everything at once.

| Cell | What it does |
|---|---|
| **Cell 1** | Unzips your data into `/content/Hackathon_competition_data` |
| **Cell 2** | Installs libraries and starts the pipeline timer |
| **Cell 3** | Sets the folder paths and counts your `.dcm` files |
| **Cell 4** | Reads one file to confirm the metadata tags work |
| **Cell 5** | Reads all 50 files in parallel and builds the metadata table |
| **Cell 6** | Displays the full metadata table |
| **Cell 7** | Prints modality and body part counts |
| **Cell 8** | Shows a modality × body part grid |
| **Cell 9** | Copies each file into its organised folder |
| **Cell 10** | Confirms all 50 files landed in the right place |
| **Cell 11** | Prints the full directory tree |
| **Cell 12** | *(Optional)* Saves the output as a ZIP — uncomment lines to activate |
| **Cell 13** | Prints the timing breakdown for every step |

---

### Step 5 — Download Your Results

Run this in a new cell at the bottom of the notebook:

```python
from google.colab import files
import shutil

shutil.make_archive('organized_dataset', 'zip', 'organized_dataset')
files.download('organized_dataset.zip')
```

This zips the organised folder and triggers a download to your computer.

---

### Common Errors

| Error | Fix |
|---|---|
| `FileNotFoundError: Hackathon_competition_data.zip` | The ZIP was not uploaded. Go back to Step 3 and upload it. |
| `Found 0 DICOM files` | Change `DICOM_FOLDER` in Cell 3 to `/content/Hackathon_competition_data/Hackathon_competition_data` |
| `NameError: name 'dcm_files' is not defined` | A cell was skipped. Use **Runtime → Restart and run all** |
| Session disconnected | Click Reconnect, re-upload the ZIP, and run all cells again from Cell 1 |

---

*DATICAN Hackathon 6 — Medical DICOM Data Organisation Pipeline, 2025.*
