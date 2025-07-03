# Day 1 Lab: AI Introduction and Prompt Engineering

## Lab Overview  
**Prerequisites:** Azure account with access to Azure OpenAI Service  
**Objective:** Learn fundamental AI concepts and master prompt engineering techniques using Azure OpenAI

---

## Setup Instructions

### Step 1: Azure Resource Group Setup
1. Sign in to the [Azure portal](https://portal.azure.com)
2. Create a new Resource Group:
   - Name: `manulife-hackathon-rg`
   - Region: `East US` or `Canada Central`

### Step 2: Create Azure OpenAI Service
1. Navigate to **Create a resource** → **AI + Machine Learning** → **Azure OpenAI**
2. Configure the service:
   - Subscription: Your subscription
   - Resource Group: `manulife-hackathon-rg`
   - Region: `East US` (or available region)
   - Name: `manulife-openai-[yourname]`
   - Pricing tier: Standard S0

### Step 3: Deploy GPT Models
1. Navigate to Azure AI Foundry Studio
2. Go to **Deployments** → **Create new deployment**
3. Deploy the following models:
   - **GPT-4o**: For complex reasoning tasks
   - **GPT-3.5-turbo**: For general tasks
   - **text-embedding-ada-002**: For embeddings (Day 4 prep)

---

## Lab Exercises

### Exercise 1: Basic Prompt Engineering

#### Task 1.1: Simple Prompts
Test these basic prompts in Azure AI Foundry Chat Playground:

```
Prompt 1: "What is artificial intelligence?"
Prompt 2: "Explain artificial intelligence in simple terms for a 10-year-old."
Prompt 3: "Write a technical definition of artificial intelligence for a software engineer."
```

**Observation Points:**
- How does specificity affect the response?
- What happens when you add context about the audience?

#### Task 1.2: Role-Based Prompting
Try these role-based prompts:

```
Prompt: "You are a financial advisor at Manulife. Explain how AI can help with retirement planning."
Prompt: "You are a data scientist. Explain the difference between supervised and unsupervised learning."
```

### Exercise 2: Advanced Prompt Techniques

#### Task 2.1: Few-Shot Learning
Create a few-shot prompt for insurance claim classification:

```
Here are examples of insurance claim classifications:

Claim: "Car accident on Highway 401, minor fender bender"
Classification: Auto - Minor Damage
Priority: Low

Claim: "House fire caused significant damage to kitchen and living room"
Classification: Property - Major Damage  
Priority: High

Claim: "Slip and fall at grocery store, sprained ankle"
Classification: Personal Injury - Minor
Priority: Medium

Now classify this claim:
Claim: "Tree fell on roof during storm, water damage in multiple rooms"
Classification: ?
```

#### Task 2.2: Chain of Thought Prompting
Use this structured approach for complex problem solving:

```
Problem: A Manulife customer has $50,000 to invest. They are 35 years old, want to retire at 65, and have moderate risk tolerance. What investment strategy would you recommend?

Think through this step by step:
1. Calculate investment timeline
2. Assess risk tolerance implications
3. Consider age-appropriate asset allocation
4. Factor in Manulife product offerings
5. Provide specific recommendations with rationale
```

### Exercise 3: Industry-Specific Applications

#### Task 3.1: Customer Service Automation
Create prompts for common Manulife scenarios:

```
Scenario 1: Policy Inquiry
"You are a Manulife customer service AI. A customer asks: 'When does my life insurance policy expire?' 
Policy details: Term life, 20-year term, started in 2020, premium $45/month
Respond professionally and helpfully."

Scenario 2: Claims Process
"Guide a customer through filing a travel insurance claim for a cancelled flight due to weather."
```

#### Task 3.2: Financial Planning Assistant
```
"You are a Manulife financial planning assistant. Create a personalized savings strategy for:
- Age: 28
- Income: $75,000 CAD
- Goals: Buy house in 5 years, retire comfortably
- Current savings: $15,000
- Monthly expenses: $4,000

Provide specific, actionable recommendations."
```

---

## Challenge Tasks

### Challenge 1: Prompt Optimization
Take this poorly written prompt and improve it:

**Poor Prompt:** "Tell me about investing"

**Your Improved Prompt:** [Write your optimized version]

### Challenge 2: Multi-Turn Conversation
Design a conversation flow for a customer onboarding chatbot that:
1. Gathers customer information
2. Assesses financial goals  
3. Recommends appropriate Manulife products
4. Schedules a follow-up consultation

---

## Resources

### Prompt Engineering Best Practices
1. **Be Specific**: Include details about format, tone, and length
2. **Provide Context**: Give background information and examples
3. **Use Structure**: Break complex tasks into steps
4. **Iterate**: Test and refine your prompts
5. **Consider Edge Cases**: Think about unusual inputs

### Useful Prompt Templates
```
Role-Based: "You are a [role] at [company]. [Task] for [audience]."
Step-by-Step: "Complete this task step by step: 1) [step] 2) [step] 3) [step]"
Format-Specific: "Provide your response in [format] with [specific requirements]"
```

### Next Steps
- Save your best prompts for use in Day 2-4 labs
- Experiment with different temperature settings (0.1-1.0)
- Try various models and compare responses

---

## Troubleshooting

**Common Issues:**
- **Inconsistent responses**: Lower temperature (0.2-0.5)
- **Responses too short**: Ask for specific length or detail level
- **Off-topic responses**: Add more context and constraints
- **Factual errors**: Include verification instructions in prompt
