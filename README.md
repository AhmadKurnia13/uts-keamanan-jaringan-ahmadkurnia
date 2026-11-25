Repo ini berisi bukti pengerjaan UTS Praktik Keamanan Jaringan: jawaban lengkap
Kasus 9, screenshot setiap langkah, dan source lab Docker untuk mengulang seluruh
serangan. **Semua serangan hanya boleh dijalankan di lingkungan lab lokal.**
Jangan memindai atau menyerang host di luar lab.

## Isi repo

```
lab-network-attack/
├── README.md                              ← file ini (penjelasan umum)
├── jawaban.md                             ← jawaban UTS Kasus 9: hitungan kasus,
│                                            7 tugas, command, bukti, penjelasan
├── ss/                                    ← 30 screenshot bukti (tugas 1–7)
│   └── tugas 1/ … tugas 7/
└── 01-sumber-lab/                         ← source lab
    ├── README.md                          ← cara build image dan menjalankan lab
    ├── setup.sh                           ← setup image otomatis
    ├── images/
    │   ├── uts-openssl/Dockerfile         ← image untuk Pertemuan 2 (OpenSSL)
    │   ├── uts-kali-tools/Dockerfile      ← image untuk Pertemuan 3–7 (hping3, dig,
    │   │                                   tcpdump, scapy, aircrack-ng, arpspoof)
    │   └── uts-dnsmasq/Dockerfile         ← image untuk Pertemuan 7 (resolver DNS lab)
    ├── b/
    │   ├── b1-compose/docker-compose.yml  ← Tugas 1: jaringan internal (target + attacker)
    │   ├── b3-syn-flood/docker-compose.yml← Tugas 6: SYN flood
    │   └── b4-dns-exfil/docker-compose.yml← Tugas 7: DNS exfiltration
    ├── kasus/
    │   ├── k5-scapy/kirim_icmp.py         ← skrip ICMP dengan Scapy (Tugas 5)
    │   └── k9-dns-detect/analisis_dns.py  ← skrip deteksi DNS exfiltration (Tugas 7)
    └── samples/                           ← panduan & checklist pembuatan capture
```

**Yang sengaja tidak ikut repo:**

- `handshake-kN.cap` dan `wordlist-kN.txt` — file contoh **disediakan penguji**
  dan masuk `.gitignore`, jadi hasil clone tidak bisa menjalankan Tugas 4 tanpa
  kedua file itu.
- `02-dokumen/` (lembar soal & rubrik) — berkas ujian, tidak dipublikasikan di
  repo publik. Materi pertemuan 1–7 lengkap ada di repositori mata kuliah:
  <https://github.com/yastiaisyah/Network-Security-Course-Bank>

## Urutan pemakaian

1. **Baca** `jawaban.md` — berisi kasus (NIM → jumlah digit → mod 10), urutan
   langkah, command siap pakai, screenshot bukti, dan penjelasan tiap tugas.
2. **Siapkan image** dari `01-sumber-lab`. Semua lab memakai jaringan
   `internal: true` (tanpa akses internet), sehingga paket harus sudah ada di
   image sebelum lab dijalankan:
   ```bash
   cd 01-sumber-lab
   docker build -t uts-openssl images/uts-openssl
   docker build -t uts-kali-tools images/uts-kali-tools
   docker build -t uts-dnsmasq images/uts-dnsmasq
   docker pull alpine:3.20 && docker pull nginx:alpine
   ```
   Atau jalankan `bash setup.sh build`.
3. **Tentukan kasus** dari NIM: jumlahkan seluruh digit, ambil sisa bagi 10, dan
   sisa 0 berarti Kasus 10. Contoh NIM 19552011024: jumlah digit 30, sisa 0,
   maka Kasus 10. (Jawaban di repo ini = **Kasus 9**, NIM 24552011027 → 29 → 9.)
4. **Kerjakan kasus** mengikuti lembar perintah per kasus yang diedarkan dosen
   untuk bagian kasus Anda. Setiap kasus mencakup tujuh tugas (Pertemuan 1
   sampai 7) dengan bobot sama.
5. **Lampirkan** jawaban, output terminal, dan bukti setiap tugas dalam satu
   berkas `jawaban.md`, di awal ditulis jumlah digit NIM, sisa bagi, dan nomor
   kasus.

## Catatan di mesin ini

- Shell default adalah **fish** — semua perintah di `jawaban.md` ber sintaks
  bash, jadi jalankan `bash` dulu sebelum menyalin, atau pakai script.
- Plugin `docker compose` tidak terpasang; pakai **`docker-compose`** (tanda
  hubung). Kalau di mesin lain pluginnya ada, ganti perintahnya jadi
  `docker compose` — parameter sama persis.

```

Kalau dibandingin dari dua repo referensi itu, punya **Dafa** udah simpel tapi belum ada `README.md` dan *About*-nya masih kosong[cite: 78], sedangkan punya **Andrian** udah rapi banget dengan `README.md` dan `.gitignore`, cuma bagian *About* & *Topics*-nya juga masih kosong dan file `samples` miliknya ikut ke-blok `.gitignore`[cite: 79, 81].

Supaya repo kamu **lebih rapi, kelihatan profesional, dan seragam** dengan gaya repo kamu sebelumnya (`uts-pemweb1-ahmadkurnia`)[cite: 77], kita gabungin semua keunggulannya: pakai **struktur lengkap (`jawaban.md` + `01-sumber-lab/samples`)**, **`.gitignore` pintar** (membuang file *private key* & log sementara tanpa memblokir `samples/`), **`README.md` lengkap ber-badge**, plus bagian **About & Topics** yang terisi penuh.

---

## 1. Pengaturan Repository Baru, About, & Topics (di GitHub)

Saat bikin repository baru di `[github.com/new](https://github.com/new)` (klik tombol hijau **New** di profil kamu)[cite: 77]:

| Bagian | Isi yang Direkomendasikan (Langsung Copy-Paste) |
| :--- | :--- |
| **Repository name** | `uts-keamanan-jaringan-ahmadkurnia` *(atau `uts-network-security-k8`)* |
| **Visibility** | `Public` |
| **Initialize repo** | **Jangan centang** *Add a README*, *.gitignore*, atau *License* (karena kita push dari lokal biar tidak bentrok) |
| **About — Description** | `UTS Keamanan Jaringan (24552011297 - Ahmad Kurnia - TIF RP 24E CNS): Praktik Infrastruktur & Network Attacks Pertemuan 1–7 (Kasus 8) berbasis Docker terisolasi.` |
| **About — Website** | `[https://ahmadkurnia-portofolio.lovable.app](https://ahmadkurnia-portofolio.lovable.app)` *(opsional, bisa pakai link portofolio kamu)* |
| **About — Topics** | `network-security` `docker` `cybersecurity` `docker-compose` `openssl` `scapy` `wireshark` `aircrack-ng` `dns-exfiltration` `utb` |

*(Cara isi **About & Topics**: setelah repo jadi, klik ikon **gerigi / Settings** di sebelah tulisan **About** di sisi kanan halaman repo → tempel Description, Website, dan ketik Topics satu per satu → klik **Save changes**.)*

---

## 2. Siapkan File `.gitignore` (Wajib Biar Repo Bersih & Aman)

Di folder `01-sumber-lab/` kamu sekarang ada file sisa praktikum (`key-k8.pem`, `cert-k8.pem`, `laporan-k8.enc`, `hasil-k8.txt`, `dns-k8.log`)[cite: 76]. Supaya *private key* dan file sementara itu tidak ikut ter-upload, tapi folder **`samples/` tetap ikut ter-push**, buat file baru bernama **`.gitignore`** di root folder `UTS-Network-Security` (sejajar dengan `jawaban.md`) lalu isi dengan ini:

```gitignore
# Artefak sementara & private key hasil praktikum Tugas 2 & Tugas 7
01-sumber-lab/*.pem
01-sumber-lab/*.key
01-sumber-lab/*.enc
01-sumber-lab/laporan-k*.txt
01-sumber-lab/hasil-k*.txt
01-sumber-lab/dns-k*.log

# Abaikan folder duplikat bawaan yang tidak terpakai
01-source-lab/

# File sementara OS, Editor, & Python
.DS_Store
Thumbs.db
__pycache__/
*.pyc
.vscode/
```

> **Kenapa ini lebih bagus?** File sensitif/sementara seperti `key-k8.pem` tidak bocor ke publik, tapi seluruh isi **`01-sumber-lab/samples/`** (termasuk `handshake-k8.cap` & `wordlist-k8.txt`) tetap aman ter-push ke GitHub!

---

## 3. Ganti Isi `README.md` Utama (Versi Sempurna)

Buka file **`README.md`** di root folder `UTS-Network-Security` (sejajar dengan `jawaban.md`)[cite: 76], hapus isi lamanya, lalu *copy-paste* template modern di bawah ini:

````markdown
# 🛡️ UTS Praktik Keamanan Jaringan — Infrastruktur & Network Attacks (Pertemuan 1–7)

![Docker](https://img.shields.io/badge/Docker-2496ED?style=for-the-badge&logo=docker&logoColor=white)
![Kali Linux](https://img.shields.io/badge/Kali_Tools-557C94?style=for-the-badge&logo=kalilinux&logoColor=white)
![Python](https://img.shields.io/badge/Python_Scapy-3776AB?style=for-the-badge&logo=python&logoColor=white)
![OpenSSL](https://img.shields.io/badge/OpenSSL-721412?style=for-the-badge&logo=openssl&logoColor=white)
![Case](https://img.shields.io/badge/Studi_Kasus-Kasus_8_(k8)-1E3A5F?style=for-the-badge)

```text
 _   _ _____ _______        _____  ____  _  __  ____  _____ ____ 
| \ | | ____|_   _\ \      / / _ \|  _ \| |/ / / ___|| ____/ ___|
|  \| |  _|   | |  \ \ /\ / / | | | |_) | ' /  \___ \|  _|| |    
| |\  | |___  | |   \ V  V /| |_| |  _ <| . \   ___) | |__| |___ 
|_| \_|_____| |_|    \_/\_/  \___/|_| \_\_|\_\ |____/|_____\____|

        UTS KEAMANAN JARINGAN — UNIVERSITAS TEKNOLOGI BANDUNG
           Ahmad Kurnia | 24552011297 | TIF RP 24E CNS
```

Repositori ini berisi dokumentasi lengkap, source lab Docker, folder `samples/`, dan laporan jawaban (`jawaban.md`) untuk **Ujian Tengah Semester (UTS) Mata Kuliah Keamanan Jaringan (Pertemuan 1–7)** pada **Program Studi Teknik Informatika, Universitas Teknologi Bandung (UTB)**.

> ⚠️ **Pernyataan Etika:** Seluruh pengujian dan simulasi serangan dijalankan sepenuhnya pada lingkungan laboratorium Docker lokal yang terisolasi (`internal: true`). Dilarang memindai atau mengarahkan serangan ke host mana pun di luar lab.

---

## 👤 Identitas Mahasiswa & Penentuan Kasus

| Keterangan | Detail |
| :--- | :--- |
| **Nama** | Ahmad Kurnia |
| **NIM** | `24552011297` |
| **Kelas / Semester** | TIF RP 24E CNS / Semester 5 |
| **Mata Kuliah** | Keamanan Jaringan (3 SKS) |
| **Dosen Pengampu** | Yasti Aisyah Primianjani, S.Kom., M.S.F. |
| **Perhitungan Kasus** | Digit: `2+4+5+5+2+0+1+1+2+9+7 = 38` → `38 mod 10 = 8` → **Kasus 8 (`k8`)** |

### Parameter Kasus 8 (`k8`)
- **Container Target:** `target-k8`
- **Volume Docker:** `vol-k8`
- **File Laporan:** `laporan-k8.txt`
- **Kata Sandi Enkripsi:** `kunci-k8-2026`
- **Domain DNS Exfiltration:** `k8.exfil.lab`
- **Sample WPA2 (Tugas 4):** `handshake-k8.cap` & `wordlist-k8.txt`
- **NIM dalam Hex (Tugas 7):** `3234353532303131323937`

---

## 📋 Ringkasan 7 Tugas yang Dikerjakan

Seluruh output terminal asli, perintah *reproducible*, dan analisis teknis tercantum lengkap di berkas **[`jawaban.md`](./jawaban.md)**:

| No | Pertemuan | Topik Utama | Ringkasan Pembuktian |
| :---: | :---: | :--- | :--- |
| **1** | P1 | **Docker, Volume & Compose** | Persistensi NIM `24552011297` pada `vol-k8` & akses Nginx di jaringan `internal: true`. |
| **2** | P2 | **Kriptografi (AES, SHA, X.509)** | Enkripsi-dekripsi AES-256-CBC dengan hash SHA-256 identik + sertifikat self-signed `CN=k8.exfil.lab`. |
| **3** | P3 | **Layer 2 — ARP Spoofing** | Pemalsuan MAC gateway lewat `arpspoof` & pemulihan permanen via Static ARP (`PERM`). |
| **4** | P4 | **Wireless — WPA2 Handshake** | Analisis `handshake-k8.cap` & `wordlist-k8.txt` dengan `aircrack-ng` + 4-Way Handshake. |
| **5** | P5 | **Layer 3 — ICMP & Scapy** | Pengiriman paket ICMP Echo Request kustom (`kirim_icmp.py`) dengan balasan `TTL=64`, `Type=0`. |
| **6** | P6 | **Layer 4 — SYN Flood & TCP** | Pengujian beban `hping3 --flood`, observasi `SYN_RECV`, & tangkapan 3-Way Handshake (`tcpdump`). |
| **7** | P7 | **Layer 7 — DNS Exfiltration** | Eksfiltrasi hex NIM ke `k8.exfil.lab`, deteksi anomali via `analisis_dns.py`, & decode ulang. |

---

## 📁 Struktur Repositori

```text
uts-keamanan-jaringan-ahmadkurnia/
├── README.md                              # Dokumentasi utama repositori
├── jawaban.md                             # Jawaban lengkap UTS Kasus 8 (output & analisis)
├── .gitignore                             # Filter artefak sementara & private key
├── cleanup.sh                             # Skrip pembersihan lingkungan lab
├── 01-sumber-lab/                         # Infrastruktur & source lab Docker
│   ├── images/
│   │   ├── uts-openssl/Dockerfile         # Image OpenSSL (Tugas 2)
│   │   ├── uts-kali-tools/Dockerfile      # Image Kali Tools: hping3, scapy, tcpdump, aircrack-ng, dsniff
│   │   └── uts-dnsmasq/Dockerfile         # Image DNS resolver lab (Tugas 7)
│   ├── b/
│   │   ├── b1-compose/docker-compose.yml  # Lab isolasi internal (Tugas 1)
│   │   ├── b3-syn-flood/docker-compose.yml# Lab TCP SYN Flood (Tugas 6)
│   │   └── b4-dns-exfil/docker-compose.yml# Lab DNS Exfiltration (Tugas 7)
│   ├── kasus/
│   │   ├── k5-scapy/kirim_icmp.py         # Skrip Scapy ICMP (Tugas 5)
│   │   └── k9-dns-detect/analisis_dns.py  # Skrip deteksi DNS exfiltration (Tugas 7)
│   └── samples/                           # File capture (.cap), wordlist (.txt), & panduan
└── 02-dokumen/                            # Dokumen soal, rubrik, & lembar perintah
```

---

## 🚀 Cara Menjalankan Ulang Lab (Reproducibility)

> Semua lab Compose menggunakan jaringan `internal: true` (tanpa akses internet), sehingga image wajib di-*build* terlebih dahulu sebelum pengujian.

```bash
# 1. Clone repositori dan masuk ke folder sumber lab
git clone [https://github.com/AhmadKurnia13/uts-keamanan-jaringan-ahmadkurnia.git](https://github.com/AhmadKurnia13/uts-keamanan-jaringan-ahmadkurnia.git)
cd uts-keamanan-jaringan-ahmadkurnia/01-sumber-lab

# 2. Build custom image & pull base image
docker build -t uts-openssl images/uts-openssl
docker build -t uts-kali-tools images/uts-kali-tools
docker build -t uts-dnsmasq images/uts-dnsmasq
docker pull alpine && docker pull nginx:alpine && docker pull vulnerables/web-dvwa && docker pull kalilinux/kali-rolling

# 3. Ikuti urutan perintah lengkap Kasus 8 pada berkas ../jawaban.md
```

---

## 📚 Referensi

- Repositori Resmi Mata Kuliah: [yastiaisyah/Network-Security-Course-Bank](https://github.com/yastiaisyah/Network-Security-Course-Bank)
````

*(Opsional: Kalau kamu juga mau naruh file laporan **`Laporan_UTS_Keamanan_Jaringan_Kasus8_Ahmad_Kurnia_24552011297.pdf`** atau folder screenshot di repo seperti Andrian, tinggal copy saja ke folder `UTS-Network-Security/` sebelum push—langsung otomatis ikut ter-upload!)*

---

## 4. Langkah Push ke GitHub Lewat PowerShell (VS Code)

Buka terminal PowerShell di VS Code, pastikan posisinya ada di folder **`UTS-Network-Security`** (naik satu tingkat dari `01-sumber-lab` pakai `cd ..`):

```powershell
# 1. Pastikan berada di folder UTS-Network-Security (bukan 01-sumber-lab)
cd D:\Downloads\Network-Security-Course-Bank-main\UTS-Network-Security

# 2. Inisialisasi Git baru di folder ini & pakai branch main
git init
git branch -M main

# 3. Cek daftar file yang akan di-upload (PASTIKAN samples/, jawaban.md, README.md ada, dan *.pem/*.enc TIDAK ada)
git status

# 4. Stage semua file dan lakukan commit pertama
git add .
git commit -m "feat: upload UTS Keamanan Jaringan Kasus 8 (jawaban.md, lab Docker, dan samples)"

# 5. Hubungkan ke repository GitHub yang baru kamu buat (sesuaikan nama repo jika berbeda)
git remote add origin https://github.com/AhmadKurnia13/uts-keamanan-jaringan-ahmadkurnia.git

# 6. Push ke GitHub
git push -u origin main
```

### Checklist Verifikasi Cepat Setelah `git push`
1. Buka `[https://github.com/AhmadKurnia13/uts-keamanan-jaringan-ahmadkurnia](https://github.com/AhmadKurnia13/uts-keamanan-jaringan-ahmadkurnia)` di browser.
2. Pastikan **`README.md`** tampil rapi dengan *badges* dan tabel identitas, serta **`jawaban.md`** dan **`01-sumber-lab/samples/`** terlihat di daftar file.
3. Pastikan file `key-k8.pem`, `cert-k8.pem`, dan `dns-k8.log` **tidak ikut masuk** di folder `01-sumber-lab/`.
4. Klik ikon gerigi ⚙️ di kanan bagian **About**, lalu masukkan **Description**, **Website**, dan **Topics** dari Bagian 1 di atas.

*(Tips: Sebelum `git add .`, kalau di dalam `01-sumber-lab/samples/` kamu hanya ingin menyisakan file Kasus 8 saja biar ekstra bersih seperti Dafa[cite: 80] — atau mau dibiarkan semua `k1`–`k10` — dua-duanya aman; membiarkan seluruh isi `samples/` juga bagus karena tetap lengkap.)*

Kalau pas jalanin `git status` atau `git push` muncul pesan error (misalnya login GitHub atau branch bentrok), langsung *paste* ke sini biar langsung kita beresin!

```