# Starter Guide: Creating & Interacting with the Customer Support AI Agent

This guide provides the direct steps to create your **Customer Support AI Agent** and its associated **n8n Tool** directly from GitHub.

---

## ⚡ Step 1: Create the Agent

Run the following command for your platform. This uses the `TRUGEN_AGENT_CONFIG.json` hosted on GitHub to ensure the latest configuration is used.

### 🍎 macOS / 🐧 Linux (Bash, Zsh)

```bash
curl -s https://raw.githubusercontent.com/Bharath8080/Workflows_Trugen-AI/refs/heads/main/Customer-Support-AI-Agent/TRUGEN_AGENT_CONFIG.json | \
curl --request POST \
  --url https://api.trugen.ai/v1/ext/agent \
  --header "Content-Type: application/json" \
  --header "x-api-key: YOUR_API_KEY" \
  --data @-
```

### 💙 Windows PowerShell

```powershell
$config = Invoke-RestMethod -Uri "https://raw.githubusercontent.com/Bharath8080/Workflows_Trugen-AI/refs/heads/main/Customer-Support-AI-Agent/TRUGEN_AGENT_CONFIG.json"
Invoke-RestMethod -Method Post -Uri "https://api.trugen.ai/v1/ext/agent" `
  -Headers @{ "Content-Type" = "application/json"; "x-api-key" = "YOUR_API_KEY" } `
  -Body ($config | ConvertTo-Json -Depth 10)
```

---

## 🛠️ Step 2: Create the n8n Tool

Run the following to connect your agent to your n8n workflow. Replace the webhook URL placeholder with your actual production URL.

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
    "name": "n8n_tool",
    "description": "This agent searches workflows and data inside n8n and returns results via a Respond to Webhook node.",
    "parameters": {
      "type": "object",
      "properties": {
        "searchQuery": {
          "type": "string",
          "description": "The search term is used to determine which relevant tool should be used. The agent processes the request using the appropriate tool and sends the result back through the Respond to Webhook node."
        }
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

### 💙 Windows PowerShell

```powershell
Invoke-RestMethod -Method Post -Uri "https://api.trugen.ai/v1/ext/tool" `
  -Headers @{ "Content-Type" = "application/json"; "x-api-key" = "YOUR_API_KEY" } `
  -Body '{
  "type": "tool.api",
  "schema": {
    "type": "function",
    "name": "n8n_tool",
    "description": "This agent searches workflows and data inside n8n and returns results via a Respond to Webhook node.",
    "parameters": {
      "type": "object",
      "properties": {
        "searchQuery": {
          "type": "string",
          "description": "The search term is used to determine which relevant tool should be used. The agent processes the request using the appropriate tool and sends the result back through the Respond to Webhook node."
        }
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

---

## 🎨 Step 3: Finalizing Setup in Trugen Dashboard

1.  **Log in**: Go to your [Trugen AI Dashboard](https://app.trugen.ai/).
2.  **Verify**: Ensure agent **"Customer Support Agent"** and tool **"n8n_tool"** are visible.
3.  **Edit Agent**: Link the **"n8n_tool"** tool.
4.  **Save**: Click **Save Agent**.
