<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>Find Missing People</title>

<style>
body {
  margin: 0;
  font-family: Arial;
  background: black;
  color: white;
}

header {
  background: linear-gradient(red, black);
  padding: 20px;
  text-align: center;
}

h1 {
  margin: 0;
  font-size: 30px;
}

.container {
  padding: 20px;
  text-align: center;
}

input, textarea, select {
  width: 90%;
  padding: 10px;
  margin: 8px;
  border-radius: 5px;
  border: none;
}

button {
  background: red;
  color: white;
  padding: 10px 20px;
  border: none;
  cursor: pointer;
  border-radius: 5px;
}

.card {
  background: #111;
  border: 1px solid red;
  margin: 15px;
  padding: 15px;
  border-radius: 10px;
}

img {
  max-width: 100%;
  border-radius: 10px;
}

.reward {
  color: yellow;
  font-weight: bold;
}
</style>
</head>

<body>

<header>
  <h1>🔍 FIND MISSING PEOPLE</h1>
  <p>Help reunite families ❤️</p>

  <!-- Language Selector -->
  <select onchange="changeLang(this.value)">
    <option value="en">English</option>
    <option value="hi">Hindi</option>
    <option value="es">Spanish</option>
    <option value="fr">French</option>
  </select>
</header>

<div class="container">

<h2>Report Missing Person</h2>

<form onsubmit="addPerson(event)">
  <input type="text" id="name" placeholder="Name" required>
  <input type="text" id="lastSeen" placeholder="Last Seen Location" required>
  <textarea id="details" placeholder="Details"></textarea>
  <input type="text" id="contact" placeholder="Contact Info" required>
  <input type="number" id="reward" placeholder="Reward Amount (optional)">
  <input type="file" id="photo" accept="image/*">
  <br>
  <button type="submit">Submit</button>
</form>

<h2>Missing People</h2>
<div id="list"></div>

</div>

<script>

// Language texts
const text = {
  en: {
    title: "FIND MISSING PEOPLE"
  },
  hi: {
    title: "गुमशुदा लोगों को खोजें"
  },
  es: {
    title: "Encontrar Personas Desaparecidas"
  },
  fr: {
    title: "Trouver des personnes disparues"
  }
};

function changeLang(lang) {
  document.querySelector("h1").innerText = text[lang].title;
}

// Add person
function addPerson(e) {
  e.preventDefault();

  let name = document.getElementById("name").value;
  let lastSeen = document.getElementById("lastSeen").value;
  let details = document.getElementById("details").value;
  let contact = document.getElementById("contact").value;
  let reward = document.getElementById("reward").value;
  let photo = document.getElementById("photo").files[0];

  let reader = new FileReader();

  reader.onload = function() {
    let card = document.createElement("div");
    card.className = "card";

    card.innerHTML = `
      <img src="${reader.result}">
      <h3>${name}</h3>
      <p><b>Last Seen:</b> ${lastSeen}</p>
      <p>${details}</p>
      <p><b>Contact:</b> ${contact}</p>
      ${reward ? `<p class="reward">Reward: ₹${reward}</p>` : ""}
    `;

    document.getElementById("list").appendChild(card);
  };

  if(photo) {
    reader.readAsDataURL(photo);
  }

  document.querySelector("form").reset();
}

</script>

</body>
</html># Missing-People-