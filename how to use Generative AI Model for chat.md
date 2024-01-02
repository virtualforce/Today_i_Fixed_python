## Problem
...  
If you want to have your own chat bot then you can use the following code.  ...

## Environment
... Visual Studio Code, Python ...

## How you fix it
... You need to download a llama model first from huggingface. First of all check all of the system requirements and try to go for a quantized model and place it in your project folder. Then you need to use the llama library to adjust the parameters according to your needs and then give a prompt. 
(in case you want to try or use different models then use relevant library. However, the procedure would most porbably remain the same)
 ...

## Solution

...
from llama_cpp import Llama

llm = Llama(model_path = "Path to your model", chat_format="llama-2", n_threads=2, n_threads_batch=2, n_batch=512, last_n_tokens_size=32, n_ctx=512)

prompt = "Write a linear regression in python"

response= llm(prompt=prompt, max_tokens=256 temperature=0.5, top_p=0.75, repeat_penalty=1.2,top_k=30, )

print(response)
...