<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8" />

  <head/>
<body>
  <h1>Bandit Walkthrough - Levels</h1>

  <h2>Introduction</h2>
  <p>
    <a href="https://overthewire.org/wargames/bandit/">Bandit</a> is a wargame from OverTheWire. It teaches the fundamentals of Linux command-line usage and basic security concepts. The objective is to find passwords hidden on the system to progress from one level to the next.
  </p>

  <p>Each level below contains: a description, the key commands, a screenshot, and a link to the official page.</p>

  <div class="level">
    <h3>Level 0 → Level 1</h3>
    <p>Task: Log in via SSH.</p>
    <pre><code>ssh bandit0@bandit.labs.overthewire.org -p 2220</code></pre>
    <img src="../assets/0to1.png" alt="0to1" />
    <p><a href="https://overthewire.org/wargames/bandit/bandit0.html">Official page</a></p>
  </div>

  <div class="level">
    <h3>Level 1 → Level 2</h3>
    <p>Task: Read the content of the <code>readme</code> file in the home directory.</p>
    <pre><code>ls
cat readme</code></pre>
    <img src="../assets/1to2.png" alt="1to2" />
    <p><a href="https://overthewire.org/wargames/bandit/bandit1.html">Official page</a></p>
  </div>

  <div class="level">
    <h3>Level 2 → Level 3</h3>
    <p>Task: Handle a file named "-".</p>
    <pre><code>ls
cat ./-</code></pre>
    <img src="../assets/2to3.png" alt="2to3" />
    <p><a href="https://overthewire.org/wargames/bandit/bandit2.html">Official page</a></p>
  </div>

  <div class="level">
    <h3>Level 3 → Level 4</h3>
    <p>Task: Work with filenames containing spaces.</p>
    <pre><code>ls
cat "spaces in this filename"</code></pre>
    <img src="../assets/3to4.png" alt="3to4" />
    <p><a href="https://overthewire.org/wargames/bandit/bandit3.html">Official page</a></p>
  </div>

  <div class="level">
    <h3>Level 4 → Level 5</h3>
    <p>Task: Find and read hidden files.</p>
    <pre><code>ls -a inhere
cat inhere/.hidden</code></pre>
    <img src="../assets/4to5.png" alt="4to5" />
    <p><a href="https://overthewire.org/wargames/bandit/bandit4.html">Official page</a></p>
  </div>

  <div class="level">
    <h3>Level 5 → Level 6</h3>
    <p>Task: Identify human-readable files among many.</p>
    <pre><code>file ./*
cat ./-file07</code></pre>
    <img src="../assets/5to6.png" alt="5to6" />
    <p><a href="https://overthewire.org/wargames/bandit/bandit5.html">Official page</a></p>
  </div>

  <div class="level">
    <h3>Level 6 → Level 7</h3>
    <p>Task: Find a file based on size and non-executable property.</p>
    <pre><code>find . -type f -size 1033c ! -executable</code></pre>
    <img src="../assets/6to7.png" alt="6to7" />
    <p><a href="https://overthewire.org/wargames/bandit/bandit6.html">Official page</a></p>
  </div>

  <div class="level">
    <h3>Level 7 → Level 8</h3>
    <p>Task: Find a file based on ownership (user and group).</p>
    <pre><code>find / -type f -user bandit7 -group bandit6 -size 33c 2>/dev/null</code></pre>
    <img src="../assets/7to8.png" alt="7to8" />
    <p><a href="https://overthewire.org/wargames/bandit/bandit7.html">Official page</a></p>
  </div>

  <div class="level">
    <h3>Level 8 → Level 9</h3>
    <p>Task: Use <code>grep</code> to search within a large file.</p>
    <pre><code>grep millionth data.txt</code></pre>
    <img src="../assets/8to9.png" alt="8to9" />
    <p><a href="https://overthewire.org/wargames/bandit/bandit8.html">Official page</a></p>
  </div>

  <div class="level">
    <h3>Level 9 → Level 10</h3>
    <p>Task: Find the unique line among many duplicates.</p>
    <pre><code>sort data.txt | uniq -u</code></pre>
    <img src="../assets/9to10.png" alt="9to10" />
    <p><a href="https://overthewire.org/wargames/bandit/bandit9.html">Official page</a></p>
  </div>

  <div class="level">
    <h3>Level 10 → Level 11</h3>
    <p>Task: Extract human-readable strings from a binary file.</p>
    <pre><code>strings data.txt | grep ===</code></pre>
    <img src="../assets/10to11.png" alt="10to11" />
    <p><a href="https://overthewire.org/wargames/bandit/bandit10.html">Official page</a></p>
  </div>

  <div class="level">
    <h3>Level 11 → Level 12</h3>
    <p>Task: Decode Base64 encoded content.</p>
    <pre><code>base64 -d data.txt</code></pre>
    <img src="../assets/11to12.png" alt="11to12" />
    <p><a href="https://overthewire.org/wargames/bandit/bandit11.html">Official page</a></p>
  </div>

  <div class="level">
    <h3>Level 12 → Level 13</h3>
    <p>Task: Decode ROT13 substitution using <code>tr</code>.</p>
    <pre><code>cat data.txt | tr 'A-Za-z' 'N-ZA-Mn-za-m'</code></pre>
    <img src="../assets/12to13.png" alt="12to13" />
    <p><a href="https://overthewire.org/wargames/bandit/bandit12.html">Official page</a></p>
  </div>

  <h2>Conclusion</h2>
  <p>Up to Level 13, you’ve practiced:</p>
  <ul>
    <li>Logging in with SSH.</li>
    <li>Working with files and directories (including hidden or oddly named ones).</li>
    <li>Using commands like <code>cat</code>, <code>file</code>, <code>strings</code>, <code>grep</code>, <code>sort</code>, and <code>uniq</code>.</li>
    <li>Decoding techniques (Base64, ROT13).</li>
    <li>Searching with <code>find</code> based on size, ownership, and permissions.</li>
  </ul>
  <p>
    These are core Linux and security skills that will be useful for further challenges in Bandit and beyond.
  </p>
</body>
</html>
