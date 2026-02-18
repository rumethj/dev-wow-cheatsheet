# Code Review Process: Guidelines for Continuous Improvement and Collaboration

> A good review process requires that pull requests get addressed as soon as possible in order to prevent the project from being impeded. Ideally, pull requests are reviewed within **two hours of their submission.**

---

## Get Feedback with Pull Requests

Pull requests support reviewing and merging code collaboratively. When a developer adds a feature or fixes a bug, they create a pull request to start merging changes into the upstream branch. Team members review and approve the code before finalizing it.

Use pull requests:

- To review work in progress.
- To get early feedback.
- With the option for owners to abandon a pull request at any time without committing to merge.

---

## Get Code Reviewed

Code review during a pull request aims beyond identifying obvious bugs — that is the role of tests. Effective code review detects subtle issues that could cause costly problems later.

There is no such thing as *perfect* code; there is only **better** code. Reviewers should not require the author to polish every tiny piece of a change list before granting approval. Instead, they should balance the need to make forward progress with the importance of the changes they are suggesting.

Rather than seeking perfection, reviewers should seek **continuous improvement**.

Code review is a way to have a conversation about the code where participants will:

- **Improve code quality** by identifying and removing defects before they can be introduced into shared code branches.
- **Learn and grow** by having others review the code; we get exposed to unfamiliar design patterns or languages and can break bad habits.
- **Build shared understanding** between developers over the project's code. Code reviews encourage and strengthen collaboration and communication between developers. The team gains a clear history of all changes between the main branch and feature branches.

---

## Pre-Review Quality Requirements

Before submitting a Pull Request (PR) for review, ensure the following criteria are met.

### High-level Pre-Review Workflow (Diagram)

```mermaid
flowchart TD
    A[Start: Before submitting a PR] --> B[1. Traceability<br/>Every PR must be linked to a Jira issue/story]
    B --> C[2. Branch naming<br/>Branch name follows agreed naming conventions]
    C --> D[2.1 Branch naming convention<br/>&lt;branch_type&gt;/&lt;user_id&gt;/&lt;jira_id&gt;-&lt;short_description&gt;<br/>Examples + rules]
    D --> E[2. Pull Request (PR) title convention<br/>[jira_id] &lt;short_description&gt;]
    E --> F[3. PR description (change log quality)<br/>Clear, high-level, explains what & why]
    F --> G[NOTE: Developers are advised to integrate IDE lint tools (e.g., SonarLint)]
```

### 1) Traceability

- Every PR **must be linked to a Jira issue/story**.

### 2) Branch Naming

- The branch name **must follow the agreed naming conventions**.

#### 2.1 Branch Naming Convention

To maintain clarity and traceability, all development branches must follow the naming pattern below:

```text
<branch_type>/<user_id>/<jira_id>-<short_description>
```

**Examples:**

```text
topic/wicrlk/NEXUS-3805-define_a_SOP_for_branching
bugfix/wicrlk/NEXUS-3805-define_a_SOP_for_branching
```

##### Branch Naming Rules

| **Component**        | **Description**                                                                 |
|----------------------|---------------------------------------------------------------------------------|
| `branch_type`        | Type of the branch: `topic`, `bugfix`, or `release`. Use lowercase only.       |
| `user_id`            | Your corporate user ID. Use lowercase only.                                    |
| `jira_id`            | Corresponding Jira issue ID. Use uppercase only.                               |
| `short_description`  | Brief summary of the task (≤ 50 characters). Use lowercase and underscores.    |

When creating *topic branches* through Jira, in the **branch type** drop-down select **Feature**. When **Feature** type is selected, the branch will start with the prefix `topic`.

#### 2.2 Pull Request (PR) Title Convention

All PRs must follow a standard title format to ensure clear association with Jira issues and to improve searchability and tracking.

**Format:**

```text
[jira_id] <short_description>
```

**Example:**

```text
[NEXUS-3805] code promotion to dev platform
```

##### PR Title Rules

| **Component**       | **Description**                                                   |
|---------------------|-------------------------------------------------------------------|
| `jira_id`           | The relevant Jira issue ID. Must be in uppercase.                |
| `short_description` | A concise summary of the work (≤ 50 characters).                 |

> ⚠️ **Note:** Including the Jira ID is mandatory as it links the PR directly to the Jira issue and Bitbucket (BB), enabling automated traceability and efficient tracking.

### 3) PR Description (Change Log Quality)

The PR description is a **public and permanent record**. It should clearly communicate:

- **What** change is being made (high-level summary).
- **Why** the change is needed (context, reasoning, constraints, trade-offs).

To meet this, answer the following in the PR description:

- What does this PR do? (new feature / bug fix / refactor, etc.)
- Have you added or updated any dependencies?
- Is this covered with tests?
- How can we run/test this change?
- Does it introduce any breaking changes?

### 4) Code Coverage

- Code coverage expectations must be met.
- Any coverage-related issues must be resolved **before raising/submitting the PR**.

### 5) Static Code Analysis

- New code **must not introduce new violations** compared to the existing baseline.

### 6) Initial Build

- The initial build / CI checks must pass successfully **before submitting the PR for review**.
- At least two latest builds should have passed.

### 7) Jira Readiness for Review

- The Jira issue must be moved to the **PR Review** state.
- The Jira issue must be **assigned to the first reviewer(s)**.

### 8) PR Submission

Once all the above are satisfied and CI checks have passed, the PR can be submitted for review.

> **NOTE:** All developers are advised to integrate lint tools configured to their IDE.  
> Recommended tool: **SonarLint**  
> <https://ifsdev.atlassian.net/wiki/spaces/QS/pages/1575125098>

---

## Code Review Process

To ensure pull requests (PRs) are reviewed consistently without slowing down delivery, this process uses a **two-phase review approach**. It starts with a **distributed team review** where PRs are individually assigned and reviewed asynchronously, and only escalates to the **architect** when architectural input is required. This helps the team catch most issues early, keeps reviews predictable, and reserves architect time for the changes that truly need it.

### Phase 1: Assigned Individual Review (Team)

- A PR becomes ready for review (partial submissions allowed).
- The PR link is shared in the review chat in advance.
- Instead of a scheduled meeting, **each team member spends about 1 hour reviewing assigned PRs**.
- Review feedback includes comments, suggestions, and questions.
- **Outcome:** the team decides if the PR requires architectural review.

### Decision Gate: “Architect revisit needed?”

- **No:** The author addresses comments and finalizes the PR normally.
- **Yes:** The PR advances to Phase 2.

### Phase 2: Architect Review (Scheduled)

- The PR link is added to the architect review meeting chat, and the architect is notified.
- The architect reviews it during a **recurring 1-hour review slot** (meeting time may shift based on availability).
- The architect provides feedback, then the PR returns to the author for finalization.

---

## Effective Code Review Process – Workflow Diagram

```mermaid
flowchart LR
    %% Lanes
    subgraph Author
        A1[Step 1: Preparing review request]
        A2[Step 2: Selecting & notifying reviewers]
        A5[Step 5: Addressing the review feedback]
    end

    subgraph Reviewers
        R3[Step 3: Checking code changes proposed]
        R4[Step 4: Providing review feedback]
        D{Is there review feedback<br/>to address?}
        R6[Step 6: Review decision:<br/>Accepting or rejecting changes]
    end

    subgraph "Generative AI"
        G1[Reviewability support:<br/>Improve description and self-review]
        G2[Saving-time support:<br/>Help provide feedback]
        G3[Understanding support:<br/>Summarize & explain the change]
        G4[Understanding support:<br/>Explain coding issues reported]
        G5[Saving-time support:<br/>Assist with code-fix implementation]
    end

    Start([Changed code]) --> A1
    A1 --> A2
    A2 --> R3
    R3 --> R4
    R4 --> D
    D -- "Yes" --> A5
    A5 --> R3
    D -- "No" --> R6

    %% AI support relationships (dashed)
    A1 -. Reviewability improvement .-> G1
    A2 -. Notify & context support .-> G2
    R3 -. Understanding aid .-> G3
    R4 -. Explain issues .-> G4
    A5 -. Fix implementation help .-> G5

    classDef ai fill=#f5e1ff,stroke=#b36bff,color=#000;
    class G1,G2,G3,G4,G5 ai;
```

---

## Code Review Guidelines (For the Reviewer)

- The review should include inline comments for each significant change to facilitate tracking and future learning.

**References on style guides:**

- General Google style guides: <https://google.github.io/styleguide/>
  - Go: <https://google.github.io/styleguide/go/>
  - JavaScript: <https://google.github.io/styleguide/jsguide.html>
  - Java: <https://google.github.io/styleguide/javaguide.html>
  - JSON: <https://google.github.io/styleguide/jsoncstyleguide.xml>
  - Markdown: <https://google.github.io/styleguide/docguide/style.html>
  - Python: <https://google.github.io/styleguide/pyguide.html>
  - Shell: <https://google.github.io/styleguide/shellguide.html>
- Tekton docs formatting: <https://tekton.dev/docs/contribute/doc-con-formatting/>
- Bitbucket Pipelines formatting:  
  <https://support.atlassian.com/bitbucket-cloud/docs/build-test-and-deploy-with-pipelines/>
- Rust style guide: <https://doc.rust-lang.org/style-guide/>

If the PR review is completed and you are satisfied with the changes, you should **approve the PR**.

---

## How to Handle Reviewer Comments (For the Change Log Owner)

When a change log is submitted for review, it is common for the reviewer to provide feedback through various comments. Understanding how to effectively manage and address reviewer comments is essential.

### Don’t Take It Personally

- The objective of a code review is to uphold the quality of our codebase and products. When a reviewer offers feedback on your code, treat it as their effort to assist you, enhance the codebase, and benefit build and deployment, rather than as a personal criticism of you or your skills.
- **Never respond in anger to code review comments.** It is a serious breach of professional etiquette that will remain in the code review tool indefinitely. If you find yourself too angry or irritated to respond kindly, step away from your computer for a while or focus on another task until you regain the composure needed to reply politely.

### Fix the Code

- If a reviewer expresses confusion about any aspect of your code, your initial action should be to clarify the code itself.
- If the code remains unclear, consider inserting a code comment to explain the purpose of the code. Only when a code comment appears unnecessary should you resort to providing an explanation within the code review tool.
- When a reviewer struggles to understand a section of your code, it is likely that others reviewing the code in the future will face similar challenges. Composing a response in the code review tool does not benefit future readers; improving the code or adding comments does.

### Think Collaboratively

- Writing a change log can be a demanding task that requires significant effort. It is gratifying to submit one for review and feel a sense of completion.
- It can be disheartening to receive feedback requesting changes, particularly if you do not share the same perspective.
- In such situations, pause and reflect on whether the reviewer's input offers valuable insights that can benefit the codebase and build/deployment processes. Your first goal should be to **understand** the reviewer’s requests.
- If you do not understand the feedback, ask for clarification.
- If you understand the comments but hold a different viewpoint, approach the situation with a **collaborative** mindset, not a combative or defensive one.

### Resolve Conflicts

The initial approach to conflict resolution should prioritize reaching consensus with your reviewer.

If reaching consensus proves challenging, refer to the following guidance on handling such scenarios:

- <https://google.github.io/eng-practices/review/reviewer/standard.html>

---

## PR Merge

- As a best practice, **always delete the branch after merging the PR.**

---

## Resources

- **Best Kept Secrets of Peer Code Review**, Copyright © 2013 by SmartBear Software  
  (see attached PDF in the original Confluence page)[1]