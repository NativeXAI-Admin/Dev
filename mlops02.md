graph TB
    subgraph "Databricks Development Workspace"
        subgraph "Tier 1: Experimentation"
            A[Data Scientists] --> B[Feature Branches]
            B --> C[Experiment Jobs]
            C --> D[Local Testing]
        end
        
        subgraph "Tier 2: Integration"
            D --> E[Master Branch]
            E --> F[Integration Pipeline]
            F --> G{Basic CI/CD<br/>Unit Tests<br/>Vulnerability Scan}
        end
        
        subgraph "Tier 3: Build Validation"
            G --> H[Build Environment]
            H --> I[Build Pipeline]
            I --> J{Comprehensive Validation<br/>Code Standards<br/>Performance Tests<br/>Security Scans}
            J --> K[Artifact Assembly]
        end
    end
    
    subgraph "Azure DevOps & Artifact Storage"
        L[ADO Build Pipeline] -.triggers.-> I
        K --> M[Azure Artifacts]
        M --> N[Model Registry]
        M --> O[Code Repository]
        M --> P[Config Management]
    end
    
    subgraph "Databricks UAT/Prod Workspaces"
        Q[Release Pipeline<br/>Azure DevOps] --> R{Pull Artifacts}
        M --> R
        R --> S[UAT Workspace]
        S --> T[Automated Tests]
        T --> U[QA Team Review]
        U --> V{Manual Approval}
        V --> W[Prod Workspace]
        W --> X[Monitoring & Logging]
    end
    
    subgraph "Governance Layer"
        Y[Approved Packages] -.enforced.-> C
        Y -.enforced.-> F
        Y -.enforced.-> I
        Z[Policy as Code] -.enforced.-> J
        Z -.enforced.-> V
    end
    
    style K fill:#90EE90
    style M fill:#FFD700
    style W fill:#FF6B6B