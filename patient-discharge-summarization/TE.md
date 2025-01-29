# Testing and Evaluation (T&E) Framework for Note Summarization - Patient Discharge Summary

*(use as guidance when completing the CHAI Applied Model Card for a note summarization - patient discharge summary use case)*

## Pre-Deployment

*(additional detail for pre-deployment stages of the AI lifecycle, can be found in the CHAI RAIG)*

### Usefulness, Usability, and Efficacy

*(additional detail for the Responsible AI Principle of Usefulness, Usability, and Efficacy can be found in the CHAI RAIG)*

**Method/Metric:**

* **Physician Documentation Quality Instrument, Nine-item tool (PDQI-9)**
  * Intended Use: 9 question survey that details aspects of usefulness. 
  * Rationale: 
  * Reference: [Physician Documentation Quality Instrument (PDQI-9)](https://pmc.ncbi.nlm.nih.gov/articles/instance/3633322/bin/ACI-03-0164-s001.pdf)
  * Open-source tooling:
  
* **DocLens**
  * Intended Use: Assesses coverage of known assertions, or facts, represented in human expert "ground truth" summaries. (1) Extract important facts from ground-truth summaries, either manually or using the LLM-as-a-judge approach (2) extract important facts from AI-generated summaries, either manually or using the LLM-as-a-judge approach (3) calculate accuracy, sensitivity, specificity, PPV, NPV of AI-extracted facts as compared to ground-truth facts.
  * Rationale: Recommend use of LLM-as-judge ways of generating claims from reference summaries and comparing those claims against the LLM-generated summary. One such implementation is DocLens, which captures completeness (i.e., claim recall -- requires reference), conciseness (i.e., claim precision -- requires reference), and attribution accuracy (reference-free). Other implementations include SummaQA.
  * Reference: [DocLens: Multi-aspect Fine-grained Medical Text Evaluation](https://aclanthology.org/2024.acl-long.39/)
  * Open-source tooling: 

### Fairness, Equity, and Bias Management

*(additional detail for the Responsible AI Principle of Fairness, Equity, and Bias Management can be found in the CHAI RAIG)*

Method:

Metric:

### Safety and Reliability

*(additional detail for the Responsible AI Principle of Safety and Reliability can be found in the CHAI RAIG)*

Method:

Metric:

### Transparency, Intelligibility, and Accountability

*(additional detail for the Responsible AI Principle of Transparency, Intelligibility, and Accountability can be found in the CHAI RAIG)*

Method:

Metric:

### Security and Privacy

*(additional detail for the Responsible AI Principle of Security and Privacy can be found in the CHAI RAIG)*

Method:

Metric:

## Post-Deployment

*(additional detail for post-deployment stages of the AI lifecycle, can be found in the CHAI RAIG)*

### Usefulness, Usability, and Efficacy

*(additional detail for the Responsible AI Principle of Usefulness, Usability, and Efficacy can be found in the CHAI RAIG)*

Method:

Metric:

### Fairness, Equity, and Bias Management

*(additional detail for the Responsible AI Principle of Fairness, Equity, and Bias Management can be found in the CHAI RAIG)*

Method:

Metric:

### Safety and Reliability

*(additional detail for the Responsible AI Principle of Safety and Reliability can be found in the CHAI RAIG)*

Method:

Metric:

### Transparency, Intelligibility, and Accountability

*(additional detail for the Responsible AI Principle of Transparency, Intelligibility, and Accountability can be found in the CHAI RAIG)*

Method:

Metric:

### Security and Privacy

*(additional detail for the Responsible AI Principle of Security and Privacy can be found in the CHAI RAIG)*

Method:

Metric:
