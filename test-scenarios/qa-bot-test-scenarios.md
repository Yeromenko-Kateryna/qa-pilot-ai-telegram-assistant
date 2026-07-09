# QA Pilot AI — Test Scenarios

## TC-01: Start command

### Input

```text
/start
```

### Expected Result

The bot introduces itself as a QA assistant and lists supported QA tasks:

- test case generation;
- bug report drafting;
- QA checklist creation;
- requirement analysis;
- test data suggestions;
- automation guidance.

---

## TC-02: Test case generation

### Input

```text
Generate exactly 6 login form test cases in one-line format.
```

### Expected Result

The bot returns a compact list of 6 test cases:

- 2 positive cases;
- 2 negative cases;
- 2 edge cases.

The response should also include short test data and avoid long explanations.

---

## TC-03: Bug report drafting

### Input

```text
Create a short bug report for: Login button does not work after valid credentials.
```

### Expected Result

The bot returns a structured bug report with:

- Title;
- Environment;
- Preconditions;
- Steps to reproduce;
- Actual result;
- Expected result;
- Severity;
- Priority;
- Attachments / logs.

---

## TC-04: QA checklist

### Input

```text
Create a compact QA checklist for an online shopping cart.
```

### Expected Result

The bot returns a compact checklist covering:

- item management;
- calculations and pricing logic;
- persistence and session state;
- UI and navigation;
- automation recommendations.

---

## TC-05: Requirement ambiguity analysis

### Input

```text
Analyze in 3 short bullets: quick registration.
```

### Expected Result

The bot identifies ambiguity in the requirement and provides a compact response with:

- ambiguous terms;
- clarifying questions;
- improved requirement suggestion.

---

## TC-06: Telegram response length handling

### Input

```text
Generate a detailed login test plan.
```

### Expected Result

If the AI response is too long, the workflow should shorten the message before sending it to Telegram.

Expected fallback text:

```text
Message shortened for Telegram. Ask for the extended version if needed.
```

---

## Notes

During testing, two integration issues were identified:

1. Long AI responses could exceed Telegram message delivery limits.
2. Gemini API could return a rate-limit/quota error when too many requests were sent too quickly.

The workflow was improved with response-length control, and the Gemini model can be changed without changing the overall architecture.