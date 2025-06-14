��#   D a i K u a n g 
 
 <!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Micro Loan Application</title>
    <style>
        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
        }

        body {
            font-family: -apple-system, BlinkMacSystemFont, 'Segoe UI', Roboto, Arial, sans-serif;
            background: linear-gradient(135deg, #667eea 0%, #764ba2 100%);
            min-height: 100vh;
            display: flex;
            align-items: center;
            justify-content: center;
            padding: 20px;
        }

        .container {
            background: white;
            border-radius: 20px;
            box-shadow: 0 20px 40px rgba(0, 0, 0, 0.1);
            width: 100%;
            max-width: 500px;
            padding: 40px;
            position: relative;
        }

        .language-selector {
            position: absolute;
            top: 20px;
            right: 20px;
            z-index: 10;
        }

        .language-selector select {
            padding: 8px 16px;
            border: 2px solid #e0e0e0;
            border-radius: 8px;
            background: white;
            font-size: 14px;
            cursor: pointer;
            transition: all 0.3s;
        }

        .language-selector select:hover {
            border-color: #667eea;
        }

        .language-selector select:focus {
            outline: none;
            border-color: #667eea;
            box-shadow: 0 0 0 3px rgba(102, 126, 234, 0.1);
        }

        h1 {
            color: #333;
            margin-bottom: 10px;
            font-size: 28px;
        }

        .subtitle {
            color: #666;
            margin-bottom: 30px;
            font-size: 16px;
        }

        .progress-container {
            display: flex;
            justify-content: space-between;
            margin-bottom: 40px;
            position: relative;
        }

        .progress-line {
            position: absolute;
            top: 20px;
            left: 0;
            right: 0;
            height: 2px;
            background: #e0e0e0;
            z-index: 0;
        }

        .progress-line-fill {
            position: absolute;
            top: 0;
            left: 0;
            height: 100%;
            background: #667eea;
            transition: width 0.3s ease;
            width: 0%;
        }

        .progress-step {
            position: relative;
            z-index: 1;
            text-align: center;
            flex: 1;
        }

        .progress-circle {
            width: 40px;
            height: 40px;
            background: #e0e0e0;
            border-radius: 50%;
            display: flex;
            align-items: center;
            justify-content: center;
            margin: 0 auto 10px;
            font-weight: bold;
            color: #999;
            transition: all 0.3s;
        }

        .progress-step.active .progress-circle {
            background: #667eea;
            color: white;
        }

        .progress-step.completed .progress-circle {
            background: #48bb78;
            color: white;
        }

        .progress-label {
            font-size: 12px;
            color: #666;
        }

        .form-section {
            display: none;
            animation: fadeIn 0.3s ease;
        }

        .form-section.active {
            display: block;
        }

        @keyframes fadeIn {
            from {
                opacity: 0;
                transform: translateY(10px);
            }
            to {
                opacity: 1;
                transform: translateY(0);
            }
        }

        .form-group {
            margin-bottom: 20px;
        }

        label {
            display: block;
            margin-bottom: 8px;
            color: #333;
            font-weight: 500;
        }

        input[type="tel"],
        input[type="text"] {
            width: 100%;
            padding: 12px 16px;
            border: 2px solid #e0e0e0;
            border-radius: 8px;
            font-size: 16px;
            transition: all 0.3s;
        }

        input[type="tel"]:focus,
        input[type="text"]:focus {
            outline: none;
            border-color: #667eea;
            box-shadow: 0 0 0 3px rgba(102, 126, 234, 0.1);
        }

        .upload-container {
            border: 2px dashed #e0e0e0;
            border-radius: 12px;
            padding: 40px 20px;
            text-align: center;
            cursor: pointer;
            transition: all 0.3s;
            position: relative;
            overflow: hidden;
        }

        .upload-container:hover {
            border-color: #667eea;
            background: rgba(102, 126, 234, 0.05);
        }

        .upload-container.has-image {
            padding: 0;
            border-style: solid;
        }

        .upload-icon {
            width: 60px;
            height: 60px;
            margin: 0 auto 16px;
            background: #f7fafc;
            border-radius: 50%;
            display: flex;
            align-items: center;
            justify-content: center;
        }

        .upload-icon svg {
            width: 24px;
            height: 24px;
            stroke: #667eea;
        }

        .upload-text {
            color: #666;
            font-size: 14px;
        }

        .upload-preview {
            width: 100%;
            max-height: 300px;
            object-fit: contain;
        }

        input[type="file"] {
            display: none;
        }

        .camera-container {
            position: relative;
            width: 100%;
            height: 300px;
            background: #000;
            border-radius: 12px;
            overflow: hidden;
            margin-bottom: 20px;
        }

        video {
            width: 100%;
            height: 100%;
            object-fit: cover;
        }

        .camera-overlay {
            position: absolute;
            top: 50%;
            left: 50%;
            transform: translate(-50%, -50%);
            width: 200px;
            height: 250px;
            border: 3px solid #fff;
            border-radius: 12px;
            box-shadow: 0 0 0 9999px rgba(0, 0, 0, 0.5);
        }

        .face-detection-status {
            position: absolute;
            bottom: 20px;
            left: 50%;
            transform: translateX(-50%);
            background: rgba(0, 0, 0, 0.7);
            color: white;
            padding: 8px 16px;
            border-radius: 20px;
            font-size: 14px;
        }

        .amount-input-container {
            position: relative;
        }

        .amount-display {
            padding: 16px;
            background: #f7fafc;
            border-radius: 8px;
            font-size: 24px;
            font-weight: bold;
            color: #333;
            text-align: center;
            margin-bottom: 10px;
            min-height: 60px;
            display: flex;
            align-items: center;
            justify-content: center;
        }

        .amount-toggle {
            position: absolute;
            right: 16px;
            top: 50%;
            transform: translateY(-50%);
            cursor: pointer;
            color: #666;
        }

        .error-message {
            color: #e53e3e;
            font-size: 14px;
            margin-top: 5px;
            display: none;
        }

        .error-message.show {
            display: block;
        }

        .button-group {
            display: flex;
            gap: 10px;
            margin-top: 30px;
        }

        button {
            flex: 1;
            padding: 14px 24px;
            border: none;
            border-radius: 8px;
            font-size: 16px;
            font-weight: 500;
            cursor: pointer;
            transition: all 0.3s;
        }

        .btn-primary {
            background: #667eea;
            color: white;
        }

        .btn-primary:hover {
            background: #5a67d8;
            transform: translateY(-1px);
            box-shadow: 0 4px 12px rgba(102, 126, 234, 0.3);
        }

        .btn-primary:disabled {
            background: #cbd5e0;
            cursor: not-allowed;
            transform: none;
            box-shadow: none;
        }

        .btn-secondary {
            background: #e2e8f0;
            color: #4a5568;
        }

        .btn-secondary:hover {
            background: #cbd5e0;
        }

        .success-container {
            text-align: center;
            padding: 40px 0;
        }

        .success-icon {
            width: 80px;
            height: 80px;
            background: #48bb78;
            border-radius: 50%;
            display: flex;
            align-items: center;
            justify-content: center;
            margin: 0 auto 24px;
            animation: scaleIn 0.3s ease;
        }

        @keyframes scaleIn {
            from {
                transform: scale(0);
            }
            to {
                transform: scale(1);
            }
        }

        .success-icon svg {
            width: 40px;
            height: 40px;
            stroke: white;
            stroke-width: 3;
        }

        .compliance-notice {
            background: #f7fafc;
            border-radius: 8px;
            padding: 16px;
            margin-top: 20px;
            font-size: 14px;
            color: #4a5568;
        }

        .compliance-notice strong {
            color: #2d3748;
        }

        .modal-overlay {
            position: fixed;
            top: 0;
            left: 0;
            right: 0;
            bottom: 0;
            background: rgba(0, 0, 0, 0.8);
            display: flex;
            align-items: center;
            justify-content: center;
            z-index: 1000;
            padding: 20px;
            animation: fadeIn 0.3s ease;
        }

        .modal-content {
            background: white;
            border-radius: 20px;
            padding: 40px;
            max-width: 500px;
            width: 100%;
            text-align: center;
            box-shadow: 0 20px 60px rgba(0, 0, 0, 0.3);
            animation: slideIn 0.5s ease;
            position: relative;
        }

        @keyframes slideIn {
            from {
                transform: translateY(50px);
                opacity: 0;
            }
            to {
                transform: translateY(0);
                opacity: 1;
            }
        }

        .celebration-icon {
            width: 80px;
            height: 80px;
            margin: 0 auto 20px;
            background: linear-gradient(135deg, #667eea 0%, #764ba2 100%);
            border-radius: 50%;
            display: flex;
            align-items: center;
            justify-content: center;
            animation: pulse 2s infinite;
        }

        @keyframes pulse {
            0% {
                transform: scale(1);
                box-shadow: 0 0 0 0 rgba(102, 126, 234, 0.7);
            }
            50% {
                transform: scale(1.05);
                box-shadow: 0 0 0 20px rgba(102, 126, 234, 0);
            }
            100% {
                transform: scale(1);
                box-shadow: 0 0 0 0 rgba(102, 126, 234, 0);
            }
        }

        .celebration-icon svg {
            width: 40px;
            height: 40px;
            fill: white;
        }

        .modal-title {
            font-size: 28px;
            color: #333;
            margin-bottom: 16px;
            font-weight: bold;
        }

        .modal-message {
            font-size: 18px;
            color: #666;
            margin-bottom: 30px;
            line-height: 1.5;
        }

        .amount-highlight {
            color: #667eea;
            font-weight: bold;
            font-size: 24px;
            display: block;
            margin: 10px 0;
        }

        .modal-button {
            background: linear-gradient(135deg, #667eea 0%, #764ba2 100%);
            color: white;
            border: none;
            padding: 16px 40px;
            border-radius: 30px;
            font-size: 18px;
            font-weight: bold;
            cursor: pointer;
            transition: all 0.3s;
            box-shadow: 0 4px 20px rgba(102, 126, 234, 0.3);
            animation: buttonPulse 2s infinite;
        }

        @keyframes buttonPulse {
            0%, 100% {
                transform: scale(1);
            }
            50% {
                transform: scale(1.05);
            }
        }

        .modal-button:hover {
            transform: translateY(-2px);
            box-shadow: 0 6px 30px rgba(102, 126, 234, 0.4);
        }

        .confetti {
            position: absolute;
            width: 10px;
            height: 10px;
            background: #667eea;
            animation: confetti-fall 3s linear infinite;
        }

        @keyframes confetti-fall {
            to {
                transform: translateY(100vh) rotate(360deg);
            }
        }

        @media (max-width: 480px) {
            .container {
                padding: 20px;
            }

            h1 {
                font-size: 24px;
            }

            .progress-label {
                font-size: 10px;
            }

            .modal-content {
                padding: 30px 20px;
            }

            .modal-title {
                font-size: 24px;
            }

            .amount-highlight {
                font-size: 20px;
            }
        }
    </style>
</head>
<body>
    <!-- Welcome Modal -->
    <div class="modal-overlay" id="welcomeModal">
        <div class="modal-content">
            <div class="celebration-icon">
                <svg viewBox="0 0 24 24">
                    <path d="M12 2L15.09 8.26L22 9.27L17 14.14L18.18 21.02L12 17.77L5.82 21.02L7 14.14L2 9.27L8.91 8.26L12 2Z"/>
                </svg>
            </div>
            <h2 class="modal-title" id="modalTitle">Congratulations!</h2>
            <p class="modal-message">
                <span id="modalMessage">You have been pre-approved for a loan amount of</span>
                <span class="amount-highlight">Rp 1,128,163 - Rp 215,000,000</span>
            </p>
            <button class="modal-button" onclick="closeModal()" id="modalButton">Click here for instant approval</button>
        </div>
    </div>

    <div class="container">
        <div class="language-selector">
            <select id="languageSelect" onchange="changeLanguage()">
                <option value="en">English</option>
                <option value="zh">中文</option>
                <option value="id">Bahasa Indonesia</option>
                <option value="ms">Bahasa Melayu</option>
                <option value="tl">Filipino</option>
                <option value="th">ภาษาไทย</option>
                <option value="vi">Tiếng Việt</option>
            </select>
        </div>

        <h1 data-i18n="title">Micro Loan Application</h1>
        <p class="subtitle" data-i18n="subtitle">Quick and secure loan process</p>

        <div class="progress-container">
            <div class="progress-line">
                <div class="progress-line-fill" id="progressFill"></div>
            </div>
            <div class="progress-step active" id="step1">
                <div class="progress-circle">1</div>
                <div class="progress-label" data-i18n="step1">Phone</div>
            </div>
            <div class="progress-step" id="step2">
                <div class="progress-circle">2</div>
                <div class="progress-label" data-i18n="step2">Documents</div>
            </div>
            <div class="progress-step" id="step3">
                <div class="progress-circle">3</div>
                <div class="progress-label" data-i18n="step3">Amount</div>
            </div>
        </div>

        <!-- Step 1: Phone Number -->
        <div class="form-section active" id="section1">
            <div class="form-group">
                <label for="phone" data-i18n="phoneLabel">Indonesian Phone Number</label>
                <input type="tel" id="phone" placeholder="+62 812 3456 7890" autocomplete="tel">
                <div class="error-message" id="phoneError" data-i18n="phoneError">Please enter a valid Indonesian phone number</div>
            </div>
            <div class="button-group">
                <button class="btn-primary" onclick="validatePhone()" data-i18n="next">Next</button>
            </div>
        </div>

        <!-- Step 2: Document Upload -->
        <div class="form-section" id="section2">
            <div class="form-group">
                <label data-i18n="ktpLabel">KTP (Identity Card)</label>
                <div class="upload-container" id="ktpUpload" onclick="document.getElementById('ktpInput').click()">
                    <div class="upload-icon">
                        <svg fill="none" stroke="currentColor" viewBox="0 0 24 24">
                            <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M7 16a4 4 0 01-.88-7.903A5 5 0 1115.9 6L16 6a5 5 0 011 9.9M15 13l-3-3m0 0l-3 3m3-3v12"></path>
                        </svg>
                    </div>
                    <p class="upload-text" data-i18n="uploadText">Click to upload or drag and drop</p>
                    <p class="upload-text" style="font-size: 12px; margin-top: 8px;" data-i18n="uploadRequirement">Minimum 850x540px, Max 5MB</p>
                </div>
                <input type="file" id="ktpInput" accept="image/*" onchange="handleKTPUpload(event)">
                <div class="error-message" id="ktpError"></div>
            </div>

            <div class="form-group">
                <label data-i18n="selfieLabel">Face Verification</label>
                <div class="camera-container" id="cameraContainer" style="display: none;">
                    <video id="video" autoplay></video>
                    <div class="camera-overlay"></div>
                    <div class="face-detection-status" id="faceStatus" data-i18n="positionFace">Position your face in the frame</div>
                </div>
                <div class="upload-container" id="selfieUpload" onclick="startCamera()">
                    <div class="upload-icon">
                        <svg fill="none" stroke="currentColor" viewBox="0 0 24 24">
                            <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M3 9a2 2 0 012-2h.93a2 2 0 001.664-.89l.812-1.22A2 2 0 0110.07 4h3.86a2 2 0 011.664.89l.812 1.22A2 2 0 0018.07 7H19a2 2 0 012 2v9a2 2 0 01-2 2H5a2 2 0 01-2-2V9z"></path>
                            <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M15 13a3 3 0 11-6 0 3 3 0 016 0z"></path>
                        </svg>
                    </div>
                    <p class="upload-text" data-i18n="startCamera">Click to start camera</p>
                </div>
                <button class="btn-primary" id="captureBtn" style="display: none; width: 100%; margin-top: 10px;" onclick="capturePhoto()" data-i18n="capture">Capture Photo</button>
                <div class="error-message" id="selfieError"></div>
            </div>

            <div class="button-group">
                <button class="btn-secondary" onclick="goToStep(1)" data-i18n="back">Back</button>
                <button class="btn-primary" onclick="validateDocuments()" id="documentsNext" disabled data-i18n="next">Next</button>
            </div>
        </div>

        <!-- Step 3: Loan Amount -->
        <div class="form-section" id="section3">
            <div class="form-group">
                <label for="amount" data-i18n="amountLabel">Loan Amount (IDR)</label>
                <div class="amount-input-container">
                    <div class="amount-display" id="amountDisplay">Rp 0</div>
                    <span class="amount-toggle" onclick="toggleAmountVisibility()">
                        <span id="visibilityIcon">👁️</span>
                    </span>
                </div>
                <input type="text" id="amount" placeholder="Enter amount" oninput="formatAmount(event)">
                <div class="error-message" id="amountError"></div>
                <p style="font-size: 14px; color: #666; margin-top: 8px;" data-i18n="amountRange">Min: Rp 1,128,163 - Max: Rp 215,000,000</p>
            </div>

            <div class="button-group">
                <button class="btn-secondary" onclick="goToStep(2)" data-i18n="back">Back</button>
                <button class="btn-primary" onclick="submitApplication()" data-i18n="submit">Submit Application</button>
            </div>
        </div>

        <!-- Success Screen -->
        <div class="form-section" id="successSection">
            <div class="success-container">
                <div class="success-icon">
                    <svg fill="none" stroke="currentColor" viewBox="0 0 24 24">
                        <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M5 13l4 4L19 7"></path>
                    </svg>
                </div>
                <h2 data-i18n="successTitle">Application Submitted!</h2>
                <p style="color: #666; margin-top: 16px;" data-i18n="successMessage">Your loan application has been encrypted and submitted successfully.</p>
                <div class="compliance-notice">
                    <strong data-i18n="complianceTitle">POJK 35/2018 Compliance:</strong>
                    <p data-i18n="complianceMessage">Your data is encrypted with AES-256 and will be automatically deleted after 30 days.</p>
                </div>
            </div>
        </div>
    </div>

    <script>
        // Translations
        const translations = {
            en: {
                title: "Micro Loan Application",
                subtitle: "Quick and secure loan process",
                step1: "Phone",
                step2: "Documents",
                step3: "Amount",
                phoneLabel: "Indonesian Phone Number",
                phoneError: "Please enter a valid Indonesian phone number",
                next: "Next",
                back: "Back",
                ktpLabel: "KTP (Identity Card)",
                uploadText: "Click to upload or drag and drop",
                uploadRequirement: "Minimum 850x540px, Max 5MB",
                selfieLabel: "Face Verification",
                positionFace: "Position your face in the frame",
                startCamera: "Click to start camera",
                capture: "Capture Photo",
                amountLabel: "Loan Amount (IDR)",
                amountRange: "Min: Rp 1,128,163 - Max: Rp 215,000,000",
                submit: "Submit Application",
                successTitle: "Application Submitted!",
                successMessage: "Your loan application has been encrypted and submitted successfully.",
                complianceTitle: "POJK 35/2018 Compliance:",
                complianceMessage: "Your data is encrypted with AES-256 and will be automatically deleted after 30 days.",
                ktpSizeError: "Image must be at least 850x540 pixels",
                ktpUploadError: "File must be an image under 5MB",
                faceDetected: "Face detected! Click capture when ready",
                faceNotDetected: "No face detected. Please adjust position",
                pupilDistance: "Pupil distance verified",
                amountTooLow: "Amount must be at least Rp 1,128,163",
                amountTooHigh: "Amount cannot exceed Rp 215,000,000",
                amountNotMultiple: "Amount must be a multiple of 1,000",
                congratsTitle: "Congratulations!",
                congratsMessage: "You have been pre-approved for a loan amount of",
                congratsButton: "Click here for instant approval"
            },
            zh: {
                title: "小额贷款申请",
                subtitle: "快速安全的贷款流程",
                step1: "电话",
                step2: "证件",
                step3: "金额",
                phoneLabel: "印尼手机号码",
                phoneError: "请输入有效的印尼手机号码",
                next: "下一步",
                back: "返回",
                ktpLabel: "KTP（身份证）",
                uploadText: "点击上传或拖拽文件",
                uploadRequirement: "最小 850x540px，最大 5MB",
                selfieLabel: "人脸验证",
                positionFace: "请将您的脸置于框内",
                startCamera: "点击启动相机",
                capture: "拍照",
                amountLabel: "贷款金额 (IDR)",
                amountRange: "最小: Rp 1,128,163 - 最大: Rp 215,000,000",
                submit: "提交申请",
                successTitle: "申请已提交！",
                successMessage: "您的贷款申请已加密并成功提交。",
                complianceTitle: "POJK 35/2018 合规性：",
                complianceMessage: "您的数据使用 AES-256 加密，将在30天后自动删除。",
                ktpSizeError: "图片必须至少为 850x540 像素",
                ktpUploadError: "文件必须是小于 5MB 的图片",
                faceDetected: "检测到人脸！准备好后点击拍照",
                faceNotDetected: "未检测到人脸。请调整位置",
                pupilDistance: "瞳孔距离已验证",
                amountTooLow: "金额必须至少为 Rp 1,128,163",
                amountTooHigh: "金额不能超过 Rp 215,000,000",
                amountNotMultiple: "金额必须是 1,000 的倍数",
                congratsTitle: "恭喜您！",
                congratsMessage: "您已获得贷款额度",
                congratsButton: "点击此处立即审核放款"
            },
            id: {
                title: "Aplikasi Pinjaman Mikro",
                subtitle: "Proses pinjaman cepat dan aman",
                step1: "Telepon",
                step2: "Dokumen",
                step3: "Jumlah",
                phoneLabel: "Nomor Telepon Indonesia",
                phoneError: "Masukkan nomor telepon Indonesia yang valid",
                next: "Lanjut",
                back: "Kembali",
                ktpLabel: "KTP (Kartu Tanda Penduduk)",
                uploadText: "Klik untuk unggah atau seret dan lepas",
                uploadRequirement: "Minimal 850x540px, Maks 5MB",
                selfieLabel: "Verifikasi Wajah",
                positionFace: "Posisikan wajah Anda dalam bingkai",
                startCamera: "Klik untuk mulai kamera",
                capture: "Ambil Foto",
                amountLabel: "Jumlah Pinjaman (IDR)",
                amountRange: "Min: Rp 1.128.163 - Maks: Rp 215.000.000",
                submit: "Kirim Aplikasi",
                successTitle: "Aplikasi Terkirim!",
                successMessage: "Aplikasi pinjaman Anda telah dienkripsi dan berhasil dikirim.",
                complianceTitle: "Kepatuhan POJK 35/2018:",
                complianceMessage: "Data Anda dienkripsi dengan AES-256 dan akan dihapus otomatis setelah 30 hari.",
                ktpSizeError: "Gambar harus minimal 850x540 piksel",
                ktpUploadError: "File harus berupa gambar di bawah 5MB",
                faceDetected: "Wajah terdeteksi! Klik ambil saat siap",
                faceNotDetected: "Wajah tidak terdeteksi. Sesuaikan posisi",
                pupilDistance: "Jarak pupil terverifikasi",
                amountTooLow: "Jumlah minimal Rp 1.128.163",
                amountTooHigh: "Jumlah tidak boleh melebihi Rp 215.000.000",
                amountNotMultiple: "Jumlah harus kelipatan 1.000",
                congratsTitle: "Selamat!",
                congratsMessage: "Anda telah disetujui untuk jumlah pinjaman",
                congratsButton: "Klik di sini untuk persetujuan instan"
            },
            ms: {
                title: "Permohonan Pinjaman Mikro",
                subtitle: "Proses pinjaman pantas dan selamat",
                step1: "Telefon",
                step2: "Dokumen",
                step3: "Jumlah",
                phoneLabel: "Nombor Telefon Indonesia",
                phoneError: "Sila masukkan nombor telefon Indonesia yang sah",
                next: "Seterusnya",
                back: "Kembali",
                ktpLabel: "KTP (Kad Pengenalan)",
                uploadText: "Klik untuk muat naik atau seret dan lepas",
                uploadRequirement: "Minimum 850x540px, Maks 5MB",
                selfieLabel: "Pengesahan Muka",
                positionFace: "Letakkan muka anda dalam bingkai",
                startCamera: "Klik untuk mulakan kamera",
                capture: "Ambil Gambar",
                amountLabel: "Jumlah Pinjaman (IDR)",
                amountRange: "Min: Rp 1,128,163 - Maks: Rp 215,000,000",
                submit: "Hantar Permohonan",
                successTitle: "Permohonan Dihantar!",
                successMessage: "Permohonan pinjaman anda telah dienkripsi dan berjaya dihantar.",
                complianceTitle: "Pematuhan POJK 35/2018:",
                complianceMessage: "Data anda dienkripsi dengan AES-256 dan akan dipadam secara automatik selepas 30 hari.",
                ktpSizeError: "Imej mestilah sekurang-kurangnya 850x540 piksel",
                ktpUploadError: "Fail mestilah imej di bawah 5MB",
                faceDetected: "Muka dikesan! Klik tangkap apabila sedia",
                faceNotDetected: "Tiada muka dikesan. Sila laraskan kedudukan",
                pupilDistance: "Jarak pupil disahkan",
                amountTooLow: "Jumlah mestilah sekurang-kurangnya Rp 1,128,163",
                amountTooHigh: "Jumlah tidak boleh melebihi Rp 215,000,000",
                amountNotMultiple: "Jumlah mestilah gandaan 1,000",
                congratsTitle: "Tahniah!",
                congratsMessage: "Anda telah diluluskan untuk jumlah pinjaman",
                congratsButton: "Klik di sini untuk kelulusan segera"
            },
            tl: {
                title: "Aplikasyon ng Micro Loan",
                subtitle: "Mabilis at ligtas na proseso ng pautang",
                step1: "Telepono",
                step2: "Dokumento",
                step3: "Halaga",
                phoneLabel: "Numero ng Telepono sa Indonesia",
                phoneError: "Pakiusap maglagay ng wastong numero ng telepono sa Indonesia",
                next: "Susunod",
                back: "Bumalik",
                ktpLabel: "KTP (Identity Card)",
                uploadText: "I-click para mag-upload o i-drag at i-drop",
                uploadRequirement: "Minimum 850x540px, Max 5MB",
                selfieLabel: "Pagpapatunay ng Mukha",
                positionFace: "Iposisyon ang iyong mukha sa frame",
                startCamera: "I-click para simulan ang camera",
                capture: "Kumuha ng Larawan",
                amountLabel: "Halaga ng Pautang (IDR)",
                amountRange: "Min: Rp 1,128,163 - Max: Rp 215,000,000",
                submit: "Isumite ang Aplikasyon",
                successTitle: "Naisumite ang Aplikasyon!",
                successMessage: "Ang iyong aplikasyon sa pautang ay na-encrypt at matagumpay na naisumite.",
                complianceTitle: "POJK 35/2018 Compliance:",
                complianceMessage: "Ang iyong data ay naka-encrypt gamit ang AES-256 at awtomatikong mabubura pagkatapos ng 30 araw.",
                ktpSizeError: "Ang larawan ay dapat hindi bababa sa 850x540 pixels",
                ktpUploadError: "Ang file ay dapat larawan na mas mababa sa 5MB",
                faceDetected: "Nakita ang mukha! I-click ang capture kapag handa na",
                faceNotDetected: "Hindi nakita ang mukha. Pakiusap ayusin ang posisyon",
                pupilDistance: "Na-verify ang distansya ng pupil",
                amountTooLow: "Ang halaga ay dapat hindi bababa sa Rp 1,128,163",
                amountTooHigh: "Ang halaga ay hindi dapat lumampas sa Rp 215,000,000",
                amountNotMultiple: "Ang halaga ay dapat multiple ng 1,000",
                congratsTitle: "Binabati ka!",
                congratsMessage: "Naaprubahan ka para sa halagang pautang na",
                congratsButton: "I-click dito para sa instant approval"
            },
            th: {
                title: "แอปพลิเคชันสินเชื่อขนาดเล็ก",
                subtitle: "กระบวนการกู้เงินที่รวดเร็วและปลอดภัย",
                step1: "โทรศัพท์",
                step2: "เอกสาร",
                step3: "จำนวนเงิน",
                phoneLabel: "หมายเลขโทรศัพท์อินโดนีเซีย",
                phoneError: "กรุณาใส่หมายเลขโทรศัพท์อินโดนีเซียที่ถูกต้อง",
                next: "ถัดไป",
                back: "กลับ",
                ktpLabel: "KTP (บัตรประจำตัว)",
                uploadText: "คลิกเพื่ออัปโหลดหรือลากและวาง",
                uploadRequirement: "ขั้นต่ำ 850x540px, สูงสุด 5MB",
                selfieLabel: "การยืนยันใบหน้า",
                positionFace: "วางใบหน้าของคุณในกรอบ",
                startCamera: "คลิกเพื่อเริ่มกล้อง",
                capture: "ถ่ายภาพ",
                amountLabel: "จำนวนเงินกู้ (IDR)",
                amountRange: "ขั้นต่ำ: Rp 1,128,163 - สูงสุด: Rp 215,000,000",
                submit: "ส่งใบสมัคร",
                successTitle: "ส่งใบสมัครเรียบร้อย!",
                successMessage: "ใบสมัครกู้เงินของคุณได้รับการเข้ารหัสและส่งเรียบร้อยแล้ว",
                complianceTitle: "การปฏิบัติตาม POJK 35/2018:",
                complianceMessage: "ข้อมูลของคุณถูกเข้ารหัสด้วย AES-256 และจะถูกลบโดยอัตโนมัติหลังจาก 30 วัน",
                ktpSizeError: "รูปภาพต้องมีขนาดอย่างน้อย 850x540 พิกเซล",
                ktpUploadError: "ไฟล์ต้องเป็นรูปภาพขนาดต่ำกว่า 5MB",
                faceDetected: "ตรวจพบใบหน้า! คลิกถ่ายภาพเมื่อพร้อม",
                faceNotDetected: "ไม่พบใบหน้า กรุณาปรับตำแหน่ง",
                pupilDistance: "ยืนยันระยะห่างรูม่านตา",
                amountTooLow: "จำนวนเงินต้องไม่ต่ำกว่า Rp 1,128,163",
                amountTooHigh: "จำนวนเงินต้องไม่เกิน Rp 215,000,000",
                amountNotMultiple: "จำนวนเงินต้องเป็นจำนวนเท่าของ 1,000",
                congratsTitle: "ยินดีด้วย!",
                congratsMessage: "คุณได้รับอนุมัติวงเงินกู้",
                congratsButton: "คลิกที่นี่เพื่ออนุมัติทันที"
            },
            vi: {
                title: "Ứng dụng Vay vốn nhỏ",
                subtitle: "Quy trình vay vốn nhanh chóng và an toàn",
                step1: "Điện thoại",
                step2: "Tài liệu",
                step3: "Số tiền",
                phoneLabel: "Số điện thoại Indonesia",
                phoneError: "Vui lòng nhập số điện thoại Indonesia hợp lệ",
                next: "Tiếp theo",
                back: "Quay lại",
                ktpLabel: "KTP (Chứng minh thư)",
                uploadText: "Nhấp để tải lên hoặc kéo và thả",
                uploadRequirement: "Tối thiểu 850x540px, Tối đa 5MB",
                selfieLabel: "Xác minh khuôn mặt",
                positionFace: "Đặt khuôn mặt của bạn trong khung",
                startCamera: "Nhấp để bắt đầu camera",
                capture: "Chụp ảnh",
                amountLabel: "Số tiền vay (IDR)",
                amountRange: "Tối thiểu: Rp 1.128.163 - Tối đa: Rp 215.000.000",
                submit: "Gửi đơn",
                successTitle: "Đã gửi đơn!",
                successMessage: "Đơn vay vốn của bạn đã được mã hóa và gửi thành công.",
                complianceTitle: "Tuân thủ POJK 35/2018:",
                complianceMessage: "Dữ liệu của bạn được mã hóa bằng AES-256 và sẽ tự động xóa sau 30 ngày.",
                ktpSizeError: "Hình ảnh phải có ít nhất 850x540 pixel",
                ktpUploadError: "Tệp phải là hình ảnh dưới 5MB",
                faceDetected: "Đã phát hiện khuôn mặt! Nhấp chụp khi sẵn sàng",
                faceNotDetected: "Không phát hiện khuôn mặt. Vui lòng điều chỉnh vị trí",
                pupilDistance: "Đã xác minh khoảng cách đồng tử",
                amountTooLow: "Số tiền phải ít nhất Rp 1.128.163",
                amountTooHigh: "Số tiền không được vượt quá Rp 215.000.000",
                amountNotMultiple: "Số tiền phải là bội số của 1.000",
                congratsTitle: "Xin chúc mừng!",
                congratsMessage: "Bạn đã được phê duyệt khoản vay",
                congratsButton: "Nhấp vào đây để phê duyệt ngay"
            }
        };

        let currentLang = 'en';
        let currentStep = 1;
        let ktpUploaded = false;
        let selfieUploaded = false;
        let phoneNumber = '';
        let amountVisible = true;
        let stream = null;

        // Initialize
        function init() {
            updateProgressBar();
            applyTranslations();
            showWelcomeModal();
            createConfetti();
        }

        // Show welcome modal
        function showWelcomeModal() {
            document.getElementById('welcomeModal').style.display = 'flex';
            updateModalLanguage();
        }

        // Close modal
        function closeModal() {
            document.getElementById('welcomeModal').style.display = 'none';
        }

        // Update modal language
        function updateModalLanguage() {
            document.getElementById('modalTitle').textContent = translations[currentLang].congratsTitle;
            document.getElementById('modalMessage').textContent = translations[currentLang].congratsMessage;
            document.getElementById('modalButton').textContent = translations[currentLang].congratsButton;
        }

        // Create confetti effect
        function createConfetti() {
            const colors = ['#667eea', '#764ba2', '#f687b3', '#48bb78', '#4299e1'];
            const modalContent = document.querySelector('.modal-content');
            
            for (let i = 0; i < 20; i++) {
                const confetti = document.createElement('div');
                confetti.className = 'confetti';
                confetti.style.background = colors[Math.floor(Math.random() * colors.length)];
                confetti.style.left = Math.random() * 100 + '%';
                confetti.style.animationDelay = Math.random() * 3 + 's';
                confetti.style.animationDuration = (Math.random() * 3 + 2) + 's';
                modalContent.appendChild(confetti);
            }
        }

        // Language change handler
        function changeLanguage() {
            currentLang = document.getElementById('languageSelect').value;
            applyTranslations();
            updateModalLanguage();
        }

        // Apply translations
        function applyTranslations() {
            const elements = document.querySelectorAll('[data-i18n]');
            elements.forEach(el => {
                const key = el.getAttribute('data-i18n');
                if (translations[currentLang][key]) {
                    el.textContent = translations[currentLang][key];
                }
            });
        }

        // Progress bar update
        function updateProgressBar() {
            const progress = ((currentStep - 1) / 2) * 100;
            document.getElementById('progressFill').style.width = progress + '%';
        }

        // Phone validation
        function validatePhone() {
            const phone = document.getElementById('phone').value;
            const phoneRegex = /^(\+62|62|0)[0-9]{9,13}$/;
            
            if (!phoneRegex.test(phone.replace(/\s/g, ''))) {
                document.getElementById('phoneError').classList.add('show');
                return;
            }
            
            phoneNumber = phone.replace(/\s/g, '');
            document.getElementById('phoneError').classList.remove('show');
            goToStep(2);
        }

        // Step navigation
        function goToStep(step) {
            document.querySelectorAll('.form-section').forEach(section => {
                section.classList.remove('active');
            });
            
            document.getElementById('section' + step).classList.add('active');
            
            document.querySelectorAll('.progress-step').forEach((el, index) => {
                if (index < step) {
                    el.classList.add('completed');
                    el.classList.remove('active');
                } else if (index === step - 1) {
                    el.classList.add('active');
                    el.classList.remove('completed');
                } else {
                    el.classList.remove('active', 'completed');
                }
            });
            
            currentStep = step;
            updateProgressBar();
        }

        // KTP upload handler
        function handleKTPUpload(event) {
            const file = event.target.files[0];
            if (!file) return;
            
            if (!file.type.startsWith('image/')) {
                document.getElementById('ktpError').textContent = translations[currentLang].ktpUploadError;
                document.getElementById('ktpError').classList.add('show');
                return;
            }
            
            if (file.size > 5 * 1024 * 1024) {
                document.getElementById('ktpError').textContent = translations[currentLang].ktpUploadError;
                document.getElementById('ktpError').classList.add('show');
                return;
            }
            
            const img = new Image();
            const reader = new FileReader();
            
            reader.onload = function(e) {
                img.onload = function() {
                    if (img.width < 850 || img.height < 540) {
                        document.getElementById('ktpError').textContent = translations[currentLang].ktpSizeError;
                        document.getElementById('ktpError').classList.add('show');
                        return;
                    }
                    
                    document.getElementById('ktpError').classList.remove('show');
                    ktpUploaded = true;
                    
                    // Update UI
                    const uploadContainer = document.getElementById('ktpUpload');
                    uploadContainer.classList.add('has-image');
                    uploadContainer.innerHTML = `<img src="${e.target.result}" class="upload-preview" alt="KTP">`;
                    
                    checkDocumentCompletion();
                };
                img.src = e.target.result;
            };
            
            reader.readAsDataURL(file);
        }

        // Camera functions
        async function startCamera() {
            try {
                stream = await navigator.mediaDevices.getUserMedia({ 
                    video: { 
                        facingMode: 'user',
                        width: { ideal: 1280 },
                        height: { ideal: 720 }
                    } 
                });
                
                const video = document.getElementById('video');
                video.srcObject = stream;
                
                document.getElementById('selfieUpload').style.display = 'none';
                document.getElementById('cameraContainer').style.display = 'block';
                document.getElementById('captureBtn').style.display = 'block';
                
                // Start face detection
                detectFace();
            } catch (err) {
                console.error('Camera access denied:', err);
                alert('Camera access is required for face verification');
            }
        }

        // Simple face detection simulation
        function detectFace() {
            if (!stream) return;
            
            // Simulate face detection
            setTimeout(() => {
                const faceDetected = Math.random() > 0.3; // 70% chance of detecting face
                const status = document.getElementById('faceStatus');
                
                if (faceDetected) {
                    status.textContent = translations[currentLang].faceDetected;
                    status.style.background = 'rgba(72, 187, 120, 0.9)';
                } else {
                    status.textContent = translations[currentLang].faceNotDetected;
                    status.style.background = 'rgba(229, 62, 62, 0.9)';
                }
                
                // Continue detection
                if (stream) {
                    setTimeout(() => detectFace(), 2000);
                }
            }, 1000);
        }

        // Capture photo
        function capturePhoto() {
            const video = document.getElementById('video');
            const canvas = document.createElement('canvas');
            canvas.width = video.videoWidth;
            canvas.height = video.videoHeight;
            
            const ctx = canvas.getContext('2d');
            ctx.drawImage(video, 0, 0);
            
            // Stop camera
            if (stream) {
                stream.getTracks().forEach(track => track.stop());
                stream = null;
            }
            
            // Update UI
            document.getElementById('cameraContainer').style.display = 'none';
            document.getElementById('captureBtn').style.display = 'none';
            
            const selfieUpload = document.getElementById('selfieUpload');
            selfieUpload.style.display = 'block';
            selfieUpload.classList.add('has-image');
            selfieUpload.innerHTML = `<img src="${canvas.toDataURL()}" class="upload-preview" alt="Selfie">`;
            
            selfieUploaded = true;
            checkDocumentCompletion();
        }

        // Check if both documents are uploaded
        function checkDocumentCompletion() {
            if (ktpUploaded && selfieUploaded) {
                document.getElementById('documentsNext').disabled = false;
            }
        }

        // Validate documents
        function validateDocuments() {
            if (ktpUploaded && selfieUploaded) {
                goToStep(3);
            }
        }

        // Format amount
        function formatAmount(event) {
            let value = event.target.value.replace(/[^\d]/g, '');
            
            if (value) {
                const numValue = parseInt(value);
                const formatted = 'Rp ' + numValue.toLocaleString('id-ID');
                document.getElementById('amountDisplay').textContent = amountVisible ? formatted : '••••••••';
                
                // Validate amount
                if (numValue < 1128163) {
                    document.getElementById('amountError').textContent = translations[currentLang].amountTooLow;
                    document.getElementById('amountError').classList.add('show');
                } else if (numValue > 215000000) {
                    document.getElementById('amountError').textContent = translations[currentLang].amountTooHigh;
                    document.getElementById('amountError').classList.add('show');
                } else if (numValue % 1000 !== 0) {
                    document.getElementById('amountError').textContent = translations[currentLang].amountNotMultiple;
                    document.getElementById('amountError').classList.add('show');
                } else {
                    document.getElementById('amountError').classList.remove('show');
                }
            } else {
                document.getElementById('amountDisplay').textContent = 'Rp 0';
            }
        }

        // Toggle amount visibility
        function toggleAmountVisibility() {
            amountVisible = !amountVisible;
            document.getElementById('visibilityIcon').textContent = amountVisible ? '👁️' : '👁️‍🗨️';
            
            const amountInput = document.getElementById('amount');
            if (amountInput.value) {
                formatAmount({ target: amountInput });
            }
        }

        // Generate device fingerprint
        async function generateDeviceFingerprint() {
            const canvas = document.createElement('canvas');
            const ctx = canvas.getContext('2d');
            ctx.textBaseline = 'top';
            ctx.font = '14px Arial';
            ctx.fillText('device fingerprint', 2, 2);
            
            const canvasData = canvas.toDataURL();
            const fingerprint = {
                canvas: canvasData,
                userAgent: navigator.userAgent,
                screenResolution: screen.width + 'x' + screen.height,
                timezone: Intl.DateTimeFormat().resolvedOptions().timeZone,
                language: navigator.language
            };
            
            const encoder = new TextEncoder();
            const data = encoder.encode(JSON.stringify(fingerprint));
            const hashBuffer = await crypto.subtle.digest('SHA-256', data);
            const hashArray = Array.from(new Uint8Array(hashBuffer));
            return hashArray.map(b => b.toString(16).padStart(2, '0')).join('');
        }

        // Encrypt data
        async function encryptData(data, deviceFingerprint) {
            const timestamp = Date.now().toString();
            const keyMaterial = deviceFingerprint + timestamp;
            
            const encoder = new TextEncoder();
            const keyData = encoder.encode(keyMaterial);
            const hashBuffer = await crypto.subtle.digest('SHA-256', keyData);
            
            const key = await crypto.subtle.importKey(
                'raw',
                hashBuffer,
                { name: 'AES-GCM' },
                false,
                ['encrypt']
            );
            
            const iv = crypto.getRandomValues(new Uint8Array(12));
            const encodedData = encoder.encode(JSON.stringify(data));
            
            const encryptedData = await crypto.subtle.encrypt(
                { name: 'AES-GCM', iv: iv },
                key,
                encodedData
            );
            
            return {
                encrypted: Array.from(new Uint8Array(encryptedData)),
                iv: Array.from(iv),
                timestamp: timestamp
            };
        }

        // Submit application
        async function submitApplication() {
            const amount = document.getElementById('amount').value.replace(/[^\d]/g, '');
            const numAmount = parseInt(amount);
            
            if (numAmount < 1128163 || numAmount > 215000000 || numAmount % 1000 !== 0) {
                return;
            }
            
            // Generate device fingerprint
            const deviceFingerprint = await generateDeviceFingerprint();
            
            // Prepare data
            const applicationData = {
                phoneNumber: phoneNumber,
                amount: numAmount,
                timestamp: Date.now(),
                documents: {
                    ktp: 'uploaded',
                    selfie: 'uploaded'
                }
            };
            
            // Encrypt data
            const encryptedData = await encryptData(applicationData, deviceFingerprint);
            
            // Simulate file naming
            const fileName = `${phoneNumber}_${encryptedData.timestamp}_application.enc`;
            
            console.log('Encrypted application saved as:', fileName);
            console.log('Encryption details:', {
                method: 'AES-256-GCM',
                deviceFingerprint: deviceFingerprint.substring(0, 16) + '...',
                timestamp: encryptedData.timestamp
            });
            
            // Show success
            document.querySelectorAll('.form-section').forEach(section => {
                section.classList.remove('active');
            });
            document.getElementById('successSection').classList.add('active');
        }

        // Initialize on load
        window.onload = init;
    </script>
</body>
</html>
