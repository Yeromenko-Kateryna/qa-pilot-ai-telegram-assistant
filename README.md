# QA Pilot AI — Telegram QA Assistant with n8n and Gemini

QA Pilot AI is an AI-powered Telegram assistant designed to support daily QA tasks for a Junior QA / QA Automation Engineer.

The bot helps generate compact test cases, draft bug reports, create QA checklists, analyze ambiguous requirements, suggest test data, and provide basic automation hints.

## Tech Stack

- n8n
- Telegram Bot API
- Google Gemini Chat Model
- n8n AI Agent
- Simple Memory
- Prompt Engineering

## Workflow

The automation workflow is built in n8n:

```text
Telegram Trigger → AI Agent → Send a text message
                 ├ Google Gemini Chat Model
                 └ Simple Memory
```

## Features

- Generates positive, negative, and edge test cases
- Drafts structured bug reports
- Creates compact QA checklists
- Analyzes requirements for ambiguity
- Suggests test data and edge cases
- Provides basic Playwright automation hints
- Maintains short conversation context with Simple Memory
- Uses response length control to avoid Telegram message delivery errors

## Example Use Cases

### Test Case Generation

User request:

```text
Generate exactly 6 login form test cases.
```

Bot response includes:

- Scope
- Assumptions
- Positive test cases
- Negative test cases
- Edge cases
- Test data
- Risks and clarifying questions

### Bug Report Drafting

User request:

```text
Create a short bug report for: Login button does not work after valid credentials.
```

Bot response includes:

- Title
- Environment
- Preconditions
- Steps to reproduce
- Actual result
- Expected result
- Severity
- Priority
- Attachments / logs

### QA Checklist Creation

User request:

```text
Create a compact QA checklist for an online shopping cart.
```

Bot response includes a compact checklist for:

- Item management
- Calculations and pricing logic
- Persistence and session state
- UI and navigation
- Basic automation hints

### Requirement Analysis

User request:

```text
Analyze this requirement for ambiguity: "User should be able to quickly register on the website."
```

Bot response identifies ambiguous terms, asks clarifying questions, and suggests a more testable requirement.

## Screenshots

### n8n Workflow

![n8n workflow](docs/workflow-screenshot.png)

### Start / Bot Capabilities

![start demo](docs/telegram-demo-start.png)

### Test Case Generation Demo

![test cases demo](docs/telegram-demo-test-cases.png)

### Bug Report Demo

![bug report demo](docs/telegram-demo-bug-report.png)

### QA Checklist Demo

![checklist demo](docs/telegram-demo-checklist.png)

### Requirement Analysis Demo

![requirement analysis demo](docs/telegram-demo-requirement-analysis.png)

## QA Improvements Implemented

During testing, the bot initially generated long responses that exceeded Telegram message delivery limits.

To improve reliability, response length rules were added to the system prompt and output-length control was applied before sending messages back to Telegram.

This helped prevent message delivery failures and made the bot responses more suitable for Telegram.

## Security Notes

API keys, Telegram bot tokens, and n8n credentials are not included in this repository.

## What I Learned

- How to build an AI-powered Telegram workflow in n8n
- How to connect Telegram Trigger, AI Agent, Gemini Chat Model, Simple Memory, and Telegram Send Message
- How to design a QA-focused system prompt
- How to test AI assistant behavior with QA scenarios
- How to identify and fix output-length issues in Telegram integrations