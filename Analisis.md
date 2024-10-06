# Hasil Benchmark Apache:

## 1. By Busyness:

- Permintaan per detik: 966.01 [#/sec]
- Waktu per permintaan: 60.236 ms
- Permintaan gagal: 68
- Transfer rate: 58.35 Kbytes/sec

## 2. By Requests:

- Permintaan per detik: 1650.00 [#/sec]
- Waktu per permintaan: 6.061 ms
- Permintaan gagal: 66
- Transfer rate: 580.18 Kbytes/sec

## 3. By Traffic:

- Permintaan per detik: 636.53 [#/sec]
- Waktu per permintaan: 15.703 ms
- Permintaan gagal: 66
- Transfer rate: 224.87 Kbytes/sec

# Hasil Benchmark Nginx :

## 1. Nginx Least Connections:

- Permintaan per detik: 1736.50 [#/sec]
- Waktu per permintaan: 5.759 ms
- Permintaan gagal: 66
- Transfer rate: 534.04 Kbytes/sec

## 2. Nginx Round Robin:

- Permintaan per detik: 545.36 [#/sec]
- Waktu per permintaan: 18.337 ms
- Permintaan gagal: 67
- Transfer rate: 167.77 Kbytes/sec

# ANALISIS KESIMPULAN

## Apache vs Nginx:

- **Kinerja Permintaan per Detik**: Nginx, terutama dalam mode Least Connections, unggul secara signifikan dibandingkan Apache, menangani 1736 permintaan per detik dibandingkan dengan performa terbaik Apache di 1650 permintaan per detik.
- **Waktu Respons**: Nginx menunjukkan waktu respons yang lebih cepat di kedua mode (5.759 ms di Least Connections dan 18.337 ms di Round Robin) dibandingkan dengan Apache, yang memiliki waktu respons terbaik 6.061 ms di salah satu modenya.
- **Transfer Rate**: Transfer rate tertinggi dipegang oleh Apache dalam mode By Requests (580.18 Kbytes/sec), namun Nginx juga menunjukkan hasil yang kompetitif di Least Connections dengan 534.04 Kbytes/sec.
- **Permintaan Gagal**: Kedua server menunjukkan angka permintaan gagal yang relatif serupa di semua mode, berkisar antara 66 hingga 68.

## Efisiensi Mode Nginx:

- **Least Connections**: Nginx dalam mode Least Connections lebih efisien dalam menangani permintaan per detik dengan waktu respons yang lebih rendah dibandingkan dengan semua mode Apache dan Nginx Round Robin.
- **Round Robin**: Mode Round Robin di Nginx menunjukkan performa lebih rendah dibandingkan dengan Least Connections, namun masih cukup kompetitif dibandingkan dengan beberapa mode Apache.

## Apache Performance:

- Apache menunjukkan performa terbaik dalam mode By Requests, dengan permintaan per detik tertinggi dan waktu respons yang cepat. Namun, dalam mode By Busyness dan By Traffic, kinerjanya menurun secara signifikan.

## Rekomendasi:

- **Jika beban koneksi tinggi** dan dibutuhkan server yang dapat menangani banyak permintaan per detik dengan waktu respons rendah, Nginx dalam mode Least Connections adalah pilihan terbaik.
- **Untuk transfer data tinggi**, Apache dalam mode By Requests memberikan transfer rate tertinggi, namun Nginx tetap menjadi alternatif yang efisien secara keseluruhan.
