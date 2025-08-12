# Motion Tokenizer Training & Evaluation Pipeline

A comprehensive repository for training and evaluating various motion tokenization methods on human motion datasets.

## Overview

This repository implements and compares multiple motion tokenization approaches:
- **VQ-VAE**: Vector Quantized Variational Autoencoder (single layer)
- **Residual VQ-VAE (RQ-VAE)**: Multi-layer residual quantization 
- **VAE**: Variational Autoencoder
- **AE**: Standard Autoencoder

## Supported Datasets

- **HumanML3D** (primary)
- **Motion-X** 
- **HuMo100M**

## Quick Start

### Installation
```bash
git clone https://github.com/your-org/motion-tokenizer.git
cd motion-tokenizer
pip install -r requirements.txt
```

### Training RQ-VAE (8-layer)
```bash
python train.py --model rq_vae --layers 8 --dataset humanml3d --codebook_size 1024
```

### Evaluation
```bash
python evaluate.py --model_path checkpoints/rq_vae_8.pth --metrics fid mpjpe
```

## Benchmark Results

### HumanML3D Dataset

| Model | Code Size | FID ↓ | MPJPE ↓ |
|-------|-----------|-------|---------|
| VQ-VAE₁ | 1024 | 0.183 | 47.54 |
| RQ-VAE₆ | 1024 | 0.032 | 23.58 |
| **RQ-VAE₈** | 1024 | **0.009** | **20.42** |
| PRQ₄ | 1024 | 0.007 | 14.06 |
| PRQ₆ | 1024 | **0.004** | **13.56** |

## Repository Structure

```
motion-tokenizer/
├── models/
│   ├── vq_vae.py          # VQ-VAE implementation
│   ├── rq_vae.py          # Residual VQ-VAE (6/8 layers)
│   ├── vae.py             # VAE implementation
│   └── autoencoder.py     # Standard AE
├── data/
│   └── humanml3d.py       # HumanML3D data loader
├── training/
│   ├── train.py           # Training script
│   └── config.py          # Configuration files
├── evaluation/
│   ├── evaluate.py        # Evaluation metrics
│   └── metrics.py         # FID, MPJPE calculations
└── utils/
    └── motion_utils.py    # Motion processing utilities
```

## Key Features

- **Multi-layer RQ-VAE**: Extends MoMask's 6-layer approach to 8 layers
- **Comprehensive Evaluation**: FID and MPJPE metrics
- **Modular Design**: Easy to add new tokenization methods
- **HumanML3D Focus**: Optimized for human motion representation

## Training Details

### RQ-VAE₈ Configuration
- **Layers**: 8 residual quantization layers
- **Codebook Size**: 1024 per layer
- **Target FID**: ~0.009 on HumanML3D
- **Architecture**: Based on MoMask with additional quantization layers

### Hyperparameters
```python
{
    "learning_rate": 2e-4,
    "batch_size": 64,
    "num_epochs": 300,
    "commitment_loss": 0.25,
    "quantize_dropout": 0.1
}
```

## Usage Examples

### Training Custom Model
```python
from models.rq_vae import RQVAETokenizer

tokenizer = RQVAETokenizer(
    input_dim=263,  # HumanML3D feature dim
    num_layers=8,
    codebook_size=1024
)

# Training loop
for batch in dataloader:
    loss = tokenizer.training_step(batch)
    loss.backward()
```

### Tokenization
```python
# Encode motion to discrete tokens
tokens = tokenizer.encode(motion_sequence)

# Decode tokens back to motion
reconstructed = tokenizer.decode(tokens)
```

## Evaluation Metrics

- **FID (Fréchet Inception Distance)**: Measures distribution similarity
- **MPJPE (Mean Per Joint Position Error)**: Joint-level reconstruction accuracy

## Contributing

1. Fork the repository
2. Create feature branch (`git checkout -b feature/new-tokenizer`)
3. Implement your tokenizer in `models/`
4. Add evaluation in `evaluation/`
5. Update benchmarks and submit PR

## References

- MoMask: Multi-Modal Masked Modeling for Motion Generation
- MotionLCM: Real-time Controllable Motion Generation
- HumanML3D: 3D Human Motion-Language Dataset

---

*For questions or issues, please open a GitHub issue.*
