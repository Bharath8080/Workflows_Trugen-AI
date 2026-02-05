# Starter Guide: Creating & Interacting with the Dental Appointment AI Agent

This guide provides the direct steps to create your **Dental Appointment AI Agent** and its associated **n8n Tools**.

---

## ⚡ Step 1: Create the Agent

Run the following command for your platform. This uses the `DENTAL_AGENT_CONFIG.json` hosted on GitHub to ensure the latest configuration is used.

### 🍎 macOS / 🐧 Linux (Bash, Zsh)

```bash
curl -s https://raw.githubusercontent.com/Bharath8080/Workflows_Trugen-AI/refs/heads/main/dental_appointment_agent/DENTAL_AGENT_CONFIG.json | \
curl --request POST \
  --url https://api.trugen.ai/v1/ext/agent \
  --header "Content-Type: application/json" \
  --header "x-api-key: YOUR_API_KEY" \
  --data @-
```

### 💙 Windows PowerShell

```powershell
$config = Invoke-RestMethod -Uri "https://raw.githubusercontent.com/Bharath8080/Workflows_Trugen-AI/refs/heads/main/dental_appointment_agent/DENTAL_AGENT_CONFIG.json"
Invoke-RestMethod -Method Post -Uri "https://api.trugen.ai/v1/ext/agent" `
  -Headers @{ "Content-Type" = "application/json"; "x-api-key" = "YOUR_API_KEY" } `
  -Body ($config | ConvertTo-Json -Depth 10)
```

---

## 🛠️ Step 2: Create the n8n Tools

Run these commands to create the three tools required for the workflow. Replace the webhook URL placeholder with your production URL.

### 🍎 macOS / 🐧 Linux (Bash, Zsh)

**1. Create `get_availability`:**

```bash
curl --request POST \
  --url https://api.trugen.ai/v1/ext/tool \
  --header "Content-Type: application/json" \
  --header "x-api-key: YOUR_API_KEY" \
  --data '{
  "type": "tool.api",
  "schema": {
    "type": "function",
    "name": "get_availability",
    "description": "This tool checks whether a specific appointment time slot is available on the Pearly Whites Dental calendar using an n8n webhook.",
    "parameters": {
      "type": "object",
      "properties": {
        "appointmentStartTime": {
          "type": "string",
          "description": "The requested appointment start timestamp in Central Time that needs to be checked for availability."
        }
      },
      "required": ["appointmentStartTime"]
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

**2. Create `create_appointment`:**

```bash
curl --request POST \
  --url https://api.trugen.ai/v1/ext/tool \
  --header "Content-Type: application/json" \
  --header "x-api-key: YOUR_API_KEY" \
  --data '{
  "type": "tool.api",
  "schema": {
    "type": "function",
    "name": "create_appointment",
    "description": "This tool creates a dental appointment in the Pearly Whites Dental scheduling system via an n8n webhook.",
    "parameters": {
      "type": "object",
      "properties": {
        "appointmentStartTime": {
          "type": "string",
          "description": "The confirmed appointment start timestamp in Central Time. The appointment duration is automatically 1 hour."
        }
      },
      "required": ["appointmentStartTime"]
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

**3. Create `log_patient_details`:**

```bash
curl --request POST \
  --url https://api.trugen.ai/v1/ext/tool \
  --header "Content-Type: application/json" \
  --header "x-api-key: YOUR_API_KEY" \
  --data '{
  "type": "tool.api",
  "schema": {
    "type": "function",
    "name": "log_patient_details",
    "description": "This tool logs patient call details and appointment information into a Google Sheet via an n8n webhook.",
    "parameters": {
      "type": "object",
      "properties": {
        "patientName": {
          "type": "string",
          "description": "Full name of the patient who called and booked the appointment."
        },
        "callTimestamp": {
          "type": "string",
          "description": "The timestamp representing when the patient call was handled. This must be derived from the system time."
        },
        "insuranceProvider": {
          "type": "string",
          "description": "The patient’s dental insurance provider."
        },
        "appointmentTimestamp": {
          "type": "string",
          "description": "The confirmed appointment start time that was scheduled using the create_appointment tool."
        },
        "questionsAndConcerns": {
          "type": "string",
          "description": "Any symptoms, dental issues, or questions the patient mentioned during the call. Leave empty if none were provided."
        }
      },
      "required": ["patientName", "callTimestamp", "insuranceProvider", "appointmentTimestamp", "questionsAndConcerns"]
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
# 1. get_availability
Invoke-RestMethod -Method Post -Uri "https://api.trugen.ai/v1/ext/tool" `
  -Headers @{ "Content-Type" = "application/json"; "x-api-key" = "YOUR_API_KEY" } `
  -Body '{
  "type": "tool.api",
  "schema": {
    "type": "function",
    "name": "get_availability",
    "description": "This tool checks whether a specific appointment time slot is available on the Pearly Whites Dental calendar using an n8n webhook.",
    "parameters": {
      "type": "object",
      "properties": {
        "appointmentStartTime": {
          "type": "string",
          "description": "The requested appointment start timestamp in Central Time that needs to be checked for availability."
        }
      },
      "required": ["appointmentStartTime"]
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

# 2. create_appointment
Invoke-RestMethod -Method Post -Uri "https://api.trugen.ai/v1/ext/tool" `
  -Headers @{ "Content-Type" = "application/json"; "x-api-key" = "YOUR_API_KEY" } `
  -Body '{
  "type": "tool.api",
  "schema": {
    "type": "function",
    "name": "create_appointment",
    "description": "This tool creates a dental appointment in the Pearly Whites Dental scheduling system via an n8n webhook.",
    "parameters": {
      "type": "object",
      "properties": {
        "appointmentStartTime": {
          "type": "string",
          "description": "The confirmed appointment start timestamp in Central Time. The appointment duration is automatically 1 hour."
        }
      },
      "required": ["appointmentStartTime"]
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

# 3. log_patient_details
Invoke-RestMethod -Method Post -Uri "https://api.trugen.ai/v1/ext/tool" `
  -Headers @{ "Content-Type" = "application/json"; "x-api-key" = "YOUR_API_KEY" } `
  -Body '{
  "type": "tool.api",
  "schema": {
    "type": "function",
    "name": "log_patient_details",
    "description": "This tool logs patient call details and appointment information into a Google Sheet via an n8n webhook.",
    "parameters": {
      "type": "object",
      "properties": {
        "patientName": {
          "type": "string",
          "description": "Full name of the patient who called and booked the appointment."
        },
        "callTimestamp": {
          "type": "string",
          "description": "The timestamp representing when the patient call was handled. This must be derived from the system time."
        },
        "insuranceProvider": {
          "type": "string",
          "description": "The patient dental insurance provider."
        },
        "appointmentTimestamp": {
          "type": "string",
          "description": "The confirmed appointment start time that was scheduled using the create_appointment tool."
        },
        "questionsAndConcerns": {
          "type": "string",
          "description": "Any symptoms, dental issues, or questions the patient mentioned during the call. Leave empty if none were provided."
        }
      },
      "required": ["patientName", "callTimestamp", "insuranceProvider", "appointmentTimestamp", "questionsAndConcerns"]
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
2.  **Verify**: Ensure agent **"Dental Appointment Agent"** and the three tools are visible.
3.  **Edit Agent**: Link the **get_availability**, **create_appointment**, and **log_patient_details** tools.
4.  **Save**: Click **Save Agent**.
