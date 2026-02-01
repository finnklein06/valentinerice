<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8" />
<meta name="viewport" content="width=device-width, initial-scale=1.0" />
<title>Valentine</title>

<style>
  body {
    margin: 0;
    height: 100vh;
    font-family: -apple-system, BlinkMacSystemFont, "Segoe UI", sans-serif;
    background: #f6c1d1;
    display: flex;
    justify-content: center;
    align-items: center;
    overflow: hidden;
  }

  .card {
    background: #fff;
    padding: 30px 25px 40px;
    border-radius: 16px;
    text-align: center;
    width: 90%;
    max-width: 420px;
    box-shadow: 0 10px 30px rgba(0,0,0,0.15);
    position: relative;
    transition: transform 0.6s ease;
  }

  .emoji {
    font-size: 60px;
    margin-bottom: 15px;
  }

  h1 {
    font-size: 22px;
    margin-bottom: 30px;
    font-weight: 600;
  }

  .buttons {
    position: relative;
    height: 120px;
  }

  button {
    border: none;
    border-radius: 999px;
    padding: 14px 28px;
    font-size: 18px;
    cursor: pointer;
    position: absolute;
    transition: transform 0.2s ease;
  }

  #yes {
    background: #ff4d6d;
    color: #fff;
    left: 50%;
    transform: translateX(-50%);
    bottom: 0;
  }

  #no {
    background: #e5e5e5;
    color: #000;
    left: 50%;
    transform: translateX(-50%);
    top: 0;
  }

  .hint {
    margin-top: 15px;
    font-size: 13px;
    color: #777;
  }

  /* YES animation */
  .success {
    position: absolute;
    inset: 0;
    background: #fff;
    border-radius: 16px;
    display: flex;
    flex-direction: column;
    justify-content: center;
    align-items: center;
    animation: pop 0.6s ease forwards;
    z-index: 5;
  }

  .success h2 {
    font-size: 26px;
    margin: 15px 0 5px;
  }

  .success p {
    font-size: 16px;
    color: #555;
  }

  @keyframes pop {
    from { transform: scale(0.6); opacity: 0; }
    to   { transform: scale(1); opacity: 1; }
  }

  /* floating hearts */
  .heart {
    position: absolute;
    font-size: 24px;
    animation: floatUp 2.5s ease forwards;
    pointer-events: none;
  }

  @keyframes floatUp {
    from { transform: translateY(0) scale(1); opacity: 1; }
    to   { transform: translateY(-120px) scale(1.5); opacity: 0; }
  }
</style>
</head>

<body>
  <div class="card" id="card">
    <div class="emoji">🐱❤️</div>
    <h1>rice will you be my valentine?</h1>

    <div class="buttons">
      <button id="no">No</button>
      <button id="yes">Yes</button>
    </div>

    <div class="hint">"No" seems a bit shy 😈</div>
  </div>

<script>
  const noBtn = document.getElementById("no");
  const yesBtn = document.getElementById("yes");
  const card = document.getElementById("card");

  let yesScale = 1;

  function moveNoButton() {
    const rect = card.getBoundingClientRect();
    const maxX = rect.width - noBtn.offsetWidth;
    const maxY = rect.height - noBtn.offsetHeight - 60;

    noBtn.style.left = Math.random() * maxX + "px";
    noBtn.style.top  = Math.random() * maxY + "px";

    yesScale += 0.15;
    yesBtn.style.transform = `translateX(-50%) scale(${yesScale})`;
  }

  noBtn.addEventListener("mouseenter", moveNoButton);
  noBtn.addEventListener("touchstart", e => {
    e.preventDefault();
    moveNoButton();
  });

  yesBtn.addEventListener("click", () => {
    // disable buttons
    yesBtn.disabled = true;
    noBtn.disabled = true;

    // success overlay
    const success = document.createElement("div");
    success.className = "success";
    success.innerHTML = `
      <div style="font-size:60px">🎉💖</div>
      <h2>Yay! 💘</h2>
      <p>Best decision ever.</p>
    `;
    card.appendChild(success);

    // hearts
    for (let i = 0; i < 12; i++) {
      const heart = document.createElement("div");
      heart.className = "heart";
      heart.textContent = "❤️";
      heart.style.left = Math.random() * window.innerWidth + "px";
      heart.style.bottom = "0px";
      document.body.appendChild(heart);

      setTimeout(() => heart.remove(), 2500);
    }
  });
</script>
</body>
</html>
