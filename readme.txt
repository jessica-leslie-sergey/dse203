CONTENTS OF THIS FILE
---------------------

1. Project Title
2. Project Description
3. Datasets
4. How to Run the Project Files
5. Credits



1. Project Title:
------------------

The Jobissimo Project. Navigation through Occupations, Job Listings, Courses.



2. Project Description:
-----------------------


For more information on ONET, please visit following website:
- https://www.onetonline.org/
- https://services.onetcenter.org/

Note: ONET username and password are available upon request. They were provided
by the ONET team and should not be published in open source.

Dice Dataset:
https://www.kaggle.com/datasets/PromptCloudHQ/us-technology-jobs-on-dicecom

Coursera Dataset:
- https://www.kaggle.com/datasets/khusheekapoor/coursera-courses-dataset-2021



3. Converted Datasets, Code and Presentations GIT Repository:
-------------------------------------------------------------

To download the code, datasets and project presentations please visit GitHub location:
- https://github.com/spring-camm-sergey/dse230

Files Description:

Datasets (datasets.zip) contains:
- BRFSS_2020_main_dataset.csv							this is the main dataset, downloaded from CDC website as SAS file (https://www.cdc.gov/brfss/annual_data/2020/files/LLCP2020XPT.zip) and converted into .csv in SAS Studio.
- Behavioral_Risk_Factor_Surveillance_System__BRFSS__Historical_Questions.csv	this file contains features codes, corresponding questions and possible answers.
- BRFSS_feature_codes_map.csv 							this file contains features codes and corresponding questions in the short form.


Code:
- project_notebook_1_Description_EDA.ipynb					Notebook 1: Project description, Setup, EDA
- project_notebook_2_Data_Preparation.ipynb					Notebook 2: Data Preparation
- project_notebook_3_Modeling_Evaluation.ipynb					Notebook 3: Modeling and Evaluation

- project_notebook_all.ipynb							Contains all the code and cells from notebooks 1,2,3 in one large notebook

Presentations:
- project_proposal_presentation.pdf						project proposal presentation PDF
- project_final_presentation.pdf						final project presentation PDF



4. How to Install and Run the Project:
--------------------------------------
- All files are located in project GIT repository: https://github.com/spring-camm-sergey/dse230

a. Download and unzip datasets.zip into your working directory (<work_dir>):
- https://github.com/spring-camm-sergey/dse230/blob/main/datasets.zip?raw=true

b. Place all CSV files from the previous step into HDFS. Example:
	hadoop fs -copyFromLocal <work_dir>/BRFSS_2020_main_dataset.csv /;
	hadoop fs -copyFromLocal <work_dir>/Behavioral_Risk_Factor_Surveillance_System__BRFSS__Historical_Questions.csv /;
	hadoop fs -copyFromLocal <work_dir>/BRFSS_feature_codes_map.csv /;


c. Download the code files (.ipynb) and place them into your working directory

d. Run the code:

Jupiter Notebook (Lab): open the .ipynb files and click Run > Run All Cells for the following files (keeping the same order):
- project_notebook_1_Description_EDA.ipynb
- project_notebook_2_Data_Preparation.ipynb
- project_notebook_3_Modeling_Evaluation.ipynb

- or just project_notebook_all.ipynb can be executed, it contains all the code in one file

e. Clean-up HDFS:

	hadoop fs -rm /BRFSS_2020_main_dataset.csv;
	hadoop fs -rm /BRFSS_feature_codes_map.csv;
	hadoop fs -rm /Behavioral_Risk_Factor_Surveillance_System__BRFSS__Historical_Questions.csv;
	hadoop fs -rm -r /df_features_transformation.csv;


5. Credits:
-----------

The project initiated as part of UCSD's DSE230 final project coursework.
The ML script was developed by below student maintainers and under the guidance of professor M. H. Nguyen (PhD).

Current Maintainers: 									Sergey Gurvich <sgurvich@ucsd.edu>
											Chunxia Tong <chtong@ucsd.edu>
											Camm Perera <cperera@ucsd.edu>











-----------------------------------------------------------------------------
-----------------------------------------------------------------------------
Repository Contents:

root
    src
        final_neo4j_files                       - final data for export to neo4j

        input_datasets
            Coursera.csv                        - original courses data
            coursera_small.csv                  - small sampled courses data
            dice_com-job_us_sample.csv          - original job listings data
            dice_small.csv                      - small sampled job listing data
            occupations_dataset_downloaded.csv  - downloaded ONET data

        output_datasets                         - output data (before neo4j)
        temp_datasets                           - intermediate data

        step1_process_listings.ipynb
        step2_process_courses.ipynb
        step3_match_listing_courses_skills.ipynb
        step4_create_occupation_related_nodes.ipynb
        step5_create_belongs_to_relation.ipynb
        step6_prepare_neo4j_files.ipynb

    presentation
        DSE203_Presentation.pptx
        Neo4j Queries.docx

requirements.txt                                - for pip install
README.md                                       - this file

-----------------------------------------------------------------------------
-----------------------------------------------------------------------------
Steps to run the code:
1. Execute notebooks in their order:
    step1_process_listings.ipynb
    step2_process_courses.ipynb
    step3_match_listing_courses_skills.ipynb
    step4_create_occupation_related_nodes.ipynb
    step5_create_belongs_to_relation.ipynb
    step6_prepare_neo4j_files.ipynb

Note:   we provided small sample datasets for testing and developement.
        To use them, step1 and step2 notebooks reading data corresponding lines
        should be uncommented.

2. Export to Neo4J (need to run in one line):
<neo4j_path_to_bin_folder>/neo4j-admin  import --force --multiline-fields=true
--nodes=<path_to_final_neo4j_files_folder>/final_neo4j_files/occupation__node.csv,
<path_to_final_neo4j_files_folder>/final_neo4j_files/skill__node.csv,
<path_to_final_neo4j_files_folder>/final_neo4j_files/listing__node.csv,
<path_to_final_neo4j_files_folder>/final_neo4j_files/course__node.csv,
<path_to_final_neo4j_files_folder>/final_neo4j_files/location__node.csv,
<path_to_final_neo4j_files_folder>/final_neo4j_files/company__node.csv,
<path_to_final_neo4j_files_folder>/final_neo4j_files/career_outlook__node.csv
--relationships=<path_to_final_neo4j_files_folder>/final_neo4j_files/located_in__relation.csv,
<path_to_final_neo4j_files_folder>/final_neo4j_files/needs__relation.csv,
<path_to_final_neo4j_files_folder>/final_neo4j_files/teaches__relation.csv,
<path_to_final_neo4j_files_folder>/final_neo4j_files/posted__relation.csv,
<path_to_final_neo4j_files_folder>/final_neo4j_files/belongs_to__relation.csv,
<path_to_final_neo4j_files_folder>/final_neo4j_files/has_future__relation.csv

-----------------------------------------------------------------------------
-----------------------------------------------------------------------------
