# GAN–CNN Hybrid Image Generation

> **Project brief · Research and learning prototype**  
> A notebook-based exploration of adversarial image generation using convolutional neural networks.

## At a glance

| | |
|---|---|
| **Project** | GAN With CNN Hybrid 16 |
| **Implementation** | TensorFlow / Keras in a Jupyter notebook |
| **Primary components** | Convolutional generator and discriminator |
| **Current image target** | 64 × 64, single-channel grayscale (as configured in the notebook) |
| **Latent input** | 100-dimensional random noise |
| **Training configuration** | 50 epochs; batch size 256 (configurable) |
| **Status** | Educational prototype; run and validate with a prepared dataset before drawing performance conclusions |

## Project overview

This project demonstrates the core training loop of a Generative Adversarial Network (GAN). A **generator** maps random latent vectors to synthetic images. A **discriminator**, built from convolutional layers, learns to distinguish training examples from generated samples. During training, the generator learns to produce outputs that increasingly challenge the discriminator.

The notebook is designed as a hands-on starting point for exploring CNN-based image generation, adversarial objectives, training behavior, and visual inspection of generated samples. It is not presented as a benchmark or as evidence of production-ready image quality.

## How the system works

1. **Prepare image data.** Supply `x_train` as a NumPy array with image dimensions and channels compatible with the models. The notebook expects images normalized to the `[-1, 1]` range for its `tanh` generator output.
2. **Generate candidates.** The generator transforms random vectors of length `LATENT_DIM` into images.
3. **Score real and generated images.** The CNN discriminator produces a logit for each input image.
4. **Update both networks.** Binary cross-entropy losses and separate Adam optimizers drive adversarial training.
5. **Inspect progress.** A fixed set of latent vectors is used to produce periodic image grids, making changes across checkpoints easier to compare.
6. **Save the generator.** The notebook saves the trained generator under `saved_models/`.

## Repository entry point

- [`GAN_With_CNN_HYBRID16.ipynb`](../GAN_With_CNN_HYBRID16.ipynb) — model definitions, training code, sample visualization, and generator saving.

## Getting started

1. Open the notebook in Jupyter or Google Colab.
2. Install TensorFlow, NumPy, and Matplotlib in the active environment.
3. Load or define a dataset as `x_train` **before** the dataset-preparation cell.
4. Verify the images' shape, channel count, numeric type, and normalization.
5. Confirm the generator output shape matches the training images, then run cells in order.
6. Review saved sample grids and generator/discriminator losses; repeat experiments with documented settings.

Example environment setup:

```bash
pip install tensorflow numpy matplotlib notebook
jupyter notebook GAN_With_CNN_HYBRID16.ipynb
```

## Important implementation notes

- The notebook's configured output is 64 × 64 grayscale. Its generator and discriminator must agree with the dataset dimensions. Changing only `target_image_shape` after building the models does not rebuild those models; configure the target dimensions before model construction.
- The dataset cell refers to `x_train`; it does not download or load a dataset by itself. Define the dataset first.
- Images should be converted to floating point and normalized to `[-1, 1]` to align with the generator's `tanh` output.
- The training step samples `BATCH_SIZE` noise vectors. Ensure the actual final batch has that size (for example, use `drop_remainder=True`) or adapt the training step to use the current batch size.
- A GAN loss value alone is not a quality metric. Inspect generated samples and record the dataset, preprocessing, configuration, and checkpoints when comparing runs.
- Training can be resource-intensive. Start with a small experiment to confirm the pipeline works before running the full epoch count.

## Suggested experiment record

For each run, note:

- Dataset source, license, split, and preprocessing
- Image height, width, channels, and normalization
- Latent dimension, batch size, epoch count, and optimizer settings
- Hardware and framework versions
- Generator/discriminator loss history
- Sample grids at consistent checkpoints
- Known limitations, failures, and next changes

## Responsible use

Use datasets you have permission to use, retain their attribution and license information, and review generated outputs for memorization, bias, or misleading use. Clearly label synthetic images where their origin could otherwise be misunderstood.

## Project article

This page is a polished, Notion-ready project brief stored in the repository as Markdown. Import or paste it into Notion if you want a live Notion page; this repository does not currently have a Notion publishing integration.
