# Capstone Project
## Early Signal Emergence in Effort, Skill, and Mastery

## Overview
This project investigates whether meaningful signals about student performance emerge before final course completion.

Using longitudinal assessment data, the project combines exploratory data analysis (EDA), prediction modeling, classification modeling, and intervention-oriented analysis to examine how effort, skill, and mastery evolve over instructional time.

The goal is to determine whether early patterns in student behavior can help inform earlier and more effective instructional interventions.

---

## Dataset
The dataset consists of longitudinal assessment records capturing student performance across multiple instructional steps, including:

- Stepwise attempt counts (`new_attempts_step_i`)
- Stepwise accuracy measures (`new_accuracy_step_i`)
- Outcome categories (wrong, quarter, half, full credit)
- Revision behavior (corrections, regressions, laterals)

The data is structured to track performance longitudinally across instructional steps.

---

## Exploratory Data Analysis (EDA)
EDA examines structural patterns in student learning behavior.

Key analyses include:

- Distribution of new work outcomes
- Distribution of revisions
- Mastery growth over time
- Mastery distribution across grade bands
- Relationship between effort and skill

### Key EDA Findings
- First-attempt outcomes are dominated by full credit, with meaningful partial credit structure.
- Revision behavior is primarily corrective.
- Mastery distribution begins to stabilize around Step 7 (mid-course).
- Effort and skill define multiple pathways to similar outcomes.

---

## Prediction Modeling

Ridge regression with polynomial features is used to evaluate predictive signal over instructional time.

Modeling includes:
- Cross-validated model selection (GridSearchCV)
- Stepwise prediction performance (MSE)
- Stepwise prediction performance (R²)
- Feature influence (Permutation Importance)
- Tiered prediction performance (MSE)
- Tiered prediction performance (R²)
- Tiered feature influence (Permutation Importance)

### Key Prediction Findings
- Prediction error decreases steadily across instructional steps.
- By approximately Step 7, final grades can be estimated with 9% average prediction error.
- By approximately Step 10, average prediction error decreases to roughly 7%.
- Predictive signal strengthens steadily and emerges well before final outcomes are observed.
- Effort and skill begin similarly but separate over time, with effort becoming increasingly influential for prediction.
- Prediction dynamics differ across performance tiers before converging later in instruction.

---

## Classification Modeling

Logistic regression with polynomial features is used to evaluate intervention-oriented classification signal over instructional time.

Modeling includes:
- Cross-validated model selection (GridSearchCV)
- Stepwise classification performance (ROC-AUC)
- Decision boundary and confusion matrix analysis
- Stepwise confusion count analysis

### Key Classification Findings
- Classification performance strengthens steadily across instructional steps.
- Meaningful intervention-oriented signal emerges well before final outcomes are observed.
- Most classification uncertainty occurs near the decision boundary.
- Effort and skill jointly produce interpretable intervention regions.

---

## Intervention Proof of Concept (POC)

This section explores whether prediction and classification outputs can be translated into interpretable intervention-oriented profiles.

Analyses combine predicted grade, classification risk, and behavioral mode summaries to examine structural differences between broad student archetypes.

### Key Intervention Findings
- Predicted grade and classification risk produce strong and interpretable separation across archetypes.
- Students classified as At Risk maintain substantially lower predicted grades and substantially higher estimated risk than students classified as Passing.
- Intervention-oriented signal remains visible after aggregation into broad intervention archetypes.
- Behavioral mode distributions differ meaningfully across archetypes, with students classified as At Risk exhibiting substantially lower SURGE behavior and elevated frequencies across all remaining behavioral modes.

---

## Conclusion
This project shows that student assessment data contains meaningful early signals of performance.

Key takeaways:
- Learning structure becomes visible before final outcomes.
- Meaningful prediction becomes possible around mid-course, with practical grade estimation emerging before instruction is complete.
- Effort and skill contribute differently over time, with effort becoming increasingly important for explaining later performance.
- Predictive signal emerges differently across performance groups before converging toward greater consistency later in instruction.
- Classification modeling produces stable intervention-oriented separation well before final outcomes are observed.
- Intervention-oriented profiles provide interpretable summaries of student behavior and projected outcomes.

These findings suggest clear value in earlier and more targeted instructional interventions, particularly as predictive and classification signals stabilize over instructional time.

---

## Key Visualizations

### Exploratory Data Analysis

#### New Work Distribution
![New Work Distribution](images/01_eda_new_work_distribution.png)

First-attempt outcomes are dominated by full credit while still preserving meaningful partial-credit structure. The distribution suggests substantial progress occurs immediately during initial exposure rather than relying primarily on later revision.

<br>

#### Revisions Distribution
![Revisions Distribution](images/02_eda_revisions_distribution.png)

Revision behavior is primarily corrective, indicating students more frequently improve prior outcomes than regress. This suggests that learning trajectories tend to move toward increasing mastery rather than fluctuating randomly over time.

<br>

#### Mastery Spread
![Mastery Spread](images/03_eda_mastery_spread.png)

Median mastery approaches the 40% threshold near Step 7, suggesting a midpoint transition in aggregate performance. The persistent spread indicates substantial variation in student trajectories.

<br>

#### Mastery Distribution
![Mastery Distribution](images/04_eda_mastery_distribution.png)

Grade-band structure stabilizes around Step 7, with the overall distribution taking shape well before the final steps. This indicates that performance patterns emerge earlier than final outcomes alone might suggest.

<br>

#### Effort and Skill Relationship
![Effort and Skill Relationship](images/05_eda_effort_skill_relationship.png)

Effort and skill define multiple pathways to similar outcomes. The geometry highlights that stronger performance requires alignment between both factors. 

<br>

### Prediction Modeling

#### Ridge GridSearchCV Heatmap
![Ridge GridSearchCV Heatmap](images/11_prediction_ridge_gridsearchcv_heatmap.png)

Cross-validation results indicate that low-degree polynomial ridge models provide strong and stable predictive performance while limiting unnecessary complexity.

<br>

#### Global Prediction Diagnostics
![Global Prediction Diagnostics](images/12_prediction_global_diagnostics.png)

Predicted and actual grades align closely, while residuals exhibit limited systematic structure. These diagnostics suggest the selected ridge model captures meaningful outcome structure while remaining sufficiently stable for later stepwise analysis. 

<br>

#### Stepwise Prediction Performance (MSE)
![Stepwise Prediction Performance (MSE)](images/13_prediction_stepwise_mse.png)

Prediction error decreases steadily throughout instruction, with substantial improvement emerging around the middle instructional steps. These results suggest meaningful grade estimation becomes possible well before final outcomes are observed.

<br>

#### Stepwise Prediction Performance (R²)
![Stepwise Prediction Performance (R²)](images/14_prediction_stepwise_r2.png)

Predictive signal strengthens steadily throughout instruction, with strong explanatory power emerging by approximately Step 7 and continuing to increase thereafter.

<br>

#### Stepwise Feature Influence (Permutation Importance)
![Stepwise Feature Influence (Permutation Importance)](images/15_prediction_stepwise_pi.png)

Feature influence evolves throughout instruction, with effort and skill beginning similarly before separating over later instructional steps. The increasing influence of effort suggests pacing-related behavior becomes progressively more informative for prediction as instruction advances. 

<br>

#### Tiered Prediction Performance (MSE)
![Tiered Prediction Performance (MSE)](images/16_prediction_tiered_mse.png)

Prediction error decreases across both performance tiers as additional instructional information becomes available. Although early prediction behavior differs across groups, prediction reliability steadily improves and becomes increasingly similar later in instruction.

<br>

#### Tiered Prediction Performance (R²)
![Tiered Prediction Performance (R²)](images/17_prediction_tiered_r2.png)

Predictive signal emerges differently across performance tiers, with stronger early explanatory power appearing within higher-performing trajectories before convergence later in instruction.

<br>

#### Tiered Feature Influence (Permutation Importance)
![Tiered Feature Influence (Permutation Importance)](images/18_prediction_tiered_pi.png)

Feature influence differs across performance tiers, with effort exhibiting stronger separation within higher-performing trajectories while remaining closer to skill within lower-performing trajectories.

<br>

### Classification Modeling

#### Logistic GridSearchCV Heatmap
![Logistic GridSearchCV Heatmap](images/21_classification_logistic_gridsearchcv_heatmap.png)

Cross-validation results indicate that low-degree polynomial logistic models provide strong and stable classification performance while limiting unnecessary complexity. 

<br>

#### Stepwise Classification Performance (ROC-AUC)
![Stepwise Classification Performance (ROC-AUC)](images/22_classification_stepwise_roc_auc.png)

Classification performance improves steadily throughout instruction, with meaningful intervention-oriented signal emerging well before final outcomes are observed.

<br>

#### Stepwise Confusion Counts
![Stepwise Confusion Counts](images/23_classification_stepwise_confusion_counts.png)

False negatives generally decrease over time while true positives remain consistently high, suggesting intervention reliability strengthens as additional instructional information accumulates.

<br>

#### Final Decision Boundary and Confusion Matrix
![Final Decision Boundary and Confusion Matrix](images/24_classification_final_decision_boundary_confusion_matrix.png)

The logistic decision surface produces strong overall classification performance while preserving realistic uncertainty near borderline trajectories.

<br>

### Intervention Proof of Concept (POC)

#### Archetype Counts
![Archetype Counts](images/31_intervention_archetype_counts.png)

Students separate into distinct intervention-oriented groups despite aggregation into only two broad archetypes. The distribution suggests predictive and classification outputs retain meaningful structure when translated into practical intervention categories. 

<br>

#### Average Archetype Grade Prediction
![Average Archetype Grade Prediction](images/32_intervention_archetype_pred_grade.png)

Predicted grade separates strongly across archetypes, with students classified as At Risk maintaining substantially lower expected performance than students classified as Passing. This suggests prediction outputs remain interpretable after aggregation into intervention-oriented profiles. 

<br>

#### Average Archetype Risk
![Average Archetype Risk](images/33_intervention_archetype_risk.png)

Estimated classification risk differs substantially across archetypes, indicating that intervention-oriented grouping preserves strong separation between lower-risk and higher-risk trajectories. 

<br>

#### Average Archetype Behavioral Modes
![Average Archetype Behavioral Modes](images/34_intervention_archetype_behavioral_modes.png)

Behavioral mode distributions differ meaningfully across archetypes. Students classified as At Risk exhibit substantially lower SURGE behavior and elevated frequencies across all remaining behavioral modes, with the strongest relative separation appearing in STALL behavior.



