# Fair Finance
Fair Finance is a UK-based social business that specializes in providing affordable personal loans to financially excluded individuals. The company targets customers who are typically rejected by mainstream banks or exploited by high-cost credit providers. See more [`fair finance`](https://fairfinance.org.uk/about-us/)

This software suite powers Fair Finance’s digital operations, covering customer applications, internal tools, core business logic, analytics, data synchronization, and integrations.

## Overview

### Customer-portal Application

#### [`ff-customer-portal`](https://github.com/fairfinance-limited/ff-customer-portal)
**Customer Application Platform**
- **Purpose**: Primary interface for loan applications and account management.
- **Technology**:
  - Next.js 14 (React 18)
  - UI: Material UI (MUI) 6
  - Testing: Playwright
- **Third-Party & Services**:
    - ff-api(Central backend service)
    - ff-tracker: User behavior tracking system for application form analytics
- **Key Features**:
  - Multi-step loan application form with validation
  - Loan tracking and repayment management
  - Customer profile and settings

###  Administrative Applications

#### [`ff-internal-portal`](https://github.com/fairfinance-limited/ff-internal-portal)
**Internal Portal Dashboard**
- **Purpose**: Internal tools for Fair Finance staff to manage operations.
- **Technology**:
  - Next.js RC (React RC)
  - UI : Material UI (MUI) 6
- **Third-Party & Services**:
    - ff-api: Central backend service
    - Google Analytics: Google Analytics Data API used for marketing analytics and user behavior analysis
    - Anthropic Claude: AI-powered analytics
    - AWS S3: Document storage and file management system via presigned URLs
- **Key Features**:
  - Loan application review and processing
  - Customer data management and CRM integration
  - Analytics and reporting
  - Data Visualizations and statistics

### ⚡ Backend Services

#### [`ff-api`](https://github.com/fairfinance-limited/ff-api)
**Core Business Logic API**
- **Purpose**: Central backend service handling all business operations
- **Technology**:
  - Node.js (Express.js API framework) with TypeScript
  - Serverless Framework on AWS Lambda
  - Deployment & Infrastructure:
    - GitHub Actions: workflows for automated CI/CD
    - Terraform: manage core infrastructure
  - Databases:
    - MongoDB: Customer data and forms, operational data
    - SQL Server (RDS): loan data, customer information, personal details
- **Third-Party & Services**:
    - Microsoft Dynamics 365: CRM system integration using REST API
    - Anchor LMS: Loan Management System using SOAP/XML API
    - Open Banking Vision (OBV): Bank account data and transaction analysis
    - Google Analytics: User behavior tracking and marketing analytics
    - AWS Services:
      - S3: Document storage and file management
      - SQS: messaging and task queues
      - SES: Transactional emails
      - Cognito: User authentication and authorization
      - Athena/Glue: Analytics data processing
- **Key Features**:
  - API endpoints for customer-portal & internal-portal
  - Loan application processing.
  - Secure Integration with external systems (Microsoft Dynamics 365 (CRM), Loan Management System(LMS), Open Banking Vision(obv))
  - Business rule enforcement and decision logic
  - Tracking & Reporting

#### [`ff-proxy`](https://github.com/fairfinance-limited/ff-proxy)
**Secure API Gateway**
- **Purpose**: Reverse proxy service providing secure, centralized access to external financial APIs and services
- **Technology**: 
  - NGINX: Reverse proxy server
  - Infrastructure:
    - AWS EC2: Hosting environment
    - VPC: Network isolation
  - Deployment & Infrastructure:
    - Terraform: Infrastructure as code
    - GitHub Actions: Automated deployments
- **Third-Party & Services: (proxy connects to)**:
    - Open Banking Vision (OBV): Bank transaction data and financial analysis
    - Microsoft Dynamics 365: CRM and customer data
- **Key Features**:
  - IP whitelisting for third-party API access
  - Credential management and request transformation
  - Centralized access point for external integrations (e.g., Open Banking Vision, Dynamics 365)

### Data and Analytics

#### [`ff-data-analysis`](https://github.com/fairfinance-limited/ff-data-analysis)
**Financial Data Processing Platform**
- **Purpose**: A robust analytics platform built to process, transform, and visualize financial data from various sources.
- **Technology**:
  - Node.js: Core processing engine for the ADP module
  - Python: Powers the Dynamics CRM integration
- **Third-Party & Services**:
    - Microsoft Dynamics 365: CRM and customer data
    - Anchor LMS: Loan Management System
- **Key Features**:
  - Processes financial and loan application data
  - Provides analytical insights
  - Transforms financial and loan data into structured formats
  - Retrieves and analyzes loan application data

#### [`ff-tracker`](https://github.com/fairfinance-limited/ff-tracker)
**Customer Journey Analytics**
- **Purpose**: Tracks user behavior through loan application forms to identify drop-off points, optimize conversion rates, and detect potential duplicate applications
- **Technology**:
  - Node.js with Express: Backend processing service
  - Deployment & Infrastructure:
    - AWS ECS: Container orchestration for backend service
    - AWS ECR: Docker image registry
    - GitHub Actions: CI/CD workflows for deployment
- **Third-Party & Services**:
    - AWS Services:
      - Lambda: Event ingestion gateway with environment routing
      - S3: Storage for tracking data (events, user sessions)
      - SQS FIFO: Message queuing for ordered event processing
- **Key Features**:
  - Real-time session tracking and user flow mapping
  - Conversion funnel analysis and drop-off identification
  - CSV data extraction and storage for analytics

### Data Synchronization Services

#### [`ff-backup-sync`](https://github.com/fairfinance-limited/ff-backup-sync)
**Anchor LMS Data Integration**
- **Purpose**: Automated synchronization system that retrieves, converts, stores, and restores Anchor LMS database backups
- **Technology**:
  - Node.js (Express.js API framework) with TypeScript
  - Deployment & Infrastructure:
    - GitHub Actions: workflows for automated CI/CD
    - Terraform: manage core infrastructure
    - Windows EC2: Hosting environment
  - Databases:
    - PostgreSQL (RDS): structured data storage
- **Third-Party & Services**:
  - Anchor LMS: Source of proprietary SQL backups (.sqb format)
  - SFTP server: Backup file retrieval point
  - Databases:
    - SQL Server (RDS): SQL Server databases used to restore Anchor database backups data.
  - AWS Services:
    - EC2 Windows: Processing server for backup conversion
    - S3: Long-term storage for original and converted backups
    - SSM: Secure parameter storage
    - VPC: Network isolation and security
- **Key Features**:
  - Daily automated backup retrieval from SFTP server
  - Proprietary format conversion (.sqb to .bak)
  - Secure storage in AWS S3 and restoration to RDS SQL Server
  - RESTful API for manual operations
  - Data integrity verification and validation

#### [`ff-obv-backup-sync`](https://github.com/fairfinance-limited/ff-obv-backup-sync)
**Third-Party Data Backup Service**
- **Purpose**: Service that automates the retrieval, transformation, and secure archival of Open Banking data tied to loan applications stored in CRM.
- **Technology**:
  - Node.js (Express.js API framework) with TypeScript
  - Deployment & Infrastructure:
    - GitHub Actions: workflows for automated CI/CD
    - Terraform: manage core infrastructure
  - Databases:
    - PostgreSQL (RDS): structured data storage
- **Third-Party & Services**:
  - Microsoft Dynamics 365 (CRM): Source of loan application data
  - Open Banking Vision (OBV): Financial data provider
  - AWS Services:
    - SSM: Securely stores all sensitive credentials
    - S3: Terraform state storage
    - VPC: Network isolation
- **Key Features**:
  - Fetches applications with OBV references from Dynamics CRM
  - Retrieves detailed Open Banking data using references
  - Automated synchronization of Open Banking data 
  - Structured storage in PostgreSQL with transaction safety
  - Data validation and integrity checking
