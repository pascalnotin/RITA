# <img src="_static/lighton_small.png" width=60/> RITA: a Study on Scaling Up Generative Protein Sequence Models

[![GitHub license](https://img.shields.io/badge/license-MIT-blue.svg)](LICENSE)  [![Twitter](https://img.shields.io/twitter/follow/LightOnIO?style=social)](https://twitter.com/LightOnIO)

RITA is a family of autoregressive protein models, developed by a collaboration of [Lighton](https://lighton.ai/), the [OATML group](https://oatml.cs.ox.ac.uk/) at Oxford, and the [Debbie Marks Lab](https://www.deboramarkslab.com/) at Harvard.

Model | #Params | d_model | layers | lm loss uniref-100
--- | --- | --- | --- | --- | 
[Small](https://huggingface.co/lightonai/RITA_s) | 85M  | 768 | 12 | 2.31
[Medium](https://huggingface.co/lightonai/RITA_m) | 300M | 1024 | 24 | 2.01
[Large](https://huggingface.co/lightonai/RITA_l)| 680M | 1536 | 24 | 1.82
[XLarge](https://huggingface.co/lightonai/RITA_xl)| 1.2B | 2048 | 24 | 1.70 

## Results
A link to the paper with all the results will be provided soon.
<p align="center">
<img src="_static/perplexity.png" width=800/>
</p>

## Usage 
Instantiate a model like so:

    from transformers import AutoModel, AutoModelForCausalLM
    model = AutoModelForCausalLM.from_pretrained("lightonai/RITA_s, trust_remote_code=True")
    tokenizer = AutoTokenizer.from_pretrained("lightonai/RITA_s")

for generation use we support pipelines:
   
   
    rita_gen = pipeline('text-generation', model=model, tokenizer = tokenizer)
    sequences = rita_gen("MAB", max_length=20, do_sample=True, top_k=950, repetition_penalty=1.2, 
                         num_return_sequences=2, eos_token_id=2)
    for seq in sequences:
        print(f"seq: {seq['generated_text'].replace(' ', '')}")

## How to cite
Coming soon.
