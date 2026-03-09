<!DOCTYPE html>
<html lang="id">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>CBT TKA Matematika SMP</title>
<link href="https://fonts.googleapis.com/css2?family=Plus+Jakarta+Sans:wght@400;500;600;700;800&family=JetBrains+Mono:wght@400;600&display=swap" rel="stylesheet">
<style>
  :root {
    --navy: #0d1b3e;
    --navy2: #162552;
    --blue: #2563eb;
    --blue-light: #3b82f6;
    --accent: #f59e0b;
    --accent2: #fbbf24;
    --green: #10b981;
    --red: #ef4444;
    --bg: #f0f4ff;
    --card: #ffffff;
    --text: #1e293b;
    --muted: #64748b;
    --border: #e2e8f0;
    --correct: #dcfce7;
    --wrong: #fee2e2;
    --radius: 14px;
  }

  * { box-sizing: border-box; margin: 0; padding: 0; }

  body {
    font-family: 'Plus Jakarta Sans', sans-serif;
    background: var(--bg);
    color: var(--text);
    min-height: 100vh;
  }

  /* ── HEADER ── */
  .header {
    background: linear-gradient(135deg, var(--navy) 0%, var(--navy2) 60%, #1e3a8a 100%);
    color: white;
    padding: 0;
    position: sticky;
    top: 0;
    z-index: 100;
    box-shadow: 0 4px 20px rgba(13,27,62,.4);
  }
  .header-inner {
    max-width: 900px;
    margin: 0 auto;
    padding: 14px 20px;
    display: flex;
    align-items: center;
    gap: 16px;
    flex-wrap: wrap;
  }
  .header-badge {
    background: var(--accent);
    color: var(--navy);
    font-weight: 800;
    font-size: 11px;
    padding: 3px 10px;
    border-radius: 20px;
    letter-spacing: .5px;
    text-transform: uppercase;
  }
  .header h1 {
    font-size: 16px;
    font-weight: 700;
    flex: 1;
  }
  .header h1 span { color: var(--accent2); }
  #timer {
    font-family: 'JetBrains Mono', monospace;
    font-size: 18px;
    font-weight: 600;
    background: rgba(255,255,255,.12);
    padding: 6px 14px;
    border-radius: 8px;
    color: #fff;
    letter-spacing: 1px;
    border: 1px solid rgba(255,255,255,.2);
    transition: background .3s;
  }
  #timer.urgent { background: rgba(239,68,68,.4); animation: pulse .8s infinite; }
  @keyframes pulse { 0%,100%{opacity:1} 50%{opacity:.7} }

  /* ── PROGRESS BAR ── */
  .progress-wrap {
    background: var(--navy);
    padding: 0 20px 10px;
  }
  .progress-inner { max-width: 900px; margin: 0 auto; }
  .progress-info { display:flex; justify-content:space-between; font-size:11px; color:rgba(255,255,255,.6); margin-bottom:5px; }
  .progress-bar {
    height: 5px;
    background: rgba(255,255,255,.15);
    border-radius: 99px;
    overflow: hidden;
  }
  .progress-fill {
    height: 100%;
    background: linear-gradient(90deg, var(--accent), var(--accent2));
    border-radius: 99px;
    transition: width .4s ease;
  }

  /* ── MAIN ── */
  .main { max-width: 900px; margin: 0 auto; padding: 24px 16px; }

  /* ── SOAL NAVIGATOR ── */
  .nav-grid {
    display: grid;
    grid-template-columns: repeat(auto-fill, minmax(38px, 1fr));
    gap: 6px;
    background: var(--card);
    border-radius: var(--radius);
    padding: 16px;
    margin-bottom: 20px;
    box-shadow: 0 2px 12px rgba(0,0,0,.06);
  }
  .nav-btn {
    aspect-ratio: 1;
    border: 2px solid var(--border);
    background: white;
    border-radius: 8px;
    font-size: 12px;
    font-weight: 700;
    cursor: pointer;
    font-family: inherit;
    transition: all .18s;
    color: var(--muted);
    display:flex; align-items:center; justify-content:center;
  }
  .nav-btn:hover { border-color: var(--blue-light); color: var(--blue); }
  .nav-btn.answered { background: var(--navy); border-color: var(--navy); color: white; }
  .nav-btn.active { background: var(--blue); border-color: var(--blue); color: white; transform: scale(1.12); }
  .nav-btn.pgk { border-style: dashed; }
  .nav-btn.bs-type { border-radius: 50%; }

  .legend { display:flex; gap:12px; margin-top:10px; flex-wrap:wrap; }
  .legend-item { display:flex; align-items:center; gap:5px; font-size:11px; color:var(--muted); }
  .legend-dot { width:12px; height:12px; border-radius:3px; border:2px solid; }

  /* ── CARD SOAL ── */
  .soal-card {
    background: var(--card);
    border-radius: var(--radius);
    padding: 28px;
    box-shadow: 0 2px 16px rgba(0,0,0,.07);
    margin-bottom: 20px;
    animation: fadeIn .25s ease;
  }
  @keyframes fadeIn { from{opacity:0;transform:translateY(8px)} to{opacity:1;transform:translateY(0)} }

  .soal-meta {
    display: flex;
    align-items: center;
    gap: 10px;
    margin-bottom: 18px;
    flex-wrap: wrap;
  }
  .soal-num {
    background: var(--navy);
    color: white;
    font-size: 13px;
    font-weight: 800;
    padding: 4px 14px;
    border-radius: 8px;
  }
  .tipe-badge {
    font-size: 11px;
    font-weight: 700;
    padding: 3px 10px;
    border-radius: 20px;
    text-transform: uppercase;
    letter-spacing: .4px;
  }
  .tipe-pg   { background:#dbeafe; color:#1d4ed8; }
  .tipe-pgk  { background:#fef3c7; color:#b45309; }
  .tipe-bs   { background:#d1fae5; color:#065f46; }

  .konteks-box {
    background: #f8faff;
    border-left: 4px solid var(--blue);
    border-radius: 0 10px 10px 0;
    padding: 14px 16px;
    font-size: 14px;
    line-height: 1.7;
    margin-bottom: 16px;
    color: var(--text);
    white-space: pre-line;
  }
  .instruksi {
    font-size: 12.5px;
    color: #dc2626;
    font-weight: 600;
    font-style: italic;
    margin-bottom: 12px;
    padding: 6px 12px;
    background: #fff1f2;
    border-radius: 6px;
    border: 1px solid #fecdd3;
  }
  .pertanyaan {
    font-size: 15px;
    font-weight: 600;
    color: var(--text);
    margin-bottom: 16px;
    line-height: 1.6;
  }

  /* ── OPTIONS ── */
  .options { display:flex; flex-direction:column; gap:10px; }

  .option-btn {
    display: flex;
    align-items: flex-start;
    gap: 12px;
    padding: 12px 16px;
    border: 2px solid var(--border);
    border-radius: 10px;
    background: white;
    cursor: pointer;
    font-family: inherit;
    font-size: 14px;
    text-align: left;
    transition: all .18s;
    color: var(--text);
    line-height: 1.5;
  }
  .option-btn:hover:not(.disabled) { border-color: var(--blue-light); background: #eff6ff; }
  .option-btn .opt-label {
    min-width: 28px;
    height: 28px;
    background: var(--bg);
    border-radius: 6px;
    display:flex; align-items:center; justify-content:center;
    font-weight: 700;
    font-size: 12px;
    color: var(--navy);
    flex-shrink: 0;
  }
  .option-btn.selected { border-color: var(--blue); background: #eff6ff; }
  .option-btn.selected .opt-label { background: var(--blue); color: white; }
  .option-btn.correct { border-color: var(--green); background: var(--correct); }
  .option-btn.correct .opt-label { background: var(--green); color: white; }
  .option-btn.wrong { border-color: var(--red); background: var(--wrong); }
  .option-btn.wrong .opt-label { background: var(--red); color: white; }
  .option-btn.disabled { cursor: default; }

  /* PGK checkboxes */
  .option-btn.pgk-opt { }
  .option-btn.pgk-opt .opt-label { border-radius: 4px; border: 2px solid var(--border); background: white; }
  .option-btn.pgk-opt.selected .opt-label {
    background: var(--accent);
    border-color: var(--accent);
    color: var(--navy);
  }

  /* ── BENAR SALAH TABLE ── */
  .bs-table { width:100%; border-collapse: collapse; margin-top: 8px; }
  .bs-table th {
    background: var(--navy);
    color: white;
    padding: 10px 14px;
    font-size: 12px;
    text-align: left;
  }
  .bs-table th:last-child, .bs-table th:nth-last-child(2) { text-align: center; width: 80px; }
  .bs-table td {
    padding: 10px 14px;
    border-bottom: 1px solid var(--border);
    font-size: 13.5px;
    vertical-align: middle;
  }
  .bs-table tr:nth-child(even) td { background: #f8faff; }
  .bs-label { width:32px; font-weight:700; color:var(--navy); }
  .bs-radio {
    display:flex; align-items:center; justify-content:center;
  }
  .bs-radio input[type=radio] { display:none; }
  .bs-radio label {
    width: 30px; height: 30px;
    border: 2px solid var(--border);
    border-radius: 50%;
    cursor: pointer;
    display:flex; align-items:center; justify-content:center;
    font-size: 14px;
    transition: all .18s;
    background: white;
  }
  .bs-radio label:hover { border-color: var(--blue); }
  .bs-radio input:checked + label { border-color: var(--blue); background: var(--blue); color: white; }
  .bs-radio.benar input:checked + label { background: var(--green); border-color: var(--green); }
  .bs-radio.salah input:checked + label { background: var(--red); border-color: var(--red); }

  /* ── PEMBAHASAN ── */
  .pembahasan {
    margin-top: 18px;
    border-top: 2px dashed var(--border);
    padding-top: 16px;
    display: none;
    animation: fadeIn .3s ease;
  }
  .pembahasan.show { display: block; }
  .pemb-header {
    font-size: 12px;
    font-weight: 700;
    color: var(--muted);
    letter-spacing: .5px;
    text-transform: uppercase;
    margin-bottom: 10px;
    display:flex; align-items:center; gap:6px;
  }
  .rumus-box {
    background: #eff6ff;
    border: 1px solid #bfdbfe;
    border-radius: 8px;
    padding: 10px 14px;
    font-size: 13px;
    font-weight: 600;
    color: #1d4ed8;
    margin-bottom: 10px;
  }
  .step { font-size: 13px; color: var(--text); margin-bottom: 5px; padding-left: 18px; position:relative; line-height:1.6; }
  .step::before { content: "→"; position:absolute; left:0; color:var(--blue); font-weight:700; }
  .jawaban-final {
    margin-top: 10px;
    padding: 10px 14px;
    background: #dcfce7;
    border-radius: 8px;
    font-weight: 700;
    font-size: 13.5px;
    color: #065f46;
    border: 1px solid #86efac;
  }
  /* BS pembahasan table */
  .bs-pemb-row { border-bottom: 1px solid var(--border); padding: 8px 0; font-size: 13px; }
  .bs-pemb-label { font-weight:700; color: var(--navy); margin-right:8px; }
  .bs-pemb-jawaban { display:inline-block; padding:1px 8px; border-radius:4px; font-size:11px; font-weight:700; margin-right:8px; }
  .bs-pemb-jawaban.benar { background:#dcfce7; color:#065f46; }
  .bs-pemb-jawaban.salah { background:#fee2e2; color:#991b1b; }

  /* ── ACTIONS ── */
  .actions {
    display:flex; gap:10px; flex-wrap:wrap;
    margin-top: 4px;
  }
  .btn {
    padding: 11px 22px;
    border-radius: 10px;
    border: none;
    font-family: inherit;
    font-size: 14px;
    font-weight: 700;
    cursor: pointer;
    transition: all .18s;
    display:flex; align-items:center; gap:7px;
  }
  .btn-primary { background: var(--blue); color: white; }
  .btn-primary:hover { background: #1d4ed8; transform: translateY(-1px); }
  .btn-outline { background: white; color: var(--navy); border: 2px solid var(--border); }
  .btn-outline:hover { border-color: var(--blue); color: var(--blue); }
  .btn-accent { background: var(--accent); color: var(--navy); }
  .btn-accent:hover { background: var(--accent2); }
  .btn-green { background: var(--green); color: white; }
  .btn-green:hover { background: #059669; }
  .btn:disabled { opacity:.4; cursor:default; transform:none !important; }

  /* ── RESULT SCREEN ── */
  #result-screen {
    display: none;
    background: var(--card);
    border-radius: var(--radius);
    padding: 40px 28px;
    text-align: center;
    box-shadow: 0 4px 24px rgba(0,0,0,.1);
    animation: fadeIn .4s ease;
  }
  .result-emoji { font-size: 64px; margin-bottom: 12px; }
  .result-title { font-size: 28px; font-weight: 800; color: var(--navy); margin-bottom: 6px; }
  .result-sub { font-size: 15px; color: var(--muted); margin-bottom: 28px; }
  .score-big {
    font-size: 72px;
    font-weight: 800;
    font-family: 'JetBrains Mono', monospace;
    color: var(--blue);
    line-height: 1;
    margin-bottom: 8px;
  }
  .score-label { font-size: 13px; color: var(--muted); margin-bottom: 28px; }
  .stats-grid {
    display: grid;
    grid-template-columns: repeat(3, 1fr);
    gap: 14px;
    margin-bottom: 28px;
  }
  .stat-box {
    padding: 16px 10px;
    border-radius: 12px;
    border: 2px solid var(--border);
  }
  .stat-box.correct-box { border-color: var(--green); background: var(--correct); }
  .stat-box.wrong-box { border-color: var(--red); background: var(--wrong); }
  .stat-box.skip-box { border-color: var(--border); background: #f8faff; }
  .stat-num { font-size: 28px; font-weight: 800; }
  .stat-lbl { font-size: 11px; color: var(--muted); margin-top: 2px; }
  .correct-box .stat-num { color: var(--green); }
  .wrong-box .stat-num { color: var(--red); }
  .predikat {
    display: inline-block;
    padding: 6px 20px;
    border-radius: 20px;
    font-weight: 700;
    font-size: 14px;
    margin-bottom: 24px;
  }

  /* ── REVIEW ── */
  #review-section { display:none; margin-top: 24px; }
  .review-item {
    background: var(--card);
    border-radius: 12px;
    padding: 20px;
    margin-bottom: 14px;
    border-left: 4px solid var(--border);
    box-shadow: 0 1px 8px rgba(0,0,0,.05);
  }
  .review-item.correct { border-left-color: var(--green); }
  .review-item.wrong { border-left-color: var(--red); }
  .review-item.partial { border-left-color: var(--accent); }

  /* ── RESPONSIVE ── */
  @media(max-width:600px) {
    .soal-card { padding: 18px; }
    .header-inner { padding: 12px 14px; }
    .stats-grid { grid-template-columns: repeat(3,1fr); }
    .score-big { font-size: 56px; }
  }
</style>
</head>
<body>

<!-- HEADER -->
<div class="header">
  <div class="header-inner">
    <span class="header-badge">TKA</span>
    <h1>Latihan Soal <span>Matematika SMP</span></h1>
    <div id="timer">45:00</div>
  </div>
  <div class="progress-wrap">
    <div class="progress-inner">
      <div class="progress-info">
        <span id="progress-text">Soal 1 dari 20</span>
        <span id="answered-count">0 dijawab</span>
      </div>
      <div class="progress-bar"><div class="progress-fill" id="progress-fill" style="width:5%"></div></div>
    </div>
  </div>
</div>

<div class="main">

  <!-- NAVIGATOR -->
  <div class="nav-grid" id="nav-grid"></div>

  <!-- SOAL AREA -->
  <div id="soal-area">
    <div class="soal-card" id="soal-card"></div>
    <div class="actions" id="actions"></div>
  </div>

  <!-- RESULT SCREEN -->
  <div id="result-screen"></div>

  <!-- REVIEW SECTION -->
  <div id="review-section"></div>

</div>

<script>
// ════════════════════════════════════════════════════════
// DATA SOAL
// ════════════════════════════════════════════════════════
const soalData = [
  // ── PILIHAN GANDA BIASA ──────────────────────────────
  {
    no:1, tipe:"pg",
    konteks:"Sebuah toko buku menjual novel dengan harga Rp45.000 per buku. Toko memberikan diskon 20% untuk pembelian minimal 3 buku.",
    tanya:"Jika Rara membeli 4 buku novel, berapa total yang harus dibayar Rara?",
    opsi:["Rp144.000","Rp162.000","Rp180.000","Rp126.000"],
    jawaban:"A",
    rumus:"Harga setelah diskon = harga asal × (1 – diskon%)",
    langkah:["Harga 1 buku = Rp45.000","Beli 4 buku → syarat diskon terpenuhi (≥3 buku)","Diskon 20% → harga/buku = 45.000 × 0,80 = Rp36.000","Total 4 buku = 4 × 36.000 = Rp144.000"],
    jawabanFinal:"✅ Jawaban: A. Rp144.000"
  },
  {
    no:2, tipe:"pg",
    konteks:"Pak Budi memiliki kebun berbentuk persegi panjang. Panjang kebun adalah (3x + 2) meter dan lebarnya (x + 4) meter.",
    tanya:"Jika keliling kebun adalah 44 meter, berapakah nilai x?",
    opsi:["2","3","4","5"],
    jawaban:"C",
    rumus:"Keliling persegi panjang = 2 × (panjang + lebar)",
    langkah:["K = 2(p + l) = 44 → p + l = 22","(3x+2) + (x+4) = 22","4x + 6 = 22 → 4x = 16 → x = 4","Cek: p = 3(4)+2 = 14, l = 4+4 = 8 → K = 2(22) = 44 ✓"],
    jawabanFinal:"✅ Jawaban: C. x = 4"
  },
  {
    no:3, tipe:"pg",
    konteks:"Data nilai ulangan Matematika 7 siswa: 65, 70, 80, 75, 90, 70, 85.",
    tanya:"Nilai rata-rata ulangan tersebut adalah ...",
    opsi:["72,5","75,0","76,4","77,5"],
    jawaban:"C",
    rumus:"Rata-rata = jumlah data ÷ banyak data",
    langkah:["Jumlah = 65+70+80+75+90+70+85 = 535","Banyak data = 7","Rata-rata = 535 ÷ 7 = 76,43 ≈ 76,4"],
    jawabanFinal:"✅ Jawaban: C. 76,4"
  },
  {
    no:4, tipe:"pg",
    konteks:"Sebuah kolam renang berbentuk balok memiliki panjang 10 m, lebar 4 m, dan kedalaman 2 m. Kolam akan diisi air hingga penuh.",
    tanya:"Berapa liter air yang dibutuhkan? (1 m³ = 1.000 liter)",
    opsi:["60.000 liter","80.000 liter","100.000 liter","120.000 liter"],
    jawaban:"B",
    rumus:"Volume balok = p × l × t",
    langkah:["V = 10 × 4 × 2 = 80 m³","Konversi: 80 × 1.000 = 80.000 liter"],
    jawabanFinal:"✅ Jawaban: B. 80.000 liter"
  },
  {
    no:5, tipe:"pg",
    konteks:"Dua buah roda gigi terhubung. Roda A memiliki 24 gigi dan roda B memiliki 36 gigi. Roda A berputar 9 kali.",
    tanya:"Berapa kali roda B berputar?",
    opsi:["4 kali","5 kali","6 kali","8 kali"],
    jawaban:"C",
    rumus:"Gigi A × putaran A = Gigi B × putaran B",
    langkah:["24 × 9 = 36 × n","216 = 36n → n = 6"],
    jawabanFinal:"✅ Jawaban: C. 6 kali"
  },
  {
    no:6, tipe:"pg",
    konteks:"Dalam sebuah kelas terdapat 30 siswa. 18 siswa menyukai basket, 15 siswa menyukai voli, dan 8 siswa menyukai keduanya.",
    tanya:"Berapa siswa yang tidak menyukai keduanya?",
    opsi:["3","4","5","6"],
    jawaban:"C",
    rumus:"n(A∪B) = n(A) + n(B) – n(A∩B)",
    langkah:["n(basket ∪ voli) = 18 + 15 – 8 = 25","Tidak menyukai keduanya = 30 – 25 = 5"],
    jawabanFinal:"✅ Jawaban: C. 5 siswa"
  },
  {
    no:7, tipe:"pg",
    konteks:"Sebuah tangga disandarkan ke dinding. Kaki tangga berjarak 5 m dari dinding dan panjang tangga adalah 13 m.",
    tanya:"Setinggi berapa tangga menyandar pada dinding?",
    opsi:["10 m","11 m","12 m","14 m"],
    jawaban:"C",
    rumus:"Teorema Pythagoras: tinggi² = tangga² – jarak²",
    langkah:["tinggi² = 13² – 5² = 169 – 25 = 144","tinggi = √144 = 12 m"],
    jawabanFinal:"✅ Jawaban: C. 12 m"
  },
  {
    no:8, tipe:"pg",
    konteks:"Sebuah tabungan awal Rp2.000.000 dengan bunga sederhana 5% per tahun.",
    tanya:"Berapa total tabungan setelah 3 tahun?",
    opsi:["Rp2.100.000","Rp2.200.000","Rp2.300.000","Rp2.500.000"],
    jawaban:"C",
    rumus:"Total = modal + (modal × suku bunga × waktu)",
    langkah:["Bunga/tahun = 2.000.000 × 5% = Rp100.000","Bunga 3 tahun = 3 × 100.000 = Rp300.000","Total = 2.000.000 + 300.000 = Rp2.300.000"],
    jawabanFinal:"✅ Jawaban: C. Rp2.300.000"
  },

  // ── PILIHAN GANDA KOMPLEKS ───────────────────────────
  {
    no:9, tipe:"pgk",
    instruksi:"Pilih semua pernyataan yang BENAR! Jawaban benar lebih dari satu.",
    konteks:"Sebuah ojek online mengenakan tarif:\n• Biaya dasar: Rp5.000\n• Biaya per km: Rp2.500\nSeorang pelanggan memiliki saldo maksimal Rp30.000.",
    tanya:"Manakah pernyataan yang benar?",
    opsi:[
      "A. Jika x = jarak (km), model matematikanya: 2.500x + 5.000 ≤ 30.000",
      "B. Jarak maksimum yang bisa ditempuh adalah 10 km",
      "C. Jika jarak 11 km, biaya total melebihi saldo pelanggan",
      "D. Penambahan 1 km menambah biaya Rp5.000"
    ],
    jawaban:["A","B","C"],
    rumus:"Model pertidaksamaan: biaya tetap + (biaya/km × jarak) ≤ anggaran",
    langkah:[
      "Model: 2.500x + 5.000 ≤ 30.000 → A BENAR ✓",
      "2.500x ≤ 25.000 → x ≤ 10 → B BENAR ✓",
      "x=11: 2.500(11)+5.000 = 32.500 > 30.000 → C BENAR ✓",
      "Biaya per km = Rp2.500 (bukan 5.000) → D SALAH ✗"
    ],
    jawabanFinal:"✅ Jawaban: A, B, C"
  },
  {
    no:10, tipe:"pgk",
    instruksi:"Pilih semua pernyataan yang BENAR! Jawaban benar lebih dari satu.",
    konteks:"Data tinggi badan (cm) 8 siswa: 72, 68, 75, 80, 68, 77, 80, 80",
    tanya:"Manakah pernyataan yang benar tentang data tersebut?",
    opsi:[
      "A. Modus data tersebut adalah 80",
      "B. Median data tersebut adalah 76",
      "C. Rata-rata data tersebut adalah 75",
      "D. Jangkauan data tersebut adalah 12"
    ],
    jawaban:["A","B","C","D"],
    rumus:"Modus=terbanyak, Median=tengah, Mean=rata-rata, Jangkauan=maks–min",
    langkah:[
      "Urut: 68,68,72,75,77,80,80,80",
      "Modus = 80 (muncul 3×) → A BENAR ✓",
      "Med
