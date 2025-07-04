# AWS Certified AI Practitioner
## 0. Resources
- [Ultimate AWS Certified AI Practitioner AIF-C01](https://www.udemy.com/course/aws-ai-practitioner-certified/)
## 1. Introduction
1. brief AI history
    1. 1950s
        1. Alan Turing: "Turing Test"
        2. John McCarthy: "Artificial Intelligence"
    3. 1970s: MYCIN
    4. 1990s: Machine Learning and Data Mining
    5. 1997: Deep Blue
    6. 2010s: AlphaGO
    7. 2020s: AI in everyday life
2. AI use cases
    1. Transcribe and Translate
    2. Transportation
    3. Recognition and Generation
    4. Coding
    5. Medical Diagnosis, Fraud Detection
3. AWS Overview
    1. Cloud is the on demand delivery of IT resources
    2. Private Cloud, Public Cloud, Hybrid Cloud
    3. Five Characteristic
        1. On-demand self service
        2. Broad network access
        3. Multi-tenancy and resource pooling
        4. Rapid elasticity and scalability
        5. Measured service
    4. Six Advantages
        1. Trade capital expense for operation expense
        2. Benefit from massive economies of scale
        3. Stop guessing capacity
        4. Increase speed and agility
        5. Stop spending money running and maintaining data centers
        6. Go global in minutes
    5. Types of Cloud
        1. Infrastructure as a Service (IaaS)
        2. Platform as a Service (PaaS)
        3. Software as a Service (SaaS)
    6. Pricing of the AWS
        1. Compute
        2. Storage
        3. Data transfer **OUT** of the Cloud
    7. AWS Regions
        1. Region: cluster of data centers, has 3 to 6 AZ
        2. Availability Zone: each AZ has one or more data centers
        3. Points of Presence (Edge Location)
    8. Share Responsibility Model
        1. AWS: Responsibility for the security of hte cloud
        2. User: Responsibility for the security in the cloud

## GenAI and Amazon Bedrock
1. Generative AI
    1. GenAI generate new data that is similar to the data it was trained on
    2. Data >(train) Foundation Model (generate)> new Data
    3. Large Language Models: Foundation Models focus on generate coherent連貫的 human-like text
    4. Non-deterministic: the generated text may be different even with same prompt
    5. Diffusion Model
    6. GenAI Concepts
        1. Tokenization: raw text into a sequence of tokens
            1. word-base
            2. subword
        2. Context Window: maximum input tokens
        3. Embeddings: create vectors out of text, images, audio, etc.
            1. vector have a high dimensionality to capture many features for input

2. Bedrock is a PaaS
    1. Fully-managed by Amazon
    2. Unified API
    3. Out-of-the box feature: Fine-tuning, RAG, Agent, etc.
    4. Security, Privacy, Governance and Responsible feature
3. Bedrock Hands-On
    1. `Configure` > `Model access`:select and request access means agree to Terms
    2. `Test`: 
        1. to access AI models through a web browser
        2. can compare multiple models at the same time
4. Criteria for choosing Foundation Model
    1. Model types, capability, performance, context windows
    2. Level of customization, licensing agreement
    3. Price
5. Custom models
    1. `Tune` > `Custom models`: Distillation蒸餾, Fine-tuning, Continued pre-training
    2. Fine-Tuning
        1. Fine-Tuning will change the weight of the base foundation model
        2. Training data must adhere to a specific format and store in Amazon S3
        3. It uses **labeled data** / prompt-response pairs to improve the performance on a particular knowledge
        4. Single-Turn Messaging training data example
        ```json
        {
            "system": "You are an helpful assistant.",
            "message": [
                {
                    "role": "user",
                    "content": "what is AWS"
                },
                {
                    "role": "assistant",
                    "content": "it's Amazon Web Services."
                }
            ]
        }
        ```
        5. Multi-Turn Messaging: user > assistant > user > assistant > ...
    3. Continued Pre-Training
        1. It uses unlabeled data to make a model expert in a specific domain

6. Evaluating a Module
    1. `Assess` > `Evaluation`
    2. Question > Compare Benchmark answers and Generate answer > Evaluating by human, metrics or models
    3. Automated Metrics
        1. Recall-Oriented Understudy for Gisting Evaluation (ROUGE)
            1. for evaluating summarization and translation
            2. ROUGE-N: measure the number of matching n-grams 測量有多少n個連接在一起的單字
                1. e.g. ROUGE-2 
                2. `Pen Pineapple Apple Pen` vs `Pen Apple Apple Pen`
                3. only `Apple Pen` count as one matching
            3. ROUGE-N: longest common subsequence
        2. Bilingual Evaluation Understudy
            1. for evaluating translation
            2. Consider both precision and penalizes懲罰 too much brevity簡潔
        3. BERTScore: Semantic similarity
        4. Perplexity: how well the model predicts the next token (lower is better)
    4. Business Metrics
        1. User Satisfaction
        2. Average Revenue Per User (ARPU) 每使用者平均收入
        3. Cross-Domain Performance: model's ability to perform cross different domains
        4. Conversion Rate 轉換率
        5. Efficiency
        
7. Knowledge bases
    1. `Build` > `Knowledge bases`
    2. It is used for Retrieval Augmented Generation (RAG)
    3. Data Sources (split)> Document Chunks > Embedding Model (save)> Vector Database
    4. Data Sources: Amazon S3, Confluence, MS SharePoint, Salesforce, etc.
    5. Vector Database
        1. Amazon OpenSearch
        2. Amazon Aurora PostgreSQL
        3. Amazon Neptune
        4. 3rd party vector database: MongoDB, Pinecone, etc.
    6. Use Case
        1. Customer Service
        2. Legal Research
        3. Healthcare

8. GuardRails
    1. `Build` > `GuardRails`
    2. It's mainly used for filter undesirable and harmful content
    3. It can also
        1. remove Personally Identifiable Information (PII)
        2. Reduce hallucination

9. Agents
    1. `Build` > `Agents`
    2. Agents workflow
        1. Task (send)> Agent (Models) >(gather) data (send)> Models > Chain of Thought
        2. Chain of Thought >(call) Action Group >(generate) Result
        3. Result (send)> Agent (Models) (send task+result)> Models > Final Response
    4. Action Group: API Call or Function

10. Bedrock with AWS CloudWatch
    1. `Configure` > `Settings` > Model Invocation Logging
    2. send invocation log to S3 and CloudWatch Log
    3. Use CloudWatch Metric to get more detail info

11. Pricing
    1. On-Demand
        1. Text Models: input/output token
        2. Embedding Models: input token
        3. Image Models: image generated
    2. Batch
        1. Output will be a single file in Amazon S3
        2. up to 50% discount
    3. Provisioned Throughput
        1. Purchase Models for a certain time
    4. Improvement techniques cost (cheap to expensive)
        1. Prompt Engineering
        2. RAG
        3. Fine-tuning
        4. Continued Pre-Training
        