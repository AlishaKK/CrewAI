### **🛠️ Orchestrator-Workers in One Line:**  
**An orchestrator (manager) breaks a big task into smaller subtasks and assigns them to worker agents (helpers) to complete efficiently.**  

---

### **🚀 How It Works (Simple & Fast)**
1️⃣ **Orchestrator:** Gives instructions to AI workers.  
2️⃣ **Workers:** Complete subtasks (e.g., writing, refining, summarizing).  
3️⃣ **Final Output:** The orchestrator combines results into one polished response.  

---

### **💡 Code: AI Writing & Refining a Blog**  

```python
from crewai.flow.flow import Flow, start, listen
from litellm import completion

class OrchestratorFlow(Flow):
    model = "gpt-4o-mini"

    @start()  # 📝 Step 1: AI writes a draft
    def initial_draft(self):
        response = completion(
            model=self.model,
            messages=[{"role": "user", "content": "Write a blog post on AI automation."}]
        )
        draft = response["choices"][0]["message"]["content"].strip()
        print("\n📝 Draft Created:\n", draft)
        return draft  

    @listen(initial_draft)  # ✨ Step 2: AI refines the draft
    def refine_draft(self, draft):
        response = completion(
            model=self.model,
            messages=[{"role": "user", "content": f"Improve this for clarity: {draft}"}]
        )
        refined = response["choices"][0]["message"]["content"].strip()
        print("\n🎨 Refined Draft:\n", refined)
        return refined  

if __name__ == "__main__":  # 🚀 Run the process
    flow = OrchestratorFlow()
    final_draft = flow.kickoff()
    print("\n✅ Final Blog Post:\n", final_draft)
```

---

### **🎯 What Happens?**
✅ AI **writes** a draft → 🎨 AI **improves** it → ✅ **Final version is ready!**  

🔥 **This is like a boss assigning tasks to a smart AI team!**  

