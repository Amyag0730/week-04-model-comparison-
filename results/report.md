# Model Comparison Report Week 4 
**Name:** [Amy Aguaysa]
 **Date:** [05/05/26]
 **Capstone Project
:** [Model Discovery & API Integration]
 **My Component:** [CyberSecurity] 

## Test Setup **Input dataset:** 5 [domain] text samples covering:
 - 2 clearly concerning/high-severity records 
- 1 ambiguous/edge case record 
- 2 routine/benign records 

**Models tested:** 
1. cardiffnlp/twitter-roberta-base-sentiment-latest (sentiment) 
2. facebook/bart-large-mnli (zero-shot classification) 
3. dslim/bert-large-NER (named entity recognition)
 4. chat/completions (LLM classification) 

**Evaluation criteria:** 
label accuracy, confidence score, speed, ease of integration in n8n 
## Results Summary

| Record | Sentiment | Zero-Shot | NER Entities | Groq |
|--------|-----------|-----------|---------------|------|
| 1 | Positive (0.4013) | Possible anomaly (0.9) | Moscow | HIGH |
| 2 | Positive (0.4013) | Routine activity (1.0) | None | INFORMATIONAL |
| 3 | Positive (0.4013) | Possible anomaly (0.8) | Amazon | MEDIUM |
| 4 | Positive (0.4013) | Possible anomaly (0.8) | SSH | CRITICAL |
| 5 | Positive (0.4013) | Routine activity (1.0) | None | INFORMATIONAL |

## Analysis
**Where models agreed:** 
The zero-shot model and Groq agreed that records 2 and 5 were routine/benign. They also both identified records 1, 3, and 4 as concerning or possible anomalies.

**Where models disagreed:** 
The sentiment model disagreed with the other models because it labeled every record as positive, even the concerning security alerts. This may be because sentiment analysis is designed to detect emotional tone, not security severity. NER also did not classify severity; it only found named entities like Moscow, Amazon, and SSH.

**Most accurate model overall:** 
The Groq LLM classification was the most accurate overall because it gave the most sensible severity levels and included reasoning for each alert.

**Fastest/most practical:** 
I believe model 4, Groq classification, would be the easiest model to use because it provides detailed information along with the level of severity of each message.

## Recommended Models for My Capstone Component
**Component:** Security alert classification workflow

**Primary model:** Groq chat/completions — This model is the best fit because it can classify alerts by severity and explain the reason behind each classification.

**Secondary model:** facebook/bart-large-mnli — This model can help identify whether a message is routine activity or a possible anomaly.

**Rejected models and why:**

- **cardiffnlp/twitter-roberta-base-sentiment-latest:** This model was not the right fit because it lacked accuracy for this task. It labeled every text prompt as positive, which caused false results. This can be detrimental because it lowers the program’s efficiency and could cause serious security alerts to be overlooked.
- **dslim/bert-large-NER:** This model was useful for finding entities, but it did not classify severity. It works better as a support model rather than the main model.

## Failure Cases and Limitations
Model 1, the sentiment model, gave me false positive results, which was surprising because the other models were able to identify the concerning text prompts more accurately. I would have to look further into my workflow to distinguish whether the issue is with the model itself or with how my program is processing the results. Another limitation is that NER only extracts names, places, or organizations, so it does not fully explain whether an alert is dangerous.

## Next Steps
If I had more time, I would test different Hugging Face models and compare their accuracy. This would be an interesting challenge to see how the table changes with different model types. Additionally, I would like to use different n8n nodes and better understand their purposes in the workflow.
