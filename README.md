# 🧱 Atari Breakout (16-Bit x86 Assembly)

A console-based clone of the classic Atari Breakout game developed entirely in 16-bit x86 Assembly language. This project demonstrates low-level system architecture, bypassing standard OS calls to interact directly with hardware memory and I/O ports.

## 🚀 Technical Highlights & Features

Instead of relying on modern game engines, this game is built from the ground up using raw CPU instructions:

* **Direct Video Memory Access (DMA):** Renders the UI, boundaries, paddle, and ball by writing hexadecimal color attributes directly to the VGA text mode memory segment (`0xB800`).
* **Custom Hardware Interrupts (ISR):** Hijacks the standard keyboard interrupt (`INT 9`) to read from I/O port `0x60`. This allows for real-time, asynchronous paddle movement (Left/Right arrows) without pausing or blocking the main game loop.
* **Hardware-Level Audio:** Utilizes the PC Speaker I/O ports (`42h` and `61h`) to generate dynamic sound frequencies based on different collision events (paddle hits vs. brick breaks).
* **Complex Collision Physics:** Implements multi-tier brick degradation (Red -> Yellow -> Green) and calculates 6 distinct trajectory angles (45°, 90°, 135°, 225°, 270°, 315°) using raw mathematical wrapping.

## 🛠️ Tech Stack

* **Language:** x86 Assembly Language (NASM)
* **Architecture:** 16-bit Real Mode (`org 0x100` COM file execution)
* **Environment:** DOSBox Emulator

## 🎮 Game Rules & Mechanics

1.  **Objective:** Break all the bricks without letting the ball hit the bottom floor.
2.  **Controls:** Press and hold `<-` (Left Arrow) or `->` (Right Arrow) to move the paddle. Press `ESC` to quit.
3.  **Brick Mechanics:** Bricks have different health levels indicated by color. 
    * Red (4 hits) -> Orange (3 hits) -> Yellow (2 hits) -> Green (1 hit).
4.  **Scoring & Lives:** Players start with 3 lives. The score and remaining lives are dynamically updated in the top corners of the screen.

## ⚙️ How to Run Locally

1.  Install [DOSBox](https://www.dosbox.com/).
2.  Mount the project directory within the DOSBox terminal:
    ```assembly
    mount c c:\path\to\your\folder
    c:
    ```
3.  Compile the assembly code into an executable (using NASM):
    ```assembly
    nasm GameCode.asm -o game.com
    ```
4.  Run the game:
    ```assembly
    game.com
    ```

## 👥 Collaboration
This project was developed as a 2-person collaboration for the Computer Organization and Assembly Language (COAL) course. My specific focus was on managing the direct memory access for the graphics and writing the interrupt service routine for real-time keyboard inputs.
