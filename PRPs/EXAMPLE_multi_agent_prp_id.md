name: "Sistem Multi-Agen: Agen Riset dengan Sub-Agen Draf Email"
description: |

## Tujuan
Membangun sistem multi-agen Pydantic AI di mana Agen Riset utama menggunakan API Brave Search dan memiliki Agen Draf Email (menggunakan API Gmail) sebagai alat. Ini menunjukkan pola agen-sebagai-alat dengan integrasi API eksternal.

## Prinsip Inti
1. **Konteks adalah Raja**: Sertakan SEMUA dokumentasi, contoh, dan peringatan yang diperlukan
2. **Lingkaran Validasi**: Sediakan tes/lint yang dapat dieksekusi yang dapat dijalankan dan diperbaiki oleh AI
3. **Padat Informasi**: Gunakan kata kunci dan pola dari basis kode
4. **Kesuksesan Bertahap**: Mulai dari yang sederhana, validasi, lalu tingkatkan

---

## Tujuan
Membuat sistem multi-agen siap produksi di mana pengguna dapat meneliti topik melalui CLI, dan Agen Riset dapat mendelegasikan tugas pembuatan draf email ke Agen Draf Email. Sistem harus mendukung banyak penyedia LLM dan menangani otentikasi API dengan aman.

## Mengapa
- **Nilai bisnis**: Mengotomatiskan alur kerja penelitian dan pembuatan draf email
- **Integrasi**: Menunjukkan pola multi-agen Pydantic AI tingkat lanjut
- **Masalah yang dipecahkan**: Mengurangi pekerjaan manual untuk komunikasi email berbasis penelitian

## Apa
Aplikasi berbasis CLI di mana:
- Pengguna memasukkan kueri penelitian
- Agen Riset mencari menggunakan API Brave
- Agen Riset dapat memanggil Agen Draf Email untuk membuat draf Gmail
- Hasilnya dikirim kembali ke pengguna secara real-time

### Kriteria Keberhasilan
- [ ] Agen Riset berhasil mencari melalui API Brave
- [ ] Agen Email membuat draf Gmail dengan otentikasi yang tepat
- [ ] Agen Riset dapat memanggil Agen Email sebagai alat
- [ ] CLI memberikan respons streaming dengan visibilitas alat
- [ ] Semua tes lolos dan kode memenuhi standar kualitas

## Semua Konteks yang Diperlukan

### Dokumentasi & Referensi
```yaml
# WAJIB DIBACA - Sertakan ini dalam konteks jendela Anda
- url: https://ai.pydantic.dev/agents/
  why: Pola pembuatan agen inti
  
- url: https://ai.pydantic.dev/multi-agent-applications/
  why: Pola sistem multi-agen, terutama agen-sebagai-alat
  
- url: https://developers.google.com/gmail/api/guides/sending
  why: Autentikasi API Gmail dan pembuatan draf
  
- url: https://api-dashboard.search.brave.com/app/documentation
  why: Titik akhir REST API Brave Search
  
- file: examples/agent/agent.py
  why: Pola untuk pembuatan agen, pendaftaran alat, dependensi
  
- file: examples/agent/providers.py
  why: Pola konfigurasi LLM multi-penyedia
  
- file: examples/cli.py
  why: Struktur CLI dengan respons streaming dan visibilitas alat

- url: https://github.com/googleworkspace/python-samples/blob/main/gmail/snippet/send%20mail/create_draft.py
  why: Contoh resmi pembuatan draf Gmail
```

### Struktur Basis Kode Saat Ini
```bash
.
├── examples/
│   ├── agent/
│   │   ├── agent.py
│   │   ├── providers.py
│   │   └── ...
│   └── cli.py
├── PRPs/
│   └── templates/
│       └── prp_base.md
├── INITIAL.md
├── GEMINI_id.md
└── requirements.txt
```

### Struktur Basis Kode yang Diinginkan dengan File yang Akan Ditambahkan
```bash
.
├── agents/
│   ├── __init__.py               # Inisialisasi paket
│   ├── research_agent.py         # Agen utama dengan Pencarian Brave
│   ├── email_agent.py           # Sub-agen dengan kemampuan Gmail
│   ├── providers.py             # Konfigurasi penyedia LLM
│   └── models.py                # Model Pydantic untuk validasi data
├── tools/
│   ├── __init__.py              # Inisialisasi paket
│   ├── brave_search.py          # Integrasi API Brave Search
│   └── gmail_tool.py            # Integrasi API Gmail
├── config/
│   ├── __init__.py              # Inisialisasi paket
│   └── settings.py              # Manajemen lingkungan dan konfigurasi
├── tests/
│   ├── __init__.py              # Inisialisasi paket
│   ├── test_research_agent.py   # Tes agen riset
│   ├── test_email_agent.py      # Tes agen email
│   ├── test_brave_search.py     # Tes alat pencarian Brave
│   ├── test_gmail_tool.py       # Tes alat Gmail
│   └── test_cli.py              # Tes CLI
├── cli.py                       # Antarmuka CLI
├── .env.example                 # Template variabel lingkungan
├── requirements.txt             # Dependensi yang diperbarui
├── README.md                    # Dokumentasi komprehensif
└── credentials/.gitkeep         # Direktori untuk kredensial Gmail
```

### Masalah & Keunikan yang Diketahui
```python
# KRITIS: Pydantic AI memerlukan async di seluruh kode - tidak ada fungsi sinkron dalam konteks async
# KRITIS: API Gmail memerlukan alur OAuth2 pada eksekusi pertama - credentials.json diperlukan
# KRITIS: API Brave memiliki batas kecepatan - 2000 permintaan/bulan di tier gratis
# KRITIS: Pola agen-sebagai-alat memerlukan penerusan ctx.usage untuk pelacakan token
# KRITIS: Draf Gmail memerlukan pengkodean base64 dengan format MIME yang tepat
# KRITIS: Selalu gunakan impor absolut untuk kode yang lebih bersih
# KRITIS: Simpan kredensial sensitif di .env, jangan pernah mengunggahnya ke repositori
```

## Cetak Biru Implementasi

### Model data dan struktur

```python
# models.py - Struktur data inti
from pydantic import BaseModel, Field
from typing import List, Optional
from datetime import datetime

class ResearchQuery(BaseModel):
    query: str = Field(..., description="Topik penelitian yang akan diselidiki")
    max_results: int = Field(10, ge=1, le=50)
    include_summary: bool = Field(True)

class BraveSearchResult(BaseModel):
    title: str
    url: str
    description: str
    score: float = Field(0.0, ge=0.0, le=1.0)

class EmailDraft(BaseModel):
    to: List[str] = Field(..., min_items=1)
    subject: str = Field(..., min_length=1)
    body: str = Field(..., min_length=1)
    cc: Optional[List[str]] = None
    bcc: Optional[List[str]] = None

class ResearchEmailRequest(BaseModel):
    research_query: str
    email_context: str = Field(..., description="Konteks untuk pembuatan email")
    recipient_email: str
```

### Daftar tugas yang harus diselesaikan

```yaml
Tugas 1: Menyiapkan Konfigurasi dan Lingkungan
BUAT config/settings.py:
  - POLA: Gunakan pydantic-settings seperti contoh yang menggunakan os.getenv
  - Muat variabel lingkungan dengan nilai default
  - Validasi kunci API yang diperlukan ada

BUAT .env.example:
  - Sertakan semua variabel lingkungan yang diperlukan dengan deskripsi
  - Ikuti pola dari examples/README.md

Tugas 2: Implementasikan Alat Pencarian Brave
BUAT tools/brave_search.py:
  - POLA: Fungsi async seperti examples/agent/tools.py
  - Klien REST sederhana menggunakan httpx (sudah ada di requirements)
  - Tangani batas kecepatan dan kesalahan dengan baik
  - Kembalikan model BraveSearchResult yang terstruktur

Tugas 3: Implementasikan Alat Gmail
BUAT tools/gmail_tool.py:
  - POLA: Ikuti alur OAuth2 dari quickstart Gmail
  - Simpan token.json di direktori credentials/
  - Buat draf dengan pengkodean MIME yang tepat
  - Tangani penyegaran otentikasi secara otomatis

Tugas 4: Buat Agen Draf Email
BUAT agents/email_agent.py:
  - POLA: Ikuti struktur examples/agent/agent.py
  - Gunakan Agent dengan pola deps_type
  - Daftarkan gmail_tool sebagai @agent.tool
  - Kembalikan model EmailDraft

Tugas 5: Buat Agen Riset
BUAT agents/research_agent.py:
  - POLA: Pola multi-agen dari dokumentasi Pydantic AI
  - Daftarkan brave_search sebagai alat
  - Daftarkan email_agent.run() sebagai alat
  - Gunakan RunContext untuk dependency injection

Tugas 6: Implementasikan Antarmuka CLI
BUAT cli.py:
  - POLA: Ikuti pola streaming examples/cli.py
  - Output berwarna dengan visibilitas alat
  - Tangani async dengan benar menggunakan asyncio.run()
  - Manajemen sesi untuk konteks percakapan

Tugas 7: Tambahkan Tes Komprehensif
BUAT tests/:
  - POLA: Cerminkan struktur tes contoh
  - Mock panggilan API eksternal
  - Uji jalur normal, kasus tepi, kesalahan
  - Pastikan cakupan minimal 80%

Tugas 8: Buat Dokumentasi
BUAT README.md:
  - POLA: Ikuti struktur examples/README.md
  - Sertakan pengaturan, instalasi, penggunaan
  - Langkah konfigurasi kunci API
  - Diagram arsitektur
```

### Pseudocode per tugas

```python
# Tugas 2: Alat Pencarian Brave
async def search_brave(query: str, api_key: str, count: int = 10) -> List[BraveSearchResult]:
    # POLA: Gunakan httpx seperti contoh yang menggunakan aiohttp
    async with httpx.AsyncClient() as client:
        headers = {"X-Subscription-Token": api_key}
        params = {"q": query, "count": count}
        
        # PERHATIAN: API Brave mengembalikan 401 jika kunci API tidak valid
        response = await client.get(
            "https://api.search.brave.com/res/v1/web/search",
            headers=headers,
            params=params,
            timeout=30.0  # KRITIS: Atur timeout untuk menghindari hang
        )
        
        # POLA: Penanganan error terstruktur
        if response.status_code != 200:
            raise BraveAPIError(f"API mengembalikan kode {response.status_code}")
        
        # Parsing dan validasi dengan Pydantic
        data = response.json()
        return [BraveSearchResult(**result) for result in data.get("web", {}).get("results", [])]

# Tugas 5: Agen Riset dengan Agen Email sebagai Alat
@research_agent.tool
async def create_email_draft(
    ctx: RunContext[AgentDependencies],
    recipient: str,
    subject: str,
    context: str
) -> str:
    """Buat draf email berdasarkan konteks penelitian."""
    # KRITIS: Teruskan usage untuk pelacakan token
    result = await email_agent.run(
        f"Buat email untuk {recipient} tentang: {context}",
        deps=EmailAgentDeps(subject=subject),
        usage=ctx.usage  # POLA dari dokumentasi multi-agen
    )
    
    return f"Draf dibuat dengan ID: {result.data}"
```

### Titik Integrasi
```yaml
LINGKUNGAN:
  - tambahkan ke: .env
  - vars: |
      # Konfigurasi LLM
      LLM_PROVIDER=openai
      LLM_API_KEY=sk-...
      LLM_MODEL=gpt-4
      
      # Brave Search
      BRAVE_API_KEY=BSA...
      
      # Gmail (path ke credentials.json)
      GMAIL_CREDENTIALS_PATH=./credentials/credentials.json
      
KONFIGURASI:
  - OAuth Gmail: Eksekusi pertama akan membuka browser untuk otorisasi
  - Penyimpanan token: ./credentials/token.json (dibuat otomatis)
  
KETERGANTUNGAN:
  - Perbarui requirements.txt dengan:
    - google-api-python-client
    - google-auth-httplib2
    - google-auth-oauthlib
```

## Lingkaran Validasi

### Tingkat 1: Sintaks & Gaya
```bash
# Jalankan ini PERTAMA - perbaiki semua error sebelum melanjutkan
ruff check . --fix              # Perbaiki masalah gaya secara otomatis
mypy .                          # Pemeriksaan tipe
```
