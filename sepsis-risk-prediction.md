# Testing and Evaluation (T&E) Framework for Sepsis Risk Prediction

*(to be included in CHAI Applied Model Card)*

## Pre-Deployment

*(additional detail for pre-deployment stages of the AI lifecycle, can be found in the CHAI RAIG)*

### Usefulness, Usability, and Efficacy

*(additional detail for the Responsible AI Principle of Usefulness, Usability, and Efficacy can be found in the CHAI RAIG)*

Method:

* Ground Theory Analysis

Measure:

* Sequential Organ Failure Assessment (SOFA) score
* Risk ratio (outcome rate if exposed to AI model over outcome rate if not exposed to AI model)

Metric:

* Area under the curve (AUC)—receiver operating characteristic (ROC) (AUC-ROC)
* Area under the curve (AUC)—precision recall curve (PRC) (AUC-PRC)
* Precision (or Positive Predictive Value, PPV)
* Recall (or Sensitivity)
* Specificity
* F1 score
* Root Mean Squared Error (RMSE)
* Coefficient of Determination (R-squared)

### Fairness, Equity, and Bias Management

*(additional detail for the Responsible AI Principle of Fairness, Equity, and Bias Management can be found in the CHAI RAIG)*

Method:

* HOUSES index to compare balanced error rate (BER) against different socioeconomic status (SES) levels
* Use of interviews or qualitative approach to understand how biases could be introduced into the workflow
* Differential Missingness: Target label of interest might be collected differently as function of vulnerable subgroups
* Potential Differential Performance Across Socio-Economic Statuses (SES)

Measure:

* Parity: Equalized Odds (prediction errors are distributed equally across different groups) or Equalized Opportunity (prediction errors are distributed equally across the different groups, limited to the condition-positive individuals)

Metric:

* Area under the curve (AUC)—receiver operating characteristic (ROC) (AUC-ROC)
* Area under the curve (AUC)—precision recall curve (PRC) (AUC-PRC)
* Confusion Matrix
* Parity: Equalized Odds Criterion ensures similar True Positive Rates and False Positive Rates across all demographic groups
* Parity: Equalized Opportunity Criterion could be used, which means ensuring only similar True Positive Rates across all demographic groups

### Safety and Reliability

*(additional detail for the Responsible AI Principle of Safety and Reliability can be found in the CHAI RAIG)*

Method:

* Risk Framework: Assess the safety and reliability of predictive AI algorithms using a risk framework. Examples include: National Institute of Standards and Technology (NIST) Artificial Intelligence Risk Management Framework (AI RMF 1.0), ISO/IEC 23894:2024, ISO/IEC 42001:2023, CHAI Responsible AI Guide
* **Task Analysis:** Conduct a task analysis, failure modes and effects analysis (FMEA), or detailed walkthroughs to identify potential failure points.
* **Non-Inferiority Assessment:** Compare the AI system to clinician experts, particularly in cases where prioritization tools are used, to ensure adequacy.
* **Explainability:** Use explainability to evaluate generalizability, safety, and usability.
* **Human-in-the-Loop:** Ensure human involvement in high-risk situations for verification of AI outputs.

Measure:

* Percentage of Errors: Quantitative measure of errors over a given number of cases.
* Number of Successful Predictions: Quantitative measure of reliability (e.g., number of correct predictions over total cases).
* Implications of Inaccuracy: Outcomes such as poorer health outcomes or added stress on the healthcare workforce.
* Likelihood of Failure at Identified Failure Points: Measure developed and evaluated during pre-implementation.

Metric:

* Accuracy: Evaluate the correctness of the AI model's predictions (e.g., percentage of correct predictions).
* Reliability: Consistency of the AI model's performance.
* False Positives and False Negatives: Metrics for pre-implementation safety evaluation.
* Explainability Dimensions: Calibrated confidence scores; Clinical judgment of appropriateness for a given measure

### Transparency, Intelligibility, and Accountability

*(additional detail for the Responsible AI Principle of Transparency, Intelligibility, and Accountability can be found in the CHAI RAIG)*

Metric:

* Saliency Maps: highlight the important regions of the input data, such as images, that influenced the model’s decisions, but also consider the reliability of these maps and the rational for that region of the data being included
* Locally Interpretable Model-Agnostic Explanations (LIME) and Shapley Values (SHAP): understand what parts of the input data is influencing the model’s decisions but also consider that the approach does not always give a reason for the data influencing the model.
* Prototypical Explanations: to identify which parts of the model are contributing to the model’s decisions. This approach relies on human experts to identify prototypes for the explanation to use as a comparison, which can be a limitation of the approach

### Security and Privacy

*(additional detail for the Responsible AI Principle of Security and Privacy can be found in the CHAI RAIG)*

Method:

* Using security guidelines (e.g., NIST, ISO/IEC, OECD) and refining them with nuanced expert judgment.
* Consulting security-minded individuals and including a Data Protection Officer in the planning phase to develop a data governance strategy.
* Conducting Data Protection Impact Assessments (DPIA) during the design phase.
* Threat modeling to anticipate and prepare for potential breaches, including attacker incentives and impact evaluations.

Measure:

* Evaluation of the likelihood and impact of various attack vectors.
* Data provenance tracking to ensure data integrity.

Metric:

* Numeric results from risk assessments (e.g., likelihood and severity of attack scenarios).
* Outcomes of privacy preservation evaluations (e.g., degree of compliance from DPIA).

## Post-Deployment

*(additional detail for post-deployment stages of the AI lifecycle, can be found in the CHAI RAIG)*

### Usefulness, Usability, and Efficacy

*(additional detail for the Responsible AI Principle of Usefulness, Usability, and Efficacy can be found in the CHAI RAIG)*

Method:

* **Usability Testing and Heuristic Evaluation.** In addition to the intrinsic and extrinsic evaluation conducted in the pre-implementation stages, one must consider the user’s interaction with the system. Use usability testing and heuristic evaluation to evaluate the AI system's interface.
* **User satisfaction surveys**
* **Home Ownership, Utilities, Savings, Employment, and Schooling (HOUSES)** index to compare balanced error rate (BER) against different SES levels: The HOUSES index is used to measure SES in healthcare contexts. When applied to fairness metrics like BER, it compares the rate of errors across different SES levels. This helps assess whether an AI model's error rates are equitable across socioeconomic groups, identifying potential disparities in how different SES groups experience model performance (e.g., if low-SES groups are more likely to experience errors

Metric:

* **System Usability Scale (SUS):** can be conducted to measure end-user satisfaction
* **Potential Differential Performance Across Socio-Economic Statuses (SES):** this metric refers to the possibility that an AI model or system performs differently based on the socioeconomic background of the users or subjects. It evaluates whether individuals from different SES levels (e.g., income, education, occupation) experience varying levels of accuracy, error rates, or outcomes from the system, potentially highlighting biases or inequities in how the system treats different socioeconomic groups

Measure:

* **Equalized Odds** (prediction errors are distributed equally across different groups)
* **Equalized Opportunity** (prediction errors are distributed equally across the different groups, limited to the condition-positive individuals).

### Fairness, Equity, and Bias Management

*(additional detail for the Responsible AI Principle of Fairness, Equity, and Bias Management can be found in the CHAI RAIG)*

Method:

* **Comparative Biases:** Compare the biases of the general population, the specific population, and the data used
* **Implement a process for identifying and recognizing model drift:** three main types of drift that should be acknowledged, monitored and mitigated: concept drift, data drift, label drift.

Metric:

* **balanced error rate (BER)**

### Safety and Reliability

*(additional detail for the Responsible AI Principle of Safety and Reliability can be found in the CHAI RAIG)*

Metric:

* **False alarm rate:** A specific quantitative measure of how often the algorithm generates false positives.
* **False negative rate:** A quantitative measure of how often the algorithm fails to detect sepsis

### Transparency, Intelligibility, and Accountability

*(additional detail for the Responsible AI Principle of Transparency, Intelligibility, and Accountability can be found in the CHAI RAIG)*

Method:

* **Random forest:** to identify the 10 most important features used in predictions and send those features to users to determine where to start the evaluation to explain output; users can focus on the data elements that can change the least to impact the prediction class
* Store all predictions of the model for a specified time period to allow for ongoing monitoring of performance degradation

### Security and Privacy

*(additional detail for the Responsible AI Principle of Security and Privacy can be found in the CHAI RAIG)*

Method:

* **Dynamic post-implementation audits** with regularly updated security protocols based on new threats and emerging vulnerabilities.
* **Limiting access to AI models** to mitigate privacy attacks, ensuring only authorized users have access to sensitive parts of the model and its output.
* **Intercepting AI model outputs** to counter security threats and prevent adversarial data extraction.
* **Input filtering** to mitigate adversarial attacks, though acknowledging its potential weaknesses.

**Authenticated inputs or inputs with provenance** to defend against adversarial attacks, particularly in sensitive applications like imaging.
