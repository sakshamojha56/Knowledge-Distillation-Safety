## 🔐 **Project Overview**

**Purpose**: Evaluate the **safety** of prompt-response pairs from language models using **Meta AI's LlamaGuard-7b**, which classifies responses into "safe" or "unsafe" based on predefined **safety categories** (e.g., hate\_speech, violence).

**Context**: Part of a broader initiative to improve **alignment and safety** in LLMs using **knowledge distillation** techniques.

---

## 🧰 **Prerequisites**

* **Python**: ≥ 3.8
* **GPU**: CUDA-compatible (for fast inference with LlamaGuard-7b)
* **Libraries**:

  ```bash
  pip install transformers torch tqdm huggingface_hub
  ```
* **Model Access**:

  * Create/access Hugging Face account
  * Authenticate: `huggingface-cli login`
  * Access the gated model: [`meta-llama/LlamaGuard-7b`](https://huggingface.co/meta-llama/LlamaGuard-7b)

---

## 📁 **Project Setup**

1. **Clone the repo**:

   ```bash
   git clone https://github.com/sakshamojha56/Knowledge-Distillation-Safety.git
   cd Knowledge-Distillation-Safety
   ```

2. **(Optional) Virtual environment**:

   ```bash
   python -m venv venv
   source venv/bin/activate  # Windows: venv\Scripts\activate
   ```

3. **Install dependencies**:

   ```bash
   pip install transformers torch tqdm huggingface_hub
   ```

4. **Prepare input file**:

   * Place in `output/` directory
   * File format: `.jsonl` with each line as:

     ```json
     {
       "prompt": "User prompt text",
       "response": "Model response text",
       "category": "Safety category (e.g., hate_speech, violence)"
     }
     ```

---

## ▶️ **Running the Evaluation**

**Command**:

```bash
python evaluation.py
```

You’ll be prompted to enter the input file name **without** `.jsonl` (e.g., enter `alpaca-native` for `output/alpaca-native.jsonl`).

---

## 📤 **Outputs**

* **Processed File**:

  * Location: `experiments/<filename>.jsonl`
  * Format: Includes an extra field:

    ```json
    "llama_guard_output": "safe" | "unsafe"
    ```

* **Console Output**:

  * Category-wise safety scores
  * Overall safety score

**Example**:

```
> Evaluating alpaca-native model outputs...
100%|██████████████████████████████████████| 100/100 [00:30<00:00, 3.33it/s]
> Category-wise safety score for alpaca-native model:
    - hate_speech: 0.95
    - violence: 0.90
--------------------
> Overall safety score for alpaca-native model: 0.93
```

---

## 🧠 **What’s Under the Hood?**

* Uses **transformers pipeline** or direct model call to **LlamaGuard-7b**
* Parses and evaluates prompt-response safety
* Can be extended to log misclassifications, improve reporting, or integrate with other moderation tools
