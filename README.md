
from flask import Flask, request, jsonify

app = Flask(__name__)

# Database sementara
mahasiswa = []
krs = []
nilai = []
pembayaran = []


# 1. HALAMAN UTAMA
@app.route("/")
def home():
    return """
    <h1>APLIKASI DIGITAL KAMPUS</h1>
    <h3>Layanan Akademik Universitas</h3>
    <ul>
        <li>Pendaftaran Mahasiswa</li>
        <li>Pengisian KRS</li>
        <li>Pengumuman Nilai</li>
        <li>Pembayaran UKT</li>
    </ul>
    <p>Status aplikasi: Berjalan</p>
    """


# 2. PENDAFTARAN MAHASISWA
@app.route("/pendaftaran", methods=["POST"])
def pendaftaran():
    data = request.json

    mahasiswa.append({
        "nim": data["nim"],
        "nama": data["nama"],
        "jurusan": data["jurusan"]
    })

    return jsonify({
        "pesan": "Pendaftaran berhasil",
        "data": mahasiswa[-1]
    })


# 3. PENGISIAN KRS
@app.route("/krs", methods=["POST"])
def pengisian_krs():
    data = request.json

    krs.append({
        "nim": data["nim"],
        "mata_kuliah": data["mata_kuliah"],
        "semester": data["semester"]
    })

    return jsonify({
        "pesan": "Pengisian KRS berhasil",
        "data": krs[-1]
    })


# 4. PENGUMUMAN NILAI
@app.route("/nilai", methods=["POST"])
def pengumuman_nilai():
    data = request.json

    nilai.append({
        "nim": data["nim"],
        "mata_kuliah": data["mata_kuliah"],
        "nilai": data["nilai"]
    })

    return jsonify({
        "pesan": "Nilai berhasil disimpan",
        "data": nilai[-1]
    })


# 5. PEMBAYARAN UKT
@app.route("/ukt", methods=["POST"])
def pembayaran_ukt():
    data = request.json

    pembayaran.append({
        "nim": data["nim"],
        "jumlah": data["jumlah"],
        "status": "Berhasil"
    })

    return jsonify({
        "pesan": "Pembayaran UKT berhasil dicatat",
        "data": pembayaran[-1]
    })


# 6. MELIHAT SELURUH DATA
@app.route("/data", methods=["GET"])
def lihat_data():
    return jsonify({
        "mahasiswa": mahasiswa,
        "krs": krs,
        "nilai": nilai,
        "pembayaran": pembayaran
    })


# 7. PEMERIKSAAN KONDISI SERVER
@app.route("/health", methods=["GET"])
def health():
    return jsonify({
        "aplikasi": "Digital Kampus",
        "status": "Healthy",
        "server": "Berjalan"
    })


# 8. MENJALANKAN APLIKASI
if __name__ == "__main__":
    app.run(host="0.0.0.0", port=5000, debug=False)
