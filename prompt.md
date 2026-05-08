# 🌟 PROMPT: Build “LanternLLM” (Mini PyTorch Chatbot on AMD ROCm)

You are an expert ML engineer and systems architect specializing in PyTorch, ROCm (AMD GPU stack), and lightweight LLM training pipelines on consumer hardware.

Your task is to design and generate a complete, production-quality mini AI chatbot project named:

> LanternLLM

The system must be optimized for:

GPU: **AMD Radeon RX 6650 XT (8GB VRAM)**\
RAM: **16GB system memory**\
OS: **Ubuntu 24.04 LTS**\
ROCm: **1.18 + ROCm extension 1.15 compatibility layer**\

## 🧠 PROJECT GOAL

Build a **local, trainable chatbot system** that:

- Trains on a local dataset folder called `train`
- Supports multiple file formats:
  - '.txt'
  - '.pdf'
  - '.md'
  - '.json'
  - (extensible parser system for future formats)\
- Uses PyTorch (ROCm-compatible)
- Runs fully offline after training
- Has a simple CLI + optional REST API inference mode

The model should be:

- Small-scale transformer or GPT-style decoder-only model
- Optimized for low VRAM (8GB constraint)
- Capable of incremental training (fine-tuning on local data)
## 🏗️ REQUIRED OUTPUT FORMAT

You MUST output a **complete project blueprint**, including:

1. 📁 Project File Structure

Design a modular structure like:
```
LanternLLM/
│
├── data/
│   ├── train/
│   ├── processed/
│   └── loaders/
│
├── models/
│   ├── architecture.py
│   ├── tokenizer.py
│   ├── config.py
│
├── training/
│   ├── train.py
│   ├── dataset.py
│   ├── preprocessing.py
│   ├── collate.py
│
├── inference/
│   ├── chat.py
│   ├── generate.py
│
├── api/
│   ├── server.py (FastAPI or Flask)
│
├── utils/
│   ├── file_parser.py
│   ├── logger.py
│   ├── device.py (ROCm detection)
│
├── checkpoints/
├── requirements.txt
└── README.md
```
---
### 2. 🧠 Model Architecture

Define:

- A **small GPT-style decoder-only transformer**
- Attention mechanism optimized for low VRAM
- Gradient checkpointing support
- Mixed precision (FP16 / BF16 if supported in ROCm)
- Token embedding strategy
- Positional encoding method

Include:

- Parameter sizing recommendation for 8GB GPU
- Batch size recommendations
- Sequence length limits
---
### 3. ⚙️ ROCm + AMD OPTIMIZATION

You MUST include:

- PyTorch ROCm installation notes
- Device handling (`torch.device("cuda" if rocm else "cpu")`)
- Memory optimization strategies:
- gradient accumulation
- activation checkpointing
- reduced precision training
- Workarounds for AMD GPU limitations vs CUDA
---
### 4. 📂 DATA PIPELINE (IMPORTANT)

Implement a robust ingestion system:

#### Must support:
- `.txt` → raw text loader
- `.pdf` → PyPDF / pdfminer extraction
- `.json` → structured chat data parsing
- `.md` → markdown cleanup parser

Pipeline steps:

1. Load files from train/
2. Normalize text
3. Clean noise (headers, footers, encoding issues)
4. Chunk into training sequences
5. Tokenize using custom tokenizer or BPE

---

###  5. 🧪 TRAINING SYSTEM

Include:

- Full train.py script
- Dataset class
- DataLoader with collate function
- Training loop with:
  - loss logging
  - checkpoint saving
  - validation split
- Learning rate scheduler
- Gradient clipping

Must include:

- resume training support
- checkpoint versioning system
---
### 6. 💬 INFERENCE ENGINE

Create:

- CLI chatbot (chat.py)
- Streaming token generation
- Temperature, top-k, top-p sampling controls
- Conversation memory buffer

Optional:

- simple web API (FastAPI)

---

### 7. 🧰 UTILITIES

Include:

- ROCm GPU detection utility
- File parser abstraction layer
- Logging system (structured logs)
- Config loader (YAML or JSON)

---

### 8. 📦 requirements.txt

Must include:

- torch (ROCm compatible build)
- transformers (optional but explain tradeoffs)
- numpy
- tqdm
- fastapi (optional)
- pypdf or pdfminer
- sentencepiece (if tokenizer used)
- regex / nltk (light preprocessing)

---
### 9. 📘 README.md

Include:

- Setup instructions for Ubuntu 24.04
- ROCm installation notes
- How to prepare dataset
- How to train
- How to run chatbot
- Performance expectations on RX 6650 XT
- Fully **GitHub** Ready

---

### ⚡ IMPORTANT CONSTRAINTS
- NO CUDA assumptions
- Must explicitly support ROCm
- Must be lightweight enough for 8GB VRAM
- Avoid huge transformer models (no GPT-3 scale ideas)
- Prefer efficiency over scale
- Everything should run locally

---
### 🚀 EXTRA CREDIT (OPTIONAL BUT PREFERRED)

If possible, also include:

- Quantization strategy (4-bit or 8-bit inference)
- LoRA-style fine-tuning option
- Simple dataset augmentation pipeline
- Memory-mapped dataset loading for large files

--
### 🎯 FINAL OUTPUT REQUIREMENT

Return:

1. Full architecture explanation
2. Complete file tree
3. Key code snippets for each module
4. Training + inference workflows
5. ROCm-specific optimizations
6. Setup guide

Make it production-quality, not toy-level.