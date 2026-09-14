# Arsip Riwayat Deployment — Project Vercel Lama (`gensiti1` / akun `morenoryandika`)

> **Ini arsip, bukan dokumen kerja aktif.** Disusun **14 September 2026**, sebelum migrasi
> kepemilikan project Vercel dari akun `morenoryandika` (tim Vercel **"GENSITI SOMS"**, slug
> `gensiti1`) ke akun **`generusbekasitimur@gmail.com`**.
>
> - **Project ID**: `prj_wFBTEAPLaHqs24uuFKwL7AwapRkS`
> - **Team ID**: `team_jQN5VrZowCfoQhCcMrNlG9nD`
> - **Terhubung ke GitHub**: `Moreno19Ryan/gensiti-app` (org/user lama — belum menunjuk ke
>   `generusbekasitimur-arch/gensiti-app` per tanggal arsip ini dibuat)
>
> Project Vercel lama ini **SENGAJA dibiarkan ada, tidak dihapus**, sebagai referensi kalau
> sewaktu-waktu butuh detail lebih dalam (full build log, function log runtime, analytics,
> dst.) yang tidak semuanya terekam ringkas di tabel bawah ini.

---

## ⚠️ Catatan cakupan data — baca dulu sebelum menganggap ini lengkap

Data di bawah diambil lewat Vercel MCP tool `list_deployments`, dipaginasi sampai habis
(halaman ke-3 kosong — jadi ini **seluruh riwayat yang masih bisa diakses lewat API/tool**,
bukan dipotong sengaja oleh saya). Hasilnya: **40 deployment**, semuanya jatuh di rentang
**27 Juli 2026 – 4 Agustus 2026 (WIB)**.

Ini janggal dibandingkan `HANDOFF.md` yang mencatat sesi kerja sejak **16 Juli 2026**, dan
project Vercel ini sendiri dibuat ~akhir Juni 2026 (`createdAt` project = 28 Juni 2026 UTC).
Artinya ada **rentang ±4 minggu (akhir Juni – 26 Juli 2026) yang deployment-nya tidak lagi
muncul lewat API ini** — saya tidak bisa memastikan penyebabnya dari sesi ini (dugaan paling
masuk akal: retensi riwayat deployment di plan **Hobby** Vercel, tapi bisa juga sebab lain).

**Kalau riwayat periode itu penting buat Reno**, cek manual di Vercel Dashboard
(`vercel.com/gensiti1/gensiti-app` → tab **Deployments** → coba scroll/"load more" sampai
paling bawah) **SEBELUM migrasi selesai** — begitu ownership pindah, belum tentu tampilannya
persis sama atau semudah ini diakses lagi.

---

## Ringkasan cepat

| | |
|---|---|
| Total deployment tercatat | **40** |
| Rentang waktu | 27 Juli 2026 – 4 Agustus 2026 (WIB) |
| Production | 20 |
| Preview | 20 |
| Status build | **40/40 READY** — tidak ada satu pun `ERROR` di riwayat yang tercatat |
| Branch produksi | `main` (semua deployment `target=production` dari branch ini) |
| Branch kerja utama | `claude/gemini-gensiti-collaboration-1vrtvi` (long-lived, sumber sebagian besar preview PR #27–#39) |
| Branch kerja lain | `claude/trigger-vercel-redeploy` (1 preview, PR #26 — lihat insiden di bawah) |

---

## Rilis utama & insiden (cocok dengan `HANDOFF.md`)

- **27 Jul, sha `d9b94a1`, PR #26 — "chore: trigger Vercel redeploy"**: bukan fitur, ini
  commit kosong untuk memaksa Vercel build ulang. `HANDOFF.md` (sesi 27 Juli, penyelesaian A4)
  mencatat Vercel sempat **tidak auto-deploy** commit merge PR #25, dan tombol Redeploy di
  dashboard cuma membangun ulang commit lama — bukan HEAD terbaru. Ini fix-nya.
- **28 Jul, sha `9bcb7b4`, PR #27 — "B1 Gamifikasi, notifikasi push, export konsisten, jendela
  presensi otomatis"**: rilis gabungan terbesar dalam arsip ini — 6 preview build beruntun
  (badge gamifikasi, banner aktivasi push, pratinjau+cetak PDF konsisten, jendela presensi
  otomatis berbasis waktu) di-squash jadi satu merge ke production.
- **28 Jul, PR #28–#31 — seri "Berita LDII"**: fitur baru (mirror RSS berita LDII) dibangun
  dan diiterasi 4x berturut-turut dalam satu hari (tambah gambar, share WhatsApp, ganti ikon).
- **28 Jul, sha `a1dec52`, PR #32 — "Generalisasi Berita LDII jadi Berita Organisasi"**:
  refactor arsitektur — satu tabel & satu Edge Function menangani banyak sumber (LDII,
  PERSINAS ASAD, SENKOM), gantikan skema khusus-LDII dari PR #28-31.
- **28 Jul, sha `03366d9`, PR #34 — "Bookmark Berita & FAQ/Panduan"**: dua fitur baru sekaligus.
- **29 Jul, sha `9460dde`, PR #36 — "Fix: keyboard HP menutup tiap 1 karakter di semua form
  modal"**: bugfix penting — root cause di `Modal.tsx` (dipakai 13 halaman), semua form input
  di HP kena.
- **29 Jul, PR #37 & #39 — Redesain navigasi Opsi C Tahap 1 & 2**: sidebar desktop (`07b5a90`)
  lalu bottom nav mobile (`2058d5c`) jadi gaya liquid glass — dua tahap, dua hari berdekatan.
- **4 Agustus, sha `8f4e2f6`, PR #40 — "A3: backup otomatis ke Storage (Opsi C) + koreksi
  guardrail database branch"**: **rilis terakhir di project lama ini** (dan masih jadi HEAD
  `main` saat arsip ini dibuat) — backup database otomatis mingguan ke Supabase Storage.
  Preview-nya sendiri sudah build 29 Juli 13:34 WIB, tapi baru merge ke production 6 hari
  kemudian (4 Agustus) — konsisten dengan `HANDOFF.md` yang mencatat proses verifikasi
  restorability nyata (bukan cuma asumsi) sebelum dianggap selesai.

---

## Riwayat lengkap, kronologis

### Juli 2026

#### 27 Juli 2026

| Waktu (WIB) | Commit | Pesan commit | Branch | Environment | Status |
|---|---|---|---|---|---|
| 00:42 | `cfdb3ed` | Audit menyeluruh + fondasi UX: sistem toast & dialog konfirmasi (#22) | `main` | Production | READY |
| 00:42 | `50ec549` | Docs: catat penyelesaian B4 (menu Pengaturan) di HANDOFF & WISHLIST_ASSESSMENT (#21) | `main` | Production | READY |
| 09:32 | `882119f` | docs: tambah KONSEP_GENSITI.md (visi, alur kerja, roadmap rilis) (#1) | `main` | Production | READY |
| 15:58 | `1472b30` | UX: a11y Modal.tsx (focus trap, Escape) + skeleton loader 6 halaman utama (#23) | `main` | Production | READY |
| 16:02 | `72198ec` | UX: transisi halus antar halaman & antar menu sidebar (#24) | `main` | Production | READY |
| 19:34 | `91f1587` | chore: trigger Vercel redeploy (webhook sempat tidak jalan otomatis utk merge A4) | `claude/trigger-vercel-redeploy` | Preview (PR #26) | READY |
| 21:16 | `d9b94a1` | Merge PR #26 — chore: trigger Vercel redeploy | `main` | Production | READY |
| 21:24 | `78c3033` | docs: catat penyelesaian A4 (PR #25), insiden deploy, dan cleanup mitigasi darurat | `claude/gemini-gensiti-collaboration-1vrtvi` | Preview (PR #27) | READY |
| 22:20 | `f49183d` | docs: catat penyelesaian item #5, #7, #8 audit (search_path, RLS auth.uid(), index FK) | `claude/gemini-gensiti-collaboration-1vrtvi` | Preview (PR #27) | READY |

#### 28 Juli 2026

| Waktu (WIB) | Commit | Pesan commit | Branch | Environment | Status |
|---|---|---|---|---|---|
| 00:38 | `c80be72` | B1: Gamifikasi ringan v1 -- badge personal Generus (bukan leaderboard) | `claude/gemini-gensiti-collaboration-1vrtvi` | Preview (PR #27) | READY |
| 05:42 | `085ea48` | Notifikasi: banner ajakan aktifkan push di halaman utama | `claude/gemini-gensiti-collaboration-1vrtvi` | Preview (PR #27) | READY |
| 06:39 | `ab941f5` | Pratinjau+Cetak langsung konsisten di semua export, filter jenis kelamin Data Generus | `claude/gemini-gensiti-collaboration-1vrtvi` | Preview (PR #27) | READY |
| 07:06 | `48e6449` | Kegiatan: jendela presensi otomatis berbasis waktu, hapus status manual | `claude/gemini-gensiti-collaboration-1vrtvi` | Preview (PR #27) | READY |
| 07:27 | `9bcb7b4` | **Merge PR #27 — B1 Gamifikasi, notifikasi push, export konsisten, jendela presensi otomatis** | `main` | Production | READY |
| 08:03 | `5461592` | Tambah menu Berita LDII -- mirror ringkasan RSS feed publik ldii.or.id | `claude/gemini-gensiti-collaboration-1vrtvi` | Preview (PR #28) | READY |
| 08:06 | `60e6f27` | **Merge PR #28 — Menu Berita LDII** | `main` | Production | READY |
| 08:20 | `29fcba4` | Berita LDII: bersihkan teks feed, tambah gambar, redesain kartu jadi menarik | `claude/gemini-gensiti-collaboration-1vrtvi` | Preview (PR #29) | READY |
| 08:22 | `a0df30c` | Merge PR #29 — Berita LDII: bersihkan teks feed, tambah gambar | `main` | Production | READY |
| 08:39 | `cbe0808` | Berita LDII: tambah bagikan WhatsApp, filter kategori, dan pencarian | `claude/gemini-gensiti-collaboration-1vrtvi` | Preview (PR #30) | READY |
| 08:50 | `3853708` | Merge PR #30 — Berita LDII: bagikan WhatsApp, filter kategori, pencarian | `main` | Production | READY |
| 08:58 | `02e160f` | Berita LDII: pakai ikon WhatsApp asli, bukan emoji generik | `claude/gemini-gensiti-collaboration-1vrtvi` | Preview (PR #31) | READY |
| 09:14 | `ec43751` | Merge PR #31 — Berita LDII: pakai ikon WhatsApp asli | `main` | Production | READY |
| 15:01 | `6efda04` | Generalisasi Berita LDII jadi Berita Organisasi (LDII, PERSINAS ASAD, SENKOM) | `claude/gemini-gensiti-collaboration-1vrtvi` | Preview (PR #32) | READY |
| 15:12 | `a1dec52` | **Merge PR #32 — Generalisasi Berita LDII jadi Berita Organisasi** | `main` | Production | READY |
| 15:45 | `275c680` | Berita Organisasi: tambah DPD LDII Kota Bekasi sebagai sumber ke-4 | `claude/gemini-gensiti-collaboration-1vrtvi` | Preview (PR #33) | READY |
| 15:51 | `a20bb4e` | Merge PR #33 — Berita Organisasi: tambah DPD LDII Kota Bekasi | `main` | Production | READY |
| 19:42 | `4b510da` | Tambah fitur Bookmark Berita & FAQ/Panduan | `claude/gemini-gensiti-collaboration-1vrtvi` | Preview (PR #34) | READY |
| 19:46 | `03366d9` | **Merge PR #34 — Tambah fitur Bookmark Berita & FAQ/Panduan** | `main` | Production | READY |
| 20:35 | `e27158e` | Redesain nav tab Berita jadi glassmorphism ala iOS Liquid Glass / One UI | `claude/gemini-gensiti-collaboration-1vrtvi` | Preview (PR #35) | READY |
| 20:50 | `e2bd8fe` | Merge PR #35 — Redesain nav tab Berita jadi glassmorphism | `main` | Production | READY |

#### 29 Juli 2026

| Waktu (WIB) | Commit | Pesan commit | Branch | Environment | Status |
|---|---|---|---|---|---|
| 00:09 | `439c1ca` | Fix: keyboard HP menutup tiap 1 karakter di semua form modal | `claude/gemini-gensiti-collaboration-1vrtvi` | Preview (PR #36) | READY |
| 00:47 | `9460dde` | **Merge PR #36 — Fix: keyboard HP menutup tiap 1 karakter di semua form modal** | `main` | Production | READY |
| 01:24 | `7f532e9` | Redesain navigasi Opsi C (Tahap 1): sidebar desktop jadi liquid glass | `claude/gemini-gensiti-collaboration-1vrtvi` | Preview (PR #37) | READY |
| 06:02 | `07b5a90` | **Merge PR #37 — Redesain navigasi Opsi C (Tahap 1): sidebar desktop jadi liquid glass** | `main` | Production | READY |
| 09:22 | `a0830e0` | docs: tambah catatan gap akses Dashboard di runbook recovery Super Admin | `claude/gemini-gensiti-collaboration-1vrtvi` | Preview (PR #38) | READY |
| 09:24 | `ebdc1c7` | Merge PR #38 — docs: tambah catatan gap akses Dashboard di runbook recovery Super Admin | `main` | Production | READY |
| 09:44 | `f85dc2c` | Redesain navigasi Opsi C (Tahap 2): bottom nav mobile liquid glass | `claude/gemini-gensiti-collaboration-1vrtvi` | Preview (PR #39) | READY |
| 09:48 | `2058d5c` | **Merge PR #39 — Redesain navigasi Opsi C (Tahap 2): bottom nav mobile liquid glass** | `main` | Production | READY |
| 13:34 | `66863a3` | A3: backup otomatis ke Storage (Opsi C) + koreksi guardrail database branch | `claude/gemini-gensiti-collaboration-1vrtvi` | Preview (PR #40) | READY |

### Agustus 2026

#### 4 Agustus 2026

| Waktu (WIB) | Commit | Pesan commit | Branch | Environment | Status |
|---|---|---|---|---|---|
| 08:19 | `8f4e2f6` | **Merge PR #40 — A3: backup otomatis ke Storage (Opsi C) + koreksi guardrail database branch** ⬅ *HEAD `main` saat arsip ini dibuat* | `main` | Production | READY |

---

*Disusun otomatis dari Vercel MCP `list_deployments` (project lama `gensiti1`), 14 September 2026.*
