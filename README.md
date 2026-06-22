graph TD
    %% Phase 1: Application & Data Gathering
    subgraph Phase 1: Application & Data Gathering
        A[Customer Applies for Credit Card] --> B[Submit Documents:<br/>Name, Address, Income, SSN]
        B --> C[Bank Receives Application]
        C --> D{Gather Data Sources}
        D --> D1[(Application Data)]
        D --> D2[(Credit Bureaus Data<br/>TransUnion, Equifax, etc.)]
        D --> D3[(Internal Bank Data)]
    end

    %% Phase 2: Risk Assessment
    subgraph Phase 2: Risk Assessment & Modeling
        D1 & D2 & D3 --> E[1. Policy Threshold & KPI Evaluation]
        E --> E1[Credit History:<br/>Score, Missed Payments, Defaults,<br/>Enquiries, Vintage, Delinquency, NPA]
        E --> E2[Debt Burden & Income:<br/>DTI, EMIs, Utilization, Cash Flow]
        
        E1 & E2 --> F{Clears Initial<br/>Thresholds?}
        F -- No --> Z[Reject Application]
        
        F -- Yes --> G[2. Advanced Risk Modeling]
        G --> G1[Calculate Scorecard &<br/>Probability of Default - PD]
        
        G1 --> H{Passes Risk<br/>Models?}
        H -- No --> Z
    end

    %% Phase 3: Financial Viability
    subgraph Phase 3: Financial Viability & Decision
        H -- Yes --> I[Step 1: Determine Terms]
        I --> I1[Assign Credit Limit<br/>Based on Income/Debt]
        I --> I2[Assign APR<br/>Risk-Based Pricing via PD]
        
        I1 & I2 --> J[Step 2: Calculate Expected Revenue<br/>Limit x Utilization x APR + Fees]
        
        J --> K[Step 3: Calculate Profitability]
        K --> K1[NRAR = Expected Revenue - Expected Loss]
        K1 --> K2[Expected Profitability = NRAR - Operating Costs]
        
        K2 --> L{Step 4: Meets<br/>Hurdle Rate?}
        
        L -- Yes --> M[Approve Application:<br/>Offer Limit & APR]
        L -- No --> N[Generate Counter-Offer:<br/>Lower Limit or Higher APR]
        N -. Re-evaluate .- J
    end
    
    %% Styling
    classDef reject fill:#ffe6e6,stroke:#ff0000,stroke-width:2px;
    classDef approve fill:#e6ffe6,stroke:#008000,stroke-width:2px;
    class Z reject;
    class M approve;
