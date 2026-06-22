``` mermaid
flowchart TD
    %% Phase 1: Application Intake Phase
    subgraph Phase_1 ["1. Application Intake Phase"]
        direction TB
        A["Customer Submits Application<br/><b>Captured Data:</b> Name, Address, Income details, SSN"]
        
        B["Bank Receives Application<br/><b>Data Aggregation (3 Sources):</b><br/>• Application Data (Customer provided)<br/>• Credit Bureau Data (TransUnion, Equifax, Experian)<br/>• Internal Bank Data (Prior relationships)"]
        
        A --> B
    end

    %% Phase 2: Risk Assessment Phase
    subgraph Phase_2 ["2. Risk Assessment Phase (Automated Filtering)"]
        direction TB
        C["Policy Threshold & KPI Evaluation<br/><br/><b>Credit History Evaluation:</b><br/>• Credit Score: Benchmarked against historical consumer data<br/>• Missed Payments: Evaluates past payment behavior<br/>• Default History: Checks for prior loan/credit failures<br/>• Number of Enquiries: Monitors recent hard inquiries (credit hungriness)<br/>• Vintage: Length of credit relationship (longer = stability)<br/>• Delinquency Rate: Historical roll-overs (e.g., 30-60 DPD)<br/>• NPA Ratio: Measures Non-Performing Asset ratio<br/><br/><b>Debt Burden & Income Evaluation:</b><br/>• Debt Burden: DTI ratio, current EMIs, utilization ratios<br/>• Income: Verified to ensure steady debt-servicing cash flow"]
        
        B --> C
    end

    %% Phase 3: Advanced Risk Modeling Phase
    subgraph Phase_3 ["3. Advanced Risk Modeling Phase"]
        direction TB
        D["Advanced Risk Modeling Engine<br/>• <b>Risk Models:</b> Internal ML models calculate custom score (e.g., Application Scorecard)<br/>• <b>Output:</b> Calculates Probability of Default (PD)"]
        
        E{"Risk Threshold Pass?"}
        
        F(["Application Rejected"])
        
        C --> D
        D --> E
        E -- No --> F
    end

    %% Phase 4: Financial Viability Phase
    subgraph Phase_4 ["4. Financial Viability Phase (Revenue & Profitability)"]
        direction TB
        G["Step 1: Determine APR & Credit Limit<br/>• <b>Credit Limit:</b> Based on Income, Debt Burden, internal risk tier<br/><i>Rule: Higher income + lower debt = higher limit</i><br/>• <b>APR Pricing:</b> Risk-based pricing using customer's PD & Credit Score<br/><i>Rule: Lower-risk = lower APR | Higher-risk = higher APR</i>"]
        
        H["Step 2: Calculate Expected Revenue<br/>• <b>Forecast:</b> Assigned Credit Limit × Expected Utilization = Predicted Revolving Balance<br/>• <b>Calculation:</b> (Predicted Revolving Balance × APR) + Annual/Transactional Fees"]
        
        I["Step 3: Calculate Net Risk-Adjusted Revenue & Profitability<br/>• <b>NRAR</b> = Expected Revenue - Expected Loss (Driven by PD)<br/>• <b>Expected Profitability</b> = NRAR - Operating Costs"]
        
        E -- Yes --> G
        G --> H
        H --> I
    end

    %% Phase 5: Final Approval Decision Phase
    subgraph Phase_5 ["5. Final Approval Decision Phase"]
        direction TB
        J{"Is Expected Profitability ≥<br/>Internal Hurdle Rate?"}
        
        K["Application Approved<br/>(Formally offer calculated Credit Limit and APR)"]
        
        L(["Move to Approved Applications Workflow"])
        
        M["Route for Counter-Offer<br/>(Adjust variables: lower credit limit or higher APR)"]
        
        I --> J
        J -- "Yes (Case A: Above Hurdle Rate)" --> K
        K --> L
        J -- "No (Case B: Below Hurdle Rate)" --> M
    end

    %% Loop-back connection spanning subgraphs
    M -- "Recalculate Profitability" --> G

    %% Styling to enhance visual clarity
    classDef reject fill:#ffcccc,stroke:#ff0000,stroke-width:2px;
    classDef approve fill:#ccffcc,stroke:#00aa00,stroke-width:2px;
    classDef loop fill:#fff0cc,stroke:#ffaa00,stroke-width:2px,stroke-dasharray: 5 5;
    
    class F reject;
    class L approve;
    class M loop;
