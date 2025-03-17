# Automated Smart Contract Security Scanner

In the world of blockchain, smart contracts are crucial but their immutability poses risks if they contain vulnerabilities. Imagine deploying a contract with a re-entrancy flaw, leading to significant losses. Such incidents highlight the need for robust security.

The Automated Smart Contract Security Scanner addresses this by providing automated, comprehensive analysis of Solidity contracts. It detects vulnerabilities like re-entrancy and integer overflow, offering detailed remediation suggestions. With on-chain bytecode verification, it ensures deployed contracts match the analyzed code.

This tool empowers developers and auditors, enhancing trust and reliability in decentralized applications.

## Overview

The Automated Smart Contract Security Scanner is built to help users:

- Automatically scan Solidity code for known vulnerabilities using static analysis.
- Generate detailed reports with vulnerability type, severity, and remediation suggestions.
- Integrate with blockchain networks for on-chain bytecode verification.
- Provide a modular and scalable design for future enhancements.

## Documentation

The project is currently documented with the following core documents:

- **[Project Requirements Document](/docs/requirements.md)**: Outlines the functional and non-functional requirements of the scanner.
- **[Threat Model and Security Analysis Document](/docs/threatModel_and_securityAnalysis.md)**: Details potential threats, risk assessments, and mitigation strategies.
- **[Architecture Documentation](/docs/architecture.md)**: Describes the high-level system architecture, module breakdown, and data flow.
- **[Detailed Technical Design Document](/docs/detailedTechnicalDesign.md)**: Provides in-depth technical details on module implementations, key algorithms, and integration points.

> **Note**: Testing & Deployment documentation, as well as User and Developer Guides, will be added later as the project matures.

## Features

- **Automated Analysis**: Analyze Solidity smart contracts to detect vulnerabilities automatically.
- **User-Friendly Dashboard**: Visualize results with interactive charts, tables, and detailed code snippets.
- **On-Chain Verification**: Fetch and compare deployed bytecode for integrity verification.
- **Modular Architecture**: Easily extend the system to incorporate additional checks and support more blockchains.

## Tech Stack

- **Frontend**: React (or Next.js), Chart.js for visualization, Prism.js for code highlighting.
- **Backend**: Python with Flask for API endpoints.
- **Analysis Engine**: Python interfacing with the Solidity compiler (solc) for AST generation and vulnerability scanning.
- **Blockchain Integration**: Web3.py for Ethereum interactions.
- **Data Storage**: JSON for initial vulnerability signature storage (potential to move to SQLite).

## Usage

- **Uploading Code**: Use the dashboard to upload your Solidity contracts either via file upload or a code editor.
- **Scanning**: The analysis engine will parse and scan the code, then generate a vulnerability report.
- **On-Chain Verification**: Enter a contract address to trigger on-chain bytecode retrieval and comparison.

## Future Enhancements

- Extend vulnerability detection to cover additional smart contract issues.
- Integrate continuous testing and deployment pipelines.
- Improve scalability and performance optimizations.
- Develop comprehensive User and Developer Guides.
- Support additional blockchain platforms beyond Ethereum.
