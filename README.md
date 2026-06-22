``` mermaid
flowchart TD
    %%-----------------------------------------
    %% Phase 1: Application Intake Phase
    %%-----------------------------------------
    subgraph Phase_1 ["1. Application Intake Phase"]
        direction TB
        A["Customer Submits Application<br/><b>Captured Data:</b> Name, Address, Income details, SSN"]
        B["Bank Receives Application<br/><b>Data Aggregation (Ingestion from 3 Sources):</b><br/>1. Application Data: Direct from customer<br/>2. Credit Bureau Data: Pulled from TransUnion, Equifax, Experian<br/>3. Internal Bank Data: Prior footprints, active relationships"]
        
        A --> B
    end

    %%-----------------------------------------
    %% Phase 2: Risk Assessment Phase
    %%-----------------------------------------
    subgraph Phase_2 ["2. Risk Assessment Phase (Automated Filtering)"]
        direction TB
        C["Policy Threshold & KPI Evaluation"]
        C_Hist["<b>Credit History Evaluation:</b><br/>• Credit Score: Benchmarked against historical data<br/>• Missed Payments: Frequency = risk profile<br/>• Default History: Multiple defaults = high-risk<br/>• Number of Enquiries: Monitors 'credit hungriness'<br/>• Vintage: Length of credit (longer = lower risk)<br/>• Delinquency Rate: Historical roll-overs (e.g., 30-60 DPD)<br/>• NPA Ratio: Measures critical risk level"]
        C_Debt["<b>Debt Burden & Income Evaluation:</b><br/>• Debt Burden: DTI ratio, monthly EMIs, credit utilization<br/>• Income: Verified for steady debt-servicing cash flow"]
        
        B --> C
        C --- C_Hist
        C_Hist --- C_Debt
    end

    %%-----------------------------------------
    %% Phase 3: Advanced Risk Modeling Phase
    %%-----------------------------------------
    subgraph Phase_3 ["3. Advanced Risk Modeling Phase"]
        direction TB
        D["Advanced Risk Modeling Engine<br/>• <b>Risk Models:</b> Internal ML/statistical models calculate custom score<br/>• <b>Output:</b> Calculates Probability of Default (PD) over specific timeframe"]
        
        E{"Risk Threshold Pass?"}
        F(["Application Rejected<br/>(Adverse action codes generated for regulatory disclosure)"])
        
        C_Debt --> D
        D --> E
        E -- "No" --> F
    end

    %%-----------------------------------------
    %% Phase 4: Financial Viability Phase
    %%-----------------------------------------
    subgraph Phase_4 ["4. Financial Viability Phase (Revenue & Profitability)"]
        direction TB
        G["Step 1: Determine APR & Credit Limit<br/>• <b>Credit Limit:</b> Based on Income, Debt Burden, internal risk tier<br/><i>Rule: Higher income + lower debt = higher limit</i><br/>• <b>APR Pricing:</b> Risk-based using PD & Credit Score<br/><i>Rule: Lower-risk = lower APR | Higher-risk = higher APR</i>"]
        
        H["Step 2: Calculate Expected Revenue<br/>• <b>Forecast Logic:</b> Assigned Credit Limit × Expected Utilization = Predicted Revolving Balance<br/>• <b>Calculation:</b> (Predicted Balance × APR) + Annual/Transactional Fees"]
        
        I["Step 3: Calculate Net Risk-Adjusted Revenue & Profitability<br/>• <b>NRAR</b> = Expected Revenue - Expected Loss (Driven by PD)<br/>• <b>Expected Profitability</b> = NRAR - Operating Costs"]
        
        E -- "Yes" --> G
        G --> H
        H --> I
    end

    %%-----------------------------------------
    %% Phase 5: Final Approval Decision Phase
    %%-----------------------------------------
    subgraph Phase_5 ["5. Final Approval Decision Phase"]
        direction TB
        J{"Expected Profitability ≥<br/>Internal Hurdle Rate?"}
        K["Application Approved<br/>Formally offer calculated Credit Limit and APR to customer"]
        L(["Move to Approved Applications Workflow"])
        M["Route for Counter-Offer<br/>Adjust variables (lower credit limit or higher APR) to force passing profitability"]
        
        I --> J
        J -- "Case A: Yes (Above Hurdle)" --> K
        K --> L
        J -- "Case B: No (Below Hurdle)" --> M
    end

    M -- "Loop back to recalculate profitability metrics" --> G

    %%-----------------------------------------
    %% Phase 6: Onboarding & Card Issuance Phase
    %%-----------------------------------------
    subgraph Phase_6 ["6. Onboarding & Card Issuance Phase"]
        direction TB
        N["KYC & AML Final Verification<br/><b>Actions:</b> Watchlist compliance (PEP, Sanctions) & identity verification<br/><b>KPIs:</b> False Positive Rate, Onboarding Drop-off Rate"]
        O["Core Banking Account Creation<br/><b>Actions:</b> Generate unique PAN, allocate credit line, core ledger setup"]
        P["Physical & Digital Card Issuance<br/><b>Actions:</b> Provision virtual card to digital wallets, print/ship physical card<br/><br/><b>Financial Impact (CAC):</b><br/>Onboarding Cost = KYC Vendor Fees + Card Production & Shipping Cost"]
        
        L --> N
        N --> O
        O --> P
    end

    %%-----------------------------------------
    %% Phase 7: Usage & Portfolio Management Phase
    %%-----------------------------------------
    subgraph Phase_7 ["7. Usage & Portfolio Management Phase (Active Lifecycle)"]
        direction TB
        Q["Active Card Usage & Ongoing Revenue Generation"]
        Q_Rev["<b>Revenue Calculation:</b><br/>Interchange Revenue = Purchase volume x interchange rate<br/>Interest Income (NIM) = Avg. Outstanding Balance X NIM Rate<br/>Fee Income<br/>Total Revenue = Interchange Revenue + Interest Income + Fee Income"]
        Q_Prof["<b>Profitability Calculation:</b><br/>Cost = Cost of Funds (CoF) + Rewards & Loyalty Expense + operational costs<br/>Profit = Total Revenue - Costs"]
        
        R["Continuous Behavioral Scoring Engine<br/><b>Logic:</b> ML models track transactions, utilization, payment velocity dynamically<br/><b>KPIs:</b> Activation Rate (30/60/90 Days), Revolver Rate, Utilization Rate, Share of Wallet (SoW)"]
        
        S{"Portfolio Actions Decision Fork"}
        T(["Case A: Credit Limit Increase (CLI)<br/>Trigger: Optimal Behavioral Score, high/safe utilization"])
        U(["Case B: Credit Limit Decrease (CLD) or Account Block<br/>Trigger: Early warning indicators (maxing limits, paying minimums)"])
        V(["Case C: Retention & Cross-Sell<br/>Trigger: Low usage, high-value targeted with balance transfers/loans"])
        
        P --> Q
        Q --- Q_Rev
        Q_Rev --- Q_Prof
        Q_Prof --> R
        R --> S
        S --> T
        S --> U
        S --> V
    end

    %%-----------------------------------------
    %% Phase 8: Delinquency & Collections Phase
    %%-----------------------------------------
    subgraph Phase_8 ["8. Delinquency & Collections Phase"]
        direction TB
        DelinqTrigger(["Account Trigger: Fails to pay Minimum Amount Due (MAD) by due date"])
        W["Early-Stage Collections (1 to 30 DPD - Bucket 1)<br/><b>Strategy:</b> Soft reminders (SMS, email, IVR) for customer convenience<br/><b>Financial Impact:</b> Loss Provisioning begins (IFRS 9 / CECL)"]
        X["Mid-Stage Collections (31 to 90 DPD - Buckets 2 & 3)<br/><b>Strategy:</b> Direct human outreach, card temporarily blocked<br/><b>KPIs:</b> Roll Rates, Cure Rate, Right Party Connect (RPC) Rate"]
        Y["Late-Stage Collections (91 to 180 DPD)<br/><b>Strategy:</b> Aggressive negotiation, restructure plans, settlement waivers<br/><b>Financial Impact:</b> Classified as Non-Performing Asset (NPA)"]
        
        Q_Prof -.-> DelinqTrigger
        DelinqTrigger --> W
        W --> X
        X --> Y
    end

    %%-----------------------------------------
    %% Phase 9: Charge-Off & Recovery Phase
    %%-----------------------------------------
    subgraph Phase_9 ["9. Charge-Off & Recovery Phase"]
        direction TB
        UncollectTrigger(["Trigger: Reaches 180 DPD without a successful cure"])
        Z["Charge-Off & Technical Write-Off<br/><b>Action:</b> Bank writes off outstanding principal balance as bad debt loss<br/><b>Impact:</b> Net Profitability Impact = - (Gross Charge-Off Balance + Operational Collection Expenses)"]
        
        AA{"Recovery Strategy Decision Fork"}
        AB(["Internal/External Agency Recovery<br/>Outsource to 3rd-party debt collectors (keeps 15–30% of recovered funds)"])
        AC(["Debt Sale<br/>Sell toxic asset bundle to distressed debt buyers (4 to 12 cents per dollar)"])
        AD(["Legal Action (Litigation)<br/>Reserved for high-balance accounts to legally garnish verifiable assets/income"])
        
        AE["Ultimate Lifecycle End-State Metrics"]
        AE_Rec["<b>Recovery Rate (%)</b> =<br/>(Total Recovered Funds + Debt Sale Proceeds) / Gross Charge-Off Balance"]
        AE_NCO["<b>NCO Ratio (%)</b> =<br/>(Gross Charge-Offs - Recoveries) / Average Total Outstanding Portfolio Balance"]
        
        Y -.-> UncollectTrigger
        UncollectTrigger --> Z
        Z --> AA
        AA --> AB
        AA --> AC
        AA --> AD
        
        AB --> AE
        AC --> AE
        AD --> AE
        AE --- AE_Rec
        AE_Rec --- AE_NCO
    end

    %% Styling configurations for visual distinction
    classDef reject fill:#ffcdd2,stroke:#d32f2f,stroke-width:2px;
    classDef approve fill:#c8e6c9,stroke:#388e3c,stroke-width:2px;
    classDef loop fill:#fff9c4,stroke:#fbc02d,stroke-width:2px;
    classDef alert fill:#ffe0b2,stroke:#f57c00,stroke-width:2px;
    classDef metrics fill:#e1bee7,stroke:#8e24aa,stroke-width:2px;

    class F reject;
    class L approve;
    class M loop;
    class DelinqTrigger,UncollectTrigger alert;
    class AE,AE_Rec,AE_NCO metrics;
