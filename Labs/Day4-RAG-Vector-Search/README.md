# Day 4 Lab: RAG and AI Vector Search with Azure AI Foundry

## Lab Overview
**Prerequisites:** Days 1-3 completed, Azure AI Foundry project active  
**Objective:** Implement Retrieval-Augmented Generation (RAG) using Azure AI Search and vector embeddings for intelligent document retrieval

---

## Setup Instructions

### Step 1: Create Azure AI Search Service
1. Navigate to Azure Portal → **Create a resource**
2. Search for **Azure AI Search**
3. Configure:
   - Name: `manulife-search-service`
   - Resource Group: `manulife-hackathon-rg`
   - Location: Same as your other resources
   - Pricing tier: **Standard** (for vector search capabilities)

### Step 2: Set Up Storage Account
1. Create **Azure Storage Account**:
   - Name: `manulifedocs[random]`
   - Performance: Standard
   - Replication: LRS (Locally redundant storage)
   - Enable hierarchical namespace (Data Lake Gen2)

### Step 3: Prepare Sample Documents
Create a container called `knowledge-base` and upload sample Manulife documents (we'll use pre-created sample documents).

---

## Lab Task Overview

### Exercise 1: Document Preparation and Ingestion

#### Task 1.1: Review Sample Manulife Knowledge Base
We've prepared realistic Manulife policy documents for the lab:

**Sample Policy Documents:**

1. **Life Insurance Policy Guide (life-insurance-guide.md)**
2. **Travel Insurance FAQ (travel-insurance-faq.md)**  
3. **Investment Products Overview (investment-products.md)**
4. **Claims Process Manual (claims-process.md)**
5. **Customer Service Procedures (customer-service.md)**

#### Task 1.2: Upload Documents to Storage
1. Navigate to your storage account
2. Create container: `knowledge-base`
3. Upload the provided sample documents
4. Set container access level to **Blob (anonymous read access for blobs only)**

#### Task 1.3: Set Up Azure AI Search Service and Import Data
1. Navigate to your Azure AI Search service in the Azure portal
2. Click on **Import data**
3. Select **Azure Blob Storage** as the data source
4. Connect to your storage account and select the `knowledge-base` container
5. Configure the cognitive skills:
   - Enable OCR if you have any image-based documents
   - Enable **Extract key phrases** and **Generate vector embeddings**
   - Select the Azure AI Service (Azure OpenAI) where your embedding model is deployed
   - Choose `text-embedding-ada-002` as the embedding model

6. Configure the index with the following fields:
   - **id** (Key, Retrievable)
   - **content** (Searchable, Retrievable)
   - **title** (Searchable, Retrievable, Filterable)
   - **category** (Filterable, Facetable, Retrievable)
   - **vectorized_content** (Vector, Dimensions: 1536)
```

### Exercise 2: Vector Search Implementation

#### Task 2.1: Configure Vector Search in Azure AI Search
1. In your search service, the index was created during data import with vector search capabilities
2. Review the index structure:
   - Note how the text content has been automatically vectorized
   - Vector fields are optimized for semantic search using the HNSW algorithm
   - Default vector search parameters are already configured (cosine similarity)

3. Examine the Search Explorer:
   - Navigate to your search service in the Azure portal
   - Click on **Search explorer**
   - Try a few basic searches to verify your documents are indexed

#### Task 2.2: Test Hybrid Search in Search Explorer
Try different search modes in the Search Explorer:

1. **Keyword Search**: 
   - Search query: `premium calculation life insurance`
   - Keep the default search settings

2. **Vector Search**:
   - Enable **Semantic search**
   - Set **Semantic configuration** to default
   - Search query: `How is my life insurance premium calculated?`

3. **Hybrid Search**:
   - Enable both **Keyword** and **Semantic** search
   - Add filter: `category eq 'life-insurance'`
   - Search query: `What factors determine my life insurance rate?`
```

#### Task 2.3: Test Vector Search Capabilities
Test various search scenarios:

**Test Query 1: Simple Product Question**
```
Query: "What are the benefits of whole life insurance?"
Expected: Relevant sections from life insurance documents
```

**Test Query 2: Process Question**
```
Query: "How do I file a travel insurance claim?"
Expected: Step-by-step process from claims documentation
```

**Test Query 3: Complex Comparison**
```
Query: "Compare term life vs whole life insurance for a 35-year-old"
Expected: Comparative information from multiple documents
```

### Exercise 3: RAG Implementation Using Azure OpenAI Chat Playground

#### Task 3.1: Connect Azure AI Search to Chat Playground
1. Navigate to the Azure OpenAI Studio in your browser
2. Select **Chat** from the left menu to open the Chat Playground
3. Click on **Add data** in the chat assistant setup panel
4. Select **Add a data source** and choose **Azure AI Search**
5. Configure your data connection:
   - Select your Azure AI Search service
   - Choose the index you created earlier
   - Select **Hybrid (vector + text)** as the search type
   - Choose fields to search on: `content` and `vectorized_content`
   - Set fields to retrieve: `title`, `content`, `category`
6. Click **Save and close**

#### Task 3.2: Configure Chat Settings and System Message
1. Configure the chat settings:
   - Set **Temperature** to 0.3 for more consistent responses
   - Enable **Retrieval augmented generation**
   - Set **Top results** to 5

2. Edit the system message to create a Manulife customer service assistant:
```
You are a helpful Manulife customer service assistant. Use the provided context from the knowledge base to answer customer questions accurately and helpfully.

Follow these guidelines:
- Answer based primarily on the provided context
- If information is not in the context, say so clearly
- Provide specific references to policy sections when relevant
- Maintain a professional, helpful tone
- Include relevant policy numbers or document references when available

When providing answers:
1. Be concise but thorough
2. Use bullet points for multi-step processes
3. Offer to connect customers with specialists for complex questions
4. Always cite the source documents you're using
```

#### Task 3.3: Test the RAG System with Customer Queries
Test your RAG implementation with these sample queries:

1. **Simple Product Question**:
   ```
   "What are the benefits of whole life insurance?"
   ```
   
   Expected: The system should retrieve information from the life insurance policy guide.

2. **Process Question**:
   ```
   "How do I file a travel insurance claim?"
   ```
   
   Expected: The system should provide step-by-step instructions from the travel insurance FAQ.

3. **Complex Comparison**:
   ```
   "Compare term life vs whole life insurance for a 35-year-old"
   ```
   
   Expected: The system should compile information from multiple documents.

#### Task 3.4: Use Evaluation Dataset for Quality Assessment
Use the evaluation dataset from Day 2 to systematically test your RAG system:

1. Open the evaluation dataset file:
   ```
   ../Day2-Azure-AI-Foundry-Overview/evaluation-dataset.json
   ```

2. Filter for relevant scenarios:
   - Focus on `product_knowledge`, `claims_processing`, `policy_details`, and `retirement_planning` categories
   - Try 3-5 scenarios from each category

3. For each test scenario:
   - Paste the input query into your Chat Playground
   - Compare the generated answer with the expected output
   - Examine the retrieved documents shown in the chat interface
   - Note which documents were retrieved and their relevance

4. Create a simple evaluation spreadsheet with these columns:
   - Scenario ID
   - Query
   - Retrieved Documents
   - Answer Quality (1-5)
   - Faithfulness to Documents (1-5)
   - Notes/Observations

### Exercise 4: Integration with Copilot Studio

#### Task 4.1: Connect Azure OpenAI Service to Copilot Studio
1. Navigate to Copilot Studio portal (https://copilot.microsoft.com)
2. Open your existing Copilot from Day 3 or create a new one
3. Go to the **Configurations** tab
4. Select **Azure OpenAI** from the available connections
5. Configure the connection:
   - Enter your Azure OpenAI resource name
   - Enter your API key
   - Set the deployment name for your GPT-4 model
   - Test the connection

#### Task 4.2: Add Azure AI Search as a Data Source
1. Navigate to **Data** in the Copilot Studio menu
2. Click on **+ Add** and select **Azure AI Search**
3. Configure the connection:
   - Enter your Azure AI Search service endpoint
   - Enter your API key
   - Select the index you created earlier
   - Set the search options:
     - Vector search: Enabled
     - Top results: 5
     - Filter criteria: None (initially)
4. Click **Save and train** to update your Copilot

#### Task 4.3: Create Custom Topics for Document-Based Answers
1. Go to **Topics** in the Copilot Studio menu
2. Create a new topic called "Policy Information"
3. Add trigger phrases:
   - "Tell me about life insurance"
   - "How do travel insurance claims work"
   - "What investment products do you offer"
   - "Explain the claims process"

4. In the authoring canvas, add a **Message** node with this text:
```
I'll check our policy documentation for you.

Based on Manulife's policy documentation, here's what I found:

{{GetPolicyInfo.response}}

This information comes from our official policy documents. Would you like me to explain any specific part in more detail?
```

5. Add a flow step using the **Get data from AI Search** action:
   - Configure the action with:
     - Name: GetPolicyInfo
     - Query: Use the "user message" variable
     - Add attribution: Enabled
     - Show thinking: Disabled

6. Add conditional branches for handling cases when information is not found

---

## Evaluation Criteria

### Technical Performance
- **Retrieval Accuracy**: Relevant documents retrieved for queries
- **Answer Quality**: Accurate, helpful, and complete responses
- **Response Time**: Fast retrieval and generation (<3 seconds)
- **Scalability**: Handle concurrent users and large document corpus

### Business Value
- **Customer Satisfaction**: Improved self-service capabilities
- **Agent Efficiency**: Reduced escalation to human agents
- **Knowledge Coverage**: Comprehensive information retrieval
- **Compliance**: Accurate policy and regulatory information

### System Reliability
- **Availability**: High uptime and fault tolerance
- **Consistency**: Reliable results across similar queries
- **Security**: Proper access controls and data protection
- **Monitoring**: Comprehensive logging and alerting

---

## Best Practices

### RAG Architecture
1. **Chunk Size Optimization**: Balance context and specificity (1000-2000 tokens)
2. **Overlap Strategy**: Ensure important information isn't split (10-20% overlap)
3. **Hybrid Search**: Combine keyword and vector search for best results
4. **Metadata Enrichment**: Include document type, date, category for filtering
5. **Quality Gates**: Implement confidence thresholds and fallback strategies

### Vector Search Optimization
1. **Embedding Model Selection**: Use domain-specific or fine-tuned models
2. **Index Configuration**: Optimize HNSW parameters for your data
3. **Query Expansion**: Enhance queries with synonyms and related terms
4. **Reranking**: Apply additional scoring after initial retrieval
5. **Cache Strategy**: Cache frequent queries and embeddings

### Production Considerations
1. **Data Privacy**: Ensure sensitive information is properly protected
2. **Audit Trail**: Log all searches and responses for compliance
3. **Performance Monitoring**: Track latency, accuracy, and user satisfaction
4. **Cost Management**: Monitor token usage and API calls
5. **Continuous Improvement**: Regular evaluation and optimization

---

## Resources

### Documentation
- [Azure AI Search Vector Search](https://docs.microsoft.com/azure/search/vector-search-overview)
- [RAG with Azure OpenAI](https://docs.microsoft.com/azure/ai-services/openai/concepts/use-your-data)
- [Azure AI Foundry RAG Implementation](https://docs.microsoft.com/azure/ai-foundry/concepts/retrieval-augmented-generation)

### Sample Code
- Azure AI Search Python SDK examples
- OpenAI embeddings implementation
- RAG pipeline templates
- Evaluation frameworks

### Tools and Libraries
- LangChain for RAG orchestration
- Azure SDK for Python/JavaScript
- Semantic Kernel for .NET
- Vector database comparisons

---

## Troubleshooting

### Common Issues
- **Poor retrieval quality**: Adjust chunk size, improve metadata, tune search parameters
- **Slow response times**: Optimize index configuration, implement caching, reduce embedding dimensions
- **Inconsistent answers**: Improve prompt engineering, add quality gates, enhance document preprocessing
- **High costs**: Optimize embedding generation, implement smart caching, tune retrieval parameters

### Performance Optimization
- **Embedding Efficiency**: Batch embedding generation, cache common queries
- **Search Optimization**: Use filters effectively, implement result caching
- **Generation Efficiency**: Optimize prompt length, use appropriate model sizes
- **System Architecture**: Implement proper load balancing and scaling strategies

### Quality Improvement
- **Document Quality**: Regular content audits, standardized formatting
- **Retrieval Tuning**: A/B testing different parameters, user feedback integration
- **Answer Generation**: Prompt optimization, fact-checking mechanisms
- **User Experience**: Clear source attribution, confidence indicators, fallback options

---

## Next Steps

### Production Deployment
1. **Security Review**: Complete security assessment and penetration testing
2. **Performance Testing**: Load testing and capacity planning
3. **User Training**: Train customer service team on new capabilities
4. **Gradual Rollout**: Phased deployment with monitoring and feedback collection

### Continuous Improvement
1. **Analytics Implementation**: Set up comprehensive monitoring and analytics
2. **Feedback Loops**: Implement user feedback collection and analysis
3. **Model Updates**: Plan for regular model and knowledge base updates
4. **Integration Expansion**: Connect additional data sources and systems

This completes the comprehensive RAG and Vector Search lab for Day 4 of your Manulife Hackathon!
