```mermaid
flowchart TD
    %% 1. DATA INGESTION
    subgraph 1. Data Ingestion Phase
        APP([Customer Application]) --> INGEST[Data Collection Service]
        INGEST --> D1[Application Docs<br>- Name<br>- Address<br>- Verified Income<br>- SSN]
        INGEST --> D2[External Credit Bureaus<br>- TransUnion<br>- Equifax<br>- Experian]
        INGEST --> D3[Internal Bank Data<br>- Prior Banking Accounts<br>- Historical Balances]
    end

    %% 2. STAGE 1 GATE
    D1 & D2 & D3 --> GATE1{Stage 1:<br>Policy Threshold Filter}

    %% 3. POLICY & KPI EVALUATION
    subgraph 2. Policy Threshold & KPI Evaluation
        GATE1 -->|Passes Initial Screen| KPI_HIST[Credit History Evaluation]
        GATE1 -->|Passes Initial Screen| KPI_DEBT[Debt Burden & Income Verification]

        subgraph Credit History KPIs
            KPI_HIST --> K1[Credit Score Benchmark]
            KPI_HIST --> K2[Missed Payments Frequency]
            KPI_HIST --> K3[Historical Loan Defaults]
            KPI_HIST --> K4[No. of Recent Enquiries]
            KPI_HIST --> K5[Credit Relationship Vintage]
            KPI_HIST --> K6[Delinquency Rate Bucket Migration]
            KPI_HIST --> K7[Non-Performing Asset Ratio]
        end

        subgraph Debt & Cash Flow KPIs
            KPI_DEBT --> K8[Debt-to-Income Ratio]
            KPI_DEBT --> K9[Existing Monthly EMIs]
            KPI_DEBT --> K10[Credit Utilization Ratios]
        end
    end

    %% 4. ADVANCED RISK MODELING
    K1 & K2 & K3 & K4 & K5 & K6 & K7 & K8 & K9 & K10 --> ML[3. Advanced Risk Modeling]
    
    subgraph Machine Learning Layer
        ML --> SCORE[Application Scorecard Engine]
        SCORE --> PD[Calculate Probability of Default]
    end

    %% TRIPPERS FOR REJECTION
    GATE1 -->|Fails Policy Limits| REJ([Application Rejected])
    
    %% 5. FINANCIAL VIABILITY
    subgraph 4. Financial Viability Engine
        PD --> S1[Step 1: Assign Capacity & Pricing<br>- Credit Limit Assignment<br>- Risk-Based APR Pricing]
        S1 --> S2[Step 2: Forecast Expected Revenue<br>- Balance Utilization Projection<br>- Interest Income + Fees]
        S2 --> S3["Step 3: Calculate NRAR & Net Profit<br>NRAR = Expected Revenue - Expected Loss<br>Net Profit = NRAR - Operating Costs"]
    end

    %% 6. FINAL DECISION
    S3 --> DECIDE{Step 4: Decision Gate<br>Expected Profit >= Hurdle Rate?}
    
    DECIDE -->|Yes: Meets Profit Target| APPROVE([Approve & Issue Credit Card])
    DECIDE -->|No: Below Target Margin| REJ2([Reject / Route to Counter-Offer])
