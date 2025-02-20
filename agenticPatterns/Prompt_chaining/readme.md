

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





