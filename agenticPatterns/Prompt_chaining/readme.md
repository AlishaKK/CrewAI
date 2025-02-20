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

It’s like **following a step-by-step recipe** instead of making everything at once! 🍽️🚀

Here's the updated code with an additional function, `generate_intro`, that generates an introduction for the blog post based on the generated outline.

Now, the flow includes an additional step where it generates an introduction for the blog post based on the outline. Let me know if you need further refinements! 🚀

from crewai.flow.flow import Flow, start, listen
from litellm import completion  # Replace with your preferred LLM API client

class TopicOutlineFlow(Flow):
    model = "gpt-4o-mini"

    @start()
    def generate_topic(self):
        # Prompt the LLM to generate a blog topic.
        response = completion(
            model=self.model,
            messages=[{
                "role": "user",
                "content": "Generate a creative blog topic for 2025."
            }]
        )
        topic = response["choices"][0]["message"]["content"].strip()
        print(f"Generated Topic: {topic}")
        return topic

    @listen(generate_topic)
    def generate_outline(self, topic):
        # Now chain the output by using the topic in a follow-up prompt.
        response = completion(
            model=self.model,
            messages=[{
                "role": "user",
                "content": f"Based on the topic '{topic}', create a detailed outline for a blog post."
            }]
        )
        outline = response["choices"][0]["message"]["content"].strip()
        print("Generated Outline:")
        print(outline)
        return outline

if __name__ == "__main__":
    flow = TopicOutlineFlow()
    final_outline = flow.kickoff()
    print("Final Output:")
    print(final_outline)


