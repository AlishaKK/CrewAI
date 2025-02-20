**Workflow: Evaluator-optimizer**


![image](https://github.com/user-attachments/assets/f9c802f8-f575-4110-92e6-e0dba78bfb3c)


**In the evaluator-optimizer workflow, one LLM call generates a response while another provides evaluation and feedback in a loop.**  

---

### **🚀 How It Works (Simple & Clear)**  
1️⃣ **📝 Generator AI** → Writes an initial response.  
2️⃣ **🔍 Evaluator AI** → Reviews and suggests improvements.  
3️⃣ **✨ Generator AI** → Refines based on feedback.  
4️⃣ **♻️ Repeats** until high-quality output is achieved!  

---

### **💡 Code Example: AI Writing & Improving a Summary**  

```python
from crewai.flow.flow import Flow, start, listen
from litellm import completion

class EvaluatorOptimizerFlow(Flow):
    model = "gpt-4o-mini"

    @start()  # 📝 Step 1: AI creates a draft
    def generate_response(self):
        response = completion(
            model=self.model,
            messages=[{"role": "user", "content": "Summarize the benefits of AI in education."}]
        )
        draft = response["choices"][0]["message"]["content"].strip()
        print("\n📝 Initial Summary:\n", draft)
        return draft  

    @listen(generate_response)  # 🔍 Step 2: AI evaluates & refines
    def evaluate_and_optimize(self, draft):
        response = completion(
            model=self.model,
            messages=[{"role": "user", "content": f"Review and enhance this summary for clarity: {draft}"}]
        )
        improved = response["choices"][0]["message"]["content"].strip()
        print("\n✨ Improved Summary:\n", improved)
        return improved  

if __name__ == "__main__":  # 🚀 Run the process
    flow = EvaluatorOptimizerFlow()
    final_summary = flow.kickoff()
    print("\n✅ Final Summary:\n", final_summary)
```

---

### **🎯 What Happens?**  
✔️ **AI writes** a summary → 🔍 **AI evaluates & improves** → 🔄 **Loop continues** → ✅ **Final version is polished!**  

🔥 **It’s like an AI writer and AI editor working in harmony!**  

Would you like an **advanced version** with multiple improvement cycles for even better results? 🚀
