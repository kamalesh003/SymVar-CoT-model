# SymVar-CoT-model-
**UNIQUE SAMPLES:**
<img width="989" height="315" alt="Screenshot 2025-10-02 215915" src="https://github.com/user-attachments/assets/3ec71d3c-fd49-4fba-87d1-c3d71f601210" />

<img width="1679" height="342" alt="Screenshot 2025-10-02 220021" src="https://github.com/user-attachments/assets/f8dffc02-0f07-4bd4-8ea5-3c5a741e3120" />

# TOKEN COST PER QUERY COMPARISON

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



