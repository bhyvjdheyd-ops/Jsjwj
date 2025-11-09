<!DOCTYPE html>
<html lang="fa">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>خبر فوری آنلاین</title>
  <style>
    body {
      background-color: #111;
      color: #fff;
      font-family: sans-serif;
      text-align: center;
    }
    h1 {
      color: #ff3b3b;
    }
    #news {
      margin: 20px auto;
      max-width: 600px;
      text-align: right;
      line-height: 1.8;
    }
    .item {
      background: #222;
      border-radius: 10px;
      padding: 10px;
      margin: 10px 0;
    }
  </style>
</head>
<body>
  <h1>📰 خبر فوری آنلاین</h1>
  <div id="news">در حال بارگذاری خبرها...</div>

  <script>
    async function loadNews() {
      try {
        const res = await fetch("https://api.rss2json.com/v1/api.json?rss_url=https://www.khabaronline.ir/rss");
        const data = await res.json();
        const container = document.getElementById("news");
        container.innerHTML = "";
        data.items.slice(0, 10).forEach(item => {
          const div = document.createElement("div");
          div.className = "item";
          div.innerHTML = `<b>${item.title}</b><br>${item.pubDate}<br><a href="${item.link}" target="_blank" style="color:#4af">مشاهده خبر</a>`;
          container.appendChild(div);
        });
      } catch {
        document.getElementById("news").innerHTML = "❌ خطا در دریافت خبرها";
      }
    }
    loadNews();
  </script>
</body>
</html>
