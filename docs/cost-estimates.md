# Cost Estimates

**Note:** This document is a **Work In Progress (WIP)** and is subject to updates as more information is gathered or changes occur in the implementation process.

This document provides an estimated monthly cost for implementing the "Dra. Jô" solution, detailing the components involved, cost justifications, and explanations for any free usage limits.

## Monthly Cost Estimate

### 1. **Channel (WhatsApp)**
- **Service:** WhatsApp via Twilio
- **Estimated Cost:** Depends on the volume of messages sent and received.
  - **Cost per message:** Twilio charges a fee per message sent and received, with rates varying depending on the number of messages and the destination. The average cost is R$0.20 per message.
  - **Example:** If 10,000 messages are sent per month, the cost would be approximately R$2,000.00.
- **Free Usage:** Twilio offers an initial free tier with a limited number of messages for testing. After reaching this limit, the service becomes paid.

### 2. **Backend (Flask and Docker)**
- **Service:** Flask (Python) and Docker (Containers)
- **Estimated Cost:** Free
  - **Justification:** Flask and Docker are open-source technologies and free to use. However, costs may arise in the production environment depending on infrastructure usage.
  - **Limit:** None, as long as the services are hosted on private servers or infrastructure with no additional costs. If hosted on the cloud, costs will be related to infrastructure.

### 3. **Cloud Infrastructure (AWS)**
- **Service:** Amazon Web Services (AWS)
- **Estimated Cost:** Approximately R$500.00 to R$2,000.00 per month, depending on usage.
  - **Cost per Service:**
    - **EC2 (Computing):** Cost of an EC2 instance to run the backend (starting at R$150.00 per month for a small instance).
    - **DynamoDB:** Charges on DynamoDB are based on read and write capacity, as well as storage. A small-scale database may incur costs ranging from R$100.00 to R$500.00 per month, depending on workload.
    - **S3:** The storage cost on S3 depends on the volume of data stored. For a small volume of files (images, videos), the cost may vary between R$50.00 and R$200.00 per month.
- **Free Usage:** AWS offers a free tier for new users, which includes limited resources for EC2, DynamoDB, and S3.

### 4. **API Integration (Twilio)**
- **Service:** Twilio for WhatsApp integration
- **Estimated Cost:** Charges based on the number of messages and interactions.
  - **Cost per sent and received message:** R$0.20 per message.
  - **Example:** For 10,000 messages per month, the cost would be approximately R$2,000.00.
- **Free Usage:** There is no ongoing free usage for this service, but Twilio may offer limited free usage for testing.

### 5. **Natural Language Processing (Gemini 1.5 Flash)**
- **Service:** Gemini 1.5 Flash
- **Estimated Cost:** Approximately R$1,000.00 to R$3,000.00 per month, depending on the volume of queries and model complexity.
  - **Justification:** The cost depends on request volume and computational load. Platforms like Gemini typically charge based on API calls or computational usage.
- **Free Usage:** There is no unlimited free usage for this technology, but the service may offer a limited free tier for testing.

### 6. **Data Storage (DynamoDB and S3)**
- **Service:** Amazon DynamoDB (NoSQL) and Amazon S3 (File Storage)
- **Estimated Cost:** Approximately R$100.00 to R$500.00 per month, depending on the volume of data stored and operations performed.
  - **DynamoDB:** Costs are based on read and write operations, as well as storage.
  - **S3:** The storage cost is based on the amount of data stored and data transfer.
- **Free Usage:** AWS offers a free tier for DynamoDB and S3 with usage limits.

### 7. **External APIs**
- **Service:** External APIs (Payment, Scheduling, etc.)
- **Estimated Cost:** Depends on the volume of interactions and the type of service contracted.
  - **Example:** A payment API may charge per transaction or on a monthly basis, ranging from R$0.50 to R$5.00 per processed transaction.
- **Free Usage:** Some APIs may offer free tiers with usage limits or reduced fees for testing.

### 8. **Monitoring and Logs**
- **Service:** Monitoring and logging tools (CloudWatch, ELK Stack, etc.)
- **Estimated Cost:** Approximately R$100.00 to R$500.00 per month, depending on the amount of data monitored and stored.
- **Free Usage:** AWS CloudWatch offers a free tier, limited to 5GB of logs per month.

---

## Summary of Estimated Monthly Costs

| Component                    | Estimated Cost (R$)       |
|------------------------------|---------------------------|
| Twilio (WhatsApp)             | R$2,000.00                |
| AWS (EC2, DynamoDB, S3)       | R$500.00 to R$2,000.00    |
| Gemini Flash                  | R$1,000.00 to R$3,000.00  |
| External APIs                 | R$0.00 to R$500.00        |
| Monitoring and Logs           | R$100.00 to R$500.00      |
| **Total Estimated**           | **R$3,600.00 to R$8,000.00** |

---

## Final Considerations

- **Scalability:** The final cost may vary significantly as usage grows, with increased interactions and additional resource requirements.
- **Free Usage Limits:** Services offer free usage tiers for new users, but once the free tier limits are exceeded, costs will increase.
- **Variable Estimates:** The costs may adjust based on actual data consumption, message volume, and interactions with external APIs.

This estimate provides an overview of the expected costs for implementing the system and may be adjusted as the platform grows and more resources are utilized.
