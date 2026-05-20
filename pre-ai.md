```mermaid
graph TD
    %% Define Nodes and Layers
    subgraph "Silo 1: SCHEDULED SCANNING (Reactive/Periodic)"
        ScannerA[Network Vulnerability Scanner] -->|"Trigger Schedule (e.g., Weekly)"| AssetDB[Static Asset Inventory]
        ScannerB["App/API Security Tester (DAST/SAST)"] -->|"Daily/Weekly Build"| SourceCode[Code Repository]
    end

    subgraph "Silo 2: MANUAL TRIAGE (Human-Centric)"
        ScannerA -.->|"Unfiltered Raw Scan Data"| ReportDB[(Raw Vulnerability DB)]
        ScannerB -.->|"Unfiltered Raw Scan Data"| ReportDB

        ReportDB ==>|"Bulk PDF/CSV Data"| AnalystTriage["Security Analyst (Tier 1/2)"]
        AnalystTriage ==>|"Manual Correlation & Suppression"| ValidatedFindings[(Validated Findings DB)]
        RiskDB[(External Threat Intelligence)] -.->|"Static Context"| AnalystTriage
    end

    subgraph "Silo 3: PRIORITIZATION & TICKET MANAGEMENT"
        ValidatedFindings ==>|"CVSS Base Score Only"| PrioritizationEngine{Prioritization Logic}
        BusinessDB[(Business Asset Priority)] -.->|"Static Input"| PrioritizationEngine
        PrioritizationEngine ==>|"Ranked Fix List"| TicketSystem[IT Service Management / Jira]
    end

    subgraph "Silo 4: REMEDIATION (The Patch Gap)"
        TicketSystem ==>|"Fix Ticket"| ITOps[IT Operations Team]
        ITOps ==>|"Test & Schedule Patch"| ProductionSys[(Production Systems)]
    end

    %% Apply Styles
    style ScannerA fill:#f9f,stroke:#333,stroke-width:1px
    style ScannerB fill:#f9f,stroke:#333,stroke-width:1px
    style ReportDB fill:#eee,stroke:#999,stroke-width:1px
    style ValidatedFindings fill:#eee,stroke:#999,stroke-width:1px
    style AnalystTriage fill:#ff9,stroke:#333,stroke-width:2px,stroke-dasharray: 5 5
    style PrioritizationEngine fill:#ff9,stroke:#333,stroke-width:2px
    style TicketSystem fill:#dfd,stroke:#333,stroke-width:1px
    style ITOps fill:#dfd,stroke:#333,stroke-width:1px
