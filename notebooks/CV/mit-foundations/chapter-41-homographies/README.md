# Chapter 41: Homographies

## Overview

This notebook is a Chapter 41 companion tutorial for MIT Foundations of Computer Vision. It turns the chapter's homography ideas into a small, inspectable PyTorch workflow: define a synthetic projective transformation, estimate it from point correspondences with normalized DLT, make the fit robust with RANSAC, and use the recovered mapping for synthetic perspective correction through inverse warping.

The emphasis is educational rather than system-building. The notebook uses synthetic correspondences and a synthetic checkerboard so the geometry, validation metrics, and failure cases stay easy to interpret on CPU without introducing real-image keypoint detection, descriptor matching, or panorama stitching complexity.

## What this notebook covers

- homography intuition and planar assumptions
- homogeneous coordinates
- applying a 3x3 homography to 2D points
- DLT homography estimation
- point normalization and scale ambiguity
- reprojection-error validation
- RANSAC outlier rejection
- grid transformation visualization
- noisy correspondence and inlier/outlier visualization
- perspective correction with inverse warping
- bilinear interpolation
- parameter sweeps
- failure cases
- limitations

## How to run

Run the notebook from the repository root:

```bash
make execute-notebook NOTEBOOK=CV/mit-foundations/chapter-41-homographies/index.ipynb
```

The notebook is CPU-compatible and uses only synthetic data generated inside the notebook. No external image assets are required.

## Key visualizations

- grid transformation under a known homography
- noisy correspondences after adding Gaussian perturbations and synthetic outliers
- RANSAC inlier/outlier visualization compared with the true synthetic split
- original / distorted / rectified checkerboard
- parameter sweep plots for noise sensitivity and RANSAC success under increasing outlier ratios
- failure-case output for nearly collinear correspondences and extreme outlier rates

## Validation metrics

- scale-normalized matrix error: compares the estimated homography to the synthetic ground-truth matrix after normalizing scale, which is necessary because homographies are defined only up to a nonzero scalar
- mean reprojection error: the primary geometric validation metric, measuring how closely the estimated homography maps source points to their observed destination points
- RANSAC precision / recall: precision measures how many predicted inliers are truly inliers, while recall measures how many true inliers RANSAC recovers
- inlier ratio: the fraction of correspondences that survive the RANSAC reprojection-error threshold
- rectification MAE: a synthetic sanity check for dense perspective correction; lower is better, but it is not expected to be exactly zero because inverse warping and bilinear interpolation introduce resampling error

## Limitations

This is a controlled synthetic demonstration. It isolates the projective geometry by using synthetic correspondences and known checkerboard corners, which makes it easy to inspect DLT, RANSAC, and inverse warping behavior without extra pipeline complexity.

The notebook does not address real-image keypoint detection, descriptor matching, lens distortion, occlusion, non-planar scenes, exposure changes, or panorama seam blending. It should be read as an educational PyTorch implementation of core homography ideas, not as a production image-stitching system.

## Reproducibility notes

- the notebook fixes random seeds for the synthetic experiments
- no external image files are required
- synthetic correspondences and the checkerboard are generated directly in the notebook
- the implementation is expected to run on CPU
