# Starter Guide: Creating & Interacting with the Customer Support AI Agent

This guide provides the direct steps to create your **Customer Support AI Agent** and its associated **n8n Tool**, and how to begin interacting with the finished agent.

---

## ⚡ Step 1: Create the Agent

Run the following command for your platform to create the agent using the `TRUGEN_AGENT_CONFIG.json` file.

---

---

## 🍎 macOS / 🐧 Linux (Bash, Zsh)

**Using Local File:**

```bash
curl --request POST \
  --url https://api.trugen.ai/v1/ext/agent \
  --header "Content-Type: application/json" \
  --header "x-api-key: YOUR_API_KEY" \
  --data @TRUGEN_AGENT_CONFIG.json
```

**Using GitHub URL (No Download Needed):**

```bash
curl -s https://raw.githubusercontent.com/Bharath8080/Workflows_Trugen-AI/refs/heads/main/Customer-Support-AI-Agent/TRUGEN_AGENT_CONFIG.json | \
curl --request POST \
  --url https://api.trugen.ai/v1/ext/agent \
  --header "Content-Type: application/json" \
  --header "x-api-key: YOUR_API_KEY" \
  --data @-
```

---

## 💙 Windows **PowerShell**

**Using Local File:**

```powershell
Invoke-RestMethod -Method Post -Uri "https://api.trugen.ai/v1/ext/agent" `
  -Headers @{ "Content-Type" = "application/json"; "x-api-key" = "YOUR_API_KEY" } `
  -InFile "TRUGEN_AGENT_CONFIG.json"
```

**Using GitHub URL:**

```powershell
$config = Invoke-RestMethod -Uri "https://raw.githubusercontent.com/Bharath8080/Workflows_Trugen-AI/refs/heads/main/Customer-Support-AI-Agent/TRUGEN_AGENT_CONFIG.json"
Invoke-RestMethod -Method Post -Uri "https://api.trugen.ai/v1/ext/agent" `
  -Headers @{ "Content-Type" = "application/json"; "x-api-key" = "YOUR_API_KEY" } `
  -Body ($config | ConvertTo-Json -Depth 10)
```

---

## 🪟 Windows **Command Prompt (CMD)**

```cmd
curl -X POST "https://api.trugen.ai/v1/ext/agent" ^
  -H "Content-Type: application/json" ^
  -H "x-api-key: YOUR_API_KEY" ^
  -d @TRUGEN_AGENT_CONFIG.json
```

---

### 3. Verify Agent Success

After running the command, the API will return an `agent_id`. Keep this for your records.

---

## 🛠️ Step 2: Create the n8n Tool

Unlike the agent, the tool configuration is small enough to run as a single command. Run the following to connect your agent to your n8n workflow.

### 🍎 macOS / 🐧 Linux (Bash, Zsh)

```bash
curl --request POST \
  --url https://api.trugen.ai/v1/ext/tool \
  --header "Content-Type: application/json" \
  --header "x-api-key: YOUR_API_KEY" \
  --data '{
  "type": "tool.api",
  "schema": {
    "type": "function",
    "name": "N8n_Customer_Support",
    "description": "This agent searches workflows and data inside n8n and returns results via a Respond to Webhook node.",
    "parameters": {
      "type": "object",
      "properties": {
        "searchQuery": {
          "type": "string",
          "description": "The search term is used to determine which relevant tool should be used."
        }
      },
      "required": ["searchQuery"]
    }
  },
  "request_config": {
    "method": "POST",
    "url": "https://YOUR_SUBDOMAIN.n8n.cloud/webhook/YOUR_UNIQUE_ID",
    "headers": {}
  },
  "event_messages": {
    "on_start": { "message": "Processing..." },
    "on_success": { "message": "Success!" },
    "on_delay": { "delay": 3000, "message": "Working..." },
    "on_error": { "message": "Failed." }
  }
}'
```

### 💙 Windows **PowerShell**

```powershell
Invoke-RestMethod -Method Post -Uri "https://api.trugen.ai/v1/ext/tool" `
  -Headers @{ "Content-Type" = "application/json"; "x-api-key" = "YOUR_API_KEY" } `
  -Body '{
  "type": "tool.api",
  "schema": {
    "type": "function",
    "name": "N8n_Customer_Support",
    "description": "This agent searches workflows and data inside n8n and returns results via a Respond to Webhook node.",
    "parameters": {
      "type": "object",
      "properties": {
        "searchQuery": { "type": "string", "description": "The search term." }
      },
      "required": ["searchQuery"]
    }
  },
  "request_config": {
    "method": "POST",
    "url": "https://YOUR_SUBDOMAIN.n8n.cloud/webhook/YOUR_UNIQUE_ID"
  },
  "event_messages": {
    "on_start": { "message": "Processing..." },
    "on_success": { "message": "Success!" },
    "on_error": { "message": "Failed." }
  }
}'
```

### 🪟 Windows **Command Prompt (CMD)**

```cmd
curl -X POST "https://api.trugen.ai/v1/ext/tool" ^
  -H "Content-Type: application/json" ^
  -H "x-api-key: YOUR_API_KEY" ^
  -d "{\"type\":\"tool.api\",\"schema\":{\"type\":\"function\",\"name\":\"N8n_Customer_Support\",\"description\":\"This agent searches workflows and data inside n8n and returns results via a Respond to Webhook node.\",\"parameters\":{\"type\":\"object\",\"properties\":{\"searchQuery\":{\"type\":\"string\",\"description\":\"The search term is used to determine which relevant tool should be used. The agent processes the request using the appropriate tool and sends the result back through the Respond to Webhook node.\"}},\"required\":[\"searchQuery\"]}},\"request_config\":{\"method\":\"POST\",\"url\":\"https://YOUR_SUBDOMAIN.n8n.cloud/webhook/YOUR_UNIQUE_ID\"},\"event_messages\":{\"on_start\":{\"message\":\"Processing...\"},\"on_success\":{\"message\":\"Success!\"},\"on_delay\":{\"delay\":3000,\"message\":\"Working...\"},\"on_error\":{\"message\":\"Failed.\"}}}"
```

---

## 🎨 Step 3: Finalizing Setup in Trugen Dashboard

Once you have successfully run the CURL commands for both the **Agent** and the **Tool**, follow these steps to link them and start your conversation:

1.  **Log in**: Go to your [Trugen AI Dashboard](https://app.trugen.ai/).
2.  **Verify**: You will see your new agent named **"Customer Support Agent"** and your tool named **"N8n_Customer_Support"**.
3.  **Edit Agent**: Click to **Edit** the "Customer Support Agent".
4.  **Link Tool**:
    - Navigate to the **Tools** section within the agent editor.
    - Select the **"N8n_Customer_Support"** tool from the list.
5.  **Save**: Click **Save Agent** to apply the changes.

> [!IMPORTANT]
> **Check your Webhook**: Double-check that your n8n Production Webhook URL is correctly added to your tool settings before saving.

### 🎉 Success!

You are now ready to interact with your **Customer Support Agent**. Open the agent link or embed the iframe to start a high-performance video conversation powered by Trugen AI and n8n!

---

## 🚦 Final Checklist

1. **API Key**: Ensure `YOUR_API_KEY` is replaced in both the Agent and Tool commands.
2. **Webhook URL**: The Tool command MUST have your Production n8n Webhook URL.
3. **Deployment Mode**: Use the GitHub URL method for the cleanest agent creation experience.
