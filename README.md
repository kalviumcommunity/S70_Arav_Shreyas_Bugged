
#  Bugged — Your AI Debugging Copilot for VS Code

> **Automatically detect, understand, and fix bugs with step-by-step replays, Git awareness, and intelligent debugging.**

Bugged is an AI-powered debugging assistant built as a VS Code extension. It reads your entire codebase, understands errors, interprets git history, injects debugging logic, and fixes bugs for you — just like a real software engineer would.

---

##  Features

###  Smart Bug Detection

* Scans and chunks your **entire codebase** using AI-aware context windows
* Watches for runtime errors, logs, and test failures
* Hooks into your terminal, console, and CI logs to catch bugs in real time

###  AI-Powered Fixing Engine

* Understands errors like stack traces, undefined behavior, and crashes
* Uses RAG to pull relevant code, commits, and diffs for context
* Calls custom functions to suggest or apply code fixes
* Auto-injects debugging code if first attempt fails
* Re-attempts fix using new debug insights until resolved

###  Markdown Fix Reports

* After every bug fix, generates a clean `.md` file that contains:

  *  What the bug was
  *  Why it happened
  *  Steps taken to fix it
  *  Final code diff / patch

###  Bonus: Fix Replay System

* Replay every fix step-by-step
* View and **revert or reapply patches**
* Add **manual comments** to fix reports
* Fix suggestions include a **"Fix" button** — click to apply

###  Git Integration

* Parses **Git history, commit diffs, and blame metadata**
* Associates bugs with recent changes
* Adds traceability: "This bug came from commit abc123 by Alice"

###  Manual Error Reporting (Human-in-the-Loop)

* You can manually report a bug just by prompting:

  * "Something broke in this function..."
  * "Why is this loop causing issues?"
* Bugged will:

  * Chunk the right code
  * Run its RAG pipeline
  * Fix or explain the issue like a real dev

###  Error Understanding Engine

* Reads console logs, stack traces, test failures, and runtime exceptions
* Matches logs with source lines + Git context
* Supports backend + frontend + test failures

###  Works With or Without Git

Whether you're hacking on a throwaway script or debugging a production repo:

* **Git Project:** Full Git context (blame, diffs, commit logs)
* **Non-Git Project:** Uses local analysis, fallback tracing, and raw code context
*  Optionally allows you to manually tag or name snapshots for tracking

---

##  Project Concepts Explained

###  Prompting

Users can report issues and request fixes by simply typing prompts like:

* "Fix the error in this file"
* "Why is this function throwing an exception?"
* "Debug this loop"
  The system interprets natural language and routes the prompt to the proper logic for analysis and fixing.

###  Structured Output

All bug fixes return structured JSON with:

* File path
* Line number(s)
* Fix description
* Explanation
* Patch/diff
  This structure ensures predictable integration with the extension UI and Markdown reporting system.

###  Function Calling

Bugged uses OpenAI's function calling to:

* Detect specific error types
* Suggest context-aware fixes
* Inject debug code
* Manage retry logic and validation
  Each function is defined with strict schemas for inputs and outputs.

###  RAG (Retrieval-Augmented Generation)

We use LangChain and vector databases (Chroma/Weaviate) to:

* Chunk and embed the codebase
* Retrieve relevant functions/files related to the bug
* Pass only the most relevant context to the model
  This makes fixes accurate, efficient, and scalable across large codebases.

---


##  How It Works (Flow)

1.  You click the "Bugged" button in VS Code
2.  Bugged chunks your codebase and loads Git metadata
3.  Scans for bugs, errors, and logs — or waits for error triggers
4.  Matches problem with relevant code using RAG
5.  Generates structured fix plan using function calling
6.  Applies patch OR injects debug code and tries again
7.  Logs fix report in `.bugged/` folder as Markdown
8.  Adds replay entry (can undo, redo, or reapply fixes)

---

##  User Interaction Modes

*  Auto-trigger on crash/error
*  Manual bug fix request via VS Code panel
*  Prompt-based error reporting (just type your issue)
*  AI explanations of bug reasoning ("Why did this happen?")
*  Apply fix with one click
*  Replay or undo any previous fix

---
