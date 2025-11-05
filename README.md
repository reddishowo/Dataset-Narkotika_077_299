# Dataset Narkotika PN Surabaya 2025

> Kumpulan 55 putusan pidana narkotika Pengadilan Negeri Surabaya (PN Sby) bulan September 2025 beserta lembar ringkasan terstruktur.

---

## Ringkasan

- Fokus pada tindak pidana narkotika golongan I (sabu, ganja, ekstasi) dengan variasi dakwaan tunggal maupun kumulatif.
- Setiap putusan tersedia sebagai PDF asli (`Dataset/Narkotika/*.pdf`) dan direferensikan oleh metadata terstruktur (`Overview/Overview.xlsx`) dengan 25 kolom naratif.
- Rentang tanggal sidang 3 s/d 30 September 2025, melibatkan 55 perkara dengan panel hakim berbeda.
- Cocok untuk riset NLP hukum, ekstraksi informasi, analisis pola penjatuhan hukuman, serta pembangunan sistem penelusuran putusan.

---

## Struktur Folder

- `Dataset/Narkotika.zip` - arsip sumber berisi 55 berkas putusan.
- `Dataset/Narkotika/` - hasil ekstraksi arsip, tiap file dinamai `NomorPerkara_Pid.Sus_2025_PN_Sby.pdf`.
- `Overview/Overview.xlsx` - ringkasan metadata hasil kurasi manual dari setiap putusan.

```
Dataset-Narkotika_077_299/
├─ Dataset/
│  ├─ Narkotika.zip
│  └─ Narkotika/
│     ├─ 1334_Pid.Sus_2025_PN_Sby.pdf
│     ├─ ... (total 55 berkas)
│     └─ 1946_Pid.Sus_2025_PN_Sby.pdf
└─ Overview/
	└─ Overview.xlsx
```

---

## Statistik Cepat

- Jumlah perkara: 55
- Rentang tanggal persidangan: 3 September 2025 - 30 September 2025
- Sebaran hari sidang: didominasi Selasa - Kamis (37 dari 55 perkara)
- Jenis pidana dominan: kepemilikan, penguasaan, peredaran narkotika golongan I
- Format naskah: PDF bahasa Indonesia, rata-rata 25-35 halaman, berformat resmi Mahkamah Agung

---

## Skema Metadata (`Overview/Overview.xlsx`)

| Kolom | Deskripsi singkat |
| --- | --- |
| `Id` | Nama berkas PDF yang menjadi referensi perkara. |
| `judul` | Judul putusan sebagaimana tercantum di dokumen. |
| `nomor` | Nomor perkara lengkap (contoh: `1334/Pid.Sus/2025/PN Sby`). |
| `irah irah` | Bagian pembuka "Demi Keadilan Berdasarkan Ketuhanan Yang Maha Esa". |
| `nama pengadilan negeri` | Nama pengadilan pemutus (seluruh entri: PN Surabaya). |
| `keterangan perkara` | Ringkasan konteks perkara dan pasal yang didakwakan. |
| `identitas terdakwa` | Identitas resmi terdakwa (nama, TTL, alamat, pekerjaan). |
| `penangkapan` | Kronologi penangkapan dan penyitaan awal. |
| `riwayat_perkara_penahanan` | Riwayat penahanan dan tahapan proses peradilan. |
| `tuntutan` | Amar tuntutan Penuntut Umum termasuk pidana dan denda. |
| `dakwaan` | Uraian dakwaan primer maupun subsider. |
| `bukti saksi` | Ringkasan keterangan saksi. |
| `bukti ahli` | Ringkasan pendapat ahli (bila tersedia). |
| `bukti terdakwa` | Keterangan atau pengakuan terdakwa. |
| `bukti surat` | Bukti surat atau dokumen pendukung. |
| `petunjuk bb` | Rincian barang bukti dan statusnya. |
| `fakta hukum` | Fakta-fakta hukum yang dinyatakan terbukti. |
| `pertimbangan hukum` | Pertimbangan yuridis sebelum amar putusan. |
| `putusan` | Amar putusan lengkap (pidana pokok, denda, biaya perkara, dan lain-lain). |
| `hari` | Hari sidang pembacaan putusan (format teks). |
| `tanggal` | Tanggal sidang; konversi ke ISO diperlukan untuk analisis kuantitatif. |
| `tahun` | Tahun penjatuhan putusan (seluruhnya 2025). |
| `siapa yang memutus` | Susunan majelis hakim yang memutus. |
| `panitera pengganti` | Panitera pengganti yang mendampingi sidang. |
| `tanda tangan majelis` | Status atau catatan mengenai tanda tangan elektronik atau manual. |

---

## Cara Mulai Cepat

```bash
# 1) Opsional: buat lingkungan virtual
python -m venv .venv
.\.venv\Scripts\Activate

# 2) Pasang paket dasar untuk membaca metadata
pip install pandas openpyxl

# 3) Muat metadata dan lihat ringkasan awal
python - <<"PY"
import pandas as pd
df = pd.read_excel('Overview/Overview.xlsx')
df['tanggal'] = pd.to_datetime(df['tanggal'], errors='coerce')
print(df[['Id', 'nomor', 'tanggal']].head())
print('Rentang tanggal:', df['tanggal'].min(), 's.d.', df['tanggal'].max())
PY
```

---

## Contoh Pipeline Analitik

1. Ekstraksi teks: gunakan `pdfplumber`, `PyMuPDF`, atau OCR (`tesseract`) untuk mengubah PDF menjadi teks mentah.
2. Pembersihan: normalisasi heading, hapus footer, dan segmentasikan per bagian seperti `PERTIMBANGAN HUKUM` dan `AMAR`.
3. Penandaan entitas: terapkan NER untuk mendeteksi nama pihak, barang bukti, pasal undang-undang, dan lokasi penangkapan.
4. Analisis kuantitatif: korelasikan lamanya pidana dengan berat barang bukti, jenis narkotika, atau peran terdakwa.
5. Visualisasi: bangun dashboard timeline putusan, distribusi denda, serta jaringan relasi terdakwa dan saksi.

---

## Rekomendasi Studi Lanjutan

- Klasifikasi hukuman: prediksi pidana dan denda berdasarkan narasi fakta serta dakwaan.
- Ringkasan otomatis: bangun summarizer amar putusan untuk konsumsi publik dan paralegal.
- Legal question answering: kembangkan sistem tanya jawab berbasis retrieval untuk UU Narkotika dan putusan PN Surabaya.
- Evaluasi konsistensi: bandingkan putusan serupa guna menguji keselarasan dengan UU No. 35 Tahun 2009 dan regulasi turunannya.

---

## Pertimbangan Etis dan Kepatuhan

- Data memuat identitas terdakwa dan pihak terkait; gunakan secara bertanggung jawab dan patuhi regulasi perlindungan data Indonesia.
- Saat mempublikasikan analisis, pertimbangkan anonimisasi atau pseudonimisasi informasi sensitif sesuai pedoman Mahkamah Agung.
- Dataset ini tidak menggantikan nasihat hukum profesional; interpretasi hukum sebaiknya melibatkan pakar yang kompeten.

---

## Kontribusi

- Gunakan issue untuk melaporkan kekeliruan metadata atau mengusulkan penambahan anotasi.
- Sertakan referensi perkara serta langkah reproduksi ketika mengirim pull request.
- Dokumentasikan skrip ekstraksi atau transformasi agar peninjau dapat memverifikasi perubahan.

---

## Lisensi dan Hak Cipta

- Putusan pengadilan adalah dokumen publik; hak cipta berada pada Pengadilan Negeri Surabaya atau Mahkamah Agung RI.
- Metadata (`Overview/Overview.xlsx`) dirilis dengan lisensi Creative Commons Attribution 4.0 (CC BY 4.0) kecuali dinyatakan lain oleh pemilik repositori.
- Cantumkan atribusi ke Dataset Narkotika PN Surabaya 2025 saat memanfaatkan dataset ini dalam publikasi atau produk turunan.

---

## Riwayat Versi

- v1.0 (November 2025): rilis perdana dengan 55 putusan pidana narkotika dan 25 kolom metadata naratif.

---