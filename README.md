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


## Challenges / TODOs
1. 模型-找在中文/小说上fine tune的生成模型(high probability localization of llm)
2. 文本选择-文本替换成英文
3. prompt-增加关于style部分的高维数据，必须要集体说出literary analysis的组成->优化summarize这部分，或看别的query transformation【必须要加domain expertise】
4. prompt-生成prompt做prompt engineering
5. chunking-如果sentence字少，跟上下embedding作比较，划分到那部分chunk->chunk是“丰富的”
6. evalution-增加benckmark
7. 模型-换成更好的openai英文模型