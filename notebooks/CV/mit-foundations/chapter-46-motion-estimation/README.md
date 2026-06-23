# Chapter 46: Motion Estimation

This chapter adds an educational patch-matching demo for basic motion estimation. The notebook builds two synthetic grayscale frames in PyTorch, applies a known translation, and estimates motion by searching for the best matching patch inside a local window.

## What the notebook covers

- motion-estimation intuition using frame 1, frame 2, local patches, search windows, matching costs, and motion vectors
- explicit motion-sign convention where positive `dx` means rightward motion and positive `dy` means downward image motion
- a CPU-friendly synthetic translation example with known ground-truth motion
- readable PyTorch helper functions for patch extraction, SSD/SAD costs, local search, sparse motion estimation, and endpoint error
- simple border handling where candidate patches near image edges may be skipped if a full patch cannot be extracted safely
- validation using predicted motion, ground truth, endpoint error, exact integer-vector recovery ratio in the synthetic setting, and candidate comparison counts
- a small parameter study over patch size, search radius, and noise level
- failure cases for undersized search windows and repeated-pattern ambiguity

## How to run it

From the repository root:

```bash
make execute-notebook NOTEBOOK=CV/mit-foundations/chapter-46-motion-estimation/index.ipynb
```

The notebook itself uses `device = torch.device("cpu")`, so the computation is CPU-compatible even when launched from the standard notebook environment.

## Key visualizations

- frame 1 and frame 2 shown side by side
- a highlighted query patch in frame 1
- the search window in frame 2
- an SSD matching-cost heatmap
- the best matching patch
- sparse motion vectors overlaid on frame 1
- failure-case heatmaps showing why matching breaks

## Validation metrics

- predicted motion vector versus ground-truth motion vector
- endpoint error
- correct match ratio over multiple sampled patches, defined here as exact integer-vector recovery in the controlled synthetic setup
- number of candidate comparisons and approximate runtime

## Limitations

- integer-pixel matching only
- assumes brightness consistency
- sensitive to low texture, repeated patterns, occlusion, and motion boundaries
- designed as an educational patch-matching demo, not a full optical-flow system
