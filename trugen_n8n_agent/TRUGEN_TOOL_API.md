# Trugen Tool API Creation

Below are **working versions of your exact request** for each environment.

---

## 🪟 Windows **Command Prompt (CMD)**

```cmd
curl -X POST "https://api.trugen.ai/v1/ext/tool" ^
 -H "Content-Type: application/json" ^
 -H "x-api-key: YOUR_API_KEY" ^
 -d "{\"type\":\"tool.api\",\"schema\":{\"type\":\"function\",\"name\":\"N8n_Customer_Support\",\"description\":\"This agent searches workflows and data inside n8n and returns results via a Respond to Webhook node.\",\"parameters\":{\"type\":\"object\",\"properties\":{\"searchQuery\":{\"type\":\"string\",\"description\":\"The search term is used to determine which relevant tool should be used. The agent processes the request using the appropriate tool and sends the result back through the Respond to Webhook node.\"}},\"required\":[\"searchQuery\"]}},\"request_config\":{\"method\":\"POST\",\"url\":\"https://YOUR_SUBDOMAIN.n8n.cloud/webhook/YOUR_UNIQUE_ID\",\"headers\":{}},\"event_messages\":{\"on_start\":{\"message\":\"Processing...\"},\"on_success\":{\"message\":\"Success!\"},\"on_delay\":{\"delay\":3000,\"message\":\"Working...\"},\"on_error\":{\"message\":\"Failed.\"}}}"
```

**CMD Rules**

- Line break = `^`
- Only double quotes
- Escape JSON quotes as `\"`

---

## 💙 Windows **PowerShell**

```powershell
curl -Method POST "https://api.trugen.ai/v1/ext/tool" `
 -Headers @{
   "Content-Type" = "application/json"
   "x-api-key"    = "YOUR_API_KEY"
 } `
 -Body '{
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
          "description": "The search term is used to determine which relevant tool should be used. The agent processes the request using the appropriate tool and sends the result back through the Respond to Webhook node."
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

---

## 🍎 macOS / 🐧 Linux (Bash, Zsh)

This is the format your original command was meant for:

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
          "description": "The search term is used to determine which relevant tool should be used. The agent processes the request using the appropriate tool and sends the result back through the Respond to Webhook node."
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

---

## 🔁 Don’t Forget

Replace:

```
https://YOUR_SUBDOMAIN.n8n.cloud/webhook/YOUR_UNIQUE_ID
```

with your real n8n webhook URL.

---

### ⭐ Pro Tip (Works Everywhere)

Save JSON as **body.json**, then run:

```bash
curl -X POST https://api.trugen.ai/v1/ext/tool \
 -H "Content-Type: application/json" \
 -H "x-api-key: YOUR_API_KEY" \
 --data @body.json
```

No escaping issues, cleaner, easier to edit.
