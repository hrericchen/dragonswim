<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <title>Dragon Swim Team</title>

  <style>
    /* ===== Global ===== */
    * {
      box-sizing: border-box;
    }

    body {
      margin: 0;
      font-family: Arial, sans-serif;
      background: #f4f8fc;
      color: #222;
      opacity: 0;
    }

    /* ===== Navbar ===== */
    header {
      position: fixed;
      top: 0;
      width: 100%;
      padding: 18px 40px;
      background: #1E90FF;
      display: flex;
      justify-content: space-between;
      align-items: center;
      color: white;
      z-index: 1000;
      transition: box-shadow 0.3s ease;
    }

    header h1 {
      margin: 0;
      font-size: 22px;
      letter-spacing: 1px;
    }

    #loginBtn {
      background: white;
      color: #1E90FF;
      border: none;
      padding: 10px 18px;
      border-radius: 8px;
      font-weight: bold;
      cursor: pointer;
      transition: all 0.2s ease;
    }

    /* ===== Hero ===== */
    .hero {
      height: 90vh;
      background: linear-gradient(to right, #1E90FF, #4facfe);
      color: white;
      display: flex;
      flex-direction: column;
      justify-content: center;
      align-items: center;
      text-align: center;
      padding: 40px;
    }

    .hero h2 {
      font-size: 48px;
      margin-bottom: 15px;
    }

    .hero p {
      font-size: 18px;
      max-width: 600px;
      line-height: 1.5;
    }

    /* ===== Content ===== */
    main {
      padding: 80px 20px;
      max-width: 900px;
      margin: auto;
    }

    .card {
      background: white;
      padding: 30px;
      border-radius: 12px;
      box-shadow: 0 10px 25px rgba(0,0,0,0.08);
      margin-bottom: 40px;
    }

    .card h3 {
      margin-top: 0;
      color: #1E90FF;
    }

    footer {
      text-align: center;
      padding: 30px;
      color: #777;
    }
  </style>
</head>

<body>

  <!-- ===== Navbar ===== -->
  <header id="navbar">
    <h1>Dragon Swim Team</h1>
    <button id="loginBtn">Coach Login</button>
  </header>

  <!-- ===== Hero Section ===== -->
  <section class="hero">
    <h2 id="heroTitle">Welcome to Dragon Swim</h2>
    <p>
      A competitive and supportive swim team focused on excellence,
      teamwork, and personal growth.
    </p>
  </section>

  <!-- ===== Main Content ===== -->
  <main>
    <div class="card">
      <h3>About Our Team</h3>
      <p>
        <!-- ✏️ WRITE ABOUT YOUR TEAM HERE -->
        Dragon Swim Team is dedicated to developing strong swimmers
        through disciplined training, encouragement, and community.
        Our athletes compete at multiple levels while building lifelong
        skills and friendships.
      </p>
    </div>

    <div class="card">
      <h3>Practice & Values</h3>
      <p>
        <!-- ✏️ WRITE MORE HERE -->
        We emphasize technique, consistency, and respect. Coaches
        focus on individual improvement while fostering a team-first
        mindset.
      </p>
    </div>
  </main>

  <footer>
    © 2026 Dragon Swim Team
  </footer>

  <!-- ===== JavaScript ===== -->
  <script>
    // Page fade-in
    window.addEventListener("load", () => {
      document.body.style.transition = "opacity 0.8s ease";
      document.body.style.opacity = 1;
    });

    // Navbar shadow on scroll
    const navbar = document.getElementById("navbar");
    window.addEventListener("scroll", () => {
      navbar.style.boxShadow =
        window.scrollY > 10 ? "0 4px 15px rgba(0,0,0,0.2)" : "none";
    });

    // Login button animation
    const loginBtn = document.getElementById("loginBtn");

    loginBtn.addEventListener("mouseenter", () => {
      loginBtn.style.transform = "scale(1.05)";
    });

    loginBtn.addEventListener("mouseleave", () => {
      loginBtn.style.transform = "scale(1)";
    });

    loginBtn.addEventListener("click", () => {
      // CHANGE THIS when your login page exists
      window.location.href = "login.html";
    });
  </script>

</body>
</html>
