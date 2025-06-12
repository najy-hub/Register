<!DOCTYPE html>
<html lang="ar" dir="rtl">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1" />
  <title>سجّل في الدورة التدريبية</title>
  <style>
    @import url('https://fonts.googleapis.com/css2?family=Cairo:wght@400;700&display=swap');
    body {
      font-family: 'Cairo', sans-serif;
      margin: 0;
      background: linear-gradient(to bottom, #0f0f0f, #1a1a1a);
      color: #f5f5f5;
    }
    header {
      background: url('https://images.unsplash.com/photo-1600585154340-be6161a56a0c?auto=format&fit=crop&w=1200&q=80') center/cover no-repeat;
      height: 240px;
      position: relative;
      display: flex;
      align-items: center;
      justify-content: center;
      color: white;
      text-align: center;
    }
    header::after {
      content: "";
      position: absolute;
      inset: 0;
      background: rgba(0, 0, 0, 0.6);
    }
    header h1 {
      position: relative;
      font-size: 24px;
      z-index: 1;
      max-width: 90%;
      padding: 0 10px;
      text-shadow: 0 2px 6px rgba(0,0,0,0.6);
    }
    .container {
      background-color: #1e1e1e;
      padding: 20px;
      border-radius: 14px;
      box-shadow: 0 8px 24px rgba(0, 0, 0, 0.5);
      max-width: 95%;
      margin: -60px auto 40px;
      z-index: 2;
      position: relative;
    }
    h2 {
      text-align: center;
      color: #fcd34d;
      font-size: 20px;
    }
    label {
      display: block;
      margin-top: 12px;
      font-size: 14px;
    }
    input, select {
      width: 100%;
      padding: 10px;
      margin-top: 5px;
      border: 1px solid #333;
      border-radius: 8px;
      background-color: #2a2a2a;
      color: #fff;
      font-size: 15px;
    }
    .phone-group {
      display: flex;
      gap: 8px;
    }
    .phone-group select {
      flex: 1;
    }
    .phone-group input {
      flex: 2;
    }
    button {
      width: 100%;
      margin-top: 20px;
      padding: 12px;
      background: linear-gradient(to right, #facc15, #fbbf24);
      color: #1a1a1a;
      font-size: 16px;
      font-weight: bold;
      border: none;
      border-radius: 8px;
      cursor: pointer;
      transition: background 0.3s, transform 0.2s;
    }
    button:hover {
      background: linear-gradient(to right, #fde68a, #fcd34d);
      transform: scale(1.02);
    }
    .success {
      display: none;
      text-align: center;
      color: #22c55e;
      margin-top: 15px;
      font-weight: bold;
      font-size: 15px;
    }
    @media (max-width: 480px) {
      header {
        height: 180px;
      }
      header h1 {
        font-size: 20px;
      }
      .phone-group {
        flex-direction: column;
      }
      button {
        font-size: 15px;
      }
    }
  </style>
</head>
<body>
  <header>
    <h1>ابدأ رحلتك في عالم الطاقة الشمسية باحترافية وتميّز!</h1>
  </header>

  <div class="container">
    <h2>سجّل الآن</h2>
    <form id="leadForm" action="https://script.google.com/macros/s/AKfycbyqk94TFkIxmsn1v12OnFgS-ni7E8-0kBztlm43i14ydpUiAJHVrJ-L2u9W3ZuyozBg/exec" method="POST">
      <label for="name">الاسم الكامل:</label>
      <input type="text" id="name" name="name" required />

      <label for="email">البريد الإلكتروني:</label>
      <input type="email" id="email" name="email" required />

      <label for="phone">رقم الهاتف:</label>
      <div class="phone-group">
        <select id="countryCode" required>
          <option value="+20">🇪🇬 +20</option>
          <option value="+966">🇸🇦 +966</option>
          <option value="+971">🇦🇪 +971</option>
          <option value="+218">🇱🇾 +218</option>
          <option value="+962">🇯🇴 +962</option>
          <option value="+964">🇮🇶 +964</option>
          <option value="+212">🇲🇦 +212</option>
          <option value="+249">🇸🇩 +249</option>
          <option value="+974">🇶🇦 +974</option>
          <option value="+968">🇴🇲 +968</option>
          <option value="+1">🇺🇸 +1</option>
        </select>
        <input type="tel" id="phone" placeholder="123456789" required />
      </div>

      <input type="hidden" name="fullPhone" id="fullPhone" />
      <button type="submit">سجّل الآن</button>
    </form>
    <div class="success" id="successMsg">✅ تم إرسال بياناتك بنجاح!</div>
  </div>

  <script>
    function preparePhone() {
      const code = document.getElementById("countryCode").value;
      const phone = document.getElementById("phone").value.trim();
      document.getElementById("fullPhone").value = `${code}${phone}`;
    }

    const form = document.getElementById("leadForm");
    form.addEventListener("submit", function (e) {
      e.preventDefault();
      preparePhone();
      const formData = new FormData(form);
      fetch(form.action, {
        method: "POST",
        body: formData
      })
      .then((res) => res.text())
      .then((text) => {
        if (text.includes("success")) {
          document.getElementById("successMsg").style.display = "block";
          form.reset();
        } else if (text.includes("duplicate")) {
          alert("لقد قمت بالتسجيل مسبقاً.");
        } else {
          alert("حدث خطأ أثناء التسجيل، الرجاء المحاولة مرة أخرى.");
        }
      });
    });
  </script>
</body>
</html>
