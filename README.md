# Understanding Integer Addition in Transformers

Understanding the inner workings of machine learning models like Transformers is vital for their safe and ethical use. 
This repository contains a CoLab ( [./Understanding_Addition_in_Transformers.ipynb](https://github.com/apartresearch/conceptual-interp/blob/main/Understanding_Addition_in_Transformers.ipynb) ) that presents an in-depth analysis of a one-layer Transformer model trained for integer addition.

The CoLab creates, trains and then analyses a 1 layer Transformer model that performs integer addition e.g. 33357+82243=115600. Each digit is a separate token. For 5 digit addition, the model is given 12 "question" (input) tokens, and the model must then predict the correct 6 "answer" (output) tokens:   

![QuestionAnswer](./QuestionAnswer.svg?raw=true "Question Answer Shape")

This CoLab allowed the authors to understand the model's addition algorithm, summarised in this diagram: 

![StaircaseA3_Summary](./StaircaseA3_Summary.svg?raw=true "StaircaseA3_Summary")

Summary diagram legend: **A:** The 5 digit question is revealed token by token. The highest-value digit is revealed first. **B:** From the "=" token, the model attentions heads focus on successive pairs of digits, giving a 'staircase' attention pattern visible in 15 digit, 5 digit, etc addition. **C:** The 3 heads are time-offset from each other by 1 token so in each epoch data from 3 tokens is available. **D:** To calculate A3, the 3 heads do independent simple mathematical calculations on D3, D2 & D1. The results are combined by the MLP layer using 60 trigrams. A3 is calculated one token before it is needed. This approach is repeated for all answer digits.

This more detailed diagram shows how the model's addition algorithm is "coded" in the attention heads:
![StaircaseA3_Detailed](./StaircaseA3_Detailed.svg?raw=true "StaircaseA3_Detailed")

Detailed diagram legend: **A:** For A3, the addition algorithm combines information from digits 3, 2 and 1. **B:** 1st Head calculates MC1 on digit 1. **C:** 2nd Head calculates MC1 and MS9 (which are independent of each other and so at most one is true) on digit 2. **D:** 3rd Head does Base Add on digit 3. **E:** The MLP layer uses trigrams to combine the information from the 3 heads to give the final answer A3. 

## Tips for using the Colab
 * You can run all the code in the CoLab notebook yourself in Google CoLab ( https://colab.research.google.com/ ). You can change the code and experiment.
 * To use the notebook, in Google CoLab, **you will need to** go to Runtime > Change Runtime Type and select GPU as the hardware accelerator.
 * The graphs are interactive!
 * Use the table of contents pane in the sidebar to navigate
 * Collapse irrelevant sections with the dropdown arrows
 * Search the page using the search in the sidebar, not CTRL+F
