# Artificial Intelligence Assignment
## A Classical AI Reasoning Agent for RuleTaker, CounterBench and FOLIO

A Python-based Classical AI Reasoning Agent that converts natural-language knowledge bases into logical representations and answers queries using classical reasoning algorithms. The system implements Forward Chaining, Unification, Structural Causal Models, Abduction, Intervention, and First-Order Logic Resolution to solve reasoning tasks across three benchmark datasets.

---

## Project Overview

The objective of this assignment is to develop a classical AI reasoning system capable of understanding facts, rules, logical relationships, and causal dependencies from natural-language knowledge bases.

The agent processes a knowledge base and a query, converts the input into an internal logical representation, selects an appropriate reasoning engine, and generates a final True/False prediction.

The implementation uses classical symbolic reasoning techniques rather than relying on generative AI to directly produce final predictions.

## Datasets

This project uses three public benchmark datasets:

1. **RuleTaker** – Natural-language reasoning using facts and logical rules.
2. **CounterBench** – Counterfactual reasoning using structural causal models.
3. **FOLIO** – First-Order Logic reasoning and logical entailment.

## Implemented Reasoning Engines

### 1. RuleTaker – Forward Chaining and Unification

- Converts natural-language facts and rules into logical representations.
- Represents knowledge using predicates, facts, and Horn clauses.
- Implements stratified forward chaining.
- Uses unification to match predicates and variables.
- Supports Negation as Failure (NAF) under the Closed-World Assumption (CWA).
- Implements explicit negation under the Open-World Assumption (OWA) in the relational reasoning engine.
- Uses premise counters and cached facts for efficient inference.

### 2. CounterBench – Structural Causal Models

- Represents causal relationships using Structural Causal Models (SCMs).
- Supports AND, OR, and NOT causal mechanisms.
- Implements backward abduction to infer possible causes.
- Handles interventions using the `do()` operator.
- Performs forward inference to evaluate counterfactual outcomes.
- Supports joint and nested interventions.

### 3. FOLIO – First-Order Logic Resolution

- Parses First-Order Logic formulas.
- Converts logical expressions into Conjunctive Normal Form (CNF).
- Implements implication elimination and negation normal form conversion.
- Performs Skolemization and clause generation.
- Implements unification with occurs check.
- Uses binary resolution, factoring, and set-of-support search.
- Includes a rule-based Natural Language to First-Order Logic translator.
- Supports True, False, and Uncertain reasoning.

## System Architecture

The reasoning pipeline consists of the following stages:

1. **Input Processing:** Receives a natural-language knowledge base and query.
2. **Logical Representation:** Converts input statements into facts, rules, predicates, or causal equations.
3. **Engine Selection:** Selects the appropriate reasoning engine based on the input structure.
4. **Classical Inference:** Executes the corresponding reasoning algorithm.
5. **Output Generation:** Produces the final prediction.

## Experimental Results

The following results were obtained using the implemented reasoning agent on public dataset splits.

| Dataset / Split | Reasoning Method | Accuracy |
|---|---|---:|
| RuleTaker Train (1000) | Forward Chaining | 98.30% |
| RuleTaker Test (250) | Forward Chaining | 97.60% |
| RuleTaker OOD Test (375) | Forward Chaining | 99.47% |
| CounterBench (1200) | Structural Causal Model | 94.58% |
| FOLIO Train (300) – Gold FOL | Resolution | 79.33% |
| FOLIO Validation (203) – Gold FOL | Resolution | 81.28% |
| FOLIO Validation (203) – NL to FOL | Resolution | 63.55% |

**Additional CounterBench results:**
- Default configuration: 94.58%
- Without "instead of" abduction: 91.67%
- With unknown root variables set to 1: 95.00%

**Note:** Gold FOL results evaluate the FOL reasoning engine using provided logical representations. Natural Language to FOL results additionally depend on the pattern-based translation component.

## Technologies and Tools

- Python
- Jupyter Notebook
- Hugging Face Datasets
- Regular Expressions
- Symbolic AI
- First-Order Logic
- Structural Causal Models
- Classical Inference Algorithms

## Repository Structure

```text
Artificial-Intelligence-Assignment/
│
├── reasoning_agent.ipynb
│
├── report.pdf
│
├── submission.csv
│
├── README.md
│
└── README.txt
```

## Installation and Execution

### 1. Clone the Repository

```bash
git clone https://github.com/mohit07-debug/Artificial-Intelligence-Assignment.git
```

### 2. Navigate to the Project Directory

```bash
cd Artificial-Intelligence-Assignment
```

### 3. Install Required Dependencies

```bash
pip install datasets pandas huggingface_hub
```

### 4. Open the Jupyter Notebook

```bash
jupyter notebook reasoning_agent.ipynb
```

Alternatively, open the notebook using Google Colab or JupyterLab.

### 5. Hugging Face Dataset Access

The FOLIO dataset may require access approval on Hugging Face.

- Visit the FOLIO dataset page: https://huggingface.co/datasets/yale-nlp/FOLIO
- Accept the dataset access conditions if required.
- Authenticate with your Hugging Face account when prompted.

### 6. Run the Notebook

Execute the notebook cells sequentially to:

- Load the public datasets.
- Parse knowledge bases and queries.
- Execute the three reasoning engines.
- Run sanity tests.
- Evaluate accuracy and inference time.
- Generate prediction outputs.

## Submission CSV

The repository includes `submission.csv` with two columns:

- `id`
- `label`

The currently included CSV contains 250 predictions generated using the public RuleTaker test split. It is a demonstration output and not a prediction file for the instructor's private evaluation dataset.

To generate predictions for another evaluation dataset, configure `TEST_PATH` in the notebook and execute the final submission cell.

## Limitations

- Natural-language parsing relies on predefined linguistic patterns.
- Unusual sentence structures and complex relationships may not be parsed correctly.
- CounterBench abduction does not explore every possible causal assignment.
- The FOLIO English-to-FOL translator has limited coverage.
- Resolution search is bounded by a time limit.

## Author

**Mohit Jalani**
**(M26MER004)**

M.Tech – Robotics

Indian Institute of Technology Jodhpur  
Jodhpur, Rajasthan, India

---

*Developed as part of an academic assignment on Classical Artificial Intelligence Reasoning.*
