# Evaluation Dataset for Azure AI Foundry Agent

This folder contains a comprehensive evaluation dataset (`evaluation-dataset.json`) designed for testing and evaluating AI agents in a financial services context. The dataset consists of 20 carefully crafted customer service scenarios that mimic real-world interactions between customers and Manulife representatives.

## Dataset Structure

The evaluation dataset is structured as a JSON file with the following format:

```json
{
  "title": "Manulife Customer Service Agent Evaluation Dataset",
  "description": "A comprehensive set of customer service scenarios for evaluating Azure AI Foundry agents",
  "version": "1.0",
  "createdDate": "2025-07-03",
  "scenarios": [
    {
      "id": "scenario_001",
      "category": "product_knowledge",
      "input": "Customer question text",
      "expectedOutput": "Ideal agent response",
      "evaluationCriteria": {
        "criterion1": "Description of what to evaluate",
        "criterion2": "Description of what to evaluate",
        "criterion3": "Description of what to evaluate"
      },
      "difficulty": "basic|intermediate|advanced"
    },
    // More scenarios...
  ]
}
```

## Using the Evaluation Dataset

### With Azure AI Foundry Evaluation Framework

1. Navigate to **Evaluation** → **Create new evaluation**
2. Upload the `evaluation-dataset.json` file or paste relevant scenarios
3. Configure evaluation metrics to match the criteria in the dataset
4. Run evaluation against your agent to measure performance

### For Manual Testing

1. Use the scenarios as a structured way to test your agent
2. Compare the agent's responses with the expected outputs
3. Score each response based on the provided evaluation criteria
4. Track performance across different categories and difficulty levels

## Scenario Categories

The dataset includes scenarios across multiple categories important for financial services:

- **product_knowledge**: Testing agent's knowledge of insurance and investment products
- **customer_retention**: Evaluating how the agent handles cancellation requests
- **claims_processing**: Testing guidance on submitting and tracking claims
- **retirement_planning**: Evaluating financial planning advice quality
- **policy_details**: Testing knowledge of coverage specifics
- **compliance**: Evaluating regulatory compliance in responses
- **beneficiary_changes**: Testing process guidance for policy changes
- **technical_support**: Evaluating troubleshooting capabilities
- **complaint_handling**: Testing how agent manages customer dissatisfaction
- **premium_payments**: Evaluating knowledge of payment processes
- **life_events**: Testing response to major customer life changes
- **international_coverage**: Evaluating knowledge of cross-border insurance issues
- **fraud_prevention**: Testing security awareness and customer protection
- **product_comparison**: Evaluating ability to explain product differences
- **policy_reinstatement**: Testing knowledge of recovery processes
- **digital_services**: Evaluating guidance for online account management
- **group_benefits**: Testing knowledge of employer-provided insurance
- **underwriting**: Evaluating explanation of risk assessment processes
- **tax_information**: Testing knowledge of tax implications for financial products
- **foreign_residency**: Testing guidance for customers moving internationally

## Difficulty Levels

Scenarios are categorized into three difficulty levels:

- **Basic**: Straightforward questions with factual answers
- **Intermediate**: More complex scenarios requiring process knowledge
- **Advanced**: Nuanced situations requiring deep product knowledge, compliance awareness, or personalization

## Extending the Dataset

You can extend this dataset by:

1. Adding new scenarios to cover additional product lines
2. Creating industry-specific variations for different business units
3. Developing scenarios for specialized services like wealth management
4. Adding multilingual scenarios for language capabilities testing

## Integration with RAG Systems

This dataset is also used in Day 4's RAG implementation lab to:

1. Test retrieval quality by comparing retrieved documents with expected knowledge
2. Evaluate answer generation based on retrieved content
3. Compare performance between traditional and RAG-enhanced agents
4. Identify knowledge gaps in the document corpus
