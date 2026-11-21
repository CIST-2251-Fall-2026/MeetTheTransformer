# DistilGPT2 Text Generation Experiment
 
## Model and Versions
This project uses the model distilbert/distilgpt2 from Hugging Face. It is an 82-million-parameter English text-generation model distributed under the Apache 2.0 License. I ran it with PyTorch 2.15.0+cpu and Transformers 5.23.0 on Python 3.13.9.
 
## Setup
1. Install the packages by running python -m pip install torch transformers.
2. Open Comp5Transformer.ipynb in VS Code and choose a Python kernel that has these packages installed.
3. Run the cells from top to bottom. The first run downloads the model files into the Hugging Face cache.
 
## Training Versus Inference
Training is when a model learns by changing its weights using large amounts of example text. Inference is when a trained model is used to produce output and its weights do not change. This project only uses inference. I did not train DistilGPT2. I loaded it and used it to generate text.
 
## Tokens
Tokens are the pieces of text the model reads and writes. A token can be a whole word, part of a word, or punctuation and each token has a number called a token ID. In my notebook, the word "Tokenization" was split into two tokens, "Token" and "ization," while words like "cat" and "unbelievable" stayed as one token each.
 
## How Context Affects Generation
The model writes one token at a time based on all the text that comes before it, so the prompt is the context that guides the output. When I asked for the same advice in three different ways and kept the seed and settings the same, the answers changed so much. Adding "for a beginner" gave a short answer to ask a teacher and asking it as a question gave a vague answer about teaching instead of learning.
 
## What I Learned from Sampling
The seed and temperature runs used the prompt "The best way to learn programming is" with up to 50 new tokens and sampling turned on. Running it twice with seed 42 gave the same text, so another developer can reproduce my results by using the same seed. Seed 7 gave different text. When I changed only the temperature, 0.3 gave one short sentence followed by blank lines, 1.0 gave a longer answer that drifted off topic and 1.5 made up a quote from a named person as if it were real. Higher temperatures made the output more varied but also more likely to invent details.
 
## Surprising Behavior and Risk
At temperature 1.5 the model invented a quote from a named person at a university. In a customer-facing product, this could make customers believe false information or think a real person or school said something they never said. I also saw the model write an unprompted line, "I love you, and I hate you" and produce a hidden right-to-left override character in the middle of a word. A product using this model would need checks to catch made-up facts, off-topic text, and hidden characters.
 
## Results
All code and outputs are in Comp5Transformer.ipynb, with written notes after the tokenization, temperature, prompt wording and failure steps.