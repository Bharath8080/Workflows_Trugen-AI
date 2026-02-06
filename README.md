# Workflows_Trugen-AI

A collection of standardized n8n workflows integrated with Trugen AI agents for automated business processes.

## 🚀 Included Workflows

This repository contains five primary AI-driven workflows, categorized by their integration method with Trugen AI:

| Agent Name                    | Integration Method               | Primary Function                                                                        |
| :---------------------------- | :------------------------------- | :-------------------------------------------------------------------------------------- |
| **Customer Support Agent**    | **Function Calling**             | Automated responses to common customer inquiries using n8n-integrated tools.            |
| **Dental Appointment Agent**  | **Function Calling**             | Handles appointment scheduling, availability checks, and patient logging.               |
| **HR Interview Agent**        | **Post Call via Trugen AI Node** | Automates initial candidate screening and technical interviews with summary processing. |
| **Sales Qualification Agent** | **Post Call via Trugen AI Node** | Qualifies leads through conversational AI and synchronizes data with CRM systems.       |
| **Sentiment Analysis Agent**  | **Post Call via Trugen AI Node** | Processes customer feedback, analyzes sentiment (CSAT), and logs insights.              |

## 📁 Repository Structure

Each workflow resides in its own directory and includes:

- **n8n Workflow JSON**: Ready-to-import workflow file.
- **README.md**: Detailed setup guide and technical requirements.
- **TLDR.md**: High-level overview of the agent's purpose and logic flow.
- **Quickstart.md**: Commands to create the agent and tools via API.
- **Agent Configuration (JSON)**: Trugen AI agent persona and model settings.

## 🛠️ Getting Started

1.  **Import to n8n**: Download the `.json` workflow file and import it into your n8n instance.
2.  **Configure Trugen**: Use the provided `AGENT_CONFIG.json` to create your agent on the [Trugen AI Platform](https://app.trugen.ai/).
3.  **Connect Tools**: Link the n8n webhook URLs to the Trugen agent tools as described in each workflow's `README.md`.

## 🔑 Requirements

- **n8n**: A running instance (Cloud or Self-hosted).
- **Trugen AI API Key**: Required for agent and tool creation.
- **Service Specific Keys**: (e.g., Google Workspace, OpenAI) as specified in individual READMEs.
