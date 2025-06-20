# Time Table Scheduler with Genetic Algorithm 📅🧬

An automated timetable generator that uses a Genetic Algorithm to assign courses, professors, time slots, and rooms efficiently, minimizing scheduling conflicts and satisfying institutional constraints.

---

## 🔍 Overview

This project simulates a timetable scheduler using genetic algorithms. It encodes course-section assignments as binary genes and evolves solutions through selection, crossover, mutation, and fitness evaluation. The final timetable is decoded and saved as an Excel file.

---

## 🧱 Gene Structure & Encoding

Each **course section** is encoded as a 24-bit binary gene:

- **Gene Breakdown (24 bits total):**
  - 3 bits → First Lecture Day
  - 3 bits → First Lecture Time Slot
  - 6 bits → First Lecture Room
  - 3 bits → Second Lecture Day
  - 3 bits → Second Lecture Time Slot
  - 6 bits → Second Lecture Room

- **Static Course Details** (stored separately):
  - Course Name, Section, Theory/Lab, Section Strength, Assigned Professor

Each chromosome represents a full schedule:
- Chromosome length = `number_of_sections * 24`
- E.g., 46 sections × 24 bits = **1104-bit chromosome**

---

## ⚙️ Preprocessing

- **Inputs:**
  - Hardcoded arrays for: Courses, Sections, Professors, Days, Time Slots, Rooms
  - Randomized: Section strengths (30–120), Professor assignments (≤3 per professor)
  - Room info as tuples: `(room_name, room_capacity)`
  - Course type (Theory/Lab) stored explicitly and by index positioning

---

## 🧬 Genetic Algorithm Steps

1. **Initial Population**
   - 1000 randomly generated chromosomes (configurable)

2. **Fitness Function**
   - Evaluates each chromosome based on:
     - **Hard constraints**: -1 penalty
     - **Soft constraints**: -0.5 penalty
   - Constraints are documented in code

3. **Tournament Selection**
   - Selects best individuals through pairwise competition
   - Builds a new mating pool of size = population size

4. **Crossover (Two-Point)**
   - Swaps segments of genes between parents to create new children

5. **Mutation (Single-Point)**
   - Randomly flips 1 bit in each child’s gene

6. **Gene Correction**
   - Ensures that mutated/crossover genes stay within valid index ranges

---

## 📤 Output

- The first individual with **fitness score = 0** (no conflicts) is decoded
- Decoded schedule is written to an Excel file
- Excel includes Course, Section, Professor, Day, Time Slot, Room

---

## 🛠️ Tech Stack

- Python
- OpenPyXL (for Excel output)
- Random, NumPy (for operations)
- Binary-based genetic encoding

---

## 🚀 How to Run

1. Clone the repo and enter the directory:
   ```bash
   git clone https://github.com/your-username/timetable-scheduler.git
   cd timetable-scheduler
