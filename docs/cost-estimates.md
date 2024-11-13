# Cost Estimates

**Note:** This document is a **Work In Progress (WIP)** and is subject to updates as more information is gathered or changes occur in the implementation process. **Date**: November 13, 2024

This page provides an estimated monthly cost for implementing the "Dra. Jô" solution, detailing the components involved, cost justifications, and explanations for any free usage limits.

## Component Estimates

### Channel (WhatsApp)

- **Service:** WhatsApp via Twilio
- **Estimated Cost:** Costs are determined based on Meta’s conversation-based pricing, supplemented by Twilio’s per-message fees. The charges are split by conversation type, calculated per 24-hour conversation period initiated with a delivered message.
  - **Utility Conversations:** $0.008 per conversation, $0.005 per message.
  - **Authentication Conversations:** $0.0315 per conversation, $0.005 per message.
  - **Marketing Conversations:** $0.0625 per conversation, $0.005 per message.
  - **Service Conversations:** No charge for the first 1,000 conversations per month; then $0.005 per message.
- **Free Usage:** Twilio offers 1,000 free service conversations monthly, and a free evaluation period (until March 31, 2024) where messages are billed at $0.00.
- **Additional Features:** Twilio’s Engagement Suite can be added for enhanced engagement with link-shortening, click-tracking, and scheduling capabilities, billed at $0.015 per message, with the first 1,000 messages free monthly.

### Backend (Python, Flask and Docker)

- **Service:** Python, Flask and Docker
- **Estimated Cost:** Free
  - **Justification:** Python, Flask and Docker are open-source technologies, meaning there are no licensing or usage fees for their use. However, infrastructure costs may arise if these services are hosted on cloud platforms or require additional tools for deployment.
  - **Infrastructure Costs (if applicable):**
    - **Flask:** If deployed on cloud infrastructure (e.g., AWS, Azure, Google Cloud), costs will depend on the compute resources (e.g., EC2 instances, App Services) and storage (e.g., S3, EBS) required to host the Flask app. These costs can vary based on the scale of usage and the cloud provider’s pricing model.
    - **Docker:** Docker itself is free to use, but the cost can increase if using Docker Enterprise for additional features or if deploying on a cloud service (e.g., AWS ECS, Azure Kubernetes Service, or Google Kubernetes Engine), which incurs additional compute and storage charges.
  - **Limit:** No costs for the software itself, but hosting on private servers or cloud services may incur infrastructure-related costs, such as compute instances or storage fees.

### Computing (ECS)

- **Service:** Amazon Elastic Container Service (ECS)
- **Estimated Cost:** Varies based on resource usage (AWS Fargate or EC2)
  - **AWS Fargate Launch Type Model:** 
    - You pay for the amount of vCPU and memory resources that your containerized application requests. Costs are calculated from the time your container images are pulled until the ECS task terminates, rounded up to the nearest second. 
    - **Minimum Charge:** 1 minute.
    - **Pricing:** You only pay for what you use, as you use it. Charges are based on vCPU and memory usage, with no upfront fees or long-term commitments.
    - **Example:** If your application uses 0.5 vCPU and 1GB of memory for 30 minutes, you will be billed for those resources accordingly, rounded to the nearest second, with a minimum of 1 minute charge.
    - **Source:** [AWS Fargate Pricing](https://aws.amazon.com/fargate/pricing/)
  - **Amazon EC2 Launch Type Model:**
    - There are no additional charges for Amazon ECS itself. You pay for the AWS resources you create, such as EC2 instances, EBS volumes, or public IPv4 addresses.
    - **Pricing:** Based on the EC2 instances and associated resources you choose to run your application (e.g., CPU, memory, and storage). Pricing is based on the actual usage, with no minimum fees or upfront commitments.
    - **Example:** If you choose EC2 instances for container deployment, you will pay for the compute and storage resources based on the EC2 pricing model.
    - **Source:** [Amazon EC2 Pricing](https://aws.amazon.com/ec2/pricing/)
  - **Additional Information:** 
    - Amazon ECS on AWS Outposts operates the same pricing model as Amazon EC2, where you pay for EC2 capacity used in AWS Outposts.
    - **Free Usage:** No minimum usage or upfront fees, so costs scale with the usage of AWS resources like EC2 and EBS.
    - **Source:** [Amazon ECS Pricing Overview](https://aws.amazon.com/ecs/pricing/)

### Natural Language Processing (Gemini 1.5 Flash)

- **Service:** Gemini API via Google AI Studio
- **Estimated Cost:** Costs are determined based on token usage for inputs and outputs, with the following structure for free and pay-as-you-go tiers:
  - **Free Tier:** Offers testing access with 15 requests per minute (RPM), 1 million tokens per minute (TPM), and 1,500 requests per day (RPD).
    - **Free Usage:** No charge for input/output tokens or context caching; tuning is also free.
  - **Pay-as-you-go Pricing:**
    - **Standard Prompts (up to 128k tokens):**
      - Input tokens: $0.075 per 1 million tokens.
      - Output tokens: $0.30 per 1 million tokens.
      - Context caching: $0.01875 per 1 million tokens.
    - **Extended Prompts (over 128k tokens):**
      - Input tokens: $0.15 per 1 million tokens.
      - Output tokens: $0.60 per 1 million tokens.
      - Context caching: $0.0375 per 1 million tokens.
    - **Additional Storage for Context Caching:** $1.00 per 1 million tokens per hour.
- **Grounding with Google Search:** Available in the pay-as-you-go plan at $35 per 1,000 grounding requests, limited to 5,000 requests per day.
- **Tuning:** Free service; input/output pricing remains the same for tuned models.
- **Usage Limitations:** In the free tier, usage data may be collected to improve Google products, but in the pay-as-you-go tier, this data usage is excluded.

### Storage (DynamoDB and S3)

- **Services:** Amazon DynamoDB (NoSQL database) and Amazon S3 (object storage)
  
#### **DynamoDB**
- **Estimated Cost:** DynamoDB pricing depends on the capacity mode (on-demand or provisioned), read/write throughput, and storage used.
  - **On-Demand Pricing:** You pay per request for reads and writes.
    - **Reads:** $1.25 per WCU (write capacity unit) and $0.25 per RCU (read capacity unit) for every 1 million reads or writes.
    - **Storage:** $0.25 per GB per month.
  - **Provisioned Pricing:** Requires setting up read and write capacity units (RCUs/WCUs) in advance. Charges are incurred for provisioned capacity, whether used or not.
    - **RCUs/WCUs:** $1.25 per WCU per month, $0.25 per RCU per month.
    - **Storage:** $0.25 per GB per month.
  - **Free Usage:** 25 GB of storage and up to 200 million requests (read and write combined) are free every month under the AWS Free Tier for the first 12 months.
  
#### **S3**
- **Estimated Cost:** Amazon S3 charges are based on storage used, data transfer, and number of requests.
  - **Storage Cost:**
    - **Standard Storage:** $0.023 per GB for the first 50 TB/month.
    - **Intelligent-Tiering:** $0.023 per GB (standard) and $0.0125 per GB (frequent access).
  - **Requests and Data Retrieval:**
    - **PUT, COPY, POST, or LIST requests:** $0.005 per 1,000 requests.
    - **GET and all other requests:** $0.0004 per 1,000 requests.
    - **Data Transfer:** $0.09 per GB for data transferred out of S3 to the internet.
  - **Free Usage:** 5 GB of standard storage, 20,000 GET requests, and 2,000 PUT requests are free each month for the first 12 months with the AWS Free Tier.
  
#### **Additional Features:**
- **DynamoDB Streams:** Capture changes to DynamoDB tables for real-time event-driven applications, priced at $0.02 per 100,000 read requests.
- **S3 Versioning:** Allows you to keep multiple versions of an object, providing a backup mechanism at an additional storage cost.
- **S3 Glacier:** Low-cost archival storage for data retrieval after hours, with retrieval costs of $0.004 per GB.

### External APIs

- **Service:** Varies based on the integrations selected (e.g., payment gateways, authenticators, logging platforms, third-party APIs, etc.)
- **Estimated Cost:** The cost of external APIs depends heavily on the number of integrations, the type of service, and the usage volume (e.g., transaction volume, API calls, data throughput). As integrations increase, typically, the pricing will also scale accordingly. Some common external APIs and their pricing models:
  - **Payment Gateways (e.g., Stripe, PayPal):** Generally, these services charge a fee per transaction (e.g., 2.9% + $0.30 per successful transaction). These fees can vary depending on the region, payment method, and additional services such as fraud protection.
  - **Messaging APIs (e.g., Twilio, SendGrid):** These services usually have pricing tiers based on the number of messages sent (e.g., $0.0075 per SMS message sent via Twilio) or email volume (e.g., $15 per month for 50,000 emails via SendGrid).
  - **Geolocation APIs (e.g., Google Maps API):** Many geolocation services offer tiered pricing based on usage volume. For example, Google Maps API offers a free tier with 28,000 free loads per month for certain services, with additional charges for extra usage (e.g., $5 per 1,000 requests for places API).
- **Free Usage:** Some external APIs offer free tiers or trials, but these typically come with limitations in terms of the number of requests or volume. For instance, some payment processors may offer a small number of free transactions per month or a limited volume of free API calls for messaging services.
- **Scalability:** As more integrations are added, particularly for complex services like payments or CRM platforms, costs generally rise. Some external APIs also have volume-based pricing, where you pay a discounted rate per unit once your usage exceeds certain thresholds.

---

## Summary of Estimated Monthly Costs

The estimated monthly costs for the **"Dra. Jô"** solution include key components such as WhatsApp messaging, backend hosting, natural language processing, storage, and external API integrations. Costs are calculated based on usage expectations, scalability, and cloud-based infrastructure. Below is a summarized cost estimate for each component.

1. **WhatsApp Messaging (via Twilio)**
   - **Cost Range:** R$ 50 - R$ 300
   - **Key Assumptions:** 
     - This depends on message volume, conversation types, and usage limits. The estimated range assumes moderate usage (e.g., 5,000-15,000 conversations per month).
     - The free usage tier may cover part of the costs, especially in the early stages or trial phases.
     - Usage scale can vary, so the range accommodates both smaller and more active implementations.

2. **Backend Hosting (Python, Flask, Docker, ECS)**
   - **Cost Range:** R$ 100 - R$ 500
   - **Key Assumptions:** 
     - Estimated for hosting the application and running ECS tasks (AWS Fargate/EC2). 
     - The lower end assumes small-scale usage with minimal resources, while the higher range reflects scalability for more active sessions and increased demand.
     - Variable costs for storage and resource consumption on ECS based on the number of requests and container usage.

3. **Natural Language Processing (Gemini 1.5 Flash via Google AI Studio)**
   - **Cost Range:** R$ 200 - R$ 1,000
   - **Key Assumptions:**
     - Based on token usage for queries, this is heavily tied to conversation complexity and volume.
     - Small-scale usage may fall closer to the lower end, while scaling for more frequent and complex NLP interactions will push costs toward the higher end.
     - Tuning and grounding features can drive costs up, but are optional and used selectively based on user interactions.

4. **Storage (DynamoDB and S3)**
   - **Cost Range:** R$ 50 - R$ 200
   - **Key Assumptions:**
     - Costs depend on data storage needs for user interactions and message histories, with additional charges for read/write throughput.
     - DynamoDB costs will vary with request volume (read and write operations) and storage needs, while S3 storage is tied to data volumes (e.g., message logs, media files).
     - The low end assumes moderate usage, while the higher end accounts for larger datasets, frequent access, and longer storage periods.

5. **External API Integrations**
   - **Cost Range:** R$ 100 - R$ 500
   - **Key Assumptions:**
     - This covers external services such as payment gateways (e.g., Stripe/PayPal), messaging APIs (e.g., SendGrid/Twilio), and geolocation services.
     - Costs vary depending on the number of integrations and transaction volume. 
     - The range assumes usage for a mix of basic and premium services, with API costs scaling with usage. For example, high transaction volumes or frequent API calls will incur higher fees.

---

### **Total Estimated Monthly Cost Range**

Based on the components above, the total estimated monthly cost for the **"Dra. Jô"** solution is approximately:

- **Low-End Estimate:** R$ 500 - R$ 800 per month
  - This estimate is suited for a lower-traffic, early-stage implementation or prototype phase with limited scale.

- **Mid-Range Estimate:** R$ 800 - R$ 1,500 per month
  - Suitable for an active user base with moderate traffic, data usage, and integrations.

- **High-End Estimate:** R$ 1,500 - R$ 2,500+ per month
  - This is for larger-scale operations, with high traffic, multiple API integrations, and extensive NLP processing, and will scale further as user interactions grow.

---

## Source

- [Twilio WhatsApp Pricing](https://www.twilio.com/en-us/whatsapp/pricing)
- [Gemini 1.5 Flash API Pricing](https://ai.google.dev/pricing#1_5flash)
- [Amazon DynamoDB Pricing](https://aws.amazon.com/dynamodb/pricing/), [Amazon S3 Pricing](https://aws.amazon.com/s3/pricing/)
- For external APIs, pricing details depend on the specific provider. It’s essential to consult the official API documentation or pricing pages for precise cost estimation.

## Final Considerations

- **Scalability:** The final cost may vary significantly as usage grows, with increased interactions and additional resource requirements.
- **Free Usage Limits:** Services offer free usage tiers for new users, but once the free tier limits are exceeded, costs will increase.
- **Variable Estimates:** The costs may adjust based on actual data consumption, message volume, and interactions with external APIs.
- **Dollar**: Pricing is in U.S. dollars, which can fluctuate depending on exchange rates if the service is used internationally. The actual cost may vary depending on the region and applicable taxes.

---

This estimate provides an overview of the expected costs for implementing the system and may be adjusted as the platform grows and more resources are utilized.
