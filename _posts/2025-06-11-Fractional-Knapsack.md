---
title: "Fractional Knapsack"
date: 2025-06-11
categories: [Algoritma, Programming, Tutorial]
tags: [greedy-algorithm, activity-selection, knapsack-problem, beginner-friendly]
author: "A. Alya Musaenab Asmin"
---

Halo Sobat Ngoding! 👋 Pernah ngerasa jadwal padat banget sampai bingung mau ngerjain yang mana dulu? Atau, pernah belanja kebutuhan dapur tapi tas belanjaan cuma muat segitu-gitu aja, padahal banyak barang yang pengen dibeli? 

Nah, di dunia algoritma, ada dua masalah seru yang mirip-mirip kayak gitu: **Activity Selection Problem** dan **Fractional Knapsack Problem**. Keduanya bisa kita selesaikan pakai jurus ampuh bernama Algoritma *Greedy*! Penasaran? Yuk, kita bedah satu per satu dengan santai!

## 1. Activity Selection Problem: Pilih Aktivitas Biar Nggak Tabrakan!

Bayangkan ini: Kamu punya daftar kegiatan, misalnya nonton film, belajar, olahraga, atau ketemu teman. Tiap kegiatan punya waktu mulai dan waktu selesai. Masalahnya, kamu cuma punya satu badan! Jadi, nggak mungkin bisa ngerjain dua hal sekaligus di waktu yang sama, kan?

Nah, "Activity Selection Problem" ini persis kayak gitu. Tujuannya adalah milih sebanyak mungkin aktivitas yang bisa kamu kerjakan tanpa ada yang tabrakan waktunya. Jadi, kalau satu kegiatan selesai, kegiatan berikutnya baru bisa dimulai setelah itu.

### Jurus Jitu: Algoritma Greedy untuk Pilih Aktivitas

Gimana cara milihnya biar dapat paling banyak aktivitas? Kita pakai trik *greedy*! Apa itu *greedy*? Gampangannya, *greedy* itu mikir "yang penting sekarang untung, nanti gimana-gimana dipikir belakangan."

Untuk masalah ini, jurus *greedy* kita adalah:

1. **Urutkan semua kegiatan berdasarkan waktu selesainya** dari yang paling cepat
2. **Pilih kegiatan yang selesai paling awal** sebagai yang pertama. Kenapa? Logikanya, kalau kita selesai lebih cepat, sisa waktu buat kegiatan lain jadi lebih banyak, kan?
3. **Lalu, untuk kegiatan berikutnya, pilih aja yang waktu mulainya nggak tabrakan** sama kegiatan yang barusan kita pilih

Gampang, kan? Contoh nih:

| Aktivitas | Mulai (s) | Selesai (f) |
|-----------|-----------|-------------|
| A1        | 1         | 4           |
| A2        | 3         | 5           |
| A3        | 0         | 6           |
| A4        | 5         | 7           |
| A5        | 8         | 9           |
| A6        | 5         | 9           |

**Langkah-langkahnya:**

1. Urutkan berdasarkan waktu selesai: A1 (4), A2 (5), A3 (6), A4 (7), A5 (9), A6 (9)
2. Pilih A1 (selesai paling awal)
3. A2 dan A3 tabrakan sama A1. Skip!
4. A4? Mulainya (5) lebih besar dari selesainya A1 (4). Cocok! Pilih A4. Sekarang punya {A1, A4}
5. A5? Mulainya (8) lebih besar dari selesainya A4 (7). Cocok! Pilih A5. Sekarang punya {A1, A4, A5}
6. A6? Tabrakan sama A5. Skip!

Jadi, aktivitas optimal yang bisa kamu kerjakan adalah **A1, A4, dan A5**! Lumayan banyak, kan?

### Ribet Nggak sih Ngitungnya? (Kompleksitas)

Tenang, algoritma ini efisien banget!

- **Waktu:** Paling lama itu di bagian ngurutin kegiatannya. Kalau pakai cara ngurutin yang pintar (kayak Quick Sort atau Merge Sort), itu butuh waktu sekitar $O(n \log n)$ (dibaca "N log N", di mana N itu jumlah kegiatan). Setelah diurutin, tinggal jalan sekali aja buat milih-milih, jadi $O(n)$. Totalnya ya $O(n \log n)$
- **Ruang:** Nggak butuh banyak memori tambahan kok, cuma seukuran data inputnya aja, yaitu $O(n)$

### Dipakai buat Apa aja? (Aplikasi Dunia Nyata)

Algoritma ini sering banget dipakai buat:

- **Jadwalin kelas, rapat, atau lab** di kampus/kantor
- **Jadwalin kerja CPU** di komputer kamu
- **Atur pengiriman barang** di logistik
- **Alokasi *bandwidth*** di jaringan telekomunikasi

## 2. Fractional Knapsack Problem: Isi Tas Belanja Sampai *Full*!

Sekarang, kita pindah ke masalah tas belanja. Bayangkan kamu punya tas dengan kapasitas terbatas (misalnya, cuma bisa angkut 10 kg). Di toko, ada banyak barang (beras, gula, kopi) yang masing-masing punya berat dan nilai (misalnya, gula 1 kg nilainya Rp 10.000, kopi 0.5 kg nilainya Rp 20.000). Nah, "Knapsack Problem" itu intinya gimana caranya kita milih barang biar total nilainya maksimal tapi nggak melebihi kapasitas tas.

Ada dua jenis Knapsack:

- **0/1 Knapsack:** Kamu cuma bisa ambil barang *semua* atau *nggak sama sekali*. Nggak boleh dipotong-potong
- **Fractional Knapsack:** Nah, ini yang seru! Kamu **boleh ambil sebagian** dari barang itu. Misalnya, kalau kapasitas tas sisa 0.5 kg dan kamu ketemu sekarung beras 10 kg, kamu bisa ambil 0.5 kg berasnya aja

Perbedaan ini penting! Karena boleh dipotong, "Fractional Knapsack" ini jadi lebih gampang diselesaikan pakai algoritma *greedy*. Kalau yang 0/1 Knapsack, biasanya butuh cara yang lebih rumit (pakai pemrograman dinamis).

### Strategi Greedy untuk Isi Tas Penuh Manfaat!

Untuk "Fractional Knapsack", jurus *greedy* kita juga nggak kalah simpel:

1. **Hitung "nilai per kilo"** (atau nilai per unit berat) untuk setiap barang. Caranya: `nilai barang / berat barang`
2. **Urutkan barang-barang itu dari yang "nilai per kilo"-nya paling tinggi** ke yang paling rendah
3. **Mulai ambil barang dari yang "nilai per kilo"-nya paling tinggi**. Ambil sebanyak-banyaknya sampai tasmu penuh atau barangnya habis
4. Kalau pas sampai di satu barang, tasmu tinggal sedikit kapasitasnya, **ambil aja sebagian dari barang itu** sampai tasmu bener-bener penuh!

Dengan cara ini, kamu dijamin akan mendapatkan total nilai barang yang paling maksimal!

### Contoh Kasus Fractional Knapsack

Mari kita lihat contoh praktis:

**Kapasitas tas:** 10 kg

| Barang | Berat (kg) | Nilai (Rp) | Nilai/kg |
|--------|------------|------------|----------|
| Kopi   | 2          | 40,000     | 20,000   |
| Gula   | 3          | 45,000     | 15,000   |
| Beras  | 5          | 50,000     | 10,000   |
| Tepung | 4          | 32,000     | 8,000    |

**Langkah-langkah:**

1. Urutkan berdasarkan nilai/kg: Kopi (20,000), Gula (15,000), Beras (10,000), Tepung (8,000)
2. Ambil Kopi (2 kg) → Sisa kapasitas: 8 kg
3. Ambil Gula (3 kg) → Sisa kapasitas: 5 kg  
4. Ambil Beras (5 kg) → Sisa kapasitas: 0 kg
5. Tepung nggak muat lagi

**Total nilai:** 40,000 + 45,000 + 50,000 = **Rp 135,000**

### Nggak Usah Mikir Berat (Kompleksitas)

Sama seperti Activity Selection, algoritma ini juga efisien:

- **Waktu:** Proses paling lama juga di bagian ngurutin barang berdasarkan "nilai per kilo"-nya, yaitu $O(n \log n)$. Setelah diurutkan, tinggal ambil barang-barangnya satu per satu, ini $O(n)$. Jadi, totalnya tetap $O(n \log n)$

### Dimana Saja Bisa Dipakai? (Aplikasi Dunia Nyata)

Ini dia beberapa contoh penerapan *Fractional Knapsack*:

- **Penjadwalan tugas** yang butuh sumber daya terbatas (misalnya, alokasi waktu *project*)
- **Investasi dana** ke berbagai proyek yang punya potensi keuntungan dan risiko berbeda
- **Pembagian *bandwidth*** di jaringan internet
- **Optimisasi logistik**, misalnya mengisi kontainer pengiriman

## Jadi, Algoritma Greedy itu Apa sih?

Singkatnya, algoritma *greedy* itu pendekatan di mana kita selalu membuat **pilihan terbaik saat ini juga**, tanpa mikirin dampak jangka panjangnya. Ibaratnya, kalau ada permen di depan mata, langsung ambil aja yang paling gede!

### Kelebihannya:
- Gampang banget dipahami dan diimplementasikan
- Cepat dan efisien untuk masalah-masalah tertentu
- Untuk masalah kayak Activity Selection dan Fractional Knapsack, jurus *greedy* ini emang jaminan mutu, alias **pasti menghasilkan solusi optimal**!

### Kekurangannya:
- Nah, nggak semua masalah bisa diselesaikan pakai *greedy* dan hasilnya optimal
- Kadang, pilihan terbaik sekarang malah bikin rugi di masa depan
- Jadi, harus hati-hati dan tahu kapan pakai jurus *greedy* ini!

### Kapan Pakai Greedy?

Algoritma *greedy* cocok dipakai kalau:
- Masalah bisa dipecah jadi keputusan-keputusan kecil
- Keputusan terbaik di setiap langkah akan membawa ke solusi optimal
- Nggak perlu "mundur" atau mengubah keputusan yang sudah diambil

## Implementasi Sederhana

Buat yang pengen lihat kodenya, ini contoh implementasi Activity Selection dalam Python:

```python
def activity_selection(activities):
    # Urutkan berdasarkan waktu selesai
    sorted_activities = sorted(activities, key=lambda x: x[2])
    
    selected = [sorted_activities[0]]  # Pilih yang pertama
    last_finish_time = sorted_activities[0][2]
    
    for activity in sorted_activities[1:]:
        start_time = activity[1]
        if start_time >= last_finish_time:
            selected.append(activity)
            last_finish_time = activity[2]
    
    return selected

# Contoh penggunaan
# Format: (nama, mulai, selesai)
activities = [
    ("A1", 1, 4),
    ("A2", 3, 5), 
    ("A3", 0, 6),
    ("A4", 5, 7),
    ("A5", 8, 9),
    ("A6", 5, 9)
]

result = activity_selection(activities)
print("Aktivitas terpilih:", [act[0] for act in result])
```

**Output:**
```
Aktivitas terpilih: ['A1', 'A4', 'A5']
```

## Tips dan Trik

### Untuk Activity Selection:
- Selalu urutkan berdasarkan waktu selesai, bukan waktu mulai
- Jangan tergoda untuk memilih aktivitas yang "terlihat penting" - ikuti aturan greedy
- Kalau ada tie (waktu selesai sama), pilih yang waktu mulainya lebih lambat

### Untuk Fractional Knapsack:
- Hitung rasio nilai/berat dengan teliti
- Jangan lupa, kamu boleh ambil sebagian barang!
- Kalau ada barang dengan rasio sama, pilih yang beratnya lebih ringan dulu

## Penutup

Gimana, seru kan belajar algoritma? Activity Selection dan Fractional Knapsack ini cuma dua contoh kecil dari banyak masalah yang bisa diselesaikan dengan cerdas menggunakan Algoritma *Greedy*. 

Intinya, kalau ada masalah optimasi yang bisa dipecah jadi langkah-langkah kecil dan pilihan terbaik di setiap langkah selalu membawa ke solusi terbaik secara keseluruhan, berarti itu cocok pakai *greedy*!

Semoga penjelasan santai ini bikin kamu lebih semangat belajar algoritma ya! Kalau ada pertanyaan, jangan sungkan tanya-tanya di kolom komentar atau langsung kontak kami. 

**Happy coding!** 🚀

---

*Artikel ini dibuat dengan cinta untuk para pembelajar algoritma. Jangan lupa share kalau bermanfaat!*