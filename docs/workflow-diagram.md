# n8n Candidate Selection Workflow Diagram

## Workflow Overview

```
┌─────────────────────┐     ┌─────────────────────┐     ┌─────────────────────┐
│  Google Sheets      │     │  Set Job            │     │  Initialize         │
│  Trigger            │────▶│  Requirements       │────▶│  Variables          │
└─────────────────────┘     └─────────────────────┘     └──────────┬──────────┘
                                                                    │
                                                                    ▼
┌─────────────────────┐     ┌─────────────────────┐     ┌─────────────────────┐
│  Prepare Candidate  │     │  Loop Through       │     │                     │
│  Data               │◀────│  Candidate          │◀────│  Continue Loop      │
└──────────┬──────────┘     └─────────────────────┘     └─────────────────────┘
           │                                                        ▲
           ▼                                                        │
┌─────────────────────┐     ┌─────────────────────┐     ┌─────────────────────┐
│  Google Drive       │     │  Resume             │     │  Is Processing      │
│  (Download Resume)  │────▶│  Extraction         │     │  Complete?          │
└──────────┬──────────┘     └──────────┬──────────┘     └──────────┬──────────┘
           │                            │                           │
           ▼                            ▼                           │
┌─────────────────────┐     ┌─────────────────────┐     ┌─────────────────────┐
│  Google Gemini      │     │  Evaluation         │     │  Add To             │
│  Evaluate Candidate │────▶│  JSON               │────▶│  Evaluations        │────▶
└─────────────────────┘     └─────────────────────┘     └─────────────────────┘
                                                                    │
                                                                    ▼
┌─────────────────────┐     ┌─────────────────────┐     ┌─────────────────────┐
│  Google Sheets      │     │  Generate           │     │  Save File          │
│  Output             │◀────│  Report             │◀────│  (CSV to Drive)     │
└─────────────────────┘     └─────────────────────┘     └─────────────────────┘
                                                                    ▲
                                                                    │
                                                        ┌─────────────────────┐
                                                        │  CSV Export         │
                                                        │                     │
                                                        └─────────────────────┘
```

## Key Changes from Original Workflow

1. **Replaced OpenAI LLM with Google Gemini**:
   - The "Google Gemini - EvaluateParse Candidate" node replaces the previous OpenAI node
   - This node uses the Gemini Pro model to evaluate candidate resumes against job requirements

2. **Connected Generate Report to Google Sheets**:
   - Added the "Google Sheets Output" node after the "Generate Report" node
   - This connection ensures that all report data is automatically saved to a Google Sheet for easy access and sharing

## Data Flow Explanation

1. The workflow starts when a new candidate entry is detected in the Google Sheet
2. Job requirements are set based on the position
3. Variables are initialized for tracking the evaluation process
4. Each candidate is processed in a loop:
   - Resume is downloaded from Google Drive
   - Text is extracted from the resume
   - Google Gemini evaluates the candidate against job requirements
   - Evaluation results are stored
5. When all candidates are processed:
   - Results are exported to CSV
   - CSV file is saved to Google Drive
   - A comprehensive report is generated
   - Report data is written to a Google Sheet

## Node Connections

- **Main Flow**: Google Sheets Trigger → Set Job Requirements → Initialize Variables → Loop Through Candidate → Prepare Candidate Data → Google Drive → Resume Extraction → Google Gemini → Evaluation JSON → Add To Evaluations → Is Processing Complete?
- **Loop Branch**: Is Processing Complete? (No) → Continue Loop → Loop Through Candidate
- **Output Branch**: Is Processing Complete? (Yes) → CSV Export → Save File → Generate Report → Google Sheets Output