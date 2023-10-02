# Understanding Integer Addition in Transformers

Understanding the inner workings of machine learning models like Transformers is vital for their safe and ethical use. This repository contains a CoLab that presents an in-depth analysis of a one-layer Transformer model trained for integer addition.

The CoLab defines, trains and analyses a 1 layer Transformer model that performs integer addition e.g. 33357+82243=115600. Each digit is a separate token. For 5 digit addition, the model is given 12 "question" (input) tokens, and must then predict the corresponding 6 "answer" (output) tokens:   

![QuestionAnswer](./QuestionAnswer.svg?raw=true "Question Answer Shape")


