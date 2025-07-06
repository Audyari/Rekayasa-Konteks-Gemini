### 🔄 Kesadaran & Konteks Proyek
- **Selalu baca `PLANNING.md`** di awal percakapan baru untuk memahami arsitektur, tujuan, gaya, dan batasan proyek.
- **Periksa `TASK.md`** sebelum memulai tugas baru. Jika tugas belum tercantum, tambahkan dengan deskripsi singkat dan tanggal hari ini.
- **Gunakan konvensi penamaan, struktur file, dan pola arsitektur yang konsisten** seperti yang dijelaskan di `PLANNING.md`.
- **Gunakan venv_linux** (lingkungan virtual) setiap kali menjalankan perintah Python, termasuk untuk pengujian unit.

### 🧱 Struktur & Modularitas Kode
- **Jangan pernah membuat file lebih dari 500 baris kode.** Jika sebuah file mendekati batas ini, lakukan refaktor dengan memisahkannya menjadi modul atau file bantuan.
- **Atur kode ke dalam modul yang terpisah dengan jelas**, dikelompokkan berdasarkan fitur atau tanggung jawab.
  Untuk agen, tampilannya seperti ini:
    - `agent.py` - Definisi agen utama dan logika eksekusi
    - `tools.py` - Fungsi-fungsi alat yang digunakan agen
    - `prompts.py` - Prompt sistem
- **Gunakan impor yang jelas dan konsisten** (lebih disukai impor relatif dalam paket).
- **Gunakan python_dotenv dan load_env()** untuk variabel lingkungan.

### 🧪 Pengujian & Keandalan
- **Selalu buat pengujian unit Pytest untuk fitur baru** (fungsi, kelas, rute, dll.).
- **Setelah memperbarui logika apa pun**, periksa apakah pengujian unit yang ada perlu diperbarui. Jika ya, lakukan.
- **Pengujian harus berada di folder `/tests`** yang mencerminkan struktur aplikasi utama.
  - Sertakan setidaknya:
    - 1 pengujian untuk penggunaan yang diharapkan
    - 1 kasus tepi (edge case)
    - 1 kasus kegagalan

### ✅ Penyelesaian Tugas
- **Tandai tugas yang selesai di `TASK.md`** segera setelah menyelesaikannya.
- Tambahkan sub-tugas atau TODO baru yang ditemukan selama pengembangan ke `TASK.md` di bagian "Ditemukan Selama Bekerja".

### 📎 Gaya & Konvensi
- **Gunakan Python** sebagai bahasa utama.
- **Ikuti PEP8**, gunakan type hints, dan format dengan `black`.
- **Gunakan `pydantic` untuk validasi data**.
- Gunakan `FastAPI` untuk API dan `SQLAlchemy` atau `SQLModel` untuk ORM jika diperlukan.
- Tulis **docstring untuk setiap fungsi** menggunakan gaya Google:
  ```python
  def contoh():
      """
      Ringkasan singkat.

      Args:
          parameter1 (tipe): Deskripsi.

      Returns:
          tipe: Deskripsi.
      """
  ```

### 📚 Dokumentasi & Kemudahan Pemahaman
- **Perbarui `README.md`** ketika fitur baru ditambahkan, dependensi berubah, atau langkah penyiapan dimodifikasi.
- **Beri komentar pada kode yang tidak jelas** dan pastikan semuanya dapat dipahami oleh pengembang tingkat menengah.
- Saat menulis logika yang kompleks, **tambahkan komentar sebaris `# Alasan:`** yang menjelaskan mengapa, bukan hanya apa.

### 🧠 Aturan Perilaku AI
- **Jangan pernah berasumsi tentang konteks yang hilang. Ajukan pertanyaan jika tidak yakin.**
- **Jangan pernah mengarang perpustakaan atau fungsi** – gunakan hanya paket Python yang dikenal dan terverifikasi.
- **Selalu konfirmasi jalur file dan nama modul** ada sebelum merujuknya dalam kode atau pengujian.
- **Jangan pernah menghapus atau menimpa kode yang ada** kecuali secara eksplisit diperintahkan atau jika bagian dari tugas dari `TASK.md`.
