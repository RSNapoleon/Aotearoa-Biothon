# Aotearoa-Biothon
Learn 100 native New Zealand birds, animals, insects and more. 
<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>Aotearoa Animal Challenge</title>
<style>
  body { font-family: sans-serif; text-align: center; margin: 20px; }
  img { max-width: 300px; margin: 20px 0; }
  button { display: block; margin: 10px auto; padding: 10px 20px; font-size: 16px; }
</style>
</head>
<body>

<h1>Aotearoa Animal Challenge</h1>
<div id="game">
  <h2 id="animal-name"></h2>
  <img id="animal-img" src="" alt="Animal Image">
  <div id="options"></div>
  <div id="facts" style="margin-top:20px;"></div>
  <div id="streak" style="margin-top:20px;"></div>
</div>

<script>
const species = [
  {
    english: "Kākāpō",
    maori: "Kākāpō",
    facts: [
      "Found on predator-free islands like Whenua Hou and Anchor Island",
      "Critically endangered with fewer than 250 individuals remaining",
      "Herbivorous: feeds on native plants, fruits, and seeds",
      "Threatened by introduced predators and habitat loss"
    ],
    image: "https://upload.wikimedia.org/wikipedia/commons/0/0b/Kakapo_Parrot.jpg",
    attribution: "CC BY-SA 3.0, Wikimedia Commons"
  }
];

// Daily locking logic
const startDate = new Date("2025-10-05"); // Adjust start date
const today = new Date();
const dayIndex = Math.floor((today - startDate) / (1000*60*60*24)) % species.length;

const animal = species[dayIndex];
document.getElementById("animal-name").textContent = "Which animal is this?";
document.getElementById("animal-img").src = animal.image;

const optionsDiv = document.getElementById("options");
const options = [animal.english, "Wrong 1", "Wrong 2", "Wrong 3"].sort(() => Math.random()-0.5);
options.forEach(opt => {
  const btn = document.createElement("button");
  btn.textContent = opt;
  btn.onclick = () => {
    let factsDiv = document.getElementById("facts");
    if(opt === animal.english){
      factsDiv.innerHTML = "<strong>Correct! " + animal.english + " (" + animal.maori + ")</strong><br>" + animal.facts.join("<br>") + "<br><em>" + animal.attribution + "</em>";
    } else {
      factsDiv.innerHTML = "<strong>Incorrect! The correct answer is " + animal.english + " (" + animal.maori + ")</strong><br>" + animal.facts.join("<br>") + "<br><em>" + animal.attribution + "</em>";
    }
    updateStreak();
  };
  optionsDiv.appendChild(btn);
});

function updateStreak(){
  let streak = Number(localStorage.getItem('streak')||0) + 1;
  localStorage.setItem('streak', streak);
  document.getElementById("streak").textContent = "Your current streak: " + streak;
}
</script>

</body>
</html>
