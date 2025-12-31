smart-app-lock
smart-app-lock/
│
├── index.html
├── style.css
├── script.js
├── security.js
├── assets/
│   ├── lock.png
│   ├── alarm.mp3
│   └── bg.jpg
└── README.md
<!DOCTYPE html>
<html lang="ar">
<head>
<meta charset="UTF-8">
<title>Smart App Lock</title>
<link rel="stylesheet" href="style.css">
</head>
<body>

<div class="lock-container">
  <h2>🔒 قفل التطبيقات الذكي</h2>

  <input type="password" id="pin" placeholder="أدخل الرقم السري">
  <button onclick="unlock()">فتح</button>

  <p id="status"></p>
</div>

<audio id="alarm" src="assets/alarm.mp3"></audio>

<script src="security.js"></script>
<script src="script.js"></script>
</body>
</html>
body {
  background: linear-gradient(135deg,#000,#1a1a1a);
  font-family: Tahoma;
  color: white;
  display: flex;
  justify-content: center;
  align-items: center;
  height: 100vh;
}

.lock-container {
  background: rgba(0,0,0,0.8);
  padding: 30px;
  border-radius: 20px;
  box-shadow: 0 0 30px red;
  text-align: center;
}

input {
  width: 100%;
  padding: 12px;
  margin: 10px 0;
  border-radius: 10px;
  border: none;
  font-size: 18px;
}

button {
  width: 100%;
  padding: 12px;
  background: red;
  color: white;
  border: none;
  border-radius: 10px;
  font-size: 18px;
  cursor: pointer;
}
let attempts = 0;
const correctPin = "2580";

function unlock() {
  const pin = document.getElementById("pin").value;
  const status = document.getElementById("status");

  if (pin === correctPin) {
    status.innerHTML = "✅ تم فتح التطبيق بنجاح";
    status.style.color = "lime";
    attempts = 0;
  } else {
    attempts++;
    status.innerHTML = "❌ رمز خاطئ";
    status.style.color = "red";
    playAlarm();

    if (attempts >= 3) {
      lockSystem();
    }
  }
}
function playAlarm() {
  document.getElementById("alarm").play();
}

function lockSystem() {
  document.body.innerHTML = `
    <h1 style="color:red;text-align:center;">
    🚨 تم قفل النظام مؤقتًا 🚨
    </h1>
  `;
  setTimeout(() => {
    location.reload();
  }, 10000);
}
# 🔐 Smart App Lock

برنامج قفل تطبيقات ذكي بواجهة احترافية ونظام حماية قوي.

## المميزات
- رقم سري
- إنذار عند الخطأ
- قفل مؤقت
- تصميم عصري
- قابل للتحويل لتطبيق أندرويد WebView

## الاستخدام
افتح index.html