# Fair Finance
Fair Finance is a UK-based social business that specializes in providing affordable personal loans to financially excluded individuals. The company targeting customers who are typically rejected by mainstream banks or exploited by high-cost credit providers. See more [`fair finance`](https://fairfinance.org.uk/about-us/)
, 
This software suite powers Fair Finance’s digital operations, covering customer applications, internal tools, core business logic, analytics, data synchronization, and integrations.

## Overview

### Customer-portal Application

#### [`ff-customer-portal`](./ff-customer-portal)
**Next.js Customer Application Platform**
- **Purpose**: Primary interface for loan applications and account management
- **Key Features**:
  - Multi-step loan application form with validation
  - Loan tracking and repayment management
  - Customer profile and settings

###  Administrative Applications

#### [`ff-internal-portal`](./ff-internal-portal)
**internal portal Dashboard**
- **Purpose**: Internal tools for Fair Finance staff to manage operations
- **Key Features**:
  - Loan application review and processing
  - Customer data management and CRM integration
  - Analytics and reporting
  - Data Visualizations and statistics

###  Backend Services

#### [`ff-api`](./ff-api)
**Core Business Logic API**
- **Purpose**: Central backend service handling all business operations
- **Key Responsibilities**:
  - API endpoints for customer-portal & internal-portal
  - Loan application processing and validation
  - Secure Integration with external systems (Microsoft Dynamics 365 (CRM),Loan Management System(LMS), Open Banking Vision(obv))
  - Business rule enforcement and decision logic
  - Tracking & Reporting

#### [`ff-proxy`](./ff-proxy)
**Secure API Gateway**
- **Purpose**: Reverse proxy for external service integration
- **Technology**: NGINX on AWS EC2
- **Key Features**:
  - IP whitelisting for third-party API access
  - Credential management and request transformation
  - Centralized access point for external integrations(e.g., Open Banking Vision, Dynamics 365)

### Data and Analytics

#### [`ff-data-analysis`](./ff-data-analysis)
**Financial Data Processing Platform**
- **Purpose**: A robust analytics platform built to process, transform, and visualize financial data from various sources.
- **Key Capabilities**:
  - processes financial and loan application data
  - Credit risk assessment and scoring
  - provides analytical insights
  - transforms financial and loan data into structured formats
  - Regulatory reporting and compliance analytics

#### [`ff-tracker`](./ff-tracker)
**Customer Journey Analytics**
- **Purpose**: Application session tracking and user behavior analysis
- **Key Features**:
  - Real-time session tracking and user flow mapping
  - Conversion funnel analysis and drop-off identification

### Data Synchronization Services

#### [`ff-backup-sync`](./ff-backup-sync)
**Anchor LMS Data Integration**
- **Purpose**: Automated synchronization with loan management system
- **Process**:
  - Daily SFTP retrieval of database backups from Anchor LMS
  - Format conversion and data transformation
  - Secure storage in AWS S3 and restoration to RDS SQL Server
  - Data validation and integrity checking

#### [`ff-obv-backup-sync`](./ff-obv-backup-sync)
**Third-Party Data Backup Service**
- **Purpose**: service automates the retrieval, transformation, and secure archival of Open Banking data tied to loan applications.
- **Process**:
  - Automated synchronization of Open Banking data 
  - ensures all financial records are retained for compliance, analysis, and historical tracking.
  - Data validation and integrity checking
