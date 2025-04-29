[Uploa#AIzaSyA8eYCgItUOebxOpCezDaV4UZyO49ej5QI
index.html -->
<!DOCTYPE html>
<html lang="zh-TW">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Gemini AI 聊天室</title>
    ...existing code...
</head>
<body>
    <h1>Gemini AI 聊天室</h1>
    <div id="chatbox"></div>
    <div id="input-container">
        <input type="text" id="user-input" placeholder="請輸入訊息...">
        <button onclick="sendMessage()">發送</button>
    </div>

    <script>
        const API_KEY = 'AIzaSyA8eYCgItUOebxOpCezDaV4UZyO49ej5QI';
        const API_URL = 'https://generativelanguage.googleapis.com/v1beta/models/gemini-2.0-flash:generateContent';

        async function sendMessage() {
            const input = document.getElementById('user-input');
            const message = input.value.trim();
            if (!message) return;

            addMessage(message, 'user-message');
            input.value = '';

            try {
                const response = await fetch(`${API_URL}?key=${API_KEY}`, {
                    method: 'POST',
                    headers: {
                        'Content-Type': 'application/json',
                    },
                    body: JSON.stringify({
                        contents: [{
                            parts: [{
                                text: message
                            }]
                        }]
                    })
                });

                if (!response.ok) {
                    throw new Error(`API 錯誤: ${response.status}`);
                }

                const data = await response.json();
                
                if (data.candidates && data.candidates[0]?.content?.parts?.[0]?.text) {
                    const aiResponse = data.candidates[0].content.parts[0].text;
                    addMessage(aiResponse, 'ai-message');
                } else {
                    throw new Error('無效的 API 回應格式');
                }
            } catch (error) {
                console.error('Error:', error);
                addMessage(`錯誤: ${error.message}`, 'ai-message');
            }
        }

        function addMessage(text, className) {
            const chatbox = document.getElementById('chatbox');
            const messageDiv = document.createElement('div');
            messageDiv.className = `message ${className}`;
            messageDiv.textContent = text;
            chatbox.appendChild(messageDiv);
            chatbox.scrollTop = chatbox.scrollHeight;
        }

        document.getElementById('user-input').addEventListener('keypress', function(e) {
            if (e.key === 'Enter') {
                sendMessage();
            }
        });
    </script>
</body>
</html>ding index.html…]()
