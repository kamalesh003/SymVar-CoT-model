# SymVar-CoT-model

**UNIQUE SAMPLES:**
<img width="989" height="315" alt="Screenshot 2025-10-02 215915" src="https://github.com/user-attachments/assets/3ec71d3c-fd49-4fba-87d1-c3d71f601210" />

**AVG TOKEN COST:**
<img width="1679" height="342" alt="Screenshot 2025-10-02 220021" src="https://github.com/user-attachments/assets/f8dffc02-0f07-4bd4-8ea5-3c5a741e3120" />

**TOKEN COST PER QUERY COMPARISON:**

<img width="1489" height="690" alt="image" src="https://github.com/user-attachments/assets/44eb42b6-cbb8-4022-892b-2de95a68fd4b" />


# REUSABILITY RESULT:

```bash

--- Reusability Analysis ---

Comparison between Example 1 and Example 2:
Query 1: An object moves 440 meters in 10 seconds. What is its velocity?
Query 2: An object moves 88 meters in 2 seconds. What is its velocity?
Reusable symbolic patterns detected:
  - Velocity(ENTITY,NUM)
  - Velocity(ENTITY,NUM/NUM)

Comparison between Example 1 and Example 3:
Query 1: An object moves 440 meters in 10 seconds. What is its velocity?
Query 2: The temperature drops 5°C every hour. How much will it drop in 4 hours?
No reusable patterns detected.

Comparison between Example 1 and Example 4:
Query 1: An object moves 440 meters in 10 seconds. What is its velocity?
Query 2: A freezer decreases temperature by 3°C per hour. What is the total drop after 6 hours?
No reusable patterns detected.

Comparison between Example 2 and Example 3:
Query 1: An object moves 88 meters in 2 seconds. What is its velocity?
Query 2: The temperature drops 5°C every hour. How much will it drop in 4 hours?
No reusable patterns detected.

Comparison between Example 2 and Example 4:
Query 1: An object moves 88 meters in 2 seconds. What is its velocity?
Query 2: A freezer decreases temperature by 3°C per hour. What is the total drop after 6 hours?
No reusable patterns detected.

Comparison between Example 3 and Example 4:
Query 1: The temperature drops 5°C every hour. How much will it drop in 4 hours?
Query 2: A freezer decreases temperature by 3°C per hour. What is the total drop after 6 hours?
Reusable symbolic patterns detected:
  - DropPerHour(NUM) ∧ Time(NUM)
  - TemperatureDrop(NUM*NUM)
  - NUM

--- Abstracted CoTs ---

Example 1: An object moves 440 meters in 10 seconds. What is its velocity?
Abstracted Steps:
  - Velocity(ENTITY,NUM/NUM)
  - Velocity(ENTITY,NUM)

Example 2: An object moves 88 meters in 2 seconds. What is its velocity?
Abstracted Steps:
  - Velocity(ENTITY,NUM/NUM)
  - Velocity(ENTITY,NUM)

Example 3: The temperature drops 5°C every hour. How much will it drop in 4 hours?
Abstracted Steps:
  - DropPerHour(NUM) ∧ Time(NUM)
  - TemperatureDrop(NUM*NUM)
  - NUM

Example 4: A freezer decreases temperature by 3°C per hour. What is the total drop after 6 hours?
Abstracted Steps:
  - DropPerHour(NUM) ∧ Time(NUM)
  - TemperatureDrop(NUM*NUM)
  - NUM
```


# Accessing the Fine-Tuned Model:

```bash
from openai import OpenAI

client = OpenAI()

response = client.chat.completions.create(
    model="ft:gpt-4o-mini-2024-07-18:personal::CJzhVsz3",
    messages=[{"role": "user", "content": "If all exoplanets in a system orbit their star elliptically, some have atmospheres with hydrogen, and no hydrogen-rich planet is closer than 0.5 AU, can a planet at 0.3 AU have hydrogen?"}]
)

print(response.choices[0].message.content)
```


```bash
Based on the premises given, we can analyze the conditions for a planet to have hydrogen in its atmosphere.

1. **Exoplanet(x) → OrbitsElliptically(x) → HasAtmosphereWithHydrogen(x) → α**: If a planet is an exoplanet and orbits elliptically, and if it has hydrogen-rich atmosphere, then it satisfies α.

2. **CloserThan( x, 0.5) → HasAtmosphereWithHydrogen(x)**: If a planet is closer than 0.5 AU to its star, then: it does not have a hydrogen-rich atmosphere.

From the second premise, we conclude that no hydrogen-rich planet can be closer than 0.5 AU to its star. Therefore, if a planet is at 0.3 AU, it cannot have a hydrogen-rich atmosphere.

Answer: No

```


# Standard CoT vs SymVar CoT - (Failure of Standard CoT):

```bash
Complex Query: If all zargs are either blims or clops, and some clops are not zargs, and no blims are drogs, but every drog is a zarg, can a drog be a clop?

Generating SymVar-CoT...
SymVar-CoT Output:
To determine if a drog can be a clop, we can analyze the given statements step by step.

1. **All zargs are either blims or clops**: This means that for any entity \( x \), if \( x \) is a zarg, then \( x \) is a blim or \( x \) is a clop. 
   - \( Zarg(x) \rightarrow Blim(x) \lor Clop(x) \)

2. **Some clops are not zargs**: This means there exists at least one entity \( y \) such that \( y \) is a clop and \( y \) is not a zarg.
   - \( Clop(y) \land \neg Zarg(y) \)

3. **No blims are drogs**: This means that if \( x \) is a blim, then \( x \) is not a drog.
   - \( Blim(x) \rightarrow \neg Drog(x) \)

4. **Every drog is a zarg**: This means that if \( x \) is a drog, then \( x \) is a zarg.
   - \( Drog(x) \rightarrow Zarg(x) \)
------------------------------

Generating Standard CoT using gpt-4o-mini...
Standard CoT Output:
To solve this problem, let's break down the information given step-by-step:

1. **All zargs are either blims or clops.**
   - This means that if something is a zarg, it must be either a blim or a clop.

2. **Some clops are not zargs.**
   - This indicates that there are clops that do not fall into the category of zargs.

3. **No blims are drogs.**
   - This tells us that if something is a blim, it cannot be a drog.

4. **Every drog is a zarg.**
   - This means that if something is a drog, it must also be a zarg.

Now, we need to determine if a drog can be a clop.

From point 4, since every drog is a zarg, we can conclude that all drogs must be either blims or clops (from point 1). However, from point 3, we know that no blims are drogs. Therefore, the only possibility left is that drogs must be clops.

However, we also have point 2, which states that some clops are not zargs. This means that not all clops are zargs, and since all drogs must be zargs, it follows that drogs cannot be among those clops that are not zargs.

Thus, we conclude that a drog cannot be a clop because if it were, it would contradict the statement that some clops are not zargs.

In summary, based on the logical deductions from the premises provided, a drog cannot be a clop.
------------------------------

Comparison:
Review the outputs above to compare the structure and reasoning process.

SymVar-CoT Answer: To determine if a drog can be a clop, we can analyze the given statements step by step.

1. **All zargs are either blims or clops**: This means that for any entity \( x \), if \( x \) is a zarg, then \( x \) is a blim or \( x \) is a clop. 
   - \( Zarg(x) \rightarrow Blim(x) \lor Clop(x) \)

2. **Some clops are not zargs**: This means there exists at least one entity \( y \) such that \( y \) is a clop and \( y \) is not a zarg.
   - \( Clop(y) \land \neg Zarg(y) \)

3. **No blims are drogs**: This means that if \( x \) is a blim, then \( x \) is not a drog.
   - \( Blim(x) \rightarrow \neg Drog(x) \)

4. **Every drog is a zarg**: This means that if \( x \) is a drog, then \( x \) is a zarg.
   - \( Drog(x) \rightarrow Zarg(x) \)
SymVar-CoT Compressed: 

**Standard CoT Answer: Could not extract answer.**
```

