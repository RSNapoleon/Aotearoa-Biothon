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
  #facts { margin-top: 20px; }
  #streak { margin-top: 20px; font-weight: bold; }
</style>
</head>
<body>

<h1>Aotearoa Animal Challenge</h1>
<div id="game">
  <h2 id="animal-name"></h2>
  <img id="animal-img" src="" alt="Animal Image">
  <div id="options"></div>
  <div id="facts"></div>
  <div id="streak"></div>
</div>

<script>
// ---------------------------
// Species Data (sample for brevity, expand to 100)
// ---------------------------
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
  },
  {
    english: "Kiwi (North Island)",
    maori: "Kiwi",
    facts: [
      "Found in forests across the North Island",
      "Vulnerable due to habitat loss and predators",
      "Omnivorous: eats insects, worms, berries",
      "Threatened by stoats, dogs, and habitat destruction"
    ],
    image: "https://upload.wikimedia.org/wikipedia/commons/6/6b/North_Island_kiwi.jpg",
    attribution: "CC BY-SA 4.0, Wikimedia Commons"
  },
  {
    english: "Tui",
    maori: "Tūī",
    facts: [
      "Found across New Zealand in forests and gardens",
      "Common and not currently threatened",
      "Feeds on nectar, fruits, and insects",
      "Threatened by habitat loss and introduced predators"
    ],
    image: "https://upload.wikimedia.org/wikipedia/commons/1/1a/Tui_in_New_Zealand.jpg",
    attribution: "CC BY 2.0, Wikimedia Commons"
  }
  // ... continue to 100 species
];

// ---------------------------
// Holiday-aware gameDays array
// ---------------------------
const gameDays = [
  "2025-10-06","2025-10-07","2025-10-08","2025-10-09","2025-10-10",
  "2025-10-13","2025-10-14","2025-10-15","2025-10-16","2025-10-17",
  "2025-10-20","2025-10-21","2025-10-22","2025-10-23","2025-10-24",
  "2025-10-28","2025-10-29","2025-10-30","2025-10-31",
  "2025-11-03","2025-11-04","2025-11-05","2025-11-06","2025-11-07",
  "2025-11-10","2025-11-11","2025-11-12","2025-11-13","2025-11-17",
  "2025-11-18","2025-11-19","2025-11-20","2025-11-21",
  "2025-11-24","2025-11-25","2025-11-26","2025-11-27","2025-11-28",
  "2025-12-01","2025-12-02","2025-12-03","2025-12-04","2025-12-05",
  "2025-12-08","2025-12-09","2025-12-10","2025-12-11","2025-12-12"
];

// ---------------------------
// Determine today's animal
// ---------------------------
const todayStr = new Date().toISOString().split('T')[0];
let dayIndex = gameDays.indexOf(todayStr);

const optionsDiv = document.getElementById("options");
const factsDiv = document.getElementById("facts");
const animalName = document.getElementById("animal-name");
const animalImg = document.getElementById("animal-img");
const streakDiv = document.getElementById("streak");

if(dayIndex === -1){
  animalName.textContent = "No animal today – see you tomorrow!";
  animalImg.style.display = "none";
} else {
  const animal = species[dayIndex % species.length];
  animalName.textContent = "Which animal is this?";
  animalImg.src = animal.image;
  animalImg.alt = animal.english;

  // Generate multiple-choice options
  let options = [animal.english];
  while(options.length < 4){
    let randomSpecies = species[Math.floor(Math.random()*species.length)].english;
    if(!options.includes(randomSpecies)) options.push(randomSpecies);
  }
  options.sort(() => Math.random()-0.5); // shuffle

  options.forEach(opt=>{
    const btn = document.createElement("button");
    btn.textContent = opt;
    btn.onclick = () => {
      if(opt === animal.english){
        factsDiv.innerHTML = "<strong>Correct! " + animal.english + " (" + animal.maori + ")</strong><br>" + animal.facts.join("<br>") + "<br><em>" + animal.attribution + "</em>";
        updateStreak();
      } else {
        factsDiv.innerHTML = "<strong>Incorrect! The correct answer is " + animal.english + " (" + animal.maori + ")</strong><br>" + animal.facts.join("<br>") + "<br><em>" + animal.attribution + "</em>";
        updateStreak();
      }
    };
    optionsDiv.appendChild(btn);
  });
}

// ---------------------------
// Streak tracking
// ---------------------------
function updateStreak(){
  let streak = Number(localStorage.getItem('streak')||0) + 1;
  localStorage.setItem('streak', streak);
  streakDiv.textContent = "Your current streak: " + streak;
}
</script>

</body>
</html>
