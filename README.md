# What Types of Questions Require Conversation to Answer? AskReddit Questions Dataset
#### This is the Github repo of [What Types of Questions Require Conversation to Answer? A Case Study of AskReddit Questions](https://dl.acm.org/doi/10.1145/3544549.3585600).

This dataset is a human-annotated dataset of AskReddit questions aiming to understand **what types of nebulous, open-ended questions can best be answered through conversation**.

Please join the discussion on our [Twitter Thread](https://twitter.com/windx0303/status/1647964084002758659)

## Motivation ##
Conversational systems are primarily designed to provide answers to well-defined questions. However, the real world is full of complex, ill-defined questions. Therefore we want to see what types of ill-defined, open-ended questions require conversation to answer.

The questions in this dataset were extracted from the [one-million-reddit-questions](https://huggingface.co/datasets/SocialGrep/one-million-reddit-questions) dataset.

## Takeaway ##
We found that the questions people believe require conversation to resolve satisfactorily are highly social and personal. Examples include life suggestions, socializing, and mental health. Meanwhile, the questions related to tech or information seeking were considered least requiring of conversation.
<p align="center">
  <img src="https://github.com/Crowd-AI-Lab/AskReddit/blob/c9da0cfc540f95cfd72b7815789e96a90b994a1d/img/score-q6-conversation.png" width="100%">
</p>

The above figure is the conversation score (Q6) distribution over different categories. People like to have conversations to consult on questions that do not have clear answers (e.g., mental_health and life_suggestion). For questions that have clearer answers (e.g., help_find_things and tech), conversation is less needed.

<p align="center">
  <img src="https://github.com/Crowd-AI-Lab/AskReddit/blob/c9da0cfc540f95cfd72b7815789e96a90b994a1d/img/distribution-shift.png" width="100%">
</p>

The above figure is the category distribution shift between all the questions and the ones with higher conversation preference (Conversation score (Q6) $\geq$ 3.5). Categories with the highest increase in percentage are life, mental health, and socializing.

## Asking For Help Questions ##

We consider **asking for help** questions as questions that can be responded to by a conversational agent, questions that people would ask a single ideal agent and have a finite answer were considered valid. Questions
that were not considered as asking-for-help questions were those based on personal opinions and experiences of the answerer. Questions intended to generate debate and instigate conflict were also excluded.

One of the authors first annotated 1,992 randomly sampled questions from the one-million-reddit-questions dataset to determine **asking for help** questions.

A classifier was built based on the annotation and applied to the one-million-reddit-questions dataset. It identified 129,483 asking-for-help questions.

## Collecting Human Opinions About Questions ##
From the 129,483 **asking for help** questions identified by the classifier, 500 questions were randomly sampled for human annotation on Amazon Mechanical Turk (MTurk). For each of the 500 questions, we asked nine workers to rate eight aspects using a five-point Likert Scale  ranging from (1) Strongly Disagree to (5) Strongly Agree. The following table shows the eight aspects we used. Options for Q1 ranged
from (1) Very Unlikely to (5) Very Likely. Options for Q5 were (1)
30 minutes or less, (2) 30 minutes-2 hours, (3) 2 hours-half a day,
(4) half a day-1 day, (5) 1 day or more, and (6) Undoable. Options
for Q8 ranged from (1) Very Difficult to (5) Very Easy.

| #  | Aspect       | Survey Question                                                                                                                                                                                                                                                                                                                                                                                                            |
|----|--------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Q1 | Reach-Out    | If I have this question, I would reach out to other people, such as friends, family members, colleagues, or experts, to get help. As compared to finding the answers by looking up information by myself with a computer or a smartphone.<br>(1) Very Unlikely  (2) Unlikely  (3) Neutral  (4) Likely  (5) Very Likely                                                                                                     |
| Q2 | Scope        | This question is asking for a response within a limited category. For example, questions in the following categories: Yes/No, "Does anybody else...", Either/or, "Would you rather...", polls, surveys and fill-in-the-blank questions.<br>(1) Strongly Disagree  (2) Disagree  (3) Neutral  (4) Agree  (5) Strongly Agree                                                                                                 |
| Q3 | Eliciting    | This question is more about encouraging responders to express their diverse experiences, opinions, or preferences than actually getting help.<br>(1) Strongly Disagree  (2) Disagree  (3) Neutral  (4) Agree  (5) Strongly Agree                                                                                                                                                                                           |
| Q4 | Elaboration  | This question requires or encourages the responders to further discuss with the asker in order to come up with an appropriate answer.<br>(1) Strongly Disagree  (2) Disagree  (3) Neutral  (4) Agree  (5) Strongly Agree                                                                                                                                                                                                   |
| Q5 | Duration     | Without reaching out to other people, for a layperson with no background knowledge related to this question. How long do you think it would likely take for them to figure out the answer to this question with access to the internet?<br>(1) $\leq$ 30 minutes (2) 30 minutes-2 hours (3) 2 hours-half a day (4) half a day-1 day (5) $\geq$ 1 day (6) Undoable                                                                  |
| Q6 | Conversation | If I have this question, I would prefer to have a conversation regarding the details of the question and have a further discussion with the answerer. As compared to asking the question as is and waiting for the answers.<br>(1) Strongly Disagree  (2) Disagree  (3) Neutral  (4) Agree  (5) Strongly Agree                                                                                                             |
| Q7 | Format       | Suppose I asked this question using a computer or smartphone instead of making phone calls or in-person sessions. In that case, I prefer the answer to be provided through a conversation (e.g., via WhatsApp or other messaging applications) compared to other written formats, such as emails, social media replies, or online forums.<br>(1) Strongly Disagree  (2) Disagree  (3) Neutral  (4) Agree  (5) Strongly Agree |
| Q8 | Difficulty   | Without reaching out to other people to get help, I will be able to answer the question by looking up information by myself with access to a computer or a smartphone.<br>(1) Very Difficult  (2) Difficult  (3) Neutral  (4) Easy  (5) Very Easy                                                                                                                                                                          |

## Data Schema ##
The dataset includes three files: `asking_for_help.csv`, `AskReddit_Turk_raw.csv`, and `AskReddit_Turk_processed.csv`. The following descriptions and tables shows the schema of the dataset.

`asking_for_help.csv`\
The 1,992 questions annotated by the author as asking-for-help questions or not. The two columns are “Text” and “Label” respectively, representing the questions being labeled and the label we provided. "T" indicates "True" and the question **IS** considered as a asking-for-help question, "F" indicates "False" and the question **IS NOT** considered as a asking-for-help question.

| Text                                                              | Label |
|-------------------------------------------------------------------|-------|
| What invention made some other inventions ?                       | T     |
| why is a second called a second, and not a first?                 | T     |
| What’s your first thought when you get out of bed in the morning? | F     |
| Which movies is your favorites?                                   | F     |
| ...                                                               | ...   |

`AskReddit_Turk_raw.csv`\
The 500 questions we sampled to ask MTurk workers to help annotate and the raw data we collected. 9 responses for each question were collected, resulting in 4,500 sets of results. The columns are "ID", "Text", "WorkerID", and "Q1"-"Q8". In order to protect the privacy of MTurk workers, “WorkerID”s are set as randomized numbers and do not represent workers real MTurk ID. Same “workerid” in different columns indicates that the responses were provided by the same worker.

| ID | Text                                                                           | WorkerID | Q1 | Q2 | Q3 | Q4 | Q5 | Q6 | Q7 | Q8 |
|----|--------------------------------------------------------------------------------|----------|----|----|----|----|----|----|----|----|
| 0  | How many calories could you consume daily without feeling sick?                | 0        | 4  | 4  | 2  | 5  | 2  | 3  | 2  | 4  |
| 0  | How many calories could you consume daily without feeling sick?                | 7        | 2  | 4  | 3  | 4  | 2  | 2  | 2  | 2  |
| 1  | I want to support my friend who broke up recently. What can I say to help him? | 9        | 5  | 1  | 5  | 4  | 2  | 5  | 4  | 3  |
| 1  | I want to support my friend who broke up recently. What can I say to help him? | 7        | 5  | 1  | 5  | 5  | 3  | 5  | 4  | 2  |
| ...| ...                                                                            | ...      | ...| ...| ...| ...| ...| ...| ...| ...|

`AskReddit_Turk_processed.csv`\
The processed and categorized data of the 500 questions we sampled to ask MTurk workers to help annotate. The columns are "ID", "Text", "Category", and "Q#_mean"-"Q#_std"(# for numbers 1-8). "category" represents the category we labeled for the question. Mean(mean) and standard deviation(std) score for each of the 8 survey questions(Q1-Q8) were computed from the responses of the 9 workers recruited for each sampled question. Please note that response “6” for “Q5” is discarded while calculating the score due to its difference in response nature compared to response 1-5.

| ID | Text                                                                                                                                                                                  | Category            | Q1_mean     | Q1_std      | ... | Q8_mean     | Q8_std       |
|----|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|---------------------|-------------|-------------|-----|-------------|--------------|
|  0 | How many calories could you consume daily without feeling sick?                                                                                                                       | medical_health_diet | 3.777777778 | 1.394433378 | ... | 3.444444444 |  1.236033081 |
|  1 | I want to support my friend who broke up recently. What can I say to help him?                                                                                                        | others              | 4.444444444 | 1.333333333 | ... | 3.333333333 |            1 |
|  2 | What is called when food in expensive than other materials (like electronics) and otherwise? It is related to inflation and deflation, forgot what’s it’s the name of that situation. | help_find_things    | 3.111111111 | 1.269295518 | ... | 4.111111111 | 0.3333333333 |
|  3 | I tried to delete all contents of a dvd but there is a protection that doesn't, anyone know how to deal with that ?                                                                   | tech                | 3.555555556 | 1.333333333 | ... | 3.888888889 |   0.78173596 |

## How to Cite?
```
@inproceedings{10.1145/3544549.3585600,
author = {Huang, Shih-Hong and Huang, Chieh-Yang and Lin, Ya-Fang and Huang, Ting-Hao Kenneth},
title = {What Types of Questions Require Conversation to Answer? A Case Study of AskReddit Questions},
year = {2023},
isbn = {9781450394222},
publisher = {Association for Computing Machinery},
address = {New York, NY, USA},
url = {https://doi.org/10.1145/3544549.3585600},
doi = {10.1145/3544549.3585600},
abstract = {The proliferation of automated conversational systems such as chatbots, spoken-dialogue systems, and smart speakers, has significantly impacted modern digital life. However, these systems are primarily designed to provide answers to well-defined questions rather than to support users in exploring complex, ill-defined questions. In this paper, we aim to push the boundaries of conversational systems by examining the types of nebulous, open-ended questions that can best be answered through conversation. We first sampled 500 questions from one million open-ended requests posted on AskReddit, and then recruited online crowd workers to answer eight inquiries about these questions. We also performed open coding to categorize the questions into 27 different domains. We found that the issues people believe require conversation to resolve satisfactorily are highly social and personal. Our work provides insights into how future research could be geared to align with users’ needs.},
booktitle = {Extended Abstracts of the 2023 CHI Conference on Human Factors in Computing Systems},
articleno = {319},
numpages = {9},
keywords = {Question Answering, Reddit, Conversational Systems},
location = {Hamburg, Germany},
series = {CHI EA '23}
}
```
