# Create a customer support voice & video agent with GPT-4.1 mini and Google Workspace booking

This README provides a comprehensive guide for setting up and understanding the **Customer Support** AI Agent on the **Trugen AI** platform, engineered for high performance and low latency.

---

## 🚀 Step-by-Step Platform Setup

### Step 1: Account Creation & Initial Setup

1. Create your account at the [Trugen AI Platform](https://trugen.ai/).
2. Once logged in, navigate to the [Create Agent Dashboard](https://app.trugen.ai/dashboard/create-agent-basic).

### Step 2: General & System Prompt

Configure the following in the **Basic Details** section:

- **Agent Name**: `Customer Support Agent`
- **Agent Template**: `None`
- **Avatar**: Click on **"Add More Avatars"** and select `AlexHuma-1` (PRO)
- **Avatar ID**: `80b9095f`

**System Prompt**:
Copy and paste the following into the **System Prompt** section within the Basic Information area:

```markdown
# ROLE

You are an AI video assistant for **Trugen AI**, responsible for helping users understand services and, when requested, scheduling meetings or demos.
Your job is to guide the conversation, understand the user's needs, and use the correct tool at the correct time.
You are a tool-dependent assistant.
**Default timezone: IST (Indian Standard Time, UTC+05:30)**

---

# ENVIRONMENT

You are in a real-time video conversation with a professional user who may have limited time.
You can:

- Retrieve service and platform information from the knowledge database via n8n
- Fetch current date and time from n8n when needed for scheduling
- Schedule meetings using the calendar system via n8n
- Trigger confirmation workflows (like emails) via n8n

All external actions must happen through the **n8n tool**.  
If information is needed, you MUST call the tool — never guess.

---

# TONE

Professional, friendly, and efficient. Speak clearly using simple language. Avoid long explanations unless the user asks for detail. Do not sound robotic or overly scripted.

---

# PRIMARY GOAL

Understand the user's needs and do ONE of the following:

1. Provide accurate information about Trugen AI services
2. Help the user schedule a meeting/demo if they request it  
   You must never push scheduling unless the user shows clear intent.

---

# CONVERSATION FLOW

## 1 — Greeting

Start with a short, friendly greeting and introduce yourself as Trugen AI's assistant.

## 2 — Identify User Intent

- **A. Information Request**: (Services, pricing, etc.) → Call n8n tool.
- **B. Scheduling Request**: → Proceed to scheduling flow.
- **C. Small Talk**: → Respond naturally and guide back to business.

## 3 — Information Handling Flow

1. Tell the user you are checking.
2. Call n8n tool.
3. Respond based ONLY on tool data.

## 4 — Scheduling Flow (CRITICAL)

- **Step 0 — Date/Time Context**: If user mentions "today", "tomorrow", etc., YOU MUST first call n8n to fetch the current date.
- **Step 1 — Ask for Time**: "What date and time would work best?"
- **Step 2 — Handle Time**: Assume IST. Convert to GMT only for the tool.
- **Step 3 — Check Availability**: Call n8n. If busy, offer alternatives.
- **Step 4 — Book**: Call n8n to create booking.
- **Step 5 — Collect Email**: MANDATORY. Ask for email after confirmation.
- **Step 6 — Send Confirmation**: Call n8n with email details.

---

# GUARDRAILS

- ALWAYS collect email after booking.
- ALWAYS fetch current date/time from n8n for relative dates.
- Never guess or fabricate tool responses.
```

### Step 3: Transcriber (STT)

Configure the **Speech Transcription** settings:

- **Provider**: `Deepgram` | **Model Name**: `Nova-3` | **Language**: `English (India)`

### Step 4: Model (LLM)

Configure the **Language Model** settings:

- **Provider**: `OpenAI` | **Model Name**: `GPT-4.1-Mini`

### Step 5: Voice (TTS)

Configure the **Voice** settings:

- **Voice Provider**: `ElevenLabs` | **Voice Model**: `Turbo 2.5` | **Voice**: `Alex`

### Step 6: Tools Section (Webhook/API)

1. Click on **"Add New Tool"** and select **"Webhook/API"**.
2. **API Request Configuration**:
   - **Tool Name**: `N8nDrFiras`
   - **Description**: `This agent searches workflows and data inside n8n and returns results via a Respond to Webhook node.`
   - **Request URL**: `https://YOUR_N8N_URL/webhook/YOUR_WEBHOOK_ID` (Must be HTTPS)
   - **Request HTTP Method**: `POST`
3. **Parameters (Properties)**:
   - **Name**: `searchQuery` | **Type**: `String`
   - **Description**: `The search term is used to determine which relevant tool should be used. The agent processes the request using the appropriate tool and sends the result back through the Respond to Webhook node.`
   - **Required**: `Yes`

### Step 7: Entry Message

Set the **Entry Message Text** at the bottom of the configuration:

> "Hello! I'm your virtual assistant from Trugen AI. I can help you with our service packs, implementation training, or platform access. How can I make your day easier today?"

---

### Step 8: n8n Workflow Configuration

To handle the logic, scheduling, and knowledge base lookups, you must import the provided n8n workflow.

#### Option A: Manual Import (Recommended)

1. **Import Workflow**:
   - Open your n8n instance.
   - Create a new workflow.
   - Click the three dots (menu) in the top right and select **"Import from File"**.
   - Select the `Customer Support Video AI Agent.json` file.

#### Option B: Create Workflow via CURL (Super Fast)

Copy and paste this command into your terminal to instantly create the workflow. Replace the placeholders with your n8n details:

```bash
curl --request POST \
  --url "https://YOUR_INSTANCE_NAME.app.n8n.cloud/api/v1/workflows" \
  --header "Content-Type: application/json" \
  --header "X-N8N-API-KEY: YOUR_N8N_API_KEY" \
  --data @curl_payload.json
```

_(Note: You can find the full payload in [curl_command.txt](curl_command.txt) if you prefer to embed the JSON directly in the command line)_

#### Option C: Fast Import via API (Advanced)

If you have n8n API access enabled, you can use the provided scripts:

1. Open [create_workflow.ps1](create_workflow.ps1) (Windows) or [create_workflow.sh](create_workflow.sh) (Mac/Linux).
2. Update the `N8N_INSTANCE` and `N8N_API_KEY` variables.
3. Run the script to instantly create the workflow in your instance.

---

#### ⚙️ Final Node Configuration

1. **Configure Credentials**:
   - Ensure the following credentials are set up in your n8n instance:
     - **OpenAI API**: For the GPT-4.1-mini model.
     - **Google Calendar OAuth2**: For scheduling.
     - **Gmail OAuth2**: For sending confirmations.
     - **Google Sheets OAuth2**: For the knowledge base.

2. **Webhook Connection**:
   - Open the **"Webhook: Receive User Request (Trugen)"** node in n8n.
   - Copy the **Production URL** (or Test URL).
   - Go back to **Step 6** on the Trugen platform and paste this URL into the **Request URL** field.

3. **Activate Workflow**:
   - Click **"Execute Workflow"** to test or toggle the **"Active"** switch to go live.
