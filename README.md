---
title: LLM Benchmarking Dashboard
emoji: 🤖
colorFrom: blue
colorTo: green
sdk: gradio
sdk_version: "5.9.1"
app_file: app.py
pinned: false
---

# LLM Benchmarking Dashboard

**RV College of Engineering | Department of AI & ML | Course: AI364TA**

Benchmarks three open-source Large Language Models on three NLP tasks, deployed entirely on free cloud infrastructure.

---

## Models Compared

| Model | Parameters | Organization |
|---|---|---|
| LLaMA 3.2-3B-Instruct | 3B | Meta |
| Falcon-7B-Instruct | 7B | TII (UAE) |
| Mistral-7B-Instruct-v0.2 | 7B | Mistral AI |

## Tasks & Metrics

| Task | Metric |
|---|---|
| Summarization | ROUGE-1, ROUGE-2, ROUGE-L |
| Translation (English → French) | BLEU Score |
| Reasoning (Logic & Math) | Accuracy |
| All tasks | Latency (s), GPU Memory (MB), Tokens/sec |

---

## Cloud Architecture

```
VS Code (Local)
      │ git push
      ▼
GitHub (abhip-10/llm-benchmarking) ──► GitHub Actions ──► HuggingFace Spaces (this app)
                                                                    ▲
Google Colab (T4 GPU)  ──────────────────────────────────────────────
  └─ Runs model inference                      │ pushes results
  └─ LLaMA · Falcon · Mistral                  ▼
                                    HuggingFace Datasets Hub
                                    (abhinavp10/llm-benchmark-results)
                                               │ logs
                                               ▼
                                    Weights & Biases
                                    (rvce_abhi-potharaju)
```

## How to Use

1. **Run benchmarks**: Open the [Colab notebook](https://github.com/abhip-10/llm-benchmarking/blob/main/colab_benchmark.ipynb), select T4 GPU runtime, and click Run All
2. **View results**: Click **Refresh Results** on this dashboard to load the latest benchmark data
3. **Track experiments**: View detailed logs at [wandb.ai/rvce_abhi-potharaju](https://wandb.ai/rvce_abhi-potharaju)

## Links

- GitHub Repository: https://github.com/abhip-10/llm-benchmarking
- Benchmark Results Dataset: https://huggingface.co/datasets/abhinavp10/llm-benchmark-results
- W&B Experiment Tracking: https://wandb.ai/rvce_abhi-potharaju/llm-benchmarking

---

*RV College of Engineering | Department of Artificial Intelligence and Machine Learning*
