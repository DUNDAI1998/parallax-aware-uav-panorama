<h1 align="center">Parallax-Aware UAV Panorama</h1>

<p align="center"><strong>FOUR FISHEYE · ONBOARD ERP · ULTRA-LOW-ALTITUDE UAVS</strong></p>

<p align="center">
  Official implementation for <em>From Multi-Fisheye Sensing to Panoramic Perception: A Parallax-Aware Onboard Platform for Ultra-Low-Altitude UAVs</em>.
</p>

<p align="center">
  <a href="#quick-start">QUICK START</a> ·
  <a href="stitch_parallax_aware.py">CODE</a> ·
  <a href="https://www.dropbox.com/scl/fo/idhp8w5r5s1du2wjt3qjb/AJuZcWHVsMKjzFzAc8-zLTM?rlkey=jh7k1wcxgji3w8qw0rr0vqev4&st=bz72qlfl&dl=0">DATA</a> ·
  <a href="hardware/">HARDWARE</a>
</p>

<p align="center">
  <img src="fig1_teaser.png" alt="Four synchronized fisheye streams formed into an onboard panoramic perception interface" width="100%">
</p>

<p align="center"><sub>Four synchronized fisheye streams are formed onboard into a reusable ERP interface for perception and localization.</sub></p>

## Mission

This release provides the paper's single-file `quality_full` panorama stitcher. It converts four synchronized fisheye streams into a 1280×640 equirectangular panorama (ERP) using per-overlap projection-depth selection, temporal hysteresis, CUDA projection, dynamic seams, photometric correction, and two-band fusion.

| CODE | DATA | HARDWARE |
| :--- | :--- | :--- |
| [Run the released stitcher](stitch_parallax_aware.py) | [Download the panorama and fisheye dataset](https://www.dropbox.com/scl/fo/idhp8w5r5s1du2wjt3qjb/AJuZcWHVsMKjzFzAc8-zLTM?rlkey=jh7k1wcxgji3w8qw0rr0vqev4&st=bz72qlfl&dl=0) | [Open the UAV reference CAD assembly](hardware/) |
| 1280×640 ERP, CUDA-ready | Hosted separately on Dropbox | Sanitized AP242 STEP, checksum, safety boundary |

The hardware CAD is optional for using the stitching algorithm. It is supplied as a research reference, not a certified or ready-to-fly manufacturing package. See [`hardware/`](hardware/) for the licensing boundary and safety notice.

## Capabilities

- Four synchronized fisheye inputs and a 2:1 ERP output contract
- Per-seam adaptive projection from a five-layer depth bank
- Fast-margin temporal state updates and dynamic seam selection
- CUDA execution on Jetson Orin NX, with a CPU-compatible functional path
- Separate code, data, and hardware releases with explicit reuse boundaries

## Quick start

Install the Python dependencies. On Jetson, keep the JetPack-matched CUDA PyTorch build already installed on the target device.

```bash
python3 -m pip install -r requirements.txt
```

Run the stitcher on a directory containing four synchronized camera folders:

```bash
python3 stitch_parallax_aware.py \
  --input-dir /path/to/four_fisheye_sequence \
  --calib-dir calibration \
  --refinement-path configs/image_alignment_refinement.json \
  --color-calibration-path configs/color_balance_calibration.json \
  --output-dir outputs/panoramas \
  --device auto \
  --max-frames 20
```

Use `--device cuda` for the Jetson deployment path and `--device torch-cpu` only for functional compatibility checks.

## Input convention

The default logical mapping is:

```text
left   -> left_front
bleft  -> right_front
right  -> right_back
bright -> left_back
```

The input directory must contain `fisheye_<topic>_image_raw` or `fisheye_<topic>_image_raw_compress_compressed` folders. Image filenames must end in a parseable timestamp.

## Reproducibility and boundaries

The complete Jetson protocol, including strict 20 Hz pacing, timing gates, power logging, and repeated runs, is summarized in [`docs/reproducibility.md`](docs/reproducibility.md). Runtime values in the paper require the specified target hardware and environment; desktop timings are not substitutes.

The code repository does not include YOLO/VPR weights, raw flight logs, generated experiment results, or internal development branches. Dataset details and checksums are in [`DATASET.md`](DATASET.md).

## Citation and license

If you use this repository, please cite the associated [arXiv preprint](https://arxiv.org/abs/2609.02319):

```bibtex
@misc{dai2026multifisheyesensingpanoramicperception,
  title={From Multi-Fisheye Sensing to Panoramic Perception: A Parallax-Aware Onboard Platform for Ultra-Low-Altitude UAVs},
  author={Dun Dai and Ze Lu and Cheng He and Yaowen Wang and Quan Quan},
  year={2026},
  eprint={2609.02319},
  archivePrefix={arXiv},
  primaryClass={cs.RO},
  url={https://arxiv.org/abs/2609.02319}
}
```

Machine-readable repository metadata is in [`CITATION.cff`](CITATION.cff). Code is released under the MIT License. Hardware design material in [`hardware/`](hardware/) uses its separate CERN-OHL-S v2.0 boundary.
