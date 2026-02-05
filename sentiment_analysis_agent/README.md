# Sentiment Analysis & CSAT Video AI Agent

This README provides a guide for deploying the **Sentiment Analysis** AI Agent. This workflow is designed to automatically create a feedback agent on the Trugen platform and analyze user sentiment/CSAT scores after every interaction.

---

## 🚀 Quick Start: Deployment Flow

This workflow automates the process of platform setup directly from n8n.

### Step 1: n8n Import & Credentials

1. **Import**: Upload the `Sentiment Analysis Trugen Updated.json` file into n8n.
2. **Authorize**: Connect your credentials for:
   - **Trugen AI**: API key for agent management.
   - **Google Sheets**: For feedback data storage.
   - **OpenAI**: To drive the analysis engine (GPT-4o-mini).

### Step 2: Automated Agent Creation

1. Find the node **"▶️ Click to Start Setup"** and execute it.
2. This creates the **"TruGen Feedback Intelligence Agent"** automatically with pre-coded instructions for sentiment collection.
3. The **Agent Link** and metadata are stored in your **Google Sheets** spreadsheet.

### Step 3: Webhook & Callback Sync

1. Copy your **Webhook URL** from the "Webhook" node.
2. In the Trugen Dashboard, navigate to your new agent's **Settings**.
3. Set the **Callback URL** to your n8n Webhook.
4. Set the **Callback Event** to `Call Ended`.

---

## 🏗️ Workflow Logic

### 🟢 Creation Phase

A one-time setup that registers the feedback agent on Trugen and prepares the data logging environment.

### 🔵 Feedback Capture

Users provide voice/video feedback. The agent is strictly programmed to capture interactions without bias.

### 🟣 Intelligence & Storage

Once the call ends, the workflow:

1. Receives the data via **Webhook**.
2. Fetches full conversation details.
3. Performs **AI Sentiment Analysis** (CSAT, Sentiment, Emotions, Pain Points).
4. Records structured insights into your **Google Sheets** for real-time monitoring.

---

## 🛠️ Requirements

- **Trugen AI API Access**.
- **OpenAI API Key** (Optimized for GPT-4o-mini).
- **Google Sheets**: Pre-formatted template (Link available in workflow notes).
- **n8n Instance**.
