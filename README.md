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
  },
  {
    english: "Kea",
    maori: "Kea",
    facts: [
      "Found in the South Island's alpine regions",
      "Endangered due to predation and human impact",
      "Omnivorous: feeds on plants, insects, and carrion",
      "Known for its curiosity and intelligence"
    ],
    image: "https://upload.wikimedia.org/wikipedia/commons/3/3f/Kea_Parrot.jpg",
    attribution: "CC BY-SA 3.0, Wikimedia Commons"
  },
  {
    english: "Takahe",
    maori: "Takahē",
    facts: [
      "Flightless bird found in alpine grasslands",
      "Once thought extinct, now critically endangered",
      "Herbivorous: feeds on native grasses and herbs",
      "Threatened by habitat loss and introduced predators"
    ],
    image: "https://upload.wikimedia.org/wikipedia/commons/2/2f/Takahe_Parrot.jpg",
    attribution: "CC BY-SA 3.0, Wikimedia Commons"
  },
  {
    english: "Fantail",
    maori: "Pīwakawaka",
    facts: [
      "Small insectivorous bird found throughout New Zealand",
      "Known for its distinctive tail and acrobatic flight",
      "Common in forests, gardens, and parks",
      "Feeds on insects caught mid-air"
    ],
    image: "https://upload.wikimedia.org/wikipedia/commons/2/2a/Fantail_in_New_Zealand.jpg",
    attribution: "CC BY-SA 3.0, Wikimedia Commons"
  },
  {
    english: "Bellbird",
    maori: "Korimako",
    facts: [
      "Native to New Zealand forests",
      "Feeds on nectar, insects, and fruits",
      "Known for its melodious song",
      "Plays a role in pollination"
    ],
    image: "https://upload.wikimedia.org/wikipedia/commons/3/3d/Bellbird_in_New_Zealand.jpg",
    attribution: "CC BY-SA 3.0, Wikimedia Commons"
  },
  {
    english: "Morepork",
    maori: "Ruru",
    facts: [
      "Nocturnal owl found in forests across New Zealand",
      "Feeds on insects, birds, and small mammals",
      "Known for its distinctive 'more-pork' call",
      "Plays a role in controlling insect populations"
    ],
    image: "https://upload.wikimedia.org/wikipedia/commons/4/4f/Morepork_in_New_Zealand.jpg",
    attribution: "CC BY-SA 3.0, Wikimedia Commons"
  },
  {
    english: "Rock Wren",
    maori: "Pīhoihoi",
    facts: [
      "Small, ground-dwelling bird found in alpine regions",
      "Feeds on insects and spiders",
      "Known for its cryptic plumage",
      "Threatened by habitat loss and introduced predators"
    ],
    image: "https://upload.wikimedia.org/wikipedia/commons/5/5f/Rock_Wren_in_New_Zealand.jpg",
    attribution: "CC BY-SA 3.0, Wikimedia Commons"
  },
  {
    english: "Yellow-eyed Penguin",
    maori: "Hoiho",
    facts: [
      "Found on the southeastern coast of New Zealand",
      "One of the rarest and most endangered penguins",
      "Feeds on fish and squid",
      "Threatened by habitat degradation and introduced predators"
    ],
    image: "https://upload.wikimedia.org/wikipedia/commons/3/3e/Yellow-eyed_Penguin_in_New_Zealand.jpg",
    attribution: "CC BY-SA 3.0, Wikimedia Commons"
  },
  {
    english: "Little Blue Penguin",
    maori: "Korora",
    facts: [
      "Smallest species of penguin, found along New Zealand's coastlines",
      "Feeds on fish and squid",
      "Known for its distinctive blue plumage",
      "Threatened by habitat loss and introduced predators"
    ],
    image: "https://upload.wikimedia.org/wikipedia/commons/0/0e/Little_Blue_Penguin_in_New_Zealand.jpg",
    attribution: "CC BY-SA 3.0, Wikimedia Commons"
  },
  {
    english: "Great Crested Grebe",
    maori: "Kāmana",
    facts: [
      "Large water bird found in lakes and wetlands",
      "Feeds on fish and aquatic invertebrates",
      "Known for its elaborate mating display",
      "Plays a role in controlling fish populations"
    ],
    image: "https://upload.wikimedia.org/wikipedia/commons/1/1e/Great_Crested_Grebe_in_New_Zealand.jpg",
    attribution: "CC BY-SA 3.0, Wikimedia Commons"
  },
  {
    english: "Australasian Bittern",
    maori: "Matuku",
    facts: [
      "Large, secretive heron found in wetlands",
      "Feeds on fish, frogs, and insects",
      "Known for its booming call during breeding season",
      "Threatened by habitat loss and introduced predators"
    ],
    image: "https://upload.wikimedia.org/wikipedia/commons/2/2f/Australasian_Bittern_in_New_Zealand.jpg",
    attribution: "CC BY-SA 3.0, Wikimedia Commons"
  },
  {
    english: "South Island Kaka",
    maori: "Kākā",
    facts: [
      "Forest parrot found in the South Island",
      "Feeds on fruits, seeds, and nectar",
      "Known for its playful and inquisitive nature",
      "Threatened by habitat loss and introduced predators"
    ],
    image: "https://upload.wikimedia.org/wikipedia/commons/5/5b/South_Island_Kaka_in_New_Zealand.jpg",
    attribution: "CC BY-SA 3.0, Wikimedia Commons"
  },
  {
    english: "North Island Kaka",
    maori: "Kākā",
    facts: [
      "Forest parrot found in the North Island",
      "Feeds on fruits, seeds, and nectar",
      "Known for its playful and inquisitive nature",
      "Threatened by habitat loss and introduced predators"
    ],
    image: "https://upload.wikimedia.org/wikipedia/commons/7/7d/North_Island_Kaka_in_New_Zealand.jpg",
    attribution: "CC BY-SA 3.0, Wikimedia Commons"
  },
  {
    english: "Shining Cuckoo",
    maori: "Pīpīwharauroa",
    facts: [
      "Migratory bird found in New Zealand during summer",
      "Known for its distinctive 'pīpīwharauroa' call",
      "Feeds on caterpillars and insects",
      "Plays a role in controlling insect populations"
    ],
    image: "https://upload.wikimedia.org/wikipedia/commons/3/3e/Shining_Cuckoo_in_New_Zealand.jpg",
    attribution: "CC BY-SA 3.0, Wikimedia Commons"
  },
  {
    english: "Long-tailed Cuckoo",
    maori: "Pōpokotea",
    facts: [
      "Migratory bird found in New Zealand during summer",
      "Feeds on caterpillars and insects",
      "Known for its distinctive 'pōpokotea' call",
      "Plays a role in controlling insect populations"
    ],
    image: "https://upload.wikimedia.org/wikipedia/commons/4/4e/Long-tailed_Cuckoo_in_New_Zealand.jpg",
    attribution: "CC BY-SA 3.0, Wikimedia Commons"
  },
  {
    english: "White-faced Heron",
    maori: "Ardea novaehollandiae",
    facts: [
      "Large wader found in wetlands and coastal areas",
      "Feeds on fish, frogs, and insects",
      "Known for its graceful flight and hunting technique",
      "Plays a role in controlling fish and insect populations"
    ],
    image: "https://upload.wikimedia.org/wikipedia/commons/4/4e/White-faced_Heron_in_New_Zealand.jpg",
    attribution: "CC BY-SA 3.0, Wikimedia Commons"
  },
  {
    english: "Australasian Shoveler",
    maori: "Anas rhynchotis",
    facts: [
      "Dabbling duck found in wetlands and lakes",
      "Feeds on aquatic plants and invertebrates",
      "Known for its distinctive spatula-shaped bill",
      "Plays a role in controlling aquatic plant populations"
    ],
    image: "https
::contentReference[oaicite:0]{index=0}
 

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
