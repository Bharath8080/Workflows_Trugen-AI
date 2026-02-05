# Workflows_Trugen-AI

A collection of standardized n8n workflows integrated with Trugen AI agents for automated business processes.

## 🚀 Included Workflows

This repository contains five primary AI-driven workflows, each designed for a specific industrial use case:

1.  **Dental Appointment Agent**: Handles appointment scheduling, availability checks, and patient logging for dental clinics.
2.  **HR Interview Agent**: Automates initial candidate screening and technical interviews with video AI capabilities.
3.  **Sales Qualification Agent**: Qualifies leads through conversational AI and synchronizes data with CRM systems.
4.  **Sentiment Analysis Agent**: Processes customer feedback, analyzes sentiment (CSAT), and logs insights.
5.  **Customer Support Agent**: Provides automated responses to common customer inquiries using n8n-integrated tools.

## 📁 Repository Structure

Each workflow resides in its own directory and includes:

- **n8n Workflow JSON**: Ready-to-import workflow file.
- **README.md**: Detailed setup guide and technical requirements.
- **TLDR.md**: High-level overview of the agent's purpose and logic flow.
- **Agent Configuration (JSON)**: Trugen AI agent persona and model settings.

## 🛠️ Getting Started

1.  **Import to n8n**: Download the `.json` workflow file and import it into your n8n instance.
2.  **Configure Trugen**: Use the provided `AGENT_CONFIG.json` to create your agent on the [Trugen AI Platform](https://app.trugen.ai/).
3.  **Connect Tools**: Link the n8n webhook URLs to the Trugen agent tools as described in each workflow's `README.md`.

## 🔑 Requirements

- **n8n**: A running instance (Cloud or Self-hosted).
- **Trugen AI API Key**: Required for agent and tool creation.
- **Service Specific Keys**: (e.g., Google Workspace, OpenAI) as specified in individual READMEs.
