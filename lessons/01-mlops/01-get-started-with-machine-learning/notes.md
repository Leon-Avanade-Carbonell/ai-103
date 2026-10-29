# Get started with machine learning in Azure

- Module ID: M01
- Source: https://learn.microsoft.com/en-us/training/modules/design-machine-learning-model-training-solution/
- Curriculum verified: 2026-10-28
- Exam objectives: D1 resources; D2 training and deployment foundations.
- Quiz history: [quizzes.md](quizzes.md)

## Overview and learning goals

Planned source goals: design a solution to get and prepare data, choose a service and compute for training, and prepare for deployment options. These are learning goals, not completed learning.

## Notes by Microsoft Learn unit

### M01-U01 — Introduction
Source: https://learn.microsoft.com/en-us/training/modules/design-machine-learning-model-training-solution/1-introduction

Source verified: 2026-10-28; page updated 2026-08-27.

#### The machine learning lifecycle

Microsoft Learn describes six steps:

1. **Define the problem:** establish what to predict and what counts as success.
2. **Get data:** obtain access to relevant data sources.
3. **Prepare data:** explore, clean, and transform the data.
4. **Train the model:** learn patterns and experiment with training choices.
5. **Integrate the model:** make predictions available to applications.
6. **Monitor the model:** assess whether it continues to meet its intended goals.

The lifecycle is iterative and continuous. Deployment is not the end: monitoring can lead back to earlier steps, including retraining. Design choices affect cost, speed, quality, and longevity.

#### Monitoring and evidence-based retraining

**Tutor illustration:** a retailer's demand forecasts may deteriorate when buying habits change. Compare predictions with actual outcomes and agreed success criteria. Changed behavior alone does not prove that predictions have degraded, and strong sales are not the same as accurate forecasts.

A useful reasoning principle is to gather enough evidence before retraining to avoid acting for the wrong reason. Seasonality, malicious activity, and modeling problems are possible hypotheses to investigate, not established causes. If forecasts still meet the accuracy target, continued monitoring is a reasonable response; if they no longer meet it, investigate and revisit the relevant lifecycle steps.

### M01-U02 — Define the problem
Source: https://learn.microsoft.com/en-us/training/modules/design-machine-learning-model-training-solution/2-identify-tasks

Source verified: 2026-10-28; page updated 2026-08-27. Supporting metric reference: [Understand automated machine learning results](https://learn.microsoft.com/en-us/azure/machine-learning/how-to-understand-automated-ml?view=azureml-api-2), verified 2026-10-28, updated 2026-10-19; Azure ML API v2 documentation.

#### Choose the task from the required output

Problem definition establishes the desired output, the ML task, and success criteria. The task constrains suitable algorithms and evaluation metrics.

| Task | Required output or data setup |
| --- | --- |
| Classification | A category, such as default/no default or late/on time |
| Regression | A numerical value, such as a selling price or delivery duration |
| Time-series forecasting | Future numerical values based on time-series data |
| Computer vision | Analysis of images, including object detection |
| Natural language processing | Insights extracted from text |

**Tutor illustrations:** estimating a house's dollar selling price from its features is regression; predicting whether it sells above $300,000 requests a categorical output and fits classification. A regression prediction can also be thresholded into a final category, but the required output must still be explicit. Predicting a future sale does not by itself establish time-series forecasting: the time-series setup matters.

Historical data is useful for multiple tasks. Choose regression because the requested output is numerical, not merely because past data exists or computation is involved. ML regression also differs from software regression testing.

#### Training, scoring, and evaluation

The official unit's workflow is:

**Load/import and inspect → preprocess/normalize and clean → split training/test data → choose/configure an algorithm → train → score → evaluate.**

- **Training** learns patterns from training examples and can be repeated with different choices.
- **Scoring** applies a trained model to examples to generate predictions.
- **Evaluation** compares predictions with actual outcomes and calculates performance metrics.

Producing a prediction for every example establishes that scoring produced outputs; it does not establish predictive quality. Evaluation must compare the appropriate metric with the acceptance threshold.

#### Held-out data versus representative data

**Tutor extension of the split step:** testing on the same examples used for training can overstate generalization because a model may fit their particular quirks—overfitting. Held-out data checks performance on examples not used to train the model.

Representativeness is a separate concern. Holding out city apartments does not establish performance on rural farmhouses absent from both training and test data. Evaluate relevant farmhouse examples for the intended use; this may reveal a need for better training coverage. The numerical price task can still use mean absolute error (MAE). Population mismatch does not automatically require a different metric. The farmhouse scenario is a tutor illustration, not the official unit's example.

#### Match metrics to success criteria

The supporting Azure ML API v2 reference provides the metric definitions and cautions about imbalanced classes:

- **Precision:** correctly flagged positives / all flagged positives. For borrower default, it asks how many flagged borrowers actually defaulted.
- **Recall:** correctly flagged positives / all actual positives. It asks how many actual defaults were detected.
- **Accuracy:** correct classifications / all examples. It can be high even when a model misses a minority class entirely.
- **Absolute error:** the magnitude of predicted minus actual numerical value.
- **MAE:** the mean of absolute errors across evaluated examples.

Recall is a ratio, not an exact count. Precision concerns reliability among positive flags and is relevant to reducing false alarms among them; recall concerns coverage of actual positives. Label the positive class and each population before calculating.

Compare the metric named in the requirement with its threshold. “At least 80% recall” includes equality; “MAE no greater than $15,000” requires MAE at or below that value. A different metric cannot substitute for the stated criterion.

### M01-U03 — Get and prepare data
Source: https://learn.microsoft.com/en-us/training/modules/design-machine-learning-model-training-solution/2a-prepare-data

Source verified: 2026-10-28; page updated 2026-08-27.

#### From source data to a training representation

Data quantity and quality affect model accuracy. Identify:

1. **Source:** where the data originates, such as CRM, SQL, or IoT devices.
2. **Current format:** structured, semi-structured, or unstructured. Incoming IoT JSON is semi-structured.
3. **Desired training format and serving layer:** what the training service needs and where prepared data will be available.
4. **Ingestion process:** the movement and transformation tasks that produce that representation.

Copying raw files is not necessarily sufficient preparation. Cleaning and removing unnecessary columns can help, but grouping and aggregation are needed when the required row granularity differs from the incoming readings.

#### Official IoT example architecture

The unit converts JSON temperature measurements into a table containing **average temperature per machine per minute**:

**Source → Azure Synapse Analytics copying/transformation → Azure Blob Storage prepared data → Azure Machine Learning training.**

Blob Storage is the prepared-data serving layer in this example. This is a common approach, not a mandatory architecture for every solution. The source also names Azure Databricks and Azure Machine Learning as options for ingestion pipelines.

#### Ingestion order and scheduling

An ingestion pipeline is a sequence of data movement and transformation tasks. It can be triggered manually or scheduled.

- **ETL:** extract → transform → load. Convert raw measurements to the desired table before loading that prepared table into storage.
- **ELT:** extract → load → transform. Load the data before performing the transformation.

**Tutor application:** recurring daily training can use scheduled ingestion to prepare the previous day's readings. The prepared table should be ready before training begins.

**Tutor extension on failure handling:** if preparation fails, wait and investigate rather than train on arbitrary available files. A failure might concern copying, access, or transformation; it does not prove the data itself is broken. A deliberately designed fallback using an older validated dataset differs from arbitrary-file training. These readiness/failure examples are conceptual illustrations, not an executed orchestration exercise or an explicit source mandate.

### M01-U04 — Train the model
Source: https://learn.microsoft.com/en-us/training/modules/design-machine-learning-model-training-solution/3-choose-service-train

Source verified: 2026-10-29; page updated 2026-08-27. Studied conceptually on 2026-10-29; no code or training job executed.

#### Select a service for the broader workflow

Microsoft Learn identifies model type, required training control, available time, existing organizational services, and programming-language preference as selection factors.

| Service | Source-described role |
| --- | --- |
| Azure Machine Learning | Train/manage models through studio, Python SDK, or CLI; support the end-to-end ML lifecycle. |
| Azure Databricks | Distributed Spark-based data engineering and data science; train/manage models or integrate with Azure Machine Learning. |
| Microsoft Fabric | Integrated analytics: prepare data, train models, generate predictions, and visualize data in Power BI reports. |
| Foundry Tools | Prebuilt model APIs for common tasks such as object detection; some models support customization with training data. |

**Tutor decision rules:** investigate applicable prebuilt models before assuming custom training is necessary, then evaluate suitability. Existing Spark workflows strengthen the case for Databricks. Several services can support training: select based on the broader workflow rather than treating training as exclusive to Azure Machine Learning.

#### Azure Machine Learning capabilities

The source describes data exploration/preparation, training/evaluation, registration/model management, deployment, and responsible AI assessment. Supporting capabilities include centralized datasets, on-demand compute, AutoML, orchestrated pipelines, MLflow integration, and explainability/fairness tools.

- **AutoML:** runs multiple training jobs with different algorithms and parameters to find a suitable model for the data.
- **Pipelines:** orchestrate steps for processes such as training or inferencing.
- **Tutor synthesis:** workflow orchestration and training-choice exploration are complementary; a coordinated workflow can include AutoML. This is a conceptual illustration, not an executed configuration.
- **Code-first access:** Python preference is compatible with the Python SDK; the visual studio interface is not mandatory.

### M01-U05 — Use Azure Machine Learning studio
Source: https://learn.microsoft.com/en-us/training/modules/design-machine-learning-model-training-solution/3b-use-automated-machine-learning

Source verified: 2026-10-29; page updated 2026-08-27. The following material was discussed conceptually; no workspace, compute resource, notebook, or training job was created or executed.

#### Studio, workspace, and compute are distinct

Microsoft Learn describes **studio** as the browser-based interface for managing ML resources and jobs. A **workspace** is the primary Azure Machine Learning resource, provisioned in an Azure subscription. **Compute** supplies the computational resources needed to execute work such as training.

Studio supports exploring data, running notebooks, creating jobs and pipelines, using AutoML, inspecting trained-model results, and deploying models. Opening studio does not itself create a workspace: create one or access an existing workspace.

**Tutor illustration:** a laptop browser opens studio, accesses a team's workspace, and submits a training job to Azure compute. The browser provides the interface; the selected Azure compute executes that job. This is not a claim that every possible ML workflow must run remotely.

#### Choose compute, then monitor the choice

The official unit gives these starting points:

| Choice | Consideration |
| --- | --- |
| CPU | Often sufficient and cost-effective for smaller tabular datasets. |
| GPU | Often more efficient for image or text workloads; can also help larger tabular workloads when CPUs are insufficient. |
| General purpose | Balanced CPU-to-memory ratio, useful for testing and development with smaller datasets. |
| Memory optimized | Higher memory-to-CPU ratio for memory-heavy processing. |

Monitor **training duration and compute utilization** to guide resource adjustments. The initial choice is not a guarantee of sufficient performance and need not remain fixed.

#### AutoML simplifies experiments, not approval

The unit describes an AutoML wizard in studio for configuring and running training experiments without writing training code. AutoML automates iterative model-development work; the earlier training unit describes its exploration of algorithms and parameters.

**Tutor synthesis:** suitable data and a defined problem are still needed. A trained artifact does not prove suitability for production: evaluate the results before approving deployment. Automation of training choices does not remove the need to judge model quality against application needs.

### M01-U06 — Integrate a model
Source: https://learn.microsoft.com/en-us/training/modules/design-machine-learning-model-training-solution/4-decide-between-compute-options

Source verified: 2026-10-29; page updated 2026-08-27. Studied conceptually; no model, endpoint, compute, SDK, CLI, or configuration was executed.

#### Deploy a model to an endpoint

Microsoft Learn introduces an endpoint as an address an application can call to use a deployed model for predictions. Integration requirements should be considered while designing training and selecting data.

- **Real-time predictions:** score new input when a quick response is needed. The official example recommends products immediately after a shopper selects a shirt; a purchase is not required to supply the selection input.
- **Batch predictions:** score collected data and save combined results in a file or database for later consumption. The official example generates weekly orange-juice sales forecasts for a report.

Training learns patterns to produce a model; scoring runs an already-trained model to generate predictions. Training on a collection of historical data is not itself batch prediction.

#### Decide between real-time or batch deployment

The source asks how often predictions should be generated, how soon results are needed, whether inputs are scored individually or in batches, and how much compute prediction execution needs.

**Identify the necessary frequency of scoring:** data arrival frequency does not determine prediction timing. Ask when the consumer needs the output and how much delay is acceptable. Scheduled consumption can allow batch scoring even when readings arrive every second.

**Decide on the number of predictions:** individual scoring can use one customer row or image; batch scoring can process a customer table or collection of images and collate predictions. Input quantity is a consideration alongside timing, not a substitute for the response-time requirement.

#### Consider the cost of compute

Prediction execution needs compute as well as training. Training resources do not automatically become the deployed model's serving resources: plan prediction compute and availability separately. This does not prohibit infrastructure reuse where supported.

- **Real-time:** ready compute capacity supports quick responses, with an availability cost between requests. The source illustrates container-based serving using ACI/AKS; these examples are not a verified current deployment recipe or a requirement to select either service.
- **Batch:** a compute cluster can process batches in parallel across nodes. When configured to scale idle nodes down to zero, it can reduce idle node costs. Scaling down nodes does not imply every associated Azure cost disappears.

These are foundational deployment/cost patterns, not hands-on coverage of managed online or batch endpoint provisioning. No SDK version or executable configuration was verified in this conceptual lesson.

### M01-U07 — Module assessment
Source: https://learn.microsoft.com/en-us/training/modules/design-machine-learning-model-training-solution/6-knowledge-check

Website-only. Use the Microsoft Learn source link above independently. The tutor skips this closing unit; it is excluded from tutor completion, review scheduling, and TLDR readiness. No website confirmation is required.

### M01-U08 — Summary
Source: https://learn.microsoft.com/en-us/training/modules/design-machine-learning-model-training-solution/7-summary

Website-only. Use the Microsoft Learn source link above independently. The tutor skips this closing unit; it is excluded from tutor completion, review scheduling, and TLDR readiness. No website confirmation is required.

## Key concepts and decision points

- **M01-U01:** use monitoring evidence against success criteria to decide whether to revisit the lifecycle.
- **M01-U02:** define the output, select the task, and specify the appropriate metric and acceptance threshold before judging results.
- **M01-U02:** distinguish learning patterns (training), generating predictions (scoring), and measuring quality (evaluation).
- **M01-U03:** design ingestion around the required training representation and granularity, not simply around moving raw files.
- **M01-U04:** use model needs, control, time, existing platforms, and language preferences to select services; AutoML explores training choices while pipelines coordinate steps.
- **M01-U05:** distinguish studio (interface), workspace (Azure resource), and compute (execution resources); use observed training time and utilization to revisit compute choices.
- **M01-U06:** choose prediction timing from consumer needs, not data arrival frequency; budget compute for prediction execution as well as training.

These concepts connect to D1 data infrastructure and D2 training, evaluation, and lifecycle foundations.

## Python examples
Pending study. Record prerequisites/versions, expected outcomes, and execution status.

## JavaScript examples
Pending study. Use relevant supported examples only.

## Azure CLI commands
Pending study. Record CLI/extension prerequisites and expected outcomes.

## Related configuration: YAML, Bicep, or GitHub Actions
Pending study.

## Worked examples and practice

The following are tutor-created numerical illustrations of the studied concepts. They were discussed conceptually; no code, Azure job, SDK, CLI, or lab was executed. They are worked reference examples, not assessment records.

### M01-U02 — Absolute error and MAE

A prediction of $240,000 for a house that sells for $260,000 has absolute error:

**|$240,000 − $260,000| = $20,000.**

For multiple houses, calculate each absolute error and then average them. Generating the predicted prices is scoring; calculating error against actual prices is evaluation.

### M01-U02 — Precision, recall, and an acceptance threshold

Of 200 transactions, 20 are actual frauds. A model flags 30 transactions, of which 15 are frauds:

- Precision = 15 / 30 = **50%**.
- Recall = 15 / 20 = **75%**.
- A requirement of at least 80% fraud recall is **not met**.

In a separate scenario with 10 actual frauds, 20 flags, and 8 correctly flagged frauds, precision is 8/20 = **40%** and recall is 8/10 = **80%**. The recall requirement is met because equality counts. Keep the populations and numbers from each scenario separate; total transactions is neither denominator here.

### M01-U02 — Accuracy can hide missed positives

Of 100 deliveries, 10 are late. Predicting “on time” for every delivery gives:

- Accuracy = 90 / 100 = **90%**.
- Late-delivery recall = 0 / 10 = **0%**.
- A requirement of at least 80% late recall is **not met**, despite high accuracy.

### M01-U03 — One row per machine-minute

**Task:** several valid readings arrive within the same minute for the same machine; training requires one mean-temperature row for that machine-minute.

Group by machine and minute, then calculate the mean:

- 20°C and 22°C → (20 + 22) / 2 = **21°C**, stored in one row.
- 18°C, 21°C, and 24°C → (18 + 21 + 24) / 3 = **21°C**, stored in one row.

Removing columns or cleaning values alone does not produce the required granularity. Aggregation combines multiple readings into the required single row.

### M01-U04 — Service and training-workflow selection practice

Tutor-created conceptual tasks, discussed without executing code or Azure resources:

1. **Rapid object-detection feature, no custom-training requirement:** investigate Foundry Tools for an applicable prebuilt model, then evaluate suitability.
2. **Custom-data training, algorithm comparison, model retention, deployment, and Python preference:** Azure Machine Learning fits the lifecycle and offers a Python SDK. Databricks is also a candidate, especially with an existing Spark workflow; the best choice requires organizational context.
3. **Explore several algorithms without manually configuring every run:** use AutoML for training-choice exploration; a pipeline can coordinate preparation, training, and evaluation steps around that work.

### M01-U05 — Studio and compute selection practice

Tutor-created conceptual examples; no Azure resources or training jobs were executed. Actual execution would require an Azure subscription, an accessible workspace, and appropriate access to compute.

- **Small customer-record table, no image or text processing:** start with CPU compute as a generally sufficient, cost-effective option; monitor training time and utilization before adjusting resources.
- **Prepared data and a need to explore training choices without writing each experiment:** use studio's AutoML wizard, then evaluate the trained model's results before deployment approval.
- **Browser-based management:** opening studio neither creates a workspace automatically nor makes a submitted Azure training job run on the laptop's CPU.

### M01-U06 — Prediction timing and compute practice

Tutor-created conceptual examples; no resources or code executed:

- **Minute-by-minute factory readings, report needed at 7 a.m.:** collect and score readings in batch before the report is consumed. Immediate prediction for every reading is unnecessary for this requirement.
- **Product recommendations during a page visit:** use real-time predictions. Overnight batch processing cannot supply recommendations during that visit, although a separate overnight reporting workload could use batch.
- **One sensor stream, two consumers:** immediate overheating warnings fit real-time predictions; a weekly maintenance report can use batch. Different output requirements can justify different patterns using the same source stream.
- **Infrequent requests requiring immediate responses:** low request volume does not justify delaying predictions overnight. Plan ready serving capacity and its cost.

#### Saved model, separate execution jobs

Tutor-created worked example; conceptual only, with no code or compute executed:

1. A retailer uses labeled historical customer examples to learn model parameters and save a new model: **training**.
2. A later job loads that model, predicts outcomes for 20,000 current customers, and saves the combined predictions for tomorrow's report: **batch scoring**. It does not update the model merely by processing a large table.
3. A website requiring immediate responses throughout business hours needs serving capacity ready during those hours. Waiting for the next training run or an after-hours batch would violate that timing requirement.
4. A nightly cluster that scores a saved demand model for 500 stores can scale idle nodes to zero after saving predictions. The morning report reads stored results; keeping those results available does not require the scoring nodes to keep executing. Storage and other associated costs may remain.

The reporting purpose explains when predictions are consumed; applying a saved model explains why the operation is scoring. A batch-scoring job and a training job may both use clusters, but their purpose—not the word “cluster”—distinguishes them.

## Common pitfalls and clarifications

- **Business results versus model performance:** good sales do not demonstrate accurate forecasts.
- **Required output versus implementation:** a numerical prediction can be thresholded into a category, but that does not make the output requirement ambiguous.
- **Future prediction versus forecasting setup:** a future date alone does not establish time-series forecasting.
- **Held-out versus representative:** unseen examples still need to represent the intended use.
- **Precision versus recall:** predicted-positive and actual-positive denominators answer different questions.
- **Cleaning versus aggregation:** making individual readings cleaner does not necessarily produce one row per required group.
- **Preparation failure versus invalid data:** access, copying, and transformation failures require investigation; do not assume a single cause.
- **Fabric versus Azure Machine Learning:** both support training, but Fabric is the source's integrated analytics-to-Power BI platform; Azure Machine Learning focuses on the ML lifecycle.
- **AutoML versus pipelines:** training-choice exploration and workflow orchestration address different needs and can be combined.
- **Prebuilt versus suitable:** a prebuilt model still needs evaluation against application requirements.
- **Studio versus workspace versus compute:** a management interface is not the resource it manages or the hardware executing the job.
- **Training completion versus deployment readiness:** producing a model artifact does not establish its suitability for production.
- **Training versus batch scoring:** a week's training data does not make training a batch-prediction operation; batch scoring uses a trained model to generate outputs for collected inputs.
- **Collection timing versus consumption timing:** rapid sensor arrivals can support a weekly batch report; immediate action requires a different prediction timing decision.
- **Training compute versus serving compute:** deployment execution and availability need explicit planning; they are not automatically supplied by the existence of a training job.

## Microsoft Learn search terms
- Azure Machine Learning training compute selection
- machine learning problem definition data preparation
- Azure Machine Learning model deployment options
