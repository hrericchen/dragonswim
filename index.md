---
layout: home
---

# Welcome to Dragon Swim Team

Swim Team Registration
<!DOCTYPE html>
<html>
<head>
  <title>Swim Team Registration</title>
</head>
<body>

<h2>Signup Form</h2>

<form id="signupForm">
  <input type="email" id="email" placeholder="Email" required>
  <input type="text" id="name" placeholder="Name">
  <button type="submit">Submit</button>
</form>

<script type="module">
  import { initializeApp } from "https://www.gstatic.com/firebasejs/10.7.1/firebase-app.js";
  import { getFirestore, addDoc, collection } from "https://www.gstatic.com/firebasejs/10.7.1/firebase-firestore.js";

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

  document.getElementById("signupForm").addEventListener("submit", async (e) => {
    e.preventDefault();

    await addDoc(collection(db, "users"), {
      email: email.value,
      name: name.value,
      createdAt: new Date()
    });

    alert("Submitted!");
  });
</script>

</body>
</html>
