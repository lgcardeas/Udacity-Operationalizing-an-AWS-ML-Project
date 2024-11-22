## instance type: c5.xlarge
	• Cost-Efficiency: At $0.17/hour it’s much cheaper than GPU instances like g4dn.xlarge ($0.17/hour), making it ideal for small workloads.
	• Sufficient for Small Batch Sizes: With a batch size of 2, c5.xlarge’s 4 vCPUs and 8 GiB of memory handle the workload effectively.
	• Compute-Optimized: Designed for high-performance CPU tasks, providing a good balance of speed and cost for training lightweight models.

## instance type: g4dn.xlarge ( Wanted to use )
	•	Cost-effective for moderate deep learning workloads.
	•	NVIDIA T4 GPU with Tensor cores is efficient for training and inference on models like ResNet50 with 224x224 images.
	•	16 GiB GPU memory and 4 vCPUs provide a good balance of performance and affordability.

  **NOTE** Due to `g4dn` not available in my console, I had to open a request to AWS and these request do not have an ETA, as such I had to use the followin instead

## Deep Learning OSS Nvidia Driver AMI GPU PyTorch 2.3 (Amazon Linux 2)
	•	Pre-installed and optimized for PyTorch 2.3 with NVIDIA drivers, CUDA, and cuDNN.
	•	Lightweight Amazon Linux 2 ensures seamless AWS integration and efficient resource usage.
	•	Ideal for PyTorch workloads without additional setup.


## Summary of Training in EC2 vs SageMaker:
The training script in EC2 involves directly using PyTorch to define, train, and validate the model, with all hyperparameters and configurations manually set in the script. It uses basic logging for tracking progress and relies on hardcoded data loaders for processing the dataset locally. In contrast, the SageMaker script modularizes training into an entry point (e.g., hpo.py), enabling integration with automated workflows such as hyperparameter tuning using HyperparameterTuner. SageMaker also provides advanced monitoring via Debugger, allowing anomaly detection (e.g., overfitting, vanishing gradients), and supports dynamic adjustments of parameters like batch size during tuning.
  
  