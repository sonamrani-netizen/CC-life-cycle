graph TD
    subgraph Phase 1 - Application and Data
        A[Customer Applies] --> B[Submit Documents: Name, Address, Income, SSN]
        B --> C[Bank Receives Application]
        C --> D{Gather Data}
        D --> D1[Application Data]
        D --> D2[Credit Bureaus: TransUnion / Equifax]
        D --> D3[Internal Bank Data]
    end

    subgraph Phase 2 - Risk Assessment
        D1 --> E[1. Policy Threshold Evaluation]
        D2 --> E
        D3 --> E
        
        E --> E1[Credit Check: Score, Missed, Defaults, Enquiries, Vintage]
        E --> E2[Debt Burden: DTI, EMIs, Utilization, Cash Flow]
        
        E1 --> F{Clears Initial Thresholds?}
        E2 --> F
        
        F -- No --> Z[REJECT APPLICATION]
        
        F -- Yes --> G[2. Advanced Risk Modeling]
        G --> G1[Calculate Scorecard and PD - Probability of Default]
        
        G1 --> H{Passes Risk Models?}
        H -- No --> Z
    end

    subgraph Phase 3 - Financial Viability
        H -- Yes --> I[Step 1: Determine Terms]
        I --> I1[Assign Credit Limit]
        I --> I2[Assign APR]
        
        I1 --> J[Step 2: Expected Revenue Calculation]
        I2 --> J
        
        J --> K[Step 3: Calculate Profitability]
        K --> K1[NRAR = Expected Revenue minus Expected Loss]
        K1 --> K2[Profitability = NRAR minus Operating Costs]
        
        K2 --> L{Meets Hurdle Rate?}
        
        L -- Yes --> M[APPROVE: Offer Limit and APR]
        L -- No --> N[COUNTER OFFER: Lower Limit or Higher APR]
        N -.->|Re-evaluate| J
    end
