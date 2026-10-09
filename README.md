<!DOCTYPE html>
<html lang="zh-TW">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>💖 靈魂伴侶與戀愛潛能測驗</title>
  <style>
    body {
      font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
      background: linear-gradient(135deg, #ff9a9e 0%, #fecfef 99%, #fecfef 100%);
      display: flex;
      justify-content: center;
      align-items: center;
      min-height: 100vh;
      margin: 0;
      padding: 20px;
      box-sizing: border-box;
    }
    .card {
      background: white;
      padding: 30px;
      border-radius: 20px;
      box-shadow: 0 15px 30px rgba(0,0,0,0.15);
      width: 100%;
      max-width: 400px;
      text-align: center;
    }
    h1 {
      color: #ff4b72;
      font-size: 22px;
      margin-bottom: 20px;
    }
    .input-group {
      margin-bottom: 20px;
      text-align: left;
    }
    label {
      display: block;
      font-size: 14px;
      color: #666;
      margin-bottom: 8px;
    }
    input[type="text"] {
      width: 100%;
      padding: 12px;
      border: 2px solid #ffd3e0;
      border-radius: 10px;
      box-sizing: border-box;
      font-size: 16px;
      outline: none;
    }
    input[type="text"]:focus {
      border-color: #ff4b72;
    }
    .btn {
      background: #ff4b72;
      color: white;
      border: none;
      padding: 12px 30px;
      font-size: 16px;
      border-radius: 25px;
      cursor: pointer;
      width: 100%;
      font-weight: bold;
      transition: transform 0.2s, background 0.2s;
    }
    .btn:hover {
      background: #e03a5f;
      transform: scale(1.02);
    }
    .option-btn {
      background: #f8f9fa;
      border: 2px solid #e9ecef;
      padding: 12px;
      border-radius: 10px;
      margin-bottom: 10px;
      cursor: pointer;
      text-align: left;
      font-size: 15px;
      transition: all 0.2s;
    }
    .option-btn:hover {
      border-color: #ff4b72;
      background: #fff5f7;
    }
    .hidden {
      display: none;
    }
    .loader {
      border: 5px solid #f3f3f3;
      border-top: 5px solid #ff4b72;
      border-radius: 50%;
      width: 50px;
      height: 50px;
      animation: spin 1s linear infinite;
      margin: 20px auto;
    }
    @keyframes spin {
      0% { transform: rotate(0deg); }
      100% { transform: rotate(360deg); }
    }
    .result-box {
      background: #fff0f3;
      border: 2px dashed #ff4b72;
      border-radius: 15px;
      padding: 20px;
      margin-top: 15px;
    }
  </style>
</head>
<body>

  <div class="card">
    <!-- 第一頁：輸入姓名 -->
    <div id="step1">
      <h1>💖 靈魂伴侶與戀愛測驗</h1>
      <p style="color: #888; font-size: 14px; margin-bottom: 25px;">請輸入真實資料以精準計算靈魂波長</p>
      <div class="input-group">
        <label for="userName">你的姓名：</label>
        <input type="text" id="userName" placeholder="請輸入姓名">
      </div>
      <button class="btn" onclick="startQuiz()">開始深度分析</button>
    </div>

    <!-- 第二頁：選擇題 -->
    <div id="step2" class="hidden">
      <h1 id="questionTitle">題目載入中...</h1>
      <div id="optionsContainer"></div>
    </div>

    <!-- 第三頁：假裝計算中 -->
    <div id="step3" class="hidden">
      <h1>🔮 AI 深度運算中...</h1>
      <div class="loader"></div>
      <p id="loadingText" style="color: #666; font-size: 14px;">正在比對全球戀愛資料庫...</p>
    </div>

    <!-- 第四頁：爆笑結果 -->
    <div id="step4" class="hidden">
      <h1 style="font-size: 26px;">🎉 分析結果揭曉 🎉</h1>
      <div class="result-box">
        <h2 id="resultName" style="color: #ff4b72; margin-top: 0;"></h2>
        <p style="font-size: 18px; font-weight: bold; color: #d63384;">
          🌸 你的命定戀愛屬性：<br><span style="font-size: 24px; color: #ff1493;">100% 經典拉拉 (Lesbian)！</span>
        </p>
        <hr style="border: 0; border-top: 1px solid #ffd3e0; margin: 15px 0;">
        <p style="font-size: 14px; color: #555; text-align: left; line-height: 1.6;">
          <strong>【AI 靈魂報告】</strong><br>
          經過大數據深度比對，你的靈魂磁場顯示你對男孩子毫無興趣！你天生就具備強大的「姬圈天菜」潛質，唯有女孩子才能解鎖你的心扉！<br><br>
          <strong>【轉運建議】</strong><br>
          恭喜覺醒！請於今日放學前請你的好朋友喝一杯奶茶，以順利維持你的百合運勢！
        </p>
      </div>
    </div>
  </div>

  <script>
    let name = "";
    let currentQ = 0;

    const questions = [
      {
        title: "Q1. 第一眼看到心儀對象，你最注意哪裡？",
        options: ["眼神與笑容", "穿搭風格與品味", "散發出來的獨特氣質"]
      },
      {
        title: "Q2. 你理想中的浪漫約會是？",
        options: ["漫步在夜晚的海邊", "一起去逛文青市集", "窩在家裡窩著看電影"]
      },
      {
        title: "Q3. 在感情中，你最不能忍受什麼？",
        options: ["已讀不回或消失", "沒有共同話題", "缺乏個人隱私空間"]
      }
    ];

    function startQuiz() {
      name = document.getElementById('userName').value.trim();
      if (!name) {
        alert('請先輸入你的名字喔！');
        return;
      }
      document.getElementById('step1').classList.add('hidden');
      document.getElementById('step2').classList.remove('hidden');
      showQuestion();
    }

    function showQuestion() {
      if (currentQ < questions.length) {
        const q = questions[currentQ];
        document.getElementById('questionTitle').innerText = q.title;
        const container = document.getElementById('optionsContainer');
        container.innerHTML = "";
        
        q.options.forEach(opt => {
          const btn = document.createElement('div');
          btn.className = 'option-btn';
          btn.innerText = opt;
          btn.onclick = nextQuestion;
          container.appendChild(btn);
        });
      } else {
        showLoading();
      }
    }

    function nextQuestion() {
      currentQ++;
      showQuestion();
    }

    function showLoading() {
      document.getElementById('step2').classList.add('hidden');
      document.getElementById('step3').classList.remove('hidden');

      setTimeout(() => {
        document.getElementById('loadingText').innerText = "解析靈魂波長與戀愛磁場中...";
      }, 1000);

      setTimeout(() => {
        document.getElementById('loadingText').innerText = "即將生成最終報告...";
      }, 2000);

      setTimeout(() => {
        showResult();
      }, 3000);
    }

    function showResult() {
      document.getElementById('step3').classList.add('hidden');
      document.getElementById('step4').classList.remove('hidden');
      document.getElementById('resultName').innerText = `${name} 的靈魂測驗結果`;
    }
  </script>

</body>
</html>
