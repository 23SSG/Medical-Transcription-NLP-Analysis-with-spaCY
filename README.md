# Medical-Transcription-NLP-Analysis-with-spaCY
## 🧬 Medical Transcription NLP Analysis (spaCy + scispaCy)

Biomedical data is one of the most complex and information-rich domains in data science. From clinical notes to patient records, much of this data exists in unstructured text form, making it difficult to analyze using traditional methods. This is where Natural Language Processing (NLP) becomes essential—enabling the extraction of meaningful insights such as diseases, medications, and treatment patterns from raw clinical text.

However, working with biomedical text comes with its own challenges. High-quality, publicly available datasets are scarce due to privacy concerns and regulatory restrictions. Even when available, the data is often noisy, inconsistent, and unstructured, requiring significant preprocessing before analysis.

### 📊 Project Overview

In this project, I work with unstructured medical transcription data to demonstrate how NLP techniques can be applied in the healthcare domain.

* **Dataset Source:** Medical transcription dataset scraped from the MTSamples website by Tara Boyle and made available on Kaggle
* **Initial Dataset Shape:** (4999, 6)
* **Post-Cleaning Shape:** (4966, 6)
* **Platform Used:** Databricks

The dataset consists of real-world medical transcription reports, which provide a rich source of clinical language but require careful preprocessing and domain-specific modeling.

### 🔍 Methodology

This project leverages advanced NLP techniques tailored for biomedical text:

* **Named Entity Recognition (NER):**
  Using *scispaCy* models to identify key biomedical entities such as:

  * Drug names
  * Disease/condition names

* **Rule-Based Matching:**
  To enhance extraction accuracy, NER is combined with rule-based approaches to identify:

  * Drug dosages
  * Context-specific medication patterns

By combining statistical NLP (NER) with deterministic rules, the project improves the precision of extracting clinically relevant information from unstructured text.

### 💡 Why This Matters

Accurate extraction of drugs and diseases from medical transcriptions has real-world applications in:

* Clinical decision support systems
* Pharmacovigilance and drug safety monitoring
* Healthcare analytics and research

This project highlights the potential of domain-specific NLP tools like spaCy and scispaCy in unlocking the value of biomedical text data.


⚠️Challenges in Cleaning & Preprocessing

Working with biomedical text requires a very careful balance—unlike typical NLP pipelines, aggressive preprocessing can actually degrade model performance instead of improving it.

# * Limited Preprocessing Flexibility
In standard NLP tasks, steps like removing punctuation, lowercasing, or aggressive normalization are common. However, in medical text, punctuation often carries critical meaning.
# * Removing symbols blindly can distort chemical names (e.g., hyphenated drugs)
It can also corrupt numerical expressions, such as drug dosages (e.g., “5 mg/ml”)
Selective Cleaning Approach
Due to these constraints, preprocessing had to be minimal and controlled.

# * NER Model Limitations
I experimented with the scispaCy model en_ner_bc5cdr_md, which is trained for biomedical entity recognition.
After stricter preprocessing, the model failed to recognize several expected entities
Example: The drug “Allegra” was not identified as a chemical entity
This highlights the model’s dependency on input text structure and vocabulary alignment
Impact on Downstream ML Performance
I also attempted to build ML models on top of the extracted entities from en_ner_bc5cdr_md outputs.
The resulting accuracy was not very strong
This suggests that entity extraction quality directly impacts downstream modeling performance
# * Domain-Specific Constraints
The en_ner_bc5cdr model has a limited entity scope (primarily chemicals and diseases), which restricts broader clinical insight extraction.
Additional preprocessing strategies are needed
But they must be designed carefully to preserve critical medical semantics

### ⚠️ Challenges in Data Cleaning & Preprocessing

Preprocessing biomedical text is fundamentally different from standard NLP workflows. In this project, applying conventional cleaning techniques led to loss of critical domain-specific information, requiring a more controlled and minimal approach.

* **Why Not Standard Preprocessing?**
  Typical steps like removing punctuation or aggressive normalization were avoided because:

  * Punctuation is often part of **chemical/drug names**
  * It is essential for preserving **dosage information** (e.g., `5 mg/ml`)

* **Minimal & Controlled Cleaning**
  To prevent information loss:

  * Only a limited set of characters (`'.;"`) were removed using regex
  * No aggressive transformations (like full punctuation removal or heavy normalization) were applied

* **NER Model Constraints (scispaCy)**
  The project uses the **`en_ner_bc5cdr_md`** model for Named Entity Recognition:

  * Stricter preprocessing reduced the model’s ability to detect entities
  * Example: The drug **“Allegra”** was not recognized as a chemical
  * Indicates sensitivity of biomedical NER models to input text structure

* **Impact on Machine Learning Results**

  * ML models built on extracted entities showed **lower-than-expected accuracy**
  * Performance was directly affected by incomplete or missed entity recognition

* **Dataset & Model Limitations**

  * The dataset (provided as a `.csv` file in this repository) contains **unstructured clinical text**, which still requires careful domain-aware processing
  * The **`en_ner_bc5cdr`** model supports a limited set of entity types (primarily diseases and chemicals)
  * Further improvements would require **custom preprocessing strategies or domain-specific model fine-tuning**

### 📁 Repository Contents

* `data/` → Cleaned medical transcription dataset (`.csv`)
* `notebooks/` → Jupyter Notebook with full preprocessing, NER, and analysis workflow
* `images/` → Visualizations and charts generated during analysis

### 🧠 Key Takeaway

In biomedical NLP, **more preprocessing does not mean better results**.
Preserving the structure and semantics of clinical text is critical, as even small changes can negatively impact entity recognition and downstream analysis.
