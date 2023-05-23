# Project Progress Report
## Introduction:
In this project, we extract skills from job postings using zero-shot or few-shot learning techniques, and use this data to train a Large Language Model (LLM). We built on the previous block's project by expanding the manually annotated corpus by automating the process using GPT-3 to label the data to create a larger annotated dataset. With a more comprehensive dataset, we get a more accurate representation of the current job market and equip job seekers with the skills in demand for each role in tech. After using the GPT-3 API for data labeling and prompt engineering to achieve optimal results, we feed this data (job posting as the input, job skills as the expected output) into different LLMs to compare their performance in extracting job skills given a job posting input. Creating a smaller model (compared to GPT-3) to perform this specific task of skill extraction is an efficient and inexpensive alternative to using GPT-3 to do the same extraction for a larger number of job postings.

## Motivations and Contributions/Originality

Our goal is to create a model which tags skills and tools which are required from job descriptions. As far as we are aware, there are no pretrained models designed for this task. Hence, we experimented with models on data that we created using the text-curie-001 GPT3 model. This will be useful to generate bigger corpuses and also analyze individual job listings.
With a model, we can deploy it in such a way that everyday user’s can incorporate it with their job search.

## Data:

We are continuing with the job description data from the previous block's 523 project. We labeled all the data using GPT-3 APIs. We have close to 2000 job descriptions and we labeled those for the skills required for each job. We manually went through the list of all skills to remove any mistakes made by the GPT-3 model. We would use this data to train an Entity Recognition model for skills.

## Engineering:
### Computing Infrastructure:
For training the NER model, we are utilizing both local and AWS EC2 instances.In Milestone 2, we performed data labeling on personal computers using GPT-3 API models, which enabled us to achieve better results. We did not use any specific computing infrastructure such as Google Colab or Google Cloud TPUs for this purpose.


### DL-NLP Methods:
For Named Entity Recognition (NER), we are exploring different models, including FLAN T5, RoBERTa, BERT, and DistilBERT. We have also developed an LSTM-based NER model from scratch. These models are still under development, and we are continuously experimenting with different architectures and training strategies to improve their performance.

### Framework:
For our NER model, we are utilizing PyTorch as our deep learning framework, and we have already started working with existing codebases for each of the models we are using:

FLAN T5: https://huggingface.co/docs/transformers/model_doc/t5
RoBERTa: https://huggingface.co/models?pipeline_tag=token-classification&sort=downloads
BERT: https://huggingface.co/models?pipeline_tag=token-classification&sort=downloads
DistilBERT: https://huggingface.co/models?pipeline_tag=token-classification&sort=downloads
LSTM NER: https://pytorch.org/tutorials/intermediate/seq2seq_translation_tutorial.html




## Previous Works:

After looking at "Skill Extraction from Job Postings Using Pre-trained Language Models" by Zhang et al. we found a few more papers that seem relevant to our project. First, "Retrieving Skills from Job Descriptions: A Language Model Based Extreme Multi-label Classification Framework" (2020) by Bhola et al. This paper proposes a language model-based approach for extracting skills from job descriptions using extreme multi-label classification. The authors use several pre-trained language models and fine-tune them on a large dataset of job descriptions. They also conduct experiments to evaluate their method and compare it with several baseline methods. Overall, the paper presents a novel approach to skill extraction from job descriptions and provides valuable insights into the challenges of this task. 

Another paper we found interesting was "Occupational skills extraction with FinBERT" (2020) by Mariia Chernova. This paper proposes a method for extracting occupational skills from financial job postings using the FinBERT language model, which is pre-trained on financial text. The authors also conduct experiments to evaluate their method and compare it with several baseline methods. Overall, the paper presents a novel approach to skill extraction from job postings in a specific domain.


We also have "Salience and Market-aware Skill Extraction for Job Targeting" (2020) by Shi et al. The paper appears to make several contributions to the field of skill extraction and job targeting. The salience-aware attention mechanism is a novel approach to extracting relevant skills from job postings and is likely to be more effective than traditional keyword-based approaches. The market-aware weighting method is also an interesting idea, as it recognizes that the importance of certain skills may vary depending on the job market being targeted.

Next, we see “Deep Job Understanding at LinkedIn” (2020) by Li et al. This paper presents the a Job Understanding system developed by LinkedIn, which is part of a large-scale job recommendation system. The system leverages a combination of deep learning models, natural language processing, and graph-based algorithms to provide personalized job recommendations to LinkedIn users. The authors also conduct experiments to evaluate the effectiveness of the system. Overall, the paper presents a comprehensive approach to job recommendation and provides valuable insights into the challenges of this task.

Lastly, we were impressed with the work done in “SpanBERT: Improving Pre-training by Representing and Predicting Spans” (2020) by Joshi et al. This paper presents the SpanBERT language model, which is an extension of the BERT model that is designed to better capture span representations in text. The authors achieve this by introducing a new training objective that encourages the model to predict spans of text rather than individual tokens. They evaluate the effectiveness of the SpanBERT model on a variety of natural language processing tasks and compare it to other state-of-the-art models. Overall, the paper presents a novel approach to language modeling and provides valuable insights into the importance of span representations in text.

## Evaluation:

Our baseline model LSTM model takes job description text as input and outputs the skills required for the job. The output was tagged with B-tag for the beginning token of a skill, I-tag for the token of a skill but not the beginning token, and O-tag for tokens that are not skills.
 
Based on the [evaluation result](https://github.ubc.ca/MDS-CL-2022-23/COLX_585_GPT-5uperpowered_Sea_Urchins/blob/master/code/LSTM.ipynb), the LSTM model showed a strong ability to correctly label tokens that do not represent skills (O-tag), as evidenced by its high F1 score of 0.99. However, the model struggled more in correctly identifying the initial token of a skill (B-tag) and the subsequent tokens of a skill (I-tag), with F1 scores of 0.47 and 0.41, respectively.
 
These results suggest that the model may encounter difficulty in correctly identifying where skills start and end in job descriptions. To improve the model's performance in this regard, it may be beneficial to explore alternative approaches for identifying the start and continuation of skill phrases.
 
We also used the trained LSTM model to annotate a test set and compare the result to the previous human annotation. The precision is around 27.31%. The Recall is around 23.35% and the F1 score is around 25.18%. Compared to the result using the GPT-3 model in milestone 2, the result of LSTM is better. One of the reasons might be that the LSTM model is trained on data after data cleaning, which is done by filtering data which are not skills.


## Challenges

The GPT-3 model identified the skills, but it also identified a few extra things as skills, we could not experiment much with the prompts as we had limited free credits from OpenAI. We solved the issue of incorrectly labeled skills by manually removing all the incorrect skills so that we could have noise free data for our model training.

## Conclusion:

The LSTM model has a better performance compared to the GPT-3 model for annotating skills from the job descriptions. The data cleaning plays an important part of it. We can see there is still room to improve our models.
