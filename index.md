---
layout: default
title: null
---

<head>
    <link rel="stylesheet" href="styles.css">
    <style>
    .audio-player {
      display: flex;
      align-items: center;
      gap: 10px;
      background: linear-gradient(135deg, #4b6cb7, #182848);
      padding: 12px 16px;
      border-radius: 12px;
      box-shadow: 0 4px 10px rgba(0,0,0,0.3);
      color: white;
      width: 320px;
      margin-bottom: 15px;
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
    }

    .audio-player button:hover {
      background: #ff5722;
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

Artificial Intelligence (AI) for music generation is undergoing rapid developments, with recent symbolic models leveraging sophisticated deep learning and diffusion model algorithms. However, one drawback with existing models is that they lack structural cohesion, particularly on harmonic-melodic structure. Furthermore, such existing models are largely “black-box” in nature and are not musically interpretable. This paper addresses these limitations via a novel generative music framework that incorporates concepts of Schenkerian analysis (SchA) in concert with a diffusion modeling framework. This framework, which we call ProGress(Prolongation-enhanced DiGress), adapts state-of-the-art deep models for discrete diffusion (in particular, the DiGress model of Vignac et al., 2023) for interpretable and structured music generation. Concretely, our contributions include 1) novel adaptations of the DiGress model for music generation, 2) a novel SchA-inspired phrase fusion methodology, and 3) a framework allowing users to control various aspects of the generation process to create coherent musical compositions. Results from human experiments suggest superior performance to existing state-of-the-art methods.

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

function createPlayer(url) {
  const container = document.createElement("div");
  container.className = "audio-player";

  const btn = document.createElement("button");
  btn.textContent = "▶";

  const progressWrapper = document.createElement("div");
  progressWrapper.className = "audio-progress";
  const progressBar = document.createElement("div");
  progressWrapper.appendChild(progressBar);

  const audio = document.createElement("audio");
  audio.src = url;

  btn.addEventListener("click", () => {
    if (audio.paused) {
      // Pause others
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

  audio.addEventListener("timeupdate", () => {
    progressBar.style.width = (audio.currentTime / audio.duration) * 100 + "%";
  });

  audio.addEventListener("ended", () => {
    btn.textContent = "▶";
    progressBar.style.width = "0%";
  });

  container.appendChild(btn);
  container.appendChild(progressWrapper);
  container.appendChild(audio);

  document.getElementById("players").appendChild(container);
}

audioFiles.forEach(url => createPlayer(url));
</script>
