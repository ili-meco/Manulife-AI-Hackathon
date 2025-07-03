# Day 3 Lab: Microsoft Copilot Studio for Manulife

## Lab Overview
**Duration:** 3 hours  
**Prerequisites:** Azure AI Foundry project from Day 2  
**Objective:** Build production-ready AI agents using Copilot Studio with governance and best practices for enterprise deployment

---

## Setup Instructions

### Step 1: Access Copilot Studio
1. Navigate to [Microsoft Copilot Studio](https://copilotstudio.microsoft.com)
2. Sign in with your Microsoft 365 or Azure credentials
3. Select or create an environment for development

### Step 2: Connect to Azure AI Foundry
1. In Copilot Studio, go to **Settings** → **AI capabilities**
2. Connect your Azure OpenAI service from Day 1
3. Configure model access permissions

### Step 3: Enable Premium Features
Ensure access to:
- Generative AI features
- Custom connectors
- Analytics and monitoring
- Enterprise security controls

---

## Lab Task Overview

### Exercise 1: Building Your First Copilot (60 minutes)

#### Task 1.1: Create Manulife Customer Service Copilot
1. Click **+ Create** → **New copilot**
2. Choose **Build your own** → **Conversational**
3. Configure:
   - Name: `Manulife Customer Assistant`
   - Language: English (Canada)
   - Website: `manulife.com`
   - Industry: Financial Services

#### Task 1.2: Design Conversation Flow
Create the main conversation structure:

```
Greeting Topic:
- Trigger phrases: "Hello", "Hi", "Help", "Support"
- Response: "Welcome to Manulife! I'm here to help you with your insurance and financial needs. How can I assist you today?"
- Follow-up options:
  * Policy Information
  * Claims Support  
  * Product Inquiries
  * Account Services
```

#### Task 1.3: Configure Core Topics
Build these essential topics:

**Topic 1: Policy Information**
```
Trigger Phrases:
- "policy details"
- "my coverage"
- "insurance information"
- "what's covered"

Conversation Flow:
1. Ask for policy type (Life, Auto, Home, Health)
2. Request policy number or customer ID
3. Verify identity with security questions
4. Provide policy summary
5. Offer detailed information or connect to agent
```

**Topic 2: Claims Support**
```
Trigger Phrases:
- "file a claim"
- "claim status"
- "accident report"
- "claim help"

Conversation Flow:
1. Determine claim type
2. Check if it's a new claim or status inquiry
3. Guide through appropriate process
4. Collect necessary information
5. Provide next steps and reference number
```

#### Task 1.4: Test Your Copilot
Use the **Test your copilot** pane to validate:
- Greeting responses
- Topic triggering
- Conversation flow
- Error handling

### Exercise 2: Advanced Features and Integrations (75 minutes)

#### Task 2.1: Integrate External Data Sources
Connect to Manulife systems (simulated):

1. **Create Power Automate Flow**
   - Trigger: When copilot needs policy data
   - Action: Query customer database (use sample data)
   - Return: Policy information to copilot

2. **Add Custom Connector**
   ```
   Connector Name: Manulife Policy API
   Base URL: https://api.manulife.com (simulated)
   Authentication: OAuth 2.0
   
   Operations:
   - GET /policies/{customerId}
   - GET /claims/{claimId}
   - POST /claims/new
   ```

#### Task 2.2: Implement Smart Features
Add AI-powered capabilities:

**Entity Recognition:**
```
Custom Entities:
- Policy Types: Life, Auto, Home, Travel, Health, Disability
- Claim Types: Auto Accident, Property Damage, Medical, Travel
- Customer Intent: Information, Claims, Support, Billing
```

**Conversation Intelligence:**
```
Sentiment Analysis:
- Monitor customer satisfaction during conversation
- Escalate to human agent if negative sentiment detected
- Adjust response tone based on customer emotion

Intent Classification:
- Automatically route to appropriate topic
- Suggest relevant products or services
- Provide proactive assistance
```

#### Task 2.3: Create Adaptive Cards
Design rich interactive elements:

**Policy Summary Card:**
```json
{
  "type": "AdaptiveCard",
  "version": "1.3",
  "body": [
    {
      "type": "Container",
      "items": [
        {
          "type": "TextBlock",
          "text": "Policy Summary",
          "weight": "Bolder",
          "size": "Medium"
        },
        {
          "type": "FactSet",
          "facts": [
            {
              "title": "Policy Number:",
              "value": "{policyNumber}"
            },
            {
              "title": "Coverage Type:",
              "value": "{coverageType}"
            },
            {
              "title": "Premium:",
              "value": "{monthlyPremium}/month"
            },
            {
              "title": "Next Payment:",
              "value": "{nextPaymentDate}"
            }
          ]
        }
      ]
    }
  ],
  "actions": [
    {
      "type": "Action.Submit",
      "title": "Make Payment",
      "data": {
        "action": "payment"
      }
    },
    {
      "type": "Action.Submit", 
      "title": "View Details",
      "data": {
        "action": "details"
      }
    }
  ]
}
```

### Exercise 3: Governance and Security Implementation (45 minutes)

#### Task 3.1: Configure Security Controls
Set up enterprise-grade security:

**Authentication Settings:**
```
Authentication Type: Azure AD (SSO)
User Verification: Required for sensitive operations
Session Management: 30-minute timeout
Access Control: Role-based permissions
```

**Data Loss Prevention (DLP):**
```
Sensitive Data Types:
- Social Insurance Numbers (SIN)
- Credit Card Numbers
- Policy Numbers
- Personal Health Information

Actions:
- Block transmission of sensitive data
- Mask displayed sensitive information
- Log all data access attempts
- Alert on policy violations
```

#### Task 3.2: Implement Compliance Framework
Configure for financial services compliance:

**Audit and Logging:**
```
Log Requirements:
- All customer interactions
- Data access and modifications
- Authentication events
- Error conditions and escalations

Retention Policy:
- Conversation logs: 7 years
- Audit trails: 10 years
- Performance metrics: 3 years
- Error logs: 5 years
```

**Privacy Controls:**
```
Data Handling:
- Customer consent tracking
- Data minimization principles
- Right to be forgotten implementation
- Cross-border data transfer restrictions

Consent Management:
- Explicit consent for data processing
- Granular permission controls
- Consent withdrawal mechanisms
- Regular consent refresh
```

#### Task 3.3: Set Up Monitoring and Analytics
Configure comprehensive monitoring:

**Performance Metrics:**
```
Key Performance Indicators:
- Resolution rate: Target 85%
- Customer satisfaction: Target 4.2/5
- Average handling time: Target <5 minutes
- Escalation rate: Target <15%

Business Metrics:
- Cost per interaction
- Containment rate
- First contact resolution
- Customer effort score
```

**Operational Monitoring:**
```
System Health:
- Response time monitoring
- Error rate tracking
- Availability metrics
- Capacity utilization

Quality Assurance:
- Response accuracy scoring
- Compliance adherence
- Brand consistency
- Conversation flow optimization
```

### Exercise 4: Enterprise Deployment Preparation (40 minutes)

#### Task 4.1: Environment Strategy
Plan deployment across environments:

**Development Environment:**
```
Purpose: Copilot development and testing
Access: Development team only
Data: Synthetic test data
Integrations: Mock services
Monitoring: Basic logging
```

**User Acceptance Testing (UAT):**
```
Purpose: Business stakeholder validation
Access: Selected business users
Data: Anonymized production data
Integrations: Non-production systems
Monitoring: Detailed analytics
```

**Production Environment:**
```
Purpose: Live customer interactions
Access: End users and support teams
Data: Live customer data
Integrations: Production systems
Monitoring: Full enterprise monitoring
```

#### Task 4.2: Change Management Process
Establish governance for copilot updates:

**Change Control Board:**
```
Members:
- IT Security Representative
- Business Owner
- Compliance Officer
- Customer Experience Manager
- Technical Lead

Approval Process:
1. Impact assessment
2. Security review
3. Compliance check
4. Business approval
5. Technical validation
6. Deployment scheduling
```

**Release Management:**
```
Release Types:
- Hotfix: Critical security or compliance issues
- Minor: Feature enhancements and bug fixes
- Major: Significant functionality changes

Deployment Process:
1. Code review and testing
2. Staging environment validation
3. User acceptance testing
4. Production deployment
5. Post-deployment monitoring
6. Rollback procedures
```

---

## Challenge Tasks

### Challenge 1: Multi-Channel Deployment
Deploy your copilot across multiple channels:
- Microsoft Teams integration
- Website embed widget
- Mobile app integration
- Voice-enabled interface (Power Virtual Agents)

### Challenge 2: Advanced AI Features
Implement sophisticated AI capabilities:
- Multi-language support (English/French for Canada)
- Sentiment-based conversation routing
- Predictive analytics for customer needs
- Automated quality scoring

### Challenge 3: Integration Ecosystem
Build comprehensive system integration:
- CRM system connectivity
- Payment processing integration
- Document management system
- Knowledge base integration

---

## Evaluation Criteria

### Functional Requirements
- **Conversation Quality**: Natural, helpful interactions
- **System Integration**: Seamless data flow between systems
- **User Experience**: Intuitive interface and smooth conversation flow
- **Problem Resolution**: Effective handling of customer issues

### Non-Functional Requirements
- **Security**: Proper authentication and data protection
- **Compliance**: Adherence to financial services regulations
- **Performance**: Fast response times and high availability
- **Scalability**: Ability to handle enterprise-level traffic

### Governance and Operations
- **Monitoring**: Comprehensive analytics and alerting
- **Maintenance**: Clear update and deployment processes
- **Documentation**: Complete technical and user documentation
- **Training**: User guides and admin procedures

---

## Best Practices

### Design Principles
1. **Customer-Centric**: Focus on solving real customer problems
2. **Conversational**: Natural language interactions
3. **Contextual**: Remember conversation history and customer data
4. **Graceful Degradation**: Handle errors smoothly
5. **Continuous Learning**: Regular optimization based on feedback

### Security Best Practices
1. **Zero Trust**: Verify all interactions and data access
2. **Least Privilege**: Minimal necessary permissions
3. **Data Encryption**: Protect data in transit and at rest
4. **Regular Audits**: Continuous security assessments
5. **Incident Response**: Clear procedures for security events

### Operational Excellence
1. **Monitoring**: Comprehensive observability
2. **Documentation**: Keep all materials current
3. **Testing**: Regular validation of functionality
4. **Feedback Loops**: Continuous improvement processes
5. **Disaster Recovery**: Business continuity planning

---

## Resources

### Documentation
- [Copilot Studio Documentation](https://docs.microsoft.com/power-virtual-agents/)
- [Power Platform Security](https://docs.microsoft.com/power-platform/admin/security/)
- [Financial Services Compliance](https://docs.microsoft.com/compliance/regulatory/offering-home)

### Training Materials
- Microsoft Learn: Copilot Studio modules
- Power Platform community resources
- Industry-specific implementation guides

### Support
- Microsoft support channels
- Power Platform community forums
- Internal Manulife IT support

---

## Next Steps

### Day 4 Preparation
- Export copilot configuration for integration
- Prepare customer data for RAG implementation
- Document conversation flows for vector search optimization

### Production Planning
- Schedule security review with IT team
- Plan user training sessions
- Establish ongoing maintenance procedures
- Set up monitoring dashboards

---

## Troubleshooting

### Common Issues
- **Authentication failures**: Check Azure AD configuration
- **Integration errors**: Validate API connections and permissions
- **Performance issues**: Review conversation complexity and data queries
- **Compliance violations**: Audit DLP policies and data handling

### Performance Optimization
- **Response Time**: Optimize conversation flows and reduce external calls
- **Accuracy**: Regular training data updates and intent tuning
- **User Satisfaction**: A/B testing of conversation approaches
- **Cost Management**: Monitor API usage and optimize model selection
