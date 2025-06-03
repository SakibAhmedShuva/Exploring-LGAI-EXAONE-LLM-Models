# 🚀 Exploring LGAI-EXAONE LLM Models for NER

[![Python](https://img.shields.io/badge/Python-3.9+-blue.svg)](https://python.org)
[![License](https://img.shields.io/badge/License-MIT-green.svg)](LICENSE)
[![Jupyter](https://img.shields.io/badge/Jupyter-Notebook-orange.svg)](https://jupyter.org)

This repository contains Jupyter notebooks and resources for exploring and evaluating different versions and quantization methods of the **LGAI-EXAONE Large Language Models**, primarily focusing on Named Entity Recognition (NER) tasks with structured JSON output.

---

## 📋 Overview

### Primary Goals
1. **Load and run** various LGAI-EXAONE models (base, GGUF, AWQ quantized)
2. **Evaluate performance** on sample NER tasks
3. **Compare inference speed** and output quality across different model formats
4. **Provide practical guidance** for setting up and using these models

> 💡 **Note**: All models are instructed to produce JSON-only responses for easier parsing and integration.

---

## 🤖 Models Explored

### EXAONE Models
| Model | Type | Description |
|-------|------|-------------|
| `LGAI-EXAONE/EXAONE-3.5-2.4B-Instruct` | Base | The base instruction-tuned model |
| `LGAI-EXAONE/EXAONE-3.5-2.4B-Instruct-GGUF` | GGUF | Quantized versions for CPU/GPU inference with `llama-cpp-python` |
| `LGAI-EXAONE/EXAONE-3.5-2.4B-Instruct-AWQ` | AWQ | Quantized version for optimized inference with Hugging Face Transformers |

### Comparison Models (Granite)
- `bartowski/granite-3.1-2b-instruct-GGUF`
- `ibm-granite/granite-3.3-2b-instruct-GGUF`

---

## 📓 Notebooks

### 1. `lgai-exaone-gguf.ipynb`
- **🎯 Purpose**: Demonstrates loading and running GGUF quantized models (EXAONE and Granite variants)
- **📚 Key Libraries**: `llama-cpp-python`
- **🔍 Focus**: Measures inference time for NER task on various GGUF quantization levels
- **⚙️ Quantization Levels**: Q8_0, IQ4_XS, Q4_0, Q2_K, Q4_K_S

### 2. `lgai-exaone_AWQ.ipynb`
- **🎯 Purpose**: Shows how to load and run the AWQ (Activation-aware Weight Quantization) version
- **📚 Key Libraries**: `transformers`, `autoawq`, `torch`
- **🔍 Focus**: Measures inference time for NER task on AWQ quantized EXAONE model

### 3. `lgai-exaone.ipynb`
- **🎯 Purpose**: Demonstrates the base `LGAI-EXAONE/EXAONE-3.5-2.4B-Instruct` model
- **📚 Key Libraries**: `transformers`, `torch`
- **🔍 Focus**: Baseline performance and output for NER task with full-precision model

> ⚠️ **Note**: The current content of `lgai-exaone.ipynb` may include AWQ model loading. This should be clarified/cleaned if it's meant for base model comparison.

---

## 🛠️ Setup and Installation

### Prerequisites
- **Python**: 3.9+
- **Package Manager**: `pip`
- **Hardware**: NVIDIA GPU with CUDA drivers (highly recommended)
- **Build Tools**: `cmake`, C++ compiler (if compiling `llama-cpp-python` from source)

### Installation Steps

#### 1. Clone the Repository
```bash
git clone https://github.com/SakibAhmedShuva/Exploring-LGAI-EXAONE-LLM-Models.git
cd Exploring-LGAI-EXAONE-LLM-Models
```

#### 2. Create Virtual Environment (Recommended)
```bash
python -m venv venv

# Linux/Mac
source venv/bin/activate

# Windows
venv\Scripts\activate
```

#### 3. Install Dependencies

**For GGUF Models** (`lgai-exaone-gguf.ipynb`):
```bash
pip install -r requirements.txt

# For CUDA support (if needed):
CMAKE_ARGS="-DLLAMA_CUBLAS=on" FORCE_CMAKE=1 pip install llama-cpp-python --no-cache-dir -U
```

**For AWQ and Base Transformers** (`lgai-exaone_AWQ.ipynb`, `lgai-exaone.ipynb`):
```bash
pip install -r requirements.txt
```

> 💡 **Tip**: Consider separate requirements files (`requirements_gguf.txt`, `requirements_awq.txt`) if dependencies conflict.

---

## 🚀 How to Run

### Quick Start
1. ✅ Complete the **Setup and Installation** steps
2. ✅ Activate your virtual environment
3. ✅ Launch Jupyter:
   ```bash
   jupyter lab
   # or
   jupyter notebook
   ```
4. ✅ Open desired notebook (`.ipynb` file)
5. ✅ Run cells sequentially

### Important Notes
- 📦 First code cell usually installs necessary packages
- 🔄 Subsequent cells define prompts, load models, and perform inference
- ⏳ Model downloads can take time and require significant disk space

---

## 📝 Example Task: Named Entity Recognition

All notebooks use a structured approach for NER tasks:

### System Prompt Structure
```markdown
You are a JSON-only response system. Follow these rules absolutely:
ONLY output valid, parseable JSON
...
```

### Test Instruction Example
```markdown
extract NER:
California
DRIVER LICENSE
dl 11234568
...
```

---

## 📊 Key Observations

### GGUF Models Performance
| Quantization | Quality | Speed | Size | Use Case |
|--------------|---------|-------|------|----------|
| **Q8_0** | ⭐⭐⭐⭐ | ⭐⭐⭐ | ⭐⭐ | **Recommended balance** |
| **Q4_0** | ⭐⭐⭐ | ⭐⭐⭐⭐ | ⭐⭐⭐⭐ | Fast inference |
| **Q2_K** | ⭐⭐ | ⭐⭐⭐⭐⭐ | ⭐⭐⭐⭐⭐ | Maximum speed |
| **BF16** | ⭐⭐⭐⭐⭐ | ⭐⭐ | ⭐ | Highest quality |

### AWQ Models
- ✅ **Significant speedup** over base model
- ✅ **Minimal quality loss** for NER tasks
- ⚠️ Requires `autoawq` and compatible `transformers` versions

### Inference Performance
- 🚀 **AWQ models on GPU**: Generally very fast
- ⚖️ **GGUF models**: Flexible for CPU/GPU with varying performance by quantization
- 💻 **Hardware dependency**: Performance varies significantly with available hardware

---

## 📄 License

This repository is licensed under the **[MIT License](LICENSE)**. 

> ⚠️ **Important**: Model weights are subject to their own licenses as specified by their respective Hugging Face repositories.

---

## 🤝 Contributing

Contributions are welcome! Please feel free to submit a Pull Request.

## 📞 Support

If you encounter any issues or have questions, please open an issue in this repository.

---

<div align="center">

**⭐ Star this repository if you find it helpful! ⭐**

Made with ❤️ for the ML community

</div>
