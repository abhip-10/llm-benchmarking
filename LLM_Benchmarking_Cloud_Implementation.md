# LLM Benchmarking on Cloud — Logic, Implementation & Rubric Mapping
### Course: Cloud Computing Technology and Architectures (AI364TA)
### Department of Artificial Intelligence and Machine Learning — RV College of Engineering

---

## 1. Project Overview

This project benchmarks open-source Large Language Models (LLaMA, Falcon, Mistral) on three NLP tasks — summarization, translation, and reasoning — and deploys the entire pipeline on cloud infrastructure using HuggingFace, GitHub CI/CD, and VS Code as the development environment.

---

## 2. Tools and Platforms

| Tool | Purpose | Cost |
|---|---|---|
| VS Code | Development IDE | Free |
| GitHub | Code repository + CI/CD trigger | Free |
| HuggingFace Spaces | Cloud app hosting and deployment | Free |
| HuggingFace Hub | Model registry (LLaMA, Falcon, Mistral) | Free |
| HuggingFace Datasets | Cloud storage for benchmark results | Free |
| Weights & Biases | Experiment tracking and MLOps | Free tier |
| Streamlit | Frontend dashboard framework | Free |
| ZeroGPU (HuggingFace) | Free GPU compute for inference | Free |

**Total Cost — Zero**

---

## 3. Cloud Architecture

```
┌─────────────────────────────────────────────────────┐
│                   DEVELOPER LAYER                   │
│         VS Code (Local IDE — No Heavy Compute)      │
└──────────────────────┬──────────────────────────────┘
                       │ Git Push
                       ▼
┌─────────────────────────────────────────────────────┐
│                 CI/CD PIPELINE LAYER                │
│     GitHub Repository → Auto Sync to HuggingFace   │
│         Every push triggers automatic redeploy      │
└──────────────────────┬──────────────────────────────┘
                       │ Auto Deploy
                       ▼
┌─────────────────────────────────────────────────────┐
│                  COMPUTE LAYER (CLOUD)              │
│         HuggingFace Spaces + ZeroGPU                │
│   Runs model inference on HuggingFace cloud servers │
│   Models: LLaMA 3.2 | Falcon-7B | Mistral-7B        │
└──────────────────────┬──────────────────────────────┘
                       │ Load Models
                       ▼
┌─────────────────────────────────────────────────────┐
│                MODEL REGISTRY LAYER                 │
│              HuggingFace Hub                        │
│   Versioned open-source models pulled at runtime    │
└──────────────────────┬──────────────────────────────┘
                       │ Save Results
                       ▼
┌─────────────────────────────────────────────────────┐
│                  STORAGE LAYER (CLOUD)              │
│            HuggingFace Datasets                     │
│   Benchmark scores, latency, memory usage stored    │
└──────────────────────┬──────────────────────────────┘
                       │ Display
                       ▼
┌─────────────────────────────────────────────────────┐
│                  OUTPUT LAYER                       │
│      Streamlit Dashboard — Public URL               │
│  https://huggingface.co/spaces/username/llm-bench   │
│   Live charts, model comparison, metric tables      │
└─────────────────────────────────────────────────────┘
```

---

## 4. MLOps Pipeline

```
Code Written in VS Code
        │
        ▼
Push to GitHub (Version Control)
        │
        ▼
GitHub Actions syncs to HuggingFace Space (CI/CD)
        │
        ▼
HuggingFace rebuilds environment from requirements.txt
        │
        ▼
App deployed at public URL automatically
        │
        ▼
Benchmark runs logged to Weights & Biases (Experiment Tracking)
        │
        ▼
Results stored in HuggingFace Datasets (Data Versioning)
        │
        ▼
Model versions tracked on HuggingFace Hub (Model Registry)
```

---

## 5. Benchmarking Logic

### 5.1 Models Compared

| Model | Parameters | Type |
|---|---|---|
| LLaMA 3.2 | 3B | Meta open-source |
| Falcon-7B | 7B | TII open-source |
| Mistral-7B | 7B | Mistral AI open-source |

### 5.2 Tasks Benchmarked

**Summarization**
- Input a long paragraph
- Each model generates a summary
- Evaluated using ROUGE score

**Translation**
- Input English text
- Each model translates to target language
- Evaluated using BLEU score

**Reasoning**
- Input a logical or mathematical question
- Each model generates an answer
- Evaluated using accuracy and response quality

### 5.3 Metrics Collected

| Metric | What It Measures |
|---|---|
| ROUGE Score | Summarization quality |
| BLEU Score | Translation accuracy |
| Accuracy | Reasoning correctness |
| Latency (seconds) | Time taken for inference |
| Memory Usage (MB) | Computational resource consumption |
| Tokens per Second | Inference speed |

### 5.4 Computational Resource Analysis

Each model run logs the following for fine-tuning and inference comparison:

- GPU memory consumed during inference
- Time to first token generated
- Total inference time
- Estimated cost if run on paid cloud GPU

This directly satisfies the activity objective of analyzing computational resources required for fine-tuning and inference.

---

## 6. Implementation Steps

### Step 1 — Setup VS Code

```
Install VS Code
Install Python Extension
Install GitHub Extension
Sign in to GitHub
Clone your GitHub repository locally
```

### Step 2 — Project File Structure

```
llm-benchmarking/
│
├── app.py                  # Main Streamlit application
├── benchmark.py            # Benchmarking logic and scoring
├── models.py               # Model loading from HuggingFace Hub
├── metrics.py              # ROUGE, BLEU, accuracy calculations
├── requirements.txt        # All Python dependencies
├── README.md               # Project documentation
└── .github/
    └── workflows/
        └── deploy.yml      # GitHub Actions CI/CD workflow
```

### Step 3 — requirements.txt

```
transformers
torch
streamlit
datasets
evaluate
rouge-score
sacrebleu
pandas
matplotlib
plotly
accelerate
wandb
```

### Step 4 — GitHub Actions CI/CD (deploy.yml)

```yaml
name: Sync to HuggingFace

on:
  push:
    branches: [main]

jobs:
  sync:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v3
      - name: Push to HuggingFace
        env:
          HF_TOKEN: ${{ secrets.HF_TOKEN }}
        run: |
          git remote add hf https://username:$HF_TOKEN@huggingface.co/spaces/username/llm-benchmarking
          git push hf main --force
```

Every push to GitHub main branch automatically deploys to HuggingFace Spaces.

### Step 5 — Deploy on HuggingFace

```
Create account on huggingface.co
Create new Space
Choose Streamlit as SDK
Enable ZeroGPU in Space settings
Add HF_TOKEN secret to GitHub repository settings
Push code — deployment is automatic
```

---

## 7. Team Responsibilities

| Member | Responsibility |
|---|---|
| Member 1 | Benchmarking logic, metrics calculation (benchmark.py, metrics.py) |
| Member 2 | Streamlit dashboard UI and charts (app.py) |
| Member 3 | GitHub repository, CI/CD pipeline setup (deploy.yml) |
| Member 4 | HuggingFace Space configuration, MLOps, Weights & Biases integration |

---

## 8. Rubric Mapping — Activity 1 (10 Marks)

### Rubric 1 — Cloud Deployment and Execution (3 Marks) | CO4

**What is required for Excellent (3 Marks):**
Application successfully deployed and fully executed on cloud infrastructure with live demonstration.

**How this project achieves it:**
The Streamlit app is hosted on HuggingFace Spaces which runs on HuggingFace cloud servers. Model inference for LLaMA, Falcon, and Mistral executes on ZeroGPU cloud GPU. Nothing runs locally during demonstration. The public URL proves live cloud execution. Evaluators can open the URL and run benchmarks in real time.

---

### Rubric 2 — Use of Cloud Services (3 Marks) | CO2

**What is required for Excellent (3 Marks):**
Effective use of multiple cloud services such as compute, storage, database, networking, or deployment tools.

**How this project achieves it:**

| Cloud Service | How It Is Used |
|---|---|
| HuggingFace Spaces | Cloud compute and app hosting |
| HuggingFace Hub | Model registry and versioning |
| HuggingFace Datasets | Cloud storage for benchmark results |
| ZeroGPU | Cloud GPU for model inference |
| GitHub | CI/CD pipeline and code hosting |
| Weights & Biases | Experiment tracking and monitoring |

Six distinct cloud services used across compute, storage, deployment, and monitoring layers.

---

### Rubric 3 — Cloud Architecture and Design (2 Marks) | CO3

**What is required for Excellent (2 Marks):**
Clear architecture diagram showing proper integration of cloud components and services.

**How this project achieves it:**
The architecture has five clearly defined layers — Developer, CI/CD, Compute, Storage, and Output — each mapped to a specific cloud service. The diagram shows data flow from code push to live deployment. All components interact through cloud services with no local dependencies during runtime.

---

### Rubric 4 — Demonstration and Team Communication (2 Marks) | CO5

**What is required for Excellent (2 Marks):**
Clear explanation of deployment process and architecture with participation from all team members.

**How this project achieves it:**
Each team member owns one layer of the architecture and explains it during demonstration. The CI/CD pipeline can be shown live by making a small code change, pushing to GitHub, and showing the automatic redeployment on HuggingFace within seconds. The public URL makes the demo instantly accessible to evaluators.

---

## 9. Live Demonstration Script

**Member 1** opens the public HuggingFace Spaces URL and shows the live app running on cloud

**Member 2** runs a live benchmark — enters text, selects models, shows results and charts

**Member 3** makes a small code change in VS Code, pushes to GitHub, shows CI/CD triggering and redeployment in real time

**Member 4** opens Weights & Biases dashboard showing logged experiments and model metrics

---

## 10. Deliverables Checklist

- [ ] Architecture Diagram showing all five layers and cloud services
- [ ] Deployment Summary: HuggingFace Spaces + GitHub CI/CD + ZeroGPU
- [ ] GitHub Repository Link with CI/CD workflow file
- [ ] Live Public URL for demonstration
- [ ] Weights & Biases experiment tracking dashboard
- [ ] Benchmark results comparing LLaMA, Falcon, and Mistral

---

## 11. Key Points for Evaluation

This project satisfies the not acceptable criteria check from the rubric guidelines:

- Code is not only pushed to GitHub — GitHub is only the CI/CD trigger
- Models are not stored locally — pulled from HuggingFace Hub at runtime
- Application does not run locally — all compute is on HuggingFace cloud servers

This project meets every acceptable implementation criteria:

- Application hosted on cloud platform (HuggingFace Spaces)
- Machine learning models deployed on cloud compute (ZeroGPU)
- Cloud storage used within architecture (HuggingFace Datasets)
- CI/CD pipeline for automated deployment (GitHub Actions)

---

*RV College of Engineering | Department of AI and ML | Course AI364TA*
