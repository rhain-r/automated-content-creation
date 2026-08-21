# Autonomous Blog Generation & Publishing Pipeline

An Agentic AI system that operates as an autonomous content team. Unlike linear automations, this agent utilizes a reasoning loop to generate blog topics, draft content, route drafts for human-in-the-loop (HITL) approval via WhatsApp or Slack, execute revisions, and automatically publish to the web.

Instead of manually researching topics and writing posts, this system gives an AI agent access to your intake databases, document editors, and website publishing APIs, allowing it to execute your brand's content Standard Operating Procedures (SOPs) autonomously.

## Agentic Workflow Execution

The agent operates on a continuous loop across multiple specialized workflows. Upon execution, the agent observes existing content to avoid duplicates, reasons about new topics, uses tools to generate compliant drafts, and finally executes API calls to publish the content after human approval.

## Project Overview

This project demonstrates how brands can deploy Agentic AI using LLMs (e.g., OpenAI), workspace databases (Google Sheets/Docs), messaging platforms (WhatsApp/Slack), and website CMS APIs.

Each execution creates a unique trace of the agent's "Thought -> Action -> Observation" process:
*   **Observe (Database):** The agent monitors existing topic sheets to ensure no duplicate content is generated.
*   **Reason (LLM):** Using strict system prompts and compliance schemas, the agent evaluates the generated draft, extracts required information, and checks against brand guidelines.
*   **Validate (HITL):** Before publishing, the agent pauses the workflow and routes the draft to a manager via WhatsApp or Slack for approval, ensuring zero unapproved external communications.
*   **Execute (Publish):** Upon receiving human approval, the agent automatically converts the markup to HTML and schedules the post via the website API.

## Agent Capabilities

*   **Autonomous Topic Generation:** Checks for duplicates and generates fresh, relevant blog topics automatically.
*   **Draft & Compliance Checking:** Generates comprehensive blog drafts and passes them through an automated, schema-driven compliance check.
*   **Self-Correction & Revision:** Handles feedback loops by generating revised drafts based on specific human input.
*   **Human-in-the-Loop (HITL) Safety:** Routes generated drafts to communication channels for manager approval before going live.
*   **State & Status Logging:** Updates Google Sheets at every step (Generating, Under Review, Approved, Needs Revision, Posted) to maintain an accurate memory log.

## Agent Configuration & Workflows

### 1. Blog Topic Generator
Aggregates existing topics, checks for duplicates, and generates new blog IDs and content subjects to maintain a fresh pipeline.
![Blog Topic Generator](assets/blog-topic-generator.prt1.png)

### 2. Blog Generation Pipeline
Reads intake sheets, extracts information, generates a draft, and runs a strict compliance check before converting to a Google Doc.
![Blog Generation Pipeline](assets/blog-generation-pipeline.prt2.png)

### 3. Blog Approval and Revision (HITL)
Aggregates drafts under review, sends bulk reminders, and triggers WhatsApp/Slack messages for manager approval. Dynamically routes to the Publish or Revision workflow based on human response.
![Blog Approval and Revision](assets/blog-approval-and-revision(whatsapp%20or%20slack).prt3.png)

### 4. Blog Revision Workflow
Takes feedback from the approval stage, generates a revised draft using a specialized revision model, re-runs compliance checks, and updates the existing document.
![Blog Revision Workflow](assets/blog-revision-workflow.prt4.png)

### 5. Blog Publishing
Triggers on approval, fetches the final document, formats and publishes the blog to the website, and emails a final confirmation to the stakeholders.
![Blog Publishing](assets/blog-publishing.prt5.png)

## Tech Stack

| Component | Technology |
| --- | --- |
| **Agent Framework** | Workflow Automation Engine / Webhooks |
| **LLM Reasoning Engine** | OpenAI |
| **Memory / State** | Google Sheets & Google Docs |
| **Tools (Integrations)** | WhatsApp/Slack, Gmail, Squarespace/CMS APIs |

## Repository Structure

```text
.github/
    workflows/             # CI/CD pipelines
src/
    prompts/               # System prompts for generation, revision, and compliance
    schemas/               # JSON schemas for output parsing
assets/
    blog-topic-generator.prt1.png
    blog-generation-pipeline.prt2.png
    blog-approval-and-revision(whatsapp or slack).prt3.png
    blog-revision-workflow.prt4.png
    blog-publishing.prt5.png
docs/
    architecture.md        # System design
    setup-guide.md         # Instructions to run the agent workflows
.gitignore
LICENSE
README.md
