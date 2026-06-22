``` mermaid
flowchart TD
    %%-----------------------------------------
    %% Phase 1: Application Intake Phase
    %%-----------------------------------------
    subgraph Phase_1 ["1. Application Intake Phase"]
        direction TB
        
        subgraph P1_S1 ["Customer Submission"]
            A1["<b>Captured Data:</b><br/>Name, Address,<br/>Income details, SSN"]
        end
        
        subgraph P1_S2 ["Data Aggregation (Ingested from 3 Sources)"]
            B2["1. App Data:<br/>Direct from<br/>customer"]
            B3["2. Bureau Data:<br/>Pulled from TransUnion,<br/>Equifax, Experian"]
            B4["3. Internal Data:<br/>Prior footprints,<br/>active relationships"]
            B2 --- B3 --- B4
        end
        
        A1 --> B2
    end

    %%-----------------------------------------
    %% Phase 2: Risk Assessment Phase
    %%-----------------------------------------
    subgraph Phase_2 ["2. Risk Assessment Phase (Automated Filtering)"]
        direction TB
        C["Policy Threshold<br/>& KPI<br/>Evaluation"]
        
        subgraph P2_S1 ["Credit History Evaluation"]
            C_H2["• Credit Score:<br/>Benchmarked against<br/>historical data"]
            C_H3["• Missed Payments:<br/>Frequency =<br/>risk profile"]
            C_H4["• Default History:<br/>Multiple defaults<br/>= high-risk"]
            C_H5["• Num of Enquiries:<br/>Monitors<br/>'credit hungriness'"]
            C_H6["• Vintage:<br/>Length of credit<br/>(longer = lower risk)"]
            C_H7["• Delinquency Rate:<br/>Historical roll-overs<br/>(e.g., 30-60 DPD)"]
            C_H8["• NPA Ratio:<br/>Measures critical<br/>risk level"]
            C_H2 --- C_H3 --- C_H4 --- C_H5 --- C_H6 --- C_H7 --- C_H8
        end
        
        subgraph P2_S2 ["Debt Burden & Income Evaluation"]
            C_D2["• Debt Burden:<br/>DTI ratio, EMIs,<br/>credit utilization"]
            C_D3["• Income:<br/>Verified for steady<br/>debt-servicing cash flow"]
            C_D2 --- C_D3
        end
        
        C --> C_H2
        C_H8 --- C_D2
    end

    %%-----------------------------------------
    %% Phase 3: Advanced Risk Modeling Phase
    %%-----------------------------------------
    subgraph Phase_3 ["3. Advanced Risk Modeling Phase"]
        direction TB
        
        subgraph P3_S1 ["Advanced Risk Modeling Engine"]
            D1["• <b>Risk Models:</b><br/>Internal ML models<br/>calculate custom score"]
            D2["• <b>Output:</b><br/>Calculates Prob of<br/>Default (PD) timeframe"]
            D1 --- D2
        end
        
        E{"Risk Threshold<br/>Pass?"}
        
        F(["Application<br/>Rejected"])
        F1(["(Adverse action codes<br/>generated for<br/>regulatory disclosure)"])
        F --- F1
        
        D2 --> E
        E -- "No" --> F
    end

    %%-----------------------------------------
    %% Phase 4: Financial Viability Phase
    %%-----------------------------------------
    subgraph Phase_4 ["4. Financial Viability Phase (Revenue & Profitability)"]
        direction TB
        
        subgraph P4_S1 ["Step 1: Determine APR & Credit Limit"]
            G1["• <b>Credit Limit:</b><br/>Based on Income, Debt<br/>Burden, risk tier"]
            G2["<i>Rule: Higher income<br/>+ lower debt<br/>= higher limit</i>"]
            G3["• <b>APR Pricing:</b><br/>Risk-based using<br/>PD & Credit Score"]
            G4["<i>Rule: Lower-risk<br/>= lower APR | Higher<br/>-risk = higher APR</i>"]
            G1 --- G2 --- G3 --- G4
        end
        
        subgraph P4_S2 ["Step 2: Calculate Expected Revenue"]
            H1["• <b>Forecast Logic:</b><br/>Credit Limit × Utilization<br/>= Predicted Balance"]
            H2["• <b>Calculation:</b><br/>(Pred Balance × APR)<br/>+ Annual/Txn Fees"]
            H1 --- H2
        end
        
        subgraph P4_S3 ["Step 3: Calculate Profitability"]
            I1["• <b>NRAR</b> =<br/>Expected Revenue -<br/>Expected Loss (PD)"]
            I2["• <b>Expected<br/>Profitability</b> =<br/>NRAR - Opex"]
            I1 --- I2
        end
        
        G4 --> H1
        H2 --> I1
    end

    %%-----------------------------------------
    %% Phase 5: Final Approval Decision Phase
    %%-----------------------------------------
    subgraph Phase_5 ["5. Final Approval Decision Phase"]
        direction TB
        J{"Expected Profit<br/>≥ Internal<br/>Hurdle Rate?"}
        
        subgraph P5_S1 ["Approval Workflow"]
            K1["Formally offer<br/>calculated Credit Limit<br/>and APR to customer"]
            L(["Move to Approved<br/>Applications<br/>Workflow"])
            K1 --> L
        end
        
        subgraph P5_S2 ["Counter-Offer Route"]
            M1["Adjust variables<br/>(lower limit or higher APR)<br/>to pass profitability"]
        end
        
        J -- "Case A: Yes (Above Hurdle)" --> K1
        J -- "Case B: No (Below Hurdle)" --> M1
    end

    %%-----------------------------------------
    %% Phase 6: Onboarding & Card Issuance Phase
    %%-----------------------------------------
    subgraph Phase_6 ["6. Onboarding & Card Issuance Phase"]
        direction TB
        
        subgraph P6_S1 ["KYC & AML Verification"]
            N1["<b>Actions:</b> Watchlist<br/>compliance (PEP, Sanctions)<br/>& identity verification"]
            N2["<b>KPIs:</b> False<br/>Positive Rate,<br/>Onboarding Drop-off"]
            N1 --- N2
        end
        
        subgraph P6_S2 ["Core Banking Account Creation"]
            O1["<b>Actions:</b> Generate<br/>unique PAN, allocate<br/>credit line, ledger setup"]
        end
        
        subgraph P6_S3 ["Physical & Digital Card Issuance"]
            P1["<b>Actions:</b> Provision<br/>virtual card to wallets,<br/>print/ship physical card"]
            P3["<b>Financial Impact:</b><br/>KYC Vendor Fees + Card<br/>Production & Shipping"]
            P1 --- P3
        end
        
        N2 --> O1
        O1 --> P1
    end

    %%-----------------------------------------
    %% Phase 7: Usage & Portfolio Management Phase
    %%-----------------------------------------
    subgraph Phase_7 ["7. Usage & Portfolio Management Phase"]
        direction TB
        
        subgraph P7_S1 ["Revenue Calculation"]
            Q2["Interchange Rev =<br/>Purchase volume<br/>x interchange rate"]
            Q3["Interest Inc (NIM) =<br/>Avg Outstanding Bal<br/>X NIM Rate"]
            Q5["Total Revenue =<br/>Interchange + Interest<br/>+ Fee Income"]
            Q2 --- Q3 --- Q5
        end
        
        subgraph P7_S2 ["Profitability Calculation"]
            Q7["Cost = Cost of Funds<br/>+ Rewards Exp<br/>+ operational costs"]
            Q8["Profit =<br/>Total Revenue<br/>- Costs"]
            Q7 --- Q8
        end
        
        subgraph P7_S3 ["Continuous Behavioral Scoring"]
            R1["<b>Logic:</b> ML models track<br/>txns, utilization,<br/>payment velocity"]
            R2["<b>KPIs:</b> Activation Rate,<br/>Revolver Rate,<br/>Utilization Rate, SoW"]
            R1 --- R2
        end
        
        subgraph P7_S4 ["Portfolio Actions Decision"]
            S{"Action<br/>Fork"}
            T1(["Case A: CLI<br/>Optimal Score,<br/>high/safe utilization"])
            U1(["Case B: CLD / Block<br/>Early warning indicators<br/>(maxing limits, min pay)"])
            V1(["Case C: Retention<br/>Low usage, high-value<br/>balance transfers/loans"])
            S --> T1
            S --> U1
            S --> V1
        end
        
        Q5 --> Q7
        Q8 --> R1
        R2 --> S
    end

    %%-----------------------------------------
    %% Phase 8: Delinquency & Collections Phase
    %%-----------------------------------------
    subgraph Phase_8 ["8. Delinquency & Collections Phase"]
        direction TB
        DelinqTrigger(["Account Trigger:<br/>Fails to pay MAD<br/>by due date"])
        
        subgraph P8_S1 ["Early-Stage (1-30 DPD)"]
            W1["<b>Strategy:</b> Soft<br/>reminders (SMS/email)<br/>for convenience"]
            W2["<b>Financial Impact:</b><br/>Loss Provisioning begins<br/>(IFRS 9 / CECL)"]
            W1 --- W2
        end
        
        subgraph P8_S2 ["Mid-Stage (31-90 DPD)"]
            X1["<b>Strategy:</b> Direct<br/>human outreach,<br/>card temp blocked"]
            X2["<b>KPIs:</b> Roll Rates,<br/>Cure Rate, Right Party<br/>Connect (RPC) Rate"]
            X1 --- X2
        end
        
        subgraph P8_S3 ["Late-Stage (91-180 DPD)"]
            Y1["<b>Strategy:</b> Aggressive<br/>negotiation, restructure,<br/>settlement waivers"]
            Y2["<b>Financial Impact:</b><br/>Classified as Non-<br/>Performing Asset (NPA)"]
            Y1 --- Y2
        end
        
        DelinqTrigger --> W1
        W2 --> X1
        X2 --> Y1
    end

    %%-----------------------------------------
    %% Phase 9: Charge-Off & Recovery Phase
    %%-----------------------------------------
    subgraph Phase_9 ["9. Charge-Off & Recovery Phase"]
        direction TB
        UncollectTrigger(["Trigger: Reaches<br/>180 DPD without<br/>a successful cure"])
        
        subgraph P9_S1 ["Charge-Off & Technical Write-Off"]
            Z1["<b>Action:</b> Bank writes<br/>off outstanding principal<br/>as bad debt loss"]
            Z2["<b>Impact:</b> Net Profit =<br/>- (Gross Charge-Off +<br/>Operational Coll Exp)"]
            Z1 --- Z2
        end
        
        subgraph P9_S2 ["Recovery Strategy Decision Fork"]
            AA{"Recovery<br/>Fork"}
            AB1(["Agency Recovery:<br/>Outsource to 3rd-party<br/>(keeps 15–30%)"])
            AC1(["Debt Sale:<br/>Sell toxic bundle<br/>(4-12 cents per $)"])
            AD1(["Legal Action:<br/>Reserved for high-bal<br/>garnish assets/income"])
            AA --> AB1
            AA --> AC1
            AA --> AD1
        end
        
        subgraph P9_S3 ["Ultimate Lifecycle End-State Metrics"]
            AE1["• <b>Recovery Rate</b> =<br/>(Total Recov + Sale)<br/>/ Gross Charge-Off"]
            AE2["• <b>NCO Ratio (%)</b> =<br/>(Charge-Offs - Recov)<br/>/ Avg Total Outstanding"]
            AE1 --- AE2
        end
        
        UncollectTrigger --> Z1
        Z2 --> AA
        AB1 --> AE1
        AC1 --> AE1
        AD1 --> AE1
    end

    %%-----------------------------------------
    %% Inter-Phase Connections
    %%-----------------------------------------
    B4 --> C
    C_D3 --> D1
    E -- "Yes" --> G1
    M1 -- "Loop back to recalculate metrics" --> G1
    I2 --> J
    L --> N1
    P3 --> Q2
    Q8 -.-> DelinqTrigger
    Y2 -.-> UncollectTrigger

    %%-----------------------------------------
    %% Theme & Styling Colors
    %%-----------------------------------------
    
    %% Base workflow states
    classDef reject fill:#ffcdd2,stroke:#d32f2f,stroke-width:2px;
    classDef approve fill:#c8e6c9,stroke:#388e3c,stroke-width:2px;
    classDef loop fill:#fff9c4,stroke:#fbc02d,stroke-width:2px;
    classDef alert fill:#ffe0b2,stroke:#f57c00,stroke-width:2px;
    classDef metrics fill:#e1bee7,stroke:#8e24aa,stroke-width:2px;
    
    %% Base Node Box styling
    classDef default fill:#636363,stroke:#333,stroke-width:1px;

    %% Apply Status Classes
    class F,F1 reject;
    class L approve;
    class M1 loop;
    class DelinqTrigger,UncollectTrigger alert;
    class AE1,AE2 metrics;
