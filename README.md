Done! I’ve scrubbed all those `` tags for you. The text is now clean, citation-free, and ready for your README.

---

# NDTwin Intent-to-Action Test Case Dataset README

## 1. Dataset Overview
This dataset is developed for the testing and evaluation of the Intent-to-Action Translation within the NDTwin platform. NDTwin utilizes a Network Digital Twin to mirror real-time network states, enabling administrators to manage infrastructure through natural language objectives. The dataset serves as a benchmark to validate the ability of Large Language Models (LLMs) to classify intent complexity, extract necessary parameters, and map intents to structured actions.

---

## 2. Directory Structure

*   **intent-to-action classification test set**: Contains data used to evaluate the **SVM intent classifier**, which determines the processing path.
*   **intent-to-action mapping test set**: Contains conversational data used to verify the accuracy of the final translation into executable API calls.

---

## 3. Data Format and Specifications

### Classification Test Set (`intents.json`)
Data in this set is used to test the system's ability to distinguish between operation complexities:
*   **Label 0 (Atomic Intent)**: Represents single-step operations (e.g., "Enable switch s1"). These are intended for local **Edge LLMs** to achieve sub-second translation latency.
*   **Label 1 (Multi-action Intent)**: Represents multi-ation intent (e.g., "Identify the bottleneck and reroute traffic"). These require **Cloud LLM** reasoning.

### Mapping Test Set (`Atomic action.json`, `Multi-action.json`)
Each test case follows a structured JSON conversation format involving three roles:
*   **system**: Defines the environment constraints, available NDT APIs (e.g., `GetPacketLossRate`), and some instructions.
*   **human**: The natural language input provided by the network administrator.
*   **gpt**: The ground-truth output, which includes the operational `state` (discussion or answer), the `valid` status (0 or 1), a technical `explanation`, and the resulting array of `tasks`.

---

## 4. Test Case Categories
The dataset covers a comprehensive range of network administration operations:
*   **Administrative States**: Managing device availability via `Enable` and `Disable` commands.
*   **Hardware Power Management**: Controlling device power cycles, including `Turn on`, `Power off`, and `Reboot`.
*   **Configuration Management**: Managing device nicknames, configuration backups, and firmware updates.
*   **OpenFlow Rule Management**: Installing, modifying, or deleting flow entries and group entries.
*   **Network Telemetry**: Querying real-time performance metrics such as CPU utilization, link bandwidth, latency, and packet loss.
*   **Topology Exploration**: Identifying network paths, listing hosts, and mapping device capabilities.