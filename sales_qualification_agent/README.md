# AI Sales Qualification & CRM Sync (BANT Framework)

This README covers the automated setup for the **AI Sales Qualification** Agent. This system creates a discovery agent on Trugen, scores leads using the BANT framework, and syncs all intelligence to HubSpot and Google Sheets.

---

## 🚀 Quick Start: Deployment Flow

This workflow is built for "one-click" setup from n8n.

### Step 1: n8n Import & Credentials

1. **Import**: Upload the `AI Sales Qualification & CRM Sync Workflow.json` into n8n.
2. **Authorize**: Connect your credentials for:
   - **Trugen AI**: API Key for agent management.
   - **HubSpot**: For CRM contact and deal sync.
   - **Google Workspace**: For Gmail notifications and Sheets logging.
   - **OpenAI**: For high-precision lead scoring (GPT-4o).

### Step 2: Automated Agent Initialization

1. In n8n, execute the node **"▶️ Click to Start Setup"**.
2. This creates the **"Lead Qualification Agent"** on Trugen with pre-defined discovery logic.
3. The **Agent Link** and setup metadata are automatically saved to your master **Google Sheets**.

### Step 3: Webhook Integration

1. Copy the **Webhook URL** from the "Webhook" node.
2. Open your Trugen Dashboard, select the Sales Agent, and navigate to **Settings**.
3. Point the **Callback URL** to your n8n Webhook.
4. Set the **Callback Event** to `Call Ended`.

---

## 🏗️ Intelligence Flow

### 🟢 Stage 1: Lead Capture

The manual trigger sets up the recruitment/sales environment and stores the public call link in the database.

### 🔵 Stage 2: BANT Analysis

Once a prospect interacts with the agent, the system extracts:

- **Budget**: Financial readiness.
- **Authority**: Decision-maker identification.
- **Need**: Pain point severity.
- **Timeline**: Purchase urgency.

### 🟣 Stage 3: Routing & Sync

At the end of the call, the **Webhook** triggers:

1. **Scoring**: GPT-4o assigns a final lead score (0-100).
2. **CRM Sync**: Updates HubSpot with qualification details and "Red Flags".
3. **Routing**: Assigns the lead to the Senior, Mid, or SDR team based on score and industry.
4. **Notifications**: Alerts the assigned sales rep and the prospect via branded emails.

---

## 🛠️ Requirements

- **Trugen AI API Access**.
- **OpenAI API Key** (Optimized for GPT-4o).
- **HubSpot Account**: With App Token or API access.
- **Google Workspace**: For Gmail & Sheets.
