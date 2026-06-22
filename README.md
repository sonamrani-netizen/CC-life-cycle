graph TD
    %% Phase 1: Application & Data Gathering
    Start((Start:<br>Customer Applies)) --> Docs["Submit Documents<br>- Name<br>- Address<br>- Income Details<br>- SSN"]
    Docs --> BankRec["Bank Receives & Reviews Application"]
    
    BankRec --> DataSources{"Gather Customer Data"}
    DataSources --> D1["Data Provided During Application"]
    DataSources --> D2["Credit Bureaus Data<br>(TransUnion, Equifax, Experian, etc.)"]
    DataSources --> D3["Internal Bank Data<br>(Prior relationships, if any)"]
    
    D1 & D2 & D3 --> Phase1
    
    %% Phase 2: Risk Assessment
    subgraph Risk Assessment Phase
        Phase1["1. Policy Threshold & KPI Evaluation<br>(Automatic filtering before advanced modeling)"]
        
        Phase1 --> CH["Credit History KPIs<br>• Credit Score: Benchmarked against historical data<br>• Missed Payments: Frequency correlates to higher risk<br>• Default History: Multiple failures = high risk<br>• Number of Enquiries: Recent hard inquiries (credit hungriness)<br>• Vintage: Length of credit relationship (longer = stable)<br>• Delinquency Rate: Rollover into higher past-due buckets<br>• NPA Ratio: Non-Performing Asset critical risk level"]
        
        Phase1 --> DB["Debt Burden & Income KPIs<br>• Debt Burden: DTI ratio, monthly EMIs, utilization ratios (avoid overleveraging)<br>• Income: Verified steady cash flow"]
        
        CH & DB --> Gate1{"Pass Initial Policy Thresholds?"}
        
        Gate1 -- Yes --> Phase2["2. Advanced Risk Modeling<br>(Machine learning & statistical models)"]
        Phase2 --> RM["Risk Models<br>(e.g., Application Scorecard)"]
        RM --> PD["Calculate Probability of Default (PD)<br>Statistical likelihood customer will fail to repay"]
    end
    
    Gate1 -- No --> Reject((Reject Application))
    
    %% Phase 3: Financial Viability
    PD --> Phase3
    
    subgraph Financial Viability: Revenue & Profitability
        Phase3["Shift from Risk Assessment to Financial Modeling"] --> Step1
        
        Step1["Step 1: Determine APR & Credit Limit<br>• Credit Limit: Based on Income, Debt Burden, Risk Tier<br>• APR Pricing: Risk-based pricing via PD & Credit Score"]
        
        Step1 --> Step2["Step 2: Calculate Expected Revenue<br>Formula: (Limit × Expected Utilization × APR) + Fees"]
        
        Step2 --> Step3["Step 3: Net Risk-Adjusted Revenue (NRAR) & Profitability<br>• NRAR = Expected Revenue - Expected Loss (driven by PD)<br>• Expected Profitability = NRAR - Operating Costs"]
    end
    
    Step3 --> Step4
    
    %% Phase 4: Decisioning
    subgraph The Approval Decision
        Step4{"Step 4: Evaluate Against Hurdle Rate<br>(Internal target profit margin)"}
        
        Step4 -- "Below Hurdle Rate" --> Counter["Counter-Offer Routed<br>Lower credit limit or higher APR to force profitability"]
        Step4 -- "Above Hurdle Rate" --> Approve((Approve Application:<br>Offer Formal Limit & APR))
    end
    
    %% Loops & Endings
    Counter -. "Re-evaluate profitability" .-> Step1
    Approve --> Step5["3. For Approved Applications...<br>(Proceed to Issuance & Onboarding)"]
