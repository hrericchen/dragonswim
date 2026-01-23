<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<title>Dragon Swim Team</title>
<style>
  body {
    font-family: Arial, sans-serif;
    margin: 0;
    padding: 0;
    background: linear-gradient(to bottom, #f0f8ff, #d0e7ff);
  }

  header {
    background: #1E90FF;
    color: white;
    padding: 20px 40px;
    display: flex;
    justify-content: space-between;
    align-items: center;
  }

  header h1 {
    margin: 0;
    font-size: 28px;
  }

  header button {
    padding: 10px 20px;
    font-size: 16px;
    border: none;
    border-radius: 5px;
    cursor: pointer;
    background: white;
    color: #1E90FF;
    font-weight: bold;
  }

  main {
    text-align: center;
    padding: 60px 20px;
    max-width: 800px;
    margin: auto;
  }

  main h2 {
    font-size: 32px;
    margin-bottom: 20px;
  }

  main p {
    font-size: 18px;
    color: #333;
    line-height: 1.6;
  }

  #loginArea {
    display: none;
    background: #fff;
    padding: 30px 20px;
    margin-top: 20px;
    border-radius: 10px;
    box-shadow: 0px 0px 15px #aaa;
    max-width: 400px;
    margin-left: auto;
    margin-right: auto;
  }

  input {
    display: block;
    width: 90%;
    padding: 10px;
    margin: 10px auto;
    font-size: 16px;
  }

  #loginArea button {
    width: 45%;
    margin: 10px 2.5%;
    background: #1E90FF;
    color: white;
    font-weight: bold;
  }

  #message {
    margin-top: 10px;
    color: red;
  }
</style>
</head>
<body>

<header>
  <h1>Dragon Swim Team</h1>
  <button id="showLoginBtn">Login</button>
</header>

<main>
  <h2>Welcome to Dragon Swim Team</h2>
  <p>
    This is the portal for our swim team members and coaches.  
    Coaches can log in to view and manage swimmer signups.  
    Families can use the signup form to register their swimmers.  
  </p>

  <div id="loginArea">
    <h3>Coach Login / Register</h3>
    <input type="email" id="email" placeholder="Email">
    <input type="password" id="password" placeholder="Password">
    <button id="loginBtn">Login</button>
    <button id="registerBtn">Register</button>
    <p id="message"></p>
  </div>
</main>

<script type="module">
import { initializeApp } from "https://www.gstatic.com/firebasejs/10.7.1/firebase-app.js";
import { getAuth, signInWithEmailAndPassword, createUserWithEmailAndPassword, onAuthStateChanged } from "https://www.gstatic.com/firebasejs/10.7.1/firebase-auth.js";

// ===== Replace with your Firebase config =====
 const firebaseConfig = {
    apiKey: "AIzaSyCCvxJPxLgmMvMW0DJpy44C5p2ACbLqf1E",
    authDomain: "dragon-swim.firebaseapp.com",
    projectId: "dragon-swim",
    storageBucket: "dragon-swim.firebasestorage.app",
    messagingSenderId: "353938946053",
    appId: "1:353938946053:web:1fbdf6b4a508392e6b046c"
  };

const app = initializeApp(firebaseConfig);
const auth = getAuth(app);

const showLoginBtn = document.getElementById("showLoginBtn");
const loginArea = document.getElementById("loginArea");
showLoginBtn.addEventListener("click", () => {
  loginArea.style.display = loginArea.style.display === "none" ? "block" : "none";
});

const loginBtn = document.getElementById("loginBtn");
const registerBtn = document.getElementById("registerBtn");
const message = document.getElementById("message");
const emailInput = document.getElementById("email");
const passwordInput = document.getElementById("password");

// Login
loginBtn.addEventListener("click", async () => {
  const email = emailInput.value;
  const password = passwordInput.value;
  message.textContent = "";

  try {
    await signInWithEmailAndPassword(auth, email, password);
    window.location.href = "dashboard.html"; // Redirect to dashboard
  } catch (err) {
    console.error(err);
    message.textContent = "Login failed: " + err.message;
  }
});

// Register
registerBtn.addEventListener("click", async () => {
  const email = emailInput.value;
  const password = passwordInput.value;
  message.textContent = "";

  try {
    await createUserWithEmailAndPassword(auth, email, password);
    message.style.color = "green";
    message.textContent = "Successful Registration! You can now login.";
    emailInput.value = "";
    passwordInput.value = "";
  } catch (err) {
    console.error(err);
    message.style.color = "red";
    message.textContent = "Registration failed: " + err.message;
  }
});

// Auto redirect if already logged in
onAuthStateChanged(auth, (user) => {
  if (user) {
    window.location.href = "dashboard.html";
  }
});
</script>

</body>
</html>

<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<title>Coach Dashboard - Dragon Swim Team</title>
<style>
  body { font-family: Arial, sans-serif; padding: 20px; background: #f0f8ff; }
  header { display: flex; justify-content: space-between; align-items: center; background: #1E90FF; color: white; padding: 20px; }
  header h1 { margin: 0; }
  header button { padding: 10px 20px; border: none; border-radius: 5px; cursor: pointer; background: white; color: #1E90FF; font-weight: bold; }
  table { width: 100%; border-collapse: collapse; margin-top: 20px; }
  th, td { border: 1px solid #ccc; padding: 8px; text-align: left; }
  th { background: #1E90FF; color: white; }
</style>
</head>
<body>

<header>
  <h1>Coach Dashboard</h1>
  <button id="logoutBtn">Logout</button>
</header>

<h2>Dragon Swim Signups</h2>
<table>
  <thead>
    <tr><th>Name</th><th>Email</th><th>Signup Date</th></tr>
  </thead>
  <tbody id="signupTable"></tbody>
</table>

<script type="module">
import { initializeApp } from "https://www.gstatic.com/firebasejs/10.7.1/firebase-app.js";
import { getFirestore, collection, getDocs, query, orderBy } from "https://www.gstatic.com/firebasejs/10.7.1/firebase-firestore.js";
import { getAuth, onAuthStateChanged, signOut } from "https://www.gstatic.com/firebasejs/10.7.1/firebase-auth.js";

// ===== Replace with your Firebase config =====
 const firebaseConfig = {
    apiKey: "AIzaSyCCvxJPxLgmMvMW0DJpy44C5p2ACbLqf1E",
    authDomain: "dragon-swim.firebaseapp.com",
    projectId: "dragon-swim",
    storageBucket: "dragon-swim.firebasestorage.app",
    messagingSenderId: "353938946053",
    appId: "1:353938946053:web:1fbdf6b4a508392e6b046c"
  };;

const app = initializeApp(firebaseConfig);
const db = getFirestore(app);
const auth = get
