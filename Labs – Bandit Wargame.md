<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8" />
  <title>Bandit Walkthrough - Enhanced Writeup</title>
  <style>
    body {
      font-family: Arial, sans-serif;
      margin: 20px;
      line-height: 1.6;
      background: #f9f9f9;
      color: #333;
    }
    h1, h2, h3 {
      color: #222;
    }
    .level {
      border: 1px solid #ddd;
      background: #fff;
      padding: 15px;
      margin: 20px 0;
      border-radius: 10px;
      box-shadow: 0 2px 4px rgba(0,0,0,0.05);
    }
    .level img {
      max-width: 100%;
      border: 1px solid #ccc;
      border-radius: 6px;
      margin-top: 10px;
    }
    pre {
      background: #272822;
      color: #f8f8f2;
      padding: 10px;
      border-radius: 6px;
      overflow-x: auto;
    }
    a {
      color: #0066cc;
      text-decoration: none;
    }
    a:hover {
      text-decoration: underline;
    }
  </style>
</head>
<body>
  <h1>Bandit Walkthrough - Enhanced Writeup</h1>

  <h2>Introduction</h2>
  <p>
    <a href="https://overthewire.org/wargames/bandit/">Bandit</a> هي لعبة تعليمية من OverTheWire تساعد المبتدئين في تعلم أوامر Linux الأساسية وأساسيات أمن المعلومات. الفكرة أنك تنتقل من مستوى لآخر عبر إيجاد كلمة مرور مخفية باستخدام أوامر مختلفة مثل <code>ssh</code>, <code>ls</code>, <code>cat</code>, <code>find</code>, <code>grep</code>, وغيرها.
  </p>

  <p>في هذا الدليل، لكل مستوى ستجد: الوصف، الأوامر، والنتيجة (مع صورة توضيحية).</p>

  <!-- Example structure repeated for each level -->

  <div class="level">
    <h3>Level 0 → Level 1</h3>
    <p>المطلوب: تسجيل الدخول عبر SSH.</p>
    <pre><code>ssh bandit0@bandit.labs.overthewire.org -p 2220</code></pre>
    <img src="./assets/0to1.png" alt="0to1" />
    <p><a href="https://overthewire.org/wargames/bandit/bandit0.html">رابط المستوى الرسمي</a></p>
  </div>

  <div class="level">
    <h3>Level 1 → Level 2</h3>
    <p>المطلوب: قراءة محتوى ملف <code>readme</code> في مجلد المنزل.</p>
    <pre><code>ls
cat readme</code></pre>
    <img src="./assets/1to2.png" alt="1to2" />
    <p><a href="https://overthewire.org/wargames/bandit/bandit1.html">رابط المستوى الرسمي</a></p>
  </div>

  <div class="level">
    <h3>Level 2 → Level 3</h3>
    <p>المطلوب: التعامل مع ملف اسمه "-".</p>
    <pre><code>ls
cat ./-</code></pre>
    <img src="./assets/2to3.png" alt="2to3" />
    <p><a href="https://overthewire.org/wargames/bandit/bandit2.html">رابط المستوى الرسمي</a></p>
  </div>

  <!-- ... كرر نفس النمط لبقية المستويات مع شرح وأوامر وصورة ... -->

  <div class="level">
    <h3>Level 28 → Level 29</h3>
    <p>آخر المستويات في الملف الحالي.</p>
    <img src="./assets/28to29.png" alt="28to29" />
    <p><a href="https://overthewire.org/wargames/bandit/bandit28.html">رابط المستوى الرسمي</a></p>
  </div>

  <h2>Conclusion</h2>
  <p>
    خلال هذه التحديات تعلمنا:
  </p>
  <ul>
    <li>التنقل بين الملفات واستخدام <code>ls</code>, <code>cd</code>, <code>cat</code>.</li>
    <li>استخدام <code>file</code>, <code>strings</code>, <code>grep</code>, <code>sort</code>, <code>uniq</code>.</li>
    <li>فك تشفير base64 و ROT13.</li>
    <li>البحث عبر <code>find</code> بالاعتماد على الحجم أو المالك أو النوع.</li>
  </ul>
  <p>
    هذي الأدوات أساسية لأي شخص يبي يتعلم Linux والأمن المعلوماتي. إكمال لعبة Bandit يعتبر خطوة قوية قبل الدخول لتحديات أصعب.
  </p>
</body>
</html>
