# Synthetic Brain MRI Generation for Alzheimer's Disease Using Diffusion Models

An end-to-end deep learning framework for generating, evaluating, and classifying synthetic 2D coronal brain MRI slices targeting the anterior hippocampal formation. This project fine-tunes a Denoising Diffusion Probabilistic Model (DDPM) on the OASIS-1 dataset, compares noise schedule behaviors, introduces a domain-specific RadImageNet FID metric, and evaluates diagnostic utility through patient-isolated downstream classification.

---

## 📌 Project Summary

* **Task**: Synthetic 2D Coronal MRI Generation & Downstream Alzheimer's Classification
* **Dataset**: OASIS-1 Neuroimaging Dataset (T1-weighted volumes registered in T88 space)
* **Generative Model**: Fine-tuned 2D DDPM backbone (`benetraco/brain_ddpm_128`)
* **Evaluation Metrics**: Dual-feature FID (Standard ImageNet vs. Domain-specific RadImageNet)
* **Downstream Classifiers**: Patient-isolated ResNet50 (RadImageNet), ResNet18 (ImageNet), and SimpleCNN

---

## 🛠️ Repository Architecture & Code Files

### Main Notebooks (`/`)
* **`DDPM coronal (linear).ipynb`**: Main project notebook. Contains the 2D DDPM fine-tuning pipeline under a linear noise schedule, synthetic image generation, correlation analysis, and standard FID score calculations[cite: 6].
* **`Noise Schedule Ablation.ipynb`**: Ablation experiment comparing output quality and FID scores across three noise configurations: Cosine ($T=1000$), Linear ($T=1000$), and Cosine ($T=500$)[cite: 6].
* **`RadnetFID+Classifier(linear).ipynb`**: Domain-specific evaluation notebook. Extracts features via RadImageNet to compute clinical-grade FID scores, and trains/evaluates the primary RadImageNet-pretrained ResNet50 classifier across three data configurations[cite: 5, 6].

### Miscellaneous & Utilities (`/misc`)
* **`preprocess- 3D to 2D coronal.py`**: Python script to load raw 3D T1 OASIS-1 volumes, extract 2D coronal cross-sections ($y=95$ to $y=115$), perform min-max intensity normalization, and output PNG images[cite: 6].
* **`CNN+Resnet18 classifie.ipynb`**: Baseline classification scripts evaluating dataset configurations using SimpleCNN and standard ImageNet-pretrained ResNet18[cite: 6].

---

## ⚙️ Hardware & Environment

* **Python Version**: `Python 3.9+`[cite: 6]
* **Compute Target**: NVIDIA GPU with $\ge 12\text{GB}$ VRAM (Google Colab T4 environment used)[cite: 5, 6]
* **Core Libraries**: PyTorch, Hugging Face `diffusers`, `torchvision`, `scikit-learn`, `scipy`, `numpy`, `nibabel`, `PIL`, `pandas`[cite: 5, 6]

---

## 📥 External Pretrained Weights & Resources

* **Generative Base Weights**: `benetraco/brain_ddpm_128` (Hugging Face)[cite: 6]
* **Domain Feature Extractor**: RadImageNet ResNet50 weights (`Lab-Rasool/RadImageNet`)[cite: 5, 6]
* **Distance Matrix Computations**: `scipy.linalg.sqrtm`[cite: 5, 6]

---

## 🚀 Execution Guide

1. **Preprocessing (Optional)**
   Run `misc/preprocess- 3D to 2D coronal.py` to convert raw 3D OASIS-1 Analyze volumes into normalized 2D coronal PNG slices[cite: 6].

2. **DDPM Fine-Tuning & Generation**
   Run `DDPM coronal (linear).ipynb` sequentially to load slices, fine-tune the UNet backbone, generate synthetic samples, and compute standard FID scores[cite: 6].

3. **Noise Schedule Ablation**
   Run `Noise Schedule Ablation.ipynb` to evaluate generative performance across Cosine and Linear variance schedules[cite: 6].

4. **RadImageNet FID & Primary Classification**
   Run `RadnetFID+Classifier(linear).ipynb` to extract domain-adapted medical features, calculate RadImageNet FID, and train the RadImageNet-ResNet50 classifier[cite: 5, 6].

5. **Baseline Classifiers**
   Run `misc/CNN+Resnet18 classifie.ipynb` to execute baseline performance benchmarks on SimpleCNN and standard ResNet18[cite: 6].

---

## 🤖 AI Tool Usage Declaration

AI assistants (Google Gemini and Anthropic Claude) were utilized during development for code refactoring, PyTorch debugging, Hugging Face weight mapping (remapping RadImageNet parameters to torchvision models), noise ablation setups, and synthetic filtering logic[cite: 5, 6]. Specific prompts and scopes are documented in project headers and official academic coversheets[cite: 6].