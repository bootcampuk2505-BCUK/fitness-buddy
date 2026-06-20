<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <title>28‑Day Buddy (Test)</title>
  <meta name="viewport" content="width=device-width, initial-scale=1">
  <style>
    body { font-family: system-ui, sans-serif; margin:0; padding:1rem; background:#f7f7f7; }
    .container { max-width:600px; margin:0 auto; }
    .card { background:#fff; padding:1rem; border-radius:8px; box-shadow:0 1px 3px rgba(0,0,0,0.1); margin-bottom:1rem; }
    h1 { text-align:center; margin:0 0 0.5rem; }
    button { padding:0.4rem 0.8rem; border:none; border-radius:4px; background:#007bff; color:#fff; cursor:pointer; }
    button.secondary { background:#6c757d; }
    .buddy { background:#e3f2fd; border-left:4px solid #2196f3; padding:0.5rem 0.8rem; border-radius:4px; margin-top:0.5rem; }
    label { display:block; margin-top:0.5rem; font-size:0.9rem; }
    input[type="checkbox"]{ margin-right:0.3rem; }
    .small { font-size:0.8rem; color:#666; margin-top:0.5rem; }
  </style>
</head>
<body>
<div class="container">
  <h1>28‑Day Buddy (Test)</h1>
  <div class="card">
    <div>
      <button id="prevBtn" class="secondary">◀ Previous</button>
      <span id="dayLabel" style="margin:0 0.5rem;font-weight:600;"></span>
      <button id="nextBtn">Next ▶</button>
    </div>
    <div class="small">Use this test to confirm buttons and text change. Then we’ll expand it.</div>
  </div>

  <div class="card">
    <h2>Today’s Training</h2>
    <div id="trainingText"></div>

    <h2>Buddy Message</h2>
    <div id="buddyText" class="buddy"></div>
  </div>

  <div class="card">
    <h2>Check‑in</h2>
    <label><input type="checkbox" id="didWorkout">I did today’s training.</label>
    <div class="small" id="statusText"></div>
  </div>
</div>

<script>
  // Very small dummy program just to prove the app works
  const days = [
    {
      day: 1,
      training: "Day 1: Full body basics – squats, push‑ups (wall/knees), lunges, plank.",
      buddy: "Welcome! Today is about starting gently and getting your body moving."
    },
    {
      day: 2,
      training: "Day 2: 30‑minute brisk walk or light stretching for active recovery.",
      buddy: "Nice work yesterday. Today is about keeping the habit alive with low‑stress movement."
    },
    {
      day: 3,
      training: "Day 3: Core & cardio basics – marching high knees, mountain climbers, plank.",
      buddy: "We’re waking up your core and heart. Go at a pace you can control."
    }
  ];

  let currentIndex = 0;

  const dayLabel    = document.getElementById("dayLabel");
  const trainingDiv = document.getElementById("trainingText");
  const buddyDiv    = document.getElementById("buddyText");
  const prevBtn     = document.getElementById("prevBtn");
  const nextBtn     = document.getElementById("nextBtn");
  const didWorkout  = document.getElementById("didWorkout");
  const statusText  = document.getElementById("statusText");

  const STORAGE_KEY = "buddyTestProgress";

  function loadProgress() {
    try {
      return JSON.parse(localStorage.getItem(STORAGE_KEY) || "{}");
    } catch {
      return {};
    }
  }

  function saveProgress(obj) {
    localStorage.setItem(STORAGE_KEY, JSON.stringify(obj));
  }

  function renderDay() {
    const data = days[currentIndex];
    dayLabel.textContent = "Day " + data.day;
    trainingDiv.textContent = data.training;
    buddyDiv.textContent = data.buddy;

    const prog = loadProgress();
    didWorkout.checked = !!prog["day" + data.day];
    updateStatus();
  }

  function updateStatus() {
    const data = days[currentIndex];
    const prog = loadProgress();
    const doneToday = !!prog["day" + data.day];
    const doneCount = Object.keys(prog).length;
    const total = days.length;

    statusText.textContent = doneToday
      ? `You’ve marked today as done. Total days completed: ${doneCount}/${total}.`
      : `You haven’t marked today as done yet. Completed: ${doneCount}/${total}.`;
  }

  prevBtn.addEventListener("click", () => {
    if (currentIndex > 0) {
      currentIndex--;
      renderDay();
    }
  });

  nextBtn.addEventListener("click", () => {
    if (currentIndex < days.length - 1) {
      currentIndex++;
      renderDay();
    }
  });

  didWorkout.addEventListener("change", () => {
    const data = days[currentIndex];
    const prog = loadProgress();
    if (didWorkout.checked) {
      prog["day" + data.day] = true;
    } else {
      delete prog["day" + data.day];
    }
    saveProgress(prog);
    updateStatus();
  });

  // Initial render
  renderDay();
</script>
</body>
</html>
