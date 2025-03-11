# n8n Candidate Selection Workflow Explanation

## Overview

This document provides a detailed explanation of the n8n workflow for candidate selection using Google Gemini AI.

## Workflow Nodes Explanation

### 1. Google Sheets Trigger
- **Purpose**: Monitors a Google Sheet for new candidate entries
- **Configuration**: Listens for new rows added to the specified sheet
- **Output**: Triggers the workflow when new candidates are added

### 2. Set Job Requirements
- **Purpose**: Defines job requirements based on the position
- **Implementation**: JavaScript function that sets requirements for different job positions
- **Output**: Job requirements object with skills, experience, and education criteria

### 3. Initialize Variables
- **Purpose**: Sets up variables needed for candidate processing
- **Implementation**: JavaScript function that initializes counters and arrays
- **Output**: Initialized workflow variables

### 4. Loop Through Candidate
- **Purpose**: Creates a loop to process each candidate individually
- **Implementation**: Split in Batches node with batch size of 1
- **Output**: Individual candidate data for processing

### 5. Prepare Candidate Data
- **Purpose**: Prepares the current candidate's data for evaluation
- **Implementation**: JavaScript function that extracts candidate info
- **Output**: Current candidate data ready for processing

### 6. Google Drive
- **Purpose**: Downloads the candidate's resume from Google Drive
- **Configuration**: Uses the resume file ID from candidate data
- **Output**: Resume file binary data

### 7. Resume Extraction
- **Purpose**: Extracts text from the resume file
- **Implementation**: JavaScript function that converts binary data to text
- **Output**: Plain text resume content

### 8. Google Gemini - EvaluateParse Candidate
- **Purpose**: Uses Google Gemini AI to evaluate the candidate
- **Configuration**: 
  - Model: gemini-pro
  - Prompt: Structured evaluation request
  - Temperature: 0.2 (for consistent results)
  - Response Format: JSON
- **Output**: Structured evaluation of the candidate

### 9. Evaluation JSON
- **Purpose**: Parses the Gemini evaluation results
- **Implementation**: JavaScript function that processes the JSON response
- **Output**: Structured evaluation data

### 10. Add To Evaluations
- **Purpose**: Adds the current evaluation to the collection
- **Implementation**: Simple pass-through function
- **Output**: Updated evaluation collection

### 11. Is Processing Complete?
- **Purpose**: Checks if all candidates have been processed
- **Implementation**: Conditional node comparing processed count to total
- **Output**: Decision to continue loop or proceed to reporting

### 12. Continue Loop
- **Purpose**: Returns to the loop for the next candidate
- **Implementation**: No Operation node
- **Output**: Control flow back to the loop

### 13. CSV Export
- **Purpose**: Prepares evaluation data for CSV export
- **Implementation**: JavaScript function that formats data for CSV
- **Output**: CSV-formatted evaluation data

### 14. Save File
- **Purpose**: Saves the CSV report to Google Drive
- **Configuration**: Uses the configured Google Drive folder
- **Output**: Saved CSV file information

### 15. Generate Report
- **Purpose**: Creates a comprehensive evaluation report
- **Implementation**: JavaScript function that generates summary statistics
- **Output**: Structured report data

### 16. Google Sheets Output
- **Purpose**: Writes the report data to a Google Sheet
- **Configuration**: Uses the configured results sheet ID
- **Output**: Updated Google Sheet with evaluation results

## Key Modifications from Original Workflow

1. **Replaced OpenAI LLM with Google Gemini**:
   - Changed the AI evaluation node to use Google Gemini instead of OpenAI
   - Updated prompt and response handling for Gemini's capabilities

2. **Connected Generate Report to Google Sheets**:
   - Added a Google Sheets Output node after the Generate Report node
   - Configured it to write the report data to a specified Google Sheet

## Data Flow

1. Candidate data is triggered from Google Sheets
2. Each candidate's resume is processed individually
3. Google Gemini evaluates each candidate against job requirements
4. Results are compiled into a comprehensive report
5. Report is saved as CSV to Google Drive
6. Report is also written to a Google Sheets document for easy access

## Environment Variables

The workflow uses environment variables to keep sensitive information secure:

- `GOOGLE_SHEET_ID`: ID of the input Google Sheet
- `GOOGLE_DRIVE_FOLDER_ID`: ID of the Google Drive folder for reports
- `RESULTS_GOOGLE_SHEET_ID`: ID of the output Google Sheet
- `GOOGLE_GEMINI_API_KEY`: API key for Google Gemini