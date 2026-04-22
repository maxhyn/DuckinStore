# Game Development Requirements Document: "Seaside Memory Cafe" v9.0

## 1. Project Background & Goals
[cite_start]The orange cat Seven and the old man Seon run an ice café by the sea, collecting "drifting bottle memories" that wash ashore with the waves. Players must serve the bottles with the correct food; satisfied bottles will leave behind memories and earn points. [cite: 4, 18, 23]

## 2. Visual Assets List
- **Characters**: 
    - [cite_start]Orange Cat Seven (`cat_walk_1.png`, `cat_walk_2.png`) [cite: 42]
    - [cite_start]Old Man Seon (`seon_back_1.png`, `seon_back_2.png`) [cite: 4, 11]
    - [cite_start]Duck (`duck.png`) [cite: 4, 22]
- **Customers (Memory Bottles)**: 
    - Three states: `bottle_happy.png`, `bottle_normal.png`, `bottle_angry.png`
- [cite_start]**Food**: `red_bean_ice.png`, `pineapple_bun.png`, `siu_mai.png`, `milk_tea.png` [cite: 17]
- **UI/Scene**:
    - [cite_start]Background: `background_v3.png` (**Table numbers 1-4 are already drawn directly on the image**, no code rendering required) [cite: 15]
    - Order base image: `order.png` (blank retro order slip)

## 3. Page Layout & Table Alignment Logic
- [cite_start]**Left Side**: Seon's cooking area and function bar. [cite: 11]
- [cite_start]**Bottom-Left Corner**: Serving trigger area (click to enter Order Check). [cite: 13]
- [cite_start]**Right-Side Table Area (strictly matching the background image layout)**: [cite: 15]
    - **Table 1 (Top-Left of Area)**: Top-left position on the background image.
    - **Table 2 (Top-Right of Area)**: Top-right position on the background image.
    - **Table 3 (Bottom-Left of Area)**: Bottom-left position on the background image.
    - **Table 4 (Bottom-Right of Area)**: Bottom-right position on the background image.
- [cite_start]**Developer Note**: The collision detection areas in the code must precisely overlap with the table positions drawn on the background image. [cite: 15, 38]

## 4. Core System Modules
### A. Drifting Bottle Refresh & Disappearance
- [cite_start]**Refresh**: After a bottle disappears (either successfully served or timed out), the table stays vacant for a few seconds, then randomly refreshes with a new bottle and order. [cite: 18, 23]
- **Disappearance Conditions**: 
    - [cite_start]Success: Correct food delivered within 100% of the waiting time. [cite: 21, 31]
    - [cite_start]Failure: Waiting time reaches 100% without food being delivered — the bottle disappears. [cite: 31]

### B. State System (Visual Feedback)
Waiting progress is conveyed entirely through bottle sprite swaps — no progress bars are used:
- 0-39%: `bottle_happy.png`
- 40-69%: `bottle_normal.png`
- 70-100%: `bottle_angry.png`

### C. Order Check System
[cite_start]Clicking the serving area triggers a pop-up of `order.png`: [cite: 7, 19]
- [cite_start]**Displayed Content**: Dynamically shows the "target table number," "food requirement," and "unit price" for the order on top of `order.png`. [cite: 7, 19]
- **Player Decisions**:
    - [cite_start]**Right**: Confirm as correct. **The cat enters serving mode with the food balanced on its head**. [cite: 7, 21, 35]
    - [cite_start]**Again**: An error is spotted. Seon remakes the dish, consuming additional time. [cite: 7, 20, 36]

### D. Duck Interference
- [cite_start]The Duck moves randomly around the table area; bumping into a bottle accelerates its transition to an "angry" state. [cite: 22, 23, 30]
- [cite_start]Players can click the Duck to knock it away. [cite: 22, 37]

## 5. Developer Instructions
1. [cite_start]**Static Position Alignment**: "The table numbers are already drawn on the background image. Adjust the coordinate variables in the code to ensure that bottle spawn positions and click detection areas align perfectly with the tables in the image." [cite: 15]
2. [cite_start]**Head-Carried Food Visual**: "The food icon must hover above the cat's head and move along with the cat." [cite: 35]
3. [cite_start]**Two-Frame Animation**: "Implement smooth sprite-swap animations for both the cat and the old man." [cite: 33]