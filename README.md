# Testing Imercfy - n8n Candidate Selection Workflow

This repository contains an n8n workflow for automating candidate selection processes using Google Gemini AI with enhanced evaluation criteria for Imercfy internship candidates.

## Workflow Overview

The workflow automates the candidate selection process with the following steps:

1. **Google Sheets Trigger**: Monitors a Google Sheet for new candidate entries
2. **Job Requirements Setup**: Sets up requirements based on the job position
3. **Candidate Processing Loop**: Processes each candidate in the list
4. **Resume Extraction**: Downloads and extracts text from resumes stored in Google Drive
5. **AI Evaluation**: Uses Mistral AI to evaluate candidates against job requirements
6. **Results Processing**: Compiles evaluation results and generates reports
7. **Output Generation**: Exports results to CSV, saves to Google Drive, and updates a Google Sheet with the report

## Key Features

- Replaced OpenAI LLM with Mistral Cloud Chat Model for candidate evaluation
- Connected the Generate Report node to Google Sheets for easy result tracking
- Added Window Buffer Memory for improved context handling
- Implemented separate workflow tools for Spreadsheet Operations and Conditional Logic
- Enhanced evaluation criteria with Imercfy-specific questions:
  - "Why do you think that you would be a strong candidate at Imercfy?"
  - "Why are you interested in interning with Imercfy?"

## Updated AI Agent Prompt

The AI agent now evaluates candidates on six key criteria:
1. Skills Match (0-10)
2. Experience Relevance (0-10)
3. Education Fit (0-10)
4. Overall Potential (0-10)
5. Imercfy Fit (0-10) - NEW
6. Motivation (0-10) - NEW

The overall score is now out of 60 points instead of 40, with the additional 20 points coming from the Imercfy-specific criteria.

## Workflow Tools

### Spreadsheet Operations Tool
- Handles all Google Sheets operations
- Supports both update and append operations
- Processes data in a structured format

### Conditional Logic Tool
- Evaluates candidates based on configurable conditions
- Separates qualified and unqualified candidates
- Provides detailed feedback and next steps for each path

## Setup Requirements

To use this workflow, you'll need:

1. An n8n instance
2. Google account with access to:
   - Google Sheets
   - Google Drive
3. Mistral AI API access

## Environment Variables

The workflow requires the following environment variables:

- `GOOGLE_SHEET_ID`: ID of the Google Sheet containing candidate information
- `GOOGLE_DRIVE_FOLDER_ID`: ID of the Google Drive folder for storing reports
- `RESULTS_GOOGLE_SHEET_ID`: ID of the Google Sheet for storing evaluation results
- `MISTRAL_API_KEY`: API key for Mistral AI

## Importing the Workflow

1. Download the workflow JSON files:
   - `Updated_Candidate_Selection.json` (main workflow)
   - `spreadsheet-operations-workflow.json` (supporting workflow)
   - `conditional-logic-workflow.json` (supporting workflow)
2. In your n8n instance, go to Workflows > Import From File
3. Import each workflow file
4. Configure the required credentials and environment variables

## License

This project is open-source and available under the MIT License.