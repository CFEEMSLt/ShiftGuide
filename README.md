<!DOCTYPE html>
<html lang="en">
<head>
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>C-Spine Decision Tool</title>

<style>
  body {
    font-family: -apple-system, BlinkMacSystemFont, "Segoe UI", Roboto, Arial, sans-serif;
    background: #f5f7fa;
    margin: 0;
    padding: 16px;
  }

  .container {
    max-width: 500px;
    margin: auto;
  }

  .banner {
    display: none;
    background: #c62828;
    color: #fff;
    font-size: 22px;
    font-weight: 700;
    text-align: center;
    padding: 14px;
    border-radius: 10px;
    margin-bottom: 20px;
  }

  .card {
    background: #fff;
    border-radius: 16px;
    padding: 24px;
    box-shadow: 0 10px 30px rgba(0,0,0,0.08);
    text-align: center;
  }

  .question {
    font-size: 20px;
    font-weight: 600;
    margin-bottom: 24px;
  }

  .buttons {
    display: flex;
    gap: 16px;
  }

  .btn {
    flex: 1;
    padding: 16px;
    font-size: 18px;
    border-radius: 12px;
    border: none;
    cursor: pointer;
    font-weight: 600;
  }

  .yes {
    background: #c62828;
    color: white;
  }

  .no {
    background: #2e7d32;
    color: white;
  }

  .progress {
    margin-top: 16px;
    font-size: 14px;
    color: #666;
  }

  .done {
    font-size: 20px;
    font-weight: 700;
    color: #2e7d32;
  }
</style>
</head>

<body>

<div class="container">

  <div id="warning" class="banner">
    ⚠️ COLLAR REQUIRED
  </div>

  <div class="card">
    <div id="question" class="question"></div>

    <div class="buttons">
      <button class="btn yes" onclick="answer(true)">Yes</button>
      <button class="btn no" onclick="answer(false)">No</button>
    </div>

    <div id="progress" class="progress"></div>
  </div>

</div>

<script>
const questions = [
  "High risk or questionable spinal injury mechanism?",
  "Patient age greater than 65 or less than 3 years old?",
  "Patient incompetent to participate in the exam?",
  "Midline spinal pain or tenderness with palpation?",
  "Abnormal (not baseline) neurologic function or motor strength?",
  "Numbness or tingling (paresthesia)?",
  "Sensation diminished and/or asymmetrical?",
  "Cervical rotation to 45° or flexion/extension elicits midline pain?"
];

let index = 0;
let smrRequired = false;

function render() {
  if (index < questions.length) {
    document.getElementById("question").textContent = questions[index];
    document.getElementById("progress").textContent =
      `Question ${index + 1} of ${questions.length}`;
  } else {
    document.querySelector(".buttons").style.display = "none";

    if (smrRequired) {
      document.getElementById("question").innerHTML =
        "Assessment Complete";
    } else {
      document.getElementById("warning").style.display = "none";
      document.getElementById("question").innerHTML =
        "<span class='done'>Spinal Motion Restriction NOT Required<br><small>(Per CT OEMS)</small></span>";
    }

    document.getElementById("progress").textContent = "";
  }
}

function answer(isYes) {
  if (isYes) {
    smrRequired = true;
    document.getElementById("warning").style.display = "block";
  }
  index++;
  render();
}

render();
</script>

</body>
</html>
