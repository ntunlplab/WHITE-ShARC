# Prompts used in our work

## The prompt for Scenario Rewriting in the context of data augmentation

We used the following prompt for requesting ChatGPT to rewrite the scenarios in the context of data augmentation.
Since history represents the prior conversational history, we intentionally excluded it from the scenario by marking it as `Don't mention` in the prompt. Moreover, given that providing only these two pieces of information was sufficient for ChatGPT to generate satisfactory results, there was no need to supply additional elements such as questions or rule texts.

**Prompt:**  
Please assist in rewriting `Old Scenario` as `New Scenario` while adhering to the following guidelines:  
1. The main idea should remain the same.  
2. Use different vocabulary from the original.  
3. You can add a little bit of information, but if `Don't mention` is not empty, please refrain from using that information in the `New scenario`.  
4. `New scenario` should consist of a maximum of five sentences.  
5. Give me 2 rewriting results, `New Scenario1` and `New Scenario2`.  

**Old Scenario:**  
I would like to purchase a crib for my newborn son while I'm on paternity leave helping my wife take care of the little guy.  

**Don't mention:**  
[Are you working in a UK company? Yes]  

Now generate `New Scenario1` and `New Scenario2`.  

---

**Output From ChatGPT:**  

**New Scenario1:**  
While I am temporarily away from work to assist my wife in nurturing our newborn son, I have the intention of acquiring a bassinet for his comfort and well-being.  

**New Scenario2:**  
During my period of paternal absence from my professional duties, as I provide support to my wife in caring for our recently born son, I am considering purchasing a crib to ensure his optimal care and comfort.  

---


## The prompt of ChatGPT Rule Segmentation

The following prompt is that we employ to instruct ChatGPT to simplify complex scenarios by reading the rule text, thereby transforming them into New Scenarios that are more easily understandable by the reader.

**Prompt:**  
Please segment the statement into distinct units or segments to analyze its structure and content. Every segment should not be too long, usually below 10 characters.

---

**Example:**  
If you want to sell some cards in New York: you have to either be older than 20 years old or be older than 16 years old and have a B6 certificate.

---

**Output:**  
Segment: If you want to sell some cards  
Segment: in New York  
Segment: you have to either be older than 20 years old  
Segment: or be older than 16 years old  
Segment: and have a B6 certificate.

---
