## Problem
...  
If you want to have your own chat bot deployed and want to have back and forth communication with it then you can use the following code.  ...

## Environment
... Visual Studio Code, Python ...

## How you fix it
... You need to download a llama model first from huggingface. Then you need to have a server for deployment or you can even host it on your machine locally and use postman to do back and forth communication. I am also using the time library to track the time taken by the model to load and to complete the prompt request.
 ...

## Solution
...
from llama_cpp import Llama

llm = Llama(model_path = "Path to your model", chat_format="llama-2", n_threads=2, n_threads_batch=2, n_batch=512, last_n_tokens_size=32, n_ctx=512)

class PromptRequest(BaseModel):
    Subject: str
    topic: str
    difficulty: str
    standard: int

@app.post("/Prompt")
async def OutputPrompt(request: PromptRequest):
    now = time.time()

    system = f"""You are a {request.Subject} teacher. You are given a task to create 3 Tests on {request.topic}. """
    
    user = f"""The difficulty level should be {request.difficulty} and you need to ensure that it is up to the level of {request.standard} class students"""
    
    refined_prompt = [{f"role": "system", "content": system},{"role": "user","content": user}]
       
    print("Time Taken to generate response: ",time.time() - now)
    
    return {"refined_prompt": refined_prompt}
...