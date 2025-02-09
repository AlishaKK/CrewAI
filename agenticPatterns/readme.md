**Workflow: Evaluator-optimizer**

In the evaluator-optimizer workflow, one LLM call generates a response while another provides evaluation and feedback in a loop.
![image](https://github.com/user-attachments/assets/f9c802f8-f575-4110-92e6-e0dba78bfb3c)

Yes, in the **evaluator-optimizer workflow**, you have:  

1. **Generator (Optimizer LLM)** → Creates the initial response.  
2. **Evaluator (Evaluation LLM or Human)** → Reviews the response, gives feedback.  
3. **Generator (Optimizer LLM)** → Improves the response based on feedback.  

It keeps refining until the response meets the required quality.  

Example:  
- **Generator:** Translates a sentence.  
- **Evaluator:** Checks if the meaning, tone, and grammar are correct.  
- **Generator:** Fixes issues based on feedback.  

This loop continues until the output is perfect! 🚀


