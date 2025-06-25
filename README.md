# 🧠 Mind Reader 

> A fun frontend project that creates the illusion of mind-reading using simple web technologies.

## 📖 Description

This is an interactive web-based application that simulates a playful *mind-reading experience* using pure HTML, CSS, and JavaScript. The user is asked to think of a number and enter it into the interface. Once they click the **"Read My Mind"** button, the system begins a humorous and dramatic loading sequence.

The progress bar updates with quirky messages, and after a short delay, the exact number the user entered is revealed with a **typing animation**, **sound effect**, and a **visual animation** (such as falling money). While no real magic is involved, the carefully timed interaction gives the illusion of mental telepathy.

---

## ✨ Features

- 📊 Dynamic loading bar with staged mind-reading messages  
- ⌨️ Typing effect text reveal  
- 🔊 Audio cue to enhance the reveal  
- 💸 Animated GIF (money fall) triggered at the end  
- 🎨 Custom background and visual styling  
- ✅ Fully responsive and lightweight (no frameworks used)

---

## Program
### index.html
```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <title>Mind Reader</title>
  <style>
    body {
      background: url('mind-reader-bg.png') no-repeat center center fixed;
      background-size: cover;
      color: #fff;
      font-family: 'Segoe UI', sans-serif;
      display: flex;
      flex-direction: column;
      align-items: center;
      justify-content: center;
      height: 100vh;
      margin: 0;
      overflow: hidden;
    }

    h1 {
      font-size: 4rem;
      text-align: center;
      margin-bottom: 30px;
      text-shadow: 2px 2px 5px rgba(0, 0, 0, 0.7);
    }

    input {
      padding: 20px;
      font-size: 1.2rem;
      width: 200px;
      border: none;
      border-radius: 10px;
      margin-bottom: 15px;
      text-align: center;
    }

    button {
      padding: 20px 30px;
      font-size: 1rem;
      background-color: #e91e63;
      color: white;
      border: none;
      border-radius: 10px;
      cursor: pointer;
      transition: background-color 0.3s ease;
    }

    button:hover {
      background-color: #c2185b;
    }

    .loading-message {
      font-size: 2rem;
      margin-top: 20px;
      min-height: 30px;
      text-align: center;
    }

    .progress-container {
      width: 400px;
      height: 40px;
      background-color: rgba(255, 255, 255, 0.2);
      border: 3px solid #fff;
      border-radius: 8px;
      overflow: hidden;
      margin-top: 15px;
      display: none;
    }

    .progress-bar {
      height: 100%;
      width: 0%;
      background-image: repeating-linear-gradient(
        to right,
        #05fb2e,
        #05fb2e 20px,
        #000 20px,
        #000 25px
      );
      transition: width 0.3s ease;
    }

    .reveal {
      margin-top: 30px;
      font-size: 2rem;
      font-weight: bold;
      color: #e0992e;
      min-height: 2.5rem;
      white-space: pre-wrap;
      text-align: center;
      text-shadow: 2px 2px 4px #000;
    }

    /* 💸 Money Fall GIF */
    #moneyEffect {
      position: absolute;
      top: 50%;
      left: 50%;
      transform: translate(-50%, -50%);
      width: 100vw;
      height: 100vh;
      object-fit: cover;
      z-index: 999;
      display: none;
      pointer-events: none;
    }
  </style>
</head>
<body>

  <h1>Pick any number you want, I will read your mind</h1>

  <input type="number" id="numberInput" placeholder="Enter your number" />
  <button onclick="readMind()">Read My Mind</button>

  <div class="loading-message" id="loadingMsg"></div>
  <div class="progress-container" id="progressContainer">
    <div class="progress-bar" id="progressBar"></div>
  </div>

  <div class="reveal" id="revealText"></div>

  <!-- 💸 Falling Money GIF -->
  <img src="money-fall.gif" alt="Money Fall" id="moneyEffect" />

  <!-- 🔊 Ding Sound -->
  <audio id="dingSound" src="https://www.soundjay.com/button/sounds/button-3.mp3" preload="auto"></audio>

  <script>
    function readMind() {
      const number = document.getElementById('numberInput').value.trim();
      const progressBar = document.getElementById('progressBar');
      const progressContainer = document.getElementById('progressContainer');
      const loadingMsg = document.getElementById('loadingMsg');
      const reveal = document.getElementById('revealText');
      const sound = document.getElementById('dingSound');
      const money = document.getElementById('moneyEffect');

      if (!number) {
        reveal.textContent = "Please enter a number!";
        return;
      }

      // Reset
      reveal.textContent = "";
      progressBar.style.width = "0%";
      progressContainer.style.display = "block";
      loadingMsg.textContent = "Starting...";
      money.style.display = "none";

      let progress = 0;

      const messages = [
        { percent: 25, text: "Reading your mind..." },
        { percent: 50, text: "Analysing brain pattern..." },
        { percent: 60, text: "Connecting your brain via Bluetooth..." },
        { percent: 80, text: "Calculating 6.37E+893127845151387513 POSSIBLE COMBINATIONS..." },
        { percent: 99, text: "Almost there... hang tight 🧠⚡" }
      ];

      const interval = setInterval(() => {
        progress += 1;
        progressBar.style.width = progress + "%";

        const msg = messages.find(m => m.percent === progress);
        if (msg) loadingMsg.textContent = msg.text;

        if (progress >= 99) {
          clearInterval(interval);
          setTimeout(() => {
            progressBar.style.width = "100%";
            progressContainer.style.display = "none";
            loadingMsg.textContent = "";

            const message = `You were thinking of ${number} 🤯`;
            let i = 0;
            function typeChar() {
              if (i < message.length) {
                reveal.textContent += message.charAt(i);
                i++;
                setTimeout(typeChar, 60);
              } else {
                sound.play();
                // 💸 Show money GIF
                money.style.display = "block";
                setTimeout(() => {
                  money.style.display = "none";
                }, 2000);
              }
            }
            typeChar();
          }, 1500);
        }
      }, 100); // ~10s total
    }
  </script>

</body>
</html>
```
---

## 🛠️ Tech Stack

- **HTML5** – Structural markup  
- **CSS3** – Styling and animations (including `@keyframes`)  
- **JavaScript (Vanilla)** – DOM manipulation, timing, and interaction  
- **Assets** – Background image (`mind-reader-bg.png`), sound effect, and GIF (`money-fall.gif`)

---

## 📚 Learning Outcomes

This project demonstrates:
- Event-driven JavaScript interaction
- Sequential UI updates using timers
- Typing animation logic
- Coordinating media (audio + visuals) for engaging UX
- Creative use of animations to simulate intelligence

---

## 🚀 How to Run

1. Clone or download the repository  
2. Ensure the image and GIF files are in the correct folder (`assets/`)  
3. Open `index.html` in any modern browser  
4. Think of a number and click **"Read My Mind"**

---

## Output

![Mind Reader Demo](mind-reader-output.gif)

> This GIF shows the complete user experience with loading, reveal animation, sound, and mind-reading illusion.


---

## 🧪 Use Cases

- Interactive UI demo for web portfolios  
- Mini-project for JavaScript learners  
- UX psychology experiment mockup  
- Fun illusion to impress friends or interviewers

---

## 🪪 License

This project is open-source and available under the **MIT License**.  
Feel free to reuse, remix, or enhance it!

---

## 🙌 Acknowledgements

- Sound effect by [SoundJay](https://www.soundjay.com/)
- Background and GIF assets created or sourced under free use license
