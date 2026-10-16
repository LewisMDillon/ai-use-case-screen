# AI use case screen

A one-page screening tool for deciding whether an AI use case should go ahead, and on what terms. Fifteen questions across three lenses produce a traffic-light verdict, a list of fixes, a set of human-in-the-loop rules and a row for your AI register. It is built for small and mid-sized organisations that need a defensible decision in twenty minutes without a lawyer in the room.

Live tool: https://ai-use-case-screen-8f278ad22982.herokuapp.com/

Built by Lewis Dillon for week 7 of Code Institute's AI for Business Transformation programme, where participants used it to screen their own planned deployments. Published with permission.

## What it does

You describe a use case in two sentences and answer fifteen questions. Each answer is green, amber or red, and the wording for each colour is on the card, so you match the wording rather than your instinct. The tool then works out the rest:

- A verdict for each lens and an overall verdict. Any red stops the project until it is fixed.
- The fix for every amber, drawn from a list of nine, each marked as needed or done with a name and date.
- A one-page risk note when the card shows three or more ambers, or a red is going to a specialist. Five questions in plain sentences.
- Four human-in-the-loop lines that say how the use case will run and who owns it: what the AI does alone, what a person checks, what a person decides, and who it escalates to.
- A review date, three months from the date screened by default.
- An export: one row for your AI register as CSV, a copy-to-clipboard version for pasting into a spreadsheet, and a print layout for saving as PDF.

Your answers are saved in the browser until you clear them. Nothing leaves your machine.

## The three lenses

**1. Data protection** (UK GDPR, and EU GDPR if you serve EU customers). Does personal data go in? Is any of it sensitive? Where does it go? Does it decide, or help decide, something about a person? Would they be surprised?

**2. AI risk flags** (the EU AI Act supplies the vocabulary; UK rules point the same way). Does it do a banned thing? Is it in a listed high-risk area? Does it talk to customers or the public? Does it generate realistic content? Does it reach people in the EU?

**3. AI cybersecurity** (least privilege). Can it act, or only advise? What can it reach? Does it read anything you did not write? Who approves before it acts? Can you see what it did?

The third lens treats an assistant that can act as a new employee with your logins, and gives it the access a new starter would get. The question about reading content you did not write is there because prompt injection is the attack most likely to hit a small organisation, and the defence is less reach and a person to ask, not a smarter model.

## The verdicts

| Verdict | Meaning | What it costs you |
|---|---|---|
| Green | Go. Log it in the AI register. | Two minutes. |
| Amber | One named check, done once. Then go. | An hour, a few business seats, or one line in a privacy notice. |
| Red | Stop. Get specialist help before this goes further. | A conversation with someone who does this for a living. |

Three or more ambers across the card means a written risk note before you start. The tool prompts for it and will not mark the screen complete without it.

## The nine fixes

Every amber on the card names its fix, so the to-do list writes itself.

| Fix | Triggered by amber on |
|---|---|
| Business account with a DPA | 1.1, 1.3 |
| Screen before you paste | 1.2 |
| One line in the privacy notice | 1.5 |
| Person decides, and can be asked | 1.4, 2.2 |
| Label it | 2.3, 2.4, 2.5 |
| Least privilege | 3.1, 3.2 |
| Person reviews, person sends | 3.3, 3.4 |
| Named owner, MFA, logs | 3.5 |
| Log it in the AI register | Every green or amber |

## Using it

1. Describe the use case: name, two or three sentences a stranger could follow, owner, tool and account type.
2. Answer the fifteen questions. Pick the wording that fits best. If two fit, take the worse one. Add a note where a fact decided the colour.
3. Write the four human-in-the-loop lines as you would brief a new starter.
4. Mark each triggered fix as needed or done, with a name and date. Write the risk note if the card asks for one.
5. Set the date screened, sign off, and export the register row.

Re-run the screen if the tool, the data or the reach changes.

A worked example (a sales quote assistant that reads a shared inbox and drafts replies into a review queue) is built in. Load it to see a completed card: six ambers, a risk note, and a verdict of amber with fixes.

## Using it with an AI assistant

The screen was designed so an assistant can run it and a person can check it. Paste the card's question wording and your two-sentence use case into an assistant and ask it to pick a colour for each question, quote the wording it matched, say which fact decided it, and say where it lacks a fact rather than guess. Then compare its fifteen colours with yours. Every disagreement is either a fact it did not have or a judgement you should be able to defend. Never let it pick the colour where it said it lacked a fact. Save the exchange with the register row as your reasoning.

## Running it

It is a single HTML file with no build step and no backend.

Open `index.html` in a browser, or serve the folder:

```
npm install
npx serve -l 3000
```

The repository includes a `package.json` and `serve.json` so it deploys to Heroku or any Node host as a static site with `npm start`.

## Design notes

- Rule-driven. The question set, colour wording, fix mapping and risk note prompts are defined as data at the top of the script, so the card can be revised without touching the rendering logic.
- Worst-case default. Where two colours fit, the instructions say take the worse one, and the verdict logic treats any red as a stop regardless of the other fourteen answers.
- Evidence by default. The export carries the verdicts, the four human-in-the-loop lines, the fix status and the review date, so the register row is a record of the decision and not just the result.
- Local only. State lives in the browser's localStorage. There is no account, no server and no telemetry.

## Scope

This is a screening aid to help you decide where to look harder. It is not legal advice, and a green verdict does not mean a use case is lawful; it means none of the fifteen questions found a reason to stop. If personal data leaks and people could be harmed, the ICO must hear within 72 hours. Know today who makes that call.

## Licence and attribution

Copyright 2026 Code Institute. Author: Lewis Dillon. Published as a portfolio copy with the permission of Code Institute. See `LICENSE` for terms.

The three-lens structure draws on UK GDPR and the ICO's guidance for small organisations, the EU AI Act's prohibited and high-risk categories and transparency obligations, and the OWASP Top 10 for LLM and Agentic Applications for the cybersecurity lens.
