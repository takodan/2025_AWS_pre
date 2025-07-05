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

## Artificial Intelligence and Machine Learning
1. Artificial Intelligence > Machine Learning > Deep Learning > Generative AI
2. AI components
    1. Data Layer
    2. ML Framework and Algorithm Layer
    3. Model Layer
    4. Application Layer
3. Machine Learning 
    1. Make predictions based on data
    2. Training Data
        1. Garbage in, Garbage out
        2. Labeled Data vs Unlabeled Data
        3. Structured Data vs Unstructured Data (e.g. text and image)
    3. Machine Learning types
        1. Supervised Learning
            1. Training, Validation, Test
                1. used Labeled Data
                2. 60~80% of the dataset for Training, 10~20% for Validation, 10~20% for Test
            2. Feature Engineering
                1. select and transform raw data into meaningful features for training
                2. Extraction/Creation, Selection, Transformation
            3. possible tasks:
                1. Regression: used to predict a numeric value
                2. Classification: used to predict the categorical label
                    1. Binary: 0, 1
                    2. Multi-class: more then two class
                    3. Multi-label: one object can have multiple class
        2. Unsupervised Learning
            1. use Unlabeled Data
            2. possible tasks:
                1. Clustering: Used to group similar data together
                2. Association rule learning
                3. Anomaly Detection
        3. Semi-supervised Learning
            1. used small amount of labeled data to train the model
            2. used the model to label Unlabeled Data (pseudo-labeling)
            3. re-train the model on the mix data
        4. Self-Supervised Learning
            1. create Pretext Task (used part of dataset to predict another part) to create Pseudo-Label data
            2. train the model on these Pseudo-Label data to create a Representation of the dataset
            3. used small amount of labeled data to Fine-tune the model
            4. now the model can perform the Downstream Task
    

4. Deep Learning
    1. Uses the brain like structure to create Neural Networks to process patterns in the data
    2. Input Layer > Hidden Layers > Output Layers
5. Generative AI
    1. Subset of Deep Learning
    2. Focus on generating data

## GenAI and Amazon Bedrock
1. Generative AI
    1. GenAI generate new data that is similar to the data it was trained on
    2. Unlabeled Data >(train) Foundation Model (generate)> new Data
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

2. Amazon Bedrock 
    1. Amazon Bedrock is a PaaS
    1. Fully-managed by Amazon
    2. Unified API
    3. Out-of-the box feature: Fine-tuning, RAG, Agent, etc.
    4. Security, Privacy, Governance and Responsible feature
3. Amazon Bedrock Hands-On
    1. `Configure` > `Model access`:select and request access means agree to Terms
    2. `Test`: 
        1. to access AI models through a web browser
        2. can compare multiple models at the same time
4. Criteria for choosing Foundation Model
    1. Model types, capability, performance, context windows
    2. Level of customization, licensing agreement
    3. Price
5. Amazon Bedrock Custom models
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

6. Amazon Bedrock Evaluating a Module
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
        
7. Amazon Bedrock Knowledge bases
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

8. Amazon Bedrock GuardRails
    1. `Build` > `GuardRails`
    2. It's mainly used for filter undesirable and harmful content
    3. It can also
        1. remove Personally Identifiable Information (PII)
        2. Reduce hallucination

9. Amazon Bedrock Agents
    1. `Build` > `Agents`
    2. Agents workflow
        1. Task (send)> Agent (Models) >(gather) data (send)> Models > Chain of Thought
        2. Chain of Thought >(call) Action Group >(generate) Result
        3. Result (send)> Agent (Models) (send task+result)> Models > Final Response
    4. Action Group: API Call or Function

10. Amazon Bedrock with AWS CloudWatch
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

## Prompt Engineering
1. optimizing prompt to enhance the output of models
2. Prompting element
    1. Instructions: a task for the model
    2. Context: external information to guide the model
    3. Input data: the input for which you want a response
    4. Output Indicator: the output type or format
3. Negative Prompting
    1. explicitly instruct what not to include
    2. helps to
        1. Avoid unwanted content
        2. Maintain focus
        3. Enhance Clarity
    3. add into Instructions or Output Indicator
4. Prompt Engineering Techniques
    1. Zero-Shot:without providing any example, fully rely on the model
    2. Few-Shot: provide example to the model to guide its output
    3. Chain of Thought: divide the task in to a sequence of steps
5. Model Configurations
    1. System Prompts: how the model should behave and reply
    2. Temperature: creativity of the model
        - lower means more conservative, higher means more creative
    3. Top P: limit the probable words by the possibility cap
        - e.g. 0.25 means consider the 25% most likely words
    4. Top K: limit the the number of probable words 
    5. Response length: maximum output length
    6. Stop Sequences: tokens that signal the model to stop
    7. The **output latency** is **not impacted** by Temperature, Top T, and Top K


## Amazon Q
1. Amazon Q are SaaS
2. Amazon Q Business
    1. GenAI assistant for employees managed by Amazon
    2. DataConnectors: RAG
    3. Plugins: allows Q Business to interact with 3rd party services
    4. Admin Controls: filter content (like Bedrock GuardRails)
    5. authenticate users through IAM identity center
    6. Q Apps: vibe coding service
3. Amazon Q Developer
    1. GenAI assistant for AWS developer
    2. Usage
        1. Answer questing about the AWS and your AWS account
        2. Answer questing about resource in your AWS
        3. Suggest CLI fro AWS
        4. Code companion
        5. Can be integrated with IDE
4. Amazon Q for other AWS services
    1. for Quicksight: visualize data
    2. for EC2: provides guidance and suggestions fot EC2 instance types
    3. for AWS Chatbot: access Amazon Q directly through AWS Chatbot
    4. for Glue: data integration
3. PartyRock
    1. GenAI app-building playground powered by Amazon Bedrock
