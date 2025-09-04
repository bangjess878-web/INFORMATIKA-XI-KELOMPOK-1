<!DOCTYPE html>
<html lang="id">
<head>
  <meta charset="UTF-8">
  <title>Perpustakaan E-Book</title>
  <style>
    body {
      font-family: Arial, sans-serif;
      background: #f3f4f6;
      margin: 0;
      padding: 0;
    }
    header {
      background: #1f2937;
      color: white;
      padding: 15px;
      text-align: center;
    }
    .container {
      display: grid;
      grid-template-columns: repeat(auto-fill, minmax(220px, 1fr));
      gap: 20px;
      padding: 20px;
    }
    .book {
      background: white;
      border-radius: 12px;
      box-shadow: 0 4px 8px rgba(0,0,0,0.1);
      padding: 15px;
      text-align: center;
      transition: transform 0.2s;
    }
    .book:hover {
      transform: scale(1.05);
    }
    .book img {
      width: 100px;
      height: 150px;
      object-fit: cover;
      margin-bottom: 10px;
      border-radius: 8px;
    }
    .book h3 {
      font-size: 18px;
      margin: 10px 0;
    }
    .book button {
      background: #2563eb;
      color: white;
      border: none;
      padding: 8px 12px;
      border-radius: 8px;
      cursor: pointer;
      font-size: 14px;
    }
    .book button:hover {
      background: #1d4ed8;
    }
    /* Modal */
    .modal {
      display: none;
      position: fixed;
      top: 0; left: 0;
      width: 100%; height: 100%;
      background: rgba(0,0,0,0.7);
      justify-content: center;
      align-items: center;
    }
    .modal-content {
      background: white;
      padding: 20px;
      width: 80%;
      height: 80%;
      overflow-y: auto;
      border-radius: 12px;
      box-shadow: 0 4px 12px rgba(0,0,0,0.2);
    }
    .close {
      float: right;
      font-size: 20px;
      cursor: pointer;
      color: red;
    }
  </style>
</head>
<body>
  <header>
    <h1>📚 Perpustakaan Digital - E-Book</h1>
  </header>
  
  <div class="container">
    <div class="book">
      <img src="https://via.placeholder.com/100x150" alt="Buku 1">
      <h3>Buku Pemrograman</h3>
      <button onclick="openBook('pemrograman')">Baca</button>
    </div>
    <div class="book">
      <img src="https://via.placeholder.com/100x150" alt="Buku 2">
      <h3>Buku Sejarah</h3>
      <button onclick="openBook('sejarah')">Baca</button>
    </div>
    <div class="book">
      <img src="https://via.placeholder.com/100x150" alt="Buku 3">
      <h3>Buku Fiksi</h3>
      <button onclick="openBook('fiksi')">Baca</button>
    </div>
  </div>
  
  <!-- Modal E-Book -->
  <div class="modal" id="ebookModal">
    <div class="modal-content">
      <span class="close" onclick="closeBook()">&times;</span>
      <h2 id="bookTitle"></h2>
      <p id="bookContent"></p>
    </div>
  </div>

  <script>
    const books = {
      pemrograman: {
        title: "Dasar-Dasar Pemrograman",
        content: "Isi buku ini membahas tentang logika pemrograman, algoritma, dan dasar bahasa pemrograman..."
      },
      sejarah: {
        title: "Sejarah Dunia",
        content: "Buku ini menceritakan perjalanan peradaban manusia dari zaman kuno hingga modern..."
      },
      fiksi: {
        title: "Cerita Fiksi Fantasi",
        content: "Kisah petualangan seorang anak muda yang menemukan dunia lain penuh keajaiban..."
      }
    };

    function openBook(bookKey) {
      document.getElementById("ebookModal").style.display = "flex";
      document.getElementById("bookTitle").innerText = books[bookKey].title;
      document.getElementById("bookContent").innerText = books[bookKey].content;
    }

    function closeBook() {
      document.getElementById("ebookModal").style.display = "none";
    }
  </script>
</body>
</html>
