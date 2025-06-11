<!DOCTYPE html>
<html lang="ar" dir="rtl">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1">
  <title>سجّل في الدورة التدريبية</title>
  <style>
    body {
      font-family: 'Tahoma', sans-serif;
      background: linear-gradient(to bottom, #f0f0f0, #d9e4f5);
      margin: 0;
      padding: 0;
      display: flex;
      justify-content: center;
      align-items: center;
      height: 100vh;
    }

    .container {
      background-color: white;
      padding: 30px;
      border-radius: 16px;
      box-shadow: 0 8px 20px rgba(0, 0, 0, 0.1);
      max-width: 400px;
      width: 90%;
    }

    h2 {
      text-align: center;
      color: #1a73e8;
      margin-bottom: 20px;
    }

    label {
      display: block;
      margin-top: 15px;
      font-weight: bold;
    }

    input, select {
      width: 100%;
      padding: 10px;
      margin-top: 5px;
      border: 1px solid #ccc;
      border-radius: 8px;
      font-size: 16px;
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
      margin-top: 25px;
      padding: 12px;
      background-color: #1a73e8;
      color: white;
      font-size: 16px;
      border: none;
      border-radius: 8px;
      cursor: pointer;
      transition: background-color 0.3s;
    }

    button:hover {
      background-color: #155ab6;
    }

    .success {
      display: none;
      text-align: center;
      color: green;
      margin-top: 20px;
      font-weight: bold;
    }
  </style>
</head>
<body>

  <div class="container">
    <h2>سجّل في الدورة التدريبية</h2>
    <form id="leadForm" action="https://script.google.com/macros/s/AKfycbxPvx5CXY-evqeSV6ruuTVIL74Pn1b-ZUOmGOLoBboNCaI1B-5mZ1nYL639Hj0mIN-X/exec" method="POST" target="hidden_iframe" onsubmit="preparePhone(); showMessage();">
      <label for="name">الاسم الكامل:</label>
      <input type="text" id="name" name="name" required>

      <label for="email">البريد الإلكتروني:</label>
      <input type="email" id="email" name="email" required>

      <label for="phone">رقم الهاتف:</label>
      <div class="phone-group">
        <select id="countryCode" required>
          <option value="+249">SD +249</option>
          <option value="+20">🇪🇬 +20</option>
          <option value="+966">🇸🇦 +966</option>
          <option value="+971">🇦🇪 +971</option>
          <option value="+218">🇱🇾 +218</option>
          <option value="+962">🇯🇴 +962</option>
          <option value="+964">🇮🇶 +964</option>
          <option value="+212">🇲🇦 +212</option>
          <option value="+1">🇺🇸 +1</option>
        </select>
        <input type="tel" id="phone" placeholder="123456789" required>
      </div>

      <!-- سيتم دمج المفتاح والرقم هنا -->
      <input type="hidden" name="fullPhone" id="fullPhone">

      <button type="submit">سجّل الآن</button>
    </form>
    <div class="success" id="successMsg">✅ تم إرسال بياناتك بنجاح!</div>
  </div>

  <iframe name="hidden_iframe" style="display:none;" onload="submitted && document.getElementById('successMsg').style.display = 'block';"></iframe>

  <script>
    let submitted = false;

    function preparePhone() {
      const code = document.getElementById("countryCode").value;
      const phone = document.getElementById("phone").value.trim();
      document.getElementById("fullPhone").value = `${code}${phone}`;
    }

    function showMessage() {
      submitted = true;
      setTimeout(() => {
        document.getElementById("leadForm").reset();
      }, 1000);
    }
  </script>
</body>
</html>
