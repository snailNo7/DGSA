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

