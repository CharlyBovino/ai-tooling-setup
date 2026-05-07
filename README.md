# AI Tooling Setup Project

## Objective

Document the setup process of AI-assisted development tools as part of a technical onboarding task, with a focus on problem-solving, debugging, and environment configuration.

---

## Tools Installed

- Cursor IDE (AI-powered code editor)
- Git (version control system)
- GitHub (code hosting platform)

**Note:**  
The instructions referenced installing specific AI extensions (Claude Code, Codex), but the current version of Cursor does not expose these as installable extensions. Instead, it provides built-in AI capabilities through its integrated agent system.

---

## Steps Completed

1. Installed Cursor IDE and logged in
2. Connected Cursor with GitHub
3. Attempted to clone the repository using a Cursor agent
4. Encountered missing system dependency (Git via Apple Command Line Tools)
5. Installed Apple Command Line Tools using terminal
6. Manually cloned the repository using Git
7. Re-created a new agent and successfully opened the repository in Cursor
8. Created and edited the [README.md](http://README.md) file
9. Configured Git identity and authentication
10. Committed and pushed changes to GitHub

---

## Issues Encountered

### 1. Missing Git / Apple Command Line Tools

**Problem:**  
The agent failed to clone the repository and returned the following error:  
“Tried to clone... but this environment can’t run git because Apple Command Line Tools are missing.”

**Observation:**  
The agent attempted fallback strategies using `curl`, including inspecting HTTP headers and downloaded content, but those attempts failed.

**Diagnosis:**  
Git was not available in the system because Apple Command Line Tools were not installed.

**Solution:**  
Installed Apple Command Line Tools using:

xcode-select --install

**Result:**  
Git became available in the system, enabling repository cloning operations.

---

### 2. Environment Mismatch (Cursor vs System)

**Problem:**  
After installing Git, the existing agent session did not recognize the updated system state and continued failing.

**Observation:**  
Cursor appears to run commands in an isolated execution environment that may not immediately reflect system-level changes.

**Diagnosis:**  
The agent context was initialized before Git was installed and did not refresh its environment.

**Solution:**

- Manually cloned the repository using:

git clone [https://github.com/CharlyBovino/ai-tooling-setup.git](https://github.com/CharlyBovino/ai-tooling-setup.git)

- Created a new agent from scratch
- Repeated the same request (clone/open repository)

**Result:**  
The repository was successfully opened in Cursor and recognized as a valid project.

---

### 3. GitHub Authentication Failure (Personal Access Token required)

**Problem:**  
While attempting to push changes to GitHub, the operation failed with a 403 error. GitHub no longer supports username/password authentication for Git operations from the terminal.

**Diagnosis:**  
Authentication was failing because Git requires a Personal Access Token (PAT) instead of a password.

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

git config --global [user.name](http://user.name) "CharlyBovino"  
git config --global [user.email](http://user.email) "[charlybovino.smm@gmail.com](mailto:charlybovino.smm@gmail.com)"

- Amended the previous commit to update the author information
- Performed a forced push to overwrite the incorrect commit history

**Result:**  
Commits are now correctly attributed to the GitHub account and linked to the user profile.

---

## Technical Observations

- AI agents may implement fallback strategies (e.g., `curl`) when primary tools fail
- System dependencies (like Git) are critical for developer workflows and may not be pre-installed
- Changes in the system environment are not always reflected in existing agent sessions
- Reinitializing execution context (creating a new agent) can resolve environment inconsistencies
- GitHub authentication workflows have evolved toward token-based security (PAT, Personal Access Token)
- Git maintains a separate local identity configuration that must match the remote platform for proper attribution
- Version control systems allow rewriting history (e.g., amend + force push), which should be used carefully

---

## Key Learnings

- Importance of system-level dependencies in development environments
- Value of progressive debugging instead of retrying failing steps without diagnosis
- Need to understand differences between local system state and tool-specific execution environments
- Practical handling of authentication and identity issues in Git workflows
- Improved confidence navigating real-world setup friction using AI-assisted tools

