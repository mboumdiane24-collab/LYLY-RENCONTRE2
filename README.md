<!DOCTYPE html>
<html lang="fr">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>LYLY RENCONTRE</title>

<style>
body {
    font-family: Arial, sans-serif;
    background: #fff0f5;
    margin: 0;
}

header {
    background: #ff4d88;
    color: white;
    padding: 20px;
    text-align: center;
}

.container {
    padding: 15px;
    max-width: 500px;
    margin: auto;
}

input, select {
    width: 100%;
    padding: 12px;
    margin: 6px 0;
    border: 1px solid #ddd;
    border-radius: 5px;
}

button {
    background: #ff4d88;
    color: white;
    padding: 12px;
    border: none;
    width: 100%;
    margin-top: 10px;
    border-radius: 5px;
}

.profile {
    background: white;
    padding: 12px;
    margin: 10px 0;
    border-radius: 10px;
    box-shadow: 0 2px 5px rgba(0,0,0,0.1);
}

.vip {
    color: green;
    font-weight: bold;
}

.lock {
    color: red;
    font-weight: bold;
}

.notice {
    background: #fff3cd;
    padding: 15px;
    margin: 15px 0;
    border-radius: 10px;
    text-align: center;
}
</style>
</head>

<body>

<header>
<h1>💕 LYLY RENCONTRE</h1>
<p>Trouve l’amour près de toi</p>
</header>

<div class="container">

<div class="notice">
<h3>⚠️ Frais d'inscription</h3>
<p><strong>25 000 FCFA</strong> / 1 mois</p>
<p>Paiement via WhatsApp pour activation</p>
</div>

<h2>Inscription</h2>

<input id="name" placeholder="Prénom">
<input id="age" placeholder="Âge">
<input id="city" placeholder="Ville">
<input id="whatsapp" placeholder="WhatsApp (ex: 690123456)">
<select id="gender">
<option>Homme</option>
<option>Femme</option>
</select>

<button onclick="register()">S'inscrire</button>

<h2>Membres</h2>
<div id="profiles"></div>

</div>

<script>

let users = JSON.parse(localStorage.getItem("users")) || [];

function save(){
    localStorage.setItem("users", JSON.stringify(users));
}

function register(){

    if(!name.value || !age.value || !city.value || !whatsapp.value){
        alert("Remplis tous les champs");
        return;
    }

    let user = {
        name: name.value,
        age: age.value,
        city: city.value,
        whatsapp: whatsapp.value,
        gender: gender.value,
        vip: false
    };

    users.push(user);
    save();
    displayUsers();

    alert("Inscription envoyée !");
}

function displayUsers(){

    let container = document.getElementById("profiles");
    container.innerHTML = "";

    users.forEach((user, index)=>{

        let div = document.createElement("div");
        div.className = "profile";

        div.innerHTML = `
        <h3>${user.name}, ${user.age}</h3>
        <p>${user.city}</p>

        ${
            user.vip
            ? `<span class="vip">✅ VIP</span><br>
               <a href="https://wa.me/237${user.whatsapp}">
               <button>Contacter</button></a>`
            : `<span class="lock">🔒 Profil verrouillé</span><br>
               <button onclick="pay(${index})">Payer 25 000 FCFA</button>`
        }
        `;

        container.appendChild(div);
    });
}

function pay(index){

    let msg = "Bonjour, je veux payer les frais d'inscription de 25 000 FCFA pour LYLY RENCONTRE.";

    window.open("https://wa.me/15793837250?text=" + encodeURIComponent(msg));

    let confirmPay = confirm("Paiement effectué ?");

    if(confirmPay){
        users[index].vip = true;
        save();
        displayUsers();
        alert("Compte activé !");
    }
}

displayUsers();

</script>

</body>
</html>
