# POWGAN - Policy‐Optimized WGAN for Molecule Generation

This repository provides the implementation of **POWGAN (Policy‐Optimized Wassertein Generative Adversarial Netowrk)**, a generative model designed to create novel quinoline-based molecules. POWGAN introduces an **adaptive reward scaling mechanism** to improve molecular graph connectivity while maintaining generative diversity.
This work is the development of MedGAN original work (https://www.nature.com/articles/s41598-023-50834-6), an Optimized Generative Adversarial Network with Graph Convolutional Networks for Novel Molecule Design. Now, integrating POWGAN algorithm, R-MedGAN is able to generate novel molecules with a reinforcement learning strategy.

## Key Features
- **Dynamic Reward Scaling**: Increases the reward weight stepwise when no improvement is observed for multiple epochs.
- **Baseline Reward for Non‐Connected Graphs**: Ensures molecules that are not fully connected still contribute to learning, preventing model collapse.
- **Stable Training with WGAN‐GP**: Uses Wasserstein loss with gradient penalty for improved convergence.
- **100k Quinolines Dataset**: Trains on a **100,000**-molecule subset from ZINC15. The full model runs on 1,000,000 molecule subset.

## System Requirements
To run the model, we used an **AWS g5.8xlarge** instance with the following specs:
- **GPU**: 1x NVIDIA A10G
- **vCPUs**: 32
- **RAM**: 128 GB
- **Storage**: 100 GB (recommended)

## Environment
A dockerfile is available on the repository.

## Dataset
The 100k quinoline dataset is included:
- data/non_duplicate_filtered_quinolines_zinc15_50atoms_100k.csv
Each row contains a SMILES string representing a filtered quinoline molecule.
The 100,000 saved graphs can be found on MedGAN repository (https://github.com/bmacedo111/MedGAN/tree/main/data/data_zinc15_subset-iii)

## CodeOcean run
The public capsule (DOI 10.24433/CO.0691778.v1) recreates the Docker image and launches on Code Ocean’s free Tesla T4 kernel. Because that kernel cannot accommodate the full 1 M-molecule run, the capsule bundles a 100 k-molecule subset plus the epoch-400 checkpoint.

R-MedGAN_model3_zinc15iii_RL_100k.ipynb loads the checkpoint, verifies that training has reached its final epoch, and re-saves the weights—demonstrating an end-to-end, error-free pass in under one minute.

R-MedGAN_model3_zinc15iii_RL_100k_example-runs.ipynb retrains 19 epochs on the subset so users can watch the accordion-style reward and connectivity curves rise; the matching TensorBoard log and a PNG snapshot of the metrics are included in /code.

## Implementation
### 1. R-MedGAN_WGAN-GP
- Create a `logs` folder for TensorBoard metrics (one for each model).
- Create a `training_checkpoints` directory to store each training step (one for each model).
- Create a `training_model` directory to store the model saved after training (one for each model).
- Create summaries for the generator and discriminator in both `.txt` and `.png` formats (one for each model).

### 2. R-MedGAN_generator
- Generate molecules for each model.
- Compute model performance metrics.

### 3. R-MedGAN_metrics
- TensorBoard allows to monitor metrics such as the reward (connectivity)

### 4. R-MedGAN_sample
- In the folder 'code' there is a jupyter notebook sample of a run for several epochs and the output print
- There is also a tensorboard logs image inside 'code' folder with the result for the initial example running epochs where is clear the growth of connected validity as the adaptative scaling progresses
