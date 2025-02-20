
### **🔀 Definition of Routing:**  
**Routing** classifies an input and directs it to a specialized follow-up task, allowing for separation of concerns and more specialized prompts.  

---


![image](https://github.com/user-attachments/assets/b72e9e74-f3ac-4bd8-b92d-89a589875ab1)


### **📌 When to Use Routing?**  
✅ **Handling different content types** (e.g., Tech vs. Lifestyle blogs)  
✅ **Optimizing multiple tasks separately** (avoiding one-size-fits-all prompts)  
✅ **Building modular and scalable AI workflows**  
✅ **Improving accuracy by directing inputs to specialized functions**  

---

### **💡 Simple Code Example: AI Chooses the Right Path**  

```python
from crewai.flow.flow import Flow, start, listen, router
from litellm import completion  

class RoutedFlow(Flow):
    model = "gpt-4o-mini"

    @start()  # Step 1: Generate a blog topic
    def generate_topic(self):
        response = completion(
            model=self.model,
            messages=[{"role": "user", "content": "Suggest a blog topic for 2025."}]
        )
        topic = response["choices"][0]["message"]["content"].strip()
        
        # Classify the topic as tech or lifestyle
        self.state["is_tech"] = "tech" in topic.lower()  
        
        print(f"\n📝 Generated Topic: {topic}")
        return topic  

    @router(generate_topic)  # Step 2: Route based on topic type
    def route_topic(self):
        return "tech_route" if self.state.get("is_tech") else "lifestyle_route"

    @listen("tech_route")  # Step 3A: Generate Tech Blog Outline
    def generate_tech_outline(self, topic):
        response = completion(
            model=self.model,
            messages=[{"role": "user", "content": f"Create a tech blog outline for: {topic}"}]
        )
        outline = response["choices"][0]["message"]["content"].strip()
        print("\n📌 Tech Blog Outline:\n", outline)
        return outline  

    @listen("lifestyle_route")  # Step 3B: Generate Lifestyle Blog Outline
    def generate_lifestyle_outline(self, topic):
        response = completion(
            model=self.model,
            messages=[{"role": "user", "content": f"Create a lifestyle blog outline for: {topic}"}]
        )
        outline = response["choices"][0]["message"]["content"].strip()
        print("\n📌 Lifestyle Blog Outline:\n", outline)
        return outline  

if __name__ == "__main__":  # Run the workflow
    flow = RoutedFlow()
    final_output = flow.kickoff()
    print("\n✅ Final Blog Outline:\n", final_output)
```

---

### **🎯 What Happens?**  
✔️ **AI generates a topic**  
✔️ **AI determines if it's Tech or Lifestyle**  
✔️ **AI follows the correct path and generates the right blog outline** ✅  

 **Use Routing when different types of inputs require separate processing paths!** 🚀
