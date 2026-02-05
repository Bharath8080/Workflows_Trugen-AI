# Pearly Whites Dental Appointment Handling Agent

This README provides a guide for setting up the **Dental Appointment** AI Agent. This workflow acts as a virtual back-office assistant, managing calendar availability, patient bookings, and administrative records.

---

## 🚀 Step-by-Step Platform Setup

### Step 1: Account Access

- Access the [Trugen AI Platform](https://trugen.ai/).
- Go to the [Create Agent](https://app.trugen.ai/dashboard/create-agent-basic) section.

### Step 2: Virtual Assistant Settings

- **Agent Name**: `Pearly Whites Assistant`
- **Avatar**: Professional clinical avatar.
- **LLM**: `GPT-4.1 mini` for speed and reasoning.
- **STT**: `Deepgram Nova-3`.

### Step 3: Back-Office Logic

The agent uses **Tools** to interact with clinic systems. Ensure the system prompt includes these tool rules:

- **get_availability**: Checks Google Calendar for CST slots.
- **create_appointment**: Books 1-hour slots.
- **log_patient_details**: Saves insurance and contact info.

---

## 🏗️ n8n Workflow Operation

The workflow is divided into three key stages to ensure a smooth patient experience:

### 🟢 Stage 1: Receive Request

The **Webhook Trigger** captures patient voice/video input from the Trugen terminal. It receives the transcription and session metadata.

### 🔵 Stage 2: AI Reasoning & Tool Execution

The **GPT-4.1 mini reasoning engine** determines the patient's intent:

- **Checking Dates**: Queries the calendar tool for multiple 30-60 min slots.
- **Booking**: Once a time is confirmed, it commits the 1-hour event to the calendar.
- **Onboarding**: For new patients, it collects and logs insurance details to a secure Google Sheet.

### 🟣 Stage 3: Confirmation

The workflow returns a structured status response to the video agent, enabling it to say: "Success! Your appointment for Tuesday at 2 PM is confirmed."

---

## 🛠️ Requirements

- **Trugen AI API Access**.
- **OpenAI API Key**.
- **Google Calendar API**: Connected to the clinic's master calendar.
- **Google Sheets API**: For patient record tracking.
