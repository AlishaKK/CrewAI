

### **Prompt Chaining – Simple Explanation**  

**What is it?**  
Prompt chaining breaks a big task into **smaller, connected steps**, where each LLM output becomes the input for the next step. This improves accuracy but may take more time.  
![image](https://github.com/user-attachments/assets/bba5be5c-f28f-499f-b20c-e6a9f9546e9f)


### **How it Works:**  
1. **Step 1:** One LLM does the first part of the task.  
2. **Step 2:** The output is checked (optional "gate" to ensure correctness).  
3. **Step 3:** Another LLM continues based on the previous output.  

### **When to Use It?**  
✅ When a task can be divided into **clear, fixed steps**.  
✅ When you need **higher accuracy** and don’t mind a bit more time.  

### **Examples:**  
1️⃣ **Marketing Copy → Translation**  
   - First LLM: Writes marketing content.  
   - Second LLM: Translates it into another language.  

2️⃣ **Document Writing Process**  
   - First LLM: Creates an outline.  
   - "Gate" checks if the outline is good.  
   - Second LLM: Writes the full document based on the outline.



---

### **🚀 How It Works (Step-by-Step)**  
1️⃣ **AI generates a topic** → ✍️ Example: "Future of AI in 2025."  
2️⃣ **AI uses that topic** → 📝 Creates a blog outline based on it.  
3️⃣ **Results are linked** → 🔄 One response feeds into the next.  

---

### **💡 Simple Code Example: AI Generates a Topic & Outline**  

```python
from crewai.flow.flow import Flow, start, listen
from litellm import completion  

class TopicOutlineFlow(Flow):
    model = "gpt-4o-mini"

    @start()  # Step 1: AI generates a topic
    def generate_topic(self):
        response = completion(
            model=self.model,
            messages=[{"role": "user", "content": "Suggest a creative blog topic for 2025."}]
        )
        topic = response["choices"][0]["message"]["content"].strip()
        print(f"\n📝 Blog Topic: {topic}")
        return topic

    @listen(generate_topic)  # Step 2: AI creates an outline from the topic
    def generate_outline(self, topic):
        response = completion(
            model=self.model,
            messages=[{"role": "user", "content": f"Create a detailed outline for a blog on '{topic}'."}]
        )
        outline = response["choices"][0]["message"]["content"].strip()
        print("\n📌 Blog Outline:\n", outline)
        return outline

if __name__ == "__main__":  # 🚀 Run the process
    flow = TopicOutlineFlow()
    final_outline = flow.kickoff()
    print("\n✅ Final Blog Outline:\n", final_outline)
```

---

### **🎯 What Happens?**  
✔️ **AI picks a topic** → 📌 **AI builds an outline from it** → 🔗 **Each step connects to the next!**  




