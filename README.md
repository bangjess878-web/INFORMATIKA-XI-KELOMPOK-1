<!doctype html>
<html lang="id">
<head>
  <meta charset="utf-8" />
  <meta name="viewport" content="width=device-width,initial-scale=1" />
  <title>Sulitnya Pencatatan Buku Secara Manual — Demo HTML</title>
  <style>
    :root{--bg:#f6f7fb;--card:#ffffff;--accent:#2563eb;--muted:#6b7280}
    *{box-sizing:border-box}
    body{font-family:Inter,Segoe UI,Roboto,Helvetica,Arial,sans-serif;background:var(--bg);color:#111;margin:0;padding:24px}
    header{display:flex;align-items:center;gap:16px;margin-bottom:18px}
    .logo{width:56px;height:56px;border-radius:10px;background:linear-gradient(135deg,var(--accent),#60a5fa);display:flex;align-items:center;justify-content:center;color:#fff;font-weight:700}
    h1{margin:0;font-size:20px}
    p.lead{margin:6px 0 18px;color:var(--muted)}
    .container{display:grid;grid-template-columns:1fr 420px;gap:18px}
    .card{background:var(--card);border-radius:12px;padding:18px;box-shadow:0 6px 18px rgba(10,12,20,0.06)}
    .small{font-size:13px;color:var(--muted)}
    ul{margin:8px 0 0 18px}
    .highlight{color:var(--accent);font-weight:600}
    /* form */
    label{display:block;font-size:13px;margin-bottom:6px}
    input,select,textarea{width:100%;padding:10px;border-radius:8px;border:1px solid #e6e9ef;font-size:14px}
    button{background:var(--accent);color:white;padding:10px 12px;border-radius:8px;border:0;font-weight:600;cursor:pointer}
    button.ghost{background:transparent;color:var(--accent);border:1px solid rgba(37,99,235,0.12)}
    .table-wrap{overflow:auto;margin-top:12px}
    table{width:100%;border-collapse:collapse}
    th,td{padding:10px;border-bottom:1px solid #f1f3f7;text-align:left;font-size:14px}
    th{background:#fbfdff;font-weight:700;position:sticky;top:0}
    .actions{display:flex;gap:8px}
    .tag{display:inline-block;padding:6px 8px;border-radius:999px;background:#eef2ff;color:var(--accent);font-weight:600;font-size:12px}
    footer{margin-top:18px;text-align:center;color:var(--muted);font-size:13px}
    /* responsive */
    @media (max-width:920px){.container{grid-template-columns:1fr;}}
  </style>
</head>
<body>
  <header>
    <div class="logo">BK</div>
    <div>
      <h1>Sulitnya Pencatatan Buku secara Manual</h1>
      <p class="lead">Halaman demo ini menjelaskan penyebab, dampak, dan contoh solusi sederhana berbasis web untuk memperbaiki pencatatan buku yang masih manual.</p>
    </div>
  </header>

  <div class="container">
    <main class="card">
      <section>
        <h2>Masalah Utama</h2>
        <p class="small">Pencatatan buku secara manual (buku register, catatan tangan) masih umum di perpustakaan kecil, toko buku, dan sekolah. Berikut beberapa masalah yang sering muncul:</p>
        <ul>
          <li>Kesalahan penulisan & kehilangan data akibat tulisan tangan kurang rapi atau terhapus.</li>
          <li>Duplikasi entri dan sulitnya melacak status peminjaman.</li>
          <li>Waktu pencarian catatan lama yang memakan waktu.</li>
          <li>Risiko fisik: catatan rusak, hilang atau terbakar.</li>
          <li>Sulit membuat laporan statistik (koleksi populer, frekuensi peminjaman, dsb.).</li>
        </ul>
      </section>

      <section style="margin-top:14px">
        <h2>Penyebab</h2>
        <ul>
          <li>Keterbatasan sumber daya (tidak ada komputer atau staf terlatih).</li>
          <li>Kurangnya standar pencatatan dan pelatihan.</li>
          <li>Kebiasaan lama dan resistensi terhadap perubahan.</li>
        </ul>
      </section>

      <section style="margin-top:14px">
        <h2>Dampak</h2>
        <ul>
          <li>Pelayanan menjadi lambat dan kurang profesional.</li>
          <li>Pengambilan keputusan berbasis data menjadi sulit.</li>
          <li>Risiko kehilangan aset (buku) lebih besar.</li>
        </ul>
      </section>

      <section style="margin-top:14px">
        <h2>Pendekatan Pemikiran Komputasional (singkat)</h2>
        <ol>
          <li><strong>Decomposition:</strong> Pisahkan proses menjadi: input data buku, pencarian, peminjaman, pengembalian, dan laporan.</li>
          <li><strong>Pattern recognition:</strong> Identifikasi data yang selalu sama (judul, pengarang, ISBN, status).</li>
          <li><strong>Abstraction:</strong> Fokus pada informasi penting dan singkirkan catatan berlebih yang tidak diperlukan.</li>
          <li><strong>Algorithm design:</strong> Buat langkah untuk tiap operasi (mis. algoritma cari -> filter -> tampilkan hasil).</li>
        </ol>
      </section>

      <section style="margin-top:14px">
        <h2>Contoh Solusi Sederhana (Web lokal)</h2>
        <p class="small">Di bagian samping terdapat demo formulir & tabel untuk mencatat buku. Sistem ini menyimpan data ke <em>localStorage</em> browser sehingga tidak perlu server — cocok sebagai proof-of-concept atau prototype.</p>

        <div class="table-wrap" aria-live="polite">
          <table id="booksTable" aria-describedby="booksDesc">
            <thead>
              <tr><th>#</th><th>Judul</th><th>Pengarang</th><th>Kode/ISBN</th><th>Status</th><th>Aksi</th></tr>
            </thead>
            <tbody></tbody>
          </table>
        </div>

        <p id="booksDesc" class="small">Tabel di atas menyimpan catatan buku yang ditambahkan. Gunakan tombol "Export CSV" untuk mengambil data atau "Print" untuk mencetak.</p>
      </section>

    </main>

    <aside class="card">
      <h3>Tambah Buku</h3>
      <form id="bookForm">
        <label for="title">Judul</label>
        <input id="title" name="title" required placeholder="Contoh: Matematika Dasar" />

        <label for="author" style="margin-top:8px">Pengarang</label>
        <input id="author" name="author" required placeholder="Nama pengarang" />

        <label for="code" style="margin-top:8px">Kode / ISBN</label>
        <input id="code" name="code" placeholder="Opsional: ISBN atau kode buku" />

        <label for="status" style="margin-top:8px">Status</label>
        <select id="status" name="status">
          <option value="Tersedia">Tersedia</option>
          <option value="Dipinjam">Dipinjam</option>
        </select>

        <div style="display:flex;gap:8px;margin-top:12px">
          <button type="submit">Tambah</button>
          <button type="button" class="ghost" id="clearAll">Hapus Semua</button>
        </div>

        <div style="margin-top:12px;display:flex;gap:8px">
          <button type="button" id="exportCsv" class="ghost">Export CSV</button>
          <button type="button" id="print" class="ghost">Print</button>
        </div>

        <p class="small" style="margin-top:12px">Data disimpan di <em>localStorage</em> browser. Untuk penggunaan nyata, hubungkan ke server / database.</p>
      </form>

      <hr style="margin:14px 0;border:none;border-top:1px solid #f1f3f7" />

      <div>
        <h4>Tips Implementasi</h4>
        <ul>
          <li>Backup data secara rutin (ekspor CSV)</li>
          <li>Standarisasi format kode/ISBN</li>
          <li>Berikan pelatihan singkat untuk petugas</li>
        </ul>
      </div>

      <footer>
        <small>Demo dibuat untuk ilustrasi masalah dan solusi sederhana.</small>
      </footer>
    </aside>
  </div>

  <script>
    // Simple book manager using localStorage
    const LS_KEY = 'demo_books_manual';
    const form = document.getElementById('bookForm');
    const tableBody = document.querySelector('#booksTable tbody');
    const exportBtn = document.getElementById('exportCsv');
    const printBtn = document.getElementById('print');
    const clearBtn = document.getElementById('clearAll');

    function loadBooks(){
      try{
        const raw = localStorage.getItem(LS_KEY);
        return raw? JSON.parse(raw): [];
      } catch(e){return []}
    }
    function saveBooks(list){
      localStorage.setItem(LS_KEY, JSON.stringify(list));
    }
    function render(){
      const books = loadBooks();
      tableBody.innerHTML = '';
      books.forEach((b,i)=>{
        const tr = document.createElement('tr');
        tr.innerHTML = `<td>${i+1}</td>
          <td>${escapeHtml(b.title)}</td>
          <td>${escapeHtml(b.author)}</td>
          <td>${escapeHtml(b.code||'—')}</td>
          <td><span class="tag">${b.status}</span></td>
          <td class="actions"><button data-index="${i}" class="edit">Edit</button><button data-index="${i}" class="del">Hapus</button></td>`;
        tableBody.appendChild(tr);
      });
      attachRowHandlers();
    }
    function escapeHtml(s){return String(s).replace(/&/g,'&amp;').replace(/</g,'&lt;').replace(/>/g,'&gt;')}

    form.addEventListener('submit', e=>{
      e.preventDefault();
      const title = form.title.value.trim();
      const author = form.author.value.trim();
      const code = form.code.value.trim();
      const status = form.status.value;
      if(!title || !author) return alert('Judul dan pengarang wajib diisi');
      const books = loadBooks();
      books.push({title,author,code,status,created: new Date().toISOString()});
      saveBooks(books);
      form.reset();
      render();
    });

    function attachRowHandlers(){
      document.querySelectorAll('.del').forEach(btn=>btn.onclick = ()=>{
        const idx = Number(btn.dataset.index);
        if(!confirm('Hapus entri ini?')) return;
        const books = loadBooks();
        books.splice(idx,1);
        saveBooks(books);
        render();
      });
      document.querySelectorAll('.edit').forEach(btn=>btn.onclick = ()=>{
        const idx = Number(btn.dataset.index);
        const books = loadBooks();
        const b = books[idx];
        const newTitle = prompt('Edit judul', b.title);
        if(newTitle === null) return;
        const newAuthor = prompt('Edit pengarang', b.author);
        if(newAuthor === null) return;
        b.title = newTitle.trim() || b.title;
        b.author = newAuthor.trim() || b.author;
        saveBooks(books);
        render();
      });
    }

    exportBtn.addEventListener('click', ()=>{
      const books = loadBooks();
      if(!books.length) return alert('Tidak ada data untuk diekspor');
      const rows = [ ['No','Judul','Pengarang','Kode','Status','Tanggal membuat'] ];
      books.forEach((b,i)=> rows.push([i+1,b.title,b.author,b.code||'',b.status,b.created||'']));
      const csv = rows.map(r=> r.map(c => `"${String(c).replace(/"/g,'""')}"`).join(',')).join('\n');
      const blob = new Blob([csv],{type:'text/csv'});
      const url = URL.createObjectURL(blob);
      const a = document.createElement('a');
      a.href = url; a.download = 'books_export.csv'; a.click();
      URL.revokeObjectURL(url);
    });

    printBtn.addEventListener('click', ()=>{
      window.print();
    });

    clearBtn.addEventListener('click', ()=>{
      if(!confirm('Hapus semua data? Tindakan ini tidak dapat dibatalkan.')) return;
      localStorage.removeItem(LS_KEY);
      render();
    });

    // initial demo data if empty
    (function initDemo(){
      const books = loadBooks();
      if(books.length===0){
        const sample = [
          {title:'Biologi SMA Kelas X',author:'I. Santoso',code:'B-001',status:'Tersedia',created:new Date().toISOString()},
          {title:'Ilmu Pengetahuan Alam',author:'R. Wibowo',code:'B-002',status:'Dipinjam',created:new Date().toISOString()}
        ];
        saveBooks(sample);
      }
      render();
    })();
  </script>
</body>
</html>


