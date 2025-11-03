## Task Description and Evaluation

RAG4Reports will host two tasks:

1. Automatic Report Evaluation  
2. Multilingual Report Generation

### Automatic Report Evaluation

We will provide system-generated reports from 2025 TREC RAGTIME submissions that have been judged by human annotators as the input for the shared task participants. The task is to provide a system ranking based on each report request (long-form query with a description of user background) as well as an overall ranking across all report requests. The submitted rankings will be evaluated on correlation to the ranking derived from human annotations. We will accept two types of submissions:

1. fully automatic evaluators: without any additional human inputs;  
2. semi-automatic evaluators: with an additional input of human-curated essential facts (will be provided by the organizers) that should be included in a useful report

To study the effect of document languages on the evaluation, we will accept submissions using an English translation (provided by the organizers) of the corpus or using the multilingual corpus with documents in their original languages. We will use [AutoARGUE](https://github.com/hltcoe/auto-argue) as the baseline for Task a2. 

#### Data and Submission Format

Participants will receive a set of report generation responses that need to be evaluated. Each generation system will map to a JSONL file where each line is the response to a request. The file name will be the generation system ID. Please see the submission format of the Multilingual Report Generation task for details. 

The output format should be a TSV with the columns: 

* topic\_id (string): the topic ID that this line is reporting  
* generation\_system\_id (string): the generation system that this line is reporting  
* metric\_name (string): the metric name  
* score (float): the numerical score of the metric for this generation system on this topic 

There will be a field in the submission portal to indicate which metric you would like for the shared task. You may contain multiple metrics in the submission and pick one for the evaluation.

### Multilingual Report Generation

This task involves generating long-form reports in response to a request using information retrieved from a multilingual corpus. Report requests consist of background information about the user and a statement describing their information need **in English**. In contrast to other RAG tasks, **reports should contain only information that is grounded in the corpus**. Generated reports should consist of sentences with citations and will be given a length limit. Reports should be written in the same language as the report request. The corpus consists of four million English, Chinese, Russian, and Arabic documents sampled from Common Crawl News, evenly sampled from 2021 to 2024\. The organizers will provide search services accessible through an API in addition to the corpus itself. Submitted reports will be judged automatically based on the [Auto-ARGUE framework](https://arxiv.org/abs/2509.26184), which scores reports based on whether nuggets of related information are present and correctly cited in the report. We plan to score reports using a range of LLMs to understand their agreement. 

#### Request and Submission Format

Report requests will be distributed in JSONL format as a list of individual requests, one per line. Each request will contain the following JSON fields:

* `topic_id` (string): A unique ID for this report request  
* `title` (string): A short description of the report request  
* `background` (string): Describes the context in which the report is being written  
* `problem_statement` (string): Describes what should and should not be included in the report  
* `limit` (int): Maximum number of NFKC-normalized Unicode characters the report may included

The submission format is a sequence of JSONL entries each representing one report. Each report is a JSON object containing three main objects :

* `metadata` (dictionary)  
  * `topic_id` (string): The unique ID of the input report request  
  * run\_id (string): An arbitrary string to identify the run. It is recommended to include your team name as part of the run\_id

  Other `metadata` fields may be present but will be ignored.

* `responses` (array): a list of sentence dictionaries.  
* `references` (array): a list of reference document IDs (strings). This should be the union of all cited documents. 

Sentences must appear in report order. Each sentence dictionary has the following fields:

* `text` (string): a string containing the text of the sentence  
* `citations` (dictionary): a dictionary of zero or more document IDs (strings) mapped to scores that are floating point numbers. The higher the number, the more confidence the system has in the validity of that citation.

## Submission Instruction

Please submit your runs through the Google Form that will be announced later. Each team can submit an unlimited number of submissions, but **only the last three submissions from the team for each task will be evaluated and considered in the competition.** 

Each participating team is expected to submit a system paper after the results are announced. During the conference, the winner in each task will receive a slot for an oral presentation. Other teams will be invited to present at the poster session. We strongly encourage each team to participate in the poster session to share the knowledge. 

## Important Dates

* Data release: December 10, 2025  
* Task A and B submission deadline: March 5, 2026  
* Result announcement: April 28, 2026  
* System papers due: May 12, 2026  
* Workshop dates: July 2 or 3, 2026 (TBA)