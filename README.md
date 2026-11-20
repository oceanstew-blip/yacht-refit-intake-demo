# Yacht Refit Intake (n8n demo)

A small n8n workflow that turns a yacht refit inquiry into a clear project summary, a next-step checklist, and a draft status update for a person to review.

**This is a fictional demonstration, not a product, a production system, or a quote engine.** Every vessel, person, company, email address, phone number, location and date in it is made up.

## The business problem

Refit inquiries arrive as long emails, voicemails and forwarded messages. Each one describes different work, in a different order, with different details left out. Before anyone can have a useful conversation, someone has to read it, work out what is being asked, notice what is missing, and write it up so the project lead can see it at a glance. That first pass is slow, and it is where details get lost.

## What the workflow does

1. **Starts from a made-up request.** Four fictional requests are built into the first node.
2. **Tidies the fields** and checks what is needed to understand the request: contact name, a way to reach them, vessel name and length, where the vessel is, a description of the work, and a preferred time window. It lists exactly what is missing.
3. **Categorizes with plain rules.** Keyword lists sort the request into broad project types (interior and joinery, exterior and finish, mechanical and systems, electronics and navigation) and flag it as time-sensitive when the client says it is. A request can match several types. The output shows which words matched.
4. **Builds a project summary and a next-step checklist.** The summary is a headline plus the client's own words. The checklist is a short list of intake steps, each with an owner role.
5. **Drafts a status update** from a template. A complete request gets an acknowledgment that restates what was understood. An incomplete one gets a short note asking for exactly the missing items. If there is no way to reach the client, it drafts nothing and says so.
6. **Stops at a human review gate.** Every record ends as `PENDING_HUMAN_REVIEW` with `message_sent: false`.

**What it deliberately does not do:** estimate cost, approve work, select vendors, promise timelines, or send anything. Every record lists these as `not_done_by_this_workflow`. Every draft says it is an acknowledgment only, not a quote, a schedule or an approval.

The last node, **Review queue**, shows one record per request in reading order: summary line, intake, checks, categorization, project summary, next steps, draft status update, approval.

## Setup and import

You need n8n (cloud or self-hosted). No credentials, accounts or external services are required.

1. In n8n, create a new workflow.
2. Open the workflow menu (three dots, top right) and choose **Import from file**.
3. Select [`workflow/yacht-refit-intake-demo.json`](workflow/yacht-refit-intake-demo.json).

## Sample run

1. Click **Execute workflow**. The trigger is manual.
2. Open the last node, **Review queue (read this output)**, and switch to **Table** or **JSON** view.
3. You should see four records:

| Request | Vessel | What to notice |
|---|---|---|
| YR-3001 | M/Y Sample Tide | Interior and joinery. Planned. Complete. |
| YR-3002 | S/Y Demo Breeze | Exterior and mechanical. **Time-sensitive**, because the client named a deadline and said "urgent." The checklist asks the project lead to look at it. It does not promise anything. |
| YR-3003 | M/Y Placeholder Star | **Incomplete.** Missing vessel length, location and time window. The draft asks for exactly those. |
| YR-3004 | M/Y Imaginary Wake | Electronics and navigation. Planned. |

To try your own made-up request, edit the list in the first node. The same records are in [`sample-data/fictional-refit-requests.json`](sample-data/fictional-refit-requests.json). Use made-up details only.

## Rules, not AI

The categorization is a keyword list in one Code node. It is deterministic: the same input always gives the same result, and every rule is readable. This project does not call that "AI."

Keyword rules are also blunt. A request that mentions the "upper deck" of a vessel would match the exterior rule even if the work is an audio upgrade. That is one reason a person reads every record before anything happens.

**Where AI could assist later.**
- Reading a long, messy email or voicemail transcript and pulling out the vessel, the location and the work described, into the same fields step 2 uses.
- Suggesting project types from the meaning of the request instead of single words.
- Writing a first draft of the status update in the company's tone.

Each of those would feed the same review gate.

**Where human judgment stays necessary.** Scope, cost, vendors, schedule and whether to take the project at all are decisions for the project lead. So is reading the client's tone, and deciding whether a stated deadline is realistic. This workflow organizes information. It does not make those decisions.

## Privacy boundaries

- Fictional vessels, people, companies, emails (`example.com`), phone numbers (the reserved `555-01xx` range), locations and dates only.
- No real client or vessel information, credentials, API keys, private URLs or account names.
- No pricing logic, cost estimates, vendor recommendations or real project-management methods.
- Built-in n8n nodes only. No external services. No records are created anywhere and no messages are sent.
- Works without any credentials.

## What is intentionally omitted

- Cost, schedule and vendor logic of any kind.
- Any send step, and connections to an inbox, form, CRM or project-management tool.
- Attachments such as drawings and photos.
- Duplicate detection, spam filtering and error handling.
- Real project phases or methods. The checklist here is generic intake housekeeping.

## License note

This repository has no open-source license and is published as a portfolio demonstration. Anyone can see it, but no permission to reuse it is granted by the absence of a license.

---

Built by Tami Stewart, [Tami Stewart Consults](https://tamistewartconsults.com).
