## CONTENTS OF THIS FILE:

1. Project Title
2. Project Description
3. Datasets
4. Files Description
5. How to Run the Project Files
6. Credits

# 1. Project Title
--------

The Jobissimo Project: Navigation Through Occupations, Job Listings and Courses.



# 2. Project Description
--------
The average person spends 900,000 hours at work over the course of their life-time, so it stands to reason that changing career paths should be taken seriously. The skill set a person has is integral to advancing through the working world, so we set out to connect current occupations to job listings to the Coursera courses that will give you the skills to land your dream job.

The knowledge graph created in this project accomplishes several goals:
* First is to correctly connect job listings to occupations, which allows a potential user to find more information about the job on the listing such as average salary and career outlook.
* Second is to correctly establish a relationship between what skills are needed for a job listing and what skills are taught through courses on Coursera. Or framed differently, we want to answer which courses would best teach the majority of needed skills for a job listing.
* And third, we aim to show a holistic view of jobs and skills.

The three datasets we used to create the nodes and relationships that made up this knowledge graph were datasets collected from ONET about occupations within the USA, from Dice.com for their job listings, and from Cousera's courses.

From the ONET data, collected via API calls, occupations—including their synonyms—and career outlooks were extracted into objects (nodes). Pointers (relationships) were retained between each occupation and ONET's career outlook on each.

From the Dice data, four types of objects were extracted: each job listing—including job titles and descriptions—as well as the hiring companies, the locations, and the list of skills each job required. The pointers between each of the last three object types and the job listing were also retained. This data required much cleaning and organizing before finalizing each object and pointer.

From the Coursera data, the courses themselves—including the course name, description, difficulty level, and sign-up URL—as well as the skills each course taught were extracted into objects. Pointers between each course and the skills they taught were retained.

//skills merge desc

//"belongs to" desc

//neo4j use desc

# 3. Datasets
--------
- ONET Data:
    - https://www.onetonline.org/
    - https://services.onetcenter.org/

    Note: ONET username and password are available upon request. They were provided
by the ONET team and should not be published in open source.

- Dice Dataset:
    https://www.kaggle.com/datasets/PromptCloudHQ/us-technology-jobs-on-dicecom

- Coursera Dataset:
https://www.kaggle.com/datasets/khusheekapoor/coursera-courses-dataset-2021

# 4. Files Description
--------
To download the code, datasets and project presentations please visit GitHub location:
- https://github.com/jessica-leslie-sergey/dse203

### Repository Contents:
```
/root
    /neo4j_data_zip
        data.zip                                - zip file with DB data

    /src
        /final_neo4j_files                      - final data for export to neo4j
            <list of .csv files for nodes and relations>
	    
        /input_datasets
            Coursera.csv                        - original courses data
            coursera_small.csv                  - small sampled courses data
            dice_com-job_us_sample.csv          - original job listings data
            dice_small.csv                      - small sampled job listing data
            occupations_dataset_downloaded.csv  - downloaded ONET data

        /output_datasets                        - output data (before neo4j)
	     <list of .csv files for nodes and relations, but not ready for neo4j>
	     
        /temp_datasets                          - intermediate data
	     <list of temporary .csv files>
	     
        step1_process_listings.ipynb
        step2_process_courses.ipynb
        step3_match_listing_courses_skills.ipynb
        step4_create_occupation_related_nodes.ipynb
        step5_create_belongs_to_relation.ipynb
        step6_prepare_neo4j_files.ipynb

    /presentation
        DSE203_Presentation.pptx
        Neo4j Queries.docx

requirements.txt                                - for pip install
readme.txt                                      - this file
```


# 5. How to Run the Project Files
-----------
A. Execute notebooks in their order:

    step1_process_listings.ipynb
    step2_process_courses.ipynb
    step3_match_listing_courses_skills.ipynb
    step4_create_occupation_related_nodes.ipynb
    step5_create_belongs_to_relation.ipynb
    step6_prepare_neo4j_files.ipynb

Note:   we provided small sample datasets for testing and developement.
        To use them, step1 and step2 notebooks 'read data' corresponding lines
        should be uncommented/changed.

B. Export to Neo4J (need to run in one line, replace `<path_to_final_neo4j_files_folder>` with your local path):
```
    <neo4j_path_to_db_folder>/bin/neo4j-admin  import --force --multiline-fields=true
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
```
C. It is possible to just download data.zip from neo4j_data_zip folder, unzip it in local <neo4j_path_to_db_folder> and start the DB.

# 6. Credits
-----------

The project initiated as part of UCSD's DSE203 final project coursework.
The scripts were developed by below student maintainers and under the guidance of professor Amarnath Gupta (PhD).
All creative and distribution rights reserved. Redistribution without express written permission fromt the maintaners is not allowed.

Current Maintainers:
- Jessica Allen <j4allen@ucsd.edu>
- Leslie Joe <ljoe@ucsd.edu>
- Sergey Gurvich <sgurvich@ucsd.edu>
