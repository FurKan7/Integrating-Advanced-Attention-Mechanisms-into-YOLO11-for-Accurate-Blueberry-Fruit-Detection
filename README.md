# YOLO11 with Advanced Attention for Blueberry Maturity Detection

Short abstract

We extend `YOLO11` with two attention modules — Efficient Channel Attention (ECA) and ResBlock + CBAM — to improve detection of three blueberry maturity classes (fully ripe, half-ripe, unripe) under real orchard conditions (complex backgrounds, variable illumination, occlusion). Models were trained on 8,000 images (6,000 train / 2,000 test) with 141,312 annotated boxes (~17.7 per image). ResBlock+CBAM yields the highest mAP with modest extra cost; ECA provides near-equivalent accuracy with faster inference. Advanced augmentations (mosaic, mixup) further improved robustness.

Key resources

- Paper used in design: https://ieeexplore.ieee.org/document/11112019
- Entry script: `start_train.py`
- Dependencies: `requirements.txt`


Quick start

1. Install dependencies:

	pip install -r requirements.txt

2. Train (example):

	python start_train.py --cfg ultralytics/cfg/default.yaml --data path/to/dataset.yaml --weights ''

Notes

- Add example visuals to the `img/` folder (e.g., `sample_ripe.jpg`, `attention_comparison.jpg`) to show detections.
- For detailed results and plots, place CSVs or notebooks in a `results/` folder and link them here.

Contact: open an issue or PR for questions or contributions.

---

## Repository overview

This repository contains code, configuration and supporting files for experimenting with attention-augmented `YOLO11` detectors designed for blueberry maturity detection. Key files & folders:

- `start_train.py` — training entry script.
- `requirements.txt` — Python dependency list.
- `img/` — image examples and visualization outputs (add sample images here: `img/sample_*.jpg`).
- `ultralytics/` — modified detection code and configs used in experiments.



## Training & augmentations

- Input augmentations used: mosaic, mixup, random photometric jitter, random scale/crop, horizontal flip.
- Training schedule: see `start_train.py` for hyperparameters (epochs, lr schedule, batch size). Typical run used 50–100 epochs depending on the experiment.
- Hardware: experiments were run on modern GPUs (NVIDIA series). Adjust `batch_size` to fit GPU memory.

## Results (summary)

- Both ECA and ResBlock+CBAM consistently improved precision and recall over the baseline in our tests.
- ResBlock+CBAM: best mAP (small but consistent margin), higher robustness under occlusion and mixed lighting.
- ECA: near-best accuracy with faster inference and lower FLOPs.

For full numeric results, charts, and per-class metrics, add the evaluation notebook or result CSVs to the `results/` folder and link them here.

## Visual examples

Add visualizations to the `img/` folder. Example suggested files and captions:

- `img/sample_ripe.jpg` — fully ripe blueberries detected with bounding boxes.
- `img/sample_halfripe.jpg` — half-ripe examples showing partial occlusion.
- `img/sample_unripe.jpg` — unripe cluster detections in cluttered foliage.
- `img/attention_comparison.jpg` — side-by-side detection maps: baseline vs ECA vs ResBlock+CBAM.

Place images with those filenames in `img/` and they will render in the README. Example Markdown to include an image:

![Ripe sample](img/sample_ripe.jpg)

## How to run

1. Install dependencies:

	pip install -r requirements.txt

2. Start training (example):

	python start_train.py --cfg ultralytics/cfg/default.yaml --data path/to/dataset.yaml --weights ''

3. For evaluation/inference, adapt the `start_train.py` or use the provided `predictor` in `ultralytics/engine/predictor.py`.

Refer to the code comments for exact CLI options and config parameters.

## Citation

If you use this work or the codebase, please cite the accompanying report or this repository in your publications. Key reference used in design: https://ieeexplore.ieee.org/document/11112019


---

_Short summary:_ This repository implements attention-augmented YOLO11 detectors (ECA and ResBlock+CBAM) for blueberry maturity detection. The models are trained on 8k orchard images and improve robustness in occlusion and variable lighting conditions while offering a trade-off between accuracy and inference speed.
