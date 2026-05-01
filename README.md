# NDTwin Intent-to-Action Test Case Dataset README

## 1. Dataset Overview
This dataset is developed for the testing and evaluation of the Intent-to-Action Translation within the NDTwin platform. NDTwin utilizes a Network Digital Twin to mirror real-time network states, enabling administrators to manage infrastructure through natural language objectives. The dataset serves as a benchmark to validate the ability of Large Language Models (LLMs) to classify intent complexity, extract necessary parameters, and map intents to structured actions.

---

## 2. Evaluation Methodology (Process vs. Result)
To maintain academic rigor and clarify the relationship between the dataset and the reasoning framework described in our paper:

*   **Atomic Intents (Single-step):** For these cases, the `gpt` field represents a direct translation from natural language to a single NDT API call. These are primarily used to evaluate the **Edge LLM's** zero-shot mapping accuracy.
*   **Multi-action Intents (Iterative Reasoning):** For complex intents, the `gpt` field represents the **Golden Standard (Final Goal)**. 
    *   **Note:** Although stored as a single JSON object in this dataset for evaluation purposes, our framework (as described in Sec. III-D of the paper) reaches this state through a Multi-iteration Reasoning and Retrieval process. 
    *   **Purpose:** This set evaluates whether the **Cloud LLM** can eventually synthesize the correct sequence of actions after gathering sufficient context from the NDT through multiple iterations.

---

## 3. Directory Structure

*   **intent-to-action classification test set**: Contains data used to evaluate the **SVM intent classifier**, which determines the processing path (Edge vs. Cloud).
*   **intent-to-action mapping test set**: Contains conversational data used to verify the accuracy of the final translation into executable API calls.

---

## 4. Data Format and Specifications

### Classification Test Set (`intents.json`)
Data in this set is used to test the system's ability to distinguish between operation complexities:
*   **Label 0 (Atomic Intent)**: Represents single-step operations (e.g., "Enable switch s1").
*   **Label 1 (Multi-action Intent)**: Represents multi-action intent (e.g., "Identify the bottleneck and reroute traffic").

### Mapping Test Set (`Atomic action.json`, `Multi-action.json`)
Each test case follows a structured JSON conversation format involving three roles:
*   **system**: Defines environment constraints, available NDT APIs (e.g., `GetPacketLossRate`), and operational rules.
*   **human**: The natural language input provided by the network administrator.
*   **gpt**: The **reference ground-truth** output. For complex tasks, this represents the **final plan** synthesized after the iterative reasoning process.

---

## 5. Test Case Categories
The dataset covers a comprehensive range of network administration operations:
*   **Administrative States**: Managing device availability via `Enable` and `Disable` commands.
*   **Hardware Power Management**: Controlling device power cycles, including `Turn on`, `Power off`, and `Reboot`.
*   **Configuration Management**: Managing device nicknames, configuration backups, and firmware updates.
*   **OpenFlow Rule Management**: Installing, modifying, or deleting flow entries and group entries.
*   **Network Telemetry**: Querying real-time performance metrics such as CPU utilization, link bandwidth, latency, and packet loss.
*   **Topology Exploration**: Identifying network paths, listing hosts, and mapping device capabilities.
