# LLM Confabulation (Hallucination) Leaderboard for RAG

This benchmark evaluates large language models (LLMs) based on how frequently they produce non-existent answers (confabulations or hallucinations) in response to misleading questions that are based on provided text documents. These documents are recent articles not yet included in the LLM training data. Minimizing these types of confabulation is crucial when using Retrieval-Augmented Generation (RAG). The questions are intentionally crafted to be challenging.

As of Feb 7, 2025, 192 questions, confirmed by a human to lack answers in the provided texts, have been carefully curated and assessed. The number of questions will ideally increase over time, and the error margins will continue to narrow. However, the current dataset is already sufficient to differentiate between various models.

## Combined Evaluation
Combining confabulation and non-response rates enables a comprehensive ranking. Depending on your priorities, you may prefer [fewer confabulations or fewer non-responses](https://lechmazur.github.io/leaderboard1.html). 

### 50-50 ranking

![leaderboard_dotplot](https://github.com/user-attachments/assets/66320408-69cb-47ae-bdfc-38092bc4a9e3)

|Rank|Model|Confab %|Non-Resp %|Weighted|
|---:|---|---:|---:|---:|
|1|Multi-turn ensemble|11.4|8.5|9.94|
|2|DeepSeek R1|14.6|7.7|11.13|
|3|o1|10.3|12.2|11.21|
|4|Gemini 2.0 Flash Think Exp 01-21|13.0|10.1|11.56|
|5|o1-preview|16.8|7.4|12.07|
|6|Gemini 1.5 Pro (Sept)|16.8|9.7|13.24|
|7|GPT-4o|18.4|8.5|13.44|
|8|Llama 3.1 405B|11.9|20.8|16.35|
|9|o3-mini (medium reasoning)|24.3|8.5|16.43|
|10|Gemini 2.0 Pro Exp 02-05|13.0|21.0|16.97|
|11|o1-mini|24.3|10.2|17.25|
|12|DeepSeek-V3|21.1|14.5|17.79|
|13|Qwen 2.5 72B|30.3|5.8|18.03|
|14|Grok 2 12-12|24.3|14.5|19.43|
|15|Claude 3.5 Sonnet 2024-10-22|11.9|27.8|19.82|
|16|Mistral Large 2|30.8|9.2|19.98|
|17|Qwen 2.5 Max|28.1|12.3|20.20|
|18|Claude 3 Opus|26.5|15.9|21.21|
|19|MiniMax-Text-01|40.0|3.1|21.54|
|20|Claude 3.5 Sonnet Old|27.0|16.1|21.58|
|21|Llama 3.1 70B|13.5|31.4|22.46|
|22|Llama 3.3 70B|16.2|29.4|22.78|
|23|Grok 2|24.3|22.7|23.53|
|24|Gemini 1.5 Flash|42.2|5.2|23.69|
|25|Grok Beta|24.3|23.4|23.84|
|26|Mistral Small 3|35.7|12.5|24.10|
|27|Gemma 2 27B|44.3|7.1|25.71|
|28|Gemini 2.0 Flash Exp|23.2|29.9|26.58|
|29|Gemini 2.0 Flash|23.2|30.3|26.75|
|30|Microsoft Phi-4|48.6|6.0|27.28|
|31|GPT-4 Turbo|23.8|31.4|27.59|
|32|Amazon Nova Pro|51.4|5.8|28.58|
|33|DeepSeek-V2.5|33.5|25.6|29.54|
|34|Claude 3 Haiku|57.3|10.4|33.86|
|35|Claude 3.5 Haiku|63.2|6.8|35.03|
|36|GPT-4o mini|57.3|13.6|35.44|



## Confabulation and Non-Response Rates

![01_confabulations_bars](https://github.com/user-attachments/assets/abbe417c-c91e-4f22-8dc9-579c9d699cd0)

The raw confabulation rate alone isn't sufficient for meaningful evaluation. A model that simply declines to answer most questions would achieve a low confabulation rate. To address this, the benchmark also tracks the LLM non-response rate using the same prompts and documents but specific questions with answers that are present in the text. Currently, 2,436 hard questions (see the prompts) with known answers in the texts are included in this analysis.

![02_nonresponse_bars](https://github.com/user-attachments/assets/8528206a-0ab0-4a69-a174-75d3b219ce93)

Accuracy benchmarks can also be considered for a fuller assessment. I've created a separate benchmark to test LLMs based on the extended version of the [New York Times Connections](https://github.com/lechmazur/nyt-connections/).

![nyt_connections_chart](https://github.com/user-attachments/assets/080476e4-562c-47a4-ac1a-f34b7c05f22c)



## Interesting Hallucination Results
- Reasoning appears to help. DeepSeek R1 performs much better than DeepSeek-V3, for example
- GPT-4o shows a significant improvement over GPT-4 Turbo.
- Gemini 1.5 Pro (September) performs better than Claude models, but there is no improvement with Gemini 2.0 Pro Exp 02-05.
- Llama models tend to respond cautiously, resulting in fewer confabulations but higher non-response rates


## Additional Notes
- A popular hallucination leaderboard on GitHub uses a model for evaluation of document summaries, but I found this to lead to a very high error rate and different rankings. This approach can be very misleading.
- While the initial set of questions was suggested by LLMs, the final 192 questions were all painstakingly human-verified to have no answers in the provided texts. Only a percentage of LLM-suggested questions were unequivocally answer-free.
- Despite clear prompts, LLMs often generated compound questions that effectively asked for two answers. These were removed in a separate judging step.
- The benchmark includes questions where at least one LLM confabulated, in order to minimize the number of questions requiring human assessment. Because of this, and since the questions are intentionally adversarial, the absolute percentage should not be used to infer that LLMs frequently confabulate. This leaderboard does not reflect a "typical" hallucination rate.
- In some cases, LLMs failed to provide valid responses to the questions, such as skipping certain questions altogether. This occurred only once for the human-selected questions without valid answers in the text (bad Gemma, bad), but happened more frequently for questions with valid answers. These questions were discarded.
- A temperature setting of 0 was used
- Multi-turn ensemble is my unpublished system. It utilizes multiple LLMs (that existed in Oct 2024), multi-turn dialogues, and other proprietary techniques. It is slower and more costly to run but it does very well. It [outperforms](https://x.com/LechMazur/status/1828804485033992514/photo/1) non-o1 LLMs on MMLU-Pro and GPQA.


## Updates and Other Benchmarks
- Feb 7, 2025: DeepSeek R1, o1, o3-mini (medium reasoning effort), DeepSeek-V3, Gemini 2.0 Flash Thinking Exp 01-21, Qwen 2.5 Max, Microsoft Phi-4, Amazon Nova Pro, Mistral Small 3, MiniMax-Text-01 added.
- Nov. 5, 2024: Claude 3.5 Haiku added
- Oct. 23, 2024: Grok Beta added
- Oct. 23, 2024: Claude 3.5 Sonnet (2024-10-22) added
- Oct. 15, 2024: Grok 2 added
- Also check out the [LLM Step Game](https://github.com/lechmazur/step_game), [LLM Thematic Generalization Benchmark](https://github.com/lechmazur/generalization), [LLM Creative Story-Writing Benchmark](https://github.com/lechmazur/writing), [LLM Deception Benchmark](https://github.com/lechmazur/deception) and [LLM Divergent Thinking Creativity Benchmark](https://github.com/lechmazur/divergent).
- Follow [@lechmazur](https://x.com/LechMazur) on X (Twitter) for other upcoming benchmarks and more.

