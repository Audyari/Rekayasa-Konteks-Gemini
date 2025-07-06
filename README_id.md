# Template Rekayasa Konteks

Template komprehensif untuk memulai Rekayasa Konteks - disiplin merekayasa konteks untuk asisten AI pengkodean agar mereka memiliki informasi yang diperlukan untuk menyelesaikan tugas dari awal hingga akhir.

> **Rekayasa Konteks 10x lebih baik daripada rekayasa prompt dan 100x lebih baik daripada coding asal-asalan.**

## 🚀 Mulai Cepat

```bash
# 1. Klon template ini
git clone https://github.com/coleam00/Context-Engineering-Intro.git
cd Context-Engineering-Intro

# 2. Atur aturan proyek Anda (opsional - template disediakan)
# Edit GEMINI_id.md untuk menambahkan panduan spesifik proyek Anda

# 3. Tambahkan contoh (sangat disarankan)
# Tempatkan contoh kode yang relevan di folder examples/

# 4. Buat permintaan fitur awal
# Edit INITIAL.md dengan persyaratan fitur Anda

# 5. Hasilkan PRP (Product Requirements Prompt) yang komprehensif
# Di Gemini Code, jalankan:
/generate-prp INITIAL.md

# 6. Eksekusi PRP untuk mengimplementasikan fitur
# Di Gemini Code, jalankan:
/execute-prp PRPs/nama-fitur-anda.md
```

## 📚 Daftar Isi

- [Apa itu Rekayasa Konteks?](#apa-itu-rekayasa-konteks)
- [Struktur Template](#struktur-template)
- [Panduan Langkah demi Langkah](#panduan-langkah-demi-langkah)
- [Menulis File INITIAL.md yang Efektif](#menulis-file-initialmd-yang-efektif)
- [Alur Kerja PRP](#alur-kerja-prp)
- [Menggunakan Contoh dengan Efektif](#menggunakan-contoh-dengan-efektif)
- [Praktik Terbaik](#praktik-terbaik)

## Apa itu Rekayasa Konteks?

Rekayasa Konteks mewakili pergeseran paradigma dari rekayasa prompt tradisional:

### Rekayasa Prompt vs Rekayasa Konteks

**Rekayasa Prompt:**
- Berfokus pada pemilihan kata dan frasa yang cerdik
- Terbatas pada cara Anda merumuskan tugas
- Seperti memberikan seseorang catatan tempel

**Rekayasa Konteks:**
- Sistem lengkap untuk menyediakan konteks yang komprehensif
- Termasuk dokumentasi, contoh, aturan, pola, dan validasi
- Seperti menulis naskah lengkap dengan semua detailnya

### Mengapa Rekayasa Konteks Penting

1. **Mengurangi Kegagalan AI**: Sebagian besar kegagalan agen bukanlah kegagalan model - melainkan kegagalan konteks
2. **Memastikan Konsistensi**: AI mengikuti pola dan konvensi proyek Anda
3. **Memungkinkan Fitur Kompleks**: AI dapat menangani implementasi multi-tahap dengan konteks yang tepat
4. **Dapat Memperbaiki Diri**: Lingkaran validasi memungkinkan AI memperbaiki kesalahannya sendiri

## Struktur Template

```
context-engineering-intro/
├── .gemini/
│   ├── commands/
│   │   ├── generate-prp.md    # Menghasilkan PRP yang komprehensif
│   │   └── execute-prp.md     # Mengeksekusi PRP untuk mengimplementasikan fitur
│   └── settings.local.json    # Izin Gemini Code
├── PRPs/
│   ├── templates/
│   │   └── prp_base.md       # Template dasar untuk PRP
│   └── EXAMPLE_multi_agent_prp.md  # Contoh PRP lengkap
├── examples/                  # Contoh kode Anda (penting!)
├── GEMINI_id.md                 # Aturan global untuk asisten AI
├── INITIAL.md               # Template untuk permintaan fitur
├── INITIAL_EXAMPLE.md       # Contoh permintaan fitur
└── README.md                # File ini
```

Template ini tidak fokus pada RAG dan alat dengan rekayasa konteks karena saya memiliki banyak hal lain untuk itu nanti. ;)

## Panduan Langkah demi Langkah

### 1. Siapkan Aturan Global (CLAUDE.md)

File `CLAUDE.md` berisi aturan proyek yang akan diikuti oleh asisten AI dalam setiap percakapan. Template ini mencakup:

- **Kesadaran proyek**: Membaca dokumen perencanaan, memeriksa tugas
- **Struktur kode**: Batas ukuran file, organisasi modul
- **Persyaratan pengujian**: Pola pengujian unit, harapan cakupan
- **Konvensi gaya**: Preferensi bahasa, aturan pemformatan
- **Standar dokumentasi**: Format docstring, praktik komentar

**Anda dapat menggunakan template yang disediakan apa adanya atau menyesuaikannya untuk proyek Anda.**

**Catatan:** Perintah garis miring (slash commands) adalah perintah khusus yang didefinisikan di `.claude/commands/`. Anda dapat melihat implementasinya:
- `.claude/commands/generate-prp.md` - Melihat cara penelitian dan pembuatan PRP
- `.claude/commands/execute-prp.md` - Melihat cara mengimplementasikan fitur dari PRP

Variabel `$ARGUMENTS` dalam perintah ini menerima apa pun yang Anda masukkan setelah nama perintah (misalnya, `INITIAL.md` atau `PRPs/fitur-anda.md`).

Perintah ini akan:
1. Membaca permintaan fitur Anda
2. Menelusuri basis kode untuk menemukan pola
3. Mencari dokumentasi yang relevan
4. Membuat PRP komprehensif di `PRPs/nama-fitur-anda.md`

### 4. Eksekusi PRP

Setelah dibuat, eksekusi PRP untuk mengimplementasikan fitur Anda:

```bash
/execute-prp PRPs/nama-fitur-anda.md
```

Asisten AI pengkodean akan:
1. Membaca semua konteks dari PRP
2. Membuat rencana implementasi terperinci
3. Mengeksekusi setiap langkah dengan validasi
4. Menjalankan pengujian dan memperbaiki masalah yang ditemukan
5. Memastikan semua kriteria keberhasilan terpenuhi

## Menulis File INITIAL.md yang Efektif

### Bagian-bagian Utama

**FITUR**: Spesifik dan komprehensif
- ❌ "Buat web scraper"
- ✅ "Buat web scraper async menggunakan BeautifulSoup yang mengekstrak data produk dari situs e-commerce, menangani pembatasan kecepatan, dan menyimpan hasilnya di PostgreSQL"

**CONTOH**: Manfaatkan folder examples/
- Tempatkan pola kode yang relevan di `examples/`
- Rujuk file dan pola spesifik yang akan diikuti
- Jelaskan aspek apa yang harus ditiru

**DOKUMENTASI**: Sertakan semua sumber daya yang relevan
- URL dokumentasi API
- Panduan pustaka
- Dokumentasi server MCP
- Skema basis data

**PERTIMBANGAN LAINNYA**: Tangkap detail penting
- Persyaratan autentikasi
- Batas kecepatan atau kuota
- Jebakan umum
- Persyaratan kinerja

## Alur Kerja PRP

### Cara Kerja /generate-prp

Perintah mengikuti proses ini:

1. **Fase Penelitian**
   - Menganalisis basis kode Anda untuk menemukan pola
   - Mencari implementasi serupa
   - Mengidentifikasi konvensi yang harus diikuti

2. **Pengumpulan Dokumentasi**
   - Mengambil dokumen API yang relevan
   - Menyertakan dokumentasi pustaka
   - Menambahkan masalah dan keanehan

3. **Pembuatan Blueprint**
   - Membuat rencana implementasi langkah demi langkah
   - Menyertakan gerbang validasi
   - Menambahkan persyaratan pengujian

4. **Pemeriksaan Kualitas**
   - Memberikan skor tingkat kepercayaan (1-10)
   - Memastikan semua konteks disertakan

### Cara Kerja /execute-prp

1. **Muat Konteks**: Membaca seluruh PRP
2. **Rencanakan**: Membuat daftar tugas terperinci menggunakan TodoWrite
3. **Eksekusi**: Mengimplementasikan setiap komponen
4. **Validasi**: Menjalankan pengujian dan pemeriksaan kode
5. **Iterasi**: Memperbaiki masalah yang ditemukan
6. **Selesai**: Memastikan semua persyaratan terpenuhi

Lihat `PRPs/EXAMPLE_multi_agent_prp.md` untuk contoh lengkap PRP yang dihasilkan.

## Menggunakan Contoh dengan Efektif

Folder `examples/` sangat penting untuk kesuksesan. Asisten AI pengkodean bekerja lebih baik ketika mereka dapat melihat pola yang harus diikuti.

### Yang Harus Disertakan dalam Contoh

1. **Pola Struktur Kode**
   - Cara Anda mengatur modul
   - Konvensi impor
   - Pola kelas/fungsi

2. **Pola Pengujian**
   - Struktur file pengujian
   - Pendekatan mocking
   - Gaya assertion

3. **Pola Integrasi**
   - Implementasi klien API
   - Koneksi basis data
   - Alur autentikasi

4. **Pola CLI**
   - Parsing argumen
   - Pemformatan output
   - Penanganan error

### Contoh Struktur

```
examples/
├── README.md           # Menjelaskan apa yang ditunjukkan setiap contoh
├── cli.py             # Pola implementasi CLI
├── agent/             # Pola arsitektur agen
│   ├── agent.py      # Pola pembuatan agen
│   ├── tools.py      # Pola implementasi alat
│   └── providers.py  # Pola multi-penyedia
└── tests/            # Pola pengujian
    ├── test_agent.py # Pola pengujian unit
    └── conftest.py   # Konfigurasi Pytest
```

## Praktik Terbaik

### 1. Jelas dalam INITIAL.md
- Jangan berasumsi AI tahu preferensi Anda
- Sertakan persyaratan dan batasan spesifik
- Sering merujuk contoh

### 2. Berikan Contoh yang Komprehensif
- Semakin banyak contoh = implementasi yang lebih baik
- Tunjukkan apa yang harus dilakukan DAN yang tidak boleh dilakukan
- Sertakan pola penanganan error

### 3. Gunakan Gerbang Validasi
- PRP menyertakan perintah pengujian yang harus berhasil
- AI akan mengulang sampai semua validasi berhasil
- Ini memastikan kode berfungsi pada percobaan pertama

### 4. Manfaatkan Dokumentasi
- Sertakan dokumen API resmi
- Tambahkan sumber daya server MCP
- Rujuk bagian dokumentasi tertentu

### 5. Sesuaikan GEMINI_id.md
- Tambahkan konvensi Anda
- Sertakan aturan spesifik proyek
- Definisikan standar pengkodean

## Sumber Daya

- [Dokumentasi Gemini Code](https://docs.anthropic.com/en/docs/claude-code)
- [Praktik Terbaik Rekayasa Konteks](https://www.philschmid.de/context-engineering)
