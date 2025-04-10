# DGSA

<img src='./imgs/OverView.png' width=90%>

## Brief Introduction
Recent works enhance robustness, they also introduce security risks (e.g., adversarial noise). Most existing attack methods (e.g., Set-level Guided Attacks, SGA) primarily focus on transferability while neglecting stealth and often require a high attack budget.We propose a novel \textbf{\textit{Dual-Level Guided Sparse Attack (DGSA)}}, which employs dual-masking screening mechanism to generate sparse noise. The adversarial examples produced by DGSA exhibit highly imperceptible characteristics by leveraging a two-tiered masking strategy—\textbf{Group-level} and \textbf{Pixel-level} masks—to precisely control perturbations at different scales.

## Quick Start 
### 1. Install dependencies
See in `requirements.txt`.

### 2. Prepare datasets and models
Download the datasets, [Flickr30k](https://shannon.cs.illinois.edu/DenotationGraph/) and [MSCOCO](https://cocodataset.org/#home) (the annotations is provided in ./data_annotation/). Set the root path of the dataset in `./configs/Retrieval_flickr.yaml, image_root`.  
The checkpoints of the fine-tuned VLP models is accessible in [ALBEF](https://github.com/salesforce/ALBEF), [TCL](https://github.com/uta-smile/TCL), [CLIP](https://huggingface.co/openai/clip-vit-base-patch16).

### 3. Attack evaluation
From ALBEF to TCL on the Flickr30k dataset:
```python
python eval_albef2tcl_flickr.py 
```

From ALBEF to CLIP<sub>ViT</sub> on the Flickr30k dataset:
```python
python eval_albef2clip-vit_flickr.py 
```

From CLIP<sub>ViT</sub> to ALBEF on the Flickr30k dataset:
```python
python eval_clip-vit2albef_flickr.py 
```

From CLIP<sub>ViT</sub> to CLIP<sub>CNN</sub> on the Flickr30k dataset:
```python
python eval_clip-vit2clip-cnn_flickr.py 
```
## Transferability Evaluation
The performance of SGA on four VLP models (ALBEF, TCL, CLIP<sub>ViT</sub> and CLIP<sub>CNN</sub>), the Flickr30k dataset.
| Source  | Method     | ALBEF TR@1 | ALBEF IR@1 | TCL TR@1 | TCL IR@1 | CLIP-ViT TR@1 | CLIP-ViT IR@1 | CLNP-CNN TR@1 | CLNP-CNN IR@1 |
|---------|------------|-------------|-------------|------------|------------|----------------|----------------|----------------|----------------|
| ALBEF   | SGA        | 100         | 100         | 86.93      | 86.93      | 32.88          | 43.59          | 43.56          | 52.26          |
|         | Co-Attack  | 90.30       | 91.53       | 39.62      | 50.86      | 29.94          | 44.91          | 32.82          | 47.07          |
|         | OUR        | 98.96       | 98.78       | 70.39      | 77.55      | 35.34          | 48.07          | 44.79          | 55.19          |
| TCL     | SGA        | 91.04       | 90.95       | 100        | 100        | 33.62          | 43.33          | 43.44          | 52.80          |
|         | Co-Attack  | 50.50       | 56.38       | 99.05      | 98.93      | 30.55          | 45.43          | 35.25          | 48.47          |
|         | OUR        | 83.35       | 83.19       | 99.17      | 99.30      | 37.30          | 48.84          | 47.36          | 57.18          |
| CLIPVIT | SGA        | 27.42       | 37.04       | 31.18      | 40.81      | 100            | 100            | 57.22          | 62.98          |
|         | Co-Attack  | 7.40        | 20.28       | 10.85      | 22.00      | 89.45          | 95.04          | 25.54          | 36.09          |
|         | OUR        | 20.54       | 35.76       | 23.46      | 38.94      | 99.51          | 99.29          | 51.98          | 58.83          |
| CLIPCNN | SGA        | 18.04       | 32.44       | 23.57      | 36.76      | 44.83          | 57.26          | 100            | 100            |
|         | Co-Attack  | 10.22       | 23.43       | 12.86      | 26.43      | 27.12          | 41.04          | 98.60          | 99.59          |
|         | OUR        | 10.53       | 25.47       | 51.98      | 58.83      | 40.87          | 52.86          | 85.40          | 89.01          |

## Stealthness Evaluation
| Source Model | Attack     | PSNR   | SSIM   | LPIPS  |
|--------------|------------|--------|--------|--------|
| **ALBEF**    | PGD        | 29.24  | 0.805  | 0.143  |
|              | Co-Attack  | 30.67  | **0.910**  | **0.053**  |
|              | SGA        | 26.87  | 0.755  | 0.175  |
|              | Ours       | **32.13**  | 0.891  | 0.062  |
| **TCL**      | PGD        | 29.23  | 0.803  | 0.148  |
|              | Co-Attack  | 30.49  | **0.902**  | **0.062**  |
|              | SGA        | 27.85  | 0.749  | 0.183  |
|              | Ours       | **32.07**  | 0.889  | 0.066  |
| **CLIP-ViT** | PGD        | 29.06  | 0.835  | 0.190  |
|              | Co-Attack  | 30.24  | **0.918**  | **0.093**  |
|              | SGA        | 27.93  | 0.792  | 0.219  |
|              | Ours       | **31.61**  | 0.902  | 0.109  |
| **CLIP-CNN** | PGD        | 30.37  | 0.872  | 0.151  |
|              | Co-Attack  | 30.89  | 0.934  | 0.069  |
|              | SGA        | 38.02  | 0.978  | 0.031  |
|              | Ours       | **39.15**  | **0.984**  | **0.021**  |
## Visualization
<p align="left">
    <img src="./imgs/visualization.jpg" width=100%\>
</p>
