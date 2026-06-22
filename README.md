```mermaid
graph TD
    subgraph P1 [Phase 1: Application Data]
        A[Customer Applies] --> B[Submit Documents]
        B --> C[Bank Receives Application]
        C --> D{Gather Data}
        D --> D1[Application Data]
        D --> D2[Credit Bureaus]
        D --> D3[Internal Bank Data]
    end

    subgraph P2 [Phase 2: Risk Assessment]
        D1 --> E[Policy Threshold Evaluation]
        D2 --> E
        D3 --> E
        E --> E1[Credit Check]
        E --> E2[Debt Burden Check]
        E1 --> F{Clears Thresholds?}
        E2 --> F
        F -- No --> Z[REJECT APPLICATION]
        F -- Yes --> G[Advanced Risk Modeling]
        G --> G1[Calculate Scorecard and PD]
        G1 --> H{Passes Models?}
        H -- No --> Z
    end

    subgraph P3 [Phase 3: Financial Viability]
        H -- Yes --> I[Determine Terms]
        I --> I1[Assign Credit Limit]
        I --> I2[Assign APR]
        I1 --> J[Expected Revenue Calculation]
        I2 --> J
        J --> K[Calculate Profitability]
        K --> K1[Expected Revenue minus Expected Loss]
        K1 --> K2[NRAR minus Operating Costs]
        K2 --> L{Meets Hurdle Rate?}
        L -- Yes --> M[APPROVE APPLICATION]
        L -- No --> N[COUNTER OFFER]
        N -.-> J
    end
