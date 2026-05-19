// Bind input STRICTLY to the game box to prevent accidental UI clicks
gameBox.addEventListener('mousedown', handleInput);

gameBox.addEventListener('touchstart', (e) => {
    e.preventDefault(); // Prevent double-firing with simulated mouse events
    handleInput();
}, { passive: false });
Here is a professional, portfolio-ready `README.md` file tailored exactly to the code you provided. It highlights the technical decisions—like decoupling the timer from the render loop and using Vanilla JS—that will stand out to hiring managers.

***
```markdown
# NEURO_RESPONSE: 3D Precision Reaction Timer

![HTML5](https://img.shields.io/badge/HTML5-E34F26?style=for-the-badge&logo=html5&logoColor=white)
![CSS3](https://img.shields.io/badge/CSS3-1572B6?style=for-the-badge&logo=css3&logoColor=white)
![JavaScript](https://img.shields.io/badge/JavaScript-F7DF1E?style=for-the-badge&logo=javascript&logoColor=black)
![Three.js](https://img.shields.io/badge/Three.js-000000?style=for-the-badge&logo=threedotjs&logoColor=white)

**Neuro_Response** is a high-performance, single-page web application designed to measure human reaction time with sub-millisecond precision. Built entirely with Vanilla JavaScript and Three.js, this project serves as a technical showpiece demonstrating low-latency event handling, strict state management, and optimized 3D render loops without reliance on heavy front-end frameworks.

[**Live Demo 🚀**](#) *(Insert your GitHub Pages/Vercel link here)*

---

## 🎯 Strategic Goals & Architecture

While a reaction timer is conceptually simple, executing it with absolute precision requires careful architectural planning. This project focuses on three core engineering pillars:

### 1. Sub-Millisecond Precision (`performance.now()`)
Standard JavaScript `Date.now()` objects are subject to system clock drift and lack the resolution needed for cognitive testing. This application utilizes the `performance.now()` API to capture the hardware interrupt (the click/tap event) with microsecond accuracy. 

Crucially, **the timing logic is strictly decoupled from the Three.js render loop**. This ensures that minor frame drops or render lag do not artificially inflate the user's reaction time.

### 2. Strict State Machine (Anti-Cheat Logic)
To prevent erratic behavior or "cheating" (spam-clicking before the signal), the application flow is controlled by a rigid State Machine:
*   `IDLE`: Awaiting user initiation.
*   `WAITING`: A cryptographically secure random delay (2–7 seconds).
*   `ACTIVE`: The high-res timer begins.
*   `PENALTY`: Triggered if an input is detected during the `WAITING` state, instantly halting the timer and applying visual feedback (camera shake).
*   `RESULT`: Calculates the delta and categorizes the user's cognitive speed.

### 3. Framework-Less 3D Rendering
By utilizing **Vanilla JavaScript** paired with **Three.js**, the application maintains a minimal footprint. The 3D scene features a custom compound geometry (an Icosahedron encapsulating an Octahedron) that visually communicates the current state of the machine via dynamic material swapping and procedural animations (breathing, counter-rotation, and trauma-shake on faults).

---

## ✨ Features

*   **Cyber-Minimalist UI:** A distraction-free, glassmorphic dark mode interface using CSS variables and the `JetBrains Mono` typeface.
*   **Dynamic Visual Feedback:** 3D primitives react in real-time to the state machine (Neutral Wireframe ➔ Pulsing Red ➔ Solid Emerald ➔ Hot Pink Fault).
*   **Session Tracking:** In-memory tracking of the user's "Best Time" during the current session.
*   **Algorithmic Ranking:** Automatically categorizes reaction times into tiers (Amazing, Very Good, Good, Average, Below Average).
*   **Fully Responsive:** Input handling gracefully switches between mouse events (`mousedown`) on desktop and touch events (`touchstart`) on mobile to eliminate the standard 300ms mobile click delay.

---

## 💻 Installation & Usage

Because this project is built with pure Vanilla JS and a CDN link for Three.js, there is no build step or node module installation required.

1.  **Clone the repository:**
    ```bash
    git clone https://github.com/YourUsername/neuro-response.git
    ```
2.  **Navigate to the directory:**
    ```bash
    cd neuro-response
    ```
3.  **Run the application:**
    Simply open the `index.html` file in any modern web browser.
    *Alternatively, serve it using an extension like VS Code Live Server.*

---

## 🧠 Code Highlight: Event Handling

To guarantee the most "honest" measurement of reaction time, the event listener is attached to the raw `mousedown` and `touchstart` events, intentionally bypassing higher-level `click` events which carry inherent browser delay.

```javascript
// Bind input STRICTLY to the game box to prevent accidental UI clicks
gameBox.addEventListener('mousedown', handleInput);

gameBox.addEventListener('touchstart', (e) => {
    e.preventDefault(); // Prevent double-firing with simulated mouse events
    handleInput();
}, { passive: false });