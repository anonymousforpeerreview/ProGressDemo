---
layout: default
title: null
---

<head>
    <link rel="stylesheet" href="styles.css">
    <style>
    #players {
      display: grid;
      grid-template-columns: repeat(auto-fit, minmax(320px, 1fr));
      gap: 15px;
      margin-top: 15px;
    }

    .audio-player {
      display: flex;
      flex-direction: column;
      background: linear-gradient(135deg, #4b6cb7, #182848);
      padding: 12px 16px;
      border-radius: 12px;
      box-shadow: 0 4px 10px rgba(0,0,0,0.3);
      color: white;
    }

    .audio-controls {
      display: flex;
      align-items: center;
      gap: 10px;
      margin-bottom: 8px;
    }

    .audio-player button {
      background: #ff7f50;
      border: none;
      border-radius: 50%;
      width: 40px;
      height: 40px;
      color: white;
      font-size: 18px;
      cursor: pointer;
      transition: background 0.3s ease;
      flex-shrink: 0;
    }

    .audio-player button:hover {
      background: #ff5722;
    }

    .audio-progress-container {
      display: flex;
      align-items: center;
      gap: 6px;
    }

    .audio-time {
      font-size: 0.8em;
      width: 38px;
      text-align: center;
    }

    .audio-progress {
      flex: 1;
      height: 6px;
      background: rgba(255,255,255,0.3);
      border-radius: 3px;
      overflow: hidden;
    }

    .audio-progress div {
      height: 100%;
      background: #ff7f50;
      width: 0%;
      transition: width 0.1s;
    }
    </style>
</head>

<h1 style="text-align: center;">ProGress: Structured Music Generation via Graph Diffusion and Hierarchical Music Analysis</h1>
<p style="text-align: center;">
    Anonymous Authors
    <br>
    [Paper] | [Code Repo]
</p>
<small>
This is the demo page of the paper: ProGress: Structured Music Generation via Graph Diffusion and Hierarchical Music Analysis.
</small>
<br>

# Abstract



# Example

<div id="players"></div>

<script>
const audioFiles = [
  "https://duke.yul1.qualtrics.com/ControlPanel/File.php?F=F_TWXnKENrvX5TbNW",
  "https://duke.yul1.qualtrics.com/ControlPanel/File.php?F=F_SqaRufnFbLXPIcX",
  "https://duke.yul1.qualtrics.com/ControlPanel/File.php?F=F_WmiqHpdvWbgHa3Z",
  "https://duke.yul1.qualtrics.com/ControlPanel/File.php?F=F_XpbIdfRUqmkbHZM",
  "https://duke.yul1.qualtrics.com/ControlPanel/File.php?F=F_YapUmBLldzFc9nM",
  "https://duke.yul1.qualtrics.com/ControlPanel/File.php?F=F_p10bOgoomVyZgUB",
  "https://duke.yul1.qualtrics.com/ControlPanel/File.php?F=F_Ti6pFfJlltrARTN",
  "https://duke.yul1.qualtrics.com/ControlPanel/File.php?F=F_CVdrnp6jyqwq6lW",
  "https://duke.yul1.qualtrics.com/ControlPanel/File.php?F=F_00Wet0rQswbFSQb",
  "https://duke.yul1.qualtrics.com/ControlPanel/File.php?F=F_cjZVzIEjhiYsMy5"
];

function formatTime(seconds) {
  if (isNaN(seconds)) return "0:00";
  const m = Math.floor(seconds / 60);
  const s = Math.floor(seconds % 60).toString().padStart(2, "0");
  return `${m}:${s}`;
}

function createPlayer(url) {
  const container = document.createElement("div");
  container.className = "audio-player";

  const controls = document.createElement("div");
  controls.className = "audio-controls";

  const btn = document.createElement("button");
  btn.textContent = "▶";

  const audio = document.createElement("audio");
  audio.src = url;

  controls.appendChild(btn);

  const progressContainer = document.createElement("div");
  progressContainer.className = "audio-progress-container";

  const currentTimeLabel = document.createElement("div");
  currentTimeLabel.className = "audio-time";
  currentTimeLabel.textContent = "0:00";

  const progressWrapper = document.createElement("div");
  progressWrapper.className = "audio-progress";
  const progressBar = document.createElement("div");
  progressWrapper.appendChild(progressBar);

  const durationLabel = document.createElement("div");
  durationLabel.className = "audio-time";
  durationLabel.textContent = "0:00";

  progressContainer.appendChild(currentTimeLabel);
  progressContainer.appendChild(progressWrapper);
  progressContainer.appendChild(durationLabel);

  container.appendChild(controls);
  container.appendChild(progressContainer);
  controls.appendChild(progressWrapper);

  btn.addEventListener("click", () => {
    if (audio.paused) {
      document.querySelectorAll("audio").forEach(a => {
        if (a !== audio) {
          a.pause();
          a.parentElement.querySelector("button").textContent = "▶";
        }
      });
      audio.play();
      btn.textContent = "⏸";
    } else {
      audio.pause();
      btn.textContent = "▶";
    }
  });

  audio.addEventListener("loadedmetadata", () => {
    durationLabel.textContent = formatTime(audio.duration);
  });

  audio.addEventListener("timeupdate", () => {
    currentTimeLabel.textContent = formatTime(audio.currentTime);
    progressBar.style.width = (audio.currentTime / audio.duration) * 100 + "%";
  });

  audio.addEventListener("ended", () => {
    btn.textContent = "▶";
    progressBar.style.width = "0%";
    currentTimeLabel.textContent = "0:00";
  });

  container.appendChild(audio);
  document.getElementById("players").appendChild(container);
}

audioFiles.forEach(url => createPlayer(url));
</script>
