# Platform Hosting Gratis untuk Flask + MySQL

Karena InfinityFree tidak support Flask/Python, berikut alternatif platform hosting **GRATIS** yang mendukung Flask + MySQL:

## 🎯 Rekomendasi Terbaik (Gratis)

### 1. **PythonAnywhere** ⭐ (Paling Mudah)
- ✅ **Gratis** untuk starter plan
- ✅ Support Flask/Python
- ✅ Support MySQL (gratis)
- ✅ Support SQLite juga
- ✅ Mudah setup
- ✅ Web interface yang user-friendly
- **Website:** https://www.pythonanywhere.com
- **Limit:** 1 web app, 512MB storage, 1 CPU

### 2. **Railway** ⭐ (Auto-deploy dari GitHub)
- ✅ **Gratis** $5 credit/bulan
- ✅ Support Flask/Python
- ✅ Support MySQL (via addon)
- ✅ Auto-deploy dari GitHub
- ✅ Modern platform
- **Website:** https://railway.app
- **Limit:** $5 credit gratis/bulan

### 3. **Render** ⭐ (Auto-deploy dari GitHub)
- ✅ **Gratis** tier tersedia
- ✅ Support Flask/Python
- ✅ Support MySQL (via addon)
- ✅ Auto-deploy dari GitHub
- ✅ Reliable
- **Website:** https://render.com
- **Limit:** Free tier dengan beberapa limit

### 4. **Fly.io**
- ✅ **Gratis** tier
- ✅ Support Flask/Python
- ✅ Support MySQL
- ✅ Global edge network
- **Website:** https://fly.io

### 5. **Vercel** (Limited - perlu konfigurasi khusus)
- ⚠️ Lebih cocok untuk serverless
- Support Python tapi perlu konfigurasi khusus

---

## 🚀 Quick Setup Guide

### Opsi A: PythonAnywhere (Paling Mudah)

#### Langkah 1: Daftar
1. Kunjungi https://www.pythonanywhere.com
2. Daftar akun gratis
3. Verifikasi email

#### Langkah 2: Setup MySQL Database
1. Masuk ke dashboard
2. Klik tab **"Databases"**
3. Klik **"Create a new database"**
4. Pilih **MySQL**
5. Set password untuk database
6. Catat informasi:
   - Host: `username.mysql.pythonanywhere-services.com`
   - Username: `username`
   - Database name: `username$database_name`
   - Port: `3306`

#### Langkah 3: Upload Files
1. Klik tab **"Files"**
2. Upload semua file aplikasi
3. Atau clone dari GitHub:
   ```bash
   git clone https://github.com/username/repo.git
   ```

#### Langkah 4: Setup Virtual Environment
1. Buka **"Consoles"** tab
2. Buat virtual environment:
   ```bash
   cd ~/myproject
   python3.10 -m venv venv
   source venv/bin/activate
   pip install -r requirements.txt
   ```

#### Langkah 5: Konfigurasi Database di app.py
Edit `app.py`, set konfigurasi MySQL:
```python
DB_USER = 'username'  # Username PythonAnywhere Anda
DB_PASSWORD = 'password_database'  # Password yang Anda set
DB_HOST = 'username.mysql.pythonanywhere-services.com'
DB_PORT = '3306'
DB_NAME = 'username$database_name'  # Format: username$dbname
```

#### Langkah 6: Setup Web App
1. Klik tab **"Web"**
2. Klik **"Add a new web app"**
3. Pilih **"Manual configuration"**
4. Pilih Python version: **3.10**
5. Set source code: `/home/username/myproject`
6. Edit WSGI file:
   ```python
   import sys
   path = '/home/username/myproject'
   if path not in sys.path:
       sys.path.append(path)
   
   from app import app as application
   ```
7. Set environment variables (jika perlu)
8. Klik **"Reload"**

---

### Opsi B: Railway (Auto-deploy)

#### Langkah 1: Push ke GitHub
```bash
git init
git add .
git commit -m "Initial commit"
git remote add origin https://github.com/username/repo.git
git push -u origin main
```

#### Langkah 2: Setup di Railway
1. Kunjungi https://railway.app
2. Login dengan GitHub
3. Klik **"New Project"**
4. Pilih **"Deploy from GitHub repo"**
5. Pilih repository Anda
6. Railway akan auto-detect Flask

#### Langkah 3: Setup MySQL
1. Di project, klik **"+ New"**
2. Pilih **"Database"** → **"MySQL"**
3. Railway akan create MySQL database
4. Catat connection string

#### Langkah 4: Set Environment Variables
Di Railway project settings:
```
SECRET_KEY=your-secret-key-here
USE_MYSQL=true
DATABASE_URL=mysql+pymysql://user:pass@host:port/dbname
```

#### Langkah 5: Deploy
Railway akan otomatis deploy!

---

## 📝 Konfigurasi MySQL yang Mudah

Untuk memudahkan, saya sudah update `app.py` dengan konfigurasi MySQL yang mudah. Cukup edit bagian ini:

```python
# Di app.py, baris 23-27
DB_USER = 'username'  # Ganti dengan username MySQL Anda
DB_PASSWORD = 'password'  # Ganti dengan password MySQL Anda
DB_HOST = 'hostname'  # Ganti dengan host MySQL (contoh: username.mysql.pythonanywhere-services.com)
DB_PORT = '3306'  # Biasanya 3306
DB_NAME = 'database_name'  # Ganti dengan nama database
```

Atau gunakan environment variables:
```bash
export DB_USER='username'
export DB_PASSWORD='password'
export DB_HOST='hostname'
export DB_NAME='database_name'
export USE_MYSQL='true'
```

---

## ✅ Checklist Setup MySQL

- [ ] Database MySQL sudah dibuat
- [ ] Username dan password sudah dicatat
- [ ] Host dan port sudah diketahui
- [ ] Nama database sudah diketahui
- [ ] Konfigurasi di `app.py` sudah diupdate
- [ ] Test koneksi berhasil
- [ ] Tabel sudah dibuat (otomatis saat pertama run)

---

## 🔧 Troubleshooting

### Error: "Access denied"
- Pastikan username dan password benar
- Pastikan user memiliki privileges

### Error: "Unknown database"
- Pastikan database sudah dibuat
- Cek nama database (format PythonAnywhere: `username$dbname`)

### Error: "Can't connect"
- Cek host dan port
- Pastikan MySQL service berjalan
- Cek firewall settings

---

## 💡 Tips

1. **PythonAnywhere** adalah pilihan terbaik untuk pemula
2. **Railway** bagus jika sudah familiar dengan Git/GitHub
3. Gunakan **environment variables** untuk keamanan
4. **Backup database** secara berkala
5. Monitor **disk space** dan **usage**

---

## 🎓 Next Steps

1. Pilih platform hosting
2. Setup MySQL database
3. Update konfigurasi di `app.py`
4. Deploy aplikasi
5. Test semua fitur

Selamat hosting! 🚀

