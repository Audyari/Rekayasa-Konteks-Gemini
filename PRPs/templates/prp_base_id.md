name: "Template Dasar PRP v2 - Kaya Konteks dengan Lingkaran Validasi"
description: |

## Tujuan
Template yang dioptimalkan untuk agen AI guna mengimplementasikan fitur dengan konteks yang cukup dan kemampuan validasi mandiri untuk mencapai kode yang berfungsi melalui penyempurnaan berulang.

## Prinsip Inti
1. **Konteks adalah Raja**: Sertakan SEMUA dokumentasi, contoh, dan peringatan yang diperlukan
2. **Lingkaran Validasi**: Sediakan tes/lint yang dapat dieksekusi yang dapat dijalankan dan diperbaiki oleh AI
3. **Padat Informasi**: Gunakan kata kunci dan pola dari basis kode
4. **Kesuksesan Bertahap**: Mulai dari yang sederhana, validasi, lalu tingkatkan
5. **Aturan Global**: Pastikan mengikuti semua aturan di GEMINI_id.md

---

## Tujuan
[Apa yang perlu dibangun - spesifik tentang keadaan akhir dan keinginan]

## Mengapa
- [Nilai bisnis dan dampak pengguna]
- [Integrasi dengan fitur yang ada]
- [Masalah yang dipecahkan dan untuk siapa]

## Apa
[Perilaku yang terlihat oleh pengguna dan persyaratan teknis]

### Kriteria Keberhasilan
- [ ] [Hasil spesifik yang dapat diukur]

## Semua Konteks yang Diperlukan

### Dokumentasi & Referensi (daftar semua konteks yang diperlukan untuk mengimplementasikan fitur)
```yaml
# WAJIB DIBACA - Sertakan ini dalam konteks jendela Anda
- url: [URL dokumen API resmi]
  why: [Bagian/metode spesifik yang Anda perlukan]
  
- file: [path/ke/contoh.py]
  why: [Pola yang harus diikuti, jebakan yang harus dihindari]
  
- doc: [URL dokumentasi perpustakaan] 
  section: [Bagian spesifik tentang masalah umum]
  critical: [Wawasan penting yang mencegah kesalahan umum]

- docfile: [PRPs/ai_docs/file.md]
  why: [dokumen yang telah disisipkan pengguna ke dalam proyek]
```

### Struktur Basis Kode Saat Ini (jalankan `tree` di direktori root proyek) untuk mendapatkan gambaran umum basis kode
```bash

```

### Struktur Basis Kode yang Diinginkan dengan File yang Akan Ditambahkan dan Tanggung Jawab File
```bash

```

### Masalah & Keunikan yang Diketahui dari Basis Kode & Keunikan Perpustakaan
```python
# KRITIS: [Nama perpustakaan] memerlukan [pengaturan spesifik]
# Contoh: FastAPI memerlukan fungsi async untuk endpoint
# Contoh: ORM ini tidak mendukung penyisipan batch lebih dari 1000 catatan
# Contoh: Kami menggunakan pydantic v2 dan
```

## Cetak Biru Implementasi

### Model data dan struktur

Buat model data inti, kami memastikan keamanan tipe dan konsistensi.
```python
Contoh: 
 - model orm
 - model pydantic
 - skema pydantic
 - validator pydantic
```

### Daftar tugas yang harus diselesaikan untuk memenuhi PRP sesuai urutan yang harus diselesaikan

```yaml
Tugas 1:
MODIFIKASI src/modul_yang_ada.py:
  - CARI pola: "class ImplementasiLama"
  - SISIPKAN setelah baris yang berisi "def __init__"
  - JAGA tanda tangan metode yang ada

BUAT src/fitur_baru.py:
  - MIRROR pola dari: src/fitur_serupa.py
  - MODIFIKASI nama kelas dan logika inti
  - JAGA pola penanganan error tetap sama

...(...)

Tugas N:
...
```

### Pseudocode per tugas

```python
# Contoh fungsi yang akan diimplementasikan
def contoh_fitur(input_data: dict) -> dict:
    """
    Deskripsi singkat tentang apa yang dilakukan fungsi ini.
    
    Args:
        input_data: Kamus berisi data input
        
    Returns:
        Kamus berisi hasil pemrosesan
        
    Raises:
        ValueError: Jika input tidak valid
    """
    # Validasi input
    if not input_data.get('wajib'):
        raise ValueError("Field 'wajib' harus diisi")
        
    # Logika bisnis
    hasil = process_data(input_data)
    
    # Validasi output
    if not is_valid(hasil):
        raise RuntimeError("Hasil tidak valid")
        
    return hasil
```

### Titik Integrasi
```yaml
LINGKUNGAN:
  - tambahkan ke: .env
  - vars: |
      # Konfigurasi koneksi database
      DB_HOST=localhost
      DB_PORT=5432
      
      # Kredensial API eksternal
      API_KEY=rahasia
      
KONFIGURASI:
  - File konfigurasi: config/settings.py
  - Variabel lingkungan: .env
  
KETERGANTUNGAN:
  - Perbarui requirements.txt dengan dependensi baru
  - Tambahkan dependensi pengembangan jika diperlukan
```

## Lingkaran Validasi

### Tingkat 1: Sintaks & Gaya
```bash
# Jalankan ini PERTAMA - perbaiki semua error sebelum melanjutkan
ruff check . --fix              # Perbaiki masalah gaya secara otomatis
mypy .                          # Pemeriksaan tipe
black .                         # Format kode otomatis
```

### Tingkat 2: Pengujian Unit
```bash
# Jalankan pengujian unit
pytest tests/unit/

# Jalankan pengujian dengan cakupan kode
pytest --cov=src tests/unit/
```

### Tingkat 3: Pengujian Integrasi
```bash
# Jalankan pengujian integrasi
pytest tests/integration/

# Jalankan pengujian dengan laporan cakupan
pytest --cov=src --cov-append tests/integration/
```

### Tingkat 4: Pemeriksaan Kualitas Kode
```bash
# Jalankan pemeriksa kualitas kode
flake8 .
bandit -r src/
```

## Contoh Pengujian

### Pengujian Unit Dasar
```python
def test_contoh_fitur_sukses():
    """Uji kasus sukses untuk contoh_fitur"""
    input_data = {"wajib": "nilai", "opsional": 123}
    hasil = contoh_fitur(input_data)
    assert "hasil" in hasil
    assert hasil["status"] == "sukses"

def test_contoh_fitur_gagal():
    """Uji validasi input yang gagal"""
    with pytest.raises(ValueError):
        contoh_fitur({})  # Input tidak valid
```

### Pengujian Integrasi
```python
@mock.patch('modul.eksternal.fungsi')
def test_integrasi_dengan_layanan_eksternal(mock_eksternal):
    """Uji integrasi dengan layanan eksternal"""
    # Setup mock
    mock_eksternal.return_value = {"status": "ok"}
    
    # Eksekusi
    hasil = layanan_kita()
    
    # Verifikasi
    assert hasil == "sukses"
    mock_eksternal.assert_called_once()
```

### Pengujian Performa
```python
def test_performa_fitur_kritis():
    """Uji waktu eksekusi fungsi kritis"""
    import timeit
    
    waktu = timeit.timeit(
        'fungsi_kritis("input")',
        setup='from modul.utama import fungsi_kritis',
        number=1000
    )
    
    assert waktu < 1.0  # Harus selesai di bawah 1 detik untuk 1000 iterasi
```

## Langkah Selanjutnya

1. **Tinjauan Kode**: Minta rekan tim untuk meninjau implementasi
2. **Uji Penerimaan Pengguna**: Validasi dengan pengguna nyata
3. **Dokumentasi**: Perbarui dokumentasi pengguna dan pengembang
4. **Pemantauan**: Pantau metrik kinerja di produksi
5. **Umpan Balik**: Kumpulkan umpan balik untuk iterasi berikutnya
