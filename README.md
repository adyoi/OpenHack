# OpenHack

Template workspace opencode untuk keamanan siber / penetration testing — berisi 4 agen khusus (Hunt, Code, Hack, Chat). Bukan project aplikasi: setiap project yang dikerjakan diletakkan di dalam `project/`.

## Agen

| Agen | Peran | Akses |
|---|---|---|
| **Hunt** (`/hunt`, default) | Recon & vulnerability hunting: footprint target, enumerate layanan, analisis CVE, laporan risiko | `bash` (mayoritas konfirmasi), `websearch`, `webfetch` |
| **Code** (`/code`) | Code review & exploit development: audit OWASP Top 10, trace data flow, PoC | `bash` + `edit` (konfirmasi) |
| **Hack** (`/hack`) | Exploitation & post-exploitation: validasi temuan, privilege escalation, lateral movement, operasi C2 | `bash` + `edit` (konfirmasi) |
| **Chat** (`/chat`) | Tanya jawab keamanan siber — tanpa akses tool | tidak ada (`bash`/`edit` deny) |

## Aturan Penggunaan

- **Hanya serang target dengan otorisasi eksplisit dari pemilik.** Tidak ada pengecualian.
- Prefer teknik non-destruktif; konfirmasi sebelum tindakan berisiko.
- Setiap temuan dilaporkan dengan: target, temuan, risk rating (Critical/High/Medium/Low), bukti, remediasi.

## Cara Penggunaan

![Alur penggunaan OpenHack](assets/usage-flow.png)

1. **Home** — buka opencode.
2. **Add Project** — tambahkan folder repo ini sebagai project.
3. **New Session** — buat sesi kerja baru.
4. **Pilih Agent** — pilih agen sesuai kebutuhan (via TUI atau slash command):
   - `/hunt` untuk recon & vulnerability hunting (default)
   - `/code` untuk code review & exploit development
   - `/hack` untuk exploitation & post-exploitation
   - `/chat` untuk tanya jawab keamanan

> **Workspace:** semua PoC, script, dan file kerja dibuat otomatis di dalam
> folder `project/` (subfolder baru per target/engagement) agar root repo
> tetap bersih.

## Instalasi

**Prasyarat:** [Node.js](https://nodejs.org) LTS sudah terpasang (untuk cara via npm).

### Windows

```powershell
# via npm
npm install -g opencode-ai

# atau via Chocolatey
choco install opencode

# atau via Scoop
scoop install opencode
```

### Linux

```bash
# via install script resmi (direkomendasikan)
curl -fsSL https://opencode.ai/install | bash

# atau via npm
npm install -g opencode-ai

# atau via package manager (contoh Arch Linux)
sudo pacman -S opencode
```

### macOS

```bash
# via Homebrew (direkomendasikan)
brew install anomalyco/tap/opencode

# atau via npm
npm install -g opencode-ai
```

### Verifikasi & Clone

```powershell
# 1. Verifikasi instalasi
opencode --version

# 2. Clone repo (adyoi/OpenHack)
git clone https://github.com/adyoi/OpenHack.git
cd OpenHack
```

> Setelah install, buka ulang terminal agar perintah `opencode` masuk ke PATH.
> Saat pertama kali dijalankan, opencode akan meminta koneksi ke provider
> model (Anthropic, OpenAI, Google, atau model lokal).

## Memulai

```powershell
# Jalankan opencode dari root project
opencode

# Setiap session baru bekerja di dalam project/ (sub-project default)
# Pindah agen: gunakan slash command di TUI opencode (/hunt, /code, /hack, /chat),
# atau atur default_agent di opencode.json
```

## Struktur

```
OpenHack/
├── opencode.json              # config utama (default agent, username, permission)
├── README.md
├── assets/                    # ilustrasi & aset dokumentasi
│   └── usage-flow.png         # alur penggunaan (Home -> Add Project -> New Session -> Pilih Agent)
├── .opencode/                 # isi repo - definisi agen & command
│   ├── agent/                 # definisi 4 agen (hunt, code, hack, chat)
│   └── command/               # slash command: /hunt, /chat, /code, /hack, /recon
└── project/                   # sub-project default - isinya TIDAK masuk repo
    └── .gitkeep
```

## Catatan

- Config opencode **tidak hot-reload**: setelah mengubah `opencode.json`, definisi agen, skill, atau plugin — restart opencode agar berlaku.
- `project/` adalah tempat kerja per-user; isinya tidak dicantumkan di repo (lihat `.gitignore`). Tooling internal seperti C2 framework dan cryptovault dipindah ke sini setelah selesai dikembangkan.
- `node_modules` tidak disimpan; regenerasi via `npm install` di `.opencode/` jika perlu mengembangkan plugin.

## Kontributor

- [opencode](https://opencode.ai) — AI coding agent open source yang menjadi basis dari template ini

## Lisensi

[MIT License](https://opensource.org/licenses/MIT) — bebas digunakan, dimodifikasi, dan didistribusikan dengan tetap menyertakan pemberitahuan hak cipta asli.
