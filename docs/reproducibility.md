# Reproducibility notes

The released stitcher is the paper's `quality_full` profile. It is the canonical algorithm release; the lower-cost `onboard_fast` profile is not included here.

For a functional check, use a small synchronized four-view subset and run with `--device torch-cpu` if a CPU-compatible PyTorch installation is available. For the paper's embedded measurements, use the target Jetson Orin NX, the JetPack-matched CUDA PyTorch environment, 1280x640 output, and the fixed calibration/refinement files.

Runtime measurements must record the complete path from four-view availability to ERP publication. Keep input pacing, warm-up duration, deadline, queue policy, repetition count, power mode, and clock policy fixed across methods. Desktop smoke-test timing must not be reported as Jetson performance.

The repository does not include raw flight data, downstream detector/VPR weights, or generated experiment results. Those artifacts require separate licensing, privacy, and provenance review.
