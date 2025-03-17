# Architecture

## 1. Overview

The goal of this project is to create an automated tool that scans Solidity smart contracts for known vulnerabilities and presents the analysis via a user-friendly dashboard. The system is designed to be modular, allowing easy integration of additional vulnerability checks or blockchain features in the future.

## 2. System Architecture Diagram

```
                    +---------------------+
                    |   User Interface    |
                    | (Web Dashboard/UI)  |
                    +----------+----------+
                               |
                               v
                    +----------+----------+
                    |   Backend API Layer  |  <-- Handles communication
                    +----------+----------+
                               |
              +----------------+-----------------+
              |                                  |
              v                                  v

    +------------------+ +-----------------------+
    | Input Module     | | Blockchain Module     |
    | (Code Upload &   | | (On-Chain Verification|
    | Code Editor)     | | and Bytecode Fetch)   |
    +--------+---------+ +-----------+-----------+
             |                         |
             v                         |
    +------------------------+         |
    | Analysis Engine        |         |
    | (AST Generation &      | <--------
    | Vulnerability Checks)  |
    +------------------------+
                               |
                               v
                    +------------------------+
                    | Vulnerability Database |
                    | (Pattern/Signature     |
                    | Repository)            |
                    +------------------------+
```

## 3. Module Breakdown

### 3.1 Input Module

- **Function:**
  - Receives Solidity code from users either through file uploads or an integrated code editor.
- **Responsibilities:**
  - Validate input files (file type, size).
  - Pre-process code for analysis.
- **Integration Points:**
  - Communicates directly with the Analysis Engine.
  - Interfaces with the Backend API to trigger analysis.

### 3.2 Analysis Engine

- **Function:**
  - Processes Solidity code by generating an Abstract Syntax Tree (AST) using the Solidity compiler (solc).
  - Performs vulnerability detection by comparing code patterns against known vulnerability signatures.
- **Responsibilities:**
  - Parsing code, running static analysis, and generating detailed vulnerability reports.
- **Integration Points:**
  - Receives sanitized code from the Input Module.
  - Sends analysis results to the Backend API for display in the UI.
  - Optionally queries the Vulnerability Database for known patterns.

### 3.3 Vulnerability Database

- **Function:**
  - Stores definitions and signatures of common smart contract vulnerabilities (e.g., re-entrancy, integer overflow).
- **Responsibilities:**
  - Provide quick lookup for the Analysis Engine during vulnerability detection.
- **Integration Points:**
  - Directly accessed by the Analysis Engine.

### 3.4 UI Dashboard

- **Function:**
  - Presents vulnerability findings and detailed reports in a user-friendly format.
- **Responsibilities:**
  - Visualization of analysis results (charts, tables, code snippets).
  - Provides interactive elements like drill-down details and manual triggers for on-chain verification.
- **Integration Points:**
  - Fetches data via the Backend API.
  - Sends user requests (e.g., contract verification) to the Blockchain Module.

### 3.5 Blockchain Integration Module

- **Function:**
  - Interacts with blockchain networks to fetch deployed contract bytecode.
  - Verifies on-chain code against the analyzed Solidity code.
- **Responsibilities:**
  - Handle API calls to Ethereum nodes (via Web3.js/Web3.py).
  - Compare and validate on-chain bytecode integrity.
- **Integration Points:**
  - Works in conjunction with the Backend API and UI for on-demand verification requests.

### 3.6 Backend API Layer

- **Function:**
  - Acts as the communication bridge between the frontend (UI) and the backend modules (Input, Analysis, Blockchain).
- **Responsibilities:**
  - Handle API requests/responses.
  - Manage session control, error handling, and logging.
- **Integration Points:**
  - Exposes endpoints for code uploads, analysis result retrieval, and blockchain verification triggers.
  - Routes requests to the appropriate internal modules.

## 4. Data Flow

1. **User Interaction:**
   - A user uploads Solidity code via the UI.
2. **Input Module Processing:**
   - The uploaded code is validated and pre-processed.
3. **Analysis:**
   - The processed code is passed to the Analysis Engine, which generates an AST and performs vulnerability checks.
   - The Analysis Engine may query the Vulnerability Database to match known patterns.
4. **Result Delivery:**
   - Analysis results are sent back to the Backend API, which formats the data.
   - The UI Dashboard retrieves and displays the findings.
5. **On-Chain Verification:**
   - Upon user request, the Blockchain Module fetches on-chain bytecode for a given contract.
   - A comparison report is generated and sent to the UI for display.

## 5. Technology Stack

- **Frontend/UI:**
  - Framework: React or Next.js
  - Libraries: Charting libraries (Chart.js), Code highlighting (Prism.js).
- **Backend/API:**
  - Language: Python (with Flask).
  - Communication: RESTful API design.
- **Analysis Engine:**
  - Language: Python or JavaScript.
  - Tools: Solidity compiler (solc), existing static analysis libraries (e.g., Slither).
- **Blockchain Module:**
  - Libraries: Web3.py (Python).
- **Data Storage (Optional):**
  - A simple database (e.g., SQLite, MongoDB) for logging analysis results, user sessions, or vulnerability signatures.

## 6. Integration & Communication

- **Internal Communication:**
  - The Backend API serves as the central hub, orchestrating requests between the UI, Analysis Engine, and Blockchain Module.
- **External Communication:**
  - The Blockchain Module interacts with Ethereum nodes via secure API calls.
  - All communication is secured via HTTPS and follows industry best practices for data encryption and integrity.

## 7. Security Considerations

- **Input Validation:**
  - Every input (code, API calls) must be sanitized to prevent injection attacks.
- **Secure Communication:**
  - Use HTTPS for all API interactions.
- **Error Handling & Logging:**
  - Ensure that error messages do not reveal sensitive system details.
- **Access Control:**
  - Implement authentication and authorization for accessing sensitive API endpoints.

## 8. Scalability and Maintenance

- **Modular Design:**
  - The separation of components (Input, Analysis, UI, Blockchain) allows the project to scale or upgrade individual modules without affecting the entire system.
- **Future Enhancements:**
  - Easily integrate additional vulnerability checks or support for multiple blockchain networks.
- **Documentation & Code Reviews:**
  - Maintain updated documentation and conduct regular code reviews to ensure system integrity.
