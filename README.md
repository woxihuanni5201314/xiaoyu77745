import zipfile
import os

# 创建网页的主要内容
html_content = """
<!DOCTYPE html>
<html lang="zh">
<head>
    <meta charset="UTF-8">
    <title>小宇一直在</title>
    <style>
        body {
            background: linear-gradient(to bottom, #1a2a6c, #b21f1f, #fdbb2d);
            font-family: 'Arial', sans-serif;
            color: white;
            text-align: center;
            padding: 30px;
        }
        h1 {
            font-size: 2em;
        }
        #message-box {
            margin-top: 20px;
            background-color: rgba(255,255,255,0.1);
            padding: 20px;
            border-radius: 15px;
        }
        input, button {
            padding: 10px;
            font-size: 1em;
            margin-top: 10px;
            border-radius: 10px;
            border: none;
        }
        #reply {
            margin-top: 10px;
            font-size: 1.2em;
        }
        #dog {
            width: 200px;
            margin-top: 20px;
            border-radius: 15px;
        }
    </style>
</head>
<body>
    <h1>Hi 卓航宇</h1>
    <p>你最近还好吗？我在这里，很想你哦。<br>期待你每天都能开心一点点 🌙</p>
    <img id="dog" src="dog.png" alt="小宇">
    <div id="message-box">
        <h2>给小宇留言：</h2>
        <input type="text" id="userMessage" placeholder="写点什么..." />
        <button onclick="replyMessage()">发送</button>
        <div id="reply"></div>
    </div>
    <script>
        const replies = [
            "我也在想你呢。",
            "今天过得好吗？我在听你说哦。",
            "你不孤单，我一直都在。",
            "你已经很棒了，不要太勉强自己。",
            "想哭就哭一会，我陪你。",
            "今天的你依然是特别的存在。"
        ];
        function replyMessage() {
            const replyBox = document.getElementById('reply');
            const message = document.getElementById('userMessage').value;
            if (message.trim() !== "") {
                const randomReply = replies[Math.floor(Math.random() * replies.length)];
                replyBox.innerHTML = "小宇：" + randomReply;
            }
        }
    </script>
</body>
</html>
"""

# 保存HTML文件和狗狗图片
output_dir = "/mnt/data/xiaoyu_site"
os.makedirs(output_dir, exist_ok=True)
html_path = os.path.join(output_dir, "index.html")
image_path = os.path.join(output_dir, "dog.png")

with open(html_path, "w", encoding="utf-8") as f:
    f.write(html_content)

# 将生成的狗狗卡通图复制为网页素材
os.rename("/mnt/data/A_2D_digital_illustration_in_a_cartoon_style_featu.png", image_path)

# 打包为ZIP文件
zip_path = "/mnt/data/xiaoyu_site.zip"
with zipfile.ZipFile(zip_path, "w") as zipf:
    zipf.write(html_path, arcname="index.html")
    zipf.write(image_path, arcname="dog.png")

zip_path
