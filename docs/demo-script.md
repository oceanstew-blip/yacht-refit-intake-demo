# 60-second walkthrough

Use this when showing the demo to a client. Have the workflow open in n8n with the **Review queue** node visible.

**0:00 - The problem (10 sec)**
"A refit inquiry shows up as a long email or a voicemail. Before anyone can talk about the project, someone has to read it, figure out what's being asked, and notice what's missing. That first pass is where details get lost."

**0:10 - The flow (15 sec)**
Point to the canvas, left to right.
"Here's a made-up request. This step tidies it and checks what's missing. This step sorts it into broad project types using plain rules I can show you. Then it writes a summary, a short checklist, and a draft update."

**0:25 - Run it (10 sec)**
Click **Execute workflow**, then open **Review queue**.
"Four fictional requests, four records, each with a one-line summary on top."

**0:35 - Show two records (15 sec)**
Open the time-sensitive one: "The client said it's urgent and gave a deadline. The workflow flags that for the project lead. It doesn't promise anything."
Open the incomplete one: "This one never said how long the vessel is or where it is. It doesn't guess. The draft asks for exactly those two things."

**0:50 - What it won't do (10 sec)**
"It doesn't estimate cost, pick vendors, promise a timeline or send anything. Those stay with a person. The sorting is plain rules, not AI. If we add AI later to read messy emails, a person still reviews every record."

**Likely questions**
- *Can it read my inbox or form?* Yes, that would replace the first node. It is left out of this demo on purpose.
- *Can it add costs or schedule?* That is a project-lead decision and is deliberately outside this demo.
- *Whose data is this?* None. Everything is fictional.
