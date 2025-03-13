# BKG Subtraction Using PCA for Data Without Dedicated Background – JWST/MIRI/MRS

Background (BKG) subtraction can be challenging when no dedicated observations are available. This notebook presents a PCA-based method to optimally remove the background while minimizing oversubtraction.

## Overview of the Process

### **Step 1: Computing Centroids**

The centroid is computed for each file using 2D fits, storing relevant band/type information to avoid reopening files multiple times.\
**⚠ This step takes time!**

### **Step 2: Background Subtraction Using PCA**

- **PCA Model:** Computes the principal components (PCs) from selected BKG rate files of a given band. Using 20 PCs typically provides a refined background model.

- **Projection Strategy:**
  1. Mask areas within a certain radius of the central star.
  2. Compute projection coefficients on the median of different science targets with the same band but different orientations. This mitigates signal and scattered light variations while ensuring consistent background subtraction.

- **Subtraction:**
  The computed coefficients are applied to each target rate file, and the BKG-subtracted files are saved in the output directory.

## Requirements

This method **requires** a large **library of background observations**, which you must download and curate to remove poor-quality data.

If needed, I can provide a prepared library (see [Support](#feedback--support)).

**Python 11 is recommended.** Package dependencies are listed in *requirements.txt*.

## Demo

### Download

Download this Git repository, which includes the notebook and essential Python functions.



### Usage

1. Ensure dependencies are installed and run with Python 11.
2. Obtain a sufficient background observation library.
3. Set paths in the dedicated cell:

```python
bkg_dir = "../your_path/BKG-mast/"
data_dir = "../your_path/pds70/sci_bfe_fringe/"
```

4. Adjust mask parameters for optimal results:

```python
nb_fwm = 3  # How many FWM from the centroid should be masked
mflux = 90  # Percentile of brightest pixels to be masked
diff_bands = ['A34', 'B34', 'C34', 'A12', 'B12', 'C12']  # Format: "BANDCHAN", e.g., "A12"
```

### Example

The notebook generates visual outputs to assess background subtraction quality.

## Feedback / Support

Your feedback is welcome! This method has yet to be extensively tested on large datasets.

For questions or support, reach out:

💎 **Email:** [sjuillard@uliege.be](mailto\:sjuillard@uliege.be)

I can perform background subtraction for you or provide a curated background observation library.

## Acknowledgment

This script uses a Python function by Yanis Aragyrious for centroid estimation. The pipeline concept stems from discussions with Danny Gasman, Yanis Aragyrious, and Valentin Christeans.

