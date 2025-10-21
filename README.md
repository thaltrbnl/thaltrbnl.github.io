<!doctype html>
<html lang="en">
<head>
  <meta charset="utf-8" />
  <meta name="viewport" content="width=device-width,initial-scale=1" />
  <title>ICCT Colleges — Student Portal</title>
  <meta name="description" content="ICCT Colleges Student Information System" />
  <style>
    :root {
      --blue: #003399;
      --red: #cc0000;
      --white: #ffffff;
      --bg: #f5f7fb;
      --muted: #6b7280;
      --shadow: 0 6px 20px rgba(0,0,0,0.08);
    }
    [data-theme="dark"] {
      --bg: #101827;
      --white: #1f2937;
      --muted: #9aa4b2;
      --blue: #0059ff;
    }

    body {
      margin: 0;
      font-family: "Poppins", sans-serif;
      background: var(--bg);
      color: var(--blue);
    }

    header {
      display: flex;
      align-items: center;
      background: var(--blue);
      color: white;
      padding: 12px 24px;
    }
    .logo {
      display: flex;
      align-items: center;
      gap: 10px;
    }
    .logo-img {
      width: 50px;
      height: 50px;
    }
    .searchbar {
      margin-left: auto;
      display: flex;
      align-items: center;
      gap: 8px;
    }
    .searchbar input {
      padding: 8px 12px;
      border-radius: 8px;
      border: none;
      outline: none;
      width: 250px;
    }
    .top-actions {
      display: flex;
      gap: 10px;
    }
    .avatar {
      width: 36px;
      height: 36px;
      border-radius: 50%;
    }

    .app {
      display: grid;
      grid-template-columns: 240px 1fr;
      min-height: calc(100vh - 70px);
    }
    .sidebar {
      background: #e6ebfa;
      padding: 20px;
    }
    .nav-link {
      display: block;
      padding: 10px;
      border-radius: 6px;
      color: var(--blue);
      text-decoration: none;
    }
    .nav-link:hover {
      background: var(--blue);
      color: white;
    }
    .logout {
      color: var(--red);
    }

    main {
      padding: 24px;
    }
    .card {
      background: var(--white);
      border-radius: 12px;
      padding: 16px;
      box-shadow: var(--shadow);
    }
    .grid {
      display: grid;
      gap: 16px;
    }
    .cols-3 {
      grid-template-columns: repeat(3, 1fr);
    }
    .courses {
      display: grid;
      grid-template-columns: repeat(auto-fit, minmax(220px, 1fr));
      gap: 10px;
    }
    .course {
      background: #eef2ff;
      padding: 12px;
      border-radius: 10px;
    }
    .primary {
      background: var(--blue);
      color: white;
      border: none;
      padding: 8px 12px;
      border-radius: 6px;
      cursor: pointer;
    }
    .outline {
      border: 1px solid var(--blue);
      background: transparent;
      color: var(--blue);
      padding: 8px 12px;
      border-radius: 6px;
      cursor: pointer;
    }
    .modal-backdrop {
      position: fixed;
      inset: 0;
      background: rgba(0,0,0,0.4);
      display: none;
      justify-content: center;
      align-items: center;
    }
    .modal {
      background: var(--white);
      padding: 20px;
      border-radius: 10px;
      max-width: 600px;
      width: 90%;
    }
    footer {
      text-align: center;
      margin-top: 20px;
      color: var(--muted);
    }

    @media (max-width: 900px) {
      .app {
        grid-template-columns: 1fr;
      }
      .sidebar {
        display: none;
      }
    }
  </style>
</head>

<body>
  <header>
    <div class="logo">
      <img src="icct-logo.png" alt="ICCT Logo" class="logo-img">
      <div>
        <h1>ICCT Colleges</h1>
        <p>Student Information System</p>
      </div>
    </div>

    <div class="searchbar">
      <input id="search" placeholder="Search subjects, announcements..." />
      <div class="top-actions">
        <button class="btn" id="notifBtn" title="Notifications">🔔</button>
        <button class="btn" id="themeToggle" title="Toggle theme">🌓</button>
        <img src="https://ui-avatars.com/api/?name=JN&background=f4b41a&color=000" class="avatar" alt="Student Avatar">
      </div>
    </div>
  </header>

  <div class="app">
    <nav class="sidebar">
      <a class="nav-link" href="#" data-target="dashboard">🏠 Dashboard</a>
      <a class="nav-link" href="#" data-target="subjects">📘 My Subjects</a>
      <a class="nav-link" href="#" data-target="assignments">🧾 Assignments</a>
      <a class="nav-link" href="#" data-target="grades">📊 Grades</a>
      <a class="nav-link" href="#" data-target="billing">💳 Billing</a>
      <a class="nav-link" href="#" data-target="announcements">📢 Announcements</a>
      <a class="nav-link" href="#" data-target="profile">👤 Profile</a>
      <a class="nav-link logout" href="#" id="logoutBtn">⏻ Logout</a>
    </nav>

    <main>
      <section id="dashboard" class="page">
        <div class="card welcome">
          <div>
            <h2>Welcome, Johlan Natalie!</h2>
            <p class="muted">3rd Year • BS Information Technology — 1st Semester 2025</p>
          </div>
        </div>

        <div class="grid cols-3">
          <div class="card">
            <h3>My Subjects</h3>
            <div id="subjectList" class="courses"></div>
          </div>

          <div class="card">
            <h3>Upcoming Deadlines</h3>
            <table id="deadlines">
              <thead><tr><th>Task</th><th>Due</th><th>Status</th></tr></thead>
              <tbody></tbody>
            </table>
          </div>

          <div class="card">
            <h3>Quick Links</h3>
            <button class="outline" data-target="assignments">Submit Assignment</button>
            <button class="outline" data-target="billing">View Billing</button>
          </div>
        </div>
      </section>

      <section id="subjects" class="page" style="display:none">
        <div class="card">
          <h3>Subjects</h3>
          <div id="subjectDetails" class="courses"></div>
        </div>
      </section>

      <section id="assignments" class="page" style="display:none">
        <div class="card">
          <h3>Assignments</h3>
          <table>
            <thead><tr><th>Title</th><th>Subject</th><th>Due</th><th>Action</th></tr></thead>
            <tbody id="assignTable"></tbody>
          </table>
        </div>
      </section>

      <section id="grades" class="page" style="display:none">
        <div class="card">
          <h3>Grades</h3>
          <table id="gradesTable"></table>
        </div>
      </section>

      <section id="billing" class="page" style="display:none">
        <div class="card">
          <h3>Billing & Payments</h3>
          <p class="muted">Outstanding Balance: <strong>₱ 12,350.00</strong></p>
          <button class="primary" id="payNow">Pay Now</button>
        </div>
      </section>

      <section id="announcements" class="page" style="display:none">
        <div class="card">
          <h3>Announcements</h3>
          <ul id="annList"></ul>
        </div>
      </section>

      <section id="profile" class="page" style="display:none">
        <div class="card">
          <h3>Profile</h3>
          <p>Name: Johlan Natalie T. Tabornal</p>
          <p>Email: johlannatalie@gmail.com</p>
          <p>Course: BSIT</p>
        </div>
      </section>

      <footer>© 2025 ICCT Colleges — Student Portal</footer>
    </main>
  </div>

  <div id="modalBackdrop" class="modal-backdrop">
    <div class="modal card" id="modalContent"></div>
  </div>

  <script>
    const subjects = [
      { code: "OLSDF04", title: "Object-Oriented Programming (3/1)", instructor: "Mr. Chiong" },
      { code: "OLIM2", title: "Advance Database System (3/1)", instructor: "Mr. Chiong" },
      { code: "OLSIA1", title: "Systems Integration and Architecture 1 (3/1)", instructor: "Mr. Chiong" },
      { code: "OLSP2", title: "Social and Professional Issues 2", instructor: "Mr. Chiong" },
      
    ];

    const assignments = [
      { title: "Project 1", subject: "Systems Integration and Architecture 1 (3/1)", due: "2025-11-02", status: "Pending" },
      { title: "Quiz 2", subject: "Advance Database System (3/1)", due: "2025-10-28", status: "Submitted" },
    ];

    const announcements = [
      "Midterm schedule has been released!",
      "Library hours extended during finals week.",
    ];

    document.querySelectorAll("[data-target]").forEach((btn) => {
      btn.addEventListener("click", (e) => {
        e.preventDefault();
        const page = btn.getAttribute("data-target");
        document.querySelectorAll(".page").forEach((p) => (p.style.display = "none"));
        document.getElementById(page).style.display = "block";
      });
    });

    const subjectList = document.getElementById("subjectList");
    const subjectDetails = document.getElementById("subjectDetails");
    subjects.forEach((s) => {
      const div = document.createElement("div");
      div.className = "course";
      div.innerHTML = `<h4>${s.code} - ${s.title}</h4><p>${s.instructor}</p>`;
      subjectList.appendChild(div);
      subjectDetails.appendChild(div.cloneNode(true));
    });

    const assignTable = document.getElementById("assignTable");
    assignments.forEach((a) => {
      const tr = document.createElement("tr");
      tr.innerHTML = `<td>${a.title}</td><td>${a.subject}</td><td>${a.due}</td><td><button class='primary'>Submit</button></td>`;
      assignTable.appendChild(tr);
    });

    const annList = document.getElementById("annList");
    announcements.forEach((a) => {
      const li = document.createElement("li");
      li.textContent = a;
      annList.appendChild(li);
    });

    const gradesTable = document.getElementById("gradesTable");
    gradesTable.innerHTML = `
    <thead><tr><th>Subject</th><th>Grade</th></tr></thead>
    <tbody>
      <tr><td>Social and Professional Issues 2
</td><td>1.25</td></tr>
      <tr><td>Advance Database System (3/1)</td><td>1.75</td></tr>
      <tr><td>Object-Oriented Programming (3/1)</td><td>2.00</td></tr>
      <tr><td>Systems Integration and Architecture 1 (3/1)</td><td>2.00</td></tr>
      
    </tbody>`;

    const modalBackdrop = document.getElementById("modalBackdrop");
    const modalContent = document.getElementById("modalContent");
    function showModal(html) {
      modalContent.innerHTML = html + `<div style="text-align:right;margin-top:12px"><button class="outline" onclick="closeModal()">Close</button></div>`;
      modalBackdrop.style.display = "flex";
    }
    function closeModal() {
      modalBackdrop.style.display = "none";
    }

    document.getElementById("payNow").addEventListener("click", () => {
      showModal("<h3>Payment Options</h3><p>Select a payment method (demo only)</p>");
    });

    document.getElementById("search").addEventListener("input", (e) => {
      const q = e.target.value.toLowerCase();
      document.querySelectorAll(".course").forEach((card) => {
        card.style.display = card.innerText.toLowerCase().includes(q) ? "block" : "none";
      });
    });

    document.getElementById("notifBtn").addEventListener("click", () => {
      showModal("<h3>Notifications</h3><ul><li>Assignment due soon!</li><li>Tuition posted.</li></ul>");
    });

    const themeToggle = document.getElementById("themeToggle");
    themeToggle.addEventListener("click", () => {
      const isDark = document.documentElement.getAttribute("data-theme") === "dark";
      if (isDark) document.documentElement.removeAttribute("data-theme");
      else document.documentElement.setAttribute("data-theme", "dark");
    });
  </script>
</body>
</html>
