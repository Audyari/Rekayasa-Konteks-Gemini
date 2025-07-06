## FITUR:

- Agen Pydantic AI yang memiliki agen Pydantic AI lain sebagai alat.
- Agen Riset untuk agen utama dan kemudian agen Draf Email untuk sub-agen.
- CLI untuk berinteraksi dengan agen.
- Gmail untuk agen draf email, API Brave untuk agen riset.

## CONTOH:

Di folder `examples/`, terdapat README untuk Anda baca guna memahami contoh tersebut dan juga cara membuat README Anda sendiri saat membuat dokumentasi untuk fitur di atas.

- `examples/cli.py` - gunakan ini sebagai template untuk membuat CLI
- `examples/agent/` - baca semua file di sini untuk memahami praktik terbaik dalam membuat agen Pydantic AI yang mendukung berbagai penyedia dan LLM, menangani ketergantungan agen, dan menambahkan alat ke agen.

Jangan menyalin langsung contoh-contoh ini, karena ini untuk proyek yang sama sekali berbeda. Tapi gunakan ini sebagai inspirasi dan untuk praktik terbaik.

## DOKUMENTASI:

Dokumentasi Pydantic AI: https://ai.pydantic.dev/

## PERTIMBANGAN LAINNYA:

- Sertakan file .env.example, README dengan petunjuk penyiapan termasuk cara mengkonfigurasi Gmail dan Brave.
- Sertakan struktur proyek dalam README.
- Lingkungan virtual sudah disiapkan dengan dependensi yang diperlukan.
- Gunakan python_dotenv dan load_env() untuk variabel lingkungan
