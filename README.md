Here’s a clean, professional **README template** for your GitHub repository — tailored for your Knowledge Graph assignment project.
It’s concise, easy to follow, and structured like a real-world data science repository.

---

# 🧠 Personality-Enriched Knowledge Graph (Hybrid LLM + spaCy)

A hybrid pipeline that extracts entities, relationships, and personality traits from unstructured text to build an interpretable **Knowledge Graph**.
This project combines **spaCy** for structured NLP extraction and an **LLM** for reasoning-based enrichment to produce a contextual, explainable graph of human interactions.

---

## 📄 **Table of Contents**

1. [Overview](#-overview)
2. [Project Structure](#-project-structure)
3. [Installation](#-installation)
4. [Usage](#-usage)
5. [Demo](#-demo)
6. [Report](#-report)
7. [Evaluation Metrics](#-evaluation-metrics)
8. [Results Preview](#-results-preview)
9. [Acknowledgements](#-acknowledgements)

---

## 🔍 **Overview**

This repository demonstrates a **Knowledge Graph generation workflow** for text documents that include personality traits.
It uses:

* **spaCy** for entity and relationship extraction
* **OpenAI GPT / LLM** for trait enrichment and inferred links
* **NetworkX** for graph construction and visualization

The resulting KG connects people, relationships, and personality attributes — structured for both **human interpretation** and **machine reasoning**.

---

## 📁 **Project Structure**

```
📦 knowledge-graph-challenge
 ┣ 📜 README.md
 ┣ 📜 requirements.txt
 ┣ 📜 report.md
 ┣ 📜 Knowledge Graph.ipynb
 ┣ 📜 synthetic_data.txt
 ┗ 📂 outputs/
    ┣ triplets.csv
    ┣ evaluation_metrics.csv
    ┗ graph.png

```

---

## ⚙️ **Installation**

### **1. Clone the repository**

```bash
git clone https://github.com/yourusername/personality-kg.git
cd personality-kg
```

### **2. Create and activate a virtual environment**

```bash
python -m venv venv
source venv/bin/activate   # on macOS/Linux
venv\Scripts\activate      # on Windows
```

### **3. Install dependencies**

```bash
pip install -r requirements.txt
```

**Dependencies include:**

* `spacy` – NLP entity and relationship extraction
* `networkx` – Graph creation and visualization
* `matplotlib` – Drawing graphs
* `openai` – Accessing LLM enrichment (optional)
* `pandas`, `regex`, `json` – Data manipulation

*(You can also run the demo notebook without the OpenAI API by skipping the enrichment step.)*

---

## ▶️ **Usage**

### **1. Run extraction with spaCy**

```bash
python extract_spacy.py
```

* Loads text from `synthetic_data.txt`
* Outputs base relationships (`triples_spacy.json`)

### **2. Run enrichment with LLM**

```bash
python enrich_llm.py
```

* Uses the OpenAI API to identify personality traits and implied links
* Outputs enriched triples (`triples_enriched.json`)

### **3. Build and visualize the Knowledge Graph**

```bash
python build_graph.py
```

* Creates a NetworkX graph from enriched triples
* Saves visualization to `/visuals/knowledge_graph.png`
* Optional: Exports `.graphml` file for Neo4j

### **4. Evaluate graph quality**

```bash
python evaluate_metrics.py
```

* Computes metrics: **Precision**, **Entity Coverage**, **Connectivity**
* Prints a short summary to the console

---

## 🎬 **Demo**

You can also open the **Knowledge Graph Notebook** in Jupyter Notebook:

```bash
jupyter notebook Knowledge Graph.ipynb
```

Inside the notebook:

* Run cells sequentially to generate the KG.
* View visual graphs and evaluation metrics inline.
* Optionally test new sentences or personality adjectives.

---

## 🧾 **Report**

The full written report is available here:
📄 [`report`](./report.md)

The report includes:

* Abstract and background
* Workflow explanation
* Personality representation schema
* Evaluation metrics
* Results, insights, and limitations

You can cite the report as part of your documentation or share it with interview panels.

---

## 📊 Evaluation Metrics

| Metric                        | Purpose                                         | Result |
| ------------------------------ | ----------------------------------------------- | ------- |
| **Precision**                  | Percentage of correctly extracted triples       | 0.67 |
| **Recall**                     | Percentage of all true triples successfully found | 1.00 |
| **F1-score**                   | Harmonic mean of precision and recall (balance) | 0.80 |
| **Entity Coverage**            | Proportion of entities from the text captured in the graph | 1.00 |
| **Connectivity (avg degree)**  | Average number of connections per node in the graph | 1.75 |

All metrics can be recomputed by re-running the evaluation cell or script `evaluate_metrics.py`.

## 🖼 **Results Preview**

### Example Triples

```json
[
  {"subject": "Alice", "relation": "is_friends_with", "object": "Bob"},
  {"subject": "Alice", "relation": "has_trait", "object": "kind"},
  {"subject": "Bob", "relation": "works_with", "object": "Carol"},
  {"subject": "Carol", "relation": "has_trait", "object": "confident"}
]
```

### Example Visualization

📍 **Output file:** `outputs/graph.png`
Displays nodes (people and traits) and directional edges (relationships).

---

## 💡 **Tips**

* For larger datasets, chunk text into paragraphs before running LLM enrichment.
* Store results in `.graphml` or `.json` for compatibility with **Neo4j** or **GraphDB**.
* Use environment variables for your OpenAI API key:

  ```bash
  export OPENAI_API_KEY="your_api_key_here"
  ```

---

## 🙌 **Acknowledgements**

This project was developed as part of a take-home data science assignment on **Knowledge Graph Construction using LLMs**.
Concepts, workflows, and documentation were created with iterative guidance from an **LLM (GPT-5)** for research reasoning and report generation.

---

### 📬 Contact

**Author:** Mishane Vishmika Perera
**Email:** [[mishane1998@gmail.com](mailto:your.email@example.com)]
**Location:** Colombo, Sri Lanka

---
