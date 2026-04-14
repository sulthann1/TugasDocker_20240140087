# MY Website — Tugas Deploy Pertemuan 6

Aplikasi web sederhana berbasis **Spring Boot** dengan **Thymeleaf** untuk manajemen data mahasiswa. Dibuat sebagai tugas mata kuliah Deployment Perangkat Lunak.

---

## Teknologi yang Digunakan

| Teknologi | Versi | Keterangan |
|---|---|---|
| Java | 25 | Bahasa pemrograman utama |
| Spring Boot | 4.0.5 | Framework aplikasi web |
| Spring Web | - | Untuk routing dan REST/MVC |
| Thymeleaf | - | Template engine HTML |
| Lombok | - | Mengurangi boilerplate code |
| Maven | - | Build tool & dependency manager |
| Docker | - | Containerisasi aplikasi |

---

## Struktur Project

```
deploy/
├── src/
│   └── main/
│       ├── java/
│       │   └── com/tugas/deploy/
│       │       ├── controller/
│       │       │   └── UserController.java   # Handler routing halaman
│       │       ├── model/
│       │       │   └── User.java             # Model data mahasiswa
│       │       └── DeployApplication.java    # Main class Spring Boot
│       └── resources/
│           └── templates/
│               ├── home.html                 # Halaman utama & tabel data
│               └── form.html                 # Halaman form input mahasiswa
├── Dockerfile                                # Konfigurasi Docker image
├── pom.xml                                   # Dependency Maven
└── README.md
```

---

## Fitur Aplikasi

- **Halaman Home** — menampilkan tabel daftar data mahasiswa
- **Halaman Form** — input data mahasiswa (nama, NIM, jenis kelamin)
- **Data Temporary** — data disimpan di memori aplikasi, tidak menggunakan database
- **Navigasi** — tombol input data dan kembali ke home

---

## Cara Menjalankan

### 1. Menjalankan Lokal (tanpa Docker)

**Prasyarat:** Java 25, Maven terinstall

```bash
# Clone repository
git clone https://github.com/<username>/<repo-name>.git
cd deploy

# Build project
mvn clean package

# Jalankan aplikasi
java -jar target/deploy-0.0.1-SNAPSHOT.jar
```

Akses aplikasi di browser: [http://localhost:8080](http://localhost:8080)

---

### 2. Menjalankan dengan Docker

**Prasyarat:** Docker Desktop terinstall

#### Build image secara manual

```bash
# Build JAR terlebih dahulu
mvn clean package

# Build Docker image
docker build -t tugas-<NIM>:1.0 .

# Jalankan container
docker run -p 8080:8080 tugas-<NIM>:1.0
```

#### Pull image dari Docker Hub

```bash
# Pull image
docker pull <username-docker>/<nama-image>:1.0

# Jalankan container
docker run -p 8080:8080 <username-docker>/<nama-image>:1.0
```

Akses aplikasi di browser: [http://localhost:8080](http://localhost:8080)

---

## Alur Aplikasi

```
Buka Aplikasi
     │
     ▼
  Halaman Home  ◄──────────────────┐
     │                             │
     │  Klik "+ Input Data"        │ Submit berhasil
     ▼                             │
  Halaman Form ──────────────────►─┘
```

---

## Endpoint

| Method | URL | Keterangan |
|---|---|---|
| `GET` | `/` | Redirect ke `/home` |
| `GET` | `/home` | Menampilkan halaman home & tabel data |
| `GET` | `/form` | Menampilkan form input mahasiswa |
| `POST` | `/form` | Menyimpan data mahasiswa (temporary) |

---

## Model Data

**User** (`com.tugas.deploy.model.User`)

| Field | Tipe | Keterangan |
|---|---|---|
| `nama` | String | Nama lengkap mahasiswa |
| `nim` | String | Nomor Induk Mahasiswa |
| `jenisKelamin` | String | `Laki-laki` atau `Perempuan` |

---

## Dockerfile

```dockerfile
FROM eclipse-temurin:25-jdk
ARG JAR_FILE=target/*.jar
COPY ./target/deploy-0.0.1-SNAPSHOT.jar app.jar
ENTRYPOINT ["java","-jar","/app.jar"]
EXPOSE 8080
```

---

## Cara Push Image ke Docker Hub

```bash
# Login ke Docker Hub
docker login

# Tag image sesuai format
docker tag tugas-<NIM>:1.0 <username-docker>/tugas-<NIM>:1.0

# Push ke Docker Hub
docker push <username-docker>/tugas-<NIM>:1.0
```

---
##Screenshot
Halaman Login Page Saya
<img width="1920" height="1080" alt="Screenshot (222)" src="https://github.com/user-attachments/assets/774611d9-16e0-4487-becb-66b0b8edb77d" />

Halaman Home Saya
<img width="1920" height="1080" alt="Screenshot (223)" src="https://github.com/user-attachments/assets/446b609d-022d-4502-8d82-1512899869c4" />

Halaman Form Saya
<img width="1920" height="1080" alt="Screenshot (226)" src="https://github.com/user-attachments/assets/78e30248-f027-4b1a-915e-d346b9df1440" />

Halaman Form Setelah Submit
<img width="1920" height="1080" alt="Screenshot (227)" src="https://github.com/user-attachments/assets/8e03f2c1-8c72-419c-b4dc-8106e5d42a9e" />

Halaman Login Page Shahky
<img width="1920" height="1080" alt="Screenshot (234)" src="https://github.com/user-attachments/assets/3ec8bab5-5423-40e6-8ff7-02abc1f23828" />

Halaman Home Shahky
<img width="1920" height="1080" alt="Screenshot (229)" src="https://github.com/user-attachments/assets/38f445ff-4caa-4dfa-834a-8c6e2de96671" />

Halaman Form Shahky
<img width="1920" height="1080" alt="Screenshot (229)" src="https://github.com/user-attachments/assets/18875655-b63e-4f0c-8fc3-6357fcd51d8c" />

Halaman Home Setelah Submit Shahky
<img width="1920" height="1080" alt="Screenshot (231)" src="https://github.com/user-attachments/assets/20a3aefc-abbd-432e-8088-7a8a991f94a7" />

Screenshot Image
<img width="1920" height="1080" alt="Screenshot (232)" src="https://github.com/user-attachments/assets/cb32ae96-d177-4cec-aeae-20a1da307554" />

Screenshot Container
<img width="1920" height="1080" alt="Screenshot (232)" src="https://github.com/user-attachments/assets/71e7a5f2-cb67-49e2-92dd-9f57cc555500" />

## Informasi Mahasiswa

| | |
|---|---|
| **Nama** | _Sulthan Awaliya_ |
| **NIM** | _20240140087_ |
| **Kelas** | _B_ |
| **Mata Kuliah** | Deployment Perangkat Lunak |
| **Pertemuan** | 6 — Deploy dengan Docker |
