# digilocker
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>DigiLocker - Secure Document Storage</title>
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
            color: #333;
        }

        .container {
            max-width: 1200px;
            margin: 0 auto;
            padding: 20px;
        }

        .header {
            background: rgba(255, 255, 255, 0.95);
            backdrop-filter: blur(10px);
            border-radius: 15px;
            padding: 20px 30px;
            margin-bottom: 30px;
            box-shadow: 0 8px 32px rgba(0, 0, 0, 0.1);
            display: flex;
            justify-content: space-between;
            align-items: center;
        }

        .logo {
            display: flex;
            align-items: center;
            gap: 10px;
        }

        .logo-icon {
            width: 40px;
            height: 40px;
            background: linear-gradient(45deg, #667eea, #764ba2);
            border-radius: 8px;
            display: flex;
            align-items: center;
            justify-content: center;
            color: white;
            font-weight: bold;
            font-size: 18px;
        }

        .user-info {
            display: flex;
            align-items: center;
            gap: 15px;
        }

        .user-avatar {
            width: 40px;
            height: 40px;
            background: linear-gradient(45deg, #ff6b6b, #ee5a52);
            border-radius: 50%;
            display: flex;
            align-items: center;
            justify-content: center;
            color: white;
            font-weight: bold;
        }

        .main-content {
            display: grid;
            grid-template-columns: 1fr 2fr;
            gap: 30px;
        }

        .sidebar {
            background: rgba(255, 255, 255, 0.95);
            backdrop-filter: blur(10px);
            border-radius: 15px;
            padding: 25px;
            box-shadow: 0 8px 32px rgba(0, 0, 0, 0.1);
            height: fit-content;
        }

        .upload-section {
            margin-bottom: 30px;
        }

        .upload-area {
            border: 2px dashed #667eea;
            border-radius: 10px;
            padding: 30px;
            text-align: center;
            cursor: pointer;
            transition: all 0.3s ease;
            background: rgba(102, 126, 234, 0.05);
        }

        .upload-area:hover {
            border-color: #764ba2;
            background: rgba(118, 75, 162, 0.1);
        }

        .upload-area.dragover {
            border-color: #764ba2;
            background: rgba(118, 75, 162, 0.2);
            transform: scale(1.02);
        }

        .upload-icon {
            font-size: 48px;
            color: #667eea;
            margin-bottom: 15px;
        }

        .categories {
            margin-top: 30px;
        }

        .category-item {
            display: flex;
            align-items: center;
            gap: 10px;
            padding: 12px 15px;
            border-radius: 8px;
            cursor: pointer;
            transition: all 0.3s ease;
            margin-bottom: 8px;
        }

        .category-item:hover {
            background: rgba(102, 126, 234, 0.1);
        }

        .category-item.active {
            background: linear-gradient(45deg, #667eea, #764ba2);
            color: white;
        }

        .category-icon {
            width: 20px;
            height: 20px;
            border-radius: 4px;
            display: flex;
            align-items: center;
            justify-content: center;
            font-size: 12px;
        }

        .documents-section {
            background: rgba(255, 255, 255, 0.95);
            backdrop-filter: blur(10px);
            border-radius: 15px;
            padding: 25px;
            box-shadow: 0 8px 32px rgba(0, 0, 0, 0.1);
        }

        .documents-header {
            display: flex;
            justify-content: space-between;
            align-items: center;
            margin-bottom: 25px;
        }

        .search-bar {
            flex: 1;
            max-width: 300px;
            padding: 10px 15px;
            border: 2px solid #e0e0e0;
            border-radius: 8px;
            font-size: 14px;
            transition: border-color 0.3s ease;
        }

        .search-bar:focus {
            outline: none;
            border-color: #667eea;
        }

        .documents-grid {
            display: grid;
            grid-template-columns: repeat(auto-fill, minmax(250px, 1fr));
            gap: 20px;
        }

        .document-card {
            background: white;
            border-radius: 12px;
            padding: 20px;
            box-shadow: 0 4px 16px rgba(0, 0, 0, 0.1);
            transition: all 0.3s ease;
            cursor: pointer;
            border: 2px solid transparent;
        }

        .document-card:hover {
            transform: translateY(-5px);
            box-shadow: 0 8px 32px rgba(0, 0, 0, 0.15);
            border-color: #667eea;
        }

        .document-icon {
            width: 60px;
            height: 60px;
            border-radius: 8px;
            display: flex;
            align-items: center;
            justify-content: center;
            font-size: 24px;
            color: white;
            margin-bottom: 15px;
        }

        .document-info h3 {
            font-size: 16px;
            margin-bottom: 8px;
            color: #333;
        }

        .document-meta {
            font-size: 12px;
            color: #666;
            margin-bottom: 15px;
        }

        .document-actions {
            display: flex;
            gap: 10px;
        }

        .btn {
            padding: 8px 16px;
            border: none;
            border-radius: 6px;
            cursor: pointer;
            font-size: 12px;
            font-weight: 500;
            transition: all 0.3s ease;
        }

        .btn-primary {
            background: linear-gradient(45deg, #667eea, #764ba2);
            color: white;
        }

        .btn-primary:hover {
            transform: translateY(-2px);
            box-shadow: 0 4px 16px rgba(102, 126, 234, 0.3);
        }

        .btn-secondary {
            background: #f0f0f0;
            color: #666;
        }

        .btn-secondary:hover {
            background: #e0e0e0;
        }

        .modal {
            display: none;
            position: fixed;
            top: 0;
            left: 0;
            width: 100%;
            height: 100%;
            background: rgba(0, 0, 0, 0.5);
            backdrop-filter: blur(5px);
            z-index: 1000;
        }

        .modal-content {
            position: absolute;
            top: 50%;
            left: 50%;
            transform: translate(-50%, -50%);
            background: white;
            border-radius: 15px;
            padding: 30px;
            max-width: 500px;
            width: 90%;
            max-height: 80vh;
            overflow-y: auto;
        }

        .quick-actions {
            margin-top: 30px;
        }

        .action-btn {
            display: flex;
            align-items: center;
            gap: 10px;
            padding: 15px;
            width: 100%;
            border: none;
            border-radius: 8px;
            cursor: pointer;
            transition: all 0.3s ease;
            margin-bottom: 10px;
            background: rgba(102, 126, 234, 0.05);
            border: 2px solid transparent;
        }

        .action-btn:hover {
            background: rgba(102, 126, 234, 0.1);
            border-color: #667eea;
            transform: translateY(-2px);
        }

        .action-icon {
            width: 30px;
            height: 30px;
            border-radius: 6px;
            display: flex;
            align-items: center;
            justify-content: center;
            font-size: 16px;
            color: white;
        }

        .fees-grid {
            display: grid;
            grid-template-columns: repeat(auto-fit, minmax(250px, 1fr));
            gap: 20px;
            margin-bottom: 25px;
        }

        .fee-card {
            background: white;
            border-radius: 12px;
            padding: 20px;
            box-shadow: 0 4px 16px rgba(0, 0, 0, 0.1);
            border: 2px solid #e0e0e0;
            transition: all 0.3s ease;
        }

        .fee-card.selected {
            border-color: #667eea;
            background: rgba(102, 126, 234, 0.05);
        }

        .fee-card:hover {
            border-color: #667eea;
            transform: translateY(-2px);
        }

        .fee-header {
            display: flex;
            justify-content: space-between;
            align-items: center;
            margin-bottom: 15px;
        }

        .fee-amount {
            font-size: 24px;
            font-weight: bold;
            color: #667eea;
        }

        .fee-status {
            padding: 4px 12px;
            border-radius: 20px;
            font-size: 12px;
            font-weight: 500;
        }

        .fee-status.pending {
            background: #ffeaa7;
            color: #d63031;
        }

        .fee-status.paid {
            background: #00b894;
            color: white;
        }

        .fee-status.overdue {
            background: #ff6b6b;
            color: white;
        }

        .payment-methods {
            display: grid;
            grid-template-columns: repeat(auto-fit, minmax(150px, 1fr));
            gap: 15px;
            margin: 20px 0;
        }

        .payment-method {
            padding: 15px;
            border: 2px solid #e0e0e0;
            border-radius: 8px;
            text-align: center;
            cursor: pointer;
            transition: all 0.3s ease;
        }

        .payment-method:hover {
            border-color: #667eea;
        }

        .payment-method.selected {
            border-color: #667eea;
            background: rgba(102, 126, 234, 0.05);
        }

        .payment-method-icon {
            font-size: 32px;
            margin-bottom: 10px;
        }

        .chatbot-container {
            position: fixed;
            bottom: 20px;
            right: 20px;
            width: 350px;
            height: 500px;
            background: white;
            border-radius: 15px;
            box-shadow: 0 8px 32px rgba(0, 0, 0, 0.2);
            display: none;
            flex-direction: column;
            z-index: 1001;
        }

        .chatbot-header {
            background: linear-gradient(45deg, #667eea, #764ba2);
            color: white;
            padding: 15px 20px;
            border-radius: 15px 15px 0 0;
            display: flex;
            justify-content: space-between;
            align-items: center;
        }

        .admin-status {
            display: flex;
            align-items: center;
            gap: 8px;
        }

        .status-dot {
            width: 8px;
            height: 8px;
            background: #00b894;
            border-radius: 50%;
            animation: pulse 2s infinite;
        }

        @keyframes pulse {
            0% { opacity: 1; }
            50% { opacity: 0.5; }
            100% { opacity: 1; }
        }

        .chatbot-messages {
            flex: 1;
            padding: 20px;
            overflow-y: auto;
            display: flex;
            flex-direction: column;
            gap: 15px;
        }

        .message {
            max-width: 80%;
            padding: 12px 16px;
            border-radius: 18px;
            font-size: 14px;
            line-height: 1.4;
        }

        .message.admin {
            background: #f0f0f0;
            align-self: flex-start;
        }

        .message.user {
            background: linear-gradient(45deg, #667eea, #764ba2);
            color: white;
            align-self: flex-end;
        }

        .message-time {
            font-size: 11px;
            opacity: 0.7;
            margin-top: 4px;
        }

        .chatbot-input {
            display: flex;
            padding: 15px;
            border-top: 1px solid #e0e0e0;
            gap: 10px;
        }

        .chatbot-input input {
            flex: 1;
            padding: 10px 15px;
            border: 2px solid #e0e0e0;
            border-radius: 20px;
            outline: none;
            font-size: 14px;
        }

        .chatbot-input input:focus {
            border-color: #667eea;
        }

        .send-btn {
            background: linear-gradient(45deg, #667eea, #764ba2);
            color: white;
            border: none;
            border-radius: 50%;
            width: 40px;
            height: 40px;
            cursor: pointer;
            display: flex;
            align-items: center;
            justify-content: center;
            transition: all 0.3s ease;
        }

        .send-btn:hover {
            transform: scale(1.1);
        }

        .quick-replies {
            display: flex;
            gap: 8px;
            margin-bottom: 15px;
            flex-wrap: wrap;
        }

        .quick-reply {
            background: rgba(102, 126, 234, 0.1);
            border: 1px solid #667eea;
            border-radius: 15px;
            padding: 6px 12px;
            font-size: 12px;
            cursor: pointer;
            transition: all 0.3s ease;
        }

        .quick-reply:hover {
            background: #667eea;
            color: white;
        }

        .modal-header {
            display: flex;
            justify-content: space-between;
            align-items: center;
            margin-bottom: 20px;
        }

        .close-btn {
            background: none;
            border: none;
            font-size: 24px;
            cursor: pointer;
            color: #666;
        }

        .form-group {
            margin-bottom: 20px;
        }

        .form-group label {
            display: block;
            margin-bottom: 8px;
            font-weight: 500;
            color: #333;
        }

        .form-group input,
        .form-group select {
            width: 100%;
            padding: 12px;
            border: 2px solid #e0e0e0;
            border-radius: 8px;
            font-size: 14px;
            transition: border-color 0.3s ease;
        }

        .form-group input:focus,
        .form-group select:focus {
            outline: none;
            border-color: #667eea;
        }

        .stats-container {
            display: grid;
            grid-template-columns: repeat(auto-fit, minmax(150px, 1fr));
            gap: 15px;
            margin-bottom: 25px;
        }

        .stat-card {
            background: linear-gradient(45deg, #667eea, #764ba2);
            color: white;
            padding: 20px;
            border-radius: 10px;
            text-align: center;
        }

        .stat-number {
            font-size: 24px;
            font-weight: bold;
            margin-bottom: 5px;
        }

        .stat-label {
            font-size: 12px;
            opacity: 0.9;
        }

        @media (max-width: 768px) {
            .main-content {
                grid-template-columns: 1fr;
            }
            
            .header {
                flex-direction: column;
                gap: 15px;
                text-align: center;
            }
            
            .documents-grid {
                grid-template-columns: 1fr;
            }
        }
    </style>
</head>
<body>
    <div class="container">
        <header class="header">
            <div class="logo">
                <div class="logo-icon">DL</div>
                <div>
                    <h1>DigiLocker</h1>
                    <p>Secure Digital Document Storage</p>
                </div>
            </div>
            <div class="user-info">
                <span>Welcome, Student</span>
                <div class="user-avatar">S</div>
            </div>
        </header>

        <div class="main-content">
            <aside class="sidebar">
                <div class="upload-section">
                    <h3>Upload Documents</h3>
                    <div class="upload-area" onclick="document.getElementById('fileInput').click()">
                        <div class="upload-icon">📁</div>
                        <h4>Drop files here or click to upload</h4>
                        <p>Supported: PDF, JPG, PNG, DOC</p>
                    </div>
                    <input type="file" id="fileInput" multiple accept=".pdf,.jpg,.jpeg,.png,.doc,.docx" style="display: none;">
                </div>

                <div class="categories">
                    <h3>Categories</h3>
                    <div class="category-item active" onclick="filterDocuments('all')">
                        <div class="category-icon" style="background: #667eea;">📄</div>
                        <span>All Documents</span>
                    </div>
                    <div class="category-item" onclick="filterDocuments('academic')">
                        <div class="category-icon" style="background: #28a745;">🎓</div>
                        <span>Academic Records</span>
                    </div>
                    <div class="category-item" onclick="filterDocuments('certificates')">
                        <div class="category-icon" style="background: #ffc107;">🏆</div>
                        <span>Certificates</span>
                    </div>
                    <div class="category-item" onclick="filterDocuments('identity')">
                        <div class="category-icon" style="background: #dc3545;">🆔</div>
                        <span>Identity Docs</span>
                    </div>
                    <div class="category-item" onclick="filterDocuments('financial')">
                        <div class="category-icon" style="background: #17a2b8;">💳</div>
                        <span>Financial</span>
                    </div>
                    <div class="category-item" onclick="filterDocuments('others')">
                        <div class="category-icon" style="background: #6c757d;">📋</div>
                        <span>Others</span>
                    </div>
                </div>

                <div class="quick-actions">
                    <h3>Quick Actions</h3>
                    <button class="action-btn" onclick="openChatbot()">
                        <div class="action-icon" style="background: #007bff;">💬</div>
                        <span>Chat with Admin</span>
                    </button>
                </div>
            </aside>

            <main class="documents-section">
                <div class="stats-container">
                    <div class="stat-card">
                        <div class="stat-number" id="totalDocs">0</div>
                        <div class="stat-label">Total Documents</div>
                    </div>
                    <div class="stat-card">
                        <div class="stat-number" id="recentUploads">0</div>
                        <div class="stat-label">Recent Uploads</div>
                    </div>
                    <div class="stat-card">
                        <div class="stat-number">256</div>
                        <div class="stat-label">MB Used</div>
                    </div>
                </div>

                <div class="documents-header">
                    <h2>My Documents</h2>
                    <input type="text" class="search-bar" placeholder="Search documents..." id="searchInput">
                </div>

                <div class="documents-grid" id="documentsGrid">
                    <!-- Sample documents will be populated here -->
                </div>
            </main>
        </div>
    </div>

    <!-- Upload Modal -->
    <div class="modal" id="uploadModal">
        <div class="modal-content">
            <div class="modal-header">
                <h3>Upload Document</h3>
                <button class="close-btn" onclick="closeModal()">&times;</button>
            </div>
            <form id="uploadForm">
                <div class="form-group">
                    <label>Document Title</label>
                    <input type="text" id="docTitle" required>
                </div>
                <div class="form-group">
                    <label>Category</label>
                    <select id="docCategory" required>
                        <option value="">Select Category</option>
                        <option value="academic">Academic Records</option>
                        <option value="certificates">Certificates</option>
                        <option value="identity">Identity Documents</option>
                        <option value="financial">Financial</option>
                        <option value="others">Others</option>
                    </select>
                </div>
                <div class="form-group">
                    <label>Description</label>
                    <input type="text" id="docDescription" placeholder="Optional description">
                </div>
                <button type="submit" class="btn btn-primary">Upload Document</button>
            </form>
        </div>
    </div>

    <!-- Document Viewer Modal -->
    <div class="modal" id="viewerModal">
        <div class="modal-content" style="max-width: 800px;">
            <div class="modal-header">
                <h3 id="viewerTitle">Document Viewer</h3>
                <button class="close-btn" onclick="closeViewer()">&times;</button>
            </div>
            <div id="viewerContent">
                <p>Document content will be displayed here...</p>
            </div>
        </div>
    </div>

    <!-- Chatbot -->
    <div class="chatbot-container" id="chatbotContainer">
        <div class="chatbot-header">
            <div>
                <div style="font-weight: bold;">Admin Support</div>
                <div class="admin-status">
                    <span class="status-dot"></span>
                    <span style="font-size: 12px;">Online</span>
                </div>
            </div>
            <button class="close-btn" onclick="closeChatbot()" style="color: white;">&times;</button>
        </div>
        <div class="chatbot-messages" id="chatbotMessages">
            <div class="message admin">
                <div>Hello! I'm here to help you with any administrative queries. How can I assist you today?</div>
                <div class="message-time">Just now</div>
            </div>
            <div class="quick-replies">
                <div class="quick-reply" onclick="sendQuickReply('Fees inquiry')">Fees inquiry</div>
                <div class="quick-reply" onclick="sendQuickReply('Document verification')">Document verification</div>
                <div class="quick-reply" onclick="sendQuickReply('Technical support')">Technical support</div>
            </div>
        </div>
        <div class="chatbot-input">
            <input type="text" id="chatInput" placeholder="Type your message..." onkeypress="handleChatKeyPress(event)">
            <button class="send-btn" onclick="sendMessage()">📤</button>
        </div>
    </div>

    <script>
        // Sample documents data
        let documents = [
            {
                id: 1,
                title: "Semester 1 Results",
                category: "academic",
                type: "pdf",
                size: "245 KB",
                date: "2024-12-15",
                description: "First semester examination results"
            },
            {
                id: 2,
                title: "Degree Certificate",
                category: "certificates",
                type: "pdf",
                size: "1.2 MB",
                date: "2024-11-20",
                description: "Bachelor's degree certificate"
            },
            {
                id: 3,
                title: "Aadhar Card",
                category: "identity",
                type: "pdf",
                size: "156 KB",
                date: "2024-10-10",
                description: "Government issued identity card"
            },
            {
                id: 4,
                title: "Transcript",
                category: "academic",
                type: "pdf",
                size: "512 KB",
                date: "2024-12-01",
                description: "Official academic transcript"
            },
            {
                id: 5,
                title: "Course Completion Certificate",
                category: "certificates",
                type: "pdf",
                size: "389 KB",
                date: "2024-11-15",
                description: "Online course completion certificate"
            }
        ];

        // Fees data
        let feesData = [
            {
                id: 1,
                title: "Tuition Fee - Semester 1",
                amount: 25000,
                dueDate: "2025-01-15",
                status: "pending",
                description: "First semester tuition fees"
            },
            {
                id: 2,
                title: "Library Fee",
                amount: 2500,
                dueDate: "2024-12-20",
                status: "overdue",
                description: "Annual library membership fee"
            },
            {
                id: 3,
                title: "Lab Fee - Physics",
                amount: 3500,
                dueDate: "2025-02-01",
                status: "pending",
                description: "Physics laboratory usage fee"
            },
            {
                id: 4,
                title: "Registration Fee",
                amount: 1500,
                dueDate: "2024-11-15",
                status: "paid",
                description: "Annual registration fee"
            }
        ];

        let currentFilter = 'all';
        let selectedFiles = [];
        let chatMessages = [];

        // Initialize the application
        document.addEventListener('DOMContentLoaded', function() {
            renderDocuments();
            updateStats();
            setupEventListeners();
        });

        function setupEventListeners() {
            // File input change
            document.getElementById('fileInput').addEventListener('change', handleFileSelect);
            
            // Search functionality
            document.getElementById('searchInput').addEventListener('input', handleSearch);
            
            // Upload form submission
            document.getElementById('uploadForm').addEventListener('submit', handleUpload);
            
            // Drag and drop
            const uploadArea = document.querySelector('.upload-area');
            uploadArea.addEventListener('dragover', handleDragOver);
            uploadArea.addEventListener('dragleave', handleDragLeave);
            uploadArea.addEventListener('drop', handleDrop);
        }

        function handleFileSelect(event) {
            selectedFiles = Array.from(event.target.files);
            if (selectedFiles.length > 0) {
                document.getElementById('docTitle').value = selectedFiles[0].name.split('.')[0];
                document.getElementById('uploadModal').style.display = 'block';
            }
        }

        function handleDragOver(event) {
            event.preventDefault();
            event.currentTarget.classList.add('dragover');
        }

        function handleDragLeave(event) {
            event.currentTarget.classList.remove('dragover');
        }

        function handleDrop(event) {
            event.preventDefault();
            event.currentTarget.classList.remove('dragover');
            selectedFiles = Array.from(event.dataTransfer.files);
            if (selectedFiles.length > 0) {
                document.getElementById('docTitle').value = selectedFiles[0].name.split('.')[0];
                document.getElementById('uploadModal').style.display = 'block';
            }
        }

        function handleSearch(event) {
            const searchTerm = event.target.value.toLowerCase();
            const filteredDocs = documents.filter(doc => 
                doc.title.toLowerCase().includes(searchTerm) ||
                doc.description.toLowerCase().includes(searchTerm)
            );
            renderDocuments(filteredDocs);
        }

        function handleUpload(event) {
            event.preventDefault();
            
            const title = document.getElementById('docTitle').value;
            const category = document.getElementById('docCategory').value;
            const description = document.getElementById('docDescription').value;
            
            if (selectedFiles.length > 0) {
                const newDoc = {
                    id: documents.length + 1,
                    title: title,
                    category: category,
                    type: selectedFiles[0].type.includes('pdf') ? 'pdf' : 'image',
                    size: formatFileSize(selectedFiles[0].size),
                    date: new Date().toISOString().split('T')[0],
                    description: description || 'Uploaded document'
                };
                
                documents.push(newDoc);
                renderDocuments();
                updateStats();
                closeModal();
                
                // Reset form
                document.getElementById('uploadForm').reset();
                selectedFiles = [];
            }
        }

        function formatFileSize(bytes) {
            if (bytes === 0) return '0 Bytes';
            const k = 1024;
            const sizes = ['Bytes', 'KB', 'MB', 'GB'];
            const i = Math.floor(Math.log(bytes) / Math.log(k));
            return parseFloat((bytes / Math.pow(k, i)).toFixed(2)) + ' ' + sizes[i];
        }

        function filterDocuments(category) {
            currentFilter = category;
            
            // Update active category
            document.querySelectorAll('.category-item').forEach(item => {
                item.classList.remove('active');
            });
            event.target.closest('.category-item').classList.add('active');
            
            // Filter and render documents
            const filteredDocs = category === 'all' ? documents : documents.filter(doc => doc.category === category);
            renderDocuments(filteredDocs);
        }

        function renderDocuments(docsToRender = documents) {
            const grid = document.getElementById('documentsGrid');
            
            if (docsToRender.length === 0) {
                grid.innerHTML = '<p style="text-align: center; color: #666; grid-column: 1/-1;">No documents found.</p>';
                return;
            }
            
            grid.innerHTML = docsToRender.map(doc => `
                <div class="document-card" onclick="viewDocument(${doc.id})">
                    <div class="document-icon" style="background: ${getDocumentColor(doc.category)};">
                        ${getDocumentIcon(doc.type)}
                    </div>
                    <div class="document-info">
                        <h3>${doc.title}</h3>
                        <div class="document-meta">
                            ${doc.size} • ${formatDate(doc.date)}
                        </div>
                        <p style="font-size: 12px; color: #666; margin-bottom: 10px;">${doc.description}</p>
                    </div>
                    <div class="document-actions">
                        <button class="btn btn-primary" onclick="event.stopPropagation(); downloadDocument(${doc.id})">Download</button>
                        <button class="btn btn-secondary" onclick="event.stopPropagation(); shareDocument(${doc.id})">Share</button>
                    </div>
                </div>
            `).join('');
        }

        function getDocumentIcon(type) {
            switch(type) {
                case 'pdf': return '📄';
                case 'image': return '🖼️';
                case 'doc': return '📝';
                default: return '📄';
            }
        }

        function getDocumentColor(category) {
            switch(category) {
                case 'academic': return '#28a745';
                case 'certificates': return '#ffc107';
                case 'identity': return '#dc3545';
                case 'financial': return '#17a2b8';
                default: return '#6c757d';
            }
        }

        function formatDate(dateString) {
            const options = { year: 'numeric', month: 'short', day: 'numeric' };
            return new Date(dateString).toLocaleDateString('en-US', options);
        }

        function updateStats() {
            document.getElementById('totalDocs').textContent = documents.length;
            
            const recentCount = documents.filter(doc => {
                const docDate = new Date(doc.date);
                const weekAgo = new Date();
                weekAgo.setDate(weekAgo.getDate() - 7);
                return docDate >= weekAgo;
            }).length;
            
            document.getElementById('recentUploads').textContent = recentCount;
        }

        function viewDocument(id) {
            const doc = documents.find(d => d.id === id);
            if (doc) {
                document.getElementById('viewerTitle').textContent = doc.title;
                document.getElementById('viewerContent').innerHTML = `
                    <div style="text-align: center; padding: 40px;">
                        <div style="font-size: 48px; margin-bottom: 20px;">${getDocumentIcon(doc.type)}</div>
                        <h3>${doc.title}</h3>
                        <p style="color: #666; margin: 10px 0;">${doc.description}</p>
                        <div style="margin: 20px 0;">
                            <strong>Category:</strong> ${doc.category}<br>
                            <strong>Size:</strong> ${doc.size}<br>
                            <strong>Date:</strong> ${formatDate(doc.date)}
                        </div>
                        <p style="font-style: italic; color: #999;">Document preview not available in demo mode</p>
                    </div>
                `;
                document.getElementById('viewerModal').style.display = 'block';
            }
        }

        function downloadDocument(id) {
            const doc = documents.find(d => d.id === id);
            if (doc) {
                alert(`Downloading ${doc.title}...`);
            }
        }

        function shareDocument(id) {
            const doc = documents.find(d => d.id === id);
            if (doc) {
                alert(`Sharing ${doc.title}...`);
            }
        }

        function closeModal() {
            document.getElementById('uploadModal').style.display = 'none';
        }

        function closeViewer() {
            document.getElementById('viewerModal').style.display = 'none';
        }

        // Chatbot Functions
        function openChatbot() {
            document.getElementById('chatbotContainer').style.display = 'flex';
        }

        function closeChatbot() {
            document.getElementById('chatbotContainer').style.display = 'none';
        }

        function sendMessage() {
            const input = document.getElementById('chatInput');
            const message = input.value.trim();
            if (message) {
                addMessage(message, 'user');
                input.value = '';
                
                // Simulate admin response
                setTimeout(() => {
                    const response = generateAdminResponse(message);
                    addMessage(response, 'admin');
                }, 1000 + Math.random() * 2000);
            }
        }

        function sendQuickReply(message) {
            addMessage(message, 'user');
            document.querySelector('.quick-replies').style.display = 'none';
            
            setTimeout(() => {
                const response = generateAdminResponse(message);
                addMessage(response, 'admin');
            }, 1000);
        }

        function addMessage(text, sender) {
            const messagesContainer = document.getElementById('chatbotMessages');
            const messageDiv = document.createElement('div');
            messageDiv.className = `message ${sender}`;
            
            const now = new Date();
            const timeString = now.toLocaleTimeString([], { hour: '2-digit', minute: '2-digit' });
            
            messageDiv.innerHTML = `
                <div>${text}</div>
                <div class="message-time">${timeString}</div>
            `;
            
            messagesContainer.appendChild(messageDiv);
            messagesContainer.scrollTop = messagesContainer.scrollHeight;
        }

        function generateAdminResponse(userMessage) {
            const message = userMessage.toLowerCase();
            
            if (message.includes('fees') || message.includes('payment')) {
                return "I can help you with fees-related queries. Please let me know what specific information you need about your fees or payment status.";
            } else if (message.includes('document') || message.includes('certificate')) {
                return "For document-related queries, you can upload, view, and manage your documents in the main section. If you need document verification, please provide the document name and I'll assist you.";
            } else if (message.includes('technical') || message.includes('support')) {
                return "I'm here to help with technical issues. Please describe the problem you're experiencing, and I'll guide you through the solution.";
            } else if (message.includes('hello') || message.includes('hi')) {
                return "Hello! How can I assist you today? I can help with fees, documents, technical support, and other administrative matters.";
            } else {
                return "Thank you for your message. I've noted your query and will get back to you shortly. Is there anything specific I can help you with right now?";
            }
        }

        function handleChatKeyPress(event) {
            if (event.key === 'Enter') {
                sendMessage();
            }
        }

        // Close modals when clicking outside
        window.onclick = function(event) {
            const uploadModal = document.getElementById('uploadModal');
            const viewerModal = document.getElementById('viewerModal');
            
            if (event.target === uploadModal) {
                uploadModal.style.display = 'none';
            }
            if (event.target === viewerModal) {
                viewerModal.style.display = 'none';
            }
        }
    </script>
</body>
</html>
