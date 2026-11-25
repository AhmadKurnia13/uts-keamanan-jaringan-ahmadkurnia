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

- 📄 **Laporan Praktikum Lengkap (PDF):** [`Laporan_UTS_Keamanan_Jaringan_Kasus8_Ahmad_Kurnia_24552011297.pdf`](./Laporan_UTS_Keamanan_Jaringan_Kasus8_Ahmad_Kurnia_24552011297.pdf)
- 📝 **Lembar Jawaban & Output Terminal:** [`jawaban.md`](./jawaban.md)

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
