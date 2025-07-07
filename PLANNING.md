# PLANNING.md

## Arsitektur Proyek
- **Tujuan Utama:** Membangun aplikasi/sistem yang berinteraksi dengan Redis untuk tujuan caching, antrian, atau pub/sub.
- **Teknologi Utama:** Python, Redis.
- **Struktur Kode:** Mengikuti pedoman modularitas dari `GEMINI_id.md` (misalnya, pemisahan agen, tools, prompts jika relevan).
- **Konvensi Penamaan:** Konsisten dengan PEP8.

## Tujuan Proyek
- Memahami dan mengimplementasikan fitur-fitur Redis (misalnya, caching, pub/sub, struktur data).
- Mengoptimalkan penggunaan Redis dalam aplikasi.
- Memastikan keandalan dan performa sistem.

## Gaya & Batasan
- **Bahasa Pemrograman:** Python.
- **Gaya Kode:** PEP8, type hints, diformat dengan `black`.
- **Validasi Data:** Menggunakan `pydantic` jika diperlukan.
- **Pengujian:** Pytest untuk unit test, mencakup kasus penggunaan, edge case, dan kegagalan.
- **Dokumentasi:** Docstring untuk setiap fungsi, update `README.md` secara berkala.
- **Ukuran File:** Maksimal 500 baris per file.
