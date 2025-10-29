Testing and Evaluation (T&E) Framework
======================================


Usefulness, Usability, and Efficacy
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

*(additional detail for the Responsible AI Principle of Usefulness,
Usability, and Efficacy can be found in the CHAI RAIG)*

**Recommended Methods/Metrics:**

**FHIR Mapping Accuracy**

  - Intended Use: Ensures interoperability and reliability of structured datasets used in downstream applications like clinical decision support (CDS), population health analytics, cohort discovery, and automated phenotyping. Accurate mapping is essential for safe, consistent data flow across interoperable systems.
  - Description: Measures how effectively NLP or LLM-based systems convert extracted clinical entities (e.g., medications, lab values, dosage timing) into standardized FHIR or OMOP representations. Evaluates precision, recall, and completeness across key structured fields such as `Medication.form` and `dosage.timing.repeat.when`, ensuring alignment with canonical healthcare data standards.
  - Pre-implementation, Post-Implementation, or Both: Pre-implementation (Model Validation)
  - Persona (Developer, Implementer, or Both): Developer
  - Benchmark: F1-score ranged from 0.71–0.99 across different FHIR elements (e.g., 0.988 for `medicationCodeableConcept.coding`, 0.779 for `Medication.form`, 0.727 for `timing.repeat.when`), demonstrating variation across element complexity.
  - Supporting Literature: Hong et al., *Integrating Structured and Unstructured EHR Data Using an FHIR-based Type System: A Case Study with Medication Data*
  - Alignment to Use Case (Low, Medium, High): High
  - Open-source Tooling: `FHIR Validator CLI <https://confluence.hl7.org/spaces/FHIR/pages/35718580/Using+the+FHIR+Validator>`__
  - Notes about Open-source Tooling: Tools such as the FHIR Validator CLI or custom Python scripts comparing gold vs. predicted JSON objects can quantify field-level mapping correctness. Validation should cover required fields, nested structures, and optional extensions.
  - Evaluation Example: See fhir_mapping_accuracy_demo.ipynb in evaluation-notebooks Folder. 

**Extraction Accuracy**

  - Intended Use: Validates the reliability of upstream data capture before standardization, ensuring the extracted information feeding downstream decision support, analytics, and cohort discovery systems is accurate, complete, and clinically meaningful. High extraction accuracy is a prerequisite for successful mapping and model trust.
  - Description: Measures how effectively NLP or LLM-based pipelines extract key structured fields (e.g., medications, dosage, frequency, and lab results) from raw, unstructured clinical text prior to FHIR or OMOP normalization. Evaluates field-level correctness, recall of relevant entities, and the model’s ability to capture complete medication or laboratory information across diverse patient notes.
  - Pre-implementation, Post-Implementation, or Both: Pre-implementation (Model Validation)
  - Persona (Developer, Implementer, or Both): Developer
  - Benchmark: F1-score ≈ 95% across seven medication fields (validated on 34 patients); deployment across >11,000 patient records yielded a 27% increase in medication capture and 60–64% improvement in oncology data completeness.
  - Supporting Literature: Stuhlmiller et al., *A Scalable Method for Validated Data Extraction from Electronic Health Records with Large Language Models*
  - Alignment to Use Case (Low, Medium, High): High
  - Open-source Tooling: `medSpaCy <https://github.com/medspacy/medspacy>`__
  - Notes about Open-source Tooling: See `medspacy.io.DocConsumer` in the medSpaCy repository for generating structured outputs from extracted entities. Combine it with `medspacy.ner.TargetRule` and `medspacy.context.ConTextComponent` to perform rule-based extraction and assertion detection. After processing, evaluate extraction accuracy by comparing `doc._.get_data(
  

**Document Extraction Accuracy**

  - Intended Use: Ensures high-quality digitization and interpretation of scanned medical records, enabling downstream analytics, cohort discovery, and decision-support systems to rely on complete and accurate structured data. Validates the performance of NLP pipelines built on OCR-processed text in real-world EHR ingestion workflows.
  - Description: Measures how effectively deep learning–based NLP models (e.g., ClinicalBERT, BioBERT) extract structured information from scanned or semi-structured EHR documents after OCR. Evaluates classification and extraction accuracy across key variables (e.g., Apnea–Hypopnea Index [AHI], oxygen saturation [SaO₂]) using metrics such as AUROC, accuracy, and precision.
  - Pre-implementation, Post-Implementation, or Both: Pre-implementation
  - Persona (Developer, Implementer, or Both): Developer
  - Benchmark: ClinicalBERT achieved AUROC = 0.9743, Accuracy = 94.76% for AHI; AUROC = 0.9523, Accuracy = 91.61% for SaO₂, outperforming comparable NLP architectures.
  - Supporting Literature: Hsu et al., *Deep Learning-based NLP Data Pipeline for EHR Scanned Document Information Extraction*
  - Alignment to Use Case (Low, Medium, High): High
  - Open-source Tooling: `Hugging Face Transformers (BERT) <https://github.com/huggingface/transformers/blob/main/src/transformers/models/bert/modeling_bert.py>`__
  - Notes about Open-source Tooling: See `transformers.models.bert.modeling_bert.BertForSequenceClassification` in the Hugging Face Transformers repository for reference implementations of document-level classifiers. For evaluation, compute AUROC and accuracy using `sklearn.metrics.roc_auc_score` and `sklearn.metrics.accuracy_score` on model logits after sigmoid or softmax normalization.

- **Clinical Predictive Utility**

  - Intended Use: Benchmarks the clinical usefulness and efficacy of learned representations for real-world tasks such as mortality prediction. Also applicable to other EHR-derived predictions (e.g., readmission risk, deterioration), where both thresholded accuracy and discriminative capacity affect clinical trust.
  - Description: Evaluates how well the Fair Patient Model (FPM) defined in the referenced study supports downstream clinical prediction. Accuracy measures overall correctness; AUROC measures the model’s ability to distinguish between outcomes (e.g., alive vs deceased) using EHR-based patient representations.
  - Pre-implementation, Post-Implementation, or Both: Pre-implementation model evaluation
  - Persona (Developer, Implementer, or Both): Developer — evaluates model performance before deployment, focusing on representational efficacy and predictive accuracy during model design, training, and validation.
  - Benchmark: Accuracy = 0.8381; AUROC ≈ 0.6486 (30-day mortality task)
  - Supporting Literature: `arXiv:2306.03179 <https://arxiv.org/pdf/2306.03179>`__
  - Alignment to Use Case (Low, Medium, High): High
  - Open-source Tooling: `auton-survival metrics.py <https://github.com/autonlab/auton-survival/blob/master/auton_survival/metrics.py>`__
  - Notes about Open-source Tooling: See `auton_survival.metrics.survival_regression_metric` in the auton-survival repository for the built-in implementation of time-dependent AUROC (IPCW-AUC). Use `metric='auc'` with your chosen horizon (e.g., 30 days). Accuracy can also be computed with `sklearn.metrics.accuracy_score`.


- **Deterministic Reproducibility of LLM Inference**

  - Description: Evaluates the degree to which an EHR-integrated LLM produces consistent outputs when given identical inputs across runs, hardware, or parallelization settings. This metric ensures that clinicians, auditors, and regulators can rely on stable, reproducible outputs for the same patient record or query. Variability in inference undermines trust, complicates evaluation, and increases clinical risk.
  - Intended Use: Benchmarks the reliability and efficacy of LLM-based EHR tools, enabling validation of downstream tasks (e.g., summarization of patient notes, guideline-based recommendations, clinical decision support). High reproducibility strengthens model efficacy by ensuring that model evaluations remain valid across time and infrastructure.
  - Pre-implementation, Post-Implementation, or Both: Both
  - Persona (Developer, Implementer, or Both): Both
  - Benchmark: Output stability > 99% exact-match rate across 100 repeated inference runs with fixed seeds and identical input prompts; semantic variability < 1% using embedding-based similarity metrics (cosine > 0.99).
  - Supporting Literature: `Defeating Nondeterminism in LLM Inference <https://thinkingmachines.ai/blog/defeating-nondeterminism-in-llm-inference/>`__
  - Alignment to Use Case (Low, Medium, High): Medium
  - Open-source Tooling: `batch_invariant_ops <https://github.com/thinking-machines-lab/batch_invariant_ops>`__
  - Notes about Open-source Tooling: Wrap inference with `set_batch_invariant_mode(True)` to swap in batch-invariant kernels (mm, addmm, log_softmax, mean). Use greedy decoding (`temperature=0`, `top_p=0`, `top_k=1`), fix seeds, and disable dynamic batching/scheduling in your server (e.g., vLLM). Validate by running N identical queries across batch sizes and hardware to target ≥99–100% exact-match outputs. See the repo’s `deterministic_vllm_inference.py` for an implementation template.



Fairness and Bias Management
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

- **Structural Missingness Disparity Assessment (Measurement Frequency Disparities, Missingness Patterns, Mortality Prediction AUC)**

  - Description: Analyzes ICU data from MIMIC-III (n = 23,426), showing that older, male, and White patients had more frequent vital monitoring. These disparities were predictive of in-hospital mortality (AUC = 0.76), even when using only the measurement patterns—not the clinical values—demonstrating embedded structural bias in data availability.
  - Intended Use: To flag and address demographic data-collection gaps early in the AI pipeline. These fairness diagnostics help improve downstream prediction equity by informing pre-processing, feature selection, and sampling strategies. Transferable to any EHR-driven system where vital-sign frequency and missingness may vary by age, race, or gender.
  - Pre-implementation, Post-Implementation, or Both: Pre-implementation — pre-processing and model development phase.
  - Persona (Developer, Implementer, or Both): Developer — focuses on bias detection and mitigation during pre-processing and model development, directly involving data handling, feature engineering, and fairness diagnostics.
  - Benchmark: Significant demographic differences in measurement rates; AUC 0.76 using only the measurement-pattern features from the study.
  - Supporting Literature: `BMC Medical Informatics and Decision Making <https://bmcmedinformdecismak.biomedcentral.com/articles/10.1186/s12911-025-03058-9>`__
  - Alignment to Use Case (Low, Medium, High): High — directly relevant to extraction consistency and equity in recorded data.
  - Open-source Tooling:  
    `ehrapy.bias <https://github.com/theislab/ehrapy/blob/main/ehrapy/preprocessing/_bias.py>`__  
    `seeBias R evaluate_prediction.R <https://github.com/nliulab/seeBias/blob/main/R/evaluate_prediction.R>`__  
    `AIF360 sample_distortion_metric.py <https://github.com/Trusted-AI/AIF360/blob/main/aif360/metrics/sample_distortion_metric.py>`__  
    `Fairlearn MetricFrame <https://fairlearn.org/main/api_reference/fairlearn.metrics.html#fairlearn.metrics.MetricFrame>`__
  - Notes about Open-source Tooling: For structural missingness and measurement-pattern disparity analysis, use ehrapy’s bias modules (e.g., `ehrapy/bias/`), seeBias’s R functions for group-wise AUC and calibration plots, audit and mitigate with AIF360’s fairness metrics, and generate disaggregated performance results using Fairlearn’s `MetricFrame` in `fairlearn/metrics/_metric_frame.py`.


- **Counterfactual DocLens**

  - Intended Use: recommend developer change out the actual source text.
    Recommend implementer evaluate DocLens stratified by actual patient
    category.
  - Rationale: given collection of DocLens information from above, via
    Usefulness principle, stratify to assess similarities/differences
    across different patient groups.
  - Reference: `DocLens: Multi-aspect Fine-grained Medical Text
    Evaluation <https://aclanthology.org/2024.acl-long.39/>`__
  - Open-source tooling:
  - Monitoring Cadence (Time Interval, Frequency, etc.):
  - Recommended Responsible Party for Monitoring
    (Developer/Implementer):
  - Recommended Notification of Significant Changes (Yes/No, Describe
    when notification of other party is recommended):

- **Error Distribution Disparity Index (EDDI) and Equalized Odds (EO) (e.g., Contrastive Learning with Synthetic Counterparts)**

  - Description: The FairEHR-CLP framework generates demographically matched synthetic samples per patient and minimizes representation differences using contrastive learning. Evaluations were conducted on three EHR datasets (MIMIC-III, MIMIC-IV, and STARR) for delirium, opioid use disorder (OUD), and 30-day readmission prediction.
  - Intended Use: EDDI and EO metrics quantify subgroup fairness in model errors. These can be embedded in training pipelines to balance performance across demographic groups. The synthetic-matching and contrastive-learning approach can be integrated into any EHR-based AI system to proactively minimize subgroup disparities.
  - Pre-implementation, Post-Implementation, or Both: Pre-implementation — model training and evaluation.
  - Persona (Developer, Implementer, or Both): Developer — focuses on fairness-aware training and evaluation techniques such as contrastive learning and synthetic sampling. These are core Developer responsibilities for bias mitigation and ensuring equitable model performance.
  - Benchmark: FairEHR-CLP reduced EDDI and EO compared to baseline models while achieving comparable AUROC and AUPRC performance.
  - Supporting Literature: `FairEHR-CLP: Contrastive Learning for Fair EHR Prediction <https://arxiv.org/html/2402.00955v1#S3>`__
  - Alignment to Use Case (Low, Medium, High): High
  - Open-source Tooling:  
    `FairEHR-CLP Feature Extraction and Fairness Analysis Notebook <https://github.com/EternityYW/FairEHR-CLP/blob/main/feature_extraction_and_fairness_analysis.ipynb>`__  
    `Fairlearn Fairness Metrics <https://github.com/fairlearn/fairlearn/blob/main/fairlearn/metrics/_fairness_metrics.py>`__  
    `AIF360 Equalized Odds Postprocessing <https://github.com/Trusted-AI/AIF360/blob/main/aif360/algorithms/postprocessing/eq_odds_postprocessing.py>`__
  - Notes about Open-source Tooling: EDDI can be computed using the FairEHR-CLP reference notebook. Equalized Odds metrics are available directly through Fairlearn, with optional enforcement and mitigation modules in AIF360. Together, these toolkits enable both auditing and proactive correction of subgroup disparities during model development.

- **Demographic Parity Ratio; Equality of Opportunity Difference**

  - Description: Demographic parity compares positive prediction rates across groups, while equality of opportunity compares false negative rates. These fairness metrics evaluate whether predictive models produce equitable outcomes across demographic subgroups.
  - Intended Use: To detect and mitigate bias in EHR-based representation learning before deployment. Supports fairness audits for systems that rely on learned embeddings—such as summarization, cohort building, and predictive triage—ensuring subgroup performance parity.
  - Pre-implementation, Post-Implementation, or Both: Pre-implementation — model evaluation.
  - Persona (Developer, Implementer, or Both): Developer — focuses on detecting and mitigating bias during model development using learned representations.
  - Benchmark: Outperformed baseline models on all fairness metrics while preserving accuracy.
  - Supporting Literature: `Fair Patient Model (FPM) — arXiv:2306.03179 <https://arxiv.org/pdf/2306.03179>`__
  - Alignment to Use Case (Low, Medium, High): Medium
  - Open-source Tooling:  
    `Fairlearn Fairness Metrics <https://github.com/fairlearn/fairlearn/blob/main/fairlearn/metrics/_fairness_metrics.py>`__  
    `fairMLHealth Fairness Audits <https://github.com/KenSciResearch/fairMLHealth/blob/integration/fairmlhealth/__fairness_metrics.py>`__
  - Notes about Open-source Tooling: Demographic Parity Ratio and Equality of Opportunity Difference can be computed directly using fairMLHealth, which provides healthcare-specific fairness audit tools. For general Python pipelines, both metrics are implemented in Fairlearn’s metrics module, making it straightforward to integrate fairness reporting alongside model evaluation


Safety and Reliability
~~~~~~~~~~~~~~~~~~~~~~

**Recommended Methods/Metrics:**

- **Incidence of Reporting Errors Before/After Standardization**

  - Description: The Crescent City Beacon Community (CCBC) implemented a five-step standardization framework to harmonize, detect, and correct EHR data errors in quality measures. This process established consistent data handling and validation practices across clinical systems.
  - Intended Use: To measure and reduce error rates in standardized data extraction workflows, ensuring accuracy in downstream quality reporting and clinical decision support. The approach can be replicated across EHR networks to improve data integrity and reliability.
  - Pre-implementation, Post-Implementation, or Both: Both — enables before-and-after analysis of error incidence.
  - Persona (Developer, Implementer, or Both): Implementer — focuses on deploying and monitoring standardization processes in real-world EHR systems to reduce reporting errors and strengthen clinical decision-making.
  - Benchmark: Reduced reporting burden and data-entry errors over nine months, leading to measurable improvements in trust and reliability of quality reporting.
  - Supporting Literature: `Reducing Data Reporting Errors Through Standardization — PMC4371440 <https://pmc.ncbi.nlm.nih.gov/articles/PMC4371440/>`__
  - Alignment to Use Case (Low, Medium, High): High
  - Open-source Tooling: `OHDSI DataQualityDashboard <https://github.com/OHDSI/DataQualityDashboard>`__
  - Notes about Open-source Tooling: Use the open-source DataQualityDashboard to measure error incidence before and after standardization. The dashboard runs automated quality checks on OMOP CDM–formatted EHRs, enabling organizations to track, visualize, and document improvements in data quality and reporting accuracy over time.

- **Harmfulness Score (0–7), Error Counts (Inaccuracy, Omission, Hallucination), Reviewer Preference**

  - Description: Evaluated physician- versus LLM-generated discharge summaries for quality, error rates, and potential for harm. Twenty-two physicians, blinded to the source, scored each summary using an adapted AHRQ harm scale to assess the severity and type of errors present.
  - Intended Use: Harmfulness scores and error-type distributions provide a structured safety lens for evaluating narrative outputs from LLMs. This framework can validate LLM-generated summaries before clinical deployment and inform human-in-the-loop editing processes.
  - Pre-implementation, Post-Implementation, or Both: Post-generation, pre-deployment human review — can also support ongoing quality assurance (QA) in live systems.
  - Persona (Developer, Implementer, or Both): Both — Developers can use it to evaluate and refine model outputs before deployment, while Implementers can apply it in real-world QA workflows to continuously monitor safety.
  - Benchmark: LLMs produced more concise and coherent summaries but showed higher total error counts (2.91 vs. 1.82 per summary) and higher mean harmfulness (0.84 vs. 0.36). Only one LLM-generated output reached a harmfulness score ≥ 4 (permanent harm). Reviewer preference did not differ significantly between human and LLM summaries.
  - Supporting Literature: `Evaluating the Safety of LLM-Generated Clinical Summaries — PubMed 40323616 <https://pubmed.ncbi.nlm.nih.gov/40323616/>`__
  - Alignment to Use Case (Low, Medium, High): High
  - Open-source Tooling: `medmcqa Repository <https://github.com/medmcqa/medmcqa>`__ *(not a direct scorer, but applicable for quantifying inaccuracy rates in generated texts).*
  - Notes about Open-source Tooling: Use `stats.py` in the medmcqa repository to automatically compute error counts (e.g., inaccuracy detection during summary validation). Harmfulness scoring requires human evaluation using the adapted AHRQ rubric described in the referenced study.


- **Inter-rater Reliability (ICC, Krippendorff’s α), Internal Consistency (Cronbach’s α), Discriminant Validity**

  - Description: The PDSQI-9 is a human evaluation instrument used to assess the quality of LLM-generated clinical summaries across nine key dimensions, including accuracy, comprehensibility, and stigmatization. It provides standardized human evaluation for identifying reliability and validity in LLM-generated outputs.
  - Intended Use: These metrics ensure consistent, reliable, and valid human assessments of LLM-generated summaries prior to deployment. They help detect hallucinations, omissions, and inconsistencies while establishing the clinical readiness and trustworthiness of models.
  - Pre-implementation, Post-Implementation, or Both: Pre-deployment evaluation of LLM summaries — optionally post-deployment for ongoing quality monitoring.
  - Persona (Developer, Implementer, or Both): Developer — used during pre-deployment testing to validate and improve LLM output quality before clinical use.
  - Benchmark: ICC = 0.867, Cronbach’s α = 0.879, Krippendorff’s α = 0.575; demonstrated strong ability to distinguish high- versus low-quality summaries (P < .001).
  - Supporting Literature: `Evaluating Consistency and Validity of Human Assessment for LLM Clinical Summaries — PubMed 40323321 <https://pubmed.ncbi.nlm.nih.gov/40323321/>`__
  - Alignment to Use Case (Low, Medium, High): High
  - Open-source Tooling:  
    `Pingouin Reliability Module (ICC, Cronbach’s α) <https://pingouin-stats.org/build/html/_modules/pingouin/reliability.html>`__  
    `Krippendorff’s α Implementation <https://github.com/grrrr/krippendorff-alpha/blob/master/krippendorff_alpha.py>`__
  - Notes about Open-source Tooling:  
    - Compute ICC using:  
      `pg.intraclass_corr(data=df_long, targets='case_id', raters='rater_id', ratings='score')` → store ICC column results.  
    - Compute Cronbach’s α using:  
      `pg.cronbach_alpha(data=df_wide)` → record α value and confidence interval.  
    - Compute Krippendorff’s α using:  
      `alpha(reliability_data, level_of_measurement='nominal' | 'interval' ...)` after importing the Krippendorff module.  
    These implementations enable direct quantification of reliability and internal consistency for human evaluation data.


**Error Rate (Data Correctness & Completeness Validation)**

  - Intended Use: Ensures that standardized EHR datasets used for analytics or CDS reflect original clinical intent without data loss or distortion. Reduces the risk of downstream safety issues and incorrect model inferences.
  - Description: Measures the degree to which post-extraction structured EHR data accurately represents the original source records. Evaluates discrepancies introduced during normalization or mapping, as well as missing or misclassified values across core fields (e.g., laboratory results, medication attributes, encounter details).
  - Pre-implementation, Post-Implementation, or Both: Post-implementation
  - Persona (Developer, Implementer, or Both): Both
  - Benchmark: Case study identified significant discrepancies between original charts and EHR extracts, underscoring the need for ongoing validation and alerting before CDS integration.
  - Supporting Literature: Bowman et al., *Impact of Electronic Health Record Systems on Information Integrity: Quality and Safety Implications*
  - Alignment to Use Case (Low, Medium, High): High
  - Open-source Tooling: `OHDSI DataQualityDashboard <https://github.com/OHDSI/DataQualityDashboard/tree/main/inst/sql/sql_server>`__
  - Notes about Open-source Tooling: See `DataQualityDashboard/inst/sql/sql_server` in the OHDSI repository for SQL-based data-quality checks covering error rates, correctness, and completeness in OMOP Common Data Model tables. Use the “DQD Check Results” module to compute field-level percent-passed metrics and validate transformed EHR data against expected schema constraints.

**Correctness & Completeness (SHARPn Validation)**

  - Intended Use: Validates post-standardization data integrity, ensuring that key phenotyping and population analytics tasks operate on accurate, comprehensive records. Enhances reliability for secondary use cases such as clinical research and cohort identification.
  - Description: Measures how completely and correctly EHR-derived data meet predefined clinical criteria after extraction and normalization. Evaluates whether structured elements (e.g., laboratory values, diagnostic codes, vital signs) are accurately populated and conform to domain-specific definitions such as lipid or metabolic criteria.
  - Pre-implementation, Post-Implementation, or Both: Post-implementation
  - Persona (Developer, Implementer, or Both): Both
  - Benchmark: SHARPn project achieved full compliance in LDL-criteria extraction, correctly identifying 21 of 273 cases in the cohort, demonstrating accurate representation of clinical thresholds in normalized data.
  - Supporting Literature: Pathak et al., *Normalization and Standardization of Electronic Health Records for High-Throughput Phenotyping: The SHARPn Consortium*
  - Alignment to Use Case (Low, Medium, High): High
  - Open-source Tooling: `OHDSI DataQualityDashboard <https://github.com/OHDSI/DataQualityDashboard/tree/main/inst/sql/sql_server>`__, `Great Expectations Core <https://github.com/great-expectations/great_expectations/tree/develop/great_expectations/expectations/core>`__
  - Notes about Open-source Tooling: See the `DataQualityDashboard/inst/sql/sql_server/` folder for rule definitions verifying table-level and concept-level completeness in OMOP CDM datasets. Combine with `great_expectations/expectations/core/expect_table_row_count_to_equal_other_table` to confirm record-level parity between raw extracts and standardized EHR tables. Use `expect_column_values_to_not_be_null` for field completeness validation aligned with SHARPn phenotyping standards.
