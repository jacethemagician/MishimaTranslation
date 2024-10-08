# Mishima Writing Stylizer

## Overview
This project aims to transform a given text input into a style reminiscent of Yukio Mishima's writing. The workflow involves setting up a database of Mishima's works, finding similar texts, and composing prompts for generating the final output using LLMs.

![Mishima Works Banner](assets/mishima_works_banner.jpg)

*Image Source: [PR Times](https://prtimes.jp/main/html/rd/p/000000051.000047877.html)*

## Steps

<img src="assets/mishima_architecture.png" alt="Architecture" width="640" height="605"/>

1. **Set Up a Vector Database of Mishima's Works**:
   - **Text Collection**:
     - Store original texts of Mishima's works. Automating this process is ideal due to the tedious nature of manual collection.
     - Need to consider publishing versions, translators, language of choice, and copyrights.
   - **Sentence Splitting**:
     - Use the NLP module `spacy` to split texts into sentences. The base text model is Chinese (`zh_core_web_sm`).
   - **Semantic Chunking**:
     - Use embedding to find the breakpoints of certain percentile threshold between sentences with a context window 
   - **Summary Storing**
     - Include attributes such as subject matter, sentence structure, emotions etc...

2. **Find Top N Similar Texts**
   - Given a text input, first summarize it using the same prompt for stroing documents, then search the vectorstore to find the top N similar texts.

3. **Compose a Stylizer Prompt**
   - Create a structured prompt for generating the output, including:
     - An arbitrary prompt to set the role and instructions.
     - Few-shot examples retrieved from vectorstore.
     - Raw user input.

4. **Generate the Response**
   - Use the composed prompt to generate a response in the style of Yukio Mishima then display it on web.


## TODO List
| Task                                                                 | Status    | Comment                                                                                     | Priority  |
|----------------------------------------------------------------------|-----------|---------------------------------------------------------------------------------------------|-----------|
| Prompt - generate prompt for prompt engineering                      | Pending   | I expect a lot of the work will be done here, finding optimized prompt. Research on effective prompting is required, especially for novel text generation. This step will be revised constantly.                                                                                            | High      |
| Data - replace text with English                           | Pending   | Need to try out both English and Chinese to figure out which performs better. Intuition and model profile suggest English.                                                                                            | Medium    |
| Prompt - add high-dimensional data about style, must collectively state the components of literary analysis | Pending   | Optimize the summarization part, or look at other query transformations [must add domain expertise] | Medium      |
| UIUX -Use stream output to mimic handwriting                               | Pending   | UX improvement                                                                                            | Medium       |
| Chunking - if the sentence is short, compare with the surrounding embeddings and assign to that chunk | Pending   | Slight optimization on chunking gives better original text during prompting, which is a part but might not be as important as the prompt itself.                                                                         | Low    |
| Evaluation - add benchmark                                           | Pending   | Need a way to measure how good the result is. Probably human eval, maybe benchmark.                                                                                            | Low      |
| Database - record text source and subject                             | Pending   | better categorization and display in frontend.                                                                                            | Low    |
| UIUX - display top n original texts + metadata for the selected query | Pending   | Makes the whole application look better                                                                                            | Low    |
| Model - switch to a better OpenAI English model                      | Completed   | It is intuitive to use better model. Switched to gpt-4o from got-4o-mini, and result is emperically significantly better.                                                                                            | High       |
| Model - Find a model to fine-tune on Chinese/novels | Cancelled | Unless there exist an industry-standard level LLM, finding a niche model probably means I need to localize the model hosting service, losing access to OpenAI API.                                                                                            | High       |