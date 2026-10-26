# Meteor Defense

Mini game 3D berbasis browser yang dibuat menggunakan Three.js. Proyek ini disusun untuk memenuhi tugas Evaluasi Tengah Semester (ETS) mata kuliah Grafika Komputer dengan topik **Meteor Defense**.

Demo: https://salwonu.github.io/UTS_Grafkom/

## Identitas Kelompok

| Nama | NRP |
|---|---|
| Nadine Aulia Putri Fanani | 5025231206 |
| Salwa Fitri Fadiyah Hanan | 5025231220 |

## Deskripsi Proyek

Meteor Defense adalah game pertahanan planet. Pemain mengendalikan turret di permukaan planet untuk menembak meteor yang datang dari luar angkasa. Pemain harus bertahan dari 5 wave meteor dan mengalahkan boss pada wave terakhir. Game dinyatakan kalah apabila integritas planet habis, dan menang apabila seluruh wave beserta boss berhasil diselesaikan.

Selama permainan, pemain mengumpulkan credits dari meteor yang dihancurkan. Credits tersebut dapat ditukar dengan upgrade di bengkel yang muncul setiap pergantian wave.

## Teknologi

- JavaScript (ES Module)
- Three.js r160
- HTML dan CSS
- Aset model 3D format GLB (glTF)

## Cara Menjalankan

Proyek ini harus dijalankan melalui web server lokal. Membuka `index.html` secara langsung dengan klik dua kali tidak dapat dilakukan karena browser memblokir pemuatan file GLB dari `file://`. Selain itu, diperlukan koneksi internet karena Three.js dimuat dari CDN (unpkg).

**Menggunakan Live Server (VS Code)**
1. Buka folder proyek di VS Code.
2. Klik kanan pada `index.html`, lalu pilih *Open with Live Server*.

**Menggunakan Python**
1. Buka terminal pada folder proyek.
2. Jalankan perintah `python -m http.server 8000`.
3. Buka `http://localhost:8000` pada browser.

Struktur folder:

```
ets_grafkom/
├── index.html
├── README.md
└── assets/
    └── turret.glb
```

Apabila `assets/turret.glb` tidak ditemukan, game tetap berjalan menggunakan turret sederhana yang dibuat dari kode.

## Kontrol dan Interaksi

| Input | Fungsi |
|---|---|
| Klik kiri pada meteor | Menembakkan laser ke target |
| Tahan Spasi | Mengaktifkan shield (menggunakan energi) |
| E | Mengaktifkan EMP Shockwave (cooldown 15 detik) |
| Gerak mouse | Menggeser sudut kamera |
| Scroll | Zoom in dan zoom out |
| Klik orb | Mengambil power-up |
| Klik satelit | Menghancurkan satelit untuk mendapat orb |
| Tombol 1 sampai 4 atau klik | Membeli upgrade di bengkel |
| Enter | Melanjutkan ke wave berikutnya |

## Mekanisme Permainan

**Objective.** Bertahan dari 5 wave meteor dan mengalahkan boss pada wave terakhir.

**Kondisi menang dan kalah.** Pemain kalah jika integritas planet mencapai nol. Pemain menang jika wave 5 beserta boss berhasil dihancurkan. Setelah itu, tombol *Main Lagi* akan mengatur ulang seluruh kondisi permainan.

**Jenis meteor.**

| Jenis | Karakteristik |
|---|---|
| Biasa | Ukuran kecil, hancur dengan satu tembakan |
| Cepat | Bergerak dua kali lebih cepat |
| Pecah | Terpecah menjadi dua meteor kecil saat hancur |
| Besar | Membutuhkan beberapa tembakan, damage ke planet lebih besar |
| Boss | Muncul di wave 5, memiliki HP besar, dan tidak dapat ditahan shield |

**Bengkel.** Credits dapat ditukar dengan peningkatan damage, fire rate, kapasitas shield, dan perbaikan planet.

**Power-up.** Terdapat enam jenis orb: Slow-Mo, Rapid Fire, Triple Shot, Repair, Nova Bomb, dan Overcharge Shield.

**Combo.** Menghancurkan meteor secara berurutan dalam waktu singkat meningkatkan pengali skor. Combo kembali ke awal apabila planet terkena meteor.

## Pemenuhan Requirement Tugas

| Requirement | Implementasi |
|---|---|
| Scene utama, camera, renderer, ground/environment | `PerspectiveCamera`, `WebGLRenderer`, planet sebagai permukaan pertahanan, serta starfield |
| Minimal 3 jenis object | Planet, bulan, sabuk asteroid, meteor, satelit, orb power-up, dan turret |
| Scene graph parent-child | `station` berisi `planet` dan `turret`; `planet` berisi `atmosphere`; `turret` berisi `head`; `moonPivot` berisi `moon` |
| Aset GLTF/GLB | Model turret (`assets/turret.glb`) dimuat menggunakan `GLTFLoader` |
| Material PBR | `MeshStandardMaterial` pada planet, bulan, meteor, turret, satelit, dan orb |
| Minimal dua light | `AmbientLight`, `DirectionalLight` (sumber bayangan), `PointLight` (rim light), serta pool `PointLight` untuk efek ledakan |
| Cast dan receive shadow | `DirectionalLight` dengan shadow map 2048; planet, bulan, meteor, dan turret meng-cast shadow, planet dan bulan juga receive shadow |
| Environment | Starfield procedural, `FogExp2`, dan environment map (`RoomEnvironment`) untuk pantulan material logam |
| Minimal 2 animasi | Rotasi planet, orbit bulan, rotasi sabuk asteroid, orbit satelit, orb yang melayang, rotasi dan gerak meteor, serta animasi partikel |
| Minimal 3 interaksi dan `THREE.Raycaster` | Menembak target dan highlight saat hover (Raycaster), shield, EMP, zoom kamera, pembelian upgrade, serta pengambilan orb |
| Feedback visual dan minimal 2 VFX | Partikel ledakan, laser, trail meteor, shield glow, gelombang EMP, debris, glow atmosfer, dan cahaya ledakan |
| Camera dan UI/HUD | HUD berisi wave, skor, credits, combo, bar integritas planet, energi shield, cooldown EMP, serta status buff |
| Objective, win/lose, dan restart | Tujuan ditampilkan di HUD, tersedia layar menang dan kalah, serta tombol Main Lagi |

## Asset Credits

- Three.js, hak cipta para kontributor three.js, lisensi MIT, https://threejs.org
- Model turret: "Tower Defense Kit" oleh Kenney (kenney.nl), lisensi CC0 1.0, https://kenney-assets.itch.io/tower-defense-kit
- Tekstur planet, meteor, bulan, satelit, efek visual, UI/HUD, serta seluruh kode game dibuat oleh kelompok.

## Pembagian Tugas

- Nadine bertugas untuk membuat kode di awal serta mencari asset.
- Salwa bertugas untuk mengubah dan menambahkan kode, serta mendeploy program

| Nama | Kontribusi |
|---|---|
| Nadine Aulia Putri Fanani | Membuat kode di awal dan mencari asset untuk object |
| Salwa Fitri Fadiyah Hanan | Mengubah dan menambahkan beberapa kode serta mendeploy program |
