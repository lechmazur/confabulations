# LLM Confabulation (Hallucination) Leaderboard for RAG

This benchmark evaluates large language models (LLMs) based on how frequently they produce non-existent answers (confabulations or hallucinations) in response to misleading questions that are based on provided text documents. These documents are recent articles not yet included in the LLM training data. Minimizing these types of confabulation is crucial when using Retrieval-Augmented Generation (RAG). The questions are intentionally crafted to be challenging.

As of October 10, 2024, 192 questions, confirmed by a human to lack answers in the provided texts, have been carefully curated and assessed. The number of questions will ideally increase over time, and the error margins will continue to narrow. However, the current dataset is already sufficient to differentiate between various models.

![c1](https://github.com/user-attachments/assets/e2340408-d632-4327-9ae7-ccc0b02cdd76)

## Confabulation and Non-Response Rates

The raw confabulation rate alone isn't sufficient for meaningful evaluation. A model that simply declines to answer most questions would achieve a low confabulation rate. To address this, the benchmark also tracks the LLM non-response rate using the same prompts and documents but specific questions with answers that are present in the text. Currently, 2,436 hard questions (see the prompts) with known answers in the texts are included in this analysis.

![c2](https://github.com/user-attachments/assets/426b5ee1-4514-41b0-bd65-7d733782301b)


## Combined Evaluation
Combining confabulation and non-response rates enables a comprehensive ranking. Depending on your priorities, you may prefer fewer confabulations or fewer non-responses. 

| Model Name            |   Confabulations  (%) |   Non-Response Rate (%) |
|-----------------------|---------------------------------|-------------------------|
| Qwen 2.5 72B          |                            29.7 |                     5.8 |
| o1-mini               |                            24   |                    10.2 |
| o1-preview            |                            16.7 |                     7.4 |
| GPT-4 Turbo           |                            22.9 |                    31.4 |
| Gemma 2 27B           |                            44.3 |                     7.1 |
| GPT-4o mini           |                            57.3 |                    13.6 |
| Claude 3 Haiku        |                            56.8 |                    10.4 |
| Llama 3.1 70B         |                            13.5 |                    31.4 |
| Gemini 1.5 Flash      |                            41.7 |                     5.2 |
| GPT-4o                |                            18.8 |                     8.5 |
| Claude 3.5 Sonnet     |                            26.6 |                    16.1 |
| Llama 3.1 405B        |                            12.5 |                    20.8 |
| Gemini 1.5 Pro (Sept) |                            16.7 |                     9.7 |
| Claude 3 Opus         |                            26   |                    15.9 |
| Mistral Large 2       |                            31.2 |                     9.2 |
| DeepSeek-V2.5         |                            32.8 |                    25.6 |
| Multi-turn ensemble   |                            10.9 |                     8.5 |
| Grok 2                |                            24.1 |                     7.7 |

Accuracy benchmarks can also be considered for a fuller assessment. I've created a separate benchmark to test LLMs based on [New York Times Connections](https://github.com/lechmazur/nyt-connections/).

![image](https://github.com/user-attachments/assets/50a518ad-2745-4a7f-a2df-69bcebfc27b8)


## Interesting Hallucination Results
- o1-preview will be the top-performing single model across most hallucination rankings, though its improvement over GPT-4o may be somewhat underwhelming
- o1-mini ranks below GPT-4o. Don't expect its reasoning to help it hallucinate less compared to larger models.
- GPT-4o shows a significant improvement over GPT-4 Turbo.
- Gemini 1.5 Pro (September) performs better than Claude models!
- Llama models tend to respond cautiously, resulting in fewer confabulations but higher non-response rates


## Additional Notes
- A popular hallucination leaderboard on GitHub uses a model for evaluation of document summaries, but I found this to lead to a very high error rate and different rankings. This approach can be very misleading.
- While the initial set of questions was suggested by LLMs, the final 192 questions were all painstakingly human-verified to have no answers in the provided texts. Only a percentage of LLM-suggested questions were unequivocally answer-free.
- Despite clear prompts, LLMs often generated compound questions that effectively asked for two answers. These were removed in a separate judging step.
- The benchmark includes questions where at least one LLM confabulated, in order to minimize the number of questions requiring human assessment. Because of this, and since the questions are intentionally adversarial, the absolute percentage should not be used to infer that LLMs frequently confabulate. This leaderboard does not reflect a "typical" hallucination rate.
- In some cases, LLMs failed to provide valid responses to the questions, such as skipping certain questions altogether. This occurred only once for the human-selected questions without valid answers in the text (bad Gemma, bad), but happened more frequently for questions with valid answers. These questions were discarded.
- A temperature setting of 0 was used
- Multi-turn ensemble is my unpublished system. It utilizes multiple LLMs, multi-turn dialogues, and other proprietary techniques. It is slower and more costly to run but it does very well. It [outperforms](https://x.com/LechMazur/status/1828804485033992514/photo/1) non-o1 LLMs on MMLU-Pro and GPQA.


## Updates and Other Benchmarks
- Oct. 15, 2024: Grok 2 added
- Follow [@lechmazur](https://x.com/LechMazur) on X (Twitter) for other upcoming benchmarks and more.
