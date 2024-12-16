# WHITE-ShARC Dataset

WHITE-ShARC combines the characteristics of conversational dialogue and open-retrieval settings, enabling a broader range of question types and incorporating unanswerable instances.
WHITE-ShARC contains 3,404 instances of answers, 2,624 instances of follow-up questions, and 208 instances of unanswerable cases.
Both yes-no questions and Wh-questions are included.
The utterances are divided into training, development, and test sets, which include 2,687, 306, and 411 answers; 2,064, 217, and 343 follow-up questions; and 159, 23, and 26 unanswerable cases, respectively.

# Details of Dataset Construction

To cunstruct WHITE-ShARC, we used the 651 rule texts from [OR-ShARC](https://github.com/Yifan-Gao/open_retrieval_conversational_machine_reading).

## 1. Main Annotation Stage

In this stage, annotators were asked to carefully consider the intended audience and context when presented with a rule text. 
They were then guided to focus on elements such as `time`, `location`, and `reason` to craft Wh-questions. 
Minimal constraints were imposed to encourage creativity and generate diverse question formats.

### 1.1 Scenario Annotation:

For the scenarios, annotators were instructed to provide descriptions of 2 to 5 sentences with at least 15 words, focusing on the context in which a user would ask the given question. 
It is important to leave some information for potential follow-up questions.
Including irrelevant details is occasionally acceptable, reflecting real-world cases where users may provide unclear or extraneous information.

### 1.3 Follow-up Question Annotation:

Annotators were restricted to starting follow-up questions with words like `Do`, `Does`, `Did`, `Is`, `Was`, `Are`, and `Were`, limiting answers to `Yes` or `No` . 
To handle vague or unclear user queries, we used OR-ShARC rule texts to generate ambiguous Wh-questions, requiring follow-up for a final answer. 
This approach avoids open-ended follow-ups, ensuring a precise evaluation and direct comparison of model outputs.

### 1.4 Answer Annotation:
For answers, we required adherence to the rule text's terminology and encouraged brevity. Complete sentences were unnecessary; for instance, `$75` suffices instead of `You can get $75.`  
These guidelines ensure a more accurate evaluation of the model's performance.

### 1.5 Difficulties:  
Creating Wh-questions that prompt relevant follow-ups proved challenging, as it required crafting conversational questions that need further context, rather than those answerable directly from the rule text. 
To address this, we invited six annotators, selecting three as elite annotators for their creativity and detail-oriented work. 
These elite annotators generated conversational Wh-questions to engage users.
Despite this, generating large volumes of questions by elite annotators remains labor-intensive, necessitating additional augmentation methods to expand the dataset.

To train the annotators, we have prepared a set of instructional examples encompassing both conversational (multi-run dialogue) and non-conversational (single-run dialogue) formats.
Each data entry undergoes a secondary confirmation process by another annotator to ensure its accuracy and quality. 
Only when the data passes this procedure is it retained for further use.
Through this procedure, we aim to enhance the robustness and quality of our dataset, instilling confidence in its reliability and integrity.

## 2. Human Augmentation Stage

At this stage, our goal is to augment the data from the main annotation phase with more challenging examples. 
We begin by selecting existing conversational data, then provide annotators with pairs of follow-up questions and answers, which they convert into scenario information using different vocabulary. 
This increases the difficulty during both retrieval and contextual processing, such as recognizing that someone with a child cannot apply based on a rule.
We select pairs for conversion, ensuring essential information from existing scenarios is retained. 
After conversion, another annotator verifies that the modified data remains consistent with the original in content and meaning.

## 3. Transfer Stage

During the planning of the main annotation stage, we identified a specific type of Wh-question format.
This question format shares logical similarities with yes-no questions, prompting the potential transfer of data from OR-ShARC to WHITE-ShARC. 
We begin by using a rule-based method to convert yes-no questions into `Why` questions while preserving all other information. 
The annotators' main task is to create a new answer. 
To ensure a deep understanding of the rule text, annotators first label the `logic` within the text. 
Once they fully grasp the content, they generate a new answer consistent with the provided information.

### 3.1 Logic

After examining a large portion of the rule texts, we have identified several commonly occurring logic patterns.  
Most explanations below will be under the premise that a user expresses a desire to apply for a loan.  

**OR:**  
The frequent occurrence of a bulleted list format is observed in which, when any of the listed conditions are met, the user becomes eligible to apply for a loan.  

When any of the conditions in the bulleted list are satisfied, the ultimate answer will be **"Yes,"** with a **"No"** outcome only arising when none of the conditions are met.  

**AND:**  
The logic of **"AND"** is also commonly presented in the form of a bulleted list, where the user becomes eligible to apply for a loan only when all the listed conditions are met.  

In order to obtain a final **"Yes"** outcome, all the conditions must be satisfied. If any of the conditions are not met, the result will be **"No."**  

**AND in OR:**  
The main conditions in the given scenario are connected by the logic **OR**, indicating that the user is eligible for the loan if any of these conditions are met.  
However, within these main conditions, there exist sub-conditions that are connected by the logic **AND**.  
Figure 1 provides an example where there are three main conditions connected by the logic **OR**.  
In the second condition, there are two sub-conditions, namely *"a new government-sponsored student on a course"* and *"lasts longer than 6 months,"* which are connected by the logic **AND**.  

**OR in AND:**  
The opposite of **AND in OR**. In this case, the main conditions are connected by the logic **AND**, indicating that all of these conditions must be satisfied for the user to be eligible for the loan.  
However, within these main conditions, there exist sub-conditions that are connected by the logic **OR**.  

**AND-OR list:**  
In an **AND-OR list**, there is an **AND-connected condition** preceding a bulleted list with **OR-related conditions**.  

*"you get certain limit benefits"* is a mandatory condition that must be met, and any one of the three conditions following it allows the applicant to be classified as doing voluntary work and qualify for the loan.  

**OR-AND list:**  
The opposite of an **AND-OR list**, loan eligibility requires either the satisfaction of the preceding condition or the fulfillment of all conditions listed afterward.  

**Complex:**  
These rule texts often involve the interplay of multiple conditions and combinations of **AND** and **OR** relationships.  
The logic may consist of nested or cascading combinations of **AND** and **OR** operators, leading to intricate decision paths.  

**Simple:**  
There is no specific logic involved. The conditions are presented in a concise and direct manner without any complex combinations or relationships.  

**Others:**  
Rule texts that do not fit into any of the aforementioned categories.

### 3.2 Transfer Stage Guideline

#### 3.2.1 Final Utterance Transfer

Our primary objective is to generate **New Questions** and **New Answers** from OR-ShARC while retaining other relevant information. The generation of New Questions and Answers is based on the transformation of the Original Questions and Answers. When the Original Answer is **"Yes"**, the Original Question is transformed into an affirmative question starting with **"Why,"** as shown in the following example.  

<img width="460" alt="image" src="https://github.com/user-attachments/assets/7faf1671-e3e3-4118-9ebc-9201b9737501" />


If the Original Answer is **"No"**, the transformation results in a negative question.

Initially, the annotator identifies that the rule text exhibits **OR logic**. Then, by reasoning based on the scenario, it is established that the user satisfies the second condition,  
> *"a new government-sponsored student on a course that lasts longer than 6 months."*  

The **New Question** asks:  
> *"Why can I apply ...?"*  

The **New Answer** is determined as:  
> *"You are a new government-sponsored student on a course that lasts longer than 6 months."*

When the question is an **affirmative sentence** and the main logic of the rule text is **AND**, the reason you can apply for a loan is that you satisfy **all the conditions**. Therefore, the answer will include all the conditions.  
If the main logic of the rule text is **OR**, the reason you can apply for a loan is that you satisfy **at least one condition**. To avoid asking all the conditions, we only need to find the first matching reason. So, the answer will be the missing condition.  

On the other hand, when the question is **negative** and the main logic of the rule text is **AND**, the answer identifies the **first reason** that prevents you from applying for a loan. If the main logic is **OR**, the answer includes **all the conditions** since none of them are satisfied.

---

#### 3.2.2 Internal Utterance Transfer

The first step, similar to the previous process, involves converting the original question into a **"Why"** question format. We randomly formulate some questions as affirmative sentences and others as negative sentences while preserving the **rule text**, **scenario**, **history**, and **answer** in their original form.

**Why can we make this transformation?**  
This is because the original scenario and history do not provide sufficient information to make a conclusive final answer. Therefore, the answer to the original utterance is to ask a **follow-up question**. By converting it into a **"Why"** question format, we do not alter the fact that the information is incomplete. Hence, apart from the difference in the question itself, given the same other conditions, the answer for this utterance will remain the same.

<img width="459" alt="image" src="https://github.com/user-attachments/assets/f3119276-ab05-47bf-ba62-997c2ddb327e" />


This figure provides an example where we only modify the **Question**, changing it to:  
> *"Why can I get SSP?"*  

It can also be modified to:  
> *"Why can't I get SSP?"*

- If it is the former, the history informs us that the user does not meet the first condition, so the answer would be a **follow-up question** to ask the user if s/he meets the second condition.  
- If it is a **negative question**, the history informs us that the user does not meet the first condition, so we need to ask the user if s/he also does not meet the second condition to answer the final question.  

Through this simple modification, we can transfer the data from **OR-ShARC** into our new data.


### 4. Data Augmentation
We augmented the dataset with more instances where the answer is a follow-up question.  
Since manual annotation is time-consuming and costly, we utilized ChatGPT as an alternative annotator.  
We identified relevant utterances, provided the original scenario and history in the prompt, and tasked ChatGPT with rewriting the scenario.  
The goal was to preserve the original meaning while allowing for slight variations and potentially introducing new information.  
The prompt is presented in [Prompts](https://github.com/ntunlplab/WHITE-ShARC/blob/main/Prompts.md), and all ChatGPT-generated content was manually verified for quality.  

ChatGPT's rewritten scenarios were highly coherent and closely aligned with the originals.  
We generated **two new scenarios** per instance, and a review of **100 samples** showed a **100% pass rate**.  
Additionally, ChatGPT-generated scenarios were slightly longer, increasing the complexity for model reasoning.

---

## Dataset

It is divided into train, validation (dev), and test sets, with further distinctions for augmented data and scenarios involving "seen" and "unseen" rule texts.

Data Augmentation (aug): Indicates data that has been augmented for improved training and evaluation.

Seen: Refers to instances where the rule texts used in the questions also appear in the training set.

Unseen: Refers to instances where the rule texts in the questions do not appear in the training set.

### Usage

Multi-turn Question Answering: Assessing systems' ability to handle follow-up questions.

Seen vs. Unseen Generalization: Evaluating model performance on rule texts encountered during training vs. new ones.



