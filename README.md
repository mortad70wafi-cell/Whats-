<headerstatus.style.color
  <span id="chatUser">اختر مستخدم</span>
  <button onclick="toggleHide()">👻</button>
</header>
let currentUser = null;
let hiddenChats = JSON.parse(localStorage.getItem("hiddenChats")) || [];

function openChat(user) {
  if (isHidden(user)) return;

  currentUser = user;
  chatUser.innerText = user + " 🟢 متصل";
  chatBox.innerHTML = "";
}

function toggleHide() {
  if (!currentUser) return;

  if (isHidden(currentUser)) {
    hiddenChats = hiddenChats.filter(u => u !== currentUser);
    showSystem("👁️ تم إظهار الدردشة");
  } else {
    hiddenChats.push(currentUser);
    showSystem("👻 تم إخفاء الدردشة");
    currentUser = null;
    chatUser.innerText = "اختر مستخدم";
    chatBox.innerHTML = "";
  }

  localStorage.setItem("hiddenChats", JSON.stringify(hiddenChats));
  refreshUsers();
}

function isHidden(user) {
  return hiddenChats.includes(user);
}

function sendMessage() {
  if (!currentUser) return;

  const msg = message.value.trim();
  if (!msg) return;

  addMessage(msg, "sent");
  message.value = "";

  setTimeout(() => {
    if (!isHidden(currentUser)) {
      addMessage("📩 رسالة واردة", "received");
    }
  }, 1000);
}

function showSystem(text) {
  const div = document.createElement("div");
  div.style.textAlign = "center";
  div.style.color = "#94a3b8";
  div.innerText = text;
  chatBox.appendChild(div);
}
function refreshUsers() {
  document.querySelectorAll(".user").forEach(userDiv => {
    const name = userDiv.innerText.replace("👤 ", "");
    userDiv.style.display = isHidden(name) ? "none" : "block";
  });
}

refreshUsers();
