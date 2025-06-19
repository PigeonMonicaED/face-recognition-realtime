
# Sistem Absensi Wajah dengan GUI dan Anti-Spoofing

Aplikasi absensi wajah berbasis desktop yang dibangun menggunakan Python, OpenCV, dan PyQt5. Aplikasi ini mampu melakukan pengenalan wajah secara *real-time* melalui webcam untuk mencatat kehadiran.

Dilengkapi fitur **anti-spoofing** sederhana yang memanfaatkan deteksi tangan dari `cvzone` untuk mencegah upaya absensi menggunakan foto.

![Demo Aplikasi]()

## 📋 Fitur Utama

-   **Pengenalan Wajah Real-Time**: Mengidentifikasi wajah yang sudah terdaftar secara langsung dari video webcam.
-   **Pencatatan Kehadiran**: Secara otomatis menyimpan data nama, NIK, dan waktu kehadiran ke dalam daftar.
-   **Antarmuka Grafis (GUI)**: Tampilan interaktif yang menampilkan video, nama yang terdeteksi, daftar hadir, dan agenda.
-   [cite_start]**Fitur Anti-Spoofing**: Mendeteksi adanya tangan di depan wajah untuk membatalkan proses absensi, mencegah penggunaan foto[cite: 1].
-   [cite_start]**Tampilan Agenda**: Menampilkan jadwal atau agenda spesifik untuk pengguna yang terdeteksi (dapat dikonfigurasi)[cite: 1].

## 🛠️ Teknologi & Library

-   **Python 3.7+**
-   [cite_start]**PyQt5**: Untuk membangun antarmuka pengguna (GUI)[cite: 1].
-   [cite_start]**OpenCV**: Untuk pemrosesan gambar dan video[cite: 1].
-   [cite_start]**face_recognition**: Untuk deteksi dan pengenalan wajah (berbasis `dlib`)[cite: 1].
-   [cite_start]**cvzone**: Digunakan untuk deteksi tangan sebagai fitur anti-spoofing[cite: 1].
-   [cite_start]**imutils**: Serangkaian fungsi untuk mempermudah pemrosesan gambar dengan OpenCV[cite: 1].
-   [cite_start]**Numpy**: Untuk operasi numerik[cite: 1].

## ⚙️ Instalasi

Pastikan Anda memiliki Python 3.7 atau versi lebih baru dan Git terinstal di sistem Anda.

1.  **Clone Repositori**
    ```bash
    git clone [https://github.com/PigeonMonicaED/face-recognition-realtime.git](https://github.com/PigeonMonicaED/face-recognition-realtime.git)
    cd face-recognition-realtime
    ```

2.  **Buat Virtual Environment (Sangat Direkomendasikan)**
    ```bash
    python -m venv venv
    ```
    Aktifkan virtual environment:
    -   Di Windows: `.\venv\Scripts\activate`
    -   Di macOS/Linux: `source venv/bin/activate`

3.  **Install Dependensi**
    Gunakan file `requirements.txt` yang sudah disediakan di dalam repositori.
    ```bash
    pip install -r requirements.txt
    ```
    > **Catatan:** Instalasi `dlib` mungkin memakan waktu lama atau gagal jika `CMake` dan compiler C++ tidak terinstal. Jika terjadi error, pastikan Anda telah menginstal `build-essential` dan `cmake` (untuk Linux) atau Visual Studio Build Tools (untuk Windows).

4.  **Siapkan File yang Diperlukan**
    Pastikan file-file berikut berada dalam satu direktori utama proyek Anda:
    -   [cite_start]`GUI_attendance.py` [cite: 1]
    -   [cite_start]`haarcascade_frontalface_default.xml` [cite: 2]

## 🚀 Cara Penggunaan

Proses penggunaan terdiri dari tiga tahap: pengambilan data foto, training model, dan menjalankan aplikasi.

### 1. Tahap Pengambilan Foto Wajah
-   [cite_start]Jalankan skrip `ambil_foto_wajah.py` dengan argumen nama folder dan ID kamera[cite: 3]. Skrip ini akan otomatis membuat folder di dalam direktori `dataset`.
    ```bash
    python ambil_foto_wajah.py --folder_name=nama_anda --camera=0
    ```
    -   `--folder_name`: Ganti `nama_anda` dengan nama orang yang akan didaftarkan.
    -   `--camera`: ID kamera yang digunakan (biasanya dimulai dari `0`).
-   Tekan tombol **Spasi** untuk mengambil gambar, dan **ESC** untuk keluar dan menyimpan.

### 2. Tahap Training Model
-   Setelah folder dataset terisi foto, jalankan skrip training untuk membuat model pengenalan wajah:
    ```bash
    python train_model.py
    ```
-   Proses ini akan menghasilkan file `encodings.pickle`. **Pastikan file ini berada di folder yang sama dengan `GUI_attendance.py`**.

### 3. Menjalankan Aplikasi Absensi
-   Jika semua file sudah siap, jalankan aplikasi utama:
    ```bash
    python GUI_attendance.py
    ```

## 🔧 Konfigurasi Pengguna dan Agenda

[cite_start]Data pengguna (nama dan NIK) serta agenda masih bersifat *dummy* di dalam skrip `GUI_attendance.py`[cite: 1]. Untuk mengubahnya, buka file tersebut dan edit bagian berikut:

-   **Untuk mengubah daftar pengguna:**
    [cite_start]Cari variabel `user_list` di bagian paling bawah skrip dan sesuaikan isinya[cite: 1]. Nama harus cocok dengan nama folder di `dataset`.
    ```python
    # if __name__ == "__main__":
    
        # dummy data
        # imagine this from the database.
        user_list = [
            {"name": "kaka", "nik": "KKA-102378393"},
            {"name": "elonmusk", "nik": "MSK-384992949"},
            # Tambahkan pengguna baru di sini
            {"name": "nama_baru", "nik": "NIK-ANDA-DISINI"},
        ]
    ```

-   **Untuk mengubah agenda:**
    [cite_start]Cari fungsi `search_agenda` di dalam `class Ui` dan sesuaikan logikanya[cite: 1].
    ```python
    # class Ui(QtWidgets.QMainWindow):
    
        # ... (kode lainnya) ...
        
        # imagine if you use database
        def search_agenda(self, name):
            event = ""
            if name == 'kaka' :
                event = 'Jam 12:30 ngudud santai sek'
            if name == 'elonmusk':
                event = 'Jam 14:00 Membahas tentang pembayaran bitcoin'
            # Tambahkan agenda untuk pengguna baru di sini
            if name == 'nama_baru':
                event = 'Agenda untuk pengguna baru'
            return event
    ```

## 📚 Referensi & Kredit

Proyek ini merupakan pengembangan dan penyesuaian dari repositori awal oleh **fajarlabs-(https://youtu.be/UM1Z_8yi1iY?feature=shared)**.

-   [Raspberry Pi: Install OpenCV pada Python 3.7](https://yunusmuhammad007.medium.com/2-raspberry-pi-install-opencv-pada-python-3-7-menggunakan-pip3-a2504dffd984)
-   [Programmer Sought Article](https://programmersought.com/article/57453207651/)
-   [Tom's Hardware: Raspberry Pi Facial Recognition](https://www.tomshardware.com/how-to/raspberry-pi-facial-recognition)
-   https://github.com/fajarlabs/absensi_wajah/blob/master/demo.gif
```

---
### File `cara_training_foto.txt` (Versi Terbaru)

```text
# Alur Kerja Training Model Pengenalan Wajah

## 1. Clone Repositori
Mulai dengan meng-clone repositori dari GitHub:
git clone https://github.com/PigeonMonicaED/face-recognition-realtime.git
cd face-recognition-realtime


## 2. Pengambilan Foto (Capture)
Untuk mengambil sampel foto wajah sebelum melakukan training data, ketikkan perintah di bawah ini di terminal Anda.

Perintah ini akan membuat folder dengan nama yang Anda tentukan di dalam direktori 'dataset'.

python .\ambil_foto_wajah.py --folder_name=fajar --camera=0

--folder_name=[Isikan nama dari orang yang fotonya akan disimpan]
--camera=[Isikan dengan device ID kamera, indeks dimulai dari 0, 1, 2, dst.]


## 3. Training Model
Jika dataset foto sudah siap, selanjutnya jalankan perintah training.

python .\train_model.py

Perintah ini akan memproses semua gambar di folder 'dataset' dan menghasilkan file 'encodings.pickle'.


## 4. Menjalankan Aplikasi
Salin file 'encodings.pickle' yang dihasilkan dan pindahkan ke folder utama (satu folder dengan file GUI_attendance.py).

Terakhir, jalankan aplikasi utama:

python .\GUI_attendance.py
```
