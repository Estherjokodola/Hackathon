# 🏥 DATICAN Hackathon 6 — DICOM Data Organisation Pipeline

**A complete, beginner-friendly guide to running the Medical DICOM Data Organisation Pipeline on Google Colab.**

---

## 📋 Table of Contents

1. [What This Pipeline Does](#1-what-this-pipeline-does)
2. [What You Need Before You Start](#2-what-you-need-before-you-start)
3. [Understanding the Files](#3-understanding-the-files)
4. [Step-by-Step Setup Guide](#4-step-by-step-setup-guide)
   - [Step A — Open Google Colab](#step-a--open-google-colab)
   - [Step B — Upload the Notebook](#step-b--upload-the-notebook)
   - [Step C — Upload Your DICOM Data](#step-c--upload-your-dicom-data)
5. [Running the Pipeline — Cell by Cell](#5-running-the-pipeline--cell-by-cell)
   - [Cell 1 — Extract the ZIP file](#cell-1--extract-the-zip-file)
   - [Cell 2 — Install Libraries & Start Timer](#cell-2--install-libraries--start-timer)
   - [Cell 3 — Set Paths & Locate DICOM Files](#cell-3--set-paths--locate-dicom-files)
   - [Cell 4 — Inspect a Single DICOM File](#cell-4--inspect-a-single-dicom-file)
   - [Cell 5 — Extract Metadata (Parallel)](#cell-5--extract-metadata-parallel)
   - [Cell 6 — View Metadata Table](#cell-6--view-metadata-table)
   - [Cell 7 — Dataset Distribution Analysis](#cell-7--dataset-distribution-analysis)
   - [Cell 8 — Cross-tabulation](#cell-8--cross-tabulation)
   - [Cell 9 — Organise Files](#cell-9--organise-files)
   - [Cell 10 — Validate Output](#cell-10--validate-output)
   - [Cell 11 — View Directory Tree](#cell-11--view-directory-tree)
   - [Cell 12 — Save as ZIP (Optional)](#cell-12--save-as-zip-optional)
   - [Cell 13 — Final Timing Summary](#cell-13--final-timing-summary)
6. [Understanding the Output](#6-understanding-the-output)
7. [Downloading Your Results](#7-downloading-your-results)
8. [Troubleshooting Common Errors](#8-troubleshooting-common-errors)
9. [Glossary](#9-glossary)

---

## 1. What This Pipeline Does

This notebook takes a folder of **DICOM medical imaging files** (`.dcm`) — which are unorganised — and automatically sorts them into a clean, structured folder hierarchy based on three pieces of information embedded inside each file:

| Information | DICOM Tag | Example Value |
|---|---|---|
| **Modality** | What type of scan it is | `MR` (MRI), `DX` (X-ray), `MG` (Mammogram) |
| **Body Part** | Which part of the body was scanned | `BRAIN`, `SHOULDER`, `SPINE` |
| **Subject** | The patient/subject identifier | `MRN161906`, `X134` |

**Before running the pipeline**, your files look like this — a flat pile of numbers:
```
Hackathon_competition_data/
├── 1.dcm
├── 2.dcm
├── 3.dcm
...
└── 50.dcm
```

**After running the pipeline**, your files are organised like this:
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
│   ├── SKULL/
│   ├── TMJ/
│   ├── TSPINE/
│   └── WRIST/
├── MG/
│   └── BREAST/
│       ├── 234441../
│       └── 247868../
└── MR/
    ├── BRAIN/
    ├── CSPINE/
    ├── HEAD/
    ├── LSPINE/
    ├── NECK/
    ├── SPINE/
    └── TLSPINE/
```

The pipeline also records **how long each step takes** so you can measure performance.

---

## 2. What You Need Before You Start

### ✅ Requirements Checklist

| Requirement | Details |
|---|---|
| **A Google account** | Free — needed to use Google Colab |
| **A web browser** | Chrome or Firefox recommended |
| **The notebook file** | `Hackathon6_DICOM_Pipeline_Local.ipynb` |
| **The DICOM data** | `Hackathon_competition_data.zip` — your `.dcm` files zipped up |
| **Internet connection** | Required throughout |

> 💡 **No installation on your computer is needed.** Everything runs in Google Colab, which is a free cloud environment provided by Google. You do not need Python installed locally.

---

## 3. Understanding the Files

You should have these two files:

```
📄 Hackathon6_DICOM_Pipeline_Local.ipynb   ← The notebook (the code)
📦 Hackathon_competition_data.zip          ← Your DICOM data (zipped)
```

- The **`.ipynb` file** is the notebook — it contains all the code, organised into cells you run one at a time.
- The **`.zip` file** is your data — it contains all the `.dcm` DICOM image files. The notebook expects it to be named exactly `Hackathon_competition_data.zip`.

> ⚠️ **Important:** If your ZIP file has a different name, either rename it to `Hackathon_competition_data.zip` before uploading, or update the `zip_path` variable in Cell 1 to match your filename.

---

## 4. Step-by-Step Setup Guide

### Step A — Open Google Colab

1. Open your web browser and go to: **[https://colab.research.google.com](https://colab.research.google.com)**
2. If prompted, **sign in with your Google account**.
3. You will see the Colab welcome screen.

> 📸 **[SCREENSHOT 1]** — *Take a screenshot of the Google Colab homepage after signing in, showing the "New notebook" button and the welcome dialog.*

---

### Step B — Upload the Notebook

There are two ways to open the notebook:

**Option 1 — Upload from your computer (recommended for beginners)**

1. On the Colab welcome screen, click the **"Upload"** tab.
2. Click **"Choose file"** and select `Hackathon6_DICOM_Pipeline_Local.ipynb` from your computer.
3. Click **"Open"**. The notebook will load in Colab.

> 📸 **[SCREENSHOT 2]** — *Take a screenshot of the Colab file upload dialog with the "Upload" tab selected.*

**Option 2 — Open from Google Drive**

1. Save the `.ipynb` file to your Google Drive first.
2. In Colab, click **File → Open notebook → Google Drive** and find the file.

Once the notebook is open, you should see a page with multiple grey code boxes (called **cells**) separated by section headings.

> 📸 **[SCREENSHOT 3]** — *Take a screenshot of the open notebook in Colab, showing the cell layout and the section headings.*

---

### Step C — Upload Your DICOM Data

The notebook needs your `Hackathon_competition_data.zip` file to be uploaded to Colab's temporary storage (`/content/`).

1. In the left sidebar of Colab, click the **folder icon** (📁) to open the Files panel.
2. Click the **upload icon** (a page with an upward arrow) at the top of the Files panel.
3. Select `Hackathon_competition_data.zip` from your computer.
4. Wait for the upload to complete. For 50 files, this usually takes **30 seconds to 2 minutes** depending on your internet speed.
5. Once done, you should see `Hackathon_competition_data.zip` appear in the `/content/` folder in the left panel.

> 📸 **[SCREENSHOT 4]** — *Take a screenshot of the Colab Files panel on the left sidebar, showing the uploaded `Hackathon_competition_data.zip` file visible under `/content/`.*

> ⚠️ **Important:** Colab's temporary storage is wiped when your session ends (after ~90 minutes of inactivity). If you close the tab or the session disconnects, you will need to re-upload the ZIP file.

---

## 5. Running the Pipeline — Cell by Cell

> 🔴 **Critical Rule:** Always run cells **from top to bottom, in order**. Skipping or running cells out of order will cause errors because later cells depend on variables created by earlier ones.

To run a cell, click inside it and either:
- Press **`Shift + Enter`** (runs the cell and moves to the next one), or
- Click the **▶ play button** on the left side of the cell.

A cell is **running** when you see a spinning circle on the left. It is **finished** when you see a green checkmark or a number like `[1]`.

---

### Cell 1 — Extract the ZIP file

**What it does:** Unzips your `Hackathon_competition_data.zip` into a folder called `Hackathon_competition_data` inside `/content/`.

```python
import zipfile
import os

zip_path = "/content/Hackathon_competition_data.zip"
extract_path = "/content/Hackathon_competition_data"

with zipfile.ZipFile(zip_path, 'r') as zip_ref:
    zip_ref.extractall(extract_path)

print("Extraction done ✔️")
print(os.listdir(extract_path))
```

**Expected output:**
```
Extraction done ✔️
['Hackathon_competition_data']
```

> 📸 **[SCREENSHOT 5]** — *Take a screenshot of Cell 1 after running it, showing the "Extraction done ✔️" output and the file list.*

**If you see an error like `FileNotFoundError: /content/Hackathon_competition_data.zip`:**
- Your ZIP file was not uploaded, or it has a different name.
- Go back to [Step C](#step-c--upload-your-dicom-data) and re-upload the file.
- If your file has a different name, change the `zip_path` line to match. For example: `zip_path = "/content/MyData.zip"`

---

### Cell 2 — Install Libraries & Start Timer

**What it does:** Installs the two Python packages needed (`pydicom` for reading DICOM files, `pandas` for data tables), imports all libraries, and **starts the pipeline-wide timer**.

```python
!pip install pydicom pandas

import os, shutil, time
import pydicom
import pandas as pd
from pathlib import Path
from concurrent.futures import ThreadPoolExecutor, as_completed

PIPELINE_START = time.perf_counter()
STEP_TIMES = {}

print("Libraries loaded successfully ✅")
print(f"pydicom version : {pydicom.__version__}")
print(f"pandas  version : {pd.__version__}")
print(f"\n⚠️  Run all cells top-to-bottom for accurate total timing.")
```

**Expected output:**
```
Libraries loaded successfully ✅
pydicom version : 3.0.2
pandas  version : 2.2.2

⚠️  Run all cells top-to-bottom for accurate total timing.
```

> 💡 If you see lines like `Requirement already satisfied: pydicom...` — that is completely normal. It just means the library is already installed in this Colab session.

> ⚠️ **Do not re-run this cell later** unless you re-run the entire notebook from the top. `PIPELINE_START` is set here and the final timing cell depends on it. Re-running it mid-way will reset the clock.

---

### Cell 3 — Set Paths & Locate DICOM Files

**What it does:** Tells the notebook where your DICOM files are, creates the output folder, and counts how many `.dcm` files it can find.

```python
DICOM_FOLDER = r"/content/Hackathon_competition_data"   # <-- change this if needed
OUTPUT_ROOT  = "organized_dataset"
MAX_WORKERS  = 8
```

**Key variables you may need to change:**

| Variable | Default Value | When to Change It |
|---|---|---|
| `DICOM_FOLDER` | `/content/Hackathon_competition_data` | If your extracted folder has a different name or path |
| `OUTPUT_ROOT` | `organized_dataset` | If you want the output saved under a different folder name |
| `MAX_WORKERS` | `8` | Rarely needed; lower it (e.g. to `4`) if you get memory errors |

**Expected output:**
```
Found 50 DICOM files in '/content/Hackathon_competition_data'
⏱️  Step 1 completed in 0.00s
```

> 📸 **[SCREENSHOT 6]** — *Take a screenshot of Cell 3's output showing "Found 50 DICOM files" and the step timing.*

**If you see `Found 0 DICOM files`:**
- The extraction in Cell 1 may have created a nested subfolder. Check the Files panel on the left and look inside the extracted folder. You may need to add an extra level to the path, e.g.: `DICOM_FOLDER = "/content/Hackathon_competition_data/Hackathon_competition_data"`
- The fallback scan (built into the cell) will automatically try to find all files regardless of extension and print their names to help you debug.

---

### Cell 4 — Inspect a Single DICOM File

**What it does:** Reads the very first DICOM file alphabetically and prints five key pieces of metadata from it. This is a **sanity check** to confirm the files are readable and the metadata tags exist.

**Expected output:**
```
Sample file : 1.dcm
Modality    : DX
Body Part   : SHOULDER
Patient ID  : X134
Patient Name: DX_SHOULDER_X134_IBDABC
Study Date  : 20180122
⏱️  Step 2 completed in 0.00s
```

> 💡 If any field shows `N/A`, it means that particular DICOM tag is missing from the file. The pipeline will still work, but those files will be placed in an `Unknown` folder.

---

### Cell 5 — Extract Metadata (Parallel)

**What it does:** This is the most important processing cell. It reads the metadata (Modality, Body Part, Patient ID) from **all 50 DICOM files at the same time** using 8 parallel threads, then stores everything in a table called `df`.

**Why parallel?** Reading files one-by-one is slow because the program has to wait for each file to load before starting the next. By using `ThreadPoolExecutor`, it reads up to 8 files simultaneously, which is significantly faster — especially useful when you have hundreds or thousands of files.

**Expected output:**
```
Successfully parsed : 50 files
Errors              : 0 files
⏱️  Step 3 completed in 0.18s  (8 parallel threads)
```

**If you see `Errors: X files`:**
- The failed filenames and their error messages will be printed below.
- Common causes: corrupted DICOM files, files that are not actually DICOM format (e.g. `.jpg` renamed to `.dcm`).
- The pipeline will continue with the successfully parsed files — only the failed ones are skipped.

---

### Cell 6 — View Metadata Table

**What it does:** Displays the full metadata table — one row per file, showing its filename, modality, body part, and subject ID.

**Expected output** (first few rows):

| | file | modality | body_part | subject |
|---|---|---|---|---|
| 0 | 1.dcm | DX | SHOULDER | X134 |
| 1 | 10.dcm | DX | SKULL | X265 |
| 2 | 11.dcm | DX | SKULL | X365 |
| ... | ... | ... | ... | ... |

> 💡 Scroll down inside the output to see all 50 rows. You can also click the table icon in the output to make it interactive/searchable.

---

### Cell 7 — Dataset Distribution Analysis

**What it does:** Counts how many files belong to each modality and each body part, and prints a summary.

**Expected output:**
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

> 📸 **[SCREENSHOT 7]** — *Take a screenshot of Cell 7's full output showing all three distribution sections.*

---

### Cell 8 — Cross-tabulation

**What it does:** Produces a grid table showing how many files exist for each combination of modality and body part. Useful for spotting which scan type covers which anatomy.

**Expected output:**

| modality | BRAIN | BREAST | CSPINE | HEAD | ... |
|---|---|---|---|---|---|
| DX | 0 | 0 | 0 | 0 | ... |
| MG | 0 | 4 | 0 | 0 | ... |
| MR | 4 | 0 | 4 | 4 | ... |

> 💡 A `0` means that modality does not cover that body part. For example, `MR` (MRI) does not include any `BREAST` scans in this dataset — that is handled by `MG` (Mammography).

---

### Cell 9 — Organise Files

**What it does:** This is where the actual file organisation happens. It reads the metadata table and **copies** each `.dcm` file into its correct folder: `organized_dataset/MODALITY/BODY_PART/SUBJECT/filename.dcm`.

Files are copied (not moved), so your original files in `Hackathon_competition_data` remain untouched.

Like Cell 5, this uses **parallel processing** with 8 threads for faster copying.

**Expected output (first run):**
```
Files copied  : 50
Files skipped : 0 (already existed)
Organised dataset root: 'organized_dataset/'
⏱️  Step 6 completed in 0.45s  (8 parallel threads)
```

**Expected output (if you run the cell again):**
```
Files copied  : 0
Files skipped : 50 (already existed)
```
This is normal — the cell checks if a file already exists at the destination before copying, so re-running it is safe.

> 📸 **[SCREENSHOT 8]** — *Take a screenshot of Cell 9's output showing "Files copied: 50" on the first run.*

---

### Cell 10 — Validate Output

**What it does:** Walks through every folder in `organized_dataset/` and counts the `.dcm` files found. It then checks that the total matches what was in the original metadata table.

**Expected output:**
```
Total entries in organised dataset : 25
Total DICOM files confirmed        : 50
Validation status                  : ✅ PASS
```

Followed by a table listing every subject folder and how many files it contains (should be 2 per subject for this dataset).

**If you see `❌ MISMATCH`:**
- The number of files copied does not match the number parsed. This usually means some files failed to copy (e.g. due to a storage error).
- Re-run Cell 9 to attempt copying the missing files.

---

### Cell 11 — View Directory Tree

**What it does:** Prints a visual tree of the entire `organized_dataset/` folder structure so you can confirm every file is in the right place.

**Expected output (abbreviated):**
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
│   ...
├── MG/
│   └── BREAST/
│       ├── 234441../
│       └── 247868../
└── MR/
    ├── BRAIN/
    ...
    └── TLSPINE/
        └── MRN167313/
            ├── 49.dcm
            └── 50.dcm
```

> 📸 **[SCREENSHOT 9]** — *Take a screenshot of Cell 11's full directory tree output.*

---

### Cell 12 — Save as ZIP (Optional)

**What it does:** Creates a ZIP archive of the entire `organized_dataset/` folder and saves it to `/content/organized_dataset.zip`.

> ⚠️ **This cell is commented out by default.** To enable it, select all the lines in the cell and press `Ctrl + /` (Windows/Linux) or `Cmd + /` (Mac) to uncomment them, then run the cell.

```python
# Uncomment all lines below to enable:
# t0 = time.perf_counter()
# zip_name = "organized_dataset"
# zip_path = shutil.make_archive(zip_name, "zip", OUTPUT_ROOT)
# elapsed = time.perf_counter() - t0
# print(f"✅ ZIP saved to: {os.path.abspath(zip_path)}")
# STEP_TIMES[8] = elapsed
# print(f"⏱️  Step 8 completed in {elapsed:.2f}s")
```

**Expected output after uncommenting:**
```
✅ ZIP saved to: /content/organized_dataset.zip
⏱️  Step 8 completed in 1.23s
```

> 💡 See [Section 7 — Downloading Your Results](#7-downloading-your-results) for how to download this ZIP to your computer.

---

### Cell 13 — Final Timing Summary

**What it does:** Prints a complete breakdown of how long every step took, plus the total wall-clock time for the entire pipeline.

**Expected output:**
```
==================================================
  ⏱️  PIPELINE TIMING BREAKDOWN
==================================================
  Step 1: Locate files                    0.002s
  Step 2: Inspect sample                  0.003s
  Step 3: Extract metadata (parallel)     0.180s
  Step 5: Distribution analysis           0.005s
  Step 6: Organise files (parallel)       0.450s
  Step 7: Validate output                 0.005s
--------------------------------------------------
  Active compute time  :  0.645s
  Total wall-clock time: 45.20s  (incl. display/idle)
==================================================
  Files processed  : 50
  Modalities       : 3
  Body parts       : 14
  Unique subjects  : 25
==================================================
```

> 💡 **Active compute time** is the sum of just the processing steps. **Total wall-clock time** includes all the time spent displaying tables, waiting for you to scroll, etc. — so it will always be larger.

> 📸 **[SCREENSHOT 10]** — *Take a screenshot of the final timing summary output.*

---

## 6. Understanding the Output

After the pipeline completes, you will have a folder called `organized_dataset/` with the following structure:

```
organized_dataset/
├── DX/                          ← Digital X-ray
│   ├── SHOULDER/
│   │   ├── X134/                ← Subject/Patient ID
│   │   │   ├── 1.dcm
│   │   │   └── 2.dcm
│   │   └── X254/
│   ├── SINUS/
│   ├── SKULL/
│   ├── TMJ/
│   ├── TSPINE/
│   └── WRIST/
├── MG/                          ← Mammography
│   └── BREAST/
│       ├── 234441../
│       └── 247868../
└── MR/                          ← Magnetic Resonance Imaging
    ├── BRAIN/
    ├── CSPINE/
    ├── HEAD/
    ├── LSPINE/
    ├── NECK/
    ├── SPINE/
    └── TLSPINE/
```

**Dataset summary:**

| Metric | Value |
|---|---|
| Total files | 50 |
| Modalities | 3 (DX, MG, MR) |
| Body parts | 14 |
| Unique subjects | 25 |
| Files per subject | 2 (consistent) |

---

## 7. Downloading Your Results

Once the pipeline has finished, you need to download the `organized_dataset/` folder to your computer before your Colab session ends.

### Method 1 — Download as ZIP via code (recommended)

1. First, make sure you have **run and uncommented Cell 12** to create the ZIP.
2. In the **Files panel** on the left sidebar, find `organized_dataset.zip`.
3. Right-click on it and select **"Download"**.

> 📸 **[SCREENSHOT 11]** — *Take a screenshot of the Colab Files panel showing `organized_dataset.zip` with the right-click context menu open and "Download" highlighted.*

### Method 2 — Download using code

Run this in a new cell at the bottom of the notebook:

```python
from google.colab import files
import shutil

# Create ZIP if not already done
shutil.make_archive('organized_dataset', 'zip', 'organized_dataset')

# Trigger browser download
files.download('organized_dataset.zip')
```

A download will start automatically in your browser.

### Method 3 — Save to Google Drive first, then download

```python
import shutil

# Copy to your Google Drive
shutil.copytree('organized_dataset', '/content/drive/MyDrive/organized_dataset')
print("Saved to Google Drive ✅")
```

Then go to [drive.google.com](https://drive.google.com), find the `organized_dataset` folder, right-click it, and select **Download**.

> 💡 Method 3 is the safest for large datasets — it saves to Drive first so you don't lose progress if the Colab session disconnects during the browser download.

---

## 8. Troubleshooting Common Errors

### ❌ `FileNotFoundError: /content/Hackathon_competition_data.zip`
**Cause:** The ZIP file was not uploaded to Colab.  
**Fix:** Go to the Files panel (📁 icon on the left), click the upload button, and upload `Hackathon_competition_data.zip`. Then re-run Cell 1.

---

### ❌ `Found 0 DICOM files`
**Cause:** The extraction created a nested folder, or the files don't have a `.dcm` extension.  
**Fix:** In the Files panel, navigate inside the extracted folder and check the actual folder names and file extensions. Update `DICOM_FOLDER` in Cell 3 to point to the correct path. The cell's fallback scan will also print sample filenames to help you identify the correct path.

---

### ❌ `NameError: name 'dcm_files' is not defined`
**Cause:** Cell 3 was not run before Cell 4 (or later cells).  
**Fix:** Run all cells from the top in order. Use **Runtime → Run all** from the menu, or press `Ctrl+F9`.

---

### ❌ `NameError: name 'PIPELINE_START' is not defined`
**Cause:** Cell 2 (the imports and timer cell) was skipped or not run.  
**Fix:** Restart and run all cells from the top. In the menu: **Runtime → Restart and run all**.

---

### ❌ Session disconnected / "Runtime disconnected"
**Cause:** Colab sessions disconnect after ~90 minutes of inactivity, or if the browser tab is closed.  
**Fix:** Click **"Reconnect"** in the top-right corner. Then re-upload your ZIP file (it will be gone) and re-run all cells from Cell 1.

---

### ❌ `Validation status: ❌ MISMATCH`
**Cause:** The number of files in `organized_dataset/` doesn't match the number that were parsed.  
**Fix:** Re-run Cell 9 (organise files). If the mismatch persists, check if any subject IDs contain unusual characters that might have caused issues during folder creation.

---

### ⚠️ ZIP cell doesn't do anything
**Cause:** Cell 12 is commented out by default.  
**Fix:** Select all lines in Cell 12, press `Ctrl+/` (or `Cmd+/` on Mac) to uncomment them, then run the cell.

---

## 9. Glossary

| Term | Meaning |
|---|---|
| **DICOM** | Digital Imaging and Communications in Medicine — the standard file format for medical images (MRI, X-ray, CT, etc.) |
| **`.dcm`** | The file extension for DICOM files |
| **Modality** | The type of imaging equipment used (e.g. MR = MRI scanner, DX = Digital X-ray machine, MG = Mammography machine) |
| **Body Part** | The anatomical region that was scanned (e.g. BRAIN, SHOULDER, SPINE) |
| **Subject / Patient ID** | A unique code that identifies the patient without revealing their name |
| **Google Colab** | A free cloud environment by Google where you can run Python code in a browser without installing anything |
| **Notebook / `.ipynb`** | A file containing code organised into runnable cells, along with text explanations |
| **Cell** | A single block of code inside a notebook |
| **`ThreadPoolExecutor`** | A Python tool that runs multiple tasks at the same time (in parallel) to speed up processing |
| **Metadata** | Information stored inside a file that describes the file — in DICOM, this includes the patient ID, scan type, body part, date, etc. |
| **DataFrame (`df`)** | A table structure in Python (provided by the `pandas` library) used to store and analyse the metadata |
| **`/content/`** | The temporary storage folder in Google Colab — files here are lost when the session ends |
| **Wall-clock time** | The real-world elapsed time from start to finish, including pauses |
| **Active compute time** | Only the time spent actually processing (excludes display time, idle time, etc.) |

---

*README written for DATICAN Hackathon 6 — Medical DICOM Data Organisation Pipeline, 2025.*
