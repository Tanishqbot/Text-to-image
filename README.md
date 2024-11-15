# Text to Image Generation

This repository contains code for a deep learning model combining UNet architecture and CLIP embeddings, designed for image generation tasks. The model is trained on the DeepFashion dataset using noisy image embeddings and text-based descriptions to generate fashion images.

![Text to Image Generation](./output.jpg)

## Structure

- DeepFashion Dataset: Utilizes the DeepFashion dataset to pair images with captions for training.
- VAE (Variational Autoencoder): A custom VAE model is used to encode images into latent space representations.
- Noisy Embeddings: Gaussian noise is added to the embeddings using a cosine schedule for image reconstruction tasks.
- UNet: A U-Net model is employed for generating output images from noisy embeddings.
- CLIP: A pre-trained CLIP model is used for text embedding extraction.
- Training Pipeline: The model is trained using the noisy embeddings and text-image pairs.

### Dataset

The project uses the DeepFashion dataset for image-text pairs. It is a large-scale dataset for fashion-related images, paired with their textual descriptions.

In addition, the Winoground Text-to-Image Dataset is used to generate noisy embeddings for training the VAE.

#### Data Preparation

**1. Sampling from DeepFashion Dataset:**

2000 images are randomly sampled from the DeepFashion dataset along with their corresponding captions.
These images are saved locally, and the image paths and captions are stored in a CSV file (sampled_images_captions.csv).

**2. VAE Encoding:**

Images from the Winoground Text-to-Image dataset are encoded using a custom VAE model (based on ResNet-18 architecture).
The VAE generates 128x128 embeddings for each image.

**3. Gaussian Noise Addition:**

The embeddings are perturbed by adding Gaussian noise using a cosine schedule to simulate a denoising process.

#### Sampled Data

The following data is used:

Images: Stored in the `downloaded_images` folder.
Captions: Stored in a CSV file (`sampled_images_captions.csv`).

### Models Used

**VAE (Variational Autoencoder)**

A custom VAE based on ResNet-18 is used for encoding images into 128x128 latent space representations. The encoder part of ResNet-18 is repurposed to output 128x128 embeddings, which are then used in the training pipeline.

**UNet**

The UNet model, which includes the encoder, bottleneck, and decoder blocks, is used for image reconstruction. The decoder is designed to take noisy embeddings and reconstruct the original images.

**CLIP**

The CLIP model is used to extract text embeddings. It is a pre-trained model that projects both images and text into a shared embedding space, making it ideal for tasks involving both modalities.

### Workflow

**1. Data Preparation**

**2. Image Reconstruction with Noisy Embeddings**

The training pipeline uses the noisy embeddings and captions to train the UNet model for reconstructing images. The model learns to map noisy embeddings to clean images using a loss function such as MSE.

**3. Loss Calculation and Optimization**

The training pipeline uses the noisy embeddings and captions to train the UNet model for reconstructing images. The model learns to map noisy embeddings to clean images using a loss function such as MSE.

**4. Final Output and Training**

After training, the model will be able to reconstruct images from noisy embeddings and text descriptions.

### Requirements

#### Dependencies

The following libraries are required for this project:

- `torch`
- `torchvision`
- `transformers`
- `datasets`
- `pandas`
- `numpy`
- `matplotlib`
- `PIL` (Python Imaging Library)

### Results

After training, the model will be able to generate reconstructed images from noisy embeddings. Additionally, you can visualize the embeddings and their noisy versions for analysis.

### Conclusion

This project integrates VAE for image encoding, CLIP for text embedding, and UNet for image reconstruction, providing a multimodal approach for image-text generation and denoising. You can explore further improvements by tuning the models, optimizing the training pipeline, or experimenting with different architectures
