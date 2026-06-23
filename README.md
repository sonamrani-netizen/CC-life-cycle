``` mermaid
flowchart TD
    %%-----------------------------------------
    %% Phase 1: Application Intake Phase
    %%-----------------------------------------
    subgraph Phase_1 ["1. Application Intake Phase"]
        direction TB
        
        subgraph P1_S1 ["Customer Submission"]
            A1["<b>Captured Data:</b><br/>Name, Address, SSN<br/>Income details"]
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
            D2["• <br/>Calculates Prob of<br/>Default (PD)"]
            D1 --- D2
        end
        
        E{"Risk Threshold<br/>Pass?"}
        
        F(["Application<br/>Rejected"])
        
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
            G4["<i>Rule: Lower-risk =<br/>lower APR | Higher-risk<br/>= higher APR</i>"]
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
        P6_Node["Onboarding & Card Issuance Phase"]
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
    %% Phase 10: Post-Rejection Workflow & Data Lab
    %%-----------------------------------------
    subgraph Phase_10 ["10. Post-Rejection Workflow & Data Lab"]
        direction TB
        
        subgraph P10_S1 ["Immediate Operational Actions"]
            R_O1["• Adverse Action Stamping:<br/>Log regulatory<br/>decline reasons"]
            R_O2["• Cooling-Off Flagging:<br/>3-6 month master DB<br/>hard block"]
            R_O1 --- R_O2
        end
        
        subgraph P10_S2 ["System Fault Correction Lifecycle"]
            R_E1{"System Error<br/>Detected?"}
            R_E2["• Retro-Approval Workflow:<br/>Isolate cohort<br/>& clear block"]
            R_E3["• Force Card<br/>Issuance<br/>& Onboard"]
            R_E4["• Bureau Inquiry Repair:<br/>Delete hard<br/>pull flag"]
            R_E1 -- "Yes" --> R_E2
            R_E2 --> R_E3 --> R_E4
        end
        
        subgraph P10_S3 ["Data Science (Reject Inference)"]
            R_D1["• Fuzzy Augmentation:<br/>Assign calculated<br/>default prob"]
            R_D2["• Parceling:<br/>Blend 'inferred goods'<br/>into training DB"]
            R_D3["• Override Audits:<br/>Profile human<br/>exception performance"]
            R_D1 --- R_D2 --- R_D3
        end
        
        subgraph P10_S4 ["Opportunity Cost Modeling"]
            R_F1["• Expected LTV Simulation"]
            R_F2["• RAROC Adjustment:<br/>Evaluate loosening<br/>scorecard cutoff"]
            R_F1 --> R_F2
        end
        
        subgraph P10_S5 ["CRO Executive Tracking Dashboard"]
            R_K1["• Decline Rate<br/>by<br/>Channel"]
            R_K2["• Through-the-Door<br/>Metric<br/>Score"]
            R_K3["• Adverse Action<br/>Density<br/>& PSI"]
            R_K1 --- R_K2 --- R_K3
        end

        R_O2 --> R_E1
        R_E1 -- "No" --> R_D1
        R_D3 --> R_F1
        R_F2 --> R_K1
    end

    %%-----------------------------------------
    %% Inter-Phase Connections
    %%-----------------------------------------
    B4 --> C
    C_D3 --> D1
    E -- "Yes" --> G1
    M1 -- "Loop back to recalculate metrics" --> G1
    I2 --> J
    L --> P6_Node
    P6_Node --> Q2
    Q8 -.-> DelinqTrigger
    Y2 -.-> UncollectTrigger
    F --> R_O1
    R_E4 --> L

    %%-----------------------------------------
    %% Theme & Styling Colors
    %%-----------------------------------------
    
    %% Base workflow states
    classDef reject fill:#DB5858,stroke:#d32f2f,stroke-width:2px;
    classDef approve fill:#5fa462,stroke:#388e3c,stroke-width:2px;
    classDef loop fill:#766a00,stroke:#fbc02d,stroke-width:2px;
    classDef alert fill:#c4b000,stroke:#ebd300,stroke-width:2px;
    classDef metrics fill:#54225d,stroke:#8e24aa,stroke-width:2px;
    
    %% Base Node Box styling
    classDef default fill:#636363,stroke:#333,stroke-width:1px;

    %% Apply Status Classes
    class F reject;
    class L,R_E3 approve;
    class M1 loop;
    class DelinqTrigger,UncollectTrigger alert;
    class AE1,AE2,R_K1,R_K2,R_K3 metrics;
