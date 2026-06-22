
    %% Initial Application
    Start([Customer Applies for Credit Card]) --> SubDocs[Submit Documents:\nName, Address, Income, SSN]
    SubDocs --> BankRec[Bank Receives Application]
    
    %% Data Gathering
    subgraph DataSources [Data Sources]
        DS1(Application Data)
        DS2(Credit Bureaus\nTransUnion, Equifax, etc.)
        DS3(Internal Bank Data)
    end
    BankRec -.-> DataSources
    BankRec --> RA1

    %% Risk Assessment Phase
    subgraph RiskAssessment [Risk Assessment Phase]
        direction TB
        RA1[1. Policy Threshold & KPI Evaluation]
        RA1_Detail[\KPIs: Credit Score, Missed Payments, Vintage, etc.\nDebt Burden: DTI, Income\]
        RA1 --- RA1_Detail
        RA1 --> PassPolicy{Clears Initial\nThresholds?}

        PassPolicy -->|Yes| RA2[2. Advanced Risk Modeling]
        RA2 --> RA2_Detail[\Risk Models & Scorecards\nOutput: Probability of Default - PD\]
        RA2 --- RA2_Detail
        RA2 --> PassRisk{Passes Risk\nThresholds?}
    end

    %% Rejection Path
    PassPolicy -->|No| Reject([Reject Application])
    PassRisk -->|No| Reject

    %% Financial Viability Phase
    PassRisk -->|Yes| FinV1

    subgraph FinViability [Financial Viability: Revenue & Profitability]
        direction TB
        FinV1[Step 1: Determine APR & Credit Limit\nBased on Income, Debt, Risk Tier & PD]
        FinV2[Step 2: Calculate Expected Revenue\nLimit x Utilization x APR + Fees]
        FinV3[Step 3: Calculate NRAR & Profitability\nNRAR = Expected Rev - Expected Loss\nProfit = NRAR - Costs]

        FinV1 --> FinV2 --> FinV3
    end

    %% Final Decision Path
    FinV3 --> Decision{Step 4: Final Decision\nIs Expected Profitability\n>= Hurdle Rate?}

    Decision -->|Above Hurdle Rate| Approve([Approved!\nOffer Limit & APR])
    Decision -->|Below Hurdle Rate| CounterOffer[Counter-offer:\nAdjust to Lower Limit or Higher APR]

    %% Feedback Loop for Counter-offer
    CounterOffer -.->|Recalculate Viability| FinV1

    %% Styling
    classDef startEnd fill:#d4edda,stroke:#28a745,stroke-width:2px,color:#155724;
    classDef reject fill:#f8d7da,stroke:#dc3545,stroke-width:2px,color:#721c24;
    classDef decision fill:#fff3cd,stroke:#ffc107,stroke-width:2px,color:#856404;
    
    class Start,Approve startEnd;
    class Reject reject;
    class PassPolicy,PassRisk,Decision decision;
