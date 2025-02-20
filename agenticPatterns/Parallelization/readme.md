### **🚀 Definition of Parallelization:**  
**Parallelization** allows multiple tasks to run at the same time, with their outputs aggregated programmatically. It can be used in two ways:  
1. **Sectioning** – Splitting a task into independent subtasks that run in parallel.  
2. **Voting** – Running the same task multiple times to generate diverse outputs.  

---


![image](https://github.com/user-attachments/assets/85ccccde-ff44-4836-bcd5-837f4271a137)


### **📌 When to Use Parallelization?**  
✅ When tasks don’t depend on each other and can run at the same time.  
✅ When you need multiple diverse outputs for better decision-making.  
✅ When you want to speed up execution by running tasks in parallel.  

---

## **💡 Code Example: Running Multiple Tasks in Parallel**
### **1️⃣ Using `or_`: Run Multiple Tasks and Aggregate the First Completed One**
```python
from crewai.flow.flow import Flow, start, listen, or_
from litellm import completion  

class ParallelFlow(Flow):
    model = "gpt-4o-mini"

    @start()
    def generate_variant_1(self):
        response = completion(
            model=self.model,
            messages=[{"role": "user", "content": "Suggest a creative blog topic variant #1."}]
        )
        variant = response["choices"][0]["message"]["content"].strip()
        print(f"📝 Variant 1: {variant}")
        return variant

    @start()
    def generate_variant_2(self):
        response = completion(
            model=self.model,
            messages=[{"role": "user", "content": "Suggest a creative blog topic variant #2."}]
        )
        variant = response["choices"][0]["message"]["content"].strip()
        print(f"📝 Variant 2: {variant}")
        return variant

    @listen(or_(generate_variant_1, generate_variant_2))  # Runs when any one task completes
    def aggregate_variants(self, variant):
        print("✅ First Completed Variant:", variant)
        return variant

if __name__ == "__main__":
    flow = ParallelFlow()
    final_output = flow.kickoff()
    print("🎯 Final Aggregated Output:", final_output)
```
📌 **What Happens?**  
✔️ Two tasks run at the same time.  
✔️ As soon as one finishes, the aggregation function runs.  
✔️ This is useful when you only need the first available result.  

---

### **2️⃣ Using `and_`: Wait Until Both Tasks Finish Before Aggregating**
```python
from crewai.flow.flow import Flow, start, listen, and_
from litellm import completion  

class AndAggregationFlow(Flow):
    model = "gpt-4o-mini"

    @start()
    def generate_slogan(self):
        response = completion(
            model=self.model,
            messages=[{"role": "user", "content": "Generate a slogan for a futuristic brand."}]
        )
        slogan = response["choices"][0]["message"]["content"].strip()
        print(f"💡 Slogan: {slogan}")
        return slogan

    @start()
    def generate_tagline(self):
        response = completion(
            model=self.model,
            messages=[{"role": "user", "content": "Generate a tagline for a futuristic brand."}]
        )
        tagline = response["choices"][0]["message"]["content"].strip()
        print(f"🔖 Tagline: {tagline}")
        return tagline

    @listen(and_(generate_slogan, generate_tagline))  # Runs only when both tasks complete
    def combine_outputs(self, outputs):
        slogan, tagline = outputs
        combined = f"🌟 Final Branding: Slogan - '{slogan}' | Tagline - '{tagline}'"
        print("✅ Aggregated Output:", combined)
        return combined

if __name__ == "__main__":
    flow = AndAggregationFlow()
    final_output = flow.kickoff()
    print("🎯 Final Output:", final_output)
```
📌 **What Happens?**  
✔️ Two tasks run at the same time.  
✔️ The aggregation function only runs when **both** tasks finish.  
✔️ This is useful when you need all results before proceeding.  

---

### **🎯 Summary**  
🚀 **`or_`** → Triggers when the first task finishes.  
🚀 **`and_`** → Triggers only when all tasks finish.  

🔥 **Use parallelization when tasks can run independently, improving speed and efficiency!** 🚀
