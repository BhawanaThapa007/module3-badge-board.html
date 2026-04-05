<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>Module 3 Badge Board</title>
<style>
  body { font-family:'Segoe UI', Arial, sans-serif; background:#f4f6fb; color:#1e2a38; line-height:1.6; padding:20px; }
  h1 { color:#1565c0; text-align:center; }
  .badge { border:2px solid #1565c0; border-radius:10px; padding:20px; margin:15px 0; background:white; }
  .badge.locked { opacity:0.6; }
  button { background:#1565c0; color:white; border:none; padding:10px 20px; border-radius:25px; cursor:pointer; margin-top:10px; }
  .correct { color:green; font-weight:bold; }
  .incorrect { color:red; font-weight:bold; }
  .completed { background:#d4edda; border-color:#28a745; }
</style>
</head>
<body>

<h1>Module 3: Gamification Strategies</h1>
<p style="text-align:center;">Earn all 4 badges by completing the challenges!</p>

<div id="Explorer" class="badge">
  <h2>Explorer Badge</h2>
  <p>Match 3 game mechanics to their definitions:</p>
  <ul>
    <li>Points → <select data-answer="Points">
      <option value="">Select</option>
      <option value="Points">Reward for actions</option>
      <option value="Wrong">Competitive task</option>
      <option value="Wrong">Visual reward</option>
    </select></li>
    <li>Badges → <select data-answer="Badges">
      <option value="">Select</option>
      <option value="Badges">Visual reward</option>
      <option value="Wrong">Competitive task</option>
      <option value="Wrong">Award points</option>
    </select></li>
    <li>Leaderboards → <select data-answer="Leaderboards">
      <option value="">Select</option>
      <option value="Leaderboards">Display ranking</option>
      <option value="Wrong">Reward for actions</option>
      <option value="Wrong">Visual reward</option>
    </select></li>
  </ul>
  <button onclick="checkBadge('Explorer')">Check Answers</button>
  <p id="ExplorerFeedback"></p>
</div>

<div id="Analyst" class="badge">
  <h2>Analyst Badge</h2>
  <p>True/False: Mechanics work in certain conditions. Select all correct:</p>
  <label><input type="checkbox" data-answer="true"> Badges motivate when visible ✅</label><br>
  <label><input type="checkbox" data-answer="false"> Points always motivate all students ❌</label><br>
  <label><input type="checkbox" data-answer="true"> Challenges work with achievable goals ✅</label><br>
  <button onclick="checkBadge('Analyst')">Check Answers</button>
  <p id="AnalystFeedback"></p>
</div>

<div id="Strategist" class="badge">
  <h2>Strategist Badge</h2>
  <p>Pick the right mechanic for 3 classroom goals:</p>
  <ul>
    <li>Increase participation → 
      <select data-answer="Points">
        <option value="">Select</option>
        <option value="Points">Points</option>
        <option value="Badges">Badges</option>
        <option value="Wrong">None</option>
      </select></li>
    <li>Encourage mastery → 
      <select data-answer="Challenge">
        <option value="">Select</option>
        <option value="Challenge">Challenge</option>
        <option value="Badges">Badges</option>
        <option value="Wrong">None</option>
      </select></li>
    <li>Foster friendly competition → 
      <select data-answer="Leaderboards">
        <option value="">Select</option>
        <option value="Leaderboards">Leaderboards</option>
        <option value="Points">Points</option>
        <option value="Wrong">None</option>
      </select></li>
  </ul>
  <button onclick="checkBadge('Strategist')">Check Answers</button>
  <p id="StrategistFeedback"></p>
</div>

<div id="Designer" class="badge">
  <h2>Designer Badge</h2>
  <p>Choose exactly 2 mechanics for a classroom scenario (check 2 boxes):</p>
  <label><input type="checkbox" data-answer="Points"> Points</label><br>
  <label><input type="checkbox" data-answer="Challenge"> Challenge</label><br>
  <label><input type="checkbox" data-answer="Leaderboards"> Leaderboards</label><br>
  <label><input type="checkbox" data-answer="Badges"> Badges</label><br>
  <button onclick="checkBadge('Designer')">Check Answers</button>
  <p id="DesignerFeedback"></p>
</div>

<p id="completion" style="text-align:center; font-weight:bold; font-size:18px; color:#1565c0;"></p>

<script>
function checkBadge(badgeId) {
  const badge = document.getElementById(badgeId);
  const feedback = document.getElementById(badgeId + 'Feedback');
  let correct = true;

  if(badgeId === 'Explorer' || badgeId === 'Strategist') {
    const selects = badge.querySelectorAll('select');
    selects.forEach(s => { if(s.value !== s.getAttribute('data-answer')) correct = false; });
  } else if(badgeId === 'Analyst') {
    const checkboxes = badge.querySelectorAll('input[type="checkbox"]');
    checkboxes.forEach(cb => {
      const isChecked = cb.checked;
      const answer = cb.getAttribute('data-answer') === 'true';
      if(isChecked !== answer) correct = false;
    });
  } else if(badgeId === 'Designer') {
    const checkboxes = badge.querySelectorAll('input[type="checkbox"]');
    let count = 0;
    let selectedCorrect = 0;
    checkboxes.forEach(cb => {
      if(cb.checked) count++;
      if(cb.checked && (cb.getAttribute('data-answer')==='Points' || cb.getAttribute('data-answer')==='Challenge')) selectedCorrect++;
    });
    if(count !== 2 || selectedCorrect !== 2) correct = false;
  }

  if(correct) {
    badge.classList.add('completed');
    feedback.innerHTML = '<span class="correct">✅ Badge Earned!</span>';
  } else { feedback.innerHTML = '<span class="incorrect">❌ Try Again!</span>'; }

  checkCompletion();
}

function checkCompletion() {
  const badges = ['Explorer','Analyst','Strategist','Designer'];
  const allDone = badges.every(id => document.getElementById(id).classList.contains('completed'));
  if(allDone) document.getElementById('completion').innerText = '🎉 Congratulations! You earned all 4 badges!';
}
</script>

</body>
</html>
