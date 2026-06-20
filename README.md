<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <title>28‑Day Body Transformation Buddy</title>
  <meta name="viewport" content="width=device-width, initial-scale=1">
  <style>
    body {
      font-family: system-ui, -apple-system, BlinkMacSystemFont, "Segoe UI", sans-serif;
      margin: 0;
      padding: 1rem;
      background:#f7f7f7;
    }
    .container { max-width: 900px; margin: 0 auto; }
    h1 { font-size: 1.6rem; text-align: center; margin:0 0 0.5rem; }
    h2 { font-size:1.1rem; margin:0.4rem 0; }
    .subtitle { text-align:center; font-size:0.9rem; color:#555; margin-bottom:1rem; }
    .card {
      background:#fff; padding:1rem; margin-bottom:1rem;
      border-radius:8px; box-shadow:0 1px 3px rgba(0,0,0,0.08);
    }
    .controls { display:flex; align-items:center; justify-content:space-between; flex-wrap:wrap; gap:0.5rem; }
    .controls button {
      padding:0.4rem 0.8rem; border:none; border-radius:4px;
      background:#007bff; color:#fff; cursor:pointer; font-size:0.9rem;
    }
    .controls button.secondary { background:#6c757d; }
    .day-indicator { font-size:0.9rem; font-weight:600; }
    .phase-tag { font-size:0.8rem; color:#555; }
    .buddy {
      background:#e3f2fd; border-radius:6px; padding:0.6rem 0.8rem; margin-top:0.5rem;
      font-size:0.9rem; border-left:4px solid #2196f3;
    }
    .section { margin-top:0.5rem; }
    .section p { margin:0.2rem 0; font-size:0.9rem; }
    ul { margin:0.3rem 0 0.6rem 1.1rem; padding:0; font-size:0.9rem; }
    label { font-size:0.9rem; display:block; margin-top:0.4rem; }
    input[type="checkbox"] { margin-right:0.3rem; }
    input[type="number"] {
      padding:0.3rem; border-radius:4px; border:1px solid #ccc;
      font-size:0.85rem; width:80px; box-sizing:border-box;
    }
    textarea {
      width:100%; min-height:60px;
      border-radius:4px; border:1px solid #ccc; padding:0.4rem; font-size:0.85rem;
      box-sizing:border-box; margin-top:0.2rem;
    }
    .progress {
      margin-top:0.7rem; font-size:0.85rem; color:#555;
    }
    .bar-bg { width:100%; background:#eee; border-radius:999px; overflow:hidden; height:12px; margin-top:0.2rem; }
    .bar-fill { height:100%; width:0%; background:#4caf50; transition:width 0.2s linear; }
    .small { font-size:0.8rem; color:#666; }
  </style>
</head>
<body>
<div class="container">
  <h1>28‑Day Transformation Buddy</h1>
  <div class="subtitle">Daily training + nutrition focus based on your 28‑Day Body Transformation Blueprint (Home Edition).</div>

  <div class="card">
    <div class="controls">
      <button id="prevBtn" class="secondary">◀ Previous</button>
      <div>
        <div class="day-indicator" id="dayLabel"></div>
        <div class="phase-tag" id="phaseLabel"></div>
      </div>
      <button id="nextBtn">Next ▶</button>
    </div>
    <div style="margin-top:0.5rem;">
      <label for="daySelect">Jump to day:</label>
      <input type="number" id="daySelect" min="1" max="28">
      <button id="goBtn" class="secondary">Go</button>
    </div>
  </div>

  <div class="card">
    <h2>Today’s Training Plan</h2>
    <div id="trainingText" class="section"></div>

    <h2>Today’s Nutrition Focus</h2>
    <div id="nutritionText" class="section"></div>

    <h2>Buddy Message</h2>
    <div id="buddyText" class="buddy"></div>
  </div>

  <div class="card">
    <h2>Check‑ins</h2>
    <label>
      <input type="checkbox" id="didWorkout">
      I completed (or did my best with) today’s training.
    </label>
    <label>
      <input type="checkbox" id="followedNutrition">
      I followed today’s nutrition focus as best I could.
    </label>

    <label for="notes">Notes for today (how you felt, wins, struggles):</label>
    <textarea id="notes" placeholder="e.g. Found squats easier, struggled with evening snacking."></textarea>

    <div class="progress">
      Overall plan progress:
      <div class="bar-bg"><div class="bar-fill" id="overallBar"></div></div>
      <div class="small" id="overallText"></div>
    </div>
  </div>
</div>

<script>
  // 28‑day program: training + nutrition based on your blog (condensed).
  // You can tweak any text later to match your exact branding/tone.

  const program = [
    // WEEK 1 – Form & Mobility
    {
      d:1, phase:"Week 1 · Foundation (Form & Mobility)",
      training:`
        <p><strong>Full‑Body Strength (Home)</strong></p>
        <ul>
          <li>Warm‑up: 5–10 min brisk walk on the spot + arm / hip circles.</li>
          <li>3 rounds:
            <ul>
              <li>Bodyweight squats × 10–12.</li>
              <li>Push‑ups × 6–10 (wall or knees).</li>
              <li>Reverse lunges × 8–10 each leg.</li>
              <li>Plank 20–30 sec (knees if needed).</li>
            </ul>
          </li>
          <li>Cool down: gentle stretching.</li>
        </ul>`,
      nutrition:`
        <p><strong>Focus:</strong> Start eating for performance, not punishment.</p>
        <ul>
          <li>Protein at each meal (eggs, chicken, tofu, yogurt, lentils, fish).</li>
          <li>Base carbs on <em>complex</em> sources (oats, sweet potato, brown rice, wholegrain bread).</li>
          <li>Begin aiming for 2.5–3 L water.</li>
        </ul>`,
      buddy:"Welcome to Day 1! Today is about setting your ‘why’ and moving with control, not chasing exhaustion. You’ve started."
    },
    {
      d:2, phase:"Week 1 · Foundation (Form & Mobility)",
      training:`
        <p><strong>Active Recovery</strong></p>
        <ul>
          <li>30‑minute brisk walk (outside if possible) or light mobility / stretching.</li>
          <li>Keep intensity low – you should be able to hold a conversation.</li>
        </ul>`,
      nutrition:`
        <p><strong>Focus:</strong> Balanced, regular meals.</p>
        <ul>
          <li>Protein at breakfast and lunch.</li>
          <li>Half‑plate of veg at lunch and dinner.</li>
          <li>Simple snacks: fruit + nuts, veg sticks + hummus, yogurt.</li>
        </ul>`,
      buddy:"Recovery is part of the program, not a break from it. Today is about gentle movement and keeping your food simple and consistent."
    },
    {
      d:3, phase:"Week 1 · Foundation (Form & Mobility)",
      training:`
        <p><strong>Core & Cardio Basics</strong></p>
        <ul>
          <li>Warm‑up: 5–10 min marching, torso twists, shoulder rolls.</li>
          <li>3–4 rounds:
            <ul>
              <li>Marching high knees × 30 sec (or easy jog on spot).</li>
              <li>Mountain climbers × 20 total (hands on wall/table if needed).</li>
              <li>Bicycle crunches × 10–15 each side (or basic crunches).</li>
              <li>Plank 20–30 sec.</li>
            </ul>
          </li>
        </ul>`,
      nutrition:`
        <p><strong>Focus:</strong> Fuel for movement.</p>
        <ul>
          <li>Have a light carb + protein snack 60–90 min before training (e.g. banana + yogurt).</li>
          <li>Keep added sugar modest; prioritise whole foods.</li>
        </ul>`,
      buddy:"We’re waking up your core and engine. Move at a pace you can control. You’re building the base for outdoor bootcamps."
    },
    {
      d:4, phase:"Week 1 · Foundation (Form & Mobility)",
      training:`<p><strong>Rest Day</strong> – gentle walking and stretching only.</p>`,
      nutrition:`
        <p><strong>Focus:</strong> Stay on track without “dieting”.</p>
        <ul>
          <li>Eat normally – don’t starve yourself because you’re resting.</li>
          <li>Stay hydrated and keep snacking mindful (hunger vs boredom).</li>
        </ul>`,
      buddy:"Rest like an athlete today. You’re not being lazy, you’re recovering so you can train harder later."
    },
    {
      d:5, phase:"Week 1 · Foundation (Form & Mobility)",
      training:`
        <p><strong>Lower Body Focus</strong></p>
        <ul>
          <li>Warm‑up: 5–10 min brisk walk, leg swings, hip circles.</li>
          <li>3–4 rounds: squats, reverse lunges, glute bridges, wall sits.</li>
        </ul>`,
      nutrition:`
        <p><strong>Focus:</strong> Carbs + protein for leg recovery.</p>
        <ul>
          <li>Add a complex carb to your post‑workout meal (oats, rice, potato).</li>
          <li>Include a palm‑sized protein serving at lunch and dinner.</li>
        </ul>`,
