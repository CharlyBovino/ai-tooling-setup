# AI Tooling Setup Project

## Objective

Document the setup process of AI-assisted development tools as part of a technical onboarding task, focusing on problem-solving, debugging, and environment configuration.

---

## Tools Installed

- Cursor IDE (AI-powered code editor)
- Git (version control system)
- GitHub (code hosting platform)

Note: The instructions referenced installing specific AI extensions (Claude Code, Codex), but the current version of Cursor does not expose these as installable extensions.

---

## Steps Completed

1. Installed Cursor IDE and logged in.
2. Connected Cursor with GitHub.
3. Attempted to clone the repository using Cursor Agent.
4. Encountered missing system dependency (Git via Apple Command Line Tools).
5. Installed Apple Command Line Tools using terminal.
6. Manually cloned the repository using Git.
7. Re-created a new agent and successfully opened the repository in Cursor.

---

## Issues Encountered

### 1. Missing Git / Apple Command Line Tools

Problem:  
The agent failed to clone the repository and returned the following error:

“Tried to clone... but this environment can’t run git because Apple Command Line Tools are missing.”

Observation:  
The agent attempted fallback strategies using curl, but these attempts failed after inspecting HTTP headers and downloaded content.

---

### 2. Environment Mismatch (Cursor vs System)

Problem:  
After installing Git via terminal, the existing agent session did not recognize the updated system state.

Observation:  
Cursor appears to run commands in an isolated environment that may not immediately reflect system-level changes.

---

### 3. GitHub Authentication Failure (Personal Access Token required)

**Problem:**  
While attempting to push changes to GitHub, the operation failed with a 403 error. GitHub no longer supports username/password authentication for Git operations from the terminal.

**Diagnosis:**  
Authentication was failing because Git required a Personal Access Token (PAT) instead of a password.

**Solution:**

- Generated a Personal Access Token (PAT) with `repo` scope from GitHub Developer Settings
- Updated the remote repository URL to include the token for authentication

**Result:**  
Successfully authenticated and pushed changes to the remote repository.

---

### 4. Commit Author Mismatch

**Problem:**  
The commit author was incorrectly set to a different name ("Natalia Brochero"), which was not associated with the GitHub account. As a result, commits were not properly attributed.

**Diagnosis:**  
Git was using a previously configured global identity that did not match the current GitHub user.

**Solution:**

- Updated global Git configuration:
  - [user.name](http://user.name)
  - [user.email](http://user.email)
- Amended the previous commit to update the author information
- Forced push to overwrite the incorrect commit history

**Result:**  
Commits are now correctly attributed to the GitHub account and linked to the user profile.

---

## Solutions

### Solution 1 — Install required system dependencies

Executed in terminal:

xcode-select --install

This installed Apple Command Line Tools, enabling Git support.

---

### Solution 2 — Manual repository cloning

Executed:

git clone [https://github.com/CharlyBovino/ai-tooling-setup.git](https://github.com/CharlyBovino/ai-tooling-setup.git)

Result:

- Repository cloned successfully on first attempt
- No authentication issues

---

### Solution 3 — Reset agent context

Instead of continuing with the original agent:

- Created a new agent from scratch
- Repeated the same request (clone/open repository)

Result:

- Repository opened successfully
- Cursor recognized the project structure

---

## Technical Observations

- AI agents may implement fallback strategies (e.g., curl) when primary tools fail.
- System dependencies (like Git) are critical for developer workflows and may not be pre-installed.
- Changes in the system environment are not always reflected in existing agent sessions.
- Reinitializing context (new agent) can resolve environment inconsistencies.

---

## Key Learnings

- Importance of system-level dependencies in development environments
- Value of progressive debugging instead of retrying the same failing step
- Need to understand differences between local system state and tool-specific execution environments
- Practical experience handling real-world setup friction using AI-assisted tools

