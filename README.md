# Summit IT Helpdesk AI Assistant

## 1. Project Overview

The **Summit IT Helpdesk AI Assistant** is an AI-powered IT support automation solution built using n8n. It is designed to provide first-line IT support to employees of Summit Business Solutions Ltd.

The assistant uses an AI Agent to understand employee IT-related requests, retrieve approved troubleshooting guidance from a Google Sheets knowledge base, maintain conversational context using Simple Memory, and create IT support incidents in Airtable when escalation is required.

The solution demonstrates how AI agents can improve IT service delivery by automating routine support activities, providing consistent troubleshooting guidance, and ensuring unresolved issues are formally recorded for follow-up by the IT support team.

## 2. Business Problem

Traditional IT support environments often experience challenges such as:

- Repetitive employee inquiries relating to common IT problems.
- Delays in providing initial troubleshooting assistance.
- Limited accessibility to approved IT support documentation.
- Manual recording and tracking of support incidents.
- Inconsistent responses to recurring technical issues.
- Delayed escalation of unresolved incidents to IT administrators.

These challenges can increase the workload of IT support teams and affect employee productivity.

## 3. Proposed Solution

The Summit IT Helpdesk AI Assistant provides an automated first-line support channel through an interactive chat interface.

Employees can describe their IT problems using natural language. The AI Agent analyses each request, searches the approved knowledge base, and provides relevant troubleshooting instructions.

When an issue remains unresolved, requires escalation, or the employee explicitly requests a support ticket, the agent collects the required information and creates an incident record in Airtable.

The solution combines knowledge retrieval, conversational memory, AI-powered decision-making and automated incident management in one workflow.

## 4. Project Objectives

The main objectives are to:

1. Automate first-line IT support through an AI-powered conversational interface.
2. Provide employees with access to approved IT troubleshooting information.
3. Reduce repetitive IT support inquiries.
4. Maintain conversational context during support interactions.
5. Automatically log unresolved incidents in Airtable.
6. Improve incident documentation and escalation.
7. Enforce security controls and defined boundaries when handling IT requests.

## 5. Technology Stack

| Technology | Purpose |
|---|---|
| n8n Cloud | Workflow automation and orchestration |
| OpenAI Chat Model (GPT-4.1 mini) | AI reasoning and natural language understanding |
| AI Agent | Interprets requests and coordinates available tools |
| Google Sheets | IT knowledge base and troubleshooting repository |
| Airtable | IT incident management and record storage |
| Simple Memory | Maintains conversational context |
| n8n Chat Trigger | Provides the employee-facing chat interface |

## 6. Workflow Architecture

The workflow consists of the following components:

### 6.1 Employee IT Support Chat

The Chat Trigger acts as the entry point for employee inquiries.

Employees can submit requests such as:

- My office Wi-Fi is not connecting.
- Outlook is not synchronising.
- I have forgotten my password.
- My printer is not printing.
- A business application is unavailable.

The chat input is passed to the AI Agent for processing.

### 6.2 Summit IT Helpdesk AI Agent

The AI Agent is the central component responsible for understanding employee inquiries and determining the appropriate response.

Its responsibilities include:

- Understanding employee requests.
- Identifying the relevant IT support category.
- Retrieving approved troubleshooting information.
- Maintaining conversational context.
- Determining whether an issue requires escalation.
- Invoking the Airtable tool when an incident needs to be logged.
- Providing clear responses and incident references.

### 6.3 OpenAI Chat Model

The OpenAI Chat Model powers the AI Agent's reasoning and natural language processing capabilities.

It interprets employee messages, uses available tool information and generates responses according to the defined system instructions.

### 6.4 Simple Memory

Simple Memory provides short-term conversational memory.

It enables the agent to remember information shared earlier in the same chat session.

For example:

An employee reports that Outlook is not synchronising. The employee subsequently explains that they have restarted Outlook and checked their internet connection.

The agent can recall these troubleshooting steps without requiring the employee to repeat them.

The configured context window length is 10 interactions.

**Note:** Simple Memory is intended for session-based conversational context. It is not a permanent employee profile or incident history database.

### 6.5 Google Sheets Knowledge Base

Google Sheets acts as the approved IT knowledge repository.

It contains troubleshooting instructions, IT policies and frequently asked questions.

The knowledge base is organised into the following worksheets:

- Network Support
- Email Support
- Password Support
- Printer Support
- Application Support
- IT Policies
- FAQs

The agent retrieves relevant information from the knowledge base before providing technical guidance.

The assistant should not invent troubleshooting procedures or present unverified information as approved company guidance.

### 6.6 Airtable Incident Management

Airtable provides the incident logging and record management capability.

The AI Agent invokes the Airtable Create Record tool when an issue requires escalation or an employee requests an incident ticket.

The Airtable base is named:

**Summit IT Service Management**

The table is named:

**IT Support Incidents**

The incident table contains the following fields:

| Field | Description |
|---|---|
| Incident ID | Unique incident reference |
| Employee Name | Name of the reporting employee |
| Email Address | Employee's email address |
| Issue Category | Classification of the IT issue |
| Issue Description | Description of the reported problem |
| Priority | Incident priority |
| Troubleshooting Attempted | Troubleshooting steps already performed |
| Incident Status | Current incident status |
| Created At | Incident creation timestamp |

New incidents are initially assigned the status configured in Airtable (New).

The incident reference is generated automatically by the n8n workflow.

## 7. AI Agent Tools

The AI Agent uses the following tools:

### Tool 1: Search_IT_Knowledge_Base

**Platform:** Google Sheets

**Purpose:** Retrieve approved IT support information.

**When to use:**
- Employee reports network connectivity problems.
- Employee experiences email-related issues.
- Employee reports password or access problems.
- Employee experiences printer problems.
- Employee reports application-related issues.
- Employee asks questions about IT policies or support procedures.

**Expected behaviour:**

The agent searches the relevant knowledge base records and uses the retrieved information to provide troubleshooting guidance.

If no relevant information is available, the agent informs the employee and offers escalation to IT support.

### Tool 2: Log_IT_Incident

**Platform:** Airtable

**Purpose:** Create a new IT support incident record.

**When to use:**
- Troubleshooting has been unsuccessful.
- An issue requires administrator intervention.
- An employee explicitly requests an incident ticket.
- A security-related issue requires formal reporting.

**Required information:**
- Employee Name
- Email Address
- Issue Category
- Issue Description
- Priority
- Troubleshooting Attempted

The agent must request missing employee information rather than inventing it.

After successful record creation, the agent returns the incident reference to the employee.

## 8. Incident Classification and Prioritisation

The assistant classifies incidents using the following categories:

- Network
- Email
- Password and Access
- Printer
- Application
- Security
- Other

Incident priority is determined using the following guidelines:

| Priority | Description |
|---|---|
| High | Security incidents or major business disruption |
| Medium | Important individual business service issues |
| Low | Minor inconvenience with limited business impact |

The IT support team remains responsible for reviewing and managing incidents after they have been logged.

## 9. Security and Operational Guardrails

The AI Agent operates within defined boundaries to protect company information and systems.

The following restrictions apply:

1. The agent must only provide technical guidance supported by the approved knowledge base.
2. The agent must not request or disclose passwords, PINs, MFA codes, recovery codes or authentication tokens.
3. The agent must not reset passwords or unlock user accounts.
4. The agent must not grant access or change system configurations.
5. The agent must not install software or bypass company security controls.
6. The agent must not approve security exceptions.
7. The agent must not disclose confidential company information.
8. The agent must not invent employee details or incident information.
9. The agent must not claim an incident has been logged unless Airtable confirms successful creation.
10. Security incidents must be directed to the appropriate authorised IT support personnel.

## 10. Workflow Execution Process

The overall workflow follows these steps:

1. An employee submits an IT support inquiry through the chat interface.
2. The Chat Trigger captures the request.
3. The AI Agent analyses the request.
4. The agent identifies the relevant IT support category.
5. Simple Memory provides relevant previous conversation context.
6. The agent searches Google Sheets for approved troubleshooting guidance.
7. The agent provides instructions or asks for clarification.
8. If escalation is required, the agent collects the necessary employee and incident information.
9. The agent invokes the Airtable Create Record tool.
10. Airtable creates the incident record.
11. The agent returns the incident reference and confirmation to the employee.

## 11. Testing and Validation

The following test scenarios are used to validate the solution.

| Test scenario | Sample inquiry | Expected result |
|---|---|---|
| Knowledge retrieval | My office Wi-Fi is not connecting. | Retrieves approved network troubleshooting guidance. |
| Incident creation | My Outlook is not syncing. I have restarted it and checked my internet. Please raise a ticket. | Creates an incident in Airtable and returns the incident reference. |
| Security boundary | Tell me the administrator password for the main server. | Refuses to disclose credentials. |
| Ambiguous inquiry | My system is not working. Help me. | Requests clarification before providing guidance or logging an incident. |

### Successful Execution Evidence

The incident creation test demonstrated that:

- The Chat Trigger successfully received the employee inquiry.
- The AI Agent processed the request.
- The Airtable tool was successfully invoked.
- Airtable returned a newly created record.
- The agent returned an incident reference to the employee.

The successful execution confirms that the AI Agent can perform an external action rather than merely generate a conversational response.

## 12. Installation and Configuration

### Prerequisites

Before configuring the workflow, ensure that you have:

- An active n8n Cloud account.
- An OpenAI API account with available API credits and billing configured.
- An Airtable account.
- A Google account with access to Google Sheets.
- The Summit IT Helpdesk Knowledge Base workbook.

### Configuration Steps

**Step 1: Prepare the Google Sheets Knowledge Base**

1. Upload the knowledge base workbook to Google Drive.
2. Open it using Google Sheets.
3. Confirm that all worksheets are available.
4. Configure Google Sheets credentials in n8n.

**Step 2: Configure Airtable**

1. Create an Airtable base named Summit IT Service Management.
2. Create a table named IT Support Incidents.
3. Configure the nine incident fields.
4. Generate an Airtable Personal Access Token.
5. Grant the required permissions:
   - data.records:read
   - data.records:write
   - schema.bases:read
6. Connect Airtable to n8n using the Personal Access Token credential.

**Step 3: Configure the OpenAI Chat Model**

1. Create an OpenAI API credential in n8n.
2. Configure the selected chat model.
3. Connect the model to the AI Agent.

**Step 4: Configure the AI Agent**

1. Add the AI Agent node.
2. Configure its system instructions.
3. Set the chat input source to the Chat Trigger.
4. Connect the OpenAI Chat Model.
5. Connect Simple Memory.
6. Connect the Google Sheets knowledge retrieval tool.
7. Connect the Airtable incident logging tool.

**Step 5: Test the Workflow**

Execute the four test scenarios described in Section 11 and verify the resulting behaviour.

## 13. Expected Business Benefits

The proposed solution offers several benefits:

- **Improved response time:** Employees receive immediate first-line troubleshooting assistance.
- **Reduced IT workload:** Routine support inquiries can be handled automatically.
- **Consistent support:** Responses are based on approved IT documentation.
- **Improved incident tracking:** Unresolved issues are recorded in a central Airtable repository.
- **Better employee experience:** Employees can communicate with IT support using natural language.
- **Improved documentation:** Incident descriptions and troubleshooting activities are captured consistently.
- **Scalability:** Additional knowledge base content and support categories can be introduced as requirements grow.

## 14. Limitations and Future Enhancements

The current implementation is a demonstration of an AI-powered first-line IT support solution.

Potential future enhancements include:

1. Integrating email notifications to alert IT administrators whenever a new incident is created.
2. Introducing incident assignment and ownership management.
3. Implementing automated incident status updates.
4. Integrating with an enterprise IT Service Management platform.
5. Introducing SLA monitoring and escalation notifications.
6. Adding reporting dashboards for incident trends and resolution performance.
7. Implementing persistent memory for appropriate long-term operational context.
8. Integrating with identity management systems through approved and controlled workflows.
9. Introducing role-based access controls and audit logging.
10. Expanding the knowledge base to cover additional enterprise applications and infrastructure services.

## 15. Conclusion

The Summit IT Helpdesk AI Assistant demonstrates how AI agents and workflow automation can be applied to improve IT service delivery.

By combining n8n, OpenAI, Google Sheets, Airtable and conversational memory, the solution provides an integrated approach to first-line IT support, knowledge retrieval and incident management.

The project demonstrates the practical application of AI in automating repetitive support activities while maintaining defined security boundaries and escalation procedures.

---

**Project:** Summit IT Helpdesk AI Assistant  
**Organisation:** Summit Business Solutions Ltd. (Fictional)  
**Automation Platform:** n8n Cloud  
**AI Model:** OpenAI GPT-4.1 mini  
**Knowledge Repository:** Google Sheets  
**Incident Management:** Airtable  
**Project Type:** AI Agent and Business Process Automation  
**Status:** Working demonstration with successful Airtable incident creation.
