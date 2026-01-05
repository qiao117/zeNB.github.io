# zeNB.github.io
<!DOCTYPE html>
<html lang="zh-CN">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>交互式欢迎页面</title>
    <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.4.0/css/all.min.css">
    <style>
        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
            font-family: 'Segoe UI', 'Microsoft YaHei', sans-serif;
        }
        
        body {
            display: flex;
            justify-content: center;
            align-items: center;
            min-height: 100vh;
            background: linear-gradient(135deg, #6a11cb 0%, #2575fc 100%);
            padding: 20px;
        }
        
        .container {
            width: 100%;
            max-width: 1200px;
            text-align: center;
        }
        
        .header {
            margin-bottom: 50px;
            color: white;
        }
        
        .header h1 {
            font-size: 2.8rem;
            margin-bottom: 10px;
            text-shadow: 2px 2px 4px rgba(0, 0, 0, 0.2);
        }
        
        .header p {
            font-size: 1.2rem;
            opacity: 0.9;
            max-width: 600px;
            margin: 0 auto;
        }
        
        .cards-container {
            display: flex;
            justify-content: center;
            flex-wrap: wrap;
            gap: 30px;
            margin-bottom: 40px;
        }
        
        .card {
            background-color: rgba(255, 255, 255, 0.95);
            border-radius: 20px;
            padding: 30px 20px;
            width: 300px;
            min-height: 350px;
            display: flex;
            flex-direction: column;
            align-items: center;
            justify-content: space-between;
            box-shadow: 0 15px 30px rgba(0, 0, 0, 0.2);
            transition: all 0.4s ease;
            cursor: pointer;
            overflow: hidden;
            position: relative;
        }
        
        .card:hover {
            transform: translateY(-15px);
            box-shadow: 0 25px 40px rgba(0, 0, 0, 0.25);
        }
        
        .card-icon {
            width: 100px;
            height: 100px;
            border-radius: 50%;
            display: flex;
            align-items: center;
            justify-content: center;
            margin-bottom: 25px;
            font-size: 2.8rem;
            color: white;
        }
        
        .card:nth-child(1) .card-icon {
            background: linear-gradient(to right, #ff7e5f, #feb47b);
        }
        
        .card:nth-child(2) .card-icon {
            background: linear-gradient(to right, #4facfe, #00f2fe);
        }
        
        .card:nth-child(3) .card-icon {
            background: linear-gradient(to right, #a8edea, #fed6e3);
        }
        
        .card h2 {
            font-size: 1.8rem;
            margin-bottom: 20px;
            color: #333;
        }
        
        .card p {
            color: #666;
            line-height: 1.6;
            margin-bottom: 20px;
            padding: 0 10px;
        }
        
        .card-button {
            background-color: #4a6ee0;
            color: white;
            border: none;
            padding: 12px 30px;
            border-radius: 50px;
            font-size: 1rem;
            font-weight: 600;
            cursor: pointer;
            transition: all 0.3s ease;
            box-shadow: 0 5px 15px rgba(74, 110, 224, 0.3);
        }
        
        .card-button:hover {
            background-color: #3a5ed0;
            transform: scale(1.05);
        }
        
        .modal {
            display: none;
            position: fixed;
            top: 0;
            left: 0;
            width: 100%;
            height: 100%;
            background-color: rgba(0, 0, 0, 0.7);
            z-index: 1000;
            justify-content: center;
            align-items: center;
            animation: fadeIn 0.3s ease;
        }
        
        .modal-content {
            background-color: white;
            width: 90%;
            max-width: 500px;
            border-radius: 20px;
            padding: 40px;
            box-shadow: 0 20px 50px rgba(0, 0, 0, 0.3);
            position: relative;
            animation: slideUp 0.4s ease;
        }
        
        .modal-header {
            display: flex;
            justify-content: space-between;
            align-items: center;
            margin-bottom: 20px;
        }
        
        .modal-title {
            font-size: 1.8rem;
            color: #333;
        }
        
        .close-btn {
            background: none;
            border: none;
            font-size: 2rem;
            color: #888;
            cursor: pointer;
            transition: color 0.3s;
        }
        
        .close-btn:hover {
            color: #333;
        }
        
        .modal-body {
            font-size: 1.1rem;
            line-height: 1.6;
            color: #555;
        }
        
        .welcome-message {
            font-size: 1.4rem;
            color: #4a6ee0;
            font-weight: 600;
            text-align: center;
            padding: 20px;
            background-color: #f5f7ff;
            border-radius: 10px;
            margin: 20px 0;
        }
        
        .developer-name {
            font-size: 2.2rem;
            color: #4a6ee0;
            font-weight: 700;
            text-align: center;
            padding: 20px;
            margin: 20px 0;
            border: 3px dashed #4a6ee0;
            border-radius: 10px;
        }
        
        .unavailable {
            font-size: 1.2rem;
            color: #ff6b6b;
            text-align: center;
            padding: 20px;
            margin: 20px 0;
            background-color: #fff5f5;
            border-radius: 10px;
        }
        
        .unavailable i {
            font-size: 3rem;
            margin-bottom: 15px;
            display: block;
        }
        
        .footer {
            color: white;
            opacity: 0.8;
            font-size: 0.9rem;
            padding: 20px;
        }
        
        @keyframes fadeIn {
            from { opacity: 0; }
            to { opacity: 1; }
        }
        
        @keyframes slideUp {
            from { transform: translateY(50px); opacity: 0; }
            to { transform: translateY(0); opacity: 1; }
        }
        
        @media (max-width: 768px) {
            .cards-container {
                flex-direction: column;
                align-items: center;
            }
            
            .card {
                width: 100%;
                max-width: 350px;
            }
            
            .header h1 {
                font-size: 2.2rem;
            }
        }
    </style>
</head>
<body>
    <div class="container">
        <div class="header">
            <h1>交互式欢迎页面</h1>
            <p>点击下方卡片探索不同功能，每个卡片都有独特的内容和交互效果</p>
        </div>
        
        <div class="cards-container">
            <!-- 欢迎卡片 -->
            <div class="card" id="welcome-card">
                <div>
                    <div class="card-icon">
                        <i class="fas fa-hand-wave"></i>
                    </div>
                    <h2>欢迎</h2>
                    <p>点击这里查看欢迎信息。我们很高兴您能访问这个页面，希望您有愉快的体验。</p>
                </div>
                <button class="card-button" onclick="openWelcome()">查看欢迎语</button>
            </div>
            
            <!-- 开发者卡片 -->
            <div class="card" id="developer-card">
                <div>
                    <div class="card-icon">
                        <i class="fas fa-code"></i>
                    </div>
                    <h2>开发者</h2>
                    <p>点击这里了解本页面的开发者信息。感谢开发者的辛勤工作，创造了这个精美的页面。</p>
                </div>
                <button class="card-button" onclick="openDeveloper()">查看开发者</button>
            </div>
            
            <!-- 看视频卡片 -->
            <div class="card" id="video-card">
                <div>
                    <div class="card-icon">
                        <i class="fas fa-video"></i>
                    </div>
                    <h2>看视频</h2>
                    <p>点击这里查看视频内容。请注意，此功能目前正在开发中，敬请期待后续更新。</p>
                </div>
                <button class="card-button" onclick="openVideo()">观看视频</button>
            </div>
        </div>
        
        <div class="footer">
            <p>交互式欢迎页面 © 2023 | 点击卡片探索功能</p>
        </div>
    </div>
    
    <!-- 欢迎模态框 -->
    <div class="modal" id="welcome-modal">
        <div class="modal-content">
            <div class="modal-header">
                <h2 class="modal-title">欢迎页面</h2>
                <button class="close-btn" onclick="closeModal('welcome-modal')">&times;</button>
            </div>
            <div class="modal-body">
                <p>欢迎来到这个交互式演示页面！</p>
                <div class="welcome-message">
                    <i class="fas fa-heart"></i>
                    <p>热烈欢迎您的访问！</p>
                    <p>感谢您探索这个交互式页面，我们精心设计了每个功能，希望您喜欢！</p>
                </div>
                <p>这是一个功能演示页面，展示了三种不同的交互模式。您可以点击上方其他卡片查看更多功能。</p>
            </div>
        </div>
    </div>
    
    <!-- 开发者模态框 -->
    <div class="modal" id="developer-modal">
        <div class="modal-content">
            <div class="modal-header">
                <h2 class="modal-title">开发者信息</h2>
                <button class="close-btn" onclick="closeModal('developer-modal')">&times;</button>
            </div>
            <div class="modal-body">
                <p>本页面由以下开发者创建：</p>
                <div class="developer-name">乔XX</div>
                <p>乔XX是一位富有创造力的前端开发者，专注于创造美观且用户友好的交互界面。</p>
                <p>此页面展示了现代Web开发技术，包括HTML5、CSS3和JavaScript，实现了流畅的动画效果和响应式设计。</p>
            </div>
        </div>
    </div>
    
    <!-- 视频模态框 -->
    <div class="modal" id="video-modal">
        <div class="modal-content">
            <div class="modal-header">
                <h2 class="modal-title">视频功能</h2>
                <button class="close-btn" onclick="closeModal('video-modal')">&times;</button>
            </div>
            <div class="modal-body">
                <p>视频播放功能</p>
                <div class="unavailable">
                    <i class="fas fa-tools"></i>
                    <p>视频功能正在开发中，尚未开放</p>
                    <p>我们正在努力开发视频播放功能，将为您带来精彩的视频内容。</p>
                    <p>请耐心等待，我们会在后续更新中开放此功能！</p>
                </div>
                <p>您可以关注页面更新，一旦视频功能完成，我们将立即通知您。</p>
            </div>
        </div>
    </div>

    <script>
        // 打开欢迎模态框
        function openWelcome() {
            document.getElementById('welcome-modal').style.display = 'flex';
        }
        
        // 打开开发者模态框
        function openDeveloper() {
            document.getElementById('developer-modal').style.display = 'flex';
        }
        
        // 打开视频模态框
        function openVideo() {
            document.getElementById('video-modal').style.display = 'flex';
        }
        
        // 关闭模态框
        function closeModal(modalId) {
            document.getElementById(modalId).style.display = 'none';
        }
        
        // 点击模态框外部关闭
        window.onclick = function(event) {
            const modals = document.querySelectorAll('.modal');
            modals.forEach(modal => {
                if (event.target === modal) {
                    modal.style.display = 'none';
                }
            });
        }
        
        // 添加卡片点击事件
        document.addEventListener('DOMContentLoaded', function() {
            const cards = document.querySelectorAll('.card');
            
            cards.forEach(card => {
                card.addEventListener('click', function(e) {
                    // 防止按钮点击触发两次
                    if (e.target.classList.contains('card-button')) return;
                    
                    const cardId = this.id;
                    
                    if (cardId === 'welcome-card') {
                        openWelcome();
                    } else if (cardId === 'developer-card') {
                        openDeveloper();
                    } else if (cardId === 'video-card') {
                        openVideo();
                    }
                });
            });
        });
    </script>
</body>
</html>
