<!DOCTYPE html>
<html lang="id">
<head>
  <meta charset="UTF-8">
  <title>Perpustakaan Digital E-Book</title>
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
    .upload-section {
      background: white;
      padding: 15px;
      margin: 20px;
      border-radius: 12px;
      text-align: center;
      box-shadow: 0 4px 8px rgba(0,0,0,0.1);
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
      background: rgba(0,0,0,0.8);
      justify-content: center;
      align-items: center;
    }
    .modal-content {
      background: white;
      padding: 10px;
      width: 90%;
      height: 90%;
      border-radius: 12px;
      display: flex;
      flex-direction: column;
    }
    .modal-content iframe {
      flex: 1;
      border: none;
      border-radius: 8px;
    }
    .close {
      align-self: flex-end;
      font-size: 20px;
      cursor: pointer;
      color: red;
      margin-bottom: 8px;
    }
  </style>
</head>
<body>
  <header>
    <h1>📚 Perpustakaan Digital - E-Book</h1>
  </header>

  <!-- Upload Buku -->
  <div class="upload-section">
    <input type="file" id="upload" accept="application/pdf">
    <button onclick="addBook()">Tambah Buku</button>
  </div>

  <!-- Daftar Buku -->
  <div class="container" id="bookList"></div>

  <!-- Modal PDF Reader -->
  <div class="modal" id="ebookModal">
    <div class="modal-content">
      <span class="close" onclick="closeBook()">&times;</span>
      <iframe id="pdfViewer"></iframe>
    </div>
  </div>

  <script>
    let books = [];

    function addBook() {
      const fileInput = document.getElementById('upload');
      const file = fileInput.files[0];

      if (file) {
        const url = URL.createObjectURL(file);
        const book = {
          title: file.name,
          url: url
        };
        books.push(book);
        renderBooks();
      } else {
        alert("Pilih file PDF terlebih dahulu!");
      }
    }

    function renderBooks() {
      const list = document.getElementById('bookList');
      list.innerHTML = "";
      books.forEach((book, index) => {
        list.innerHTML += `
          <div class="book">
            <h3>${book.title}</h3>
            <button onclick="openBook(${index})">Baca</button>
          </div>
        `;
      });
    }

    function openBook(index) {
      document.getElementById("ebookModal").style.display = "flex";
      document.getElementById("pdfViewer").src = books[index].url;
    }

    function closeBook() {
      document.getElementById("ebookModal").style.display = "none";
      document.getElementById("pdfViewer").src = "";
    }
  </script>
</body>
</html>
