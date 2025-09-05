<!DOCTYPE html>
<html lang="id">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Aplikasi Pencatatan Buku</title>
    <!-- Tailwind CSS -->
    <link href="https://cdn.jsdelivr.net/npm/tailwindcss@2.2.19/dist/tailwind.min.css" rel="stylesheet">
    <!-- Font Awesome -->
    <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.0.0/css/all.min.css" integrity="sha512-9usAa10IRO0HhonpyAIVpjrylPvoDwiPUiKdWk5t3PyolY1cOd4DSE0Ga+ri4AuTroPR5aQvXU9xC6qOPnzFeg==" crossorigin="anonymous" referrerpolicy="no-referrer" />
    <style>
        /* Tambahan style untuk mempercantik tampilan */
        body {
            font-family: 'Arial', sans-serif;
            background-color: #f0f2f5;
        }
        .book-item {
            background-color: white;
            border-radius: 0.5rem;
            padding: 1rem;
            margin-bottom: 1rem;
            box-shadow: 0 1px 3px 0 rgba(0, 0, 0, 0.1), 0 1px 2px 0 rgba(0, 0, 0, 0.06);
        }
    </style>
</head>
<body class="bg-gray-100">
    <!-- Header -->
    <header class="bg-blue-500 text-white py-4">
        <div class="container mx-auto flex items-center justify-between">
            <h1 class="text-2xl font-semibold">
                <i class="fas fa-book mr-2"></i>
                Catatan Buku
            </h1>
            <nav>
                <a href="#" class="hover:text-blue-200 mr-4">Beranda</a>
                <a href="#" class="hover:text-blue-200">Tentang</a>
            </nav>
        </div>
    </header>

    <!-- Main Content -->
    <div class="container mx-auto mt-8">
        <!-- Form Input Buku -->
        <div class="bg-white shadow-md rounded px-8 pt-6 pb-8 mb-4">
            <h2 class="text-xl font-semibold mb-4">Tambah Buku Baru</h2>
            <form id="bookForm">
                <div class="mb-4">
                    <label class="block text-gray-700 text-sm font-bold mb-2" for="judul">Judul Buku:</label>
                    <input class="shadow appearance-none border rounded w-full py-2 px-3 text-gray-700 leading-tight focus:outline-none focus:shadow-outline" id="judul" name="judul" type="text" placeholder="Judul" required>
                </div>
                <div class="mb-4">
                    <label class="block text-gray-700 text-sm font-bold mb-2" for="penulis">Penulis:</label>
                    <input class="shadow appearance-none border rounded w-full py-2 px-3 text-gray-700 leading-tight focus:outline-none focus:shadow-outline" id="penulis" name="penulis" type="text" placeholder="Penulis" required>
                </div>
                <div class="mb-4">
                    <label class="block text-gray-700 text-sm font-bold mb-2" for="tahun">Tahun Terbit:</label>
                    <input class="shadow appearance-none border rounded w-full py-2 px-3 text-gray-700 leading-tight focus:outline-none focus:shadow-outline" id="tahun" name="tahun" type="number" placeholder="Tahun" required>
                </div>
                <div class="mb-6">
                    <label class="block text-gray-700 text-sm font-bold mb-2" for="kategori">Kategori:</label>
                    <input class="shadow appearance-none border rounded w-full py-2 px-3 text-gray-700 leading-tight focus:outline-none focus:shadow-outline" id="kategori" name="kategori" type="text" placeholder="Kategori" required>
                </div>
                <div class="flex items-center justify-between">
                    <button class="bg-blue-500 hover:bg-blue-700 text-white font-bold py-2 px-4 rounded focus:outline-none focus:shadow-outline" type="submit">
                        Simpan
                    </button>
                </div>
            </form>
        </div>

        <!-- Daftar Buku -->
        <div class="mt-8">
            <h2 class="text-xl font-semibold mb-4">Daftar Buku</h2>
            <div id="bookList">
                <!-- Contoh item buku -->
                <div class="book-item">
                    <h3 class="text-lg font-semibold">Judul Buku</h3>
                    <p class="text-gray-600">Penulis: Nama Penulis</p>
                    <p class="text-gray-600">Tahun Terbit: 2023</p>
                    <p class="text-gray-600">Kategori: Fiksi</p>
                </div>
                <!-- Item buku akan ditambahkan di sini -->
            </div>
        </div>
    </div>

    <!-- Footer -->
    <footer class="bg-gray-800 text-white text-center py-4 mt-8">
        <p>&copy; 2023 Aplikasi Pencatatan Buku</p>
    </footer>

    <!-- JavaScript -->
    <script>
        document.getElementById('bookForm').addEventListener('submit', function(e) {
            e.preventDefault();

            const judul = document.getElementById('judul').value;
            const penulis = document.getElementById('penulis').value;
            const tahun = document.getElementById('tahun').value;
            const kategori = document.getElementById('kategori').value;

            // Buat elemen HTML untuk item buku
            const bookItem = document.createElement('div');
            bookItem.classList.add('book-item');
            bookItem.innerHTML = `
                <h3 class="text-lg font-semibold">${judul}</h3>
                <p class="text-gray-600">Penulis: ${penulis}</p>
                <p class="text-gray-600">Tahun Terbit: ${tahun}</p>
                <p class="text-gray-600">Kategori: ${kategori}</p>
            `;

            // Tambahkan item buku ke daftar
            document.getElementById('bookList').appendChild(bookItem);

            // Reset form
            document.getElementById('bookForm').reset();
        });
    </script>
</body>
</html>
