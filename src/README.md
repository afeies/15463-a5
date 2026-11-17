# 15463-a5: Photometric stereo

All code is in `src/assgn5.ipynb`. Open it from the `src/` folder (so relative paths resolve) and run the cells from top to bottom. Every figure used in the report is saved to `data/report_images/`.

## Requirements

Python 3 with `numpy`, `matplotlib`, `scikit-image`, and `scipy`. Part 2 also needs `dcraw` to convert the RAW files (one-time step, below).

## Folders

| Path | Contents |
|---|---|
| `assgn5-report.pdf` | the report |
| `src/assgn5.ipynb` | the notebook (Part 1, then Part 2) |
| `src/cp_hw5.py` | provided helpers: `integrate_poisson`, `integrate_frankot`, `load_sources` |
| `data/report_images/` | figures saved by the notebook |
| `data/` | Part 1 face images (`input_1.tif` … `input_7.tif`); provided with the assignment, so not included in the submission |
| `data/paper/` | Part 2, object A (crumpled paper): RAW files `DSC_0371`–`DSC_0393.NEF` |
| `data/sneaker/` | Part 2, object B (sneaker): RAW files `DSC_0400`–`DSC_0421.NEF` |
| `data/paper/tiff/`, `data/sneaker/tiff/` | linear TIFFs made from the RAW files; the notebook reads these |

The RAW files and TIFFs are too large to include in the repository.

## Part 1

Copy the provided `input_1.tif` … `input_7.tif` into `data/`. Then run the cells under `# 1. Photometric stereo`.

## Part 2

**One-time step: convert RAW to linear TIFF.** From the repo root:

```bash
mkdir -p data/paper/tiff data/sneaker/tiff
for f in data/paper/*.NEF;   do dcraw -h -4 -T -w -o 1 -c "$f" > data/paper/tiff/$(basename "$f" .NEF).tiff;   done
for f in data/sneaker/*.NEF; do dcraw -h -4 -T -w -o 1 -c "$f" > data/sneaker/tiff/$(basename "$f" .NEF).tiff; done
```

| Flag | Meaning |
|---|---|
| `-h` | half-size output (3008 × 2008) |
| `-4` | 16-bit linear output (no gamma, no auto-brightening) |
| `-T` | write a TIFF |
| `-w` | use the camera's white balance |
| `-o 1` | sRGB primaries (linear) |
| `-c` | write to stdout |

Then run the cells under `# 2. Capture and reconstruct your own shapes`. They need the Part 1 helper cells to have run first.

The frames used for each light direction, the light-off (ambient) frames, and the crop boxes are listed at the top of each object's loading cell. Edit them there if the data changes.
