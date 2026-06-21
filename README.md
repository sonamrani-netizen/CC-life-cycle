```mermaid
flowchart TD
    %% 1. DATA INGESTION
    APP([Customer Application]) --> INGEST[Data Collection Service]
    INGEST --> DATA[Compile: App Docs, Bureau Data, Internal History]

    %% 2. KPI CALCULATION
    DATA --> KPI_EVAL[Calculate Core KPIs]
    
    subgraph Applicant Key Performance Indicators
        KPI_EVAL --> K_HIST[Credit History KPIs:<br>Score, Missed Payments, Defaults,<br>Enquiries, Vintage, Delinquency, NPA]
        KPI_EVAL --> K_DEBT[Debt & Capacity KPIs:<br>Debt-to-Income, EMIs, Utilization]
    end

    %% 3. GATE 1: POLICY THRESHOLD
    K_HIST & K_DEBT --> GATE1{Gate 1: Policy Thresholds<br>Do KPIs meet minimum criteria?}
    
    GATE1 -->|Fails Policy Limits| REJ([Auto-Reject Application])
    
    %% 4. ADVANCED RISK MODELING
    GATE1 -->|Passes Criteria| ML[Advanced Risk Modeling]
    
    subgraph Machine Learning Layer
        ML --> SCORE[Application Scorecard Engine]
        SCORE --> PD[Calculate Probability of Default]
    end
    
    %% 5. GATE 2: MODEL THRESHOLD
    PD --> GATE2{Gate 2: Model Threshold<br>Is PD within acceptable risk limit?}
    
    GATE2 -->|Exceeds Maximum PD| REJ
    
    %% 6. FINANCIAL VIABILITY
    GATE2 -->|Passes Model Criteria| FIN[Start Financial Viability Engine]
    
    subgraph Unit Economics Modeling
        FIN --> S1[Step 1: Assign Capacity & Pricing<br>Determine Credit Limit & APR]
        S1 --> S2[Step 2: Forecast Expected Revenue<br>Projected Utilization + Interest + Fees]
        S2 --> S3["Step 3: Calculate NRAR & Net Profit<br>NRAR = Exp. Revenue - Exp. Loss<br>Net Profit = NRAR - Op. Costs"]
    end

    %% 7. GATE 3: FINAL DECISION
    S3 --> DECIDE{Gate 3: Profitability Hurdle<br>Expected Profit >= Target Margin?}
    
    DECIDE -->|Yes: Meets Target| APPROVE([Approve & Issue Credit Card])
    DECIDE -->|No: Below Target| REJ2([Reject / Route to Counter-Offer])
