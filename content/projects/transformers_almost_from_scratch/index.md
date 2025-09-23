---
title: "Transformers Almost From Scratch"
summary: "Educational PyTorch implementation of core Transformer components with a tiny LM (and a ViT variant)."
tags: ["Transformers", "PyTorch", "NLP", "Vision", "From Scratch"]
thumbnail: "cover.png"
cover: "cover.png"   # optional: add an attention diagram or sample output
weight: 4
showToc: false
---

Similarly to my neural networks from scratch project I developed a from‑scratch exploration of the **Transformer** architecture in **PyTorch**, focused on understanding self‑attention, multi‑head attention, and Transformer blocks. 
Includes a small language model and also a Vision Transformer (ViT) variant!
Training/metrics tooling is intentionally minimal to keep the core ideas clear.

# Implementation details

{{< button href="https://github.com/jofragotre/transformers-almost-from-scratch" >}}
Code on GitHub
{{< /button >}}

## Key features
- Self‑attention with causal masking
- Multi‑head attention (configurable heads/emb size/block size)
- Transformer blocks: attention + feedforward + residual + norm
- Tiny language model with token/positional embeddings and `generate`
- Vision Transformer (ViT) model added in `models.py` (training TODO)
- Minimal, educational training script for a small text dataset

## File structure
- `self_attention.py` — attention head, multi‑head, feedforward, block (+ examples)
- `models.py` — `SmallLanguageModel` (LM head, generate), plus a ViT implementation
- `tokenizers.py` — `BaseTokenizer`, `SimpleTokenizer` (char‑level)
- `dataset/text_dataset.py` — `TextDataset`, train/val split, batching
- `train.py` — dataset/tokenizer wiring, model init, loop, text generation
- `dataset/input.txt` — raw text used for training
- `example_output.txt` — sample LM generations
- `.gitignore` — housekeeping

## Requirements
- Python 3.8+
- PyTorch 1.10+
- tqdm

Install:
```bash
pip install torch tqdm
```

## Training setup

1) Prepare data  
Place your text in `dataset/input.txt`. The `SimpleTokenizer` builds a vocab and
tokenizes characters.

2) Configure and train  
Edit hyperparameters in `train.py` (`BATCH_SIZE`, `BLOCK_SIZE`, `LEARNING_RATE`,
etc.), then:
```bash
python train.py
```

3) Generate text  
After training, use the script’s generation call or the model’s `generate`
method to sample text.

## Usage

Test core components:
```bash
python self_attention.py
```

Train the Transformer LM:
```bash
python train.py
```

## Output
- `self_attention.py` prints tensor shapes to validate attention/blocks
- `train.py` prints training/validation loss and emits generated samples
- Example generations saved to `example_output.txt`

## Notes and roadmap
- The repo prioritizes architectural clarity over training bells/whistles
- TODO:
  - Add configs, logging, checkpointing
  - Train the ViT on a tiny dataset (e.g., MNIST) as a proof of concept
  - Add metrics/plots and save/load utilities

## References
- Vaswani et al., “Attention Is All You Need” — https://arxiv.org/abs/1706.0372