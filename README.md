# Data-Fuse

Fetch Rewards Analytics Engineer Coding Exercise

## Folder structure

```
data-fuse
├── Data-Exploration.ipynb              [Jupyter notebook for task 1]
├── Data-Issues.ipynb                   [Jupyter notebook for task 3]
├── Email.eml                           [Jupyter notebook for task 4]
├── Email.pdf                           [Jupyter notebook for task 4]
├── Problem-Statement.pdf
├── README.md
├── data                                [Directory that contains the JSON files]
│   ├── brands.json
│   ├── receipts.json
│   └── users.json
├── data-model.png                      [Data Model Design for Task 1]
├── queries.md                          [Queries for Task 2]
└── requirements.txt                    [required libraries to run the jupyter notebooks]
```

## Assumptions

The objective of this test was to analyze the unstructured data within JSON files and devise a suitable data model for storing the extracted information. Following extraction, the data typically undergoes transformation based on predefined business rules before being stored in a data warehouse. In this scenario, I've assumed that all attributes are mandatory, reflected in the comprehensive class diagram representing the data model derived from the JSON files.

## Task 1: Designing a Data Model

After thorough exploration of the files, I've formulated a robust design capable of accommodating the data contained within them. The process and findings of the data exploration can be reviewed in the [Data-Exploration.ipynb](https://github.com/kedartakwane/data-fuse/blob/main/Data-Exploration.ipynb) file. Additionally, a comprehensive Class Diagram illustrating the proposed Data Model has been provided in [Data-Model](/data-model.png).

![Data-Model](/data-model.jpg)

## Task 2: SQL queries to answer predetermined questions from Stakeholders

I have answered three questions which can be found in [queries](queries.md).

## Task 3: Evaluating Data Quality Issues

Additional material to support me finding can be found in [Data-Issues](/Data-Issues.ipynb) file.

### Summary of issues with users.json

1. 495 user records contain significant duplicates, reducing unique data to 212 records after deduplication
2. 48 records have incorrect "nan" value for signUpSource, dropping to 5 post-deduplication
3. 56 records have incorrect "nan" value for state, reducing to 6 unique records with this issue
4. Incorrect "nan" values in signUpSource and state fields undermine data quality and analytics

### Summary of issues with brands.json

1. Critical attributes like category, categoryCode, brandCode missing for several brands
2. 155/1167 brands missing category, 650/1167 missing categoryCode, 234/1167 missing brandCode
3. Missing brand codes in brands.json cripples receipt item to brand affiliation
4. Populating missing category, categoryCode, brandCode attributes crucial for accurate brand analytics
5. Current brand data gaps impact receipt parsing and item-to-brand mapping

### Summary of issues with receipts.json

1. Inconsistency between Receipts and Brands - brandCodes in Receipts missing from Brands
2. Analysis shows brandCodes in Receipts not defined in Brands master list
3. Receipts reference orphan brandCodes not present in Brands

## Task 4: Informing Stakeholders

An email draft has been prepared for communication purposes. Please refer to the file named [Email.eml](Email.eml) for the draft. Alternatively, if the email draft is inaccessible, kindly review the PDF version provided for the same correspondence: [Email.pdf](Email.pdf).

## About Me

I'm Kedar, and I'm excited to bring my expertise to the role of Analytic Engineer. With over three years of experience in software engineering, I've specialized in building large-scale data pipelines, search systems, and visualizations using Python, JavaScript, Elasticsearch, and Kafka. My proficiency extends to web frameworks like Flask and React, where I've honed my skills in agile development, test-driven coding, and infrastructure automation with Docker and Kubernetes. I'm passionate about leveraging data to drive insights and make informed decisions, and I look forward to contributing to your team's success.

LinkedIn: https://linkedin.com/in/kedar-takwane

GitHub: https://github.com/kedartakwane
