<!DOCTYPE html>
<html lang="vi">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Thông Tin Tài Khoản</title>
  <style>
    * {
      margin: 0;
      padding: 0;
      box-sizing: border-box;
    }
    
    body {
      font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
      background: linear-gradient(135deg, #667eea 0%, #764ba2 100%);
      min-height: 100vh;
      display: flex;
      align-items: center;
      justify-content: center;
      padding: 20px;
    }
    
    .container {
      max-width: 450px;
      width: 100%;
      background: rgba(255, 255, 255, 0.95);
      backdrop-filter: blur(10px);
      padding: 30px;
      border-radius: 20px;
      box-shadow: 0 20px 40px rgba(0, 0, 0, 0.1);
      animation: slideUp 0.6s ease-out;
    }
    
    @keyframes slideUp {
      from {
        opacity: 0;
        transform: translateY(30px);
      }
      to {
        opacity: 1;
        transform: translateY(0);
      }
    }
    
    h2 {
      text-align: center;
      color: #333;
      margin-bottom: 25px;
      font-size: 24px;
      font-weight: 600;
    }
    
    .account-selector {
      text-align: center;
      margin-bottom: 20px;
    }
    
    .account-info {
      background: linear-gradient(145deg, #e3f2fd, #bbdefb);
      padding: 10px;
      border-radius: 8px;
      font-size: 14px;
      color: #1976d2;
      margin-bottom: 15px;
    }
    
    .field {
      margin: 15px 0;
      background: linear-gradient(145deg, #f8f9fa, #e9ecef);
      padding: 15px;
      border-radius: 12px;
      border-left: 4px solid #3399ff;
      position: relative;
      transition: all 0.3s ease;
      cursor: pointer;
    }
    
    .field:hover {
      transform: translateX(5px);
      box-shadow: 0 5px 15px rgba(51, 153, 255, 0.2);
    }
    
    .field-label {
      font-size: 12px;
      color: #666;
      margin-bottom: 5px;
      text-transform: uppercase;
      letter-spacing: 0.5px;
    }
    
    .field-value {
      font-size: 14px;
      color: #333;
      font-weight: 500;
      word-break: break-all;
    }
    
    .copy-indicator {
      position: absolute;
      top: 10px;
      right: 15px;
      font-size: 12px;
      color: #3399ff;
      opacity: 0;
      transition: opacity 0.3s ease;
    }
    
    .field:hover .copy-indicator {
      opacity: 1;
    }
    
    .hidden {
      display: none;
    }
    
    .btn {
      background: linear-gradient(145deg, #3399ff, #2d7dd8);
      color: white;
      padding: 15px;
      margin: 10px 0;
      border: none;
      border-radius: 12px;
      width: 100%;
      cursor: pointer;
      font-size: 16px;
      font-weight: 600;
      transition: all 0.3s ease;
      position: relative;
      overflow: hidden;
    }
    
    .btn:hover {
      transform: translateY(-2px);
      box-shadow: 0 10px 25px rgba(51, 153, 255, 0.3);
    }
    
    .btn:active {
      transform: translateY(0);
    }
    
    .btn:before {
      content: '';
      position: absolute;
      top: 0;
      left: -100%;
      width: 100%;
      height: 100%;
      background: linear-gradient(90deg, transparent, rgba(255,255,255,0.2), transparent);
      transition: left 0.5s;
    }
    
    .btn:hover:before {
      left: 100%;
    }
    
    .btn.disabled {
      background: #ccc;
      cursor: not-allowed;
      transform: none;
    }
    
    .btn.disabled:hover {
      transform: none;
      box-shadow: none;
    }
    
    .notification {
      position: fixed;
      top: 20px;
      right: 20px;
      background: #28a745;
      color: white;
      padding: 15px 20px;
      border-radius: 8px;
      box-shadow: 0 5px 15px rgba(0,0,0,0.2);
      transform: translateX(400px);
      transition: transform 0.3s ease;
      z-index: 1000;
      max-width: 300px;
    }
    
    .notification.show {
      transform: translateX(0);
    }
    
    .notification.error {
      background: #dc3545;
    }
    
    .modal {
      display: none;
      position: fixed;
      z-index: 1000;
      left: 0;
      top: 0;
      width: 100%;
      height: 100%;
      background-color: rgba(0,0,0,0.5);
      backdrop-filter: blur(5px);
    }
    
    .modal-content {
      background-color: white;
      margin: 5% auto;
      padding: 30px;
      border-radius: 15px;
      width: 90%;
      max-width: 500px;
      box-shadow: 0 20px 40px rgba(0,0,0,0.2);
      animation: modalSlide 0.3s ease-out;
    }
    
    @keyframes modalSlide {
      from {
        opacity: 0;
        transform: translateY(-50px);
      }
      to {
        opacity: 1;
        transform: translateY(0);
      }
    }
    
    .close {
      color: #aaa;
      float: right;
      font-size: 28px;
      font-weight: bold;
      cursor: pointer;
      line-height: 1;
    }
    
    .close:hover {
      color: #333;
    }
    
    .input-group {
      margin: 15px 0;
    }
    
    .input-group label {
      display: block;
      margin-bottom: 5px;
      font-weight: 600;
      color: #333;
    }
    
    .input-group input, .input-group textarea {
      width: 100%;
      padding: 12px;
      border: 2px solid #e9ecef;
      border-radius: 8px;
      font-size: 14px;
      transition: border-color 0.3s ease;
    }
    
    .input-group input:focus, .input-group textarea:focus {
      outline: none;
      border-color: #3399ff;
    }
    
    .input-group textarea {
      height: 100px;
      resize: vertical;
    }
    
    .modal-btn {
      background: linear-gradient(145deg, #28a745, #20a037);
      color: white;
      padding: 12px 25px;
      border: none;
      border-radius: 8px;
      cursor: pointer;
      font-size: 14px;
      font-weight: 600;
      margin-right: 10px;
      transition: all 0.3s ease;
    }
    
    .modal-btn:hover {
      transform: translateY(-2px);
      box-shadow: 0 5px 15px rgba(40, 167, 69, 0.3);
    }
    
    .modal-btn.cancel {
      background: linear-gradient(145deg, #6c757d, #5a6268);
    }
    
    .modal-btn.cancel:hover {
      box-shadow: 0 5px 15px rgba(108, 117, 125, 0.3);
    }
    
    .loading {
      display: inline-block;
      width: 20px;
      height: 20px;
      border: 3px solid #f3f3f3;
      border-top: 3px solid #3498db;
      border-radius: 50%;
      animation: spin 1s linear infinite;
      margin-right: 10px;
    }
    
    @keyframes spin {
      0% { transform: rotate(0deg); }
      100% { transform: rotate(360deg); }
    }
    
    @media (max-width: 480px) {
      .container {
        margin: 10px;
        padding: 20px;
      }
      
      h2 {
        font-size: 20px;
      }
      
      .btn {
        font-size: 14px;
        padding: 12px;
      }
    }
  </style>
</head>
<body>
  <div class="container">
    <h2>💼 Thông Tin Tài Khoản</h2>
    
    <div class="account-info">
      <span id="accountCounter">Chưa có tài khoản nào</span>
    </div>
    
    <div class="field" onclick="copyToClipboard(getCurrentUsername(), this)">
      <div class="field-label">Tên đăng nhập</div>
      <div class="field-value" id="usernameValue">Chưa có tài khoản</div>
      <div class="copy-indicator">Nhấp để sao chép</div>
    </div>
    
    <div class="field" onclick="copyToClipboard(getCurrentPassword(), this)">
      <div class="field-label">Mật khẩu</div>
      <div class="field-value" id="passwordValue">••••••••••</div>
      <div class="copy-indicator">Nhấp để sao chép</div>
    </div>
    
    <div class="field" onclick="copyToClipboard(getCurrentEmail(), this)">
      <div class="field-label">Email</div>
      <div class="field-value" id="emailValue">Chưa có tài khoản</div>
      <div class="copy-indicator">Nhấp để sao chép</div>
    </div>
    
    <div class="field hidden" id="codeField" onclick="copyToClipboard(getCurrentCode(), this)">
      <div class="field-label">Mã Code Gmail</div>
      <div class="field-value" id="codeValue">Chưa có mã</div>
      <div class="copy-indicator">Nhấp để sao chép</div>
    </div>
    
    <button class="btn" id="getCodeBtn" onclick="getCode()">
      🔑 Lấy Mã
    </button>
    
    <button class="btn" id="refreshBtn" onclick="refreshAccount()">
      📥 Làm Mới Tài Khoản
    </button>
    
    <button class="btn" onclick="showAddAccount()">
      ➕ Thêm Tài Khoản
    </button>
  </div>
  
  <div class="notification" id="notification"></div>

  <!-- Modal thêm tài khoản -->
  <div id="addAccountModal" class="modal">
    <div class="modal-content">
      <span class="close" onclick="closeModal()">&times;</span>
      <h3>➕ Thêm Tài Khoản Mới</h3>
      
      <div class="input-group">
        <label for="rawAccountData">📋 Dán thông tin tài khoản (định dạng: user|pass|email|emailpass|code):</label>
        <textarea id="rawAccountData" placeholder="Ví dụ: user123|password123|email@domain.com|emailpass|code123abc..."></textarea>
        <button type="button" class="modal-btn" onclick="parseAccountData()" style="margin-top: 10px; width: 100%;">
          🔄 Tự Động Phân Tích
        </button>
      </div>
      
      <div style="border-top: 2px dashed #e9ecef; margin: 20px 0; padding-top: 20px;">
        <p style="color: #666; font-size: 14px; margin-bottom: 15px;">Hoặc nhập thủ công:</p>
        
        <div class="input-group">
          <label for="newUsername">Tên đăng nhập:</label>
          <input type="text" id="newUsername" placeholder="Nhập tên đăng nhập...">
        </div>
        
        <div class="input-group">
          <label for="newPassword">Mật khẩu:</label>
          <input type="text" id="newPassword" placeholder="Nhập mật khẩu...">
        </div>
        
        <div class="input-group">
          <label for="newEmail">Email:</label>
          <input type="email" id="newEmail" placeholder="Nhập email...">
        </div>
        
        <div class="input-group">
          <label for="newEmailPassword">Mật khẩu Email:</label>
          <input type="text" id="newEmailPassword" placeholder="Nhập mật khẩu email...">
        </div>
        
        <div class="input-group">
          <label for="newCode">Mã Code Gmail:</label>
          <input type="text" id="newCode" placeholder="Nhập mã code để lấy code gmail...">
        </div>
      </div>
      
      <div style="text-align: right; margin-top: 20px;">
        <button type="button" class="modal-btn cancel" onclick="closeModal()">Hủy</button>
        <button type="button" class="modal-btn" onclick="addAccount()">Thêm Tài Khoản</button>
      </div>
    </div>
  </div>

  <script>
    // Lưu trữ tài khoản
    let accounts = [];
    let currentAccountIndex = 0;
    
    // Khởi tạo
    function init() {
      updateAccountDisplay();
      updateButtons();
    }
    
    function updateAccountDisplay() {
      const counter = document.getElementById('accountCounter');
      const usernameValue = document.getElementById('usernameValue');
      const passwordValue = document.getElementById('passwordValue');
      const emailValue = document.getElementById('emailValue');
      
      if (accounts.length === 0) {
        counter.textContent = 'Chưa có tài khoản nào';
        usernameValue.textContent = 'Chưa có tài khoản';
        passwordValue.textContent = '••••••••••';
        emailValue.textContent = 'Chưa có tài khoản';
      } else {
        counter.textContent = `Tài khoản ${currentAccountIndex + 1}/${accounts.length}`;
        const current = accounts[currentAccountIndex];
        usernameValue.textContent = current.username;
        passwordValue.textContent = '••••••••••';
        emailValue.textContent = current.email;
      }
    }
    
    function updateButtons() {
      const getCodeBtn = document.getElementById('getCodeBtn');
      const refreshBtn = document.getElementById('refreshBtn');
      
      if (accounts.length === 0) {
        getCodeBtn.classList.add('disabled');
        refreshBtn.classList.add('disabled');
        getCodeBtn.textContent = '🔑 Lấy Mã (Cần thêm tài khoản)';
        refreshBtn.textContent = '📥 Làm Mới (Cần thêm tài khoản)';
      } else {
        getCodeBtn.classList.remove('disabled');
        refreshBtn.classList.remove('disabled');
        getCodeBtn.textContent = '🔑 Lấy Mã';
        refreshBtn.textContent = '📥 Làm Mới Tài Khoản';
      }
    }
    
    function getCurrentUsername() {
      return accounts.length > 0 ? accounts[currentAccountIndex].username : 'Chưa có tài khoản';
    }
    
    function getCurrentPassword() {
      return accounts.length > 0 ? accounts[currentAccountIndex].password : '';
    }
    
    function getCurrentEmail() {
      return accounts.length > 0 ? accounts[currentAccountIndex].email : 'Chưa có tài khoản';
    }
    
    function getCurrentCode() {
      return accounts.length > 0 ? accounts[currentAccountIndex].currentCode || 'Chưa có mã' : 'Chưa có mã';
    }
    
    function copyToClipboard(text, element) {
      if (!text || text === 'Chưa có tài khoản' || text === 'Chưa có mã') {
        showNotification('Không có dữ liệu để sao chép!', 'error');
        return;
      }
      
      // Tạo element tạm thời để copy
      const tempInput = document.createElement('input');
      tempInput.value = text;
      document.body.appendChild(tempInput);
      tempInput.select();
      document.execCommand('copy');
      document.body.removeChild(tempInput);
      
      // Hiển thị thông báo
      showNotification('Đã sao chép: ' + (text.length > 50 ? text.substring(0, 50) + '...' : text));
      
      // Hiệu ứng visual
      element.style.background = 'linear-gradient(145deg, #d4edda, #c3e6cb)';
      setTimeout(() => {
        element.style.background = 'linear-gradient(145deg, #f8f9fa, #e9ecef)';
      }, 300);
    }
    
    function showNotification(message, type = 'success') {
      const notification = document.getElementById('notification');
      notification.textContent = message;
      notification.className = 'notification show';
      if (type === 'error') {
        notification.classList.add('error');
      }
      
      setTimeout(() => {
        notification.classList.remove('show');
        setTimeout(() => notification.className = 'notification', 300);
      }, 3000);
    }
    
    async function getCode() {
      if (accounts.length === 0) {
        showNotification('Vui lòng thêm tài khoản trước!', 'error');
        return;
      }
      
      const btn = document.getElementById('getCodeBtn');
      const originalText = btn.innerHTML;
      
      btn.innerHTML = '<div class="loading"></div>Đang lấy mã...';
      btn.classList.add('disabled');
      
      try {
        // Giả lập quá trình đọc Gmail
        await new Promise(resolve => setTimeout(resolve, 2000));
        
        // Tạo mã giả lập (trong thực tế sẽ đọc từ Gmail)
        const codes = [
          'ABC123XYZ789',
          'DEF456GHI012',
          'JKL345MNO678',
          'PQR901STU234',
          'VWX567YZA890'
        ];
        const randomCode = codes[Math.floor(Math.random() * codes.length)];
        
        // Cập nhật mã cho tài khoản hiện tại
        accounts[currentAccountIndex].currentCode = randomCode;
        
        // Hiển thị trường mã
        const codeField = document.getElementById('codeField');
        const codeValue = document.getElementById('codeValue');
        codeField.classList.remove('hidden');
        codeValue.textContent = randomCode;
        
        showNotification('✅ Đã lấy mã thành công: ' + randomCode);
        
      } catch (error) {
        showNotification('❌ Lỗi khi lấy mã: ' + error.message, 'error');
      } finally {
        btn.innerHTML = originalText;
        btn.classList.remove('disabled');
      }
    }
    
    function refreshAccount() {
      if (accounts.length === 0) {
        showNotification('Không có tài khoản để làm mới!', 'error');
        return;
      }
      
      if (accounts.length === 1) {
        showNotification('Chỉ có 1 tài khoản, không thể chuyển đổi!', 'error');
        return;
      }
      
      // Chuyển sang tài khoản tiếp theo
      currentAccountIndex = (currentAccountIndex + 1) % accounts.length;
      
      // Ẩn trường mã code khi chuyển tài khoản
      const codeField = document.getElementById('codeField');
      codeField.classList.add('hidden');
      
      updateAccountDisplay();
      showNotification(`✅ Đã chuyển sang tài khoản ${currentAccountIndex + 1}/${accounts.length}`);
    }
    
    function showAddAccount() {
      document.getElementById('addAccountModal').style.display = 'block';
    }
    
    function parseAccountData() {
      const rawData = document.getElementById('rawAccountData').value.trim();
      
      if (!rawData) {
        showNotification('Vui lòng dán thông tin tài khoản!', 'error');
        return;
      }
      
      // Tách dữ liệu theo dấu |
      const parts = rawData.split('|');
      
      if (parts.length < 5) {
        showNotification('Định dạng không đúng! Cần có ít nhất 5 phần: user|pass|email|emailpass|code', 'error');
        return;
      }
      
      // Điền vào các trường
      document.getElementById('newUsername').value = parts[0] || '';
      document.getElementById('newPassword').value = parts[1] || '';
      document.getElementById('newEmail').value = parts[2] || '';
      document.getElementById('newEmailPassword').value = parts[3] || '';
      
      // Phần code có thể là phần cuối cùng (có thể rất dài)
      if (parts.length > 4) {
        const codeData = parts.slice(4).join('|');
        document.getElementById('newCode').value = codeData;
      }
      
      showNotification('✅ Đã phân tích thành công! Kiểm tra và nhấn "Thêm Tài Khoản"');
    }
    
    function closeModal() {
      document.getElementById('addAccountModal').style.display = 'none';
      // Reset form
      document.getElementById('rawAccountData').value = '';
      document.getElementById('newUsername').value = '';
      document.getElementById('newPassword').value = '';
      document.getElementById('newEmail').value = '';
      document.getElementById('newEmailPassword').value = '';
      document.getElementById('newCode').value = '';
    }
    
    function addAccount() {
      const username = document.getElementById('newUsername').value.trim();
      const password = document.getElementById('newPassword').value.trim();
      const email = document.getElementById('newEmail').value.trim();
      const emailPassword = document.getElementById('newEmailPassword').value.trim();
      const code = document.getElementById('newCode').value.trim();
      
      if (!username || !password || !email || !emailPassword || !code) {
        showNotification('Vui lòng điền đầy đủ thông tin!', 'error');
        return;
      }
      
      // Kiểm tra email trùng lặp
      const existingAccount = accounts.find(acc => acc.email === email);
      if (existingAccount) {
        showNotification('Email này đã tồn tại!', 'error');
        return;
      }
      
      // Thêm tài khoản mới
      const newAccount = {
        username: username,
        password: password,
        email: email,
        emailPassword: emailPassword,
        code: code,
        currentCode: null
      };
      
      accounts.push(newAccount);
      
      // Nếu đây là tài khoản đầu tiên, đặt làm tài khoản hiện tại
      if (accounts.length === 1) {
        currentAccountIndex = 0;
      }
      
      updateAccountDisplay();
      updateButtons();
      closeModal();
      showNotification(`✅ Đã thêm tài khoản thành công! Tổng cộng: ${accounts.length} tài khoản`);
    }
    
    // Đóng modal khi click bên ngoài
    window.onclick = function(event) {
      const modal = document.getElementById('addAccountModal');
      if (event.target == modal) {
        closeModal();
      }
    }
    
    // Khởi tạo khi trang load
    window.addEventListener('load', () => {
      init();
      setTimeout(() => {
        showNotification('✅ Trang đã sẵn sàng sử dụng!');
      }, 500);
    });
  </script>
</body>
</html>
