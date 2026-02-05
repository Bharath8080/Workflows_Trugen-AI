# Starter Guide: Creating & Interacting with the Dental Appointment AI Agent

This guide provides the direct steps to create your **Dental Appointment AI Agent** and its associated **n8n Tools**, and how to begin interacting with the finished agent.

---

## ⚡ Step 1: Create the Agent

Run the following command for your platform to create the agent using the `DENTAL_AGENT_CONFIG.json` file.

### 🍎 macOS / 🐧 Linux (Bash, Zsh)

**Using Local File:**

```bash
curl --request POST \
  --url https://api.trugen.ai/v1/ext/agent \
  --header "Content-Type: application/json" \
  --header "x-api-key: YOUR_API_KEY" \
  --data @DENTAL_AGENT_CONFIG.json
```

**Using GitHub URL:**

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
Invoke-RestMethod -Method Post -Uri "https://api.trugen.ai/v1/ext/agent" `
  -Headers @{ "Content-Type" = "application/json"; "x-api-key" = "YOUR_API_KEY" } `
  -InFile "DENTAL_AGENT_CONFIG.json"
```

### 🪟 Windows Command Prompt (CMD)

```cmd
curl -X POST "https://api.trugen.ai/v1/ext/agent" ^
  -H "Content-Type: application/json" ^
  -H "x-api-key: YOUR_API_KEY" ^
  -d @DENTAL_AGENT_CONFIG.json
```

---

## 🛠️ Step 2: Create the n8n Tools

Created these three tools to connect your agent to your n8n workflow. Replace the webhook URL placeholder with your actual production URL.

### 🍎 macOS / 🐧 Linux (Bash, Zsh)

**1. Create `get_availability`:**

```bash
curl --request POST --url https://api.trugen.ai/v1/ext/tool \
  --header "Content-Type: application/json" --header "x-api-key: YOUR_API_KEY" \
  --data '{"type":"tool.api","schema":{"type":"function","name":"get_availability","description":"Checks for available time slots.","parameters":{"type":"object","properties":{"appointmentStartTime":{"type":"string"}},"required":["appointmentStartTime"]}},"request_config":{"method":"POST","url":"https://YOUR_SUBDOMAIN.n8n.cloud/webhook/YOUR_UNIQUE_ID"}}'
```

**2. Create `create_appointment`:**

```bash
curl --request POST --url https://api.trugen.ai/v1/ext/tool \
  --header "Content-Type: application/json" --header "x-api-key: YOUR_API_KEY" \
  --data '{"type":"tool.api","schema":{"type":"function","name":"create_appointment","description":"Creates a dental appointment.","parameters":{"type":"object","properties":{"appointmentStartTime":{"type":"string"}},"required":["appointmentStartTime"]}},"request_config":{"method":"POST","url":"https://YOUR_SUBDOMAIN.n8n.cloud/webhook/YOUR_UNIQUE_ID"}}'
```

**3. Create `log_patient_details`:**

```bash
curl --request POST --url https://api.trugen.ai/v1/ext/tool \
  --header "Content-Type: application/json" --header "x-api-key: YOUR_API_KEY" \
  --data '{"type":"tool.api","schema":{"type":"function","name":"log_patient_details","description":"Logs patient info.","parameters":{"type":"object","properties":{"patientName":{"type":"string"},"callTimestamp":{"type":"string"},"insuranceProvider":{"type":"string"},"appointmentTimestamp":{"type":"string"},"questionsAndConcerns":{"type":"string"}},"required":["patientName","callTimestamp","insuranceProvider","appointmentTimestamp","questionsAndConcerns"]}},"request_config":{"method":"POST","url":"https://YOUR_SUBDOMAIN.n8n.cloud/webhook/YOUR_UNIQUE_ID"}}'
```

### 💙 Windows PowerShell

```powershell
# get_availability
Invoke-RestMethod -Method Post -Uri "https://api.trugen.ai/v1/ext/tool" `
  -Headers @{ "Content-Type" = "application/json"; "x-api-key" = "YOUR_API_KEY" } `
  -Body '{"type":"tool.api","schema":{"type":"function","name":"get_availability","description":"Checks for available slots.","parameters":{"type":"object","properties":{"appointmentStartTime":{"type":"string"}},"required":["appointmentStartTime"]}},"request_config":{"method":"POST","url":"https://YOUR_SUBDOMAIN.n8n.cloud/webhook/YOUR_UNIQUE_ID"}}'

# create_appointment
Invoke-RestMethod -Method Post -Uri "https://api.trugen.ai/v1/ext/tool" `
  -Headers @{ "Content-Type" = "application/json"; "x-api-key" = "YOUR_API_KEY" } `
  -Body '{"type":"tool.api","schema":{"type":"function","name":"create_appointment","description":"Creates an appointment.","parameters":{"type":"object","properties":{"appointmentStartTime":{"type":"string"}},"required":["appointmentStartTime"]}},"request_config":{"method":"POST","url":"https://YOUR_SUBDOMAIN.n8n.cloud/webhook/YOUR_UNIQUE_ID"}}'

# log_patient_details
Invoke-RestMethod -Method Post -Uri "https://api.trugen.ai/v1/ext/tool" `
  -Headers @{ "Content-Type" = "application/json"; "x-api-key" = "YOUR_API_KEY" } `
  -Body '{"type":"tool.api","schema":{"type":"function","name":"log_patient_details","description":"Logs patient info.","parameters":{"type":"object","properties":{"patientName":{"type":"string"},"callTimestamp":{"type":"string"},"insuranceProvider":{"type":"string"},"appointmentTimestamp":{"type":"string"},"questionsAndConcerns":{"type":"string"}},"required":["patientName","callTimestamp","insuranceProvider","appointmentTimestamp","questionsAndConcerns"]}},"request_config":{"method":"POST","url":"https://YOUR_SUBDOMAIN.n8n.cloud/webhook/YOUR_UNIQUE_ID"}}'
```

### 🪟 Windows Command Prompt (CMD)

```cmd
:: get_availability
curl -X POST "https://api.trugen.ai/v1/ext/tool" -H "Content-Type: application/json" -H "x-api-key: YOUR_API_KEY" -d "{\"type\":\"tool.api\",\"schema\":{\"type\":\"function\",\"name\":\"get_availability\",\"description\":\"Checks slots.\",\"parameters\":{\"type\":\"object\",\"properties\":{\"appointmentStartTime\":{\"type\":\"string\"}},\"required\":[\"appointmentStartTime\"]}},\"request_config\":{\"method\":\"POST\",\"url\":\"https://YOUR_SUBDOMAIN.n8n.cloud/webhook/YOUR_UNIQUE_ID\"}}"

:: create_appointment
curl -X POST "https://api.trugen.ai/v1/ext/tool" -H "Content-Type: application/json" -H "x-api-key: YOUR_API_KEY" -d "{\"type\":\"tool.api\",\"schema\":{\"type\":\"function\",\"name\":\"create_appointment\",\"description\":\"Creates appt.\",\"parameters\":{\"type\":\"object\",\"properties\":{\"appointmentStartTime\":{\"type\":\"string\"}},\"required\":[\"appointmentStartTime\"]}},\"request_config\":{\"method\":\"POST\",\"url\":\"https://YOUR_SUBDOMAIN.n8n.cloud/webhook/YOUR_UNIQUE_ID\"}}"

:: log_patient_details
curl -X POST "https://api.trugen.ai/v1/ext/tool" -H "Content-Type: application/json" -H "x-api-key: YOUR_API_KEY" -d "{\"type\":\"tool.api\",\"schema\":{\"type\":\"function\",\"name\":\"log_patient_details\",\"description\":\"Logs info.\",\"parameters\":{\"type\":\"object\",\"properties\":{\"patientName\":{\"type\":\"string\"},\"callTimestamp\":{\"type\":\"string\"},\"insuranceProvider\":{\"type\":\"string\"},\"appointmentTimestamp\":{\"type\":\"string\"},\"questionsAndConcerns\":{\"type\":\"string\"}},\"required\":[\"patientName\",\"callTimestamp\",\"insuranceProvider\",\"appointmentTimestamp\",\"questionsAndConcerns\"]}},\"request_config\":{\"method\":\"POST\",\"url\":\"https://YOUR_SUBDOMAIN.n8n.cloud/webhook/YOUR_UNIQUE_ID\"}}"
```

---

## 🎨 Step 3: Finalizing Setup in Trugen Dashboard

1.  **Log in**: Go to your [Trugen AI Dashboard](https://app.trugen.ai/).
2.  **Verify**: Ensure agent **"Dental Appointment Agent"** and the three dental tools are visible.
3.  **Edit Agent**: Click to **Edit** the "Dental Appointment Agent" agent.
4.  **Link Tools**:
    - Navigate to the **Tools** section.
    - Select **get_availability**, **create_appointment**, and **log_patient_details**.
5.  **Save**: Click **Save Agent**.

---

## 🚦 Final Checklist

1. **API Key**: Ensure `YOUR_API_KEY` is replaced in all commands.
2. **Webhook URL**: All tools must point to your production n8n webhook URL.
3. **Configurations**: Use the local `.json` files for the most reliable setup.
