Tugas 1.
Jelaskan bagaimana mengerjakan hal-hal berikut dengan menggunakan awk dan perintah shell lain.
a. Menghitung baris, kata, dan karakter yang terdapat dalam teks.
Jawab : Untuk menghitung jumlah baris, kata, dan karakter dalam teks menggunakan awk dan perintah shell lainnya, kita dapat melakukannya dengan beberapa cara. Seperti menggunakan perintah wc (word count) Perintah wc dapat digunakan untuk menghitung jumlah baris (-l), kata (-w), dan karakter (-m) dari file paulo.txt yang telah dibuat. Program :
wc -lwm paulo.txt

Selain itu, kita dapat menggunakan awk untuk menghitung secara manual. Contohnya :
awk '{ chars += length($0); words += NF; lines++ } END { print "Lines:", lines, "Words:", words, "Characters:", chars }' paulo.txt
dimana length($0) digunakan untuk menghitung jumlah karakter di setiap baris.
NF digunakan untuk menghitung jumlah kata dalam setiap baris.
lines++ digunakan untuk menambah hitungan jumlah baris.
dan END mencetak total setelah semua baris diproses.

b. Menemukan baris-baris yang mengandung token teks tertentu, misalnya: ‘love’ ‘victory’, ‘dream’, dan lain-lain.
Jawab : Untuk menemukan baris yang mengandung kata tertentu (misalnya: "love", "victory", "dream"), kita bisa menggunakan beberapa perintah, yaitu :
- Gunakan grep untuk mencari kata dalam sebuah file atau mencari beberapa kata dengan menambahkan perintah -E (Extended Regular Expressions):
grep -E "love|victory|dream" paulo.txt
- Menggunakan awk untuk mencetak baris yang mengandung kata tertentu:
awk '/love|victory|dream/ { print }' paulo.txt. Awk membaca file baris demi baris, kemudian perintah /love|victory|dream/ akan mencari baris yang mengandung kata-kata tersebut.

c. Mengganti bagian dari teks dalam baris, misalnya ‘every’ dengan ‘each’.
Jawab : Untuk mengganti bagian dari teks dalam baris, misalnya mengganti "every" dengan "each", kita bisa menggunakan beberapa perintah, seperti :
- Menggunakan perintah sed. :
sed 's/every/each/g' paulo.txt
perintah s/every/each/ akan mengganti kata every dengan each, dan g berfungsi mengganti semua kemunculan dalam setiap baris. 
- Menggunakan awk. :
awk '{gsub("every", "each"); print}' paulo.txt

Perintah gsub("every", "each") akan mengganti semua  kemunculan "every" dengan "each" di setiap baris.
- Menggunakan perl. 
perl -pi -e 's/every/each/g' paulo.txt

Perintah tersebut akan secara langsung mengganti "every" dengan "each" di dalam file.

d. Menghitung kata dan huruf per baris.
Cara terbaik untuk menghitung kata dan huruf per baris adalah dengan menggunakan awk. 
awk '{print "Baris", NR, "- Kata:", NF, "- Huruf:", length($0)}' paulo.txt

NR berfungsi sebagai penunjuk nomor baris saat ini 
NF berfungsi untuk menghitung jumlah kata dalam baris
length($0) berfungsi untuk menghitung jumlah karakter dalam baris.

2. Jelaskan dan beri contoh dari pekerjaan-pekerjaan berikut :
a. Melakukan plot dari data yang tersimpan dalam file (kasus teks pada tugas 1)
Jawab : Untuk memplot teks pada paulo.txt yang sudah dilakukan, kita dapat menggunakan awk 
awk '{print NR, NF}' paulo.txt > data.txt
gnuplot -persist <<EOF
set title "Jumlah Kata per Baris"
set xlabel "Baris"
set ylabel "Jumlah Kata"
plot "data.txt" using 1:2 with lines title "Words per Line"
EOF

perintah awk '{print NR, NF}' paulo.txt > data.txt akan mengubah paulo.txt yang berisi file menjadi sebuah file dengan isi jumlah kata perbarisnya. 

b. Menyimpan hasil plot ke dalam file
Jawab : untuk menyimpan plot sebagai gambar PNG, gunakan perintah berikut dalam gnuplot :
set terminal png
set output "plot.png"
plot "data.txt" using 1:2 with lines title "Plot Data"
set output

- set terminal png → Menggunakan format gambar PNG.
- set output "plot.png" → Menentukan nama file output (plot.png).
- plot "data.txt" using 1:2 with lines title "Plot Data" → Membuat plot dari file data.txt.
- set output → Menutup file output.

c. Konversi data menjadi CSV
Jawab : Untuk mengkonversi data menjadi CSV dengan menggunakan awk, kita bisa menggunakan perintah :
awk '{print $1 "," $2 "," $3}' paulo.txt > data.csv
- $1, $2, $3 → Mengambil kolom 1, 2, dan 3.
- "," → Menambahkan pemisah koma antara kolom.
- > data.csv → Menyimpan hasil ke file data.csv.

d. Konversi data menjadi JSON
Jawab : File data.txt dapat di konversi menjadi JSON dengan awk :
awk 'BEGIN {print "["} {printf "  {\"id\": %s, \"nilaiA\": %s, \"nilaiB\": %s}", $1, $2, $3} NR!=NF {print ","} END {print "\n]"}' paulo.txt > data.json

Tugas 3
a. Buat program untuk mencetak kalimat “Komputasi Geofisika” ke layar, dan jelaskan setiap baris programnya, dalam,
1.  bahasa c++
Jawab : #include <iostream>  

int main() {  
    std::cout << "Komputasi Geofisika" << std::endl; 
    return 0; 
}
- #include <iostream> → Memasukkan pustaka iostream untuk input/output.
- int main() → Fungsi utama program.
- std::cout << "Komputasi Geofisika" << std::endl; → Mencetak teks ke layar.
- return 0; → Mengembalikan 0 sebagai tanda program berhasil.

2. Bahasa shell script
Jawab : #!/bin/bash  # Menentukan shell interpreter

echo "Komputasi Geofisika"  # Mencetak teks ke layar

- #!/bin/bash → Menentukan bahwa skrip dieksekusi dalam Bash shell.
- echo "Komputasi Geofisika" → Mencetak teks ke layar.

3. Skrip awk
Jawab : BEGIN {  
    print "Komputasi Geofisika"  
}
- BEGIN {} → Blok yang dieksekusi sebelum membaca input data.
- print "Komputasi Geofisika" → Mencetak teks ke layar.

b. Buat agar skrip yang ditulis menjadi program yang dapat dijalankan langsung (executable). Jelaskan tahap-tahapnya.
Jawab : 
1. bahasa c 
- Kompilasi program dengan GCC
gcc print_$kalimat.c -o print_$kalimat
- jalankan program 
./print_$kalimat

2. shell script
- Pastikan skrip memiliki shebang (#!/bin/bash) di baris pertama.
- Beri izin eksekusi dengan perintah
chmod +x print_$kalimat.sh
- jalankan program dengan 
./print_$kalimat.sh

3. Skrip AWK
- Pastikan skrip memiliki shebang (#!/usr/bin/awk -f).
- Beri izin eksekusi dengan
chmod +x print_$kalimat.awk
- Jalankan langsung dengan 
./print_$kalimat.awk

Tugas 4
a. Buat akun di github.com. Jelaskan tahap-tahapnya!
Jawab : 
- Buka browser dan kunjungi GitHub.
- Klik "Sign up" (Daftar).
- Isi data pendaftaran
- Klik "Create account"
- Verifikasi email dengan membuka email dan mengklik tautan konfirmasi.
- hubungkan terminal dengan github
sudo apt update && sudo apt install git
git config --global user.name "xxxx" 
git config --global user.email "xxxx@gmail.com" 

b. Buat repositori baru di github. Jelaskan tahap-tahapnya!
- Buka GitHub dan login.
- Klik tombol "New repository".
- Masukkan Nama repositori dan Pilih Public (terbuka) atau Private (tersembunyi)
- Klik Create repository


