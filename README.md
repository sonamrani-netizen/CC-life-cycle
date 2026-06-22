graph TD
    classDef phase fill:#f9f9f9,stroke:#333,stroke-width:2px,font-weight:bold;
    classDef reject fill:#ffebee,stroke:#c62828,stroke-width:2px;
    classDef approve fill:#e8f5e9,stroke:#2e7d32,stroke-width:2px;
    classDef decision fill:#fff3e0,stroke:#ef6c00,stroke-width:2px;

    %% Phase 1: Intake
    A["Customer Submits Application<br/>Name, Address, Income, SSN"] --> B["Bank Receives Application"]
    B --> C["Data Aggregation<br/>App Data, Bureau Data, Internal Data"]

    %% Phase 2 & 3: Risk Assessment & Modeling
    C --> D["Risk Assessment: KPI Evaluation<br/>Credit Score, Delinquency, DTI, etc."]
    D --> E["Advanced Risk Modeling Engine<br/>Calculates Probability of Default"]
    
    %% Decision Fork 1
    E --> F{"Risk Threshold Pass?"} ::: decision
    F -- No --> G["Application Rejected"] ::: reject
    
    %% Phase 4: Financial Viability
    F -- Yes --> H["Financial Viability Phase"]
    H --> I["Step 1: Determine APR & Credit Limit"]
    I --> J["Step 2: Calculate Expected Revenue"]
    J --> K["Step 3: Calculate NRAR & Expected Profitability"]
    
    %% Decision Fork 2
    K --> L{"Profitability >= Hurdle Rate?"} ::: decision
    L -- Yes --> M["Application Approved<br/>Offer Calculated Limit & APR"] ::: approve
    M --> N["Move to Approved Applications Workflow"] ::: approve
    
    %% Counter-Offer Loop
    L -- No --> O["Route for Counter-Offer"]
    O --> P["Adjust Variables<br/>Lower Credit Limit or Higher APR"]
    P -. "Recalculate" .-> I
