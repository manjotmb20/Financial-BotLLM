# Development of a Comprehensive AI-Driven Financial Advisory System

# Objective: 

### This project aims to construct an advanced AI-driven system capable of providing real-time financial advice by leveraging a state-of-the-art Large Language Model (LLM) fine-tuned on proprietary financial Q&A datasets. The system is designed to be accessible and efficient, catering to users with varying hardware capabilities through the deployment of serverless GPU infrastructures.

### Components:

#### Training Pipeline:

  - Purpose:
1. To fine-tune an open-source LLM on a proprietary Q&A dataset.
Key Features:
2. Utilization of LLM for experiment tracking and inference result logging.
3. Deployment on serverless GPU infrastructure for enhanced accessibility.
● Streaming Real-time Pipeline:
Purpose:
● To ingest and process real-time financial news, converting them into embeddings
for enhanced model input.
Key Features:
● Automated deployment on AWS EC2 via a GitHub Actions-based CI/CD pipeline.
● Inference Pipeline:
Purpose:
● To provide real-time financial advice by enhancing user queries with context from
the latest financial news and historical interactions.
Key Features:
● Deployment as a RESTful API on a serverless infrastructure, ensuring scalability
and ease of use.

# Training / Fine-tuning Pipeline 



Training pipeline that:
- loads a  Q&A dataset 
- fine-tunes an open-source LLM using QLoRA
- logs the training experiments on [Comet ML's](https://www.comet.com?utm_source=thepauls&utm_medium=partner&utm_content=github) experiment tracker & the inference results on [Comet ML's](https://www.comet.com?utm_source=thepauls&utm_medium=partner&utm_content=github) LLMOps dashboard
- stores the best model on [Comet ML's](https://www.comet.com/site/products/llmops/?utm_source=thepauls&utm_medium=partner&utm_content=github) model registry

The **training pipeline** is **deployed** using [Beam](https://docs.beam.cloud/getting-started/quickstart?utm_source=thepauls&utm_medium=partner&utm_content=github) as a serverless GPU infrastructure.

# 1. Motivation

The best way to specialize an LLM on your task is to fine-tune it on a small Q&A dataset (~100-1000 samples) coupled to our business use case.

<br/>


# 2. Install

## 2.1. Dependencies

Main dependencies you have to install yourself:
* Python 3.10
* Poetry 1.5.1

Installing all the other dependencies is as easy as running:
```shell
make install
```

Prepare credentials:
```shell
cp .env.example .env
```

## 2.2. Beam
`deploy the training pipeline to Beam ` 

**First**, you must set up Beam, as explained in the .

In addition to setting up Beam, you have to go to your [Beam account](https://www.beam.cloud and create a volume, as follows:
1. go to the `Volumes` section
2. click create `New Volume` (in the top right corner)
3. choose `Volume Name = qa_dataset` and `Volume Type = Shared`

After, run the following command to upload the Q&A dataset to the Beam volume you created:
```shell
make upload_dataset_to_beam
```

**IMPORTANT NOTE:** The training pipeline will work only on CUDA-enabled Nvidia GPUs with ~16 GB VRAM. If you don't have one and wish to run the training pipeline, you must deploy it to [Beam](https://www.beam.cloud?utm_source=thepauls&utm_medium=partner&utm_content=github). 

# 3. Usage

## 3.1. Train  
`run the training, log the experiment and model to Comet ML`
