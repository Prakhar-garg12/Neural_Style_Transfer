# 🎨 Neural Style Transfer

> Reimagine any photo as a painting — blend content with artistic style using deep learning.

[![Python](https://img.shields.io/badge/Python-3.8+-blue?logo=python&logoColor=white)](https://www.python.org/)
[![PyTorch](https://img.shields.io/badge/PyTorch-1.x-EE4C2C?logo=pytorch&logoColor=white)](https://pytorch.org/)
[![Flask](https://img.shields.io/badge/Flask-Web%20App-000000?logo=flask&logoColor=white)](https://flask.palletsprojects.com/)
[![License](https://img.shields.io/badge/License-MIT-green)](LICENSE)

---

## 📌 Overview

This project implements **Arbitrary Neural Style Transfer** — a deep learning technique that separates and recombines the *content* of one image with the *artistic style* of another. Built on top of a pre-trained **VGG encoder** and a custom **decoder**, the system uses **Adaptive Instance Normalization (AdaIN)** to achieve real-time, high-quality stylization.

A clean **Flask web interface** lets users upload their own content and style images, adjust the stylization strength (alpha), and instantly generate stylized artwork — no GPU required for inference.

---

## ✨ Features

- 🖼️ Upload any content image + style image via web UI
- 🎚️ Adjustable **alpha** parameter to control style intensity (0.0 → 1.0)
- ⚡ Real-time inference using pre-trained VGG encoder + trained decoder
- 🧠 Arbitrary style transfer — works with *any* style, not just trained ones
- 🌐 Fully deployable Flask web application (Heroku-ready with `Procfile`)
- 💻 CPU & GPU compatible

---

## 🏗️ Architecture

```
Content Image ──┐
                ├──► VGG Encoder ──► AdaIN ──► Decoder ──► Stylized Output
Style Image ────┘
```

The pipeline consists of three components:

| Component | Description |
|-----------|-------------|
| **VGG Encoder** | Pre-trained VGG-19 (normalised) used to extract content & style feature maps |
| **AdaIN Layer** | Adaptive Instance Normalization — aligns content feature statistics to style |
| **Decoder** | Custom-trained CNN that reconstructs the final stylized image from features |

The **alpha** parameter interpolates between content features and AdaIN output:

```
stylized_feats = α × AdaIN(content, style) + (1 - α) × content_feats
```

---

## 🗂️ Project Structure

```
Neural_Style_Transfer/
│
├── app.py                  # Flask web application (routes, inference pipeline)
├── train.py                # Decoder training script
│
├── utils/
│   ├── models.py           # VGGEncoder and Decoder model definitions
│   └── utils.py            # AdaIN, mean/std computation utilities
│
├── templates/
│   └── index.html          # Frontend UI template
│
├── static/uploads/         # Stores uploaded & generated images
├── content_data/           # Sample content images for training/testing
├── style_data/             # Sample style images for training/testing
├── examples/               # Pre-generated example outputs
├── experiment/             # Experimental notebooks/scripts
│
├── vgg_normalised.pth      # Pre-trained VGG encoder weights
├── decoder_final.pth       # Trained decoder weights
├── requirements.txt        # Python dependencies
├── runtime.txt             # Python runtime version
└── Procfile.txt            # Heroku deployment configuration
```

---

## 🚀 Getting Started

### Prerequisites

- Python 3.8+
- pip

### Installation

```bash
# Clone the repository
git clone https://github.com/Prakhar-garg12/Neural_Style_Transfer.git
cd Neural_Style_Transfer

# Install dependencies
pip install -r requirements.txt
```

### Run the Web App

```bash
python app.py
```

Then open your browser at `http://localhost:5000`

### Usage

1. Upload a **Content Image** (the photo you want to stylize)
2. Upload a **Style Image** (the artwork whose style you want to apply)
3. Set the **Alpha** value (0.0 = no style, 1.0 = full style transfer)
4. Click **Transfer Style** and download your result!

---

## 🖼️ Example Results

| Content | Style | Output (α=1.0) |
|---------|-------|----------------|
| Portrait photo | Van Gogh painting | Stylized portrait |
| Landscape | Kandinsky abstract | Stylized landscape |

*(See the `/examples` folder for pre-generated outputs)*

---

## 🧪 Training the Decoder

If you want to train the decoder from scratch:

```bash
python train.py
```

Training uses content images from `content_data/` and style images from `style_data/`. The encoder weights (`vgg_normalised.pth`) are frozen during training — only the decoder is learned.

---

## 📦 Dependencies

| Library | Purpose |
|---------|---------|
| `torch` / `torchvision` | Deep learning framework, image transforms |
| `flask` | Web framework |
| `flask-wtf` | Form handling & CSRF protection |
| `flask-bootstrap` | Frontend styling |
| `Pillow` | Image I/O and processing |
| `werkzeug` | Secure file uploads |

---

## 📄 Research References

This project is based on the following research papers:

1. **Arbitrary Style Transfer in Real-time with Adaptive Instance Normalization**  
   Huang & Belongie, ICCV 2017 — [arxiv.org/abs/1703.06868](https://arxiv.org/abs/1703.06868)

2. **A Neural Algorithm of Artistic Style**  
   Gatys et al., 2015 — [arxiv.org/abs/1508.06576](https://arxiv.org/abs/1508.06576)

3. **Instance Normalization: The Missing Ingredient for Fast Stylization**  
   Ulyanov et al., 2016 — [arxiv.org/abs/1603.08155](https://arxiv.org/abs/1603.08155)

4. **Perceptual Losses for Real-Time Style Transfer and Super-Resolution**  
   Johnson et al., 2016 — [arxiv.org/pdf/1409.1556](https://arxiv.org/pdf/1409.1556)

---

## 🤝 Contributing

Pull requests are welcome! For major changes, please open an issue first to discuss what you'd like to change.

---

## 👤 Author

**Prakhar Garg**  
[GitHub](https://github.com/Prakhar-garg12)

---

## 📜 License

This project is licensed under the [MIT License](LICENSE).

---

<p align="center">Made with ❤️ using PyTorch & Flask</p>
