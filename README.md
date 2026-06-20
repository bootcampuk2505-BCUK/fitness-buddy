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
    ul { margin:0.3rem 0 0.6rem 1rem; padding:0; font-size:0.9rem; }
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
  <div class="subtitle">Daily guidance for training & nutrition based on your 28‑Day Body Transformation Blueprint.</div>

  <div class="card">
    <div class="controls">
      <button id="prevBtn" class="secondary">◀ Previous</button>
      <div>
        <div class=
