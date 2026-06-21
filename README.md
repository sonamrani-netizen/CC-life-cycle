# Credit Card Underwriting & Customer Lifecycle Engine

This repository defines the decision logic, data ingestion pipeline, and financial valuation sequence for automated credit card application processing.

## System Flowchart

```mermaid
flowchart TD
    %% 1. INGESTION
    APP([Customer Application]) --> INGEST[Data Ingestion Service]
    
    INGEST --> D1[App Form: Name, Address, Income, SSN]
    INGEST --> D2[Bureaus: TransUnion, Equifax, Experian]
    INGEST --> D3[Internal DB: Prior Banking History]

    D1 --> GATE1{Stage 1: Risk Gate}
    D2 --> GATE1
    D3 --> GATE1

    subgraph Risk Assessment KPIs
        GATE1 --> KPI1[Missed Payments]
        GATE1 --> KPI2[Default History]
        GATE1 --> KPI3[No. of Enquiries]
        GATE1 --> KPI4[Vintage]
        GATE1 --> KPI5[Delinquency Rate]
        GATE1 --> KPI6[NPA Ratio]
        GATE1 --> KPI7[Debt Burden]
    end

    KPI1 --> ML[ML Scorecard / PD Engine]
    KPI2 --> ML
    KPI3 --> ML
    KPI4 --> ML
    KPI5 --> ML
    KPI6 --> ML
    KPI7 --> ML

    ML --> THRESH{Passes Risk Threshold?}
    THRESH -->|No| REJ([Auto-Reject Application])

    THRESH -->|Yes| FIN{Stage 2: Financial Viability Engine}

    subgraph Value Modeling
        FIN --> S1[Step 1: Assign Limit & APR]
        S1 --> S2[Step 2: Forecast Expected Revenue]
        S2 --> S3[Step 3: Calculate NRAR & Profitability]
    end

    S3 --> DECIDE{Net Profit > Target?}
    DECIDE -->|No| REJ
    DECIDE -->|Yes| ISSUE([Approve & Provision Card])
