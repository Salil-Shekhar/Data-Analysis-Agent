README: Expert Data Analysis Agent
Overview
This project implements an intelligent Data Analysis Agent powered by Large Language Models (LLMs). The agent uses a tool-calling architecture to interact with a Python environment, allowing it to perform real-time data processing, statistical analysis, and visual storytelling on CSV datasets.

Tech Stack
Orchestration: LangGraph (Stateful workflows)

LLM Framework: LangChain

Monitoring: LangFuse (Observability and tracing)

Compute Tool: Python REPL (for code execution)

Libraries: Pandas, Matplotlib, Seaborn, Pydantic

Key Features
Dynamic Dataset Loading: A custom tool to load CSV files directly into the agent's memory.

Autonomous Code Execution: Integration with PythonAstREPLTool to perform calculations and data manipulations.

Visual Intelligence: The agent can generate complex charts (Bar, Line, etc.) and provide human-readable explanations of the trends.

Safety Guardrails: Includes a prompt_guardrails function that blocks dangerous operations like file system manipulation or network requests.

State Management: Uses a custom AnalystAgent state to track message history and dataset status.

Getting Started
Install Dependencies:

Bash
pip install langfuse langchain-openai langgraph pandas matplotlib seaborn
Configure API Keys: Set your LangFuse and OpenRouter/OpenAI keys in the environment variables within the notebook.

Run the Graph: The system is built as a StateGraph. Invoke the graph with a natural language query like "Load dataset.csv and show me the correlation between features."

File Description: Agents.ipynb
The notebook is structured into several functional blocks that build a stateful AI agent:

1. Environment & Imports
The initial cells handle the importation of necessary LangChain and LangGraph components, as well as the configuration of LangFuse for tracing agent performance.

2. Tool Definition
Two primary tools are defined for the agent:

python_repl: Allows the LLM to write and execute Python code snippet.

load_dataset: Specifically designed to read CSV files into a global DataFrame, returning the shape and column names to the agent so it knows what data it is working with.

3. Agent Logic & Guardrails
System Prompt: Defines the agent's persona as an "Expert Data Analysis Agent," instructing it on professional tone, visualization requirements, and termination triggers (e.g., saying "ANALYSIS_COMPLETE").

Guardrails: A safety layer that checks user input against a list of blocked commands (e.g., "Delete dataset", "Run system command") to prevent malicious usage.

4. Graph Construction
The agent follows a circular workflow:

Agent Node: Processes the current state and decides whether to call a tool or respond to the user.

Tool Node: Executes the requested tools (like loading data or running code).

Conditional Routing: Uses a should_continue function to determine if the loop should continue or if the analysis is finished.

5. Execution Example
The notebook contains an execution trace where a user asks to load a Heart_Disease_Prediction.csv dataset. The agent demonstrates its ability to identify column types, map categorical data to numeric values, and respond to specific analysis requests.
