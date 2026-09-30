# 🤖 Multi-Agent Coding Solver

### A Multi-Architecture Agentic AI Framework for Coding Problem Solving

A self-contained **multi-agent coding solver** that demonstrates how specialized agents can collaborate through different agentic AI architectures to understand, generate, execute, test, critique, and verify solutions to common programming problems.

The project implements **7 specialized agents** and **7 different agentic architectures**, with an interactive **Gradio interface** for viewing generated code, test results, agent execution traces, and verification outcomes.

---

## 🌟 Project Highlights

* 🧠 **7 specialized agents**, each with a dedicated responsibility
* 🔄 **7 agentic AI architectures** for workflow orchestration
* 💻 Real Python code execution against predefined test cases
* 🧪 Automated test-case validation
* 🔍 Critique and failure analysis
* ✅ Independent final verification
* 📊 Detailed agent execution trace
* 🎨 Interactive Gradio-based user interface
* ☁️ Google Colab compatible
* 💰 No paid LLM API required
* 🛡️ Graceful handling of unsupported coding requests

---

## 🏗️ System Architecture

The system follows a multi-stage agentic workflow:

```text
                    ┌──────────────────────┐
                    │     User Request     │
                    └──────────┬───────────┘
                               │
                               ▼
                    ┌──────────────────────┐
                    │ Coordination Agent   │
                    └──────────┬───────────┘
                               │
                               ▼
                    ┌──────────────────────┐
                    │    Planning Agent    │
                    └──────────┬───────────┘
                               │
                               ▼
                    ┌──────────────────────┐
                    │    Reasoning Agent   │
                    └──────────┬───────────┘
                               │
                               ▼
                    ┌──────────────────────┐
                    │      Logic Agent     │
                    │ Code + Execution     │
                    └──────────┬───────────┘
                               │
                    ┌──────────┴──────────┐
                    ▼                     ▼
          ┌─────────────────┐   ┌─────────────────┐
          │ Pattern Agent   │   │  Critic Agent   │
          └────────┬────────┘   └────────┬────────┘
                   └──────────┬──────────┘
                              ▼
                    ┌──────────────────────┐
                    │   Verifier Agent     │
                    │ Independent Check    │
                    └──────────┬───────────┘
                               │
                               ▼
                    ┌──────────────────────┐
                    │   Verified Result    │
                    └──────────────────────┘
```

---

## 🤖 The 7 Specialized Agents

| Agent                 | Responsibility                                                  |
| --------------------- | --------------------------------------------------------------- |
| **CoordinationAgent** | Coordinates the overall workflow and assembles the final result |
| **PlanningAgent**     | Decomposes the coding task into ordered steps                   |
| **ReasoningAgent**    | Identifies the most relevant coding problem type                |
| **LogicAgent**        | Retrieves the implementation and executes it against test cases |
| **PatternAgent**      | Analyses code size, test results, and failures                  |
| **CriticAgent**       | Reviews the solution for ambiguity and correctness issues       |
| **VerifierAgent**     | Independently reruns the test suite for final verification      |

Each agent is designed around a specific responsibility instead of performing the entire task alone.

---

# 🔄 7 Agentic AI Architectures

One of the main features of this project is the ability to execute the same coding workflow using different orchestration strategies.

### 1. Single-Agent

A single coordinated workflow performs the complete coding task.

```text
Request
   ↓
Planning → Reasoning → Logic → Analysis → Critique → Verification
```

---

### 2. Sequential

Agents execute in a fixed sequence where the output of one stage becomes the input of the next.

```text
Planning
   ↓
Reasoning
   ↓
Logic
   ↓
Pattern
   ↓
Critic
   ↓
Verifier
```

---

### 3. Hierarchical

A higher-level coordinator delegates different responsibilities to specialized agents.

```text
              Coordinator
                   │
              Supervisor
                   │
       ┌───────────┼───────────┐
       ↓           ↓           ↓
   Analysis     Solver      Verification
```

---

### 4. Parallel

Independent tasks execute concurrently where possible.

For example:

```text
             ┌── Planning ──┐
Request ─────┤               ├──→ Logic
             └─ Reasoning ──┘

             ┌── Pattern ───┐
Test Results ┤              ├──→ Verification
             └── Critic ────┘
```

The implementation uses `ThreadPoolExecutor` to execute independent branches concurrently.

---

### 5. Collaborative

Agents communicate through a shared **blackboard**.

```text
Reasoning Agent
       ↓
   Blackboard
       ↓
Logic Agent → Pattern Agent → Critic Agent
       ↓
   Verification
```

Agents can read previously generated information and contribute new findings to the shared state.

---

### 6. Debate

The system introduces an Advocate–Skeptic workflow.

```text
        Advocate
   Reasoning + Logic
          │
          ▼
      Proposed
      Solution
          │
          ▼
        Skeptic
       Critic Agent
          │
     ┌────┴────┐
     │         │
   Accept    Challenge
               │
               ▼
        Alternative Match
               │
               ▼
           Verifier
```

If the proposed solution fails testing and another candidate exists, the workflow can fall back to the next-ranked candidate.

---

### 7. Supervisor

A supervisor actively monitors the workflow and can intervene when a solution fails.

```text
             Supervisor
                  │
       ┌──────────┼──────────┐
       ↓          ↓          ↓
   Reasoning    Logic     Critic
       │          │          │
       └──────────┼──────────┘
                  ↓
             Verification
                  │
          ┌───────┴───────┐
          ↓               ↓
       Success           Retry
                          ↓
                  Next Candidate
```

The Supervisor architecture can retry with another ranked template when the first candidate fails testing.

---

# 💻 Supported Coding Problems

The project includes a curated template library covering common programming problems such as:

* Two Sum
* Reverse a String
* Palindrome Check
* Fibonacci
* Factorial
* Prime Number Check
* FizzBuzz
* Binary Search
* Sorting
* Anagram Check
* Greatest Common Divisor (GCD)
* Balanced Parentheses

The system uses keyword-based matching against these predefined problem templates.

---

# ⚙️ How It Works

When a user submits a coding request:

### Step 1 — Understand the Request

The system receives the user's coding problem.

### Step 2 — Plan

The `PlanningAgent` creates an ordered workflow:

```text
Understand Requirement
        ↓
Select Algorithm
        ↓
Generate Code
        ↓
Run Tests
        ↓
Analyse Results
        ↓
Critique Code
        ↓
Verify Final Solution
```

### Step 3 — Reason

The `ReasoningAgent` compares the request with the available coding problem templates and identifies candidate matches.

### Step 4 — Generate and Execute

The `LogicAgent` retrieves the selected implementation and executes it against its predefined test cases.

### Step 5 — Analyse

The `PatternAgent` analyses:

* Number of tests passed
* Number of tests failed
* Code size
* Failing test cases

### Step 6 — Critique

The `CriticAgent` examines the result and identifies:

* Ambiguous problem matches
* Failed test cases
* Potential correctness issues

### Step 7 — Verify

The `VerifierAgent` independently reruns the test suite.

A solution is considered verified only when the verification stage confirms the test results.

---

# 🧪 Verification Approach

The project intentionally performs **real code execution** instead of simply assuming that generated code is correct.

The verification workflow is:

```text
Generated Implementation
          ↓
     Test Execution
          ↓
    Pass / Fail Results
          ↓
      Critic Review
          ↓
 Independent Re-run
          ↓
   Final Verification
```

This makes the verification process reproducible and transparent.

---

# 🖥️ Interactive Gradio Interface

The project includes a Gradio-based interface that provides:

### 📝 Coding Problem Input

Enter a natural-language programming problem.

### 💻 Generated Code

View the selected implementation.

### 🧪 Test Results

View individual test cases and their pass/fail status.

### 🔎 Agent Execution Trace

Inspect which agent performed each stage of the workflow.

### ✅ Verification Status

See whether the final solution successfully passed independent verification.

---

# 🛠️ Technologies Used

| Technology             | Purpose                                |
| ---------------------- | -------------------------------------- |
| **Python**             | Core implementation                    |
| **Gradio**             | Interactive web interface              |
| **Pandas**             | Execution trace and test-result tables |
| **ThreadPoolExecutor** | Parallel agent execution               |
| **Google Colab**       | Development and execution environment  |

---

# 📂 Project Structure

```text
multi-agent-coding-solver/
│
├── Multi-Agent-Coding-Solver.ipynb
├── README.md
├── requirements.txt
├── LICENSE
└── .gitignore
```

---

# 🚀 Getting Started

## Option 1 — Google Colab

The easiest way to run the project is using Google Colab.

1. Open the notebook:

```text
Multi-Agent-Coding-Solver.ipynb
```

2. Upload it to Google Colab.

3. Run the cells from top to bottom.

4. Launch the Gradio interface.

5. Enter a supported coding problem.

---

## Option 2 — Local Environment

Clone the repository:

```bash
git clone https://github.com/YOUR-USERNAME/multi-agent-coding-solver.git
```

Move into the project directory:

```bash
cd multi-agent-coding-solver
```

Install dependencies:

```bash
pip install -r requirements.txt
```

Open the notebook:

```bash
jupyter notebook
```

Then run:

```text
Multi-Agent-Coding-Solver.ipynb
```

---

# 📌 Example Queries

Try queries such as:

```text
Write a function to check if a number is prime.
```

```text
Reverse a given string.
```

```text
Solve the classic two sum problem.
```

```text
Check if a word is a palindrome.
```

```text
Compute the nth Fibonacci number.
```

```text
Implement binary search on a sorted list.
```

```text
Check whether parentheses and brackets are balanced.
```

---

# 🔬 Example Execution

For a request such as:

```text
Write a function to check if a number is prime.
```

The system performs:

```text
User Request
     ↓
PlanningAgent
     ↓
ReasoningAgent
     ↓
Prime Template Selection
     ↓
LogicAgent
     ↓
Code Execution
     ↓
Test Cases
     ↓
PatternAgent
     ↓
CriticAgent
     ↓
VerifierAgent
     ↓
Verified Result
```

The execution trace records the activities performed by the agents.

---

# 🎯 Project Objectives

The primary objectives of this project are:

1. Demonstrate the principles of **Agentic AI** using specialized agents.
2. Explore different **multi-agent orchestration architectures**.
3. Decompose coding tasks into independent responsibilities.
4. Execute generated solutions against real test cases.
5. Introduce automated critique and independent verification.
6. Provide transparency through an agent execution trace.
7. Compare different approaches to coordinating specialized agents.

---

# 🌟 Key Features

### Multi-Agent Design

Seven agents collaborate instead of relying on a single monolithic workflow.

### Multiple Architectures

The same task can be processed using seven different orchestration patterns.

### Real Execution

Solutions are actually executed against test cases.

### Independent Verification

The final result is independently checked before being marked as verified.

### Transparent Workflow

The execution trace shows the actions performed by each agent.

### Graceful Failure Handling

Requests that do not match the supported coding templates can be identified as unresolved instead of producing an unsupported solution.

---

# ⚠️ Current Limitations

This project intentionally uses a **curated template library and deterministic Python logic** rather than a paid or external LLM API.

Therefore:

* The solver currently supports a predefined set of coding problem types.
* Natural-language reasoning is implemented through keyword-based template matching.
* It is not intended to replace a general-purpose AI coding assistant.
* New coding problems require additional templates and test cases.

These constraints make the project reproducible without requiring external model APIs.

---

# 🔮 Future Enhancements

Potential future improvements include:

* Integrating an open-source or hosted LLM
* Supporting a larger coding-problem library
* Dynamic code generation for previously unseen problems
* Adding Python, Java, C++, and JavaScript execution
* Adding sandboxed code execution
* Automatic test-case generation
* Persistent agent memory
* Agent performance comparison
* Execution-time and complexity analysis
* Human feedback integration
* More advanced multi-agent negotiation strategies

---

# 📊 Agentic AI Concepts Demonstrated

This project demonstrates several important Agentic AI concepts:

```text
Specialized Agents
       +
Task Decomposition
       +
Planning
       +
Reasoning
       +
Tool / Code Execution
       +
Parallel Processing
       +
Agent Collaboration
       +
Critique
       +
Supervision
       +
Independent Verification
```

---

# 🏆 Why This Project?

Traditional coding systems often follow a simple:

```text
Input → Generate → Output
```

This project demonstrates a more structured approach:

```text
Input
  ↓
Plan
  ↓
Reason
  ↓
Generate
  ↓
Execute
  ↓
Analyse
  ↓
Critique
  ↓
Verify
  ↓
Final Result
```

The project therefore provides a practical demonstration of how **multi-agent workflows can divide responsibilities, coordinate tasks, validate results, and improve reliability through verification**.

---

# 📜 License

This project is licensed under the MIT License.

---

# 👨‍💻 Author

**Raghul P.**

B.Tech Information Technology
Kongu Engineering College

---

## ⭐ If you find this project useful

Consider giving the repository a ⭐ on GitHub.
