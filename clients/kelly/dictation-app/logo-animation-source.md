---
kind: asset-source
client: kelly
project: avelisse-dictation-app
tags: [kelly, dictation-app, branding, logo]
created: 2026-08-20
updated: 2026-08-22
---

# Logo Animation Source

HTML/JS canvas source for the AVELISSE animated wave+particle logo. This is what got ported into the `DictusWaveformLogo` composable and rendered as Android vector/PNG assets — see the 2026-08-20 entry in [[clients/kelly/dictation-app/updates-android|Android updates]].

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0" />

  <style>
    * {
      margin: 0;
      padding: 0;
      box-sizing: border-box;
    }

    html,
    body {
      width: 100%;
      height: 100%;
      overflow: hidden;
      background: #f7f7f7;
    }

    canvas {
      display: block;
      width: 100%;
      height: 100%;
    }
  </style>
</head>

<body>

<canvas id="canvas"></canvas>

<script>
const canvas = document.getElementById("canvas");
const ctx = canvas.getContext("2d");

let width;
let height;
let dpr;
let time = 0;


// --------------------------------------------------
// RESIZE
// --------------------------------------------------

function resize() {
  dpr = window.devicePixelRatio || 1;

  width = window.innerWidth;
  height = window.innerHeight;

  canvas.width = width * dpr;
  canvas.height = height * dpr;

  canvas.style.width = width + "px";
  canvas.style.height = height + "px";

  ctx.setTransform(dpr, 0, 0, dpr, 0, 0);
}

window.addEventListener("resize", resize);
resize();


// --------------------------------------------------
// COLORS
// --------------------------------------------------

const colors = {
  background: "#F7F7F7",
  silhouette: "#26383A",
  teal: "#007C92",
  terracotta: "#D85C27",
  sand: "#F3E5AB"
};


// --------------------------------------------------
// SOUND WAVES
// --------------------------------------------------

function drawSoundWaves() {

  const centerX = width / 2;
  const centerY = height * 0.43;

  const waveWidth = Math.min(width * 0.30, 380);

  const waves = [
    {
      color: colors.teal,
      amplitude: 22,
      frequency: 0.035,
      speed: 0.055,
      thickness: 3,
      alpha: 0.9
    },
    {
      color: colors.terracotta,
      amplitude: 12,
      frequency: 0.055,
      speed: -0.04,
      thickness: 2,
      alpha: 0.6
    },
    {
      color: colors.teal,
      amplitude: 34,
      frequency: 0.022,
      speed: 0.025,
      thickness: 2,
      alpha: 0.35
    }
  ];

  waves.forEach((wave) => {

    ctx.beginPath();

    for (
      let x = -waveWidth / 2;
      x <= waveWidth / 2;
      x += 2
    ) {

      const normalized =
        x / (waveWidth / 2);

      const envelope = Math.pow(
        Math.max(0, 1 - Math.abs(normalized)),
        0.65
      );

      const primary =
        Math.sin(
          x * wave.frequency +
          time * wave.speed
        );

      const secondary =
        Math.sin(
          x * wave.frequency * 1.8 -
          time * wave.speed * 0.7
        );

      const y =
        centerY +
        (
          primary * wave.amplitude +
          secondary * wave.amplitude * 0.25
        ) * envelope;

      if (x === -waveWidth / 2) {
        ctx.moveTo(
          centerX + x,
          y
        );
      } else {
        ctx.lineTo(
          centerX + x,
          y
        );
      }
    }

    ctx.strokeStyle = wave.color;
    ctx.globalAlpha = wave.alpha;
    ctx.lineWidth = wave.thickness;
    ctx.lineCap = "round";

    ctx.stroke();

    ctx.globalAlpha = 1;
  });
}


// --------------------------------------------------
// SMALL SOUND PARTICLES
// --------------------------------------------------

function drawParticles() {

  const centerX = width / 2;
  const centerY = height * 0.43;

  for (let i = 0; i < 16; i++) {

    const phase =
      time * 0.025 + i * 0.9;

    const x =
      centerX +
      Math.sin(phase) *
      Math.min(width * 0.17, 220);

    const y =
      centerY +
      Math.cos(
        phase * 1.4 + i
      ) * 35;

    const radius =
      1.5 +
      Math.sin(phase * 2) * 1;

    ctx.beginPath();

    ctx.arc(
      x,
      y,
      radius,
      0,
      Math.PI * 2
    );

    ctx.fillStyle =
      i % 3 === 0
        ? colors.terracotta
        : colors.teal;

    ctx.globalAlpha = 0.35;

    ctx.fill();

    ctx.globalAlpha = 1;
  }
}


// --------------------------------------------------
// MAIN ANIMATION
// --------------------------------------------------

function animate() {

  ctx.clearRect(
    0,
    0,
    width,
    height
  );

  // Background
  ctx.fillStyle = colors.background;

  ctx.fillRect(
    0,
    0,
    width,
    height
  );

  // Keep particles
  drawParticles();

  // Animated waves
  drawSoundWaves();

  time++;

  requestAnimationFrame(animate);
}

animate();

</script>

</body>
</html>
```
