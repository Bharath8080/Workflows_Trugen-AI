# HR Interview Agent – Professional Candidate Screening

This README provides a streamlined guide for deploying the **HR Interview** AI Agent using n8n and Trugen AI. This workflow is designed to automate candidate screening by creating the agent directly from n8n and logging results to Google Sheets.

---

## 🚀 Quick Start: Deployment Flow

Unlike traditional manual setup, this workflow handles agent creation and configuration automatically.

### Step 1: n8n Import & Credentials

1. **Import**: Upload the `Trugen's HR Interview Agent.json` file into your n8n instance.
2. **Authorize**: Connect your credentials for:
   - **Trugen AI**: Bring your API Key.
   - **Google Sheets**: For candidate data logging.
   - **OpenAI**: To power the screening logic (GPT-4o-mini).

### Step 2: Automated Agent Creation

1. Find the node named **"▶️ Click to Start Setup"** (Manual Trigger).
2. **Click execute**: This will automatically reach out to Trugen AI and create your agent with the pre-configured Name, System Prompt, STT (Deepgram), LLM (GPT-4o-mini), and TTS settings.
3. **Save Agent Info**: The technical details and the **Interview Link** will be automatically saved to your **Google Sheets** (in the 'Interview Info' sheet).

### Step 3: Webhook & Callback Setup

1. Copy the **Webhook URL** from the "Webhook" node in n8n.
2. Open your [Trugen Dashboard](https://app.trugen.ai/), select your newly created agent, and go to **Settings**.
3. Paste the Webhook URL into the **Callback URL** field.
4. Set the **Callback Event** to `Call Ended`.

---

## 🏗️ Workflow Architecture

### 🟢 Phase 1: Registration

The manual trigger initializes the agent on the Trugen platform and stores the call link in your database.

### 🔵 Phase 2: Live Interview

The candidate uses the link to start a voice/video interview. The agent follows the pre-coded screening logic to assess skills, experience, and salary expectations.

### 🟣 Phase 3: Automated Analysis

Once the call ends:

1. The **Webhook** receives the conversation transcript and metadata.
2. **AI Analysis**: GPT-4o-mini extracts and scores the candidate's responses.
3. **Data Logging**: Final results are appended to your **Google Sheets** for HR review.

---

## 🛠️ Requirements

- **Trugen AI API Access**.
- **OpenAI API Key**.
- **Google Workspace**: Connected to Google Sheets.
- **n8n Instance**: To run the automation.
