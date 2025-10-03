
# 🤖 AI-Powered Google Docs Generator via Telegram

This n8n workflow allows users to generate new Google Docs essays by sending a message via Telegram. It uses an AI agent to read existing documents and create a new one based on the input, then moves the document to a specified folder and sends a link back via Telegram.

## 🔧 Workflow Overview

The workflow performs the following steps:

1. **Telegram Trigger**: Listens for incoming messages from a specific Telegram chat.
2. **AI Agent Processing**:
   - Reads multiple predefined Google Docs as reference material.
   - Uses Cohere AI to generate a new essay based on the Telegram message content.
3. **Google Docs Creation**: Creates a new Google Doc with the title based on the Telegram message.
4. **Google Docs Update**: Inserts the AI-generated content into the newly created document.
5. **Google Drive File Move**: Moves the created document to a specific folder in Google Drive.
6. **Telegram Response**: Sends a link to the newly created document back to the user.

## 📦 Nodes Used

- `n8n-nodes-base.telegramTrigger`: Triggers the workflow on new Telegram messages.
- `@n8n/n8n-nodes-langchain.agent`: AI agent that processes the input and generates content.
- `@n8n/n8n-nodes-langchain.lmChatCohere`: Cohere language model used by the AI agent.
- `n8n-nodes-base.googleDocsTool`: Retrieves content from existing Google Docs for AI reference.
- `n8n-nodes-base.googleDocs`: Creates and updates the new Google Doc.
- `n8n-nodes-base.googleDrive`: Moves the created document to a specific folder.

## ⚙️ Setup Instructions

1. **Import Workflow**: Import this JSON into your n8n instance.
2. **Credentials**:
   - Set up Telegram credentials (`Telegram account 3`) and add your bot token.
   - Set up Google Docs credentials (`Google Docs account 2`) with OAuth access.
   - Set up Google Drive credentials (`Google Drive account 2`) with OAuth access.
   - Set up Cohere API credentials (`CohereApi account`) with your API key.
3. **Configure Nodes**:
   - Replace `"YOUR CHAT ID"` in the **Send a text message** node with your actual Telegram chat ID.
   - Update the folder ID in the **Move file** node (currently set to `=123`) with the correct Google Drive folder URL or ID.
   - Ensure all `googleDocsTool` nodes point to valid Google Docs (currently using placeholder ID `12345678`).
4. **Activate Webhook**: Activate the workflow and use the generated webhook URL for Telegram integration.

## 🧠 AI Behavior

The AI agent is prompted to:
> "Read all the docs documents and write a new docs essay about [Telegram message] using the same style of language — don't just repeat topics."

You can customize this prompt in the **AI** node for different behavior.

## 📁 Folder IDs

To find your Google Drive folder ID:
- Open the folder in Google Drive.
- The URL will contain the folder ID: `https://drive.google.com/drive/folders/FOLDER_ID`

## 📝 Notes

- All Google Docs used as references must be shared with the Google Docs account used in the workflow.
- The AI-generated document will be created in the default Google Docs folder unless moved.
- Make sure your Cohere API plan supports the operations used in this workflow.

## 🛠 Example Use Case

Send a message like:
> "The future of renewable energy"

And receive back a newly generated Google Doc essay on that topic, created using the style and context of your reference documents.
