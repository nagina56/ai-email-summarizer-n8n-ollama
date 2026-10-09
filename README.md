# AI Email Summarizer using n8n and Ollama

An AI-powered email summarization workflow built with **n8n and Ollama**. The project is designed to summarize email text, identify important details, extract action items, and highlight deadlines using a locally running language model.

## Project Overview

Reading long emails can take time. This automation uses a local AI model to generate concise summaries and organize the important information into a structured format.

## Features

* Summarizes email content
* Extracts important action items
* Identifies deadlines and key details
* Uses n8n for workflow automation
* Uses Ollama to run a local language model
* Avoids paid OpenAI API credits when using a local Ollama model
* Can be extended to store summaries in Google Sheets

## Tools and Technologies

* **n8n** — Workflow automation
* **Ollama** — Local AI model runtime
* **Gemma 3:4B** — Language model
* **Google Sheets** — Optional output destination
* **Prompt Engineering** — Structured email summarization

## Workflow

Manual Trigger → Edit Fields → Basic LLM Chain → Google Sheets

The Ollama Chat Model is connected to the Basic LLM Chain as its language model.

## Example Output

**Summary:** The website homepage needs to be completed by Friday.

**Action Items:**

* Complete the homepage.
* Add a contact form.
* Test the website on mobile devices.

**Deadline:** Friday

**Important Details:** The project owner should be informed if additional information is required.

*Example output for demonstration purposes.*

## Setup Instructions

### 1. Install Ollama

Download Ollama from the official website:

https://ollama.com/download

### 2. Download the model

Run this command in PowerShell:

```powershell
ollama pull gemma3:4b
```

### 3. Verify the model

```powershell
ollama list
```

### 4. Configure n8n

Open your local n8n instance and create a workflow with these nodes:

1. Manual Trigger
2. Edit Fields
3. Basic LLM Chain
4. Ollama Chat Model connected to the Basic LLM Chain
5. Google Sheets (optional)

Configure the local Ollama connection using the appropriate Base URL for your n8n environment. For a direct Windows installation, this is typically:

`http://localhost:11434`

Local Ollama connections generally do not require an API key. Docker or other deployment setups may require a different address.

### 5. Add the email text

Create an `email_text` field in the Edit Fields node and enter the email you want to summarize.

### 6. Configure the prompt

Use this prompt in the Basic LLM Chain:

```text
Summarize the following email clearly and concisely.

Return the result in this format:

Summary:
Action Items:
Deadline:
Important Details:

Email:
{{$json.email_text}}
```

### 7. Execute the workflow

Run the workflow and verify that the model returns a summary. If using Google Sheets, map the generated summary and other fields to the appropriate columns.

## Screenshots

### n8n Workflow

Add your workflow screenshot here:

`![n8n Workflow](screenshots/n8n-workflow.png)`

### Email Summary Output

Add your successful output screenshot here:

`![Email Summary Output](screenshots/email-summary-output.png)`

## Future Improvements

* Integrate Gmail to process incoming emails
* Automatically save summaries to Google Sheets
* Add priority classification
* Send notifications for important deadlines
* Process multiple emails automatically

## Learning Outcomes

* Building AI-powered automation workflows
* Connecting local language models with n8n
* Writing structured prompts
* Passing data between workflow nodes
* Integrating AI outputs with Google Sheets

## Author

Built as part of my journey into Python, AI, and workflow automation.

