```mermaid
flowchart TD
    %% Data Ingestion Stage
    APP([Customer Application]) --> INGEST[Data Collection]
    INGEST --> D1[App Docs: Name, Address, Income, SSN]
    INGEST --> D2[Credit Bureaus: TransUnion, Equifax, Experian]
    INGEST --> D3[Internal Bank Data: Prior History]

    %% Risk Assessment Stage
    D1 --> GATE1{1. Policy Thresholds}
    D2 --> GATE1
    D3 --> GATE1

    GATE1 -->|Fails Policy Limits| REJ([Reject Application])
    GATE1 -->|Passes Thresholds| ML[2. Advanced Risk Modeling]
    
    ML -->|Application Scorecard| PD[Calculate Probability of Default]

    %% Financial Viability Stage
    PD --> S1[Step 1: Determine APR & Credit Limit]
    S1 --> S2[Step 2: Calculate Expected Revenue]
    S2 --> S3[Step 3: Calculate NRAR & Profitability]

    %% Final Decision
    S3 --> DECIDE{Step 4: Expected Profit > Hurdle Rate?}
    DECIDE -->|No| REJ2([Reject / Counter-Offer])
    DECIDE -->|Yes| APPROVE([Approve & Issue Card])
