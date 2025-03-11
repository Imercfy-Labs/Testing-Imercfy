# Testing Imercfy - n8n Candidate Selection Workflow

This repository contains an n8n workflow for automating candidate selection processes using Google Gemini AI.

## Workflow Overview

The workflow automates the candidate selection process with the following steps:

1. **Google Sheets Trigger**: Monitors a Google Sheet for new candidate entries
2. **Job Requirements Setup**: Sets up requirements based on the job position
3. **Candidate Processing Loop**: Processes each candidate in the list
4. **Resume Extraction**: Downloads and extracts text from resumes stored in Google Drive
5. **Google Gemini AI Evaluation**: Uses Google Gemini to evaluate candidates against job requirements
6. **Results Processing**: Compiles evaluation results and generates reports
7. **Output Generation**: Exports results to CSV, saves to Google Drive, and updates a Google Sheet with the report

## Key Features

- Replaced OpenAI LLM with Google Gemini for candidate evaluation
- Connected the Generate Report node to Google Sheets for easy result tracking
- Automated resume analysis and candidate scoring
- Structured evaluation with skills, experience, and education matching
- Final recommendations (Hire, Consider, Reject) for each candidate

## Setup Requirements

To use this workflow, you'll need:

1. An n8n instance
2. Google account with access to:
   - Google Sheets
   - Google Drive
   - Google Gemini API

## Environment Variables

The workflow requires the following environment variables:

- `GOOGLE_SHEET_ID`: ID of the Google Sheet containing candidate information
- `GOOGLE_DRIVE_FOLDER_ID`: ID of the Google Drive folder for storing reports
- `RESULTS_GOOGLE_SHEET_ID`: ID of the Google Sheet for storing evaluation results

## Importing the Workflow

1. Download the `candidate-selection-workflow.json` file
2. In your n8n instance, go to Workflows > Import From File
3. Select the downloaded JSON file
4. Configure the required credentials and environment variables

## License

This project is open-source and available under the MIT License.