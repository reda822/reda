<!DOCTYPE html>
<html lang="ar">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>RM.MINATO</title>
  <style>
    body {
      background: url('https://encrypted-tbn0.gstatic.com/images?q=tbn:ANd9GcS-0jl6-dNBJow-Yjbyy5VWyBDMNTrF91FexbrGpmSTkg&s') no-repeat center center fixed;
      background-size: cover;
      font-family: Arial, sans-serif;
      color: white;
      margin: 0;
    }
    .sidebar-button {
      position: fixed;
      top: 20px;
      right: 20px;
      background-color: yellow;
      color: black;
      padding: 10px;
      border: none;
      cursor: pointer;
      z-index: 999;
    }
    .sidebar {
      display: none;
      position: fixed;
      top: 0;
      right: 0;
      background-color: rgba(0,0,0,0.8);
      width: 300px;
      height: 100%;
      padding: 20px;
    }
    .card {
      background-color: rgba(0, 0, 0, 0.8);
      color: white;
      padding: 20px;
      margin: 20px auto;
      border-radius: 10px;
      width: 300px;
      font-size: 16px;
    }
    .center-buttons {
      position: fixed;
      top: 50%;
      left: 50%;
      transform: translate(-50%, -50%);
      display: flex;
      gap: 10px;
    }
    .login-section, .message-section, #profileInfo {
      position: fixed;
      bottom: 80px;
      left: 20px;
      background: rgba(0, 0, 0, 0.8);
      padding: 10px;
      border-radius: 8px;
      display: none;
      color: white;
    }
    .profile-icon {
      position: fixed;
      top: 20px;
      left: 20px;
      border-radius: 50%;
      width: 46px;
      height: 46px;
      display: none;
      cursor: pointer;
    }
    .profile-icon img {
      border-radius: 50%;
      width: 100%;
      height: 100%;
    }
    .message-toggle {
      position: fixed;
      bottom: 20px;
      right: 20px;
      background: #fff;
      color: black;
      padding: 10px;
      border-radius: 8px;
      cursor: pointer;
    }
  </style>
</head>
<body>

<button class="sidebar-button" onclick="toggleSidebar()">+</button>
<div class="sidebar" id="sidebar">
  <h3>ادخل معلوماتك</h3>
  <input id="name" placeholder="الاسم الكامل"><br><br>
  <input id="date" placeholder="تاريخ الانضمام"><br><br>
  <input id="age" placeholder="العمر"><br><br>
  <input id="city" placeholder="المدينة"><br><br>
  <button onclick="saveInfo()">حفظ</button>
</div>

<div id="card-section"></div>

<div class="center-buttons">
  <a href="https://www.instagram.com/reda_chtbaoui?igsh=MnNpcjB6amxjdWFl" target="_blank">
    <img src="https://encrypted-tbn0.gstatic.com/images?q=tbn:ANd9GcR91Zs4XQvbepd_MvWruW4oT9EXifZB5A5Raper_jR3xQ&s" width="40">
  </a>
  <button onclick="showLogin()">تسجيل الدخول</button>
</div>

<div class="login-section" id="login-section">
  <input id="username" placeholder="اسم المستخدم"><br><br>
  <input id="password" placeholder="كلمة المرور" type="password"><br>
  <span id="error" style="color:red;"></span><br>
  <button onclick="validateLogin()">تسجيل</button>
</div>

<div class="profile-icon" id="profileIcon" onclick="showProfile()">
  <img src="https://lh3.googleusercontent.com/-mqOEgtzMt6Y/AAAAAAAAAAI/AAAAAAAAAAA/ALKGfknTDj7D1gseoc4KLvi5ThP3aRfvwQ/photo.jpg?sz=46" alt="Profile">
</div>
<div id="profileInfo"></div>

<button class="message-toggle" onclick="toggleMessage()">
  هل تريد ارسال رسالة للمطور المبتدئ ؟
</button>
<div class="message-section" id="messageBox">
  <textarea id="message" rows="4" cols="30" placeholder="اكتب رسالتك هنا..."></textarea><br>
  <button onclick="sendMessage()">ارسال</button>
</div>

<script>
  let userInfo = {};

  function toggleSidebar() {
    const sidebar = document.getElementById('sidebar');
    sidebar.style.display = sidebar.style.display === 'block' ? 'none' : 'block';
  }

  function saveInfo() {
    userInfo = {
      name: document.getElementById('name').value,
      date: document.getElementById('date').value,
      age: document.getElementById('age').value,
      city: document.getElementById('city').value
    };
    document.getElementById('card-section').innerHTML = `
      <div class="card">
        <strong>الاسم الكامل:</strong> ${userInfo.name}<br>
        <strong>تاريخ الانضمام:</strong> ${userInfo.date}<br>
        <strong>العمر:</strong> ${userInfo.age}<br>
        <strong>المدينة:</strong> ${userInfo.city}
      </div>
    `;
    toggleSidebar();
  }

  function showLogin() {
    document.getElementById('login-section').style.display = 'block';
  }

  function validateLogin() {
    const password = document.getElementById('password').value;
    if (password.length < 4) {
      document.getElementById('error').innerText = 'عاود عاود اياغيول';
    } else {
      document.getElementById('error').innerText = '';
      document.getElementById('profileIcon').style.display = 'block';
      document.getElementById('login-section').style.display = 'none';
    }
  }

  function showProfile() {
    document.getElementById('profileInfo').style.display = 'block';
    document.getElementById('profileInfo').innerHTML = `
      <div class="card">
        <strong>الاسم الكامل:</strong> ${userInfo.name}<br>
        <strong>العمر:</strong> ${userInfo.age}<br>
        <strong>المدينة:</strong> ${userInfo.city}
      </div>
    `;
  }

  function toggleMessage() {
    const box = document.getElementById('messageBox');
    box.style.display = box.style.display === 'block' ? 'none' : 'block';
  }

  function sendMessage() {
    const message = document.getElementById('message').value;
    window.location.href = `mailto:alshtbawyrdy@gmail.com?subject=رسالة من RM.MINATO&body=${encodeURIComponent(message)}`;
  }
</script>

</body>
</html>
