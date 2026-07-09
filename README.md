# QA Pilot AI — Telegram QA Assistant with n8n and Gemini

![Project Status](https://img.shields.io/badge/status-MVP%20completed-brightgreen)
![Built with n8n](https://img.shields.io/badge/built%20with-n8n-orange)
![Telegram Bot](https://img.shields.io/badge/integration-Telegram%20Bot-blue)
![AI Model](https://img.shields.io/badge/AI-Google%20Gemini-purple)
![QA Portfolio](https://img.shields.io/badge/portfolio-QA%20Automation-success)

QA Pilot AI is an AI-powered Telegram assistant designed to support daily QA tasks for a Junior QA / QA Automation Engineer.

The bot helps generate compact test cases, draft structured bug reports, create QA checklists, analyze ambiguous requirements, suggest test data, and provide basic automation hints.

This project was built as a portfolio project to demonstrate practical no-code/low-code automation, AI assistant configuration, QA prompt design, Telegram integration, and integration testing.

---

## Table of Contents

- [Project Overview](#project-overview)
- [Tech Stack](#tech-stack)
- [Workflow](#workflow)
- [Features](#features)
- [Example Use Cases](#example-use-cases)
- [Screenshots](#screenshots)
- [Prompt Design](#prompt-design)
- [Test Scenarios](#test-scenarios)
- [QA Improvements Implemented](#qa-improvements-implemented)
- [Known Limitations](#known-limitations)
- [Security Notes](#security-notes)
- [What I Learned](#what-i-learned)
- [Project Status](#project-status)

---

## Project Overview

| Area | Description |
|---|---|
| Project type | AI-powered Telegram QA assistant |
| Main goal | Support practical QA tasks through a Telegram bot |
| Automation tool | n8n |
| AI model | Google Gemini Chat Model |
| Target user | Junior QA / QA Automation Engineer |
| Portfolio focus | QA thinking, prompt design, integration testing, documentation |

---

## Tech Stack

- **n8n** — workflow automation
- **Telegram Bot API** — user interaction channel
- **Google Gemini Chat Model** — AI response generation
- **n8n AI Agent** — assistant logic and prompt execution
- **Prompt Engineering** — QA-focused behavior configuration
- **QA Test Design** — test cases, checklists, bug reports
- **Integration Testing** — Telegram + n8n + AI model behavior validation

---

## Workflow

The automation workflow is built in n8n.

```text
Telegram Trigger → AI Agent → Send a text message
                 └ Google Gemini Chat Model
```

### Workflow Logic

1. A user sends a message to the Telegram bot.
2. Telegram Trigger receives the incoming message.
3. AI Agent processes the message using the configured system prompt.
4. Google Gemini Chat Model generates the response.
5. Send a text message returns the answer back to the same Telegram chat.

### Credential Handling

API keys, bot tokens, and n8n credentials are stored inside n8n credentials and are not included in this repository.

---

## Features

| Feature | Description |
|---|---|
| Test case generation | Generates positive, negative, and edge test cases |
| Bug report drafting | Creates structured bug reports with standard QA fields |
| QA checklist creation | Produces compact checklists for feature testing |
| Requirement analysis | Identifies ambiguity and missing acceptance criteria |
| Test data suggestions | Suggests useful valid, invalid, and edge test data |
| Automation hints | Provides basic Playwright / TypeScript automation ideas |
| Telegram response control | Uses length limits to reduce message delivery issues |
| Integration findings | Documents external API and platform limitations |

---

## Example Use Cases

### 1. Test Case Generation

**User request:**

```text
Generate exactly 6 login form test cases.
```

**Bot response includes:**

- Scope
- Assumptions
- Positive test cases
- Negative test cases
- Edge cases
- Test data
- Risks and clarifying questions

---

### 2. Bug Report Drafting

**User request:**

```text
Create a short bug report for:
Login button does not work after valid credentials.
```

**Bot response includes:**

- Title
- Environment
- Preconditions
- Steps to reproduce
- Actual result
- Expected result
- Severity
- Priority
- Attachments / logs

---

### 3. QA Checklist Creation

**User request:**

```text
Create a compact QA checklist for an online shopping cart.
```

**Bot response includes checklist areas such as:**

- Adding items
- Removing items
- Updating quantity
- Price and total calculations
- Cart persistence
- Checkout flow
- Empty cart state
- Stock limitation handling

---

### 4. Requirement Analysis

**User request:**

```text
Analyze this requirement for ambiguity:
"User should be able to quickly register on the website."
```

**Expected bot response identifies:**

- Ambiguous wording
- Missing measurable criteria
- Clarifying questions
- A more testable requirement

---

## Screenshots

### n8n Workflow

![n8n workflow](docs/workflow-screenshot.png)

---

### Start / Bot Capabilities

![start demo](docs/telegram-demo-start.png)

---

### Test Case Generation Demo

![test cases demo](docs/telegram-demo-test-cases.png)

---

### Bug Report Demo

![bug report demo](docs/telegram-demo-bug-report.png)

---

### QA Checklist Demo

![checklist demo](docs/telegram-demo-checklist.png)

---

## Prompt Design

The assistant behavior is controlled through a system prompt stored in:

```text
prompts/system-message.md
```

The system prompt defines:

- QA assistant role
- Supported QA tasks
- Response length limits
- Test case structure
- Bug report structure
- Checklist format
- Requirement analysis format
- Rules for avoiding invented project-specific facts

### Main Prompt Goals

| Goal | Implementation |
|---|---|
| Keep responses Telegram-friendly | Maximum response length rules |
| Support QA tasks | Dedicated formats for test cases, checklists, and bug reports |
| Reduce hallucinations | Rule to avoid invented project-specific facts |
| Improve usability | Short, structured, practical answers |
| Support portfolio value | QA-focused examples and documentation |

---

## Test Scenarios

Manual test scenarios for validating the bot are stored in:

```text
test-scenarios/qa-bot-test-scenarios.md
```

### Covered Scenarios

- Bot start message
- Test case generation
- Bug report drafting
- QA checklist creation
- Requirement analysis
- Response length control
- External API limitation handling

---

## QA Improvements Implemented

During testing, the bot initially generated long responses that could exceed Telegram message delivery limits.

To improve reliability, response length rules were added to:

- the system prompt;
- the n8n output expression before sending Telegram messages.

This helped make bot responses more suitable for Telegram and reduced the risk of message delivery failures.

### Improvement Summary

| Problem Found | Improvement |
|---|---|
| AI responses were too long | Added response length rules |
| Telegram delivery could fail | Added output-length control |
| Bot could invent missing details | Added prompt rules for assumptions and clarification |
| External API could be unstable | Documented API quota and availability limitations |

---

## Known Limitations

During testing, the workflow exposed several external integration limitations:

- Gemini API returned `429 Too Many Requests` when the free-tier quota was exceeded.
- Gemini API returned temporary `503 Service Unavailable` during high demand.
- Long AI responses could exceed Telegram message delivery limits.

These are external API and platform limitations. The Telegram trigger and n8n message routing were configured successfully.

### Possible Future Reliability Improvements

- Add fallback response path when the AI model is unavailable.
- Add retry logic for temporary API failures.
- Add persistent memory after session handling is configured correctly.
- Export and document the n8n workflow JSON.
- Add more advanced Playwright-specific QA automation prompts.

---

## Security Notes

Sensitive credentials are not included in this repository.

The following values must be stored only in n8n credentials or secure environment settings:

- Telegram bot token
- Google Gemini API key
- OpenAI API key, if used
- n8n credentials

If a token is accidentally exposed, it should be revoked and regenerated immediately.

---

## What I Learned

- How to build an AI-powered Telegram workflow in n8n
- How to connect Telegram Trigger, AI Agent, Gemini Chat Model, and Telegram Send Message
- How to design a QA-focused system prompt
- How to test AI assistant behavior with QA scenarios
- How to identify and document integration issues
- How to handle response length constraints in Telegram integrations
- How external API quotas and service availability can affect automation reliability
- How to prepare a small automation project for GitHub portfolio presentation

---

## Project Status

**MVP completed.**

The project demonstrates a tested Telegram QA assistant workflow, QA-focused prompt design, documented test scenarios, screenshots, and integration findings.

### Current State

| Area | Status |
|---|---|
| Telegram bot created | Completed |
| n8n workflow configured | Completed |
| AI Agent configured | Completed |
| Gemini model connected | Completed |
| QA system prompt created | Completed |
| Demo screenshots added | Completed |
| Test scenarios documented | Completed |
| External limitations documented | Completed |

### Future Improvements

- Add fallback response path when the AI model is unavailable.
- Add retry logic for temporary API failures.
- Add persistent memory after session handling is configured correctly.
- Export and document the n8n workflow JSON.
- Add more advanced Playwright-specific QA automation prompts.