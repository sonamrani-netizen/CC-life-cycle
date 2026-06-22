``` mermaid
flowchart TD
    %%-----------------------------------------
    %% Phase 1: Application Intake Phase
    %%-----------------------------------------
    subgraph Phase_1 ["1. Application Intake Phase"]
        direction TB
        A["Customer Submits<br/>Application"]
        A1["<b>Captured Data:</b><br/>Name, Address,<br/>Income details, SSN"]
        A --- A1

        B["Bank Receives<br/>Application"]
        B1["<b>Data Aggregation</b><br/>(Ingestion from<br/>3 Sources):"]
        B2["1. App Data:<br/>Direct from<br/>customer"]
        B3["2. Bureau Data:<br/>Pulled from TransUnion,<br/>Equifax, Experian"]
        B4["3. Internal Data:<br/>Prior footprints,<br/>active relationships"]
        B --- B1 --- B2 --- B3 --- B4
        
        A1 --> B
    end

    %%-----------------------------------------
    %% Phase 2: Risk Assessment Phase
    %%-----------------------------------------
    subgraph Phase_2 ["2. Risk Assessment Phase (Automated Filtering)"]
        direction TB
        C["Policy Threshold<br/>& KPI<br/>Evaluation"]
        
        C_H1["<b>Credit History<br/>Evaluation:</b>"]
        C_H2["• Credit Score:<br/>Benchmarked against<br/>historical data"]
        C_H3["• Missed Payments:<br/>Frequency =<br/>risk profile"]
        C_H4["• Default History:<br/>Multiple defaults<br/>= high-risk"]
        C_H5["• Num of Enquiries:<br/>Monitors<br/>'credit hungriness'"]
        C_H6["• Vintage:<br/>Length of credit<br/>(longer = lower risk)"]
        C_H7["• Delinquency Rate:<br/>Historical roll-overs<br/>(e.g., 30-60 DPD)"]
        C_H8["• NPA Ratio:<br/>Measures critical<br/>risk level"]
        
        C_D1["<b>Debt Burden &<br/>Income Evaluation:</b>"]
        C_D2["• Debt Burden:<br/>DTI ratio, EMIs,<br/>credit utilization"]
        C_D3["• Income:<br/>Verified for steady<br/>debt-servicing cash flow"]
        
        C --- C_H1 --- C_H2 --- C_H3 --- C_H4 --- C_H5 --- C_H6 --- C_H7 --- C_H8
        C_H8 --- C_D1 --- C_D2 --- C_D3
        
        B4 --> C
    end

    %%-----------------------------------------
    %% Phase 3: Advanced Risk Modeling Phase
    %%-----------------------------------------
    subgraph Phase_3 ["3. Advanced Risk Modeling Phase"]
        direction TB
        D["Advanced Risk<br/>Modeling<br/>Engine"]
        D1["• <b>Risk Models:</b><br/>Internal ML models<br/>calculate custom score"]
        D2["• <b>Output:</b><br/>Calculates Prob of<br/>Default (PD) timeframe"]
        D --- D1 --- D2
        
        E{"Risk Threshold<br/>Pass?"}
        
        F(["Application<br/>Rejected"])
        F1(["(Adverse action codes<br/>generated for<br/>regulatory disclosure)"])
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
        G["Step 1:<br/>Determine APR &<br/>Credit Limit"]
        G1["• <b>Credit Limit:</b><br/>Based on Income, Debt<br/>Burden, risk tier"]
        G2["<i>Rule: Higher income<br/>+ lower debt<br/>= higher limit</i>"]
        G3["• <b>APR Pricing:</b><br/>Risk-based using<br/>PD & Credit Score"]
        G4["<i>Rule: Lower-risk<br/>= lower APR | Higher<br/>-risk = higher APR</i>"]
        G --- G1 --- G2 --- G3 --- G4
        
        H["Step 2:<br/>Calculate Expected<br/>Revenue"]
        H1["• <b>Forecast Logic:</b><br/>Credit Limit × Utilization<br/>= Predicted Balance"]
        H2["• <b>Calculation:</b><br/>(Pred Balance × APR)<br/>+ Annual/Txn Fees"]
        H --- H1 --- H2
        
        I["Step 3:<br/>Calculate Net Risk-Adj<br/>Revenue & Profitability"]
        I1["• <b>NRAR</b> =<br/>Expected Revenue -<br/>Expected Loss (PD)"]
        I2["• <b>Expected<br/>Profitability</b> =<br/>NRAR - Opex"]
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
        J{"Expected Profit<br/>≥ Internal<br/>Hurdle Rate?"}
        
        K["Application<br/>Approved"]
        K1["Formally offer<br/>calculated Credit Limit<br/>and APR to customer"]
        K --- K1
        
        L(["Move to Approved<br/>Applications<br/>Workflow"])
        
        M["Route for<br/>Counter-Offer"]
        M1["Adjust variables<br/>(lower limit or higher APR)<br/>to pass profitability"]
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
        N["KYC & AML<br/>Final<br/>Verification"]
        N1["<b>Actions:</b> Watchlist<br/>compliance (PEP, Sanctions)<br/>& identity verification"]
        N2["<b>KPIs:</b> False<br/>Positive Rate,<br/>Onboarding Drop-off"]
        N --- N1 --- N2
        
        O["Core Banking<br/>Account<br/>Creation"]
        O1["<b>Actions:</b> Generate<br/>unique PAN, allocate<br/>credit line, ledger setup"]
        O --- O1
        
        P["Physical & Digital<br/>Card<br/>Issuance"]
        P1["<b>Actions:</b> Provision<br/>virtual card to wallets,<br/>print/ship physical card"]
        P2["<b>Financial<br/>Impact (CAC):</b>"]
        P3["Onboarding Cost =<br/>KYC Vendor Fees + Card<br/>Production & Shipping"]
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
        Q["Active Card Usage<br/>& Ongoing<br/>Revenue Gen"]
        Q1["<b>Revenue Calculation:</b>"]
        Q2["Interchange Rev =<br/>Purchase volume<br/>x interchange rate"]
        Q3["Interest Inc (NIM) =<br/>Avg Outstanding Bal<br/>X NIM Rate"]
        Q4["Fee Income"]
        Q5["Total Revenue =<br/>Interchange + Interest<br/>+ Fee Income"]
        
        Q6["<b>Profitability<br/>Calculation:</b>"]
        Q7["Cost = Cost of Funds<br/>+ Rewards Exp<br/>+ operational costs"]
        Q8["Profit =<br/>Total Revenue<br/>- Costs"]
        
        Q --- Q1 --- Q2 --- Q3 --- Q4 --- Q5 --- Q6 --- Q7 --- Q8
        
        R["Continuous<br/>Behavioral<br/>Scoring Engine"]
        R1["<b>Logic:</b> ML models track<br/>txns, utilization,<br/>payment velocity"]
        R2["<b>KPIs:</b> Activation Rate,<br/>Revolver Rate,<br/>Utilization Rate, SoW"]
        R --- R1 --- R2
        
        S{"Portfolio Actions<br/>Decision<br/>Fork"}
        
        T(["Case A: Credit<br/>Limit Increase<br/>(CLI)"])
        T1(["Trigger: Optimal<br/>Behavioral Score,<br/>high/safe utilization"])
        T --- T1
        
        U(["Case B: Credit<br/>Limit Decrease (CLD)<br/>or Account Block"])
        U1(["Trigger: Early<br/>warning indicators<br/>(maxing limits, min pay)"])
        U --- U1
        
        V(["Case C:<br/>Retention &<br/>Cross-Sell"])
        V1(["Trigger: Low usage,<br/>high-value targeted with<br/>balance transfers/loans"])
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
        DelinqTrigger(["Account Trigger:<br/>Fails to pay MAD<br/>by due date"])
        
        W["Early-Stage<br/>Collections<br/>(1-30 DPD - B1)"]
        W1["<b>Strategy:</b> Soft<br/>reminders (SMS/email)<br/>for convenience"]
        W2["<b>Financial Impact:</b><br/>Loss Provisioning begins<br/>(IFRS 9 / CECL)"]
        W --- W1 --- W2
        
        X["Mid-Stage<br/>Collections<br/>(31-90 DPD - B2/3)"]
        X1["<b>Strategy:</b> Direct<br/>human outreach,<br/>card temp blocked"]
        X2["<b>KPIs:</b> Roll Rates,<br/>Cure Rate, Right Party<br/>Connect (RPC) Rate"]
        X --- X1 --- X2
        
        Y["Late-Stage<br/>Collections<br/>(91-180 DPD)"]
        Y1["<b>Strategy:</b> Aggressive<br/>negotiation, restructure,<br/>settlement waivers"]
        Y2["<b>Financial Impact:</b><br/>Classified as Non-<br/>Performing Asset (NPA)"]
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
        UncollectTrigger(["Trigger: Reaches<br/>180 DPD without<br/>a successful cure"])
        
        Z["Charge-Off &<br/>Technical<br/>Write-Off"]
        Z1["<b>Action:</b> Bank writes<br/>off outstanding principal<br/>as bad debt loss"]
        Z2["<b>Impact:</b> Net Profit =<br/>- (Gross Charge-Off +<br/>Operational Coll Exp)"]
        Z --- Z1 --- Z2
        
        AA{"Recovery<br/>Strategy<br/>Decision Fork"}
        
        AB(["Internal/External<br/>Agency<br/>Recovery"])
        AB1(["Outsource to 3rd-<br/>party collectors<br/>(keeps 15–30%)"])
        AB --- AB1
        
        AC(["Debt<br/>Sale"])
        AC1(["Sell toxic bundle<br/>to distressed debt buyers<br/>(4-12 cents per $)"])
        AC --- AC1
        
        AD(["Legal Action<br/>(Litigation)"])
        AD1(["Reserved for high-<br/>balance accounts to<br/>garnish assets/income"])
        AD --- AD1
        
        AE["Ultimate Lifecycle<br/>End-State<br/>Metrics"]
        AE1["• <b>Recovery Rate</b> =<br/>(Total Recov + Sale)<br/>/ Gross Charge-Off"]
        AE2["• <b>NCO Ratio (%)</b> =<br/>(Charge-Offs - Recov)<br/>/ Avg Total Outstanding"]
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
