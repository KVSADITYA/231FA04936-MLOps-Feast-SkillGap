CURRICULUM-INDUSTRY SKILL FEATURE STORE USING FEAST
====================================================

STUDENT DETAILS
---------------
Name: K.V.S. Aditya
Register Number: 231FA04936
Section: 9
Branch: CSE
Year: 4th Year

REPOSITORY NAME
---------------
231FA04936-MLOps-Feast-SkillGap


PROBLEM STATEMENT
-----------------
CSE graduates may have academic knowledge but still have gaps between
curriculum-based skills and skills expected by the IT industry.

This project converts a self-created curriculum-industry skill-gap dataset
into a Feast feature store and uses the stored features for a simple
machine-learning prediction.


DATASET
-------
Number of skills: 8

Skills:
1. Programming
2. Databases
3. Cloud Computing
4. Data Analysis
5. Problem Solving
6. Communication
7. Teamwork
8. Aptitude

The target variable is:
Skill_Gap_Category

Target categories:
- Low
- Medium
- High

The dataset contains synthetic CSE student records. Each entry was generated
with varied academic indicators, curriculum skill scores and industry
requirements. The dataset is intended for initial project implementation
and does not represent real student records.


FEATURE ENGINEERING
-------------------
The feature dataset is created from the original student skill-gap dataset.

Programming_Gap
Industry Programming score minus Curriculum Programming score.

Database_Gap
Industry Database score minus Curriculum Database score.

Cloud_Gap
Industry Cloud score minus Curriculum Cloud score.

DataAnalysis_Gap
Industry Data Analysis score minus Curriculum Data Analysis score.

ProblemSolving_Gap
Industry Problem Solving score minus Curriculum Problem Solving score.

Communication_Gap
Industry Communication score minus Curriculum Communication score.

Teamwork_Gap
Industry Teamwork score minus Curriculum Teamwork score.

Aptitude_Gap
Industry Aptitude score minus Curriculum Aptitude score.

Average_Curriculum_Score
Average of all curriculum skill scores.

Average_Industry_Requirement
Average of all industry requirement scores.

Calculated_Overall_Gap
Average of all individual skill gaps.

Skill_Readiness_Score
A readiness value calculated from the overall skill gap.


FEAST ARCHITECTURE
------------------
Original Dataset
       |
       v
Feature Engineering
       |
       v
Parquet Offline Data
       |
       v
Feast FeatureView
       |
       +--------------------------+
       |                          |
       v                          v
Historical Feature Retrieval   Materialization
       |                          |
       v                          v
Model Training                Online Store
                                  |
                                  v
                           Online Retrieval
                                  |
                                  v
                              Prediction


IMPLEMENTATION
--------------
Entity
The Feast entity is Student.
The join key is student_id.

Data Source
A local Parquet FileSource is used as the offline feature source.

FeatureView
The FeatureView is named student_skill_features.
It stores academic indicators, curriculum scores, industry requirements,
individual skill gaps, calculated overall gap and readiness features.

Historical Retrieval
get_historical_features() retrieves point-in-time feature values from the
offline store.

Model
A Logistic Regression model is trained using features retrieved through Feast.

Online Retrieval
After materialization, get_online_features() retrieves the latest stored
features for a student.

Prediction
The retrieved Feast features are supplied to the trained model to generate
a skill-gap category prediction.


REQUIRED ANALYSIS
-----------------
1. What is the entity in your Feast implementation?

The entity is Student, with student_id as the join key.

2. List the features stored in your FeatureView.

The FeatureView contains academic indicators, curriculum scores, industry
requirements, individual skill gaps, average curriculum score, average
industry requirement, calculated overall gap and skill-readiness score.

3. Explain how one feature was calculated.

Programming_Gap is calculated as:

Programming_Gap = Programming_Industry - Programming_Curriculum

A positive value means the industry requirement is higher than the student's
curriculum score.

4. What is the difference between the original dataset and the feature dataset?

The original dataset contains the source student records. The feature dataset
contains engineered ML features together with the Feast entity key and
timestamps.

5. What is the purpose of the offline store?

The offline store keeps historical feature data used for training and
historical feature retrieval.

6. What is the purpose of the online store?

The online store keeps materialized feature values that can be retrieved
quickly for prediction.

7. What is the purpose of feast apply?

feast apply registers the Feast entities, feature views and related definitions
in the Feast registry.

8. What does materialization do?

Materialization loads feature values from the historical source into the
online store.

9. What is the advantage of retrieving features through Feast instead of
manually calculating them separately during training and prediction?

Feast provides a consistent feature definition and retrieval mechanism between
training and prediction, reducing the possibility of calculating different
feature values in different stages.

10. State two limitations of your current dataset.

First, the dataset is synthetic and may not represent real student performance.

Second, the industry requirements are simulated and may not fully represent
current hiring-market requirements.

11. State two ways your feature store could be improved when more curriculum
and industry evidence becomes available.

First, verified industry skill requirements and job-posting information can be
added.

Second, real student assessment data can be incorporated and the feature store
can be updated regularly.


RESULTS
-------
After executing the notebook, include the following outputs in the repository
or report:

1. Historical feature output: The historical retrieval successfully fetched a DataFrame with a shape of (180, 36). This includes the 180 student records joined with their corresponding 36 feature columns (such as Skill_Gap_Category, Average_Curriculum_Score, event_timestamp, etc.) from the offline store.
2. Model accuracy: The logistic regression model achieved an accuracy of 88.89%.
3. Online feature output: The online store successfully returned the latest materialized feature values for a single student. The retrieved output is a DataFrame with 1 row and 34 columns for the student ID CSE26035.
4. One final prediction: Using the features retrieved from the online store, the model's final predicted skill-gap category for student CSE26035 is Low.


HOW TO RUN
----------
1. Open MLOps_Feast_SkillGap_Implementation.ipynb in Google Colab.
2. Run the cells from top to bottom.
3. When requested, upload:
   CSE_Employability_Skill_Gap_Unique_Dataset.csv
4. Allow feast apply to register the definitions.
5. Capture the historical retrieval, model accuracy, online retrieval and
   final prediction outputs.
6. Save the executed notebook.
7. Upload the complete project folder to the GitHub repository.


PROJECT FILES
-------------
MLOps_Feast_SkillGap_Implementation.ipynb
README.md
requirements.txt
.gitignore
data/CSE_Employability_Skill_Gap_Unique_Dataset.csv
