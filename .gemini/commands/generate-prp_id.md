# Buat PRP

## File fitur: $ARGUMENTS

Buat PRP lengkap untuk implementasi fitur umum dengan penelitian menyeluruh. Pastikan konteks diteruskan ke agen AI untuk memungkinkan validasi mandiri dan penyempurnaan berulang. Baca terlebih dahulu file fitur untuk memahami apa yang perlu dibuat, bagaimana contoh yang diberikan membantu, dan pertimbangan lainnya.

Agen AI hanya mendapatkan konteks yang Anda lampirkan ke PRP dan data pelatihan. Asumsikan agen AI memiliki akses ke basis kode dan pemutakhiran pengetahuan yang sama dengan Anda, jadi penting untuk menyertakan atau merujuk temuan penelitian Anda dalam PRP. Agen memiliki kemampuan Pencarian Web, jadi sertakan URL dokumentasi dan contoh.

## Proses Penelitian

1. **Analisis Basis Kode**
   - Cari fitur/pola serupa dalam basis kode
   - Identifikasi file yang akan dirujuk dalam PRP
   - Catat konvensi yang ada untuk diikuti
   - Periksa pola pengujian untuk pendekatan validasi

2. **Penelitian Eksternal**
   - Cari fitur/pola serupa secara online
   - Dokumentasi perpustakaan (sertakan URL spesifik)
   - Contoh implementasi (GitHub/StackOverflow/blog)
   - Praktik terbaik dan jebakan umum

3. **Klirifikasi Pengguna** (jika diperlukan)
   - Pola spesifik yang perlu dicermati dan di mana mencarinya?
   - Persyaratan integrasi dan di mana mencarinya?

## Pembuatan PRP

Menggunakan PRPs/templates/prp_base.md sebagai template:

### Konteks Penting yang Harus Disertakan dan Diteruskan ke Agen AI sebagai Bagian dari PRP
- **Dokumentasi**: URL dengan bagian spesifik
- **Contoh Kode**: Potongan kode nyata dari basis kode
- **Jebakan**: Keunikan perpustakaan, masalah versi
- **Pola**: Pendekatan yang ada untuk diikuti

### Cetak Biru Implementasi
- Mulai dengan pseudocode yang menunjukkan pendekatan
- Rujuk file nyata untuk pola
- Sertakan strategi penanganan kesalahan
- Daftar tugas yang harus diselesaikan untuk memenuhi PRP sesuai urutan yang harus diselesaikan

### Gerbang Validasi (Harus Dapat Dieksekusi) contoh untuk python
```bash
# Sintaks/Gaya
ruff check --fix && mypy .

# Pengujian Unit
uv run pytest tests/ -v
```

*** PENTING SETELAH ANDA SELESAI MENELITI DAN MENJELAJAHI BASIS KODE SEBELUM MENULIS PRP ***

*** ULTRATHINK TENTANG PRP DAN RENCANAKAN PENDEKATAN ANDA KEMUDIAN MULAI MENULIS PRP ***

## Output
Simpan sebagai: `PRPs/{nama-fitur}.md`

## Daftar Periksa Kualitas
- [ ] Semua konteks yang diperlukan disertakan
- [ ] Gerbang validasi dapat dieksekusi oleh AI
- [ ] Merujuk pada pola yang ada
- [ ] Jalan implementasi yang jelas
- [ ] Penanganan kesalahan didokumentasikan

Nilai PRP pada skala 1-10 (tingkat kepercayaan untuk berhasil dalam implementasi satu kali menggunakan kode gemini)

Ingat: Tujuannya adalah keberhasilan implementasi satu kali melalui konteks yang komprehensif.
