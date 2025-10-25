# Exno.7-Develop a prompt-based application tailored to their personal needs, fostering creativity and practical problem-solving skills while leveraging the capabilities of large language models.

# Date: 25-10-2025
# Register no: 212223040111
# Aim: To develop a prompt-based application using ChatGPT - To demonstrate how to create a prompt-based application to organize daily tasks, showing the progression from simple to more advanced prompt designs and their corresponding outputs.

#AI Tools Required: 


# Explanation: 
Prompt:
"Design a personal productivity assistant that can help manage daily tasks, schedule reminders, suggest wellness tips, and answer general queries. The assistant should interact using natural language and be adaptable to the user’s changing preferences over time."
Procedure:
1. Define the core requirements of a personal productivity assistant.
2. Identify and construct appropriate prompts for each task using an LLM (e.g., ChatGPT).
3. Simulate natural user interaction through a simple interface or command-line system.
4. Collect feedback or inputs from users and adapt responses accordingly.
5. (Optional) Integrate basic memory to simulate preference adaptation.
EXPECTED OUTPUT: - (attached the drive link)
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

# Code:
```js
import { useState } from "react";
import { Button } from "@/components/ui/button";
import { Input } from "@/components/ui/input";
import { TaskCard } from "@/components/TaskCard";
import { ChatMessage } from "@/components/ChatMessage";
import { WellnessTip } from "@/components/WellnessTip";
import { ScheduleCard } from "@/components/ScheduleCard";
import { Send, CheckCircle2, Calendar, Sparkles } from "lucide-react";
import { Card } from "@/components/ui/card";
import { Tabs, TabsContent, TabsList, TabsTrigger } from "@/components/ui/tabs";

const Index = () => {
  const [input, setInput] = useState("");
  const [messages, setMessages] = useState<Array<{ text: string; isUser: boolean }>>([
    {
      text: "Hey 👋! I'm Ticko, your productivity buddy.\nWant me to start with tasks, your schedule, or a quick wellness tip today?",
      isUser: false,
    },
  ]);

  const [tasks, setTasks] = useState([
    {
      id: "1",
      text: "Call mom",
      time: "6:00 PM",
      completed: false,
      priority: "high" as const,
    },
    {
      id: "2",
      text: "Study session",
      time: "4:00 PM",
      completed: false,
      priority: "medium" as const,
    },
  ]);

  const [schedule] = useState([
    { id: "1", title: "Morning Study Block", time: "8:00 AM", duration: "2 hours" },
    { id: "2", title: "Lunch Break", time: "12:00 PM", duration: "1 hour" },
    { id: "3", title: "Afternoon Session", time: "4:00 PM", duration: "2 hours" },
  ]);

  const wellnessTips = [
    "🌿 Take a 10-min walk and sip some water. A short stretch will boost your focus!",
    "💧 Remember to hydrate! Grab a glass of water right now.",
    "🧘‍♀️ Try a 5-minute breathing exercise to reset your energy.",
  ];

  const handleToggleTask = (id: string) => {
    setTasks(tasks.map((task) => (task.id === id ? { ...task, completed: !task.completed } : task)));
  };

  const handleSendMessage = () => {
    if (!input.trim()) return;

    const userMessage = input;
    setMessages([...messages, { text: userMessage, isUser: true }]);
    setInput("");

    setTimeout(() => {
      let response = "";
      const lowerInput = userMessage.toLowerCase();

      if (lowerInput.includes("tired") || lowerInput.includes("stressed")) {
        response = wellnessTips[Math.floor(Math.random() * wellnessTips.length)];
      } else if (lowerInput.includes("list") || lowerInput.includes("tasks")) {
        response = "Here's what's on your plate 📝\n\n" + 
          tasks.map((task, i) => `${i + 1}️⃣ ${task.text} – ${task.time || "No time set"}`).join("\n") +
          "\n\nYou're doing great! ✨";
      } else if (lowerInput.includes("add") || lowerInput.includes("remind")) {
        response = "Got it! ✅ I've noted that down. I'll remind you when it's time!";
      } else {
        response = "I'm here to help! Try asking me to:\n• List your tasks\n• Add a reminder\n• Schedule a study session\n• Get a wellness tip 💪";
      }

      setMessages((prev) => [...prev, { text: response, isUser: false }]);
    }, 600);
  };

  return (
    <div className="min-h-screen p-4 md:p-8">
      <div className="max-w-6xl mx-auto">
        {/* Header */}
        <div className="text-center mb-8">
          <div className="inline-flex items-center gap-2 px-4 py-2 rounded-full gradient-primary text-primary-foreground mb-4 shadow-soft">
            <Sparkles className="w-5 h-5" />
            <span className="font-semibold">Ticko</span>
          </div>
          <h1 className="text-4xl md:text-5xl font-bold mb-2 bg-clip-text text-transparent gradient-primary" style={{ backgroundClip: 'text', WebkitBackgroundClip: 'text', backgroundImage: 'var(--gradient-primary)' }}>
            Your AI Productivity Buddy
          </h1>
          <p className="text-muted-foreground">Stay organized, balanced, and motivated 🚀</p>
        </div>

        <div className="grid md:grid-cols-3 gap-6">
          {/* Main Chat Area */}
          <div className="md:col-span-2">
            <Card className="p-6 shadow-card">
              <div className="h-[400px] overflow-y-auto mb-4 pr-2 space-y-2">
                {messages.map((msg, idx) => (
                  <ChatMessage key={idx} message={msg.text} isUser={msg.isUser} />
                ))}
              </div>

              <div className="flex gap-2">
                <Input
                  value={input}
                  onChange={(e) => setInput(e.target.value)}
                  onKeyPress={(e) => e.key === "Enter" && handleSendMessage()}
                  placeholder="Type your message..."
                  className="flex-1 rounded-xl"
                />
                <Button
                  onClick={handleSendMessage}
                  className="rounded-xl gradient-primary shadow-soft hover:opacity-90"
                >
                  <Send className="w-4 h-4" />
                </Button>
              </div>
            </Card>
          </div>

          {/* Sidebar */}
          <div className="space-y-6">
            <Tabs defaultValue="tasks" className="w-full">
              <TabsList className="grid w-full grid-cols-2 mb-4">
                <TabsTrigger value="tasks" className="gap-2">
                  <CheckCircle2 className="w-4 h-4" />
                  Tasks
                </TabsTrigger>
                <TabsTrigger value="schedule" className="gap-2">
                  <Calendar className="w-4 h-4" />
                  Schedule
                </TabsTrigger>
              </TabsList>

              <TabsContent value="tasks" className="space-y-3">
                <Card className="p-4 shadow-card">
                  <h2 className="font-semibold mb-3 flex items-center gap-2">
                    <CheckCircle2 className="w-5 h-5 text-primary" />
                    Today's Tasks
                  </h2>
                  <div className="space-y-2">
                    {tasks.map((task) => (
                      <TaskCard key={task.id} task={task} onToggle={handleToggleTask} />
                    ))}
                  </div>
                </Card>
              </TabsContent>

              <TabsContent value="schedule" className="space-y-3">
                <Card className="p-4 shadow-card">
                  <h2 className="font-semibold mb-3 flex items-center gap-2">
                    <Calendar className="w-5 h-5 text-primary" />
                    Today's Schedule
                  </h2>
                  <div className="space-y-2">
                    {schedule.map((event) => (
                      <ScheduleCard key={event.id} event={event} />
                    ))}
                  </div>
                </Card>
              </TabsContent>
            </Tabs>

            <WellnessTip tip="💧 Remember to stay hydrated! Take a water break." />
          </div>
        </div>
      </div>
    </div>
  );
};

export default Index;
```

# Output:
<img width="1324" height="849" alt="image" src="https://github.com/user-attachments/assets/0a3fee49-e442-4d93-88cb-767b2f6611ca" />


# Result: 
The lab exercise resulted in the creation of a prototype concept for a personal assistant powered by large language models. Students were able to:
 Understand how to tailor LLM prompts to real-life applications.
 Foster creativity by designing features suited to their personal or academic lives.
 Learn prompt engineering techniques for optimal interaction with AI tools.
 Experience the versatility and utility of generative AI in solving everyday problems.
