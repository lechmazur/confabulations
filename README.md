# LLM Confabulation (Hallucination) Leaderboard for RAG

This benchmark evaluates large language models (LLMs) based on how frequently they produce non-existent answers (confabulations or hallucinations) in response to misleading questions that are based on provided text documents. These documents are recent articles not yet included in the LLM training data. Minimizing these types of confabulation is crucial when using Retrieval-Augmented Generation (RAG). The questions are intentionally crafted to be challenging.

As of October 10, 2024, 192 questions, confirmed by a human to lack answers in the provided texts, have been carefully curated and assessed. The number of questions will ideally increase over time, and the error margins will continue to narrow. However, the current dataset is already sufficient to differentiate between various models.

![image](https://github.com/user-attachments/assets/a8c0448e-f891-487f-8e23-a3da7f460475)


## Confabulation and Non-Response Rates

The raw confabulation rate alone isn't sufficient for meaningful evaluation. A model that simply declines to answer most questions would achieve a low confabulation rate. To address this, the benchmark also tracks the LLM non-response rate using the same prompts and documents. Currently, 2,436 hard questions (see the prompts) with known answers in the texts are included in this analysis.

![image](https://github.com/user-attachments/assets/7d0478eb-21d4-4c21-975b-9099cf16c3f7)


## Combined Evaluation
Combining confabulation and non-response rates enables a comprehensive ranking. Depending on your priorities, you may prefer fewer confabulations or fewer non-responses. 

Accuracy benchmarks can also be considered for a fuller assessment. I've created a separate benchmark to test LLMs based on New York Times Connections.

![image](https://github.com/user-attachments/assets/50a518ad-2745-4a7f-a2df-69bcebfc27b8)


## Interesting hallucination results
- o1-preview is likely to be the top-performing single model across most hallucination rankings, though its improvement over GPT-4o may be somewhat underwhelming
- o1-mini ranks below GPT-4o. Don't expect its reasoning to help it hallucinate less.
- GPT-4o shows a significant improvement over GPT-4 Turbo.
- Gemini 1.5 Pro (September) performs better than Claude models!
- Llama models tend to respond cautiously, resulting in fewer confabulations but higher non-response rates


## Additional Notes
- A popular hallucination leaderboard on GitHub uses a model for evaluation of document summaries, but I found this to lead to a very high error rate and different rankings. This approach can be very misleading.
- While the initial set of questions was suggested by LLMs, the final 192 questions were all painstakingly human-verified to have no answers in the provided texts. Only a percentage of LLM-suggested questions were unequivocally answer-free.
- Despite clear prompts, LLMs often generated compound questions that effectively asked for two answers. These were removed in a separate judging step.
- Questions included in the benchmark are those where at least one LLM confabulated. The absolute percentage should not be used to infer that LLMs frequently confabulate, as the questions are intentionally adversarial. This doesn't reflect a "typical" hallucination rate.
- In some cases, LLMs failed to provide valid responses to the questions, such as skipping certain questions altogether. This occurred only once for the human-selected questions without valid answers in the text (bad Gemma, bad), but happened more frequently for questions with valid answers. These questions were discarded.
- A temperature setting of 0 was used
- Multi-turn ensemble is my unpublished system. It utilizes multiple LLMs, multi-turn dialogues, and other proprietary techniques. It is slower and more costly to run but it does very well.


## Updates and Other Benchmarks
Follow [@lechmazur](https://x.com/LechMazur) on X (Twitter) for more.
