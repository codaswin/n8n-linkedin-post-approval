# LinkedIn Post Approval (n8n)

Week 4 · Day 2 assignment. An n8n workflow where AI drafts a LinkedIn post, a second AI reviews it, and nothing is saved until you approve it by email.

## Flow

1. **Topic Form** - form trigger with one required field, `Topic`.
2. **Writer Agent** - AI Agent + chat model drafts the post (hook, 120-150 words, one CTA, max 3 hashtags).
3. **Reviewer Agent** - separate AI Agent + chat model scores hook / clarity / CTA, rewrites the weakest part and returns the final post only.
4. **Email Post for Approval** - Gmail "Send message and wait for response" with Approve / Reject buttons (1 day limit). The run pauses here.
5. **Approved?** - IF node on `data.approved`.
6. **Save Approved Post** - Google Sheets "Append Row" with columns `Date | Topic | Final Post | Status`. Reject writes nothing.

## Import

1. In n8n: Workflows -> Import from File -> `LinkedIn_Post_Approval.json`.
2. Connect your own credentials: an OpenAI-compatible API (the models use Fireworks via a custom Base URL), Gmail OAuth2, Google Sheets OAuth2.
3. In **Email Post for Approval**, set your own email in `To`.
4. In **Save Approved Post**, pick your Google Sheet (headers: `Date`, `Topic`, `Final Post`, `Status`).
5. Click Test workflow, submit a topic, approve from the email.

No API keys or secrets are stored in this file.
