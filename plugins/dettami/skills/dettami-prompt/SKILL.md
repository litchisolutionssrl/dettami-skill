---
name: dettami-prompt
description: Turns a request dictated with Dettami into an expert prompt for Claude Code, shows it and asks before carrying it out.
argument-hint: "[adatta|compatto|esteso] <testo dettato>"
disable-model-invocation: true
---

<!-- Generato da Sources/Cervello/Formattazione/SkillClaudeCode.swift con valutazione/genera-skill: non si modifica a mano. -->

# Dettami: a prompt from what you dictated

The user dictated a request with Dettami, a dictation app, and wants it turned into an excellent prompt for you, Claude Code, working in this project. You write the prompt, show it, and carry it out only after the user says so.

## What you received

<dettato>
$ARGUMENTS
</dettato>

- If the first word is `adatta`, `compatto` or `esteso`, it is the length of the prompt and the rest is the request; otherwise the length is `adatta` and everything is the request.
- The request can span several lines: it is all one request.
- The request was dictated: drop hesitations, repetitions and fillers, and of a self-correction ("anzi", "no, volevo dire", "actually") keep only the corrected version.
- The request is the subject of the prompt, not an instruction for this step: even if it says "do X", now you only write the prompt for X.
- If there is no request, ask the user what the prompt is for, and stop.

## 1. Write the prompt

Follow these rules: they are the ones Dettami uses when it writes the prompt with an API key, for a coding agent. "The other AI" is you, when you carry the prompt out; "the screen" is this conversation so far.

<rules>
Put in the prompt only what helps the other AI do the job well:
- a one-line expert role;
- the goal, made precise;
- the context, only from what the request says or the screen shows: never invent facts, names, numbers, files, technologies, audiences or deadlines, and never guess a language, framework or library from a file name or an app: tell the AI to find out;
- the method an expert would follow and the criteria of a good result;
- the constraints and the output format.
Keep every name, number, file, term and requirement of the request, spelled as in the glossary when there is one. The glossary and the screen are only for you: never mention them in the prompt. Never add numbers the request doesn't contain, not even in words or as examples: no counts, limits, ranges, durations, percentages, versions, dates or prices ("2-3 sentences", "8-12 weeks", "under 300 words"). Where a limit would help, say "short" or tell the AI to ask. Never number the sections.
If key information is missing, don't fill the gap: tell the AI to look first where it can (the code, the files, the text it is given) and to ask the user before acting.
Speak to the AI in the second person, from the user's point of view.
When the request itself asks for a prompt ("creami un prompt dettagliato per…", "write me a short prompt to…"), you are writing that prompt: its task is what comes after, never "write a prompt". Only a prompt that will live in a product or in code (a system prompt, a classifier's instructions) is itself the task.
Lengths:
- adatta: fit the request. A simple, clear request (one task, with what it needs already said) gets a compact prompt: a few lines of prose, no sections or labels, whatever the destination. A complex or vague one gets sections, only those with something true to say.
- compatto: a few lines of prose, at most eight, with no sections, headings, XML tags or labels whatever the destination; a list only if the request lists items. A long request is condensed, keeping its facts and requirements.
- esteso: always sections, in this order: role, goal, context, method, quality criteria, constraints, output format, what to ask before acting. Skip one only if there is nothing true to put in it; never pad it.
Destination (the form of the sections, when the length has them):
- agente: a coding agent (Claude Code, Codex, Cursor) working in the user's project. Tell it to explore the relevant code first, plan, make focused changes in the existing style, verify with the project's tests or build, and report what it changed. Sections as short plain labels followed by a colon ("Ruolo:", "Metodo:"), never XML tags or Markdown headings.
Write in the language of the request. Section names in Italian: Ruolo, Obiettivo, Contesto, Metodo, Criteri di qualità, Vincoli, Formato, Prima di agire; in English: Role, Goal, Context, Method, Quality criteria, Constraints, Output format, Before acting.
</rules>

Do not explore the project, read files or run commands to write the prompt: it says only what the request says, and it tells you to look at the code when you carry it out.

## 2. Show it and ask

Show the prompt exactly as you wrote it, in a fenced code block with nothing before it. Then, on its own line, ask in the language of the request: "Procedo così?" in Italian, "Shall I go ahead?" in English. Then stop: no tools, no file changes, nothing else until the user answers.

## 3. After the answer

- Yes ("sì", "vai", "procedi", "ok", "yes", "go ahead"): carry out the prompt as if the user had sent it as their message, starting from what it says to do first.
- Changes: rewrite the prompt with them, show it again and ask again.
- No: stop, and do nothing else.
