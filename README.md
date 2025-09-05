<!DOCTYPE html>
<html lang="id">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Aplikasi Pencatatan Buku</title>
    <!-- CSS dasar (bisa diganti dengan Tailwind/Bootstrap) -->
    <style>
        body {
            font-family: Arial, sans-serif;
            margin: 0;
            padding: 0;
            background-color: #f4f4f4;
        }
        .container {
            width: 80%;
            margin: auto;
            overflow: hidden;
        }
        header {
            background: #508bff;
            color: white;
            padding-top: 30px;
            min-height: 70px;
            border-bottom: 3px solid #3D71C9;
        }
        header a {
            color: #fff;
            text-decoration: none;
            text-transform: uppercase;
            font-size: 16px;
        }
        header ul {
            padding: 0;
            margin: 0;
            list-style: none;
            overflow: hidden;
        }
        header li {
            float: left;
            display: inline;
            padding: 0 20px 0 20px;
        }
        header #branding {
            float: left;
        }
        header #branding h1 {
            margin: 0;
        }
        header nav {
            float: right;
            margin-top: 10px;
        }
        /* Style untuk form */
        form {
            padding: 15px;
        }
        form label {
            display: block;
            margin-bottom: 5px;
        }
        form input[type="text"],
        form input[type="number"],
        form textarea {
            width: 100%;
            padding: 8px;
            margin-bottom: 10px;
            border-radius: 4px;
            border: 1px solid #ddd;
        }
        form button {
            background-color: #508bff;
            color: white;
            padding: 10px 15px;
            border: none;
            border-radius: 4px;
            cursor: pointer;
        }
        /* Style untuk tabel */
        table {
            width: 100%;
            border-collapse: collapse;
            margin-top: 20px;
        }
        table, th, td {
            border: 1px solid #ddd;
            padding: 8px;
            text-align: left;
        }
        th {
            background-color: #508bff;
            color: white;
        }
    </style>
</head>
<body>
    <header>
        <div class="container">
            <div id="branding">
                <h1><span class="highlight">Catatan</span> Buku</h1>
            </div>
            <nav>
                <ul>
                    <li><a href="index.html">Beranda</a></li>
                    <li><a href="login.html">Login</a></li>
                    <li><a href="daftar.html">Daftar</a></li>
                </ul>
            </nav>
        </div>
    </header>

    <div class="container">
        <h2>Form Input Data Buku</h2>
        <form id="bookForm">
            <label for="judul">Judul Buku:</label>
            <input type="text" id="judul" name="judul" required>

            <label for="penulis">Penulis:</label>
            <input type="text" id="penulis" name="penulis" required>

            <label for="tahun">Tahun Terbit:</label>
            <input type="number" id="tahun" name="tahun" required>

            <label for="kategori">Kategori:</label>
            <input type="text" id="kategori" name="kategori" required>

            <button type="submit">Simpan</button>
        </form>

        <h2>Daftar Buku</h2>
        <table id="bookTable">
            <thead>
                <tr>
                    <th>Judul</th>
                    <th>Penulis</th>
                    <th>Tahun Terbit</th>
                    <th>Kategori</th>
                </tr>
            </thead>
            <tbody>
                <!-- Data buku akan ditampilkan di sini -->
            </tbody>
        </table>
    </div>

    <!-- JavaScript dasar -->
    <script>
        document.getElementById('bookForm').addEventListener('submit', function(e) {
            e.preventDefault();

            const judul = document.getElementById('judul').value;
            const penulis = document.getElementById('penulis').value;
            const tahun = document.getElementById('tahun').value;
            const kategori = document.getElementById('kategori').value;

            // Tambahkan data ke tabel
            const table = document.getElementById('bookTable').getElementsByTagName('tbody')[0];
            const newRow = table.insertRow(table.rows.length);
            const cell1 = newRow.insertCell(0);
            const cell2 = newRow.insertCell(1);
            const cell3 = newRow.insertCell(2);
            const cell4 = newRow.insertCell(3);

            cell1.innerHTML = judul;
            cell2.innerHTML = penulis;
            cell3.innerHTML = tahun;
            cell4.innerHTML = kategori;

            // Reset form
            document.getElementById('bookForm').reset();
        });
    </script>
</body>
</html>
