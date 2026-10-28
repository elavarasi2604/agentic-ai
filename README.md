```python
def cot_reasoning():
    price = 10
    quantity = 5

    print("Problem: Find the cost of 5 pens at Rs. 10 each.")
    print("Step 1: Price of one pen =", price)
    print("Step 2: Number of pens =", quantity)

    total = price * quantity
    print("Step 3: Total cost =", price, "*", quantity)
    print("Final Answer: Rs.", total)

cot_reasoning()
```

```python
def pot_reasoning():
    marks = [80, 75, 90, 85, 70]

    total = sum(marks)
    average = total / len(marks)
    highest = max(marks)

    print("Marks:", marks)
    print("Total Marks:", total)
    print("Average Marks:", average)
    print("Highest Mark:", highest)

pot_reasoning()
```

```python
def reflexion_agent():
    question = "Calculate 6 * 4"
    expected = 6 * 4
    answer = 20

    print("Question:", question)

    for attempt in range(1, 4):
        print("Attempt", attempt, ":", answer)

        if answer == expected:
            print("Answer is correct!")
            break

        print("Reflection: The answer is incorrect.")
        print("Feedback: Recalculate 6 * 4.")
        answer = 6 * 4

    print("Final Answer:", answer)

reflexion_agent()
```

```python
def react_agent():
    print("REACT APPROACH")

    action = "Practice Python programs"
    observation = "Practice improves programming skills"

    print("Action:", action)
    print("Observation:", observation)


def tot_agent():
    print("\nTREE OF THOUGHTS APPROACH")

    plans = {
        "Read Notes": 6,
        "Watch Tutorials": 7,
        "Practice Programs": 10
    }

    for plan, score in plans.items():
        print(plan, "- Score:", score)

    best_plan = max(plans, key=plans.get)
    print("Best Plan:", best_plan)


react_agent()
tot_agent()
```

```python
def lats_agent():
    # Each path contains actions and its evaluated reward.
    search_tree = [
        {"path": ["Read Documentation"], "reward": 7},
        {"path": ["Test Code"], "reward": 9},
        {"path": ["Guess Solution"], "reward": 3},
        {"path": ["Read Documentation", "Test Code"],
         "reward": 10}
    ]

    print("Exploring Search Tree:")

    for node in search_tree:
        path = " -> ".join(node["path"])
        print(path, "| Reward:", node["reward"])

    best_node = max(search_tree, key=lambda x: x["reward"])

    print("\nBest Path:", " -> ".join(best_node["path"]))
    print("Best Reward:", best_node["reward"])


lats_agent()
```

```python
import re
from collections import Counter
from math import sqrt

documents = [
    "Python is a programming language.",
    "Artificial intelligence enables intelligent machines.",
    "Machine learning learns patterns from data."
]

def tokenize(text):
    return re.findall(r"\b\w+\b", text.lower())

def cosine_similarity(query, document):
    q = Counter(tokenize(query))
    d = Counter(tokenize(document))

    common = set(q) & set(d)
    dot = sum(q[word] * d[word] for word in common)

    q_norm = sqrt(sum(v * v for v in q.values()))
    d_norm = sqrt(sum(v * v for v in d.values()))

    if q_norm == 0 or d_norm == 0:
        return 0

    return dot / (q_norm * d_norm)

def rag_agent():
    query = input("Enter your question: ")

    scores = [
        cosine_similarity(query, doc)
        for doc in documents
    ]

    best_index = max(range(len(scores)), key=scores.__getitem__)

    if scores[best_index] == 0:
        print("No relevant document found.")
    else:
        retrieved = documents[best_index]
        print("Retrieved Context:", retrieved)
        print("Answer:", retrieved)

rag_agent()
```

```python
from collections import deque

def graphrag_agent():
    graph = {
        "AI": ["Machine Learning", "Robotics"],
        "Machine Learning": ["Data", "Prediction"],
        "Robotics": ["Sensors", "Automation"],
        "Data": [],
        "Prediction": [],
        "Sensors": [],
        "Automation": []
    }

    query = input("Enter topic: ").strip().lower()

    nodes = {node.lower(): node for node in graph}
    topic = nodes.get(query)

    if topic is None:
        print("Topic not found.")
        return

    visited = set()
    queue = deque([topic])

    print("Knowledge Graph Results:")

    while queue:
        current = queue.popleft()

        if current in visited:
            continue

        visited.add(current)
        print(current)

        for neighbor in graph[current]:
            if neighbor not in visited:
                queue.append(neighbor)

graphrag_agent()
```

```python
import json
import os

def memory_agent():
    filename = "memory.json"

    if os.path.exists(filename):
        with open(filename, "r") as file:
            memory = json.load(file)
    else:
        memory = []

    note = input("Enter information to remember: ").strip()

    if note:
        memory.append(note)

        with open(filename, "w") as file:
            json.dump(memory, file, indent=4)

    print("\nStored Memory:")

    for item in memory:
        print("-", item)

memory_agent()
```

```python
def experience_replay():
    memory = []

    # State, action, next state, reward
    memory.append(("Start", "Move Right", "Middle", 5))
    memory.append(("Middle", "Jump", "End", 10))
    memory.append(("End", "Stop", "End", 2))

    print("Episodic Memory:")

    for state, action, next_state, reward in memory:
        print(
            "State:", state,
            "| Action:", action,
            "| Next State:", next_state,
            "| Reward:", reward
        )

    print("\nExperience Replay:")

    for experience in memory:
        print(experience)

    best = max(memory, key=lambda item: item[3])

    print("\nBest Experience:", best)

experience_replay()
```

```python
def evaluate_agent():
    tasks = [
        {"name": "Math Task", "expected": 4, "actual": 4},
        {"name": "Code Task", "expected": 10, "actual": 10},
        {"name": "Logic Task", "expected": 5, "actual": 3}
    ]

    passed = 0

    print("AI Agent Evaluation\n")

    for task in tasks:
        if task["expected"] == task["actual"]:
            print(task["name"], ": PASS")
            passed += 1
        else:
            print(task["name"], ": FAIL")

    total = len(tasks)
    success_rate = (passed / total) * 100

    print("\nTasks Passed:", passed, "/", total)
    print("Success Rate:", round(success_rate, 2), "%")

evaluate_agent()
```

```python
import json
import os

MEMORY_FILE = "agent_memory.json"


def load_memory():
    if os.path.exists(MEMORY_FILE):
        with open(MEMORY_FILE, "r") as file:
            return json.load(file)
    return []


def save_memory(memory):
    with open(MEMORY_FILE, "w") as file:
        json.dump(memory, file, indent=4)


def reasoning(query):
    query = query.lower()

    if "exam" in query:
        return "Prepare for the examination"
    elif "project" in query:
        return "Complete the project"
    elif "python" in query:
        return "Improve Python programming skills"
    else:
        return "Complete the requested task"


def planning(goal):
    plans = {
        "Prepare for the examination": [
            "Identify important topics",
            "Prepare study notes",
            "Practice questions"
        ],
        "Complete the project": [
            "Identify requirements",
            "Develop the application",
            "Test the application"
        ],
        "Improve Python programming skills": [
            "Revise Python basics",
            "Practice programs",
            "Solve coding problems"
        ],
        "Complete the requested task": [
            "Understand the task",
            "Perform the task",
            "Verify the result"
        ]
    }
    return plans[goal]


def agent():
    memory = load_memory()

    query = input("Enter your task: ")

    goal = reasoning(query)
    plan = planning(goal)

    print("\nReasoning:", goal)

    print("\nExecution Plan:")
    for step in plan:
        print("-", step)

    print("\nMemory:")
    previous = [
        item for item in memory
        if item["goal"] == goal
    ]

    if previous:
        print("Previous related task found.")
    else:
        print("No previous related task found.")

    result = "Task plan generated successfully."

    memory.append({
        "query": query,
        "goal": goal,
        "plan": plan,
        "result": result
    })

    save_memory(memory)

    print("\nFinal Result:", result)
    print("Memory saved successfully.")


agent()
```
