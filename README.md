# fitness-buddy

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
    h2 { font-size: 1.1rem; margin:0.3rem 0; }
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
    .day-indicator { font-size:0.9rem; }
    .phase-tag { font-size:0.8rem; color:#555; }
    .buddy {
      background:#e3f2fd; border-radius:6px; padding:0.6rem 0.8rem; margin-top:0.5rem;
      font-size:0.9rem; border-left:4px solid #2196f3;
    }
    .section { margin-top:0.5rem; }
    .section p { margin:0.2rem 0; font-size:0.9rem; }
    ul { margin:0.3rem 0 0.6rem 1rem; padding:0; font-size:0.9rem; }
    label { font-size:0.9rem; display:block; margin-top:0.4rem; }
    input[type="checkbox"] { margin-right:0.3rem; }
    .progress {
      margin-top:0.5rem; font-size:0.85rem; color:#555;
    }
    .bar-bg { width:100%; background:#eee; border-radius:999px; overflow:hidden; height:12px; margin-top:0.2rem; }
    .bar-fill { height:100%; width:0%; background:#4caf50; transition:width 0.2s linear; }
    .small { font-size:0.8rem; color:#666; }
    textarea {
      width:100%; min-height:50px;
      border-radius:4px; border:1px solid #ccc; padding:0.4rem; font-size:0.85rem;
      box-sizing:border-box; margin-top:0.2rem;
    }
  </style>
</head>
<body>
<div class="container">
  <h1>28‑Day Transformation Buddy</h1>
  <div class="subtitle">Daily guidance for training & nutrition based on your 28‑Day Body Transformation Blueprint.</div>

  <div class="card">
    <div class="controls">
      <button id="prevBtn" class="secondary">◀ Previous</button>
      <div>
        <span class="day-indicator" id="dayLabel"></span><br>
        <span class="phase-tag" id="phaseLabel"></span>
      </div>
      <button id="nextBtn">Next ▶</button>
    </div>
    <div style="margin-top:0.5rem;">
      <label for="daySelect">Jump to day:</label>
      <input type="number" id="daySelect" min="1" max="28" style="max-width:80px;">
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
    <textarea id="notes" placeholder="e.g. Struggled with push‑ups but nailed the walk. Felt more energetic after breakfast."></textarea>

    <div class="progress">
      Overall plan progress:
      <div class="bar-bg"><div class="bar-fill" id="overallBar"></div></div>
      <div class="small" id="overallText"></div>
    </div>
  </div>

</div>

<script>
  // ------------- PROGRAM DATA (28 DAYS) -----------------
  // High-level summary text per day, based on your blog structure.

  const program = [
    // WEEK 1 – Form & Mobility
    {
      day: 1, week: 1, phase: "Week 1 · Form & Mobility",
      training: `
      <p><strong>Full Body Strength (Home)</strong></p>
      <ul>
        <li>Warm‑up: 5–10 min brisk walk on the spot + arm circles + hip circles.</li>
        <li>3 rounds:
          <ul>
            <li>Bodyweight squats × 10–12 (slow, good form).</li>
            <li>Push‑ups × 6–10 (knees or wall if needed).</li>
            <li>Reverse lunges × 8–10 each leg (hold a chair if needed).</li>
            <li>Plank hold 20–30 sec (knees if needed).</li>
          </ul>
        </li>
        <li>Cool down: gentle stretching of legs, chest, shoulders.</li>
      </ul>
      `,
      nutrition: `
      <p><strong>Focus:</strong> Start eating for energy, not restriction.</p>
      <ul>
        <li>Include protein at each meal (eggs, Greek yogurt, chicken, tofu, lentils).</li>
        <li>Base your carbs on <em>complex</em> sources (oats, brown rice, sweet potato, wholegrain bread).</li>
        <li>Start aiming for 2.5–3 L of water today.</li>
      </ul>
      <p><strong>Sample day:</strong> Oats + berries + yogurt · Apple with nut butter · Salad + chicken + avocado · Veg + hummus · Salmon + sweet potato + broccoli.</p>
      `,
      buddy: "Welcome to Day 1! Today is about moving with control and setting your intention. Don’t chase fatigue yet—chase good form and a clear ‘why’ for the next 28 days."
    },
    {
      day: 2, week: 1, phase: "Week 1 · Form & Mobility",
      training: `
      <p><strong>Active Recovery</strong></p>
      <ul>
        <li>30‑minute brisk walk (outside if possible) or light stretching/mobility session.</li>
        <li>Keep intensity low; you should be able to hold a conversation.</li>
      </ul>
      `,
      nutrition: `
      <p><strong>Focus:</strong> Consistency with balanced meals.</p>
      <ul>
        <li>Hit protein at breakfast and lunch.</li>
        <li>Fill half your plate with veg at lunch and dinner.</li>
        <li>Keep snacks simple: fruit + nuts, veg sticks + hummus, yogurt.</li>
      </ul>
      `,
      buddy: "Recovery is part of training. Today the goal is to move gently and nourish your body. You’re building a habit, not chasing perfection."
    },
    {
      day: 3, week: 1, phase: "Week 1 · Form & Mobility",
      training: `
      <p><strong>Core & Cardio Basics</strong></p>
      <ul>
        <li>Warm‑up: 5–10 min marching on the spot + torso twists.</li>
        <li>3–4 rounds:
          <ul>
            <li>Marching high knees × 30 sec (or gentle jog on the spot).</li>
            <li>Mountain climbers (slow) × 20 total (hands on wall/table if needed).</li>
            <li>Bicycle crunches × 10–15 each side (or simple knee‑to‑chest crunches).</li>
            <li>Plank 20–30 sec.</li>
          </ul>
        </li>
      </ul>
      `,
      nutrition: `
      <p><strong>Focus:</strong> Fuel for movement.</p>
      <ul>
        <li>Have a small carb + protein snack 60–90 min before training (e.g. banana + yogurt).</li>
        <li>Keep added sugar moderate—prioritise whole foods.</li>
      </ul>
      `,
      buddy: "Today we wake up your core and basic cardio. Move at a pace you can control. Each rep is a vote for your future outdoor bootcamp self."
    },
    {
      day: 4, week: 1, phase: "Week 1 · Form & Mobility",
      training: `
      <p><strong>Rest Day</strong></p>
      <ul>
        <li>Light walking is fine, but no structured workout.</li>
        <li>Use 5–10 min for gentle stretching or breathing exercises.</li>
      </ul>
      `,
      nutrition: `
      <p><strong>Focus:</strong> Stay on track without “dieting”.</p>
      <ul>
        <li>Keep your usual balanced meals; don’t drastically cut food because you’re resting.</li>
        <li>Stay hydrated and keep snacking mindful (ask: “Am I hungry or just bored?”).</li>
      </ul>
      `,
      buddy: "Rest today is an investment in the next three weeks. You’re not being lazy—you’re recovering like an athlete."
    },
    {
      day: 5, week: 1, phase: "Week 1 · Form & Mobility",
      training: `
      <p><strong>Lower Body Focus</strong></p>
      <ul>
        <li>Warm‑up: 5–10 min brisk walk, leg swings, hip circles.</li>
        <li>3–4 rounds:
          <ul>
            <li>Bodyweight squats × 12–15.</li>
            <li>Reverse lunges × 8–10 each leg.</li>
            <li>Glute bridge × 12–15.</li>
            <li>Wall sit 20–30 sec.</li>
          </ul>
        </li>
      </ul>
      `,
      nutrition: `
      <p><strong>Focus:</strong> Support recovery with carbs + protein.</p>
      <ul>
        <li>Add a complex carb serving to your post‑workout meal (oats, rice, potato).</li>
        <li>Include a palm‑sized protein portion at lunch and dinner.</li>
      </ul>
      `,
      buddy: "Leg day at home builds the foundation for running on grass and tackling hills in your future bootcamps. Control each rep and breathe."
    },
    {
      day: 6, week: 1, phase: "Week 1 · Form & Mobility",
      training: `
      <p><strong>Upper Body Focus</strong></p>
      <ul>
        <li>Warm‑up: arm circles, shoulder rolls, light marching.</li>
        <li>3–4 rounds:
          <ul>
            <li>Push‑ups × 6–10 (wall or knees as needed).</li>
            <li>Tricep dips on a sturdy chair × 8–12.</li>
            <li>Superman holds × 10–15 sec (2–3 reps).</li>
            <li>Side plank 15–20 sec each side (knees if needed).</li>
          </ul>
        </li>
      </ul>
      `,
      nutrition: `
      <p><strong>Focus:</strong> Protein for upper body repair.</p>
      <ul>
        <li>Prioritise lean proteins today: chicken, turkey, fish, tofu, Greek yogurt.</li>
        <li>Keep portions of highly processed snacks smaller and occasional.</li>
      </ul>
      `,
      buddy: "Your push‑ups and upper‑body strength will pay off when you’re doing partner drills and equipment work at Bootcamp UK. Show up for your future self."
    },
    {
      day: 7, week: 1, phase: "Week 1 · Form & Mobility",
      training: `
      <p><strong>Rest + Meal Prep</strong></p>
      <ul>
        <li>No formal workout—walk and stretch as desired.</li>
        <li>Spend ~2 hours prepping:
          <ul>
            <li>Cook proteins (chicken, tofu, eggs, etc.).</li>
            <li>Cook complex carbs (rice, quinoa, potatoes).</li>
            <li>Wash/chop veg for quick salads and snacks.</li>
          </ul>
        </li>
      </ul>
      `,
      nutrition: `
      <p><strong>Focus:</strong> Set yourself up for Week 2.</p>
      <ul>
        <li>Prep at least 2–3 lunches and dinners in advance.</li>
        <li>Plan snacks: fruit, nuts, veg sticks, hummus.</li>
      </ul>
      `,
      buddy: "Today you’re building the nutrition scaffolding that keeps you consistent when life gets busy. Future‑you will be very grateful."
    },

    // WEEK 2 – HIIT & Endurance
    {
      day: 8, week: 2, phase: "Week 2 · HIIT & Endurance",
      training: `
      <p><strong>20‑Minute Full‑Body HIIT</strong> (40 sec work / 20 sec rest × 4 rounds)</p>
      <ul>
        <li>Jumping jacks or step jacks.</li>
        <li>Bodyweight squats or squat jumps.</li>
        <li>Mountain climbers (hands on chair if needed).</li>
        <li>Alternating lunges.</li>
        <li>Bicycle crunches (or knee‑to‑chest crunches).</li>
      </ul>
      `,
      nutrition: `
      <p><strong>Focus:</strong> Carb timing for HIIT.</p>
      <ul>
        <li>Have a light carb‑focused snack 60–90 min before (banana, oats, toast).</li>
        <li>Post‑workout: protein + complex carb (e.g. chicken + rice, yogurt + fruit).</li>
      </ul>
      `,
      buddy: "HIIT day! Work at a pace where you can breathe hard but still move with control. You’re teaching your heart and lungs to keep up with outdoor sessions."
    },
    {
      day: 9, week: 2, phase: "Week 2 · HIIT & Endurance",
      training: `
      <p><strong>Active Recovery</strong></p>
      <ul>
        <li>30 min easy walk or gentle mobility flow.</li>
        <li>Optional: 5–10 min of deep breathing before bed.</li>
      </ul>
      `,
      nutrition: `
      <p><strong>Focus:</strong> Hydration + veg.</p>
      <ul>
        <li>Keep water at 2.5–3 L.</li>
        <li>Try to include veg or salad with at least 2 meals.</li>
      </ul>
      `,
      buddy: "Recovery makes HIIT more effective. Think of today as maintenance for your engine, not a day off from progress."
    },
    {
      day: 10, week: 2, phase: "Week 2 · HIIT & Endurance",
      training: `
      <p><strong>20‑Minute Lower Body HIIT</strong></p>
      <ul>
        <li>Similar 40/20 format. Choose 4–5 lower‑body moves:
          <ul>
            <li>Squats / squat pulses.</li>
            <li>Reverse lunges.</li>
            <li>Glute bridges.</li>
            <li>Step‑ups on a low step.</li>
          </ul>
        </li>
      </ul>
      `,
      nutrition: `
      <p><strong>Focus:</strong> Refuel legs.</p>
      <ul>
        <li>Include a starchy carb at your post‑workout meal.</li>
        <li>Keep added sugar modest; prioritise wholegrain and root veg.</li>
      </ul>
      `,
      buddy: "Lower‑body HIIT is preparing you for hills, sprints, and team games. Go steady but committed—this is where fat loss and endurance kick up a level."
    },
    {
      day: 11, week: 2, phase: "Week 2 · HIIT & Endurance",
      training: `
      <p><strong>Upper Body Strength (slower pace)</strong></p>
      <ul>
        <li>Push‑ups, rows (with bands or household items), tricep dips, shoulder taps.</li>
        <li>Focus on controlled reps and good posture, not speed.</li>
      </ul>
      `,
      nutrition: `
      <p><strong>Focus:</strong> Protein coverage across the day.</p>
      <ul>
        <li>Aim for protein at all 3 main meals.</li>
        <li>If you snack, make at least one snack protein‑based (yogurt, eggs, hummus, protein shake).</li>
      </ul>
      `,
      buddy: "Slower doesn’t mean easier—it means more control. You’re building the strength to handle new equipment and partner drills outdoors."
    },
    {
      day: 12, week: 2, phase: "Week 2 · HIIT & Endurance",
      training: `
      <p><strong>20‑Minute Core & Cardio HIIT</strong></p>
      <ul>
        <li>Mix moves: mountain climbers, high‑knee marches/jogs, planks, dead bugs, Russian twists.</li>
        <li>Same 40/20 pattern for about 4 rounds.</li>
      </ul>
      `,
      nutrition: `
      <p><strong>Focus:</strong> Balanced plate.</p>
      <ul>
        <li>Each main meal: 1/2 veg, 1/4 protein, 1/4 complex carbs, plus a thumb of healthy fats.</li>
      </ul>
      `,
      buddy: "Core + cardio days build resilience. Every rep is making outdoor sessions feel less scary and more exciting."
    },
    {
      day: 13, week: 2, phase: "Week 2 · HIIT & Endurance",
      training: `
      <p><strong>Long Walk or Light Jog (45 min)</strong></p>
      <ul>
        <li>Walk briskly outdoors; or alternate 1 min easy jog / 2 min walk.</li>
        <li>Focus on breathing and posture, not speed.</li>
      </ul>
      `,
      nutrition: `
      <p><strong>Focus:</strong> Steady energy.</p>
      <ul>
        <li>Avoid huge blood sugar swings: pair carbs with protein or fat.</li>
        <li>Keep hydrated throughout your walk/jog.</li>
      </ul>
      `,
      buddy: "This is ‘bootcamp prep’ cardio. Picture yourself on the field, moving with the group,
