<!doctype html>

<html lang="id">
<head>
  <meta charset="utf-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1" />
  <title>Pencatatan Buku — Satu File</title>
  <style>
    :root{
      --bg:#0f172a; /* slate-900 */
      --panel:#111827; /* gray-900 */
      --muted:#94a3b8; /* slate-400 */
      --text:#e5e7eb; /* gray-200 */
      --accent:#22c55e; /* green-500 */
      --accent-2:#38bdf8; /* sky-400 */
      --danger:#ef4444; /* red-500 */
      --warning:#f59e0b; /* amber-500 */
      --shadow:0 10px 30px rgba(0,0,0,.35)
    }
    *{box-sizing:border-box}
    html,body{height:100%}
    body{margin:0;background:radial-gradient(1200px 800px at 80% -10%,rgba(56,189,248,.17),transparent 60%),radial-gradient(1200px 800px at -20% 110%,rgba(34,197,94,.16),transparent 60%),var(--bg);color:var(--text);font:500 15px/1.6 system-ui, -apple-system, Segoe UI, Roboto, Helvetica, Arial}
    a{color:var(--accent-2);text-decoration:none}
    .container{max-width:1100px;margin:auto;padding:24px}
    .app-title{display:flex;align-items:center;gap:12px}
    .logo{width:36px;height:36px;border-radius:12px;background:linear-gradient(135deg,var(--accent),var(--accent-2));box-shadow:var(--shadow)}
    .card{background:linear-gradient(180deg,rgba(255,255,255,.06),rgba(255,255,255,.04));border:1px solid rgba(255,255,255,.08);backdrop-filter:blur(6px);border-radius:18px;box-shadow:var(--shadow)}
    .panel{padding:18px}
    .grid{display:grid;gap:16px}
    .grid-2{grid-template-columns:repeat(2,minmax(0,1fr))}
    @media (max-width:820px){.grid-2{grid-template-columns:1fr}}
    .muted{color:var(--muted)}
    .btn{appearance:none;border:0;border-radius:12px;padding:10px 14px;font-weight:700;cursor:pointer;background:#1f2937;color:#e5e7eb;transition:.18s transform,.18s background}
    .btn:hover{transform:translateY(-1px)}
    .btn:active{transform:translateY(0)}
    .btn.primary{background:linear-gradient(135deg,var(--accent),#16a34a)}
    .btn.info{background:linear-gradient(135deg,#06b6d4,var(--accent-2))}
    .btn.warn{background:linear-gradient(135deg,var(--warning),#d97706)}
    .btn.danger{background:linear-gradient(135deg,var(--danger),#b91c1c)}
    .btn.ghost{background:transparent;border:1px solid rgba(255,255,255,.14)}
    .btn.small{padding:8px 10px;border-radius:10px;font-weight:600}
    .input, select, textarea{width:100%;padding:12px 12px;border-radius:12px;background:#0b1220;border:1px solid rgba(255,255,255,.12);color:var(--text);outline:none}
    .input:focus, select:focus, textarea:focus{border-color:var(--accent-2);box-shadow:0 0 0 3px rgba(56,189,248,.2)}
    .row{display:flex;gap:10px;flex-wrap:wrap}
    .row .btn{flex:1}
    .tag{display:inline-flex;align-items:center;gap:6px;background:rgba(56,189,248,.15);border:1px solid rgba(56,189,248,.35);color:#cffafe;padding:6px 10px;border-radius:999px;font-size:12px}
    .hidden{display:none !important}
    /* table */
    table{width:100%;border-collapse:collapse}
    th,td{padding:12px 10px;border-bottom:1px dashed rgba(255,255,255,.08)}
    th{font-size:13px;text-transform:uppercase;letter-spacing:.08em;color:#cbd5e1;text-align:left}
    tbody tr:hover{background:rgba(255,255,255,.03)}
    .actions{display:flex;gap:6px}
    /* toast */
    #toast{position:fixed;inset:auto 16px 16px auto;background:#0b1220;border:1px solid rgba(255,255,255,.15);padding:10px 14px;border-radius:12px;box-shadow:var(--shadow);opacity:0;transform:translateY(8px);transition:.2s}
    #toast.show{opacity:1;transform:translateY(0)}
  </style>
</head>
<body>
  <div class="container">
    <div class="app-title">
      <div class="logo"></div>
      <div>
        <h1 style="margin:0">Pencatatan Buku</h1>
        <div class="muted">Aplikasi web satu file — cocok untuk Acode (Android)</div>
      </div>
    </div><!-- AUTH CARD -->
<section id="auth" class="card panel" aria-label="Autentikasi">
  <div class="grid grid-2">
    <div>
      <h2 style="margin-top:0">Masuk</h2>
      <div class="grid">
        <input id="login-email" class="input" type="email" placeholder="Email" autocomplete="username" />
        <input id="login-pass" class="input" type="password" placeholder="Kata sandi" autocomplete="current-password" />
        <button class="btn primary" onclick="login()">Masuk</button>
      </div>
      <p class="muted" style="margin-top:10px;font-size:13px">Tip: bila belum punya akun, daftar di kanan.
      </p>
    </div>
    <div>
      <h2 style="margin-top:0">Daftar</h2>
      <div class="grid">
        <input id="reg-name" class="input" placeholder="Nama" />
        <input id="reg-email" class="input" type="email" placeholder="Email" />
        <input id="reg-pass" class="input" type="password" placeholder="Kata sandi" />
        <button class="btn info" onclick="register()">Buat Akun</button>
      </div>
      <p class="muted" style="margin-top:10px;font-size:13px">Data disimpan lokal di perangkat Anda (localStorage).</p>
    </div>
  </div>
</section>

<!-- APP CARD -->
<section id="app" class="card panel hidden" aria-label="Aplikasi">
  <header class="row" style="align-items:center;justify-content:space-between;gap:12px">
    <div class="row" style="gap:10px;align-items:center">
      <span class="tag" id="userTag">Pengguna: -</span>
      <button class="btn ghost small" onclick="logout()">Keluar</button>
    </div>
    <div class="row" style="gap:8px">
      <button class="btn small info" onclick="exportCSV()">Ekspor CSV</button>
      <label class="btn small ghost" style="cursor:pointer">
        Impor CSV
        <input id="importFile" type="file" accept=".csv" style="display:none" onchange="importCSV(event)" />
      </label>
      <button class="btn small warn" onclick="clearAllBooks()">Hapus Semua</button>
    </div>
  </header>

  <!-- FORM -->
  <div class="grid grid-2" style="margin-top:16px">
    <div class="card panel">
      <h3 style="margin-top:0" id="formTitle">Tambah Buku</h3>
      <div class="grid">
        <input class="input" id="f-judul" placeholder="Judul" />
        <input class="input" id="f-penulis" placeholder="Penulis" />
        <div class="grid" style="grid-template-columns:1fr 1fr;gap:10px">
          <input class="input" id="f-tahun" placeholder="Tahun Terbit" inputmode="numeric" />
          <input class="input" id="f-isbn" placeholder="ISBN (opsional)" />
        </div>
        <input class="input" id="f-kategori" placeholder="Kategori/Genre" />
        <div class="row">
          <button class="btn primary" id="btnSubmit" onclick="submitBook()">Simpan</button>
          <button class="btn ghost" id="btnCancel" onclick="resetForm()" style="display:none">Batal</button>
        </div>
      </div>
    </div>

    <div class="card panel">
      <h3 style="margin-top:0">Pencarian & Filter</h3>
      <div class="grid">
        <input class="input" id="q" placeholder="Cari judul/penulis/kategori" oninput="renderBooks()" />
        <div class="grid" style="grid-template-columns:1fr 1fr;gap:10px">
          <select id="filterKategori" onchange="renderBooks()">
            <option value="">Semua Kategori</option>
          </select>
          <select id="sortBy" onchange="renderBooks()">
            <option value="createdAt_desc">Terbaru</option>
            <option value="createdAt_asc">Terlama</option>
            <option value="judul_asc">Judul A→Z</option>
            <option value="judul_desc">Judul Z→A</option>
          </select>
        </div>
      </div>
    </div>
  </div>

  <!-- TABLE -->
  <div class="card panel" style="margin-top:16px">
    <div class="row" style="justify-content:space-between;align-items:center">
      <h3 style="margin:0">Daftar Buku</h3>
      <div class="muted" id="countLabel">0 buku</div>
    </div>
    <div style="overflow:auto;margin-top:8px">
      <table>
        <thead>
          <tr>
            <th>#</th>
            <th>Judul</th>
            <th>Penulis</th>
            <th>Tahun</th>
            <th>Kategori</th>
            <th>ISBN</th>
            <th style="text-align:right">Aksi</th>
          </tr>
        </thead>
        <tbody id="rows"></tbody>
      </table>
    </div>
  </div>
</section>

  </div>  <div id="toast" role="status" aria-live="polite"></div>  <script>
    // ------------------------------
    // UTIL
    // ------------------------------
    const $ = sel => document.querySelector(sel)
    const $$ = sel => [...document.querySelectorAll(sel)]
    const toast = (msg) => { const el = $('#toast'); el.textContent = msg; el.classList.add('show'); setTimeout(()=>el.classList.remove('show'), 2000) }
    const now = () => new Date().toISOString()

    // ------------------------------
    // AUTH + STORAGE (localStorage)
    // ------------------------------
    const LS_USERS = 'acode_users_v1'
    const LS_SESSION = 'acode_session_v1'

    function getUsers(){
      try{ return JSON.parse(localStorage.getItem(LS_USERS))||[] }catch{ return [] }
    }
    function saveUsers(list){ localStorage.setItem(LS_USERS, JSON.stringify(list)) }

    function currentUser(){
      try{ return JSON.parse(localStorage.getItem(LS_SESSION)) }catch{ return null }
    }
    function setSession(user){ localStorage.setItem(LS_SESSION, JSON.stringify(user)) }
    function clearSession(){ localStorage.removeItem(LS_SESSION) }

    function userBooksKey(email){ return `books_${email}` }
    function loadBooks(){
      const u = currentUser(); if(!u) return []
      try{ return JSON.parse(localStorage.getItem(userBooksKey(u.email)))||[] }catch{ return [] }
    }
    function saveBooks(arr){
      const u = currentUser(); if(!u) return
      localStorage.setItem(userBooksKey(u.email), JSON.stringify(arr))
    }

    // ------------------------------
    // AUTH HANDLERS
    // ------------------------------
    function register(){
      const name = $('#reg-name').value.trim()
      const email = $('#reg-email').value.trim().toLowerCase()
      const pass = $('#reg-pass').value
      if(!name || !email || !pass){ toast('Isi semua kolom pendaftaran'); return }
      const users = getUsers()
      if(users.some(u=>u.email===email)){ toast('Email sudah terdaftar'); return }
      users.push({name,email,pass,createdAt:now()})
      saveUsers(users)
      toast('Akun dibuat. Silakan masuk.')
      $('#login-email').value=email; $('#login-pass').value=pass
    }

    function login(){
      const email = $('#login-email').value.trim().toLowerCase()
      const pass = $('#login-pass').value
      const u = getUsers().find(u=>u.email===email && u.pass===pass)
      if(!u){ toast('Email atau sandi salah'); return }
      setSession({name:u.name,email:u.email})
      $('#userTag').textContent = `Pengguna: ${u.name}`
      $('#auth').classList.add('hidden')
      $('#app').classList.remove('hidden')
      hydrateUI()
      toast('Berhasil masuk')
    }

    function logout(){ clearSession(); $('#app').classList.add('hidden'); $('#auth').classList.remove('hidden'); toast('Keluar') }

    // ------------------------------
    // BOOKS CRUD
    // ------------------------------
    let editId = null

    function hydrateUI(){
      // isi filter kategori dari data
      const books = loadBooks()
      const cats = [...new Set(books.map(b=>b.kategori).filter(Boolean))].sort()
      const sel = $('#filterKategori')
      sel.innerHTML = '<option value="">Semua Kategori</option>' + cats.map(c=>`<option>${escapeHtml(c)}</option>`).join('')
      renderBooks()
    }

    function submitBook(){
      const judul = $('#f-judul').value.trim()
      const penulis = $('#f-penulis').value.trim()
      const tahun = $('#f-tahun').value.trim()
      const kategori = $('#f-kategori').value.trim()
      const isbn = $('#f-isbn').value.trim()

      if(!judul || !penulis){ toast('Judul & Penulis wajib'); return }
      if(tahun && !/^\d{3,4}$/.test(tahun)){ toast('Tahun tidak valid'); return }

      const books = loadBooks()
      if(editId){
        const idx = books.findIndex(b=>b.id===editId)
        if(idx>=0){ books[idx] = {...books[idx], judul, penulis, tahun, kategori, isbn, updatedAt:now()} }
        saveBooks(books)
        toast('Buku diperbarui')
      } else {
        const id = cryptoRandomId()
        books.unshift({ id, judul, penulis, tahun, kategori, isbn, createdAt:now() })
        saveBooks(books)
        toast('Buku ditambahkan')
      }
      resetForm(); hydrateUI()
    }

    function startEdit(id){
      const b = loadBooks().find(x=>x.id===id); if(!b) return
      editId = id
      $('#formTitle').textContent = 'Edit Buku'
      $('#btnSubmit').textContent = 'Simpan Perubahan'
      $('#btnCancel').style.display = 'inline-block'
      $('#f-judul').value=b.judul; $('#f-penulis').value=b.penulis; $('#f-tahun').value=b.tahun||''; $('#f-kategori').value=b.kategori||''; $('#f-isbn').value=b.isbn||''
      window.scrollTo({top:0,behavior:'smooth'})
    }

    function resetForm(){
      editId = null
      $('#formTitle').textContent = 'Tambah Buku'
      $('#btnSubmit').textContent = 'Simpan'
      $('#btnCancel').style.display = 'none'
      ;['#f-judul','#f-penulis','#f-tahun','#f-kategori','#f-isbn'].forEach(s=>$(s).value='')
    }

    function delBook(id){
      if(!confirm('Hapus buku ini?')) return
      const next = loadBooks().filter(b=>b.id!==id)
      saveBooks(next); hydrateUI(); toast('Buku dihapus')
    }

    function clearAllBooks(){
      if(!confirm('Hapus SEMUA buku?')) return
      saveBooks([]); hydrateUI(); toast('Semua data dihapus')
    }

    function renderBooks(){
      const q = $('#q').value.trim().toLowerCase()
      const cat = $('#filterKategori').value
      const sortBy = $('#sortBy').value
      let books = loadBooks()
      if(q){
        books = books.filter(b => [b.judul,b.penulis,b.kategori,b.isbn].join('|').toLowerCase().includes(q))
      }
      if(cat){ books = books.filter(b=> (b.kategori||'') === cat) }

      books.sort((a,b)=>{
        switch(sortBy){
          case 'createdAt_asc': return (a.createdAt||'').localeCompare(b.createdAt||'')
          case 'judul_asc': return (a.judul||'').localeCompare(b.judul||'')
          case 'judul_desc': return (b.judul||'').localeCompare(a.judul||'')
          default: return (b.createdAt||'').localeCompare(a.createdAt||'')
        }
      })

      const rows = books.map((b,i)=>`
        <tr>
          <td>${i+1}</td>
          <td>${escapeHtml(b.judul||'')}</td>
          <td>${escapeHtml(b.penulis||'')}</td>
          <td>${escapeHtml(b.tahun||'')}</td>
          <td>${escapeHtml(b.kategori||'')}</td>
          <td>${escapeHtml(b.isbn||'')}</td>
          <td style="text-align:right">
            <div class="actions">
              <button class="btn small ghost" title="Edit" onclick="startEdit('${b.id}')">Edit</button>
              <button class="btn small danger" title="Hapus" onclick="delBook('${b.id}')">Hapus</button>
            </div>
          </td>
        </tr>
      `).join('')

      $('#rows').innerHTML = rows || `<tr><td colspan="7" class="muted">Belum ada data</td></tr>`
      $('#countLabel').textContent = `${books.length} buku`
    }

    // ------------------------------
    // CSV IMPORT/EXPORT
    // ------------------------------
    function exportCSV(){
      const books = loadBooks()
      if(!books.length){ toast('Tidak ada data untuk diekspor'); return }
      const header = ['judul','penulis','tahun','kategori','isbn','createdAt']
      const lines = [header.join(',')]
      for(const b of books){
        const row = [b.judul,b.penulis,b.tahun,b.kategori,b.isbn,b.createdAt].map(csvCell).join(',')
        lines.push(row)
      }
      const blob = new Blob(["\ufeff"+lines.join('\n')],{type:'text/csv;charset=utf-8'})
      const a = document.createElement('a')
      a.href = URL.createObjectURL(blob)
      a.download = `buku_${(currentUser()?.email||'user').replace(/[^a-z0-9]/gi,'_')}.csv`
      document.body.appendChild(a); a.click(); a.remove()
      toast('CSV diekspor')
    }

    function importCSV(evt){
      const file = evt.target.files?.[0]; if(!file) return
      const reader = new FileReader()
      reader.onload = () => {
        const text = reader.result.toString()
        const rows = text.split(/\r?\n/).filter(Boolean)
        const header = rows.shift().split(',').map(h=>h.trim().toLowerCase())
        const idx = (name) => header.indexOf(name)
        const list = rows.map(line=>{
          const cells = parseCsvLine(line)
          return {
            id: cryptoRandomId(),
            judul: cells[idx('judul')]||'',
            penulis: cells[idx('penulis')]||'',
            tahun: cells[idx('tahun')]||'',
            kategori: cells[idx('kategori')]||'',
            isbn: cells[idx('isbn')]||'',
            createdAt: cells[idx('createdat')]||now()
          }
        }).filter(x=>x.judul && x.penulis)
        const before = loadBooks()
        saveBooks([...list, ...before])
        hydrateUI(); toast(`Impor selesai: ${list.length} buku ditambahkan`)
        evt.target.value = ''
      }
      reader.readAsText(file)
    }

    function csvCell(v){
      if(v==null) v=''
      const s = String(v).replaceAll('"','""')
      return /[",\n]/.test(s) ? `"${s}"` : s
    }
    function parseCsvLine(line){
      // simple CSV parser for a single line
      const out=[]; let cur=''; let q=false
      for(let i=0;i<line.length;i++){
        const ch=line[i]
        if(q){
          if(ch==='"' && line[i+1]==='"'){ cur+='"'; i++ }
          else if(ch==='"'){ q=false }
          else cur+=ch
        } else {
          if(ch==='"'){ q=true }
          else if(ch===','){ out.push(cur); cur='' }
          else cur+=ch
        }
      }
      out.push(cur); return out.map(s=>s.trim())
    }

    // ------------------------------
    // HELPERS
    // ------------------------------
    function cryptoRandomId(){
      // 16 bytes -> 32 hex
      if(window.crypto?.getRandomValues){
        const a = new Uint8Array(16); crypto.getRandomValues(a)
        return [...a].map(x=>x.toString(16).padStart(2,'0')).join('')
      }
      return 'id-' + Math.random().toString(36).slice(2,10)
    }
    function escapeHtml(s){ return String(s).replace(/[&<>"']/g, m=>({"&":"&amp;","<":"&lt;",">":"&gt;","\"":"&quot;","'":"&#39;"}[m])) }

    // ------------------------------
    // INIT (auto-login jika ada sesi)
    // ------------------------------
    (function init(){
      const u = currentUser()
      if(u){
        $('#userTag').textContent = `Pengguna: ${u.name}`
        $('#auth').classList.add('hidden')
        $('#app').classList.remove('hidden')
        hydrateUI()
      }
    })()
  </script></body>
</html>
