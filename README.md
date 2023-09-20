# Use-cases related to AI/ML


### Below are the 4 use-cases related to LLM (Large Language Model).  Approaches are mentioned to execute respective use-cases using LLM, prompt-engineering, RAG or API calls.


### Use case 1

> Use `AI` to analyse orders and the feedback received for a food delivery company and summarise the customer feedback. Make assumptions on the source of the data.


This use-case can be considered as `text-sumarisation` where customer's long feedback can be summarise to take effective measures or analyse these data for the betterment of the food delivery company. There are numerous food-delivery companies and usually users/customers make feedback about the food, cuisine, themes, chef etc. These feedbacks can ranges from 10-15 words to even 50 or 100 words. It is very difficult make any assumptions by reading these many feedbacks as it requires lot of efforts and weeks or months of time to analyse. In such cases LLM based model will be very helpful. Pre-trained network (`Transformer`) would help upto some extent. But these model will be generic, mostly will not cover the domain related informations. There are SOTA models which can be easily used or some model's API can be accessible to deliver the results. Such models are `Chat-GPT`, `Llama`, `BLOOM`, `FLAN-T5` etc which can directly be used.


These are very big models and uses heavy compute and spaces. For explanation perspective and see the behaviour or the significance of approaches, I have used Google's `FLAN-T5` model. It also has different variants (e.g. base, small, xl, xxl etc) but due to space constraints and other factors, I have used `base` variant of `T-5` model. I have used `Google Colab` to fine-tune. For evaluation I have used `ROUGE` metrics to see how to model is doing. The whole code-base can be trained for more epochs with mode datasets. I have used few dataset (`1%` of [public available dataset](https://www.kaggle.com/datasets/snap/amazon-fine-food-reviews)) and fine-tune for `2` epochs. Below are `ROUGE` metrics for `PEFT` based fine-tuned model. Objective is to see the difference in scoring between `base model` vs `fine-tuned model`. It can definitely do better for more data with more number of epochs.



|Model Type|rouge1|rouge2|rougeL|rougeLum|
|----------|------|------|------|---------|
|ORIGINAL MODEL|0.074|0.038|0.0568|0.0568|
|PEFT MODEL|0.117|0.025|0.12|0.12|


### Use Case 2

> Create email content to encourage customers to purchase specific products. Also, Can AI be utilised help edit/refine existing content in our Sales repository to make it more market ready?


This use-case emphasis on creating marketing e-mails by looking up the company's portfolio, it's product and other informations. It is tedious as well as erroneous task towards execution. Undoubtedly it it time-taking too. Through LLM model it can be easily achievable by prompt-engineering and `Lang Chain` techniques. `Land Chain` does provide to build chains before it get fed to the LLM's models. Models output will be based on the input and the `placeholder` will be treated as how the customer wants. This is a `text generative` model where the model objective is to generate text (can be controlled on # texts) based on the input provided.

Since the data-set can be too domain specific and does include additional data based on the information needed in the e-mail formatting. Any SOTA based `decoder` Transformer model would be sufficient to execute this task. I have used `OpenAI` API based model (*chat gpt 3.5*) for text generation and LangChain for chaining information for prompt-engineering. By collating these information results can be generated. Below is an example of such e-mail (though the contents are not real; not specific to company)

```shell

Dear [customer name], 

We love that XYZ product helps teams stay connected and informed in today’s busy world. It is a small hand-gadget with many features, including GPS navigation for staying aware of one’s location to the dear ones. The benefits of the XYZ product are numerous, from tracking progress and providing motivation to tracking location and encouraging connectivity. 

At XYZ, we believe in the power of using our products to create positive change, and we know that our product can help you achieve your goals. We encourage you to set up a time to talk more about how XYZ can help you and your team. Thank you for your time and attention. 

Sincerely, 
[Your Name]
```

### Use case 3

> Use AI to comb through multiple documents and provide answers to most frequently asked questions. This solution needs to be implemented at scale and documents can be a mix of PDF’s , excel , word , DB tables.


This use case is more on retrieving an efficient or most appropriate result from the stack of information (in this case it is `FAQ`).   I propose the development of an AI system that utilizes a `vector database` integrated with the **RAG** (Retrieval-Augmented Generation) model to efficiently retrieve and generate answers to frequently asked questions from a variety of document types. This approach ensures rapid, accurate responses while handling the scalability and diversity of document formats. `LangChain` would be very beneficial to engage different aspect of performing faster retrieval and maintaining modularity of the code. I have used `OpenAI` API calls for generating embedding vector and stored in *Chroma DB*. Efficient way to form chain and input different aspects of retrieval component to query faster.

I have extracted some FAQs on `PAN` card related user queries. Parse these data and stored in `ChromaDB` using `OpenAI` calls for embedding vector generation.

Mostly it is dependent on the `embedding vector` as it plays a critical role in determining an efficient distance on similarity score. The more prominent or efficient embedding vector would be the more close or efficient similarity score be resulting in optimal matching of questions and hence the expected answer. For exploration, I have used `ChromaDB` where the storage itself on disk (i.e. I/O operations) and retrieval would be easier. For deployment multiple processing, distributed storage, caching mechanism for storing huge amount of data. Below output is an example of few questions and answers being stored in *chroma DB* and retrieval of answers w.r.t questions.


```text

{'query': 'Can I take the delivery of Pan card at Indian address', 'result': 'Yes, you can take the delivery of your PAN card at an Indian address mentioned in your Aadhaar card.'}

{'query': 'What are the documents required to link PAN with Aadhaar?', 'result': 'The documents required to link PAN with Aadhaar are a copy of your PAN card and Aadhaar card.'}

```

### Use case 4

> How AI can help in analysing claims and utilization data to identify anomalies, trends, FW&A. Use some publicly available data and come up with the solutions.


The challenge is to leverage AI to analyze claims and utilization data to detect anomalies, identify trends, and recognize fraudulent, wasteful, and abusive activities (FW&A). The solution should be developed using publicly available data sources.

 I propose building an AI-driven system for claims and utilization data analysis. This system will employ data analytics, machine learning, and anomaly detection techniques to identify patterns, trends, and instances of FW&A. By utilizing publicly available datasets, we can demonstrate the capabilities of AI in healthcare fraud detection and insights generation.

