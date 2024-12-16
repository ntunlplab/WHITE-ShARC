# WHITE-ShARC

WHITE-ShARC combines the characteristics of conversational dialogue and open-retrieval settings, enabling a broader range of question types and incorporating unanswerable instances.
WHITE-ShARC contains 3,404 instances of answers, 2,624 instances of follow-up questions, and 208 instances of unanswerable cases.
Both yes-no questions and Wh-questions are included.
The utterances are divided into training, development, and test sets, which include 2,687, 306, and 411 answers; 2,064, 217, and 343 follow-up questions; and 159, 23, and 26 unanswerable cases, respectively.

# Details of Dataset Construction

To cunstruct WHITE-ShARC, we used the 651 rule texts from [OR-ShARC](https://github.com/Yifan-Gao/open_retrieval_conversational_machine_reading).

## Main Annotation Stage

In this stage, annotators were asked to carefully consider the intended audience and context when presented with a rule text. 
They were then guided to focus on elements such as `time`, `location`, and `reason` to craft Wh-questions. 
Minimal constraints were imposed to encourage creativity and generate diverse question formats.

## Scenario Annotation:

For the scenarios, annotators were instructed to provide descriptions of 2 to 5 sentences with at least 15 words, focusing on the context in which a user would ask the given question. 
It is important to leave some information for potential follow-up questions.
Including irrelevant details is occasionally acceptable, reflecting real-world cases where users may provide unclear or extraneous information.

## Follow-up Question Annotation:

Annotators were restricted to starting follow-up questions with words like `Do`, `Does`, `Did`, `Is`, `Was`, `Are`, and `Were`, limiting answers to `Yes` or `No` . 
To handle vague or unclear user queries, we used OR-ShARC rule texts to generate ambiguous Wh-questions, requiring follow-up for a final answer. 
This approach avoids open-ended follow-ups, ensuring a precise evaluation and direct comparison of model outputs.




