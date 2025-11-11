# Exno.7-Develop a prompt-based application tailored to their personal needs, fostering creativity and practical problem-solving skills while leveraging the capabilities of large language models.

# Date: 11/11/2025
# Register no: 212223040111
# Aim:
To develop a prompt-based application using ChatGPT - To demonstrate how to create a prompt-based application to organize daily tasks, showing the progression from simple to more advanced prompt designs and their corresponding outputs.

# AI Tools Required: 
- ChatGPT (Large Language Model by OpenAI)

- Python or Web Interface for simulating command-line interaction

Internet Browser (to access ChatGPT platform)

# Explanation: 
Prompt:
"Design a personal productivity assistant that can help manage daily tasks, schedule reminders, suggest wellness tips, and answer general queries. The assistant should interact using natural language and be adaptable to the user’s changing preferences over time."

# Procedure:
1. Define the core requirements of a personal productivity assistant.
2. Identify and construct appropriate prompts for each task using an LLM (e.g., ChatGPT).
3. Simulate natural user interaction through a simple interface or command-line system.
4. Collect feedback or inputs from users and adapt responses accordingly.
5. Integrate basic memory to simulate preference adaptation.
EXPECTED OUTPUT: - 
Output (Example Response by LLM):
Personal Productivity Assistant Features:
1. Daily Task Manager:
o Accept tasks via natural language (e.g., "Remind me to call mom at 6 PM").
o Organize tasks by priority and deadline.
o Provide daily summaries and pending items.
2. Smart Scheduler:
o Schedule events and set reminders using contextual understanding.
o Notify user of overlapping appointments or free time slots.
3. Wellness Tips Generator:
o Suggest daily wellness advice (hydration, exercise, screen-time breaks).
o Adapt suggestions based on past user preferences and responses.

# Python Code (Command-Line Version):
```py
from openai import OpenAI

client = OpenAI(api_key="YOUR_API_KEY_HERE")

base_prompt = """
You are a Personal Productivity Assistant.
You can:
- Manage daily tasks
- Schedule reminders
- Suggest wellness tips
- Answer general questions
- Adapt to user preferences based on interaction history
Always respond in a natural, helpful, and friendly tone.
"""

print("🤖 Personal Productivity Assistant Started")
print("Type 'exit' to stop.\n")

user_memory = {}

while True:
    user_input = input("You: ")

    if user_input.lower() == "exit":
        print("Assistant: Goodbye! Stay productive! 💪")
        break

    prompt = base_prompt + "\nUser Preferences: " + str(user_memory) + "\nUser says: " + user_input

    response = client.chat.completions.create(
        model="gpt-4o-mini",  # Use GPT-4o-mini for lightweight testing
        messages=[{"role": "user", "content": prompt}]
    )

    reply = response.choices[0].message.content
    print("Assistant:", reply)

    if "I prefer" in user_input or "I like" in user_input:
        user_memory["last_preference"] = user_input
```
# Expected Output:
User: Add a task to submit my report by 5 PM.

Assistant: Task added! Reminder set for 4:45 PM. Would you like me to check your progress before that?

User: Suggest a quick wellness break.

Assistant: Try a 2-minute neck stretch and drink a glass of water. You’ve been active for 90 minutes straight.

# Output
<img width="662" height="196" alt="image" src="https://github.com/user-attachments/assets/cd63cf9a-92b3-478e-bac9-d554de207ef1" />

# Result: 
The lab exercise resulted in the creation of a prototype concept for a personal assistant powered by large language models.
