<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0" />
  <title>MedCare - Hospital Management System</title>
  <style>
    :root {
      --primary: #0066cc;
      --primary-dark: #004499;
      --secondary: #00cc99;
      --danger: #ff3333;
      --warning: #ff9900;
      --success: #00cc66;
      --bg: #f5f9fc;
      --card: #ffffff;
      --text: #1a1a1a;
      --text-light: #666666;
      --border: #e0e0e0;
      --shadow: 0 2px 10px rgba(0, 0, 0, 0.1);
    }

    *  {
      margin: 0;
      padding: 0;
      box-sizing: border-box;
    }

    html { scroll-behavior: smooth; }

    body {
      font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
      background: var(--bg);
      color: var(--text);
      line-height: 1.6;
    }

    a { text-decoration: none; color: inherit; }
    img { max-width: 100%; }

    .container {
      width: min(1200px, 95vw);
      margin: 0 auto;
    }

    /* ===== AUTH PAGE ===== */
    .auth-container {
      min-height: 100vh;
      display: flex;
      align-items: center;
      justify-content: center;
      padding: 20px;
      background: linear-gradient(135deg, rgba(0, 102, 204, 0.1), rgba(0, 204, 153, 0.1));
    }

    .auth-wrapper {
      display: grid;
      grid-template-columns: 1fr 1fr;
      gap: 40px;
      max-width: 1000px;
      width: 100%;
      align-items: center;
    }

    .auth-brand {
      color: var(--primary);
    }

    .auth-brand h1 {
      font-size: 2.5rem;
      margin-bottom: 10px;
      display: flex;
      align-items: center;
      gap: 10px;
    }

    .auth-brand .icon {
      font-size: 3rem;
    }

    .auth-brand p {
      color: var(--text-light);
      font-size: 1.1rem;
      line-height: 1.8;
    }

    .auth-box {
      background: var(--card);
      border-radius: 12px;
      box-shadow: var(--shadow);
      padding: 40px;
    }

    .auth-box h2 {
      color: var(--primary-dark);
      margin-bottom: 10px;
      font-size: 1.8rem;
    }

    .auth-subtitle {
      color: var(--text-light);
      margin-bottom: 30px;
      font-size: 0.95rem;
    }

    .role-selector {
      display: grid;
      grid-template-columns: 1fr 1fr;
      gap: 12px;
      margin-bottom: 25px;
    }

    .role-option {
      display: flex;
      align-items: center;
      gap: 8px;
    }

    .role-option input {
      width: 18px;
      height: 18px;
      cursor: pointer;
      accent-color: var(--primary);
    }

    .role-option label {
      cursor: pointer;
      font-weight: 600;
      color: var(--text);
    }

    .form-group {
      margin-bottom: 18px;
    }

    .form-group label {
      display: block;
      margin-bottom: 8px;
      font-weight: 600;
      color: var(--text);
      font-size: 0.95rem;
    }

    .form-group input {
      width: 100%;
      padding: 12px 14px;
      border: 1px solid var(--border);
      border-radius: 8px;
      font: inherit;
      font-size: 1rem;
      transition: 0.3s;
    }

    .form-group input:focus {
      outline: none;
      border-color: var(--primary);
      box-shadow: 0 0 0 3px rgba(0, 102, 204, 0.1);
    }

    .error-message {
      background: #ffe0e0;
      border: 1px solid #ffcccc;
      color: var(--danger);
      padding: 12px 15px;
      border-radius: 8px;
      margin-bottom: 20px;
      display: none;
      font-size: 0.9rem;
    }

    .error-message.show {
      display: block;
    }

    .auth-btn {
      width: 100%;
      padding: 14px;
      background: var(--primary);
      color: white;
      border: none;
      border-radius: 8px;
      font-weight: 700;
      font-size: 1rem;
      cursor: pointer;
      transition: 0.3s;
      margin-top: 10px;
    }

    .auth-btn:hover {
      background: var(--primary-dark);
    }

    .toggle-auth {
      text-align: center;
      margin-top: 20px;
      color: var(--text-light);
      font-size: 0.95rem;
    }

    .toggle-auth button {
      background: none;
      border: none;
      color: var(--primary);
      font-weight: 700;
      cursor: pointer;
      text-decoration: underline;
    }

    .hidden {
      display: none !important;
    }

    /* ===== MAIN APP ===== */
    header {
      background: var(--card);
      border-bottom: 1px solid var(--border);
      box-shadow: 0 2px 5px rgba(0, 0, 0, 0.05);
      position: sticky;
      top: 0;
      z-index: 100;
    }

    .navbar {
      display: flex;
      justify-content: space-between;
      align-items: center;
      padding: 18px 0;
      flex-wrap: wrap;
      gap: 20px;
    }

    .logo {
      display: flex;
      align-items: center;
      gap: 10px;
      font-size: 1.5rem;
      font-weight: 700;
      color: var(--primary);
    }

    .logo-icon {
      font-size: 2rem;
    }

    .nav-links {
      display: flex;
      gap: 30px;
      align-items: center;
    }

    .nav-links a {
      color: var(--text);
      font-weight: 600;
      transition: 0.3s;
      position: relative;
    }

    .nav-links a:hover {
      color: var(--primary);
    }

    .nav-links a.active::after {
      content: '';
      position: absolute;
      bottom: -5px;
      left: 0;
      width: 100%;
      height: 3px;
      background: var(--primary);
    }

    .user-section {
      display: flex;
      gap: 15px;
      align-items: center;
    }

    .user-info {
      text-align: right;
    }

    .user-name {
      font-weight: 700;
      color: var(--text);
      font-size: 0.95rem;
    }

    .user-role {
      font-size: 0.8rem;
      color: var(--text-light);
    }

    .logout-btn {
      background: var(--danger);
      color: white;
      border: none;
      border-radius: 6px;
      padding: 10px 18px;
      font-weight: 700;
      cursor: pointer;
      transition: 0.3s;
    }

    .logout-btn:hover {
      background: #cc0000;
    }

    /* ===== HERO SECTION ===== */
    .hero {
      background: linear-gradient(135deg, var(--primary), var(--primary-dark));
      color: white;
      padding: 80px 0;
      text-align: center;
      margin-bottom: 50px;
    }

    .hero h1 {
      font-size: 3rem;
      margin-bottom: 15px;
    }

    .hero p {
      font-size: 1.2rem;
      opacity: 0.9;
      max-width: 600px;
      margin: 0 auto 30px;
    }

    .hero-buttons {
      display: flex;
      gap: 15px;
      justify-content: center;
      flex-wrap: wrap;
    }

    .btn {
      padding: 14px 28px;
      border-radius: 8px;
      border: none;
      font-weight: 700;
      cursor: pointer;
      transition: 0.3s;
      font-size: 1rem;
    }

    .btn-primary {
      background: var(--secondary);
      color: var(--text);
    }

    .btn-primary:hover {
      transform: translateY(-2px);
      box-shadow: 0 5px 15px rgba(0, 204, 153, 0.3);
    }

    .btn-secondary {
      background: transparent;
      color: white;
      border: 2px solid white;
    }

    .btn-secondary:hover {
      background: rgba(255, 255, 255, 0.1);
    }

    /* ===== SECTIONS ===== */
    section {
      padding: 60px 0;
      margin-bottom: 40px;
    }

    .section-title {
      text-align: center;
      margin-bottom: 50px;
    }

    .section-title h2 {
      font-size: 2.2rem;
      color: var(--primary-dark);
      margin-bottom: 10px;
    }

    .section-title p {
      color: var(--text-light);
      font-size: 1.05rem;
    }

    /* ===== DOCTORS GRID ===== */
    .doctors-grid {
      display: grid;
      grid-template-columns: repeat(auto-fill, minmax(280px, 1fr));
      gap: 25px;
      margin-bottom: 40px;
    }

    .doctor-card {
      background: var(--card);
      border-radius: 12px;
      overflow: hidden;
      box-shadow: var(--shadow);
      transition: 0.3s;
      cursor: pointer;
    }

    .doctor-card:hover {
      transform: translateY(-5px);
      box-shadow: 0 8px 20px rgba(0, 0, 0, 0.15);
    }

    .doctor-image {
      width: 100%;
      height: 220px;
      background: linear-gradient(135deg, var(--primary), var(--secondary));
      display: flex;
      align-items: center;
      justify-content: center;
      font-size: 4rem;
      color: white;
    }

    .doctor-info {
      padding: 20px;
    }

    .doctor-name {
      font-size: 1.2rem;
      font-weight: 700;
      color: var(--text);
      margin-bottom: 5px;
    }

    .doctor-specialty {
      color: var(--primary);
      font-weight: 600;
      margin-bottom: 10px;
      font-size: 0.95rem;
    }

    .doctor-details {
      color: var(--text-light);
      font-size: 0.9rem;
      margin-bottom: 15px;
    }

    .doctor-details p {
      margin: 5px 0;
    }

    .rating {
      display: flex;
      gap: 3px;
      margin-bottom: 12px;
    }

    .star {
      color: var(--warning);;
      font-size: 0.9rem;
    }

    .book-btn {
      width: 100%;
      padding: 10px;
      background: var(--primary);
      color: white;
      border: none;
      border-radius: 6px;
      font-weight: 700;
      cursor: pointer;
      transition: 0.3s;
    }

    .book-btn:hover {
      background: var(--primary-dark);
    }

    /* ===== APPOINTMENT MODAL ===== */
    .modal {
      display: none;
      position: fixed;
      top: 0;
      left: 0;
      width: 100%;
      height: 100%;
      background: rgba(0, 0, 0, 0.5);
      z-index: 1000;
      align-items: center;
      justify-content: center;
    }

    .modal.show {
      display: flex;
    }

    .modal-content {
      background: var(--card);
      border-radius: 12px;
      padding: 35px;
      max-width: 500px;
      width: 95%;
      max-height: 90vh;
      overflow-y: auto;
      box-shadow: 0 20px 60px rgba(0, 0, 0, 0.3);
    }

    .modal-close {
      float: right;
      font-size: 1.8rem;
      color: var(--text-light);
      cursor: pointer;
      background: none;
      border: none;
      line-height: 1;
    }

    .modal-close:hover {
      color: var(--text);
    }

    .modal h2 {
      color: var(--primary-dark);
      margin-bottom: 25px;
      clear: both;
    }

    .appointment-form {
      display: flex;
      flex-direction: column;
      gap: 15px;
    }

    .form-group select {
      width: 100%;
      padding: 12px 14px;
      border: 1px solid var(--border);
      border-radius: 8px;
      font: inherit;
      font-size: 1rem;
    }

    .form-group select:focus {
      outline: none;
      border-color: var(--primary);
      box-shadow: 0 0 0 3px rgba(0, 102, 204, 0.1);
    }

    .time-slots {
      display: grid;
      grid-template-columns: repeat(3, 1fr);
      gap: 10px;
      margin-top: 10px;
    }

    .time-slot {
      padding: 10px;
      border: 2px solid var(--border);
      border-radius: 6px;
      text-align: center;
      cursor: pointer;
      transition: 0.3s;
      background: white;
    }

    .time-slot:hover {
      border-color: var(--primary);
      background: rgba(0, 102, 204, 0.05);
    }

    .time-slot.selected {
      background: var(--primary);
      color: white;
      border-color: var(--primary);
    }

    .submit-appointment {
      width: 100%;
      padding: 14px;
      background: var(--success);
      color: white;
      border: none;
      border-radius: 8px;
      font-weight: 700;
      cursor: pointer;
      margin-top: 10px;
      transition: 0.3s;
    }

    .submit-appointment:hover {
      background: #00aa55;
    }

    /* ===== ADMIN SECTION ===== */
    .admin-section {
      display: grid;
      grid-template-columns: repeat(auto-fit, minmax(250px, 1fr));
      gap: 20px;
      margin-bottom: 40px;
    }

    .stat-card {
      background: var(--card);
      border-radius: 12px;
      padding: 25px;
      box-shadow: var(--shadow);
      text-align: center;
    }

    .stat-card .icon {
      font-size: 2.5rem;
      margin-bottom: 12px;
    }

    .stat-card .number {
      font-size: 2rem;
      font-weight: 700;
      color: var(--primary);
      margin-bottom: 5px;
    }

    .stat-card .label {
      color: var(--text-light);
      font-size: 0.95rem;
    }

    .admin-tabs {
      display: flex;
      gap: 12px;
      margin-bottom: 25px;
      flex-wrap: wrap;
    }

    .admin-tab {
      padding: 10px 20px;
      background: var(--card);
      border: 2px solid var(--border);
      border-radius: 8px;
      cursor: pointer;
      font-weight: 600;
      transition: 0.3s;
      color: var(--text);
    }

    .admin-tab:hover {
      border-color: var(--primary);
      color: var(--primary);
    }

    .admin-tab.active {
      background: var(--primary);
      color: white;
      border-color: var(--primary);
    }

    .tab-content {
      display: none;
    }

    .tab-content.active {
      display: block;
    }

    .admin-form {
      background: var(--card);
      border-radius: 12px;
      padding: 30px;
      box-shadow: var(--shadow);
      max-width: 600px;
    }

    .form-group-full {
      margin-bottom: 18px;
    }

    .admin-form button {
      width: 100%;
      padding: 14px;
      background: var(--primary);
      color: white;
      border: none;
      border-radius: 8px;
      font-weight: 700;
      cursor: pointer;
      margin-top: 10px;
      transition: 0.3s;
    }

    .admin-form button:hover {
      background: var(--primary-dark);
    }

    /* ===== APPOINTMENTS LIST ===== */
    .appointments-list {
      background: var(--card);
      border-radius: 12px;
      overflow: hidden;
      box-shadow: var(--shadow);
    }

    .appointment-item {
      padding: 20px;
      border-bottom: 1px solid var(--border);
      display: flex;
      justify-content: space-between;
      align-items: center;
      flex-wrap: wrap;
      gap: 15px;
    }

    .appointment-item:last-child {
      border-bottom: none;
    }

    .appointment-details {
      flex: 1;
      min-width: 200px;
    }

    .appointment-patient {
      font-weight: 700;
      color: var(--text);
      margin-bottom: 5px;
    }

    .appointment-info {
      color: var(--text-light);
      font-size: 0.9rem;
    }

    .appointment-info p {
      margin: 3px 0;
    }

    .status-badge {
      padding: 6px 12px;
      border-radius: 20px;
      font-weight: 600;
      font-size: 0.8rem;
    }

    .status-pending {
      background: #fff3cd;
      color: #856404;
    }

    .status-confirmed {
      background: #d4edda;
      color: #155724;
    }

    .status-completed {
      background: #d1ecf1;
      color: #0c5460;
    }

    .status-cancelled {
      background: #f8d7da;
      color: #721c24;
    }

    .appointment-actions {
      display: flex;
      gap: 8px;
    }

    .action-btn {
      padding: 6px 12px;
      border: none;
      border-radius: 6px;
      font-weight: 600;
      cursor: pointer;
      font-size: 0.85rem;
      transition: 0.3s;
    }

    .action-confirm {
      background: var(--success);
      color: white;
    }

    .action-confirm:hover {
      background: #00aa55;
    }

    .action-cancel {
      background: var(--danger);
      color: white;
    }

    .action-cancel:hover {
      background: #cc0000;
    }

    /* ===== RESPONSIVE ===== */
    @media (max-width: 768px) {
      .auth-wrapper {
        grid-template-columns: 1fr;
        gap: 20px;
      }

      .auth-brand {
        display: none;
      }

      .doctors-grid {
        grid-template-columns: 1fr;
      }

      .nav-links {
        gap: 15px;
        font-size: 0.9rem;
      }

      .hero h1 {
        font-size: 2rem;
      }

      .section-title h2 {
        font-size: 1.8rem;
      }

      .appointment-item {
        flex-direction: column;
        align-items: flex-start;
      }

      .admin-form {
        max-width: 100%;
      }

      .time-slots {
        grid-template-columns: repeat(2, 1fr);
      }
    }

    @media (max-width: 480px) {
      .navbar {
        gap: 10px;
      }

      .nav-links {
        gap: 8px;
        font-size: 0.8rem;
      }

      .user-section {
        flex-direction: column;
        gap: 8px;
        width: 100%;
      }

      .auth-box {
        padding: 25px;
      }

      .hero h1 {
        font-size: 1.5rem;
      }

      .hero p {
        font-size: 1rem;
      }

      .hero-buttons {
        flex-direction: column;
      }

      .btn {
        width: 100%;
      }

      .modal-content {
        padding: 20px;
      }
    }
  </style>
</head>
<body>

  <!-- ===== AUTH PAGE ===== -->
  <div id="authPage" class="auth-container">
    <div class="auth-wrapper">
      <div class="auth-brand">
        <div class="icon">🏥</div>
        <h1>MedCare</h1>
        <p>Your trusted healthcare partner. Book appointments with top specialists and manage your health efficiently.</p>
      </div>

      <div class="auth-box">
        <h2 id="authTitle">Login</h2>
        <p class="auth-subtitle" id="authSubtitle">Access your healthcare account</p>

        <div class="error-message" id="authError"></div>

        <form class="auth-form" id="authForm">
          <div class="form-group">
            <label>Account Type</label>
            <div class="role-selector">
              <div class="role-option">
                <input type="radio" id="rolePatient" name="role" value="patient" checked />
                <label for="rolePatient">Patient</label>
              </div>
              <div class="role-option">
                <input type="radio" id="roleAdmin" name="role" value="admin" />
                <label for="roleAdmin">Admin</label>
              </div>
            </div>
          </div>

          <div class="form-group">
            <label for="email">Email Address</label>
            <input type="email" id="email" placeholder="you@example.com" required />
          </div>

          <div class="form-group">
            <label for="password">Password</label>
            <input type="password" id="password" placeholder="Enter your password" required />
          </div>

          <div class="form-group" id="nameField" style="display: none;">
            <label for="fullname">Full Name</label>
            <input type="text" id="fullname" placeholder="Your full name" />
          </div>

          <div class="form-group" id="phoneField" style="display: none;">
            <label for="phone">Phone Number</label>
            <input type="tel" id="phone" placeholder="Your phone number" />
          </div>

          <button type="submit" class="auth-btn" id="authSubmitBtn">Login</button>
        </form>

        <div class="toggle-auth">
          <span id="toggleText">Don't have an account? </span>
          <button type="button" id="toggleAuthBtn" onclick="toggleAuthMode()">Sign up</button>
        </div>
      </div>
    </div>
  </div>

  <!-- ===== MAIN APP ===== -->
  <div id="mainApp" class="hidden">
    <header>
      <div class="container">
        <nav class="navbar">
          <div class="logo">
            <span class="logo-icon">🏥</span>
            MedCare
          </div>

          <div class="nav-links">
            <a href="#home" class="nav-link active">Home</a>
            <a href="#doctors" class="nav-link">Doctors</a>
            <a href="#appointments" class="nav-link">My Appointments</a>
            <a href="#admin" class="nav-link admin-link" style="display: none;">Admin</a>
          </div>

          <div class="user-section">
            <div class="user-info">
              <div class="user-name" id="userName">User</div>
              <div class="user-role" id="userRole">Patient</div>
            </div>
            <button class="logout-btn" onclick="logout()">Logout</button>
          </div>
        </nav>
      </div>
    </header>

    <!-- ===== HERO SECTION ===== -->
    <section class="hero patient-section" id="home">
      <div class="container">
        <h1>Welcome to MedCare</h1>
        <p>Book appointments with top doctors and specialists. Get quality healthcare at your convenience.</p>
        <div class="hero-buttons">
          <a href="#doctors" class="btn btn-primary">Browse Doctors</a>
