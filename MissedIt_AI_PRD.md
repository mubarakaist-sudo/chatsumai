# Product Requirements Document (PRD)

## MissedIt AI --- "What Did I Miss?"

**Version:** 1.0\
**Project type:** Individual hackathon MVP\
**Target build time:** A few hours\
**Primary requirement:** Local-first processing and privacy

## 1. Product Overview

MissedIt AI helps users quickly understand long or unread chat
conversations. It extracts key information, decisions, tasks, personal
mentions, unanswered questions, and deadlines, then presents them in a
prioritized dashboard.

The app will be deployed publicly for hackathon evaluation, with source
code pushed to GitHub. Deployment must host the application only;
conversation analysis must happen on the user's device.

## 2. Problem Statement

Users may return to hundreds of unread messages and lack time to read
everything. Important decisions, tasks, mentions, and deadlines can be
missed.

MissedIt AI turns a pasted conversation into a short briefing and
actionable checklist.

## 3. Goals

-   Summarize a conversation in a concise, readable format.
-   Identify important decisions and action items.
-   Highlight personal mentions, deadlines, and likely urgent messages.
-   Rank findings by urgency and relevance.
-   Show the original message as evidence for every extracted finding.
-   Keep conversation content and generated results on the user's
    device.
-   Provide a polished, responsive demo that can be deployed as a static
    website.

## 4. Non-Goals for the MVP

-   Direct integration with WhatsApp, Telegram, Slack, Discord, or
    email.
-   User accounts, authentication, collaboration, or a backend database.
-   Cloud AI APIs or remote processing of conversation text.
-   Notifications, scheduled background checks, or automatic message
    syncing.
-   Guaranteed understanding of every chat format or language.
-   Advanced local LLM integration unless the core MVP is complete and
    tested.

## 5. Target User

A student, project teammate, or busy group-chat member who needs to
catch up on a long conversation quickly.

## 6. Core User Flow

1.  User opens the web app.
2.  User optionally enters their name to help detect personal
    assignments and mentions.
3.  User pastes a conversation or loads a sample conversation.
4.  User clicks **Analyze Conversation**.
5.  The app analyzes the text locally in the browser.
6.  The app displays a summary and prioritized findings.
7.  User reviews each finding alongside its source message.
8.  User optionally marks action items as complete.
9.  User clicks **Clear Conversation** to remove the current input and
    results from app memory.

## 7. Functional Requirements

### 7.1 Conversation Input

-   Provide a large text area for pasted chat text.
-   Include a sample conversation button for quick evaluation.
-   Include an optional user-name field.
-   Support common exported chat formats with timestamps and sender
    names where practical.
-   Accept plain text when a recognizable export format is not detected.
-   Show helpful validation for empty input.

### 7.2 Local Analysis

-   Implement analysis using browser-side TypeScript.
-   Start with transparent, deterministic rule-based extraction.
-   Detect likely:
    -   Deadlines, dates, and times.
    -   Personal names and @mentions.
    -   Requests, assignments, and action items.
    -   Decisions and agreements.
    -   Questions and requests that may be unanswered.
    -   Urgency terms such as "urgent", "today", "ASAP", and "deadline".
-   Rank findings using urgency and relevance signals.
-   Avoid duplicate findings where possible.
-   Distinguish a planned action from a completed action.
-   Do not invent facts or infer an exact deadline unless the source
    supports it.
-   Mark ambiguous findings as **Needs review**.
-   If the app cannot confidently extract a category, show a useful
    empty state rather than fabricated results.

### 7.3 Results Dashboard

Show: - **Conversation Summary:** a concise overview generated from
locally extracted information. Do not claim free-form LLM summarization
unless a real local model is integrated. - **Urgent:** time-sensitive
findings. - **Assigned to You:** likely tasks or mentions related to the
user's name. - **Decisions:** explicit agreements or decisions. -
**Questions to Follow Up:** questions or requests that appear
unresolved, clearly labeled as possible follow-ups rather than confirmed
missed items. - **Action Checklist:** extracted tasks that users can
mark complete during the current session. - **Source Evidence:** the
original message text associated with each finding.

Provide clear priority labels such as High, Medium, and Low. Explain
that priorities are estimates.

### 7.4 Sample Data

Include a sample conversation containing: - A project deadline. - A task
assigned to the user. - A team decision. - A question about whether a
report was uploaded. - A casual, non-actionable message.

The sample should demonstrate that the app distinguishes useful
information from casual chat.

### 7.5 Privacy Controls

-   No backend or database.
-   No cloud AI API.
-   Do not send conversation text to any network endpoint.
-   Do not save conversation text or results to localStorage,
    sessionStorage, cookies, or IndexedDB.
-   Keep user-entered text and analysis results in in-memory application
    state only.
-   Clear the input, results, and related in-memory state when **Clear
    Conversation** is clicked.
-   Do not add analytics, tracking scripts, or third-party services that
    receive conversation data.
-   The UI may state **"Conversation analysis runs in your browser"**
    only if this is true in the implementation.
-   Do not claim that a local AI model is used unless a local model is
    integrated and verified.

### 7.6 Deployment and GitHub

-   Use a static frontend deployment compatible with React and Vite.
-   The deployed site must not require a backend for core functionality.
-   Push source code to a GitHub repository.
-   Include a README with setup, local run, build, deployment, and
    privacy details.
-   Never commit secrets, API keys, or real private conversations.
-   Verify the deployed version behaves the same as the local version.
-   Test browser network activity to confirm that conversation text is
    not transmitted.

## 8. Suggested Technology

-   React
-   TypeScript
-   Vite
-   Tailwind CSS (if available and quick to configure)
-   Browser-side utility functions for parsing and extraction
-   Git and GitHub
-   Static hosting such as GitHub Pages or Vercel

Avoid unnecessary backend technologies for this MVP.

## 9. Design Requirements

-   Premium, minimal, dark-mode dashboard.
-   Responsive on desktop and mobile.
-   Clear visual hierarchy and readable typography.
-   Restrained accent colors for urgency and status.
-   Simple navigation and obvious primary action.
-   Distinct cards or sections for summary, urgent items, tasks,
    decisions, and follow-ups.
-   Show evidence/source messages clearly.
-   Include loading, empty, error, and results states.
-   Make the local-processing privacy indicator visible but not
    distracting.
-   Avoid excessive animations and decorative elements that delay
    implementation.

## 10. Acceptance Criteria

The MVP is ready when: 1. The app runs locally without a backend. 2. A
user can paste a conversation and analyze it. 3. The sample conversation
produces useful findings. 4. The app detects at least one deadline, one
likely assignment, and one decision in the sample. 5. Each finding
displays source evidence. 6. Casual messages are not incorrectly
presented as confirmed tasks. 7. Empty or malformed input is handled
gracefully. 8. The user can mark checklist items complete and clear the
session. 9. The app does not send conversation text to any external
service. 10. The deployed app works and the source code is pushed to
GitHub. 11. The README accurately describes functionality and privacy
limitations.

## 11. Implementation Priorities

### P0 --- Must Have

-   Working responsive interface.
-   Paste conversation and sample data.
-   Browser-side rule-based analysis.
-   Summary/overview and prioritized categories.
-   Source evidence for findings.
-   Clear/reset and in-session checklist.
-   No external transmission or persistent storage of conversations.
-   GitHub repository and deployed demo.

### P1 --- If Time Allows

-   Better handling of multiple chat-export formats.
-   Filters and category counts.
-   Downloadable results generated locally.
-   A small browser-based language model, only if it can be integrated
    and verified without sending conversation data off-device.

### P2 --- Later

-   Direct messaging platform integrations.
-   Offline model caching and fully offline operation.
-   More languages and advanced semantic analysis.

## 12. Risks and Mitigations

-   **Rule-based analysis may miss context:** show source evidence and
    "Needs review" labels.
-   **Chat formats vary:** support common formats and provide a
    plain-text fallback.
-   **Privacy claims may be inaccurate:** inspect network requests and
    remove any external processing.
-   **Scope may exceed hackathon time:** complete P0 before attempting
    local LLM integration.
-   **Deployment may differ from local development:** test the deployed
    URL with the sample conversation.

## 13. Final Product Principle

The product should help users answer three questions quickly:

1.  What happened?
2.  What matters to me?
3.  What should I do next?

Accuracy, traceable evidence, privacy, and a reliable demo are more
important than adding many features.
