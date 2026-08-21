# System Architecture

This document outlines the architecture of the Automated Blog Generation & Publishing Pipeline. The system is designed to be modular, allowing individual workflows to operate independently while passing state through Google Sheets.

## Core Components

1. **Automation Engine (n8n):** Acts as the central orchestrator, listening for triggers (schedules or webhooks) and executing the sequential steps of the workflow.
2. **State Management (Google Sheets):** Serves as the system's database. It tracks the status of each blog post (e.g., `Drafting`, `Under Review`, `Approved`, `Published`) to prevent duplicate processing.
3. **Drafting Engine (Google Docs):** Used as the primary canvas. The LLM outputs its generated markup here, allowing for easy formatting conversion later.
4. **Reasoning & Generation (OpenAI):** Handles all cognitive tasks, including topic ideation, drafting, and compliance checking against brand guidelines.
5. **Human-in-the-Loop (WhatsApp / Slack):** Acts as the safety gate. No content is published without an explicit "Approve" signal from this channel.
6. **Publishing (CMS API):** The final destination (e.g., Squarespace, WordPress) where the approved HTML is sent to go live.

## Data Flow

1. **Trigger:** A daily schedule kicks off the workflow.
2. **Read:** The automation fetches the current pipeline from Google Sheets.
3. **Process:** OpenAI generates/revises the content based on the intake data.
4. **Halt & Prompt:** A webhook/message is sent to the manager's messaging app. The automation pauses.
5. **Resume:** A reply (Approve/Revise) triggers the next phase.
6. **Execute:** If approved, the Doc is converted to HTML and POSTed to the CMS.
7. **Log:** Google Sheets is updated to `Published` and a confirmation email is sent via Gmail.
