# Computer-Vision-and-Deep-Learning-RET503
Klasifikasi Citra Kamera Saku vs Mouse dengan ResNet18 (Transfer Learning)
Tugas: Klasifikasi citra 2 kelas: kamera (kamera saku) dan mouse
Data: 100 foto buatan sendiri (50 per kelas) 

Langkah-langkah :

A. Ambil Gambar

1. Siapkan dua benda: satu kamera saku dan satu mouse.
2. Ambil 50 foto per benda (total 100). Variasikan: depan, samping kiri/kanan, belakang, atas, bawah/dibalik, dekat dan jauh, posisi diputar, sedikit perubahan cahaya.
3. Satu benda per foto (jangan ada kamera di foto mouse, dan sebaliknya).
4. Pakai alas dan cahaya yang mirip untuk kedua kelas, supaya model tidak belajar membedakan latar.
5. Format .jpg atau .png . Foto .heic harus diubah ke JPG dulu.

B. Susun Dataset

C:\proyek\ train_resnet18.py dataset\
 kamera\   (50 foto)
mouse\    (50 foto)
Nama folder menjadi nama kelas. Cek: dir dataset harus menampilkan kamera dan mouse .

C. Pasang Python
1. Unduh dari python.org, jalankan installer, centang "Add python.exe to PATH", klik Install Now.
2. Buka terminal baru, ketik python --version (hasil di percobaan ini: Python 3.13.x).
3. Aktifkan:
   PowerShell: Set-ExecutionPolicy -Scope Process -ExecutionPolicy Bypass lalu
   venv\Scripts\activate
   Command Prompt: venv\Scripts\activate.bat
   Tanda berhasil: ada tulisan (venv) di awal baris.
4. Pasang Library: pip install torch torchvision matplotlib
5. Jalankan training: python train_resnet18.py
6. Hasil yang dihasilkan: grafik_training.png (kurva loss dan akurasi), confusion_matrix.png , hasil_training.txt (ringkasan),
   model_resnet18.pth (model).

   <img width="551" height="323" alt="image" src="https://github.com/user-attachments/assets/fcab094d-7b5b-49f5-bcdb-c420e9935669" />

Hasil Grafil dan Analisis:
A. Grafik Loss
<img width="415" height="297" alt="image" src="https://github.com/user-attachments/assets/68f2f53f-58b4-4c08-8b6f-2d5a041a5134" />
1. Loss training rendah sejak awal (sekitar 0,5 di epoch 1 dan di bawah 0,35 setelahnya), artinya model cepat menyesuaikan      diri.
2. Loss validasi melonjak ke 23,1 di epoch 2, lalu turun ke 1,8 (epoch 3), 1,3 (epoch 4), dan sekitar 0,1-0,2 sejak epoch 5.    Lonjakan ini tidak berulang.
3. Penyebab lonjakan belum diuji di eksperimen ini. Penjelasan yang masuk akal: learning rate 0,001 cukup besar untuk           melatih seluruh lapisan yang sudah pretrained, batch kecil (8) membuat statistik BatchNorm tidak stabil, dan validasi        hanya 20 citra sehingga beberapa tebakan salah dengan keyakinan tinggi langsung menaikkan loss rata-rata sangat besar.
4. Sejak epoch 5 kedua kurva berdekatan di nilai kecil, tidak ada pelebaran celah yang menandakan overfitting parah.

B. Grafik Aakurasi
<img width="406" height="290" alt="image" src="https://github.com/user-attachments/assets/1fe96730-62fc-4e6e-b118-43edfd06ca7a" />
1. Akurasi training naik dari 0,85 ke sekitar 0,99. Turunnya di epoch 11 (0,925) dan 15 sejalan dengan loss yang naik           sesaat; ini variasi wajar karena augmentasi acak dan batch kecil.
2. Akurasi validasi naik-turun di epoch 1-6 (0,55 sampai 0,95), lalu konstan 0,95 dari epoch 7 sampai 15.
3. Catatan pembacaan: akurasi training dihitung pada citra yang sudah diaugmentasi dengan model dalam mode training,            sedangkan validasi pada citra asli dengan mode evaluasi. Jadi keduanya tidak sepenuhnya sebanding, dan akurasi validasi      bisa sesekali lebih tinggi dari training.
4. Selisih akhir training dan validasi sekitar 0,04, tidak menunjukkan overfitting yang berarti.


C.Confusion matrix
<img width="330" height="293" alt="image" src="https://github.com/user-attachments/assets/8517e476-5293-4d4c-9319-64726ca6f4ad" />

1.Semua 11 kamera dikenali benar (recall 100%).
2.Satu mouse dikira kamera, sehingga precision kamera 91,7% dan recall mouse 88,9%. Semua prediksi
 "mouse" benar (precision 100%).
3.Hanya ada satu jenis kesalahan (mouse dikira kamera). Foto yang salah itu belum diperiksa; kemungkinan diambil dari sudut yang        membuat mouse tampak mirip kamera, tapi ini dugaan.
