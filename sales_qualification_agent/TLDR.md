# Create a B2B sales qualification agent with GPT-4o and HubSpot CRM sync

This n8n template creates a high-performance Sales Intelligence agent designed for automated lead discovery. Optimized for **Trugen AI**'s low-latency voice and video interfaces, it manages prospect interactions using the **BANT framework**, ensuring every lead is qualified, scored, and routed before it reaches your sales team.

## 👥 Who is this for?

- **Sales Operations Managers** looking to automate initial discovery and CRM data entry.
- **SDR & BDR Teams** wanting to focus only on highly qualified "Hot" leads.
- **B2B SaaS Businesses** with high lead volumes requiring instant qualification.
- **Growth Marketers** aiming to bridge the gap between marketing leads and sales bookings.

## 💡 What problem is this workflow solving?

B2B sales teams often suffer from:

- **Slow Response Times**: Leads going cold while waiting for a discovery call.
- **Manual Qualification**: Reps spending time on leads that lack budget or authority.
- **Inconsistent Data**: Missing or fragmented qualification details in the CRM.

This workflow solves these by using **OpenAI GPT-4o** reasoning to perform deep BANT analysis (Budget, Authority, Need, Timeline), calculate a qualification score (0-100), and automatically route leads to the correct rep in **HubSpot**.

## ⚙️ What this workflow does

- **Qualifies Leads**: Captures sales calls via Trugen AI and extracts explicit BANT signals.
- **Scores & Tiers**: Assigns a lead score and categorizes prospects into Hot, Warm, or Cold tiers.
- **Intelligent Routing**: Automatically assigns leads to Senior, Mid-Level, or SDR reps based on score and industry expertise.
- **Syncs CRM**: Creates or updates contacts in **HubSpot** with full qualification context and AI-derived insights.
- **Drives Communication**: Sends personalized confirmation emails to prospects and internal "Hot Lead" alerts to sales reps via **Gmail**.
- **Tracks Insights**: Logs comprehensive "Minutes of Meeting" (MOM), red flags, and competitive vulnerabilities to **Google Sheets**.

## 🧰 Setup

- **OpenAI**: Connect your API key (optimized for GPT-4o for complex scoring).
- **HubSpot**: Connect your HubSpot App Token for CRM synchronization.
- **Google Workspace**: Enable and connect Google Sheets and Gmail.
- **Webhook**: Link the workflow's Webhook URL to your Trugen AI Callback settings (Event: Call Ended).
- **Routing Logic**: Update the "Intelligent Routing" code node to match your specific sales team and industry mapping.

## 🛠️ How to customize this workflow

- **Scoring Model**: Adjust the BANT weights if certain criteria (like "Need") are more important for your sales process.
- **CRM Mapping**: Customize the HubSpot node to sync data to custom properties or Deal objects.
- **Team Loading**: Update the team capacity and specialization settings in the Routing Engine node.
- **Omnichannel Alerts**: Add Slack or Microsoft Teams nodes for real-time sales floor notifications.
