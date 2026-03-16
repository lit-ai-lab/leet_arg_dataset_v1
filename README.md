# LEET-Arg: A Benchmark for Evaluating Legal Causal Reasoning in Large Language Models

LEET-Arg is a benchmark dataset derived from the Logical Reasoning section of South Korea's Legal Education Eligibility Test (LEET), designed to evaluate both **answer correctness** and **reasoning fidelity** of large language models. The dataset restructures 97 Inference and Argumentation questions (2021–2025) into 315 statement-level tasks, generating 2,205 model responses paired with expert-authored reasoning paths and LLM-as-a-Judge evaluations.

## Citation

If you use this dataset in your research, please cite:

```bibtex
@article{park2025leetarg,
  title={When Correct Isn't Enough: Deconstructing Legal Causal Reasoning Capability in Large Language Models},
  author={Park, Jeewon and Park, Sungmi},
  year={2026}
}
```
## Dataset Overview

LEET-Arg comprises two complementary JSON files:

| File | Description | Records |
|------|-------------|---------|
| `LEET_Arg_Questions.json` | Original LEET questions with expert-authored explanations | 97 questions |
| `LEET_Arg_Model_Responses.json` | Model responses and LLM-as-a-Judge evaluation results | 97 × 7 models |


## Dataset 1: Questions & Expert Rationales

**File:** `LEET_questions_rationales.json`

Each entry contains a LEET Logical Reasoning problem with its expert-authored explanation.

| Field | Type | Description |
|-------|------|-------------|
| `id` | string | Unique identifier (e.g., `"2021_01"`) |
| `year` | string | Exam year (`2021`–`2025`) |
| `problem_idx` | string | Problem number within the exam |
| `objective` | string | Assessment objective of the question |
| `domain` | string | Thematic domain: `Norms`, `Humanities`, or `Society` |
| `category` | string | Reasoning type (e.g., `Argumentation and Rebuttal`, `Argument Analysis`) |
| `answer` | string | Correct answer choice |
| `original_question` | string | Full question text including passage, prompt, and choices |
| `statements` | object | Individual statements extracted from the question (keys: `statement_1`, `statement_2`, …) |
| `original_rationale` | string | Expert-authored step-by-step reasoning explanation |

## Dataset 2: Model Responses & Judge Evaluations

**File:** `LEET_model_answers.json`

Each entry contains responses from seven frontier LLMs along with evaluation scores from two LLM judges.

| Field | Type | Description |
|-------|------|-------------|
| `id` | string | Matches the question ID in Dataset 1 |
| `year` | string | Exam year |
| `problem_idx` | string | Problem number |
| `answer` | string | Correct answer |
| `models` | object | Per-model response and evaluation data (see below) |

### Evaluated Models

| Key | Model |
|-----|-------|
| `claude_opus4` | Claude Opus 4 |
| `claude_sonnet4` | Claude Sonnet 4 |
| `deepseek_r1` | DeepSeek R1 |
| `gemini-2.5-pro` | Gemini 2.5 Pro |
| `o3` | OpenAI o3 |
| `o3-pro` | OpenAI o3-pro |
| `o4-mini` | OpenAI o4-mini |

### Per-Model Structure

Each model entry contains three objects:

| Field | Description |
|-------|-------------|
| `model_rationale` | The model's answer and reasoning — includes `model_answer`, `model_rationale_full`, and per-statement rationales (`model_rationale_for_statement_1`, …) |
| `gemini_rationale_eval` | Justification fidelity scores from **Gemini 2.5 Pro** judge — per-statement evaluations with score and rationale (`gemini_rationale_eval_1`, …) |
| `o3_rationale_eval` | Justification fidelity scores from **OpenAI o3** judge — per-statement evaluations with score and rationale (`o3_rationale_eval_1`, …) |
