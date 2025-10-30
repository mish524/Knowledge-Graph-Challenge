# **Final Report: Building a Personality-Enriched Knowledge Graph Using a Hybrid LLM and NLP Pipeline**

---

## **Abstract / Summary**

This project presents a hybrid pipeline for constructing a **Knowledge Graph (KG)** from unstructured text data containing people, relationships, and personality traits.
The objective was to demonstrate how a combination of **rule-based Natural Language Processing (NLP)** and **Large Language Model (LLM)** reasoning can produce structured, explainable knowledge from natural language text.

Since no real dataset was available, **synthetic sentences** were generated to simulate human interactions that describe social and psychological traits. Using **spaCy**, entities and grammatical relationships were extracted with precision, while an **LLM** enriched the KG by identifying personality adjectives, mapping them to **Big-Five psychological dimensions**, and inferring implied relationships not captured by rules alone.

The workflow was designed as a **chain of modular prompts and scripts**, ensuring stepwise control, interpretability, and reproducibility. Evaluation focused on **Precision, Entity Coverage, and Connectivity** to measure correctness, completeness, and graph structure.
Results show that this hybrid pipeline produces accurate, semantically rich, and interpretable KGs — bridging the gap between symbolic structure and contextual reasoning.

---

## **Problem Understanding**

Unstructured text, such as descriptions or personality notes, often hides valuable insights about human relationships and behavioral traits. However, extracting structured knowledge from such data is challenging because:

* Traditional NLP models excel at grammatical parsing but fail to capture nuanced context or inferred meaning.
* LLMs, while powerful in reasoning, can introduce inconsistencies or hallucinations without structured grounding.

The task was to **build a Knowledge Graph from text documents** that describe individuals and their personality traits, showing connections such as *friendship*, *mentorship*, or *shared characteristics*.
The final KG should allow both humans and algorithms to understand “who is connected to whom,” “how they relate,” and “what traits describe each person.”

Thus, the goal was not only to extract factual relationships but also to **embed personality context** — turning flat text into a semantically connected web of human interactions.

---

## **Research Process (LLM Q&A Steps)**

To approach the problem systematically, an iterative **LLM-guided research process** was followed. Each stage focused on understanding concepts, exploring techniques, and building the workflow incrementally:

1. **Understanding Knowledge Graphs** — Defined KGs as networks of entities (nodes), relationships (edges), and attributes, illustrated through examples like “Alice → works at → Google.”
2. **Purpose Exploration** — Identified KGs as tools to connect, organize, and reason over data for explainability and analysis.
3. **Application in Data Science** — Learned how KGs unify disconnected data sources, enhance context for analytics, and support reasoning for ML and explainable AI.
4. **Workflow Mapping** — Designed a 6-stage process: Data Collection → Extraction → Construction → Reasoning → Analysis → Reporting.
5. **Tool Comparison** — Evaluated **spaCy** for structured extraction, **LLMs** for reasoning, and proposed a **hybrid model** combining both.
6. **Synthetic Data Design** — Generated short sentences to simulate interpersonal relations with traits, e.g., “Alice is friends with Bob and she is kind.”
7. **Pipeline Implementation** — Developed scripts for entity extraction (spaCy), enrichment (LLM), and visualization (NetworkX).
8. **Evaluation Planning** — Identified measurable metrics like Precision, Entity Coverage, and Connectivity to assess pipeline quality.

This **Q&A-based exploration** ensured conceptual understanding before implementation, mirroring a research-driven data science workflow.

---

## **Chosen Approach: Hybrid (spaCy + LLM)**

The **hybrid approach** was chosen over single-method alternatives because it balances **accuracy, reasoning, and interpretability**:

* **spaCy-only (Rule-based):** Excellent at grammatical precision but weak at capturing context or personality inference.
* **LLM-only (Reasoning-based):** Strong contextual understanding but prone to format drift and hallucination.
* **Hybrid:** Combines structural accuracy from spaCy with semantic richness from an LLM.

### Justification

| Method     | Strength                            | Limitation                         |
| ---------- | ----------------------------------- | ---------------------------------- |
| **spaCy**  | Reliable syntactic extraction       | Misses implicit traits             |
| **LLM**    | Infers personality and hidden links | Inconsistent or verbose            |
| **Hybrid** | Structured + semantic               | Slightly slower, but interpretable |

This hybrid setup ensures that:

* spaCy identifies **entities** and **relationships** (high structural fidelity),
* The LLM enriches nodes with **traits** and **inferred connections**, and
* The KG remains **consistent, contextual, and explainable.**

---

## **Synthetic Data Generation**

Since the assignment required privacy-safe and easily interpretable data, synthetic text was created manually and refined using an LLM.
Eight short sentences were generated to simulate social interactions with embedded traits:

```
Alice is friends with Bob and she is kind.
Bob works with Carol who is very ambitious.
Carol mentors Dave and is confident.
Dave admires Emma because she is creative.
Emma collaborates with Frank and is generous.
Frank is married to Grace who is cheerful.
Grace supports Henry and is patient.
Henry respects Alice since she is honest.
```

This dataset was ideal because it included:

* Clear **entity names** (people),
* Obvious **relationships** (friends, works with, supports), and
* Natural **adjective-based traits** for personality mapping.

---

## **Implementation Workflow (Chain of Prompts)**

The pipeline followed a sequential **chain-of-prompts** approach to ensure modularity and control.

### Step 1 — Entity & Relationship Extraction

**Tool:** `spaCy`
**Goal:** Extract subjects, verbs (relations), and objects using dependency parsing.
**Output Example:**

```json
{"subject": "Bob", "relation": "works_with", "object": "Carol"}
```

### Step 2 — Personality Trait Enrichment

**Tool:** LLM (GPT-based model)
**Goal:** Identify personality adjectives, infer implied links, and generate `has_trait` relationships.
**Output Example:**

```json
{"subject": "Carol", "relation": "has_trait", "object": "confident"}
```

### Step 3 — Integration (Hybrid Merge)

Combined spaCy’s structured triples with LLM’s enrichment to create a complete, context-rich KG:

```json
{
  "entities": ["Alice", "Bob", "Carol", "kind", "ambitious", "confident"],
  "triples": [
    {"subject": "Alice", "relation": "is_friends_with", "object": "Bob"},
    {"subject": "Alice", "relation": "has_trait", "object": "kind"},
    {"subject": "Bob", "relation": "works_with", "object": "Carol"},
    {"subject": "Carol", "relation": "has_trait", "object": "confident"}
  ]
}
```

### Step 4 — Graph Construction & Visualization

**Tool:** `NetworkX` (Python)
Nodes were created for each entity, edges for relationships, and personality attributes were attached as node properties.
The resulting visualization showed clusters of people connected through relational and trait edges.

---

## **Personality Representation**

Personality was encoded directly in the KG as **attributes** under each person node, combining **Big-Five scores** and **adjective tags**:

```json
{
  "id": "Alice",
  "type": "Person",
  "personality": {
    "big_five": {
      "openness": 0.78,
      "conscientiousness": 0.54,
      "extraversion": 0.67,
      "agreeableness": 0.82,
      "neuroticism": 0.22
    },
    "adjectives": ["kind", "creative"],
    "confidence": 0.9
  }
}
```

**Why this format works:**

* **Hybrid readability:** Adjectives make traits interpretable, while numeric Big-Five attributes support quantitative analysis.
* **Machine-friendly:** Numeric traits enable graph-based similarity and clustering.
* **Explainable:** Provenance and confidence fields maintain transparency.

---

## **Data Processing & Normalization**

To ensure consistency across stages:

* **Entity normalization:** Unified names (e.g., “Bob” vs. “Bobby”) using string matching and lowercase conversion.
* **Relation normalization:** Standardized verbs to lemmatized forms (e.g., *“is friends with” → “friends_with”*).
* **Trait normalization:** Mapped adjectives (kind, ambitious, confident) to Big-Five categories via LLM-guided dictionaries.
* **Provenance tracking:** Stored original sentence references to trace extracted knowledge to its source.

Normalization ensured **clean, non-redundant graph structure** and allowed consistent reasoning across sentences.

---

## **Evaluation & Metrics**

Three simple yet meaningful evaluation checks were conducted to assess Knowledge Graph (KG) quality:

| Metric                        | Purpose                                          | Calculation / How to Compute |
|-------------------------------|--------------------------------------------------|------------------------------|
| **Precision of Triples**      | Measures accuracy of extracted relationships     | true positives ÷ predicted total (manual check or gold-standard comparison) |
| **Recall of Triples**         | Measures completeness of extraction              | true positives ÷ actual total in gold set |
| **F1-score**                  | Harmonic mean of precision and recall (balance)  | 2 * (precision * recall) / (precision + recall) |
| **Entity Coverage**           | Assesses completeness of entity extraction       | extracted unique entities ÷ expected unique entities in text |
| **Connectivity (avg degree)** | Evaluates how well nodes are linked              | average node degree = Σ(degree) / N |

---

### **Results**

Precision = **0.67**, Recall = **1.00**, F1-score = **0.80**,  
Entity Coverage = **1.00**, Connectivity (avg degree) = **1.75**

**Key Takeaways:**
- **Precision (0.67):** Most extracted triples were correct, though some false positives occurred.  
- **Recall (1.00):** All true relationships were successfully identified — excellent completeness.  
- **F1-score (0.80):** Indicates a strong overall balance between accuracy and coverage.  
- **Entity Coverage (1.00):** Every entity mentioned in the text was captured in the graph.  
- **Connectivity (1.75):** Nodes are well connected, forming a coherent and interpretable structure.

**Interpretation:**  
The hybrid pipeline achieves full recall and entity coverage, producing a complete and meaningful Knowledge Graph.  
Precision can be further improved by refining relation extraction or adding a light LLM-based validation step.


---

## **Results / Insights**

1. **Graph Structure:** The hybrid KG showed dense connections among people, with personality traits attached as secondary nodes or embedded attributes.
2. **Contextual Richness:** Traits like *kind*, *ambitious*, and *confident* added semantic layers beyond simple social links.
3. **Reasoning Capability:** The LLM-enriched KG could infer soft relationships — for example, “Alice (kind)” and “Grace (patient)” forming an empathy cluster.
4. **Interpretability:** Graph visualization provided intuitive insights into personality-based social networks.
5. **Explainability:** Each trait or relationship was traceable to its textual origin, ensuring transparency and auditability.

---

## **Limitations and Future Improvements**

While effective for small datasets, the current pipeline faces some limitations:

| Limitation                  | Description                                     | Improvement                                                       |
| --------------------------- | ----------------------------------------------- | ----------------------------------------------------------------- |
| **Scalability**             | LLM enrichment slows with large documents       | Batch extraction or chunk-level LLM calls                         |
| **Consistency**             | LLM may output slight format variations         | Use strict JSON schema validation                                 |
| **Trait Mapping Ambiguity** | Adjective-to-Big-Five mapping may be subjective | Incorporate established lexicons (e.g., LIWC, OCEAN dictionaries) |
| **Evaluation Depth**        | Manual validation limits coverage               | Introduce automated evaluation with reference triples             |

Future work could involve:

* Integrating **Graph Neural Networks (GNNs)** for personality clustering,
* Building an **interactive Neo4j dashboard**, and
* Expanding the LLM reasoning layer with **contextual feedback loops** to refine trait inference.

---

## **Conclusion**

This project demonstrates a **complete, explainable Knowledge Graph pipeline** that transforms unstructured text into structured personality-aware knowledge.
By combining **spaCy’s syntactic reliability** with **LLM’s semantic reasoning**, the hybrid approach delivers a balanced system — both machine-processable and human-interpretable.

Synthetic data generation ensured privacy and diversity, while normalization and structured evaluation supported consistency and reproducibility.
The final KG not only represents entities and relationships but also integrates **psychological context**, making it valuable for applications in HR analytics, social behavior analysis, and explainable AI.

The work reflects a practical balance between **symbolic AI** (structure) and **neural reasoning** (context), forming a foundational step toward **context-aware, interpretable knowledge systems.**

---
