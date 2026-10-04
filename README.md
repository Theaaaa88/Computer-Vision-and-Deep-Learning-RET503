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

   



