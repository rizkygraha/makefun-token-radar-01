# STATUS — token-radar-01 (bright-sparrow-85)

Terakhir diperbarui: Selasa 17 Nov 2026 ~20:15 WIB. Deadline: Senin 14 Des 2026 17:00 WIB.

## Ringkas

Entri SELESAI DIBANGUN dan lolos semua pemeriksaan gate yang bisa dijalankan lokal.
BELUM SUBMIT — menunggu akses GitHub (lihat Blocker).

## Requirements (GET /api/competitions/token-radar-01/requirements)

- Prerequisites: Node.js 22.18+ dan browser untuk 3 screenshot. Terpenuhi:
  Node v24.22.1; screenshot diambil dengan Playwright Chromium 159 (headless shell).
- Deliverables wajib: repo_url publik, commit_sha 40 karakter, bundle transkrip,
  entry_message + entry_signature (ditandatangani wallet akun), LICENSE OSI,
  main.ts di root repo, `.makefun/owner.json` (akun wallet-only, tanpa login GitHub).
- Deadline entri: 2026-12-14T10:00:00Z. Pot $1.325, tanpa entry fee.

## Yang sudah dibangun (repo `bounties/token-radar-01`, git init 17 Nov 2026)

| File | Keterangan |
| --- | --- |
| `main.ts` | entrypoint Node 22, stdlib only (ditulis sendiri) |
| `lib/model.ts` | model radar-2 + farm plan + validasi board (ditulis sendiri) |
| `vendor/makefun-board.ts` | library dossier dari kit, byte-for-byte (sha256 sama dengan kit.json) |
| `dashboard/index.html`, `app.css`, `app.js` | dashboard statis tema gelap, tanpa network (ditulis sendiri) |
| `screenshots/1-board.png` | board, 1440×900, 152.954 byte |
| `screenshots/2-detail.png` | detail Steakhouse Financial (#1), 1440×900, 223.486 byte |
| `screenshots/3-filtered.png` | board terfilter Lending (14 baris), 1440×900, 150.116 byte |
| `LICENSE` | MIT |
| `.makefun/owner.json` | wallet akun (alamat publik) |
| `README.md` | dokumentasi entri |

Total sumber dashboard: 43.719 byte (batas teks dossier 65.536) — judge membaca
seluruh sumber. Tidak ada alamat network di file dashboard (diperiksa dengan grep).

## Metodologi rangking (radar-2, semua dari angka snapshot)

`implied = TVL × category multiple × growth × maturity × breadth × launch probability`

- **Category multiple**: median mcap/TVL protokol live-token di kategori yang sama
  (≥3 protokol, jika tidak median global), dihitung saat run dari snapshot,
  dijepit [0,05, 2,00]. Contoh: Lending 0,132; Dexs 0,342; RWA 0,275; global 0,205.
- **Growth**: 1 + clamp(change_7d, −60, 120)% / 100 × 0,5.
- **Maturity**: 0,6 + min(umur, 1095)/1095 × 0,4 (umur tak diketahui = 365 hari).
- **Breadth**: min(1 + 0,02 × (chains−1), 1,10).
- **Launch probability**: clamp(0,15 + 0,35×umur + 0,15×pertumbuhan + 0,10×ukuran,
  0,10, 0,85) — dinyatakan sebagai estimasi, bukan janji.
- Board: **178 baris** = 40 watchlist + 138 early di bawah floor $50M. 20 protokol
  di atas floor yang tidak masuk watchlist sengaja dikeluarkan (aturan watchlist
  menyaringnya — parent protocol — dan snapshot tidak bisa membedakannya dari
  produk wrapped). 24 protokol live-token dipisah, ditampilkan dengan nilai pasar.
- Farm plan: 7 langkah per protokol (dompet baru, aksi utama per kategori, aksi
  kedua yang berbeda, cadence mingguan, hold 30–60 hari, cek halaman points,
  farm log), masing-masing dengan biaya dan waktu; semua 20–600 karakter.
- Top 5: 1. Steakhouse Financial $167,6M · 2. Gauntlet $101,3M · 3. USDD $63,6M ·
  4. Veda $29,8M · 5. OpenTrade $25,4M. Total implied board $786,6M, median $878K.

## Verifikasi lokal (17 Nov 2026)

- `MAKEFUN_OUTPUT_DIR=out node main.ts --input token-radar-01-kit/input/snapshot.json`
  → OK: "758 protocols, 40 on the watchlist, 178 rows scored (138 early, 24 live
  set aside)". `boardIssue` internal lolos (coverage watchlist 40/40, rank 1..178,
  terurut menurun, nilai berbeda, langkah farm valid).
- Screenshot: Playwright Chromium 159 (headless shell, diunduh via npm) — 3 shot,
  tanpa console error. Chrome sistem (/opt/meta-chromium/chrome) TIDAK bisa
  dipakai: menolak start ("Hatch WebGL domain policy is required for browser
  startup", exit 13). Solusi: Chromium bawaan Playwright.
- Gate: board 178 baris (batas 100–4000); screenshot ≤512 KiB, 1440×900
  (sisi pendek ≥800); dossier 747.163 byte (<1,5 MiB); dashboard 3 file, 43.719
  byte; tanpa network di dashboard.
- `makefun check` / `grade-local --check`: `--check` hanya untuk kit scrape/v1;
  `makefun check` membutuhkan commit + transkrip (lihat di bawah). Scorer
  tersegel (tujuh baris gate) hanya berjalan di server saat grading; pemeriksaan
  lokal di atas mereplikasi aturannya dari `reference/gate.json` di competition.yaml.

## Transkrip — `bundle --dry-run` (dijalankan 17 Nov ~19:57 WIB, SEBELUM build)

DITEMUKAN 3 file sesi Muse app (bukan blocker):

- `sessions/muse-app/2009fd8d-c808-4009-b809-924ddf39f891.jsonl` — sesi worker ini,
  13 turns, 54 baris.
- `sessions/muse-app/89983377-8361-48f6-bd09-1394810fecea.jsonl` — sesi agen utama,
  16 turns (disimpan).
- `sessions/muse-app/cc93f902-3d6f-4515-87cb-05bf448fdcb1.jsonl` — sesi lama yang
  menulis check-me.mjs, 12 turns (disimpan).
- 1 instruction file: `context/repo/_parent-5/AGENTS.md` (dari ~/AGENTS.md).
- Yang masih kurang untuk bundle asli: `--mcp none` (atau daftar MCP),
  `--harness/--harness-version/--provider/--model/--effort`, dan usage rows via
  `--muse-usage` (diambil dari muse.db SETELAH sesi selesai — baris usage ditulis
  saat pesan terkirim; agen utama yang harus menjalankannya saat submit).
- Catatan: run record prompt yang terambil dari sesi lama ("Jadi kalau aku ingin
  login akunnya gimana?...") BUKAN prompt tugas bounty ini — saat submit, sertakan
  `--prompt-file` berisi prompt pembuka user yang sebenarnya + `--prompt-origin
  handed-off` (tugas ini diteruskan dari agen utama).

## Blocker — GitHub (penghalang submit)

- `gh auth status`: "You are not logged into any GitHub hosts." Tidak ada
  `~/.config/gh/`. JANGAN login/minta kredensial — agen utama sedang meminta
  akses GitHub ke user secara paralel.
- Repo git lokal sudah `git init` dan siap di-push begitu akses tersedia
  (remote belum ditambahkan — belum ada URL repo).
- Setelah akses tersedia: buat repo publik, push, lalu submit via
  `node token-radar-01-kit/cli/makefun.mjs submit --competition token-radar-01
  --source <repo> --commit <sha> --keypair <keypair>` + bundle transkrip
  (jangan submit sebelum bundle + usage rows lengkap).

## Catatan lain

- Kit diunduh ke `token-radar-01-kit/` + `kit.tar.gz` di direktori bounty; keduanya
  di-.gitignore (bukan bagian entri).
- Direktori kerja screenshot Playwright: `/tmp/shot` (bukan bagian entri).
- `out/` (hasil run lokal) juga di-.gitignore.
