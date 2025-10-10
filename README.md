# Paroxysmal Nocturnal Hemoglobinuria (PNH) Closer Monitoring Models

Paroxysmal Nocturnal Hemoglobinuria (PNH) is a very rare and complex blood disorder that is both difficult to diagnose and manage. 

The goal of the following two PNH Closer Monitoring Models is to help healthcare providers monitor patients more closely to reduce ongoing anemia and prevent organ dysfunction and dangerous blood clots.

<B>Model Descriptions:</B><BR>
We developed two models, designed to be used sequentially for patients diagnosed with PNH.<BR><BR>
A) <B>Pre-Treatment Model</B> (<A HREF="https://github.com/atroposhealth/pnh-progression-monitoring/blob/main/PNH_Progression_Monitoring_Pre_Treatment.xgb">PNH_Progression_Monitoring_Pre_Treatment.xgb</A>)<BR><BR>
   <B>Patients</B>: This model is for patients who have a PNH diagnosis (ICD-10 D59.5) but do not have a diagnosis of bone marrow failure (aplastic anemia or myelodysplastic syndrome).<BR>
   <B>Prediction Target</B>: The risk of developing thrombosis, organ dysfunction, or anemia.<BR>
   <B>Key Features</B>: The model uses the following patient data. For technical definitions, refer to the <A HREF="https://github.com/atroposhealth/pnh-progression-monitoring/blob/main/PNH_Progression_Monitoring_Feature_Dictionary.xlsx">feature dictionary</A>.
   <OL>
      <LI>Prior thrombosis</LI>
      <LI>Charlson comorbidity index</LI>
      <LI>Age</LI>
      <LI>Most recent hemoglobin lab value (last 6 months)</LI>
      <LI>Acute kidney injury diagnosis (last 24 months)</LI>
      <LI>Office visit count (last 3 months)</LI>
      <LI>History of congestive heart failure</LI>
   </OL>
<BR>
B) <B>Ongoing Treatment Model</B> (<A HREF="https://github.com/atroposhealth/pnh-progression-monitoring/blob/main/PNH_Progression_Monitoring_Ongoing_Treatment.xgb">PNH_Progression_Monitoring_Ongoing_Treatment.xgb</A>)<BR><BR>
   <B>Patients</B>: This model is for patients who have already started PNH treatment with one of the following medications: eculizumab, ravulizumab, iptacopan, pegcetacoplan, or danicopan.<BR>
   <B>Prediction Target</B>: The risk of worsening hemolytic anemia.<BR>
   <B>Key Features</B>: The model uses the following patient data. For technical definitions, refer to the <A HREF="https://github.com/atroposhealth/pnh-progression-monitoring/blob/main/PNH_Progression_Monitoring_Feature_Dictionary.xlsx">feature dictionary</A>.
   <OL>
      <LI>Average hemoglobin lab value (last 3 months)</LI>
      <LI>Average alanine aminotransferase (ALT) lab value (last 3 months)</LI>
      <LI>Most recent creatinine lab value (last 12 months)</LI>
      <LI>Most recent total bilirubin lab value (last 24 months)</LI>
      <LI>Chest pain diagnosis (last 24 months)</LI>
   </OL>


<B>Technical Deployment</B><BR>
The model was developed using XGBoost, a powerful machine learning algorithm. A portable XGBoost model is provided and can be used with the XGBoost package in languages such as Python or R.

<B>Model Performance and Validation</B><BR>
The model was trained on electronic health record (EHR) data from 67 million patients in the United States between 2016 and 2023. 
The model produces a continuous risk score. You will need to test and set the threshold for further clinical action within your own local environment.
The models were each tested on >330 candidate predictive features; the included features performed as well as the full models.
In the independent validation dataset (25%), the following were observed: 

| Model  | AUROC | AUPRC |
| :--- | ---: | ---: |
| Pre-Treatment | 0.76 | 0.67 |
| Ongoing | 0.76 | 0.42 |

<I>AUROC (Area Under the Receiver Operating Characteristic) and AUPRC (Area Under the Precision-Recall Curve) are common metrics for evaluating model performance.</I>

<B>Physician Review</B><BR>
To further review the models, two physicians reviewed data for 50 patients for each model and were asked to identify which patients required closer monitoring. The results are as follows:

| Model  | Threshold* | Sensitivity | Positive Predictive Value |
| :--- | ---: | ---: | ---: |
| Pre-Treatment | 0.20 | 93% | 93% |
| Ongoing | 0.15 | 83% | 80% |

<span style="color: red;"><I><B>Note: Threshold selection should be independently tested within local clinical/operating context.</B></I></span>
