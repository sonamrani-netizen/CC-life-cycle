``` mermaid
flowchart TD
    %%-----------------------------------------
    %% Phase 1: Application Intake Phase
    %%-----------------------------------------
    subgraph Phase_1 ["1. Application Intake Phase"]
        direction TB
        A["Customer Submits Application"]
        A1["<b>Captured Data:</b> Name, Address,<br/>Income details, SSN"]
        A --- A1

        B["Bank Receives Application"]
        B1["<b>Data Aggregation (Ingestion from 3 Sources):</b>"]
        B2["1. Application Data: Direct from customer"]
        B3["2. Credit Bureau Data: Pulled from<br/>TransUnion, Equifax, Experian"]
        B4["3. Internal Bank Data: Prior footprints,<br/>active relationships"]
        B --- B1 --- B2 --- B3 --- B4
        
        A1 --> B
    end

    %%-----------------------------------------
    %% Phase 2: Risk Assessment Phase
    %%-----------------------------------------
    subgraph Phase_2 ["2. Risk Assessment Phase (Automated Filtering)"]
        direction TB
        C["Policy Threshold & KPI Evaluation"]
        
        C_H1["<b>Credit History Evaluation:</b>"]
        C_H2["• Credit Score: Benchmarked against<br/>historical data"]
        C_H3["• Missed Payments: Frequency = risk profile"]
        C_H4["• Default History: Multiple defaults = high-risk"]
        C_H5["• Number of Enquiries: Monitors<br/>'credit hungriness'"]
        C_H6["• Vintage: Length of credit<br/>(longer = lower risk)"]
        C_H7["• Delinquency Rate: Historical roll-overs<br/>(e.g., 30-60 DPD)"]
        C_H8["• NPA Ratio: Measures critical risk level"]
        
        C_D1["<b>Debt Burden & Income Evaluation:</b>"]
        C_D2["• Debt Burden: DTI ratio, monthly EMIs,<br/>credit utilization"]
        C_D3["• Income: Verified for steady<br/>debt-servicing cash flow"]
        
        C --- C_H1 --- C_H2 --- C_H3 --- C_H4 --- C_H5 --- C_H6 --- C_H7 --- C_H8
        C_H8 --- C_D1 --- C_D2 --- C_D3
        
        B4 --> C
    end

    %%-----------------------------------------
    %% Phase 3: Advanced Risk Modeling Phase
    %%-----------------------------------------
    subgraph Phase_3 ["3. Advanced Risk Modeling Phase"]
        direction TB
        D["Advanced Risk Modeling Engine"]
        D1["• <b>Risk Models:</b> Internal ML/statistical models<br/>calculate custom score"]
        D2["• <b>Output:</b> Calculates Probability of Default (PD)<br/>over specific timeframe"]
        D --- D1 --- D2
        
        E{"Risk Threshold Pass?"}
        
        F(["Application Rejected"])
        F1(["(Adverse action codes generated<br/>for regulatory disclosure)"])
        F --- F1
        
        C_D3 --> D
        D2 --> E
        E -- "No" --> F
    end

    %%-----------------------------------------
    %% Phase 4: Financial Viability Phase
    %%-----------------------------------------
    subgraph Phase_4 ["4. Financial Viability Phase (Revenue & Profitability)"]
        direction TB
        G["Step 1: Determine APR & Credit Limit"]
        G1["• <b>Credit Limit:</b> Based on Income,<br/>Debt Burden, internal risk tier"]
        G2["<i>Rule: Higher income + lower debt<br/>= higher limit</i>"]
        G3["• <b>APR Pricing:</b> Risk-based using<br/>PD & Credit Score"]
        G4["<i>Rule: Lower-risk = lower APR |<br/>Higher-risk = higher APR</i>"]
        G --- G1 --- G2 --- G3 --- G4
        
        H["Step 2: Calculate Expected Revenue"]
        H1["• <b>Forecast Logic:</b> Credit Limit ×<br/>Expected Utilization = Predicted Balance"]
        H2["• <b>Calculation:</b> (Predicted Balance × APR)<br/>+ Annual/Transactional Fees"]
        H --- H1 --- H2
        
        I["Step 3: Calculate Net Risk-Adjusted Revenue<br/>& Profitability"]
        I1["• <b>NRAR</b> = Expected Revenue -<br/>Expected Loss (Driven by PD)"]
        I2["• <b>Expected Profitability</b> =<br/>NRAR - Operating Costs"]
        I --- I1 --- I2
        
        E -- "Yes" --> G
        G4 --> H
        H2 --> I
    end

    %%-----------------------------------------
    %% Phase 5: Final Approval Decision Phase
    %%-----------------------------------------
    subgraph Phase_5 ["5. Final Approval Decision Phase"]
        direction TB
        J{"Expected Profitability ≥<br/>Internal Hurdle Rate?"}
        
        K["Application Approved"]
        K1["Formally offer calculated Credit Limit<br/>and APR to customer"]
        K --- K1
        
        L(["Move to Approved Applications Workflow"])
        
        M["Route for Counter-Offer"]
        M1["Adjust variables (lower credit limit or<br/>higher APR) to force passing profitability"]
        M --- M1
        
        I2 --> J
        J -- "Case A: Yes (Above Hurdle)" --> K
        K1 --> L
        J -- "Case B: No (Below Hurdle)" --> M
    end

    M1 -- "Loop back to recalculate profitability metrics" --> G

    %%-----------------------------------------
    %% Phase 6: Onboarding & Card Issuance Phase
    %%-----------------------------------------
    subgraph Phase_6 ["6. Onboarding & Card Issuance Phase"]
        direction TB
        N["KYC & AML Final Verification"]
        N1["<b>Actions:</b> Watchlist compliance (PEP, Sanctions)<br/>& identity verification"]
        N2["<b>KPIs:</b> False Positive Rate,<br/>Onboarding Drop-off Rate"]
        N --- N1 --- N2
        
        O["Core Banking Account Creation"]
        O1["<b>Actions:</b> Generate unique PAN,<br/>allocate credit line, core ledger setup"]
        O --- O1
        
        P["Physical & Digital Card Issuance"]
        P1["<b>Actions:</b> Provision virtual card to digital<br/>wallets, print/ship physical card"]
        P2["<b>Financial Impact (CAC):</b>"]
        P3["Onboarding Cost = KYC Vendor Fees +<br/>Card Production & Shipping Cost"]
        P --- P1 --- P2 --- P3
        
        L --> N
        N2 --> O
        O1 --> P
    end

    %%-----------------------------------------
    %% Phase 7: Usage & Portfolio Management Phase
    %%-----------------------------------------
    subgraph Phase_7 ["7. Usage & Portfolio Management Phase (Active Lifecycle)"]
        direction TB
        Q["Active Card Usage & Ongoing Revenue Generation"]
        Q1["<b>Revenue Calculation:</b>"]
        Q2["Interchange Revenue = Purchase volume<br/>x interchange rate"]
        Q3["Interest Income (NIM) = Avg. Outstanding<br/>Balance X NIM Rate"]
        Q4["Fee Income"]
        Q5["Total Revenue = Interchange Revenue +<br/>Interest Income + Fee Income"]
        
        Q6["<b>Profitability Calculation:</b>"]
        Q7["Cost = Cost of Funds (CoF) + Rewards &<br/>Loyalty Expense + operational costs"]
        Q8["Profit = Total Revenue - Costs"]
        
        Q --- Q1 --- Q2 --- Q3 --- Q4 --- Q5 --- Q6 --- Q7 --- Q8
        
        R["Continuous Behavioral Scoring Engine"]
        R1["<b>Logic:</b> ML models track transactions,<br/>utilization, payment velocity dynamically"]
        R2["<b>KPIs:</b> Activation Rate (30/60/90 Days),<br/>Revolver Rate, Utilization Rate, SoW"]
        R --- R1 --- R2
        
        S{"Portfolio Actions Decision Fork"}
        
        T(["Case A: Credit Limit Increase (CLI)"])
        T1(["Trigger: Optimal Behavioral Score,<br/>high/safe utilization"])
        T --- T1
        
        U(["Case B: Credit Limit Decrease (CLD)<br/>or Account Block"])
        U1(["Trigger: Early warning indicators<br/>(maxing limits, paying minimums)"])
        U --- U1
        
        V(["Case C: Retention & Cross-Sell"])
        V1(["Trigger: Low usage, high-value targeted<br/>with balance transfers/loans"])
        V --- V1
        
        P3 --> Q
        Q8 --> R
        R2 --> S
        S --> T
        S --> U
        S --> V
    end

    %%-----------------------------------------
    %% Phase 8: Delinquency & Collections Phase
    %%-----------------------------------------
    subgraph Phase_8 ["8. Delinquency & Collections Phase"]
        direction TB
        DelinqTrigger(["Account Trigger: Fails to pay<br/>Minimum Amount Due (MAD) by due date"])
        
        W["Early-Stage Collections<br/>(1 to 30 DPD - Bucket 1)"]
        W1["<b>Strategy:</b> Soft reminders (SMS, email, IVR)<br/>for customer convenience"]
        W2["<b>Financial Impact:</b> Loss Provisioning<br/>begins (IFRS 9 / CECL)"]
        W --- W1 --- W2
        
        X["Mid-Stage Collections<br/>(31 to 90 DPD - Buckets 2 & 3)"]
        X1["<b>Strategy:</b> Direct human outreach,<br/>card temporarily blocked"]
        X2["<b>KPIs:</b> Roll Rates, Cure Rate,<br/>Right Party Connect (RPC) Rate"]
        X --- X1 --- X2
        
        Y["Late-Stage Collections (91 to 180 DPD)"]
        Y1["<b>Strategy:</b> Aggressive negotiation, restructure<br/>plans, settlement waivers"]
        Y2["<b>Financial Impact:</b> Classified as<br/>Non-Performing Asset (NPA)"]
        Y --- Y1 --- Y2
        
        Q8 -.-> DelinqTrigger
        DelinqTrigger --> W
        W2 --> X
        X2 --> Y
    end

    %%-----------------------------------------
    %% Phase 9: Charge-Off & Recovery Phase
    %%-----------------------------------------
    subgraph Phase_9 ["9. Charge-Off & Recovery Phase"]
        direction TB
        UncollectTrigger(["Trigger: Reaches 180 DPD<br/>without a successful cure"])
        
        Z["Charge-Off & Technical Write-Off"]
        Z1["<b>Action:</b> Bank writes off outstanding<br/>principal balance as bad debt loss"]
        Z2["<b>Impact:</b> Net Profitability Impact = - (Gross Charge-Off<br/>Balance + Operational Collection Expenses)"]
        Z --- Z1 --- Z2
        
        AA{"Recovery Strategy Decision Fork"}
        
        AB(["Internal/External Agency Recovery"])
        AB1(["Outsource to 3rd-party debt collectors<br/>(keeps 15–30% of recovered funds)"])
        AB --- AB1
        
        AC(["Debt Sale"])
        AC1(["Sell toxic asset bundle to distressed debt<br/>buyers (4 to 12 cents per dollar)"])
        AC --- AC1
        
        AD(["Legal Action (Litigation)"])
        AD1(["Reserved for high-balance accounts to<br/>legally garnish verifiable assets/income"])
        AD --- AD1
        
        AE["Ultimate Lifecycle End-State Metrics"]
        AE1["• <b>Recovery Rate (%)</b> =<br/>(Total Recovered Funds + Debt Sale Proceeds)<br/>/ Gross Charge-Off Balance"]
        AE2["• <b>NCO Ratio (%)</b> =<br/>(Gross Charge-Offs - Recoveries)<br/>/ Average Total Outstanding Portfolio Balance"]
        AE --- AE1 --- AE2
        
        Y2 -.-> UncollectTrigger
        UncollectTrigger --> Z
        Z2 --> AA
        AA --> AB
        AA --> AC
        AA --> AD
        
        AB1 --> AE
        AC1 --> AE
        AD1 --> AE
    end

    %% Styling configurations for visual distinction
    classDef reject fill:#ffcdd2,stroke:#d32f2f,stroke-width:2px;
    classDef approve fill:#c8e6c9,stroke:#388e3c,stroke-width:2px;
    classDef loop fill:#fff9c4,stroke:#fbc02d,stroke-width:2px;
    classDef alert fill:#ffe0b2,stroke:#f57c00,stroke-width:2px;
    classDef metrics fill:#e1bee7,stroke:#8e24aa,stroke-width:2px;
    classDef no_bg fill:none,stroke:none;

    class F,F1 reject;
    class L approve;
    class M,M1 loop;
    class DelinqTrigger,UncollectTrigger alert;
    class AE,AE1,AE2 metrics;
