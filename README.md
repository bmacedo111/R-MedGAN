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
Despite codeocean not being able to use GPU to handle the graph processing, a jupyter notebook with this run is available with the outputs to check the evolution of reward. The starting point was epoch 400 for the lowest model (100,000 graphs). In this run is posible to monitor the increase in connectivity, the reward, when the adaptative scaling grows. A tensorboard log is available to check for the metrics.

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
