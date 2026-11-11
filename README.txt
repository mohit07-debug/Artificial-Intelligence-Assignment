# Classical AI Reasoning Agent

## 1. Project Overview

This project implements a general-purpose AI reasoning agent that determines whether a given statement is logically entailed by a knowledge base.

The system follows the pipeline:

Natural Language → Internal Representation → Classical Reasoning → True/False

It uses three classical reasoning engines for RuleTaker, CounterBench, and FOLIO. The final predictions are generated using rule-based and logical reasoning techniques, not direct generative AI predictions.

## 2. Submission Files

The submission folder contains the following files:

- `reasoning_agent.ipynb` – Complete Python implementation, including natural language parsing, reasoning engines, dataset evaluation, and submission generation.
- `report.pdf` – Report describing the system architecture, reasoning algorithms, experiments, and reasoning examples.
- `submission.csv` – CSV file containing prediction IDs and predicted labels.
- `README.txt` – Project description and execution instructions.

**Note:** The currently generated `submission.csv` contains predictions on the public RuleTaker test split for demonstration. It is not a prediction file for the instructor's private evaluation dataset.

## 3. Installation Requirements

Install the required Python packages:

```bash
pip install datasets pandas huggingface_hub
```

The notebook also uses standard Python libraries and NumPy, which is installed as a dependency where required.

## 4. How to Run

1. Open `reasoning_agent.ipynb` in Google Colab or Jupyter Notebook.
2. Install the required packages.
3. Run all notebook cells sequentially, from top to bottom.
4. Complete Hugging Face authentication when prompted. FOLIO is a gated dataset, so access must be accepted on its Hugging Face page before loading it.
5. The notebook loads the public datasets, evaluates the reasoning engines, and prints accuracy and execution time.
6. The final section generates `submission.csv`.

### Using an Evaluation CSV

When an instructor-provided evaluation CSV becomes available, set its path in the final submission-generation cell:

```python
TEST_PATH = "/path/to/evaluation.csv"
OUTPUT_PATH = "submission.csv"
MODE = "cwa"
```

The evaluation adapter supports these input formats:

- RuleTaker: `context` and `statement` (or `query` / `question`)
- CounterBench: `given_info` and `question`
- FOLIO: `premises` and `conclusion`
- Supplied first-order logic: corresponding premises and conclusion FOL columns

An `id` column is used when available. Otherwise, the notebook generates sequential IDs.

The `MODE` setting controls the RuleTaker reasoning mode:

- `cwa` – Closed World Assumption, using negation as failure.
- `owa` – Open World Assumption, using explicit negation.

The current notebook setting is `cwa`.

The generated CSV contains:

- `id` – Query identifier.
- `label` – Predicted logical label (`True` or `False`).

## 5. Datasets Used

The system is developed and evaluated using the following public Hugging Face datasets:

1. **RuleTaker** – `Jise/ruletaker`
2. **CounterBench** – `CounterBench/CounterBench`
3. **FOLIO** – `yale-nlp/FOLIO`

## 6. Reasoning Algorithms

### RuleTaker

- Rule-based natural language parser.
- Horn clause representation with facts and rules.
- Stratified forward chaining.
- Unification.
- Negation as failure under CWA and explicit negation under OWA.
- Derived facts are cached for repeated queries involving the same context and reasoning mode.

### CounterBench

- Structural causal model representation.
- Abduction to infer relevant causal information.
- Intervention to modify causal variables.
- Forward inference to determine the resulting outcome.

### FOLIO

- First-order logic representation.
- Conversion into clause form.
- Skolemization.
- Unification and factoring.
- Resolution refutation using a set-of-support strategy.

A unified solver selects the appropriate reasoning engine based on the input format and knowledge-base structure.

## 7. Important Notes

- All final predictions are produced using classical reasoning algorithms.
- No generative AI model is used to directly generate True/False answers.
- The public datasets are used for development and evaluation.
- The instructor's private evaluation dataset is not included or used during development.
- Run the notebook from beginning to end to reproduce the public experiments and generate the demonstration CSV.