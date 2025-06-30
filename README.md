
---

## 🔄 The Evolutionary Workflow Cycle

Codeflow operates in a continuous, state-aware loop. An error can trigger the `Error Recovery` state at any point, ensuring stability.

**`[ Idle ]` ➔ `[ 1. Review Learnings ]` ➔ `[ 2. Plan Cycle ]` ➔ `[ 3. Execute Story ]` ➔ `[ 4. Learn from Execution ]` ➔ (back to `Idle` or `Review Learnings`)**

1.  **Review Learnings & Refine Standards:** The cycle begins by analyzing learnings from the previous cycle. Successful "pattern candidates" are formally promoted to the **Pattern Catalog**, and standards are updated.
2.  **Plan the Next Cycle:** The system analyzes requirements (PRD), researches best practices (`Context7`), defines a technical approach (`Sequential Thinking`), and creates a detailed, verifiable plan for the next story.
3.  **Execute a Story:** The AI implements a single story, strictly following the plan, applying proven patterns, and passing all automated **Quality Gates** for its complexity level.
4.  **Learn from Execution:** After successful implementation, the system analyzes the code to discover new, effective patterns and logs them as candidates for the next cycle.

---

## 🚀 Getting Started

To initialize a project with the Codeflow system:

1.  **Clone the Repository:**
    ```bash
    git clone https://github.com/your-username/codeflow-system.git
    cd codeflow-system
    ```

2.  **Install Dependencies:**
    The automation scripts require Node.js.
    ```bash
    npm install
    ```

3.  **Initialize the Project:**
    Run the initialization script. This will create the `.project_meta` directory structure and default configuration files.
    ```bash
    node .project_meta/.automation/scripts/init.js
    ```
    > ✅ Your project is now under Codeflow management. You can start interacting with the Codeflow Manager AI.

---

## 🤖 How to Interact with the Codeflow Manager

You act as the **Project Lead**, giving high-level commands. The AI acts as the **Codeflow Manager**, executing them according to the framework.

### Primary Commands

| Command                               | Description                                                                                             | Workflow Step |
| ------------------------------------- | ------------------------------------------------------------------------------------------------------- | ------------- |
| `initiate cycle`                      | Starts the workflow by reviewing past learnings and refining standards.                                  | Step 1        |
| `plan next cycle with PRD: [PRD]`     | Kicks off the planning phase using the provided Product Requirements Document.                            | Step 2        |
| `execute story [ID]`                  | Begins the implementation of a specific, planned story.                                                 | Step 3        |
| `extract learnings from story [ID]` | Analyzes a completed story to find new patterns and insights.                                             | Step 4        |
| `get status`                          | Reports the current state of the system, any active story, and next available actions.                  | Any           |
| `show pattern [ID]`                   | Displays the details of a specific pattern from the catalog.                                            | Any           |
| `report error [details]`              | Manually triggers the error recovery state for an observed issue.                                       | Any           |

---

## 🎬 Use Cases & Example Scenarios

Here are walkthroughs of how you would interact with the Codeflow Manager.

### Scenario 1: Implementing a New Feature (Standard Complexity)

**Goal:** Add a user profile page.

**1. You (Project Lead) initiate planning:**

> **`plan next cycle with PRD: "As a user, I want a profile page where I can see my username, email, and registration date so that I can review my account information."`**

**2. The Codeflow Manager responds with its analysis:**

> **`[Codeflow Manager]`**
> Acknowledged. Initiating planning for the new cycle.
>
> 1.  **PRD Validation:** PRD is clear and actionable.
> 2.  **Story Creation:** `STORY-0001: User Profile Display Page` created.
> 3.  **Complexity Triage:** Assigned **`complexityLevel: 2 (Standard)`**. Full rigor will be applied.
> 4.  **`Context7` Research:**
>     -   Querying: "React best practices for data display components."
>     -   Querying: "Securely fetching and displaying user data from a REST API."
>     -   Findings cached in `.project_meta/.context7/fetched_docs/`.
> 5.  **`Sequential Thinking` Analysis:**
>     -   *Problem:* How to fetch and render user data efficiently and securely?
>     -   *Option 1:* Client-side fetching on component mount.
>     -   *Option 2:* Server-side rendering (SSR).
>     -   *Decision:* Client-side fetching is sufficient for this non-critical page. Rationale logged in `sequential_thinking_log.json`.
> 6.  **Pattern Catalog Consultation:**
>     -   Identified applicable pattern: `PATTERN-0102-001 (Stateful Data Fetcher)`.
>
> **Status:** `cycle_planned`. Ready to execute `STORY-0001`.

**3. You (Project Lead) start the implementation:**

> **`execute story STORY-0001`**

**4. The Codeflow Manager executes and reports:**

> **`[Codeflow Manager]`**
> Executing `STORY-0001`.
>
> -   **Implementation:** `UserProfile.jsx` component created using `PATTERN-0102-001`. Unit tests `UserProfile.test.js` created.
> -   **Running Implementation Quality Gate (`Level 2`):**
>     -   ✅ Unit Test Coverage: **92%** (Threshold: ≥ 90%)
>     -   ✅ Linting: **0 errors**.
>     -   ✅ Security Scan (SAST): **0 high/critical vulnerabilities**.
>     -   ✅ `Context7` Compliance: Best practices for React hooks applied.
>     -   ✅ Pattern Compliance: `Stateful Data Fetcher` pattern correctly implemented.
>
> **Status:** `story_completed`. All quality gates passed. Ready for learning extraction.

### Scenario 2: A Complex Architectural Refactor

**Goal:** Migrate the authentication system from monolith to a microservice.

**1. You (Project Lead) initiate planning with a complex requirement:**

> **`plan next cycle with PRD: "Refactor the entire authentication system into a separate microservice to improve scalability and security."`**

**2. The Codeflow Manager responds with a more rigorous plan:**

> **`[Codeflow Manager]`**
> Acknowledged. This is a high-impact architectural change.
>
> 1.  **Story Creation:** `STORY-0002: Auth System Refactor to Microservice` created.
> 2.  **Complexity Triage:** Assigned **`complexityLevel: 3 (Complex)`**. Maximum rigor and documentation required.
> 3.  **ADR Required:** A new Architecture Decision Record (`ADR-0004`) must be created and approved for this change.
> 4.  **`Context7` Research:**
>     -   Querying: "JWT-based authentication patterns for microservices."
>     -   Querying: "API Gateway security best practices."
>     -   Querying: "Database schema migration strategies for service extraction."
> 5.  **`Sequential Thinking` Analysis:**
>     -   Deep analysis of trade-offs (e.g., performance latency vs. security isolation), risk assessment of migration path, and evaluation of communication protocols (REST vs. gRPC). Logged in `sequential_thinking_log.json`.
> 6.  **Pattern Catalog Consultation:**
>     -   Identified applicable patterns: `PATTERN-0001-003 (API Gateway)` and `PATTERN-2005-001 (Strangler Fig Application)`.
>
> **Status:** `cycle_planned`. Ready to execute `STORY-0002`.

### Scenario 3: A Minor Bug Fix (Fast-Track)

**Goal:** Fix a typo on the home page.

**1. You (Project Lead) initiate planning:**

> **`plan next cycle with PRD: "Fix typo on the homepage. Change 'Wlecome' to 'Welcome'."`**

**2. The Codeflow Manager uses the fast-track process:**

> **`[Codeflow Manager]`**
> Acknowledged. Initiating planning.
>
> 1.  **Story Creation:** `STORY-0003: Fix Homepage Typo` created.
> 2.  **Complexity Triage:** Assigned **`complexityLevel: 1 (Minor)`**. Fast-track process will be used.
> 3.  **Analysis:** No new architecture. `Context7` and `Sequential Thinking` research is skipped as this is a content change.
> 4.  **Pattern Catalog Consultation:** No applicable pattern for a typo fix.
>
> **Status:** `cycle_planned`. Ready to execute `STORY-0003`.

**3. You start the implementation:**

> **`execute story STORY-0003`**

**4. The Codeflow Manager reports with scaled-down checks:**

> **`[Codeflow Manager]`**
> Executing `STORY-0003`.
>
> -   **Implementation:** Modified `HomePage.jsx`.
> -   **Running Implementation Quality Gate (`Level 1`):**
>     -   ✅ Unit Test Coverage: Test for component rendering passed. (Threshold: Relaxed).
>     -   ✅ Linting: **0 errors**.
>     -   (Security and performance scans are skipped for Level 1).
>
> **Status:** `story_completed`.

### Scenario 4: Handling a Critical Failure

**Context:** The system is executing a story, and a critical build step fails.

**1. The Codeflow Manager detects the failure and takes immediate action:**

> **`[Codeflow Manager]`**
> **`CRITICAL ERROR DETECTED`** during execution of `STORY-0004`.
>
> -   **Trigger:** Post-condition verification failed. The integration build failed.
> -   **Current State:** `executing_story`
> -   **Action:** Halting all operations. Transitioning to **`error_recovery`** state.
> -   **Logging:** Error `ERR-20231027-0001` logged in `.project_meta/.errors/error_log.json` with full context.
> -   **Recovery Plan:** Consulting recovery matrix for `ERR-INT` (Integration Error). Executing **`rollback_to_last_good_state`**.
> -   **Executing Rollback:** Reverting codebase to commit `a1b2c3d4`. Restoring metadata from checkpoint.
>
> **Status:** `idle`. System is now in a stable state. The failed operation can be investigated and retried.

---

## 🧩 Core Components Deep Dive

-   **`Context7` Integration:** A mandatory external research service. Before any significant work, Codeflow queries `Context7` for official documentation, security best practices, and industry-standard patterns relevant to the tech stack. This ensures decisions are based on current, external knowledge, not just internal habits.
-   **`Sequential Thinking` MCP:** A mandatory internal reasoning framework. For any decision, Codeflow must use this process to break down the problem, explore alternatives, weigh pros and cons, and document the rationale. This ensures every decision is logical, evidence-based, and traceable.
-   **Pattern Catalog:** The heart of the system's learning capability. It's a living library of validated, reusable solutions for architecture, design, and implementation. Each cycle refines this catalog, making the system more effective over time.
-   **Quality Gates:** Automated, non-negotiable checkpoints in the workflow. A story cannot move from implementation to integration unless all its quality gate criteria (e.g., test coverage, security scan, pattern compliance) are met.

---

## 🤝 Contributing

We welcome contributions to improve the Codeflow System! Please follow these steps:

1.  **Fork the repository.**
2.  **Create a new feature branch** (`git checkout -b feature/your-feature-name`).
3.  **Make your changes.** Please adhere to the Codeflow principles in your development process.
4.  **Submit a pull request** with a detailed description of your changes.

All contributions will be reviewed to ensure they align with the core philosophy of the system.

---

## 📄 License

This project is licensed under the MIT License. See the [LICENSE](LICENSE) file for details.
