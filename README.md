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
1. No definitive list of writing styles exists. The provided [writing style guide](https://viktorbezdek.github.io/definitive-llm-writing-style-guide/) is comprehensive but needs refinement to a smaller set of styles to:
  - Enhance the relevance of similarity search results when users query the existing works' database.
  - Reduce the token length of API calls, which is cost-sensitive.
2. When selecting writing styles, the guide's universality should be balanced with the need for specificity to Mishima's texts. Prioritize identifying Mishima's most distinctive writing styles. Domain expertise is needed here.