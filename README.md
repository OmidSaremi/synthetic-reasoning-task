# synthetic-reasoning-task

Experimens on reasoning capacity of transformers models (T5 here). In this set of experiments, we experiment with the task in https://arxiv.org/pdf/2206.04301.pdf. Work in progress with colleagues.

-LEGO task: input describes a sequence of variable assignments as well as operations on these variables by a fixed (mathematical) group. The task is to resolve the symbols to their (binary values)
-The paper uses Encoder-only transofmers with a classification head, where the task is formulated as a multi-label classification problem
-Each binary output corresponds to an input variable in the same order. A Sample:
Input:  'a=+v; c=-g; f=+k; v=-1; g=+f; k=+a’ 
Output: (a=-1, c=1, f=-1, v=-1, g=-1, k=-1)

Our observation is that, this setting is a lot riccher with "textual encoding" of the target and generating the output in an autoregressive way at inference time.
-It allows one to experiment with the "order" of symbol resolution. For instance
"Resolution" order: ‘v=-1;a=-1;k=-1;f=-1;g=-1;c=1’
"Input" order: 'a=-1, c=1, f=-1, v=-1, g=-1, k=-1’

-Text is a natural format in human reasoning tasks
-Separates encoding from compute by fixing the encoding to be a commonly accepted format

Our experiments show:

In the "resolution" order (fixed compute budget of a single epoch with small batch size)
-Almost fully generalizes:  99.8% (~\pm  0.2) in a single epoch from only 6800 training samples 
-Generates the solutions in the resolution order (logic)
-While "input" order test accuracy after a single epoch —> 7.2% (\pm 0.31)

It appear that the "resolution" order provides “hint” as to how to the model should solve the task.