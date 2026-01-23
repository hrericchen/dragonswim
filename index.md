---
layout: home
---

# Welcome to Dragon Swim Team

</body>
</html>
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <title>Dragon Swim Team Signup</title>
  <style>
    body { font-family: Arial; padding: 40px; max-width: 500px; margin: auto; }
    input, button { display: block; width: 100%; padding: 10px; margin: 10px 0; font-size: 16px; }
    button { cursor: pointer; background: #1E90FF; color: white; border: none; border-radius: 5px; }
  </style>
</head>
<body>

<h2>Dragon Swim Team Signup</h2>

<form id="signupForm">
  <input type="email" id="email" placeholder="Email" required>
  <input type="text" id="name" placeholder="Full Name" required>
  <button type="submit">Submit</button>
</form>

<p id="message"></p>

<!-- Firebase Scripts -->
<script type="module">
import { initializeApp } from "https://www.gstatic.com/firebasejs/10.7.1/firebase-app.js";
import { getFirestore, addDoc, collection } from "https://www.gstatic.com/firebasejs/10.7.1/firebase-firestore.js";

// ===== Replace this with YOUR Firebase config =====
 const firebaseConfig = {
    apiKey: "AIzaSyCCvxJPxLgmMvMW0DJpy44C5p2ACbLqf1E",
    authDomain: "dragon-swim.firebaseapp.com",
    projectId: "dragon-swim",
    storageBucket: "dragon-swim.firebasestorage.app",
    messagingSenderId: "353938946053",
    appId: "1:353938946053:web:1fbdf6b4a508392e6b046c"
  };

const app = initializeApp(firebaseConfig);
const db = getFirestore(app);

// Form submission
const form = document.getElementById("signupForm");
const message = document.getElementById("message");

form.addEventListener("submit", async (e) => {
  e.preventDefault();

  const emailValue = document.getElementById("email").value;
  const nameValue = document.getElementById("name").value;

  // Debug
  console.log("Email:", emailValue);
  console.log("Name:", nameValue);

  if (!emailValue || !nameValue) {
    message.textContent = "Please fill in all fields!";
    return;
  }

  try {
    await addDoc(collection(db, "users"), {
      email: emailValue,
      name: nameValue,
      createdAt: new Date()
    });

    message.textContent = "Thanks! Your signup has been recorded.";
    form.reset();

  } catch (err) {
    console.error(err);
    message.textContent = "Error submitting data. Check console.";
  }
});
</script>

</body>
</html>

<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <title>Coach Admin Page</title>
  <style>
    body { font-family: Arial; padding: 40px; max-width: 700px; margin: auto; }
    input, button { display: block; width: 100%; padding: 10px; margin: 10px 0; font-size: 16px; }
    button { cursor: pointer; background: #1E90FF; color: white; border: none; border-radius: 5px; }
    table { width: 100%; border-collapse: collapse; margin-top: 20px; }
    th, td { border: 1px solid #ccc; padding: 8px; text-align: left; }
  </style>
</head>
<body>

<h2>Coach Login</h2>

<div id="loginDiv">
  <input type="email" id="loginEmail" placeholder="Email">
  <input type="password" id="loginPassword" placeholder="Password">
  <button id="loginBtn">Login</button>
  <p
