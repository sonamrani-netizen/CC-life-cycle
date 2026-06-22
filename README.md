``` mermaid
flowchart TD
    %%-----------------------------------------
    %% Phase 1: Intake
    %%-----------------------------------------
    subgraph Phase_1 ["1. Application Intake"]
        direction TB
        A["Customer Submits App<br/>(Name, Income, SSN)"]
        B["Bank Receives App<br/>(Aggregates Bureau & Internal Data)"]
        A --> B
    end

    %%-----------------------------------------
    %% Phase 2: Risk Filter
    %%-----------------------------------------
    subgraph Phase_2 ["2. Risk Assessment"]
        direction TB
        C["Policy & KPI Eval<br/>(Check Credit History & DTI)"]
        B --> C
    end

    %%-----------------------------------------
    %% Phase 3: Modeling
    %%-----------------------------------------
    subgraph Phase_3 ["3. Advanced Risk Modeling"]
        direction TB
        D["Risk Modeling Engine<br/>(Calculates Probability of Default)"]
        E{"Passes Risk Threshold?"}
        F(["Application Rejected"])
        
        C --> D
        D --> E
        E -- "No" --> F
    end

    %%-----------------------------------------
    %% Phase 4: Viability
    %%-----------------------------------------
    subgraph Phase_4 ["4. Financial Viability"]
        direction TB
        G["Step 1: Set APR & Credit Limit"]
        H["Step 2: Calculate Expected Revenue"]
        I["Step 3: Calculate Profitability (NRAR)"]
        
        E -- "Yes" --> G
        G --> H
        H --> I
    end

    %%-----------------------------------------
    %% Phase 5: Final Decision
    %%-----------------------------------------
    subgraph Phase_5 ["5. Final Approval Decision"]
        direction TB
        J{"Meets Hurdle Rate?"}
        K["Application Approved"]
        L(["Move to Approved Workflow"])
        M["Counter-Offer<br/>(Adjust Limit/APR)"]
        
        I --> J
        J -- "Yes" --> K
        K --> L
        J -- "No" --> M
    end

    M -- "Recalculate" --> G

    %%-----------------------------------------
    %% Phase 6: Issuance
    %%-----------------------------------------
    subgraph Phase_6 ["6. Onboarding & Issuance"]
        direction TB
        N["KYC & AML Verification"]
        O["Core Account Creation"]
        P["Digital & Physical Card Issuance"]
        
        L --> N
        N --> O
        O --> P
    end

    %%-----------------------------------------
    %% Phase 7: Lifecycle
    %%-----------------------------------------
    subgraph Phase_7 ["7. Usage & Portfolio Management"]
        direction TB
        Q1["Active Card Usage"]
        Q2["Calculate Ongoing Revenue & Profit"]
        R["Continuous Behavioral Scoring"]
        
        S{"Portfolio Actions"}
        T(["Case A: Credit Limit Increase"])
        U(["Case B: Credit Limit Decrease / Block"])
        V(["Case C: Retention & Cross-Sell"])
        
        P --> Q1
        Q1 --> Q2
        Q2 --> R
        R --> S
        S --> T
        S --> U
        S --> V
    end

    %%-----------------------------------------
    %% Phase 8: Collections
    %%-----------------------------------------
    subgraph Phase_8 ["8. Delinquency & Collections"]
        direction TB
        DelinqTrigger(["Fails to Pay Minimum Due"])
        W["Early Collections (1-30 DPD)"]
        X["Mid Collections (31-90 DPD)"]
        Y["Late Collections (91-180 DPD)"]
        
        Q1 -.-> DelinqTrigger
        DelinqTrigger --> W
        W --> X
        X --> Y
    end

    %%-----------------------------------------
    %% Phase 9: Recovery
    %%-----------------------------------------
    subgraph Phase_9 ["9. Charge-Off & Recovery"]
        direction TB
        UncollectTrigger(["180 DPD Reached"])
        Z["Charge-Off & Write-Off"]
        
        AA{"Recovery Strategy"}
        AB(["3rd-Party Agency"])
        AC(["Debt Sale"])
        AD(["Legal Litigation"])
        
        AE["End-State Metrics<br/>(Recovery Rate & NCO)"]
        
        Y -.-> UncollectTrigger
        UncollectTrigger --> Z
        Z --> AA
        AA --> AB
        AA --> AC
        AA --> AD
        
        AB --> AE
        AC --> AE
        AD --> AE
    end

    %% Styling
    classDef reject fill:#ffcdd2,stroke:#d32f2f,stroke-width:2px;
    classDef approve fill:#c8e6c9,stroke:#388e3c,stroke-width:2px;
    classDef loop fill:#fff9c4,stroke:#fbc02d,stroke-width:2px;
    classDef alert fill:#ffe0b2,stroke:#f57c00,stroke-width:2px;
    classDef metrics fill:#e1bee7,stroke:#8e2
