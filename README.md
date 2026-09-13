**Project Code Repository**
This repository contains the Python scripts and Jupyter notebooks used to preprocess the OASIS-1 MRI dataset, fine-tune the DDPM generative model, calculate evaluation metrics (FID), and train downstream classifiers.

Note: Due to file size limitations, the fine-tuned model weights and the raw and preprocessed MRI datasets are stored in cloud storage and are not included directly in this zip file.

• **Main Notebooks/code:** (using google collab)
**1. DDPM coronal (linear).ipynb**
This is the main project notebook. It contains the code for fine-tuning the 2D DDPM model using a linear noise schedule. It also includes the synthetic image generation pipeline, the correlation study, and the FID score calculations.


**2. Noise Schedule Ablation.ipynb**
This notebook contains the code for the noise schedule ablation experiment. It compares generated output quality and calculates FID scores across three distinct setups: Cosine (T=1000), Linear (T=1000), and Cosine (T=500).

**3. RadnetFID+Classifier(linear).ipynb**
This notebook handles the domain-specific evaluation and classification experiments. It computes the FID scores using RadImageNet feature extractions and trains/evaluates the main RadImageNet-pretrained ResNet50 classifier across the baseline and augmented dataset configurations.


• **Misc folder/codes** 
**4. preprocess- 3D to 2D coronal.py** (local python file)
A utility script used to load the raw 3D T1-weighted OASIS-1 volumes registered in T88 space, slice them along the coronal plane (y=95 to y=115), apply min-max intensity normalization, and save the extracted 2D cross-sections as PNG files.

**5. CNN+Resnet18 classifie.ipynb**
Contains the baseline classification code for evaluating dataset configurations using the simpler SimpleCNN and standard ImageNet-pretrained ResNet18 architectures.

• **Enviornment**: Python 3.9+ and the required dependencies specified in code files, A CUDA-enabled GPU (NVIDIA GPU with at least 12GB VRAM recommended) is required to run the fine-tuning, image generation, and classification training notebooks within a reasonable timeframe.

• Publicly available libraries and pre-trained weights were integrated as follows:

Hugging Face Diffusers & PyTorch: The DDPM implementation relies on diffusers.UNet2DModel and diffusers.DDPMScheduler.
Pre-trained Weights: The base model was initialized using generic brain MRI DDPM weights (benetraco/brain_ddpm_128) hosted on Hugging Face.
RadImageNet Feature Extractor: The domain-specific FID calculations and ResNet50 classifier utilize pre-trained RadImageNet weights (RadImageNet-ResNet50-PyTorch).
SciPy & NumPy: Fréchet distance calculation relies on matrix square root functions from scipy.linalg (sqrtm) and matrix utilities from numpy.

• **How to run code:**
1. Preprocessing (Optional):
If working from raw OASIS-1 3D Analyze volumes files, run the preprocessing script to generate 2D coronal slices
2.  Main DDPM Fine-Tuning & Generation:
Open and run DDPM coronal (linear).ipynb sequentially. This notebook loads the 2D slices, fine-tunes the UNet model using a linear noise schedule, generates synthetic samples, and computes standard FID scores.
3.  Ablation Study:
To reproduce the noise schedule ablation experiments, run Noise Schedule Ablation.ipynb. This tests performance across Cosine (T=500,T=1000) and Linear (T=1000) parameters.
4.  RadImageNet FID & Primary Classification:
Run RadnetFID+Classifier(linear).ipynb to compute domain-adapted RadImageNet FID metrics and train the primary ResNet50 classifier across Configurations
5.  Baseline Classifiers (Misc):
Run misc/CNN+Resnet18 classifie.ipynb to train and evaluate the alternative SimpleCNN and standard ImageNet ResNet18 models.

• **Documentation of AI Tool Usage**
• AI Assistance: Google Gemini and Anthropic Claude were used during this project. Claude provided assistance with debugging PyTorch scripts and assisting pre-trained model implementations, filter for generation of synthetic image, Loading weights from Huggingface for Radnetimage to local ResNet50 and refining code for variations in ablation study.

• Documentation Location: Detailed declarations regarding AI tool usage, specific prompts, and scope of assistance are recorded in the code files and AI Declaration section of the official coversheet submitted alongside this repository.