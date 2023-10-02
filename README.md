# Understanding Integer Addition in Transformers

Understanding the inner workings of machine learning models like Transformers is vital for their safe and ethical use. This repository contains a CoLab that presents an in-depth analysis of a one-layer Transformer model trained for integer addition.

The CoLab defines, trains and analyses a 1 layer Transformer model that performs integer addition e.g. 33357+82243=115600. Each digit is a separate token. For 5 digit addition, the model is given 12 "question" (input) tokens, and must then predict the corresponding 6 "answer" (output) tokens:   

![QuestionAnswer](./QuestionAnswer.svg?raw=true "Question Answer Shape")

This CoLab allowed the authors to understand the model's addition algorithm, summarised in this diagram: 

![StaircaseA3_Summary](./StaircaseA3_Summary.svg?raw=true "StaircaseA3_Summary")

**A:** The 5 digit question is revealed token by token. The highest-value digit is revealed first. **B:** From the "=" token, the model attentions heads focus on successive pairs of digits, giving a 'staircase' attention pattern visible in 15 digit, 5 digit, etc addition. **C:** The 3 heads are time-offset from each other by 1 token so in each epoch data from 3 tokens is available. **D:** To calculate A3, the 3 heads do independent simple mathematical calculations on D3, D2 & D1. The results are combined by the MLP layer using 60 trigrams. A3 is calculated one token before it is needed. This approach is repeated for all answer digits.
