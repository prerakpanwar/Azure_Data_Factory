# Azure_Data_Factory

## End-to-End Data Pipeline using Azure Data Factory (ADF)

This repository demonstrates a production-ready end-to-end data pipeline built using Azure Data Factory. The pipeline is triggered automatically when a file is uploaded to a source container and performs validation, transformation, and orchestration of multiple child pipelines.

## Features
- Automated pipeline trigger based on file upload
- Validation activity ensures only the correct files trigger processing
- Execute Pipeline activity to orchestrate multiple child pipelines
- Data transformation using Data Flow
- GitHub integration to fetch additional datasets
- Automatic deletion of processed files to prevent duplicate triggers
- End-to-end monitoring in the ADF portal

## Architecture Overview
Parent Pipeline (Production)
│
├─> Execute Manager Pipeline
│    └─> Copy data from source container
│    └─> Fetch additional data from GitHub
│
├─> Execute Only Selected Files Pipeline
│    └─> Validation Activity
│    └─> Get Metadata
│    └─> ForEach CSV
│         └─> If Condition (file starts with "fact")
│              └─> Copy Activity
│              └─> Data Flow Transformation


- Trigger: Storage event trigger based on a specific file (e.g., factore_sales_1.csv)
- Parent Pipeline: Orchestrates multiple child pipelines
- Child Pipelines: Handle data ingestion, validation, and transformation

## How It Works
1- Manager/Stakeholder drops file in the source container (must match the expected file name).
2- Storage trigger automatically starts the parent pipeline.
3- Manager Pipeline copies the data to the destination container and fetches additional GitHub datasets.
4- Only Selected Files Pipeline validates, filters, and processes files starting with fact.
5- Data transformation is performed using ADF Data Flow.
6- Processed files are moved to reporting and data flow output folders.
7- Pipeline runs are monitored via the ADF Monitor tab.

## Steps to Run

Clone the repository: git clone <repository-url>

- Import the ADF pipelines JSON files into your Azure Data Factory.
- Configure the source container in Azure Storage.
- Set up the storage event trigger on the parent pipeline.
- Upload a file matching the naming convention (e.g., factore_sales_1.csv) to the source container.
- Monitor pipeline execution in the Monitor tab.

## Key Concepts Learned
- Storage event triggers in ADF
- Pipeline orchestration using Execute Pipeline activity
- Data validation with Validation Activity
- Metadata handling using Get Metadata and ForEach activities
- Conditional processing using If Condition
- Data transformation using Data Flow
- Debugging and troubleshooting pipelines in real-world scenarios

## Future Enhancements
- Include more complex real-time scenarios
- Integration with Delta Lake for advanced data storage and updates
- Project-based end-to-end pipelines for full data engineering workflows

## References
- Azure Data Factory Documentation
- ADF Data Flow Overview
- Ansh Lamba

## Support
If you find this repository helpful, please ⭐ star this repo and share it with your friends or colleagues interested in data engineering.
