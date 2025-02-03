# Testing and Evaluation (T&E) Framework for Sepsis Risk Prediction

*(use as guidance when completing the CHAI Applied Model Card for a sepsis risk prediction use case)*

## Pre-Deployment

*(additional detail for pre-deployment stages of the AI lifecycle, can be found in the CHAI RAIG)*

### Usefulness, Usability, and Efficacy

*(additional detail for the Responsible AI Principle of Usefulness, Usability, and Efficacy can be found in the CHAI RAIG)*

**Method/Metric:**

* **Ground Theory Analysis**
  * Intended Use:
  * Rationale: 
  * Reference:

* **Sequential Organ Failure Assessment (SOFA) score**
  * Intended Use:
  * Rationale: 
  * Reference:
 
* **Risk Ratio**
  * Intended Use: outcome rate if exposed to AI model over outcome rate if not exposed to AI model
  * Rationale: 
  * Reference:

* **Area under the curve (AUC)—receiver operating characteristic (ROC) (AUC-ROC)**
  * Intended Use:
  * Rationale: 
  * Reference:
 
* **Area under the curve (AUC)—precision recall curve (PRC) (AUC-PRC)**
  * Intended Use:
  * Rationale: 
  * Reference:

* **Precision (or Positive Predictive Value, PPV)**
  * Intended Use:
  * Rationale: 
  * Reference:
 
* **Recall (or Sensitivity)**
  * Intended Use:
  * Rationale: 
  * Reference:

* **Specificity**
  * Intended Use:
  * Rationale: 
  * Reference:
 
* **F1 score**
  * Intended Use:
  * Rationale: 
  * Reference:

* **Root Mean Squared Error (RMSE)**
  * Intended Use:
  * Rationale: 
  * Reference:
 
* **Coefficient of Determination (R-squared)**
  * Intended Use:
  * Rationale: 
  * Reference:

### Fairness, Equity, and Bias Management

*(additional detail for the Responsible AI Principle of Fairness, Equity, and Bias Management can be found in the CHAI RAIG)*

**Method/Metric:**

* **Home Ownership, Utilities, Savings, Employment, and Schooling (HOUSES) Index**
  * Intended Use: compare balanced error rate (BER) against different socioeconomic status (SES) levels
  * Rationale: 
  * Reference: [HOUSES Index as an Innovative Socioeconomic Measure Predicts Graft Failure Among Kidney Transplant Recipients](https://pubmed.ncbi.nlm.nih.gov/31985729/)

* **Differential Missingness**
  * Intended Use:
  * Rationale: Target label of interest might be collected differently as function of vulnerable subgroups
  * Reference:
 
* **Potential Differential Performance Across Socioeconomic Statuses (SES)**
  * Intended Use: 
  * Rationale: 
  * Reference:

* **Use of interviews or qualitative approach to understand how biases could be introduced into the workflow**
  * Intended Use:
  * Rationale: 
  * Reference:
 
* **Parity: Equalized Odds**
  * Intended Use: prediction errors are distributed equally across different groups
  * Rationale: Equalized Odds Criterion ensures similar True Positive Rates and False Positive Rates across all demographic groups
  * Reference:

* **Parity: Equalized Opportunity**
  * Intended Use: prediction errors are distributed equally across the different groups, limited to the condition-positive individuals
  * Rationale: Equalized Opportunity Criterion could be used, which means ensuring only similar True Positive Rates across all demographic groups
  * Reference:

* **Area under the curve (AUC)—receiver operating characteristic (ROC) (AUC-ROC)**
  * Intended Use:
  * Rationale: 
  * Reference:
 
* **Area under the curve (AUC)—precision recall curve (PRC) (AUC-PRC)**
  * Intended Use:
  * Rationale: 
  * Reference:

* **Confusion Matrix**
  * Intended Use:
  * Rationale: 
  * Reference:


### Safety and Reliability

*(additional detail for the Responsible AI Principle of Safety and Reliability can be found in the CHAI RAIG)*

**Method/Metric:**

* **Risk Framework**
  * Intended Use: assess the safety and reliability of predictive AI algorithms using a risk framework.
  * Rationale: 
  * Reference: examples include National Institute of Standards and Technology (NIST) Artificial Intelligence Risk Management Framework (AI RMF 1.0), ISO/IEC 23894:2024, ISO/IEC 42001:2023, CHAI Responsible AI Guide

* **Task Analysis**
  * Intended Use: Conduct a task analysis, failure modes and effects analysis (FMEA), or detailed walkthroughs to identify potential failure points.
  * Rationale: 
  * Reference:
 
* **Non-Inferiority Assessment**
  * Intended Use: Compare the AI system to clinician experts, particularly in cases where prioritization tools are used, to ensure adequacy.
  * Rationale: 
  * Reference:
 
* **Likelihood of Failure at Identified Failure Points**
  * Intended Use: measure developed and evaluated during pre-implementation.
  * Rationale: 
  * Reference:

* **Number of Successful Predictions**
  * Intended Use: quantitative measure of reliability (e.g., number of correct predictions over total cases).
  * Rationale: 
  * Reference:
 
* **Percentage of Errors**
  * Intended Use: Quantitative measure of errors over a given number of cases.
  * Rationale: 
  * Reference:

* **Accuracy**
  * Intended Use: Evaluate the correctness of the AI model's predictions (e.g., percentage of correct predictions).
  * Rationale: 
  * Reference:
    

### Transparency, Intelligibility, and Accountability

*(additional detail for the Responsible AI Principle of Transparency, Intelligibility, and Accountability can be found in the CHAI RAIG)*

**Method/Metric:**

* **Saliency Maps**
  * Intended Use: highlight the important regions of the input data, such as images, that influenced the model’s decisions, but also consider the reliability of these maps and the rational for that region of the data being included
  * Rationale: 
  * Reference:

* **Locally Interpretable Model-Agnostic Explanations (LIME) and Shapley Values (SHAP)**
  * Intended Use: understand what parts of the input data is influencing the model’s decisions but also consider that the approach does not always give a reason for the data influencing the model.
  * Rationale: 
  * Reference:
 
* **Prototypical Explanations**
  * Intended Use: identify which parts of the model are contributing to the model’s decisions. This approach relies on human experts to identify prototypes for the explanation to use as a comparison, which can be a limitation of the approach
  * Rationale: 
  * Reference:

* **Availability of AI System Facts**
  * Intended Use: Include information from CHAI Applied Model Card. Binary (yes/no) response.
  * Rationale: There are more comprehensive evaluations but for pragmatic reasons we recommend the same evaluation metric for predictive and generative use cases.
  * Reference: [CHAI Applied Model Card](https://chai.org/draft-chai-applied-model-card/)


### Security and Privacy

*(additional detail for the Responsible AI Principle of Security and Privacy can be found in the CHAI RAIG)*

**Method/Metric:**

* **Consult security experts**
  * Intended Use: this may include folks such as Data Protection Officer in the planning phase to develop a data governance strategy.
  * Rationale: 
  * Reference:

* **Leverage industry security guidelines**
  * Intended Use: use security guidelines (e.g., NIST, ISO/IEC, OECD) and refine them with nuanced expert judgment.
  * Rationale: 
  * Reference:

* **Data Protection Impact Assessments (DPIA)**
  * Intended Use: conducting Data Protection Impact Assessments (DPIA) during the design phase.
  * Rationale: 
  * Reference:
 
* **Threat Modeling**
  * Intended Use: anticipate and prepare for potential breaches, including attacker incentives and impact evaluations.
  * Rationale: 
  * Reference:

* **Evaluation of the likelihood and impact of various attack vectors**
  * Intended Use:
  * Rationale: 
  * Reference:
 
* **Data Provenance Tracking**
  * Intended Use: ensure data integrity.
  * Rationale: 
  * Reference:
 
* **Numeric results from risk assessments**
  * Intended Use:
  * Rationale: 
  * Reference: e.g., likelihood and severity of attack scenarios
 
* **Outcomes of privacy preservation evaluations**
  * Intended Use:
  * Rationale: 
  * Reference: e.g., degree of compliance from DPIA


## Post-Deployment

*(additional detail for post-deployment stages of the AI lifecycle, can be found in the CHAI RAIG)*

### Usefulness, Usability, and Efficacy

*(additional detail for the Responsible AI Principle of Usefulness, Usability, and Efficacy can be found in the CHAI RAIG)*

**Method/Metric:**

* **Usability Testing and Heuristic Evaluation**
  * Intended Use: In addition to the intrinsic and extrinsic evaluation conducted in the pre-implementation stages, one must consider the user’s interaction with the system. Use usability testing and heuristic evaluation to evaluate the AI system's interface.
  * Rationale: 
  * Reference:

* **User satisfaction surveys**
  * Intended Use:
  * Rationale: 
  * Reference:
 
* **Home Ownership, Utilities, Savings, Employment, and Schooling (HOUSES) Index**
  * Intended Use: compare balanced error rate (BER) against different SES levels: The HOUSES index is used to measure SES in healthcare contexts. When applied to fairness metrics like BER, it compares the rate of errors across different SES levels. This helps assess whether an AI model's error rates are equitable across socioeconomic groups, identifying potential disparities in how different SES groups experience model performance (e.g., if low-SES groups are more likely to experience errors
  * Rationale: 
  * Reference:

* **System Usability Scale (SUS)**
  * Intended Use: can be conducted to measure end-user satisfaction
  * Rationale: 
  * Reference:
 
* **Potential Differential Performance Across Socioeconomic Statuses (SES)**
  * Intended Use: this metric refers to the possibility that an AI model or system performs differently based on the socioeconomic background of the users or subjects. It evaluates whether individuals from different SES levels (e.g., income, education, occupation) experience varying levels of accuracy, error rates, or outcomes from the system, potentially highlighting biases or inequities in how the system treats different socioeconomic groups
  * Rationale: 
  * Reference:

* **Parity: Equalized Odds**
  * Intended Use: prediction errors are distributed equally across different groups
  * Rationale: Equalized Odds Criterion ensures similar True Positive Rates and False Positive Rates across all demographic groups
  * Reference:

* **Parity: Equalized Opportunity**
  * Intended Use: prediction errors are distributed equally across the different groups, limited to the condition-positive individuals
  * Rationale: Equalized Opportunity Criterion could be used, which means ensuring only similar True Positive Rates across all demographic groups
  * Reference:
    

### Fairness, Equity, and Bias Management

*(additional detail for the Responsible AI Principle of Fairness, Equity, and Bias Management can be found in the CHAI RAIG)*

**Method/Metric:**

* **Comparative Biases**
  * Intended Use: Compare the biases of the general population, the specific population, and the data used
  * Rationale: 
  * Reference:

* **Implement a process for identifying and recognizing model drift**
  * Intended Use: three main types of drift that should be acknowledged, monitored and mitigated: concept drift, data drift, label drift.
  * Rationale: 
  * Reference:
 
* **balanced error rate (BER)**
  * Intended Use: 
  * Rationale: 
  * Reference:



### Safety and Reliability

*(additional detail for the Responsible AI Principle of Safety and Reliability can be found in the CHAI RAIG)*

**Method/Metric:**

* **False alarm rate**
  * Intended Use: specific quantitative measure of how often the algorithm generates false positives.
  * Rationale: 
  * Reference:

* **False negative rate**
  * Intended Use: specific quantitative measure of how often the algorithm fails to detect sepsis
  * Rationale: 
  * Reference:


### Transparency, Intelligibility, and Accountability

*(additional detail for the Responsible AI Principle of Transparency, Intelligibility, and Accountability can be found in the CHAI RAIG)*

**Method/Metric:**

* **Random Forest**
  * Intended Use: identify the 10 most important features used in predictions and send those features to users to determine where to start the evaluation to explain output; users can focus on the data elements that can change the least to impact the prediction class. Store all predictions of the model for a specified time period to allow for ongoing monitoring of performance degradation
  * Rationale: 
  * Reference:


### Security and Privacy

*(additional detail for the Responsible AI Principle of Security and Privacy can be found in the CHAI RAIG)*

**Method/Metric:**

* **Dynamic Post-implementation Audits**
  * Intended Use: include regularly updated security protocols based on new threats and emerging vulnerabilities.
  * Rationale: 
  * Reference:

* **Limiting Access to AI Models**
  * Intended Use: to mitigate privacy attacks, ensuring only authorized users have access to sensitive parts of the model and its output.
  * Rationale: 
  * Reference:
 
* **Intercepting AI Model Outputs**
  * Intended Use: leverage to counter security threats and prevent adversarial data extraction.
  * Rationale: 
  * Reference:

* **Input Filtering**
  * Intended Use: leverage to mitigate adversarial attacks, though acknowledging its potential weaknesses.
  * Rationale: 
  * Reference:
 
* **Authenticated Inputs or Inputs with Provenance**
  * Intended Use: leverage to defend against adversarial attacks, particularly in sensitive applications like imaging.
  * Rationale: 
  * Reference:
