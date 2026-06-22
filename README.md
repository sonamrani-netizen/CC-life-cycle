graph TD
    %% Phase 1: Application and Data Gathering
    subgraph Phase1 [Phase 1: Application and Data Gathering]
        A[Customer Applies for Credit Card] --> B["Submit Documents: Name, Address, Income, SSN"]
        B --> C[Bank Receives Application]
        C --> D{Gather Data Sources}
        D --> D1[(Application Data)]
        D --> D2[("Credit Bureaus (TransUnion, Equifax)")]
        D --> D3[(Internal Bank Data)]
    end

    %% Phase 2: Risk Assessment
    subgraph Phase2 [Phase 2: Risk Assessment and Modeling]
        D1 --> E[1. Policy Threshold and KPI Evaluation]
        D2 --> E
        D3 --> E
        
        E --> E1["Credit History: Score, Missed, Defaults, Enquiries, Vintage"]
        E --> E2["Debt Burden: DTI, EMIs, Utilization, Cash Flow"]
        
        E1 --> F{Clears Initial Thresholds?}
        E2 --> F
        
        F -- "No" --> Z[Reject Application]
        
        F -- "Yes" --> G[2. Advanced Risk Modeling]
        G --> G1["Calculate Scorecard and PD (Probability of Default)"]
        
        G1 --> H{Passes Risk Models?}
        H -- "No" --> Z
    end

    %% Phase 3: Financial Viability
    subgraph Phase3 [Phase 3: Financial Viability and Decision]
        H -- "Yes" --> I[Step 1: Determine Terms]
        I --> I1[Assign Credit Limit via Income/Debt]
        I --> I2[Assign APR via Risk-Based PD Pricing]
        
        I1 --> J["Step 2: Expected Revenue (Limit x Utilization x APR + Fees)"]
        I2 --> J
        
        J --> K[Step 3: Calculate Profitability]
        K --> K1["NRAR = Expected Revenue - Expected Loss"]
        K1 --> K2["Expected Profitability = NRAR - Operating Costs"]
        
        K2 --> L{Meets Hurdle Rate?}
        
        L -- "Yes" --> M["APPROVE: Offer Limit and APR"]
        L -- "No" --> N["COUNTER-OFFER: Lower Limit or Higher APR"]
        N -. "Re-evaluate" .-> J
    end
    
    %% Styling safely explicitly mapped for Dark/Light mode overrides
    classDef reject fill:#ffe6e6,stroke:#ff0000,stroke-width:2px,color:#990000;
    classDef approve fill:#e6ffe6,stroke:#008000,stroke-width:2px,color:#006600;
    class Z reject;
    class M approve;
