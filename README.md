# rec.sleep.repeat. n8n Agency Brain

This repository contains the files and configuration needed to run the Telegram-to-PDF "Agency Brain" via n8n.

## How it Works

1. You send a message via Telegram to your bot (e.g. "Write a content strategy for...").
2. The **n8n AI Agent** (powered by Gemini) drafts the content using the `rec.sleep.repeat.` brand voice.
3. n8n fetches the HTML template and Design System CSS from this repository.
4. n8n injects the content, logo, and CSS into the template.
5. The assembled HTML is sent to **CloudConvert** to generate a perfectly formatted A4 PDF.
6. The PDF is sent right back to you in Telegram.

## Setup Instructions

### 1. Import the Workflow
- Open your n8n instance.
- Create a new workflow.
- Click the `...` (options) menu in the top right -> `Import from file`.
- Select `workflow.json` from this repository.

### 2. Configure Credentials
You will need to add credentials for the following nodes:
- **Telegram Trigger & Telegram Node:** Add your Telegram Bot Token (get this from `@BotFather` on Telegram).
- **Google Gemini Node:** Add your Google API key.
- **CloudConvert Node:** Add your CloudConvert API key (sign up for free at cloudconvert.com).

### 3. File Paths Configuration
The "Read File" nodes in the workflow expect the files to be accessible by n8n. 
- If n8n has a local sync to this git repo, ensure the paths in the "Read File" nodes are absolute paths on your IONOS server (e.g., `/data/git/n8n-agency-brain/document_template.html`).
- If you prefer, you can switch the "Read File" nodes to "HTTP Request" nodes and fetch the raw files directly from your GitHub repository URL instead.

## Editing the Template
If you want to change how the generated PDF looks:
1. Open `document_template.html`.
2. Edit the HTML structure. Note the placeholders: `{{CSS_CONTENT}}`, `{{LOGO_SVG_CONTENT}}`, `{{HERO_CONTENT}}`, `{{BODY_CONTENT}}`.
3. The styling comes directly from `colors_and_type.css`.
