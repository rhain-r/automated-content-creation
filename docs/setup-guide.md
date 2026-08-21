# Setup & Deployment Guide

Follow these steps to deploy the Automated Content Pipeline in your own environment.

## Prerequisites

Before importing the workflows, ensure you have active accounts and API keys for the following services:
*   **OpenAI:** API Key with access to `gpt-4o` or preferred models.
*   **Google Cloud Console:** Service Account JSON with access to Google Sheets and Google Docs APIs.
*   **Messaging App (WhatsApp/Slack):** Webhook URL or Bot Token for sending and receiving approval messages.
*   **CMS (e.g., Squarespace):** API key with write permissions for publishing blog posts.

## 1. Database Setup
1. Create a new Google Sheet.
2. Create the following columns: `Blog ID`, `Topic`, `Status`, `Doc Link`, `Feedback`, `Date Published`.
3. Share the sheet with your Google Cloud Service Account email.

## 2. Importing Workflows
1. Open your automation platform (n8n, Make, etc.).
2. Import the JSON workflow files (if exported) or recreate the visual nodes as shown in the `assets/` folder.
3. Authenticate all nodes (Google, OpenAI, Slack/WhatsApp, CMS) using your credentials.

## 3. Configuring Prompts
1. Navigate to the `src/prompts/` folder in this repository.
2. Copy the system prompts.
3. Paste them into the respective OpenAI nodes within your workflow (e.g., the "Generate Blog Draft" and "Generate Revised Draft" nodes).

## 4. Testing the Pipeline
To ensure everything is working safely without accidentally publishing:
1. Disconnect the final "Publish to Website" node.
2. Trigger the "Blog Topic Generator" manually.
3. Verify that the Google Sheet populates correctly.
4. Check your messaging app for the approval prompt.
5. Once confirmed, reconnect the publishing node and deploy!
