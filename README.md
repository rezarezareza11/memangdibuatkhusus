<!DOCTYPE html>
<html lang="id">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>HAIIIIII, pasti ini Imellll</title>
    <style>
        body {
            font-family: Arial, sans-serif;
            background-color: #f4f4f9;
            display: flex;
            justify-content: center;
            align-items: center;
            height: 100vh;
            margin: 0;
            background-image: url('https://i.imgur.com/3QZQZQZ.png'); /* Gambar Dino Nailong */
            background-size: cover;
            background-repeat: repeat;
        }

        .container {
            text-align: center;
            background-color: rgba(255, 255, 255, 0.9); /* Latar belakang semi-transparan */
            padding: 20px;
            border-radius: 10px;
            box-shadow: 0 4px 8px rgba(0, 0, 0, 0.1);
            max-width: 400px;
            width: 100%;
        }

        h1 {
            color: #e91e63;
            margin-bottom: 20px;
        }

        .button-group {
            display: flex;
            gap: 10px;
            justify-content: center;
            margin-top: 20px;
        }

        button {
            background-color: #007bff;
            color: white;
            border: none;
            padding: 10px 20px;
            font-size: 16px;
            border-radius: 5px;
            cursor: pointer;
            transition: background-color 0.3s ease;
        }

        button:hover {
            background-color: #0056b3;
        }

        #yesBtn {
            background-color: #28a745;
        }

        #yesBtn:hover {
            background-color: #218838;
        }

        #noBtn {
            background-color: #dc3545;
        }

        #noBtn:hover {
            background-color: #c82333;
        }

        #notification {
            margin-top: 20px;
            font-size: 18px;
            color: #333;
        }

        /* Pop-up Styling */
        .popup {
            display: none;
            position: fixed;
            top: 50%;
            left: 50%;
            transform: translate(-50%, -50%);
            background-color: white;
            padding: 20px;
            border-radius: 10px;
            box-shadow: 0 4px 8px rgba(0, 0, 0, 0.2);
            z-index: 1000;
        }

        .popup-overlay {
            display: none;
            position: fixed;
            top: 0;
            left: 0;
            width: 100%;
            height: 100%;
            background-color: rgba(0, 0, 0, 0.5);
            z-index: 999;
        }

        .popup button {
            margin-top: 10px;
        }

        /* Tombol Tugas yang dinonaktifkan */
        #tugasBtn:disabled {
            background-color: #cccccc;
            cursor: not-allowed;
        }

        /* Sembunyikan tombol Mau dan Tidak secara default */
        #mauTidakGroup {
            display: none;
        }

        /* Iklan Shopee Palsu */
        .shopee-ad {
            background-color: #fff;
            border: 1px solid #ff5722;
            border-radius: 10px;
            padding: 15px;
            margin-top: 20px;
            text-align: left;
            box-shadow: 0 4px 8px rgba(0, 0, 0, 0.1);
            cursor: pointer;
            transition: transform 0.3s ease;
        }

        .shopee-ad:hover {
            transform: scale(1.02);
        }

        .shopee-ad img {
            width: 100%;
            border-radius: 10px;
        }

        .shopee-ad h3 {
            color: #ff5722;
            font-size: 18px;
            margin: 10px 0;
        }

        .shopee-ad p {
            font-size: 14px;
            color: #333;
        }

        .shopee-ad .price {
            font-size: 20px;
            color: #ff5722;
            font-weight: bold;
            margin: 10px 0;
        }

        .shopee-ad .cta {
            background-color: #ff5722;
            color: white;
            padding: 10px;
            text-align: center;
            border-radius: 5px;
            font-size: 16px;
        }
    </style>
</head>
<body>
    <div class="container">
        <h1>HAIIIIII, pasti ini Imellll</h1>
        <p>tolongin aku dongggggg pencett tombol durennn duluu</p>
        <div class="button-group">
            <button onclick="showPopup('Durian', '💖 Aku sangat menyukaimu! 💖')">Durian</button>
            <button id="tugasBtn" onclick="showPopup('Tugas', '🌟 Kamu sangat spesial bagiku! 🌟')" disabled>Tugas</button>
        </div>

        <!-- Tombol Mau atau Tidak (Awalnya disembunyikan) -->
        <div id="mauTidakGroup" style="margin-top: 30px;">
            <p>Apakah kamu mau menerima perasaanku?</p>
            <div class="button-group">
                <button id="yesBtn" onclick="respond('Mau')">Mau</button>
                <button id="noBtn" onclick="respond('Tidak')">Tidak</button>
            </div>
        </div>

        <!-- Notifikasi Jawaban -->
        <div id="notification"></div>

        <!-- Iklan Shopee Palsu -->
        <div class="shopee-ad" onclick="cekJawaban()">
            <img src="https://i.imgur.com/7QZQZQZ.jpg" alt="Sepatu Adidas Samba">
            <h3>Promo Spesial! Sepatu Adidas Samba</h3>
            <p>Dapatkan sepatu Adidas Samba dengan harga termurah hanya di Shopee!</p>
            <div class="price">Rp 1.299.000</div>
            <div class="cta">Beli Sekarang</div>
        </div>
    </div>

    <!-- Pop-up -->
    <div class="popup-overlay" id="popupOverlay"></div>
    <div class="popup" id="popup">
        <h2 id="popupTitle"></h2>
        <p id="popupMessage"></p>
        <button onclick="closePopup()">Tutup</button>
    </div>

    <script>
        // Fungsi untuk menampilkan pop-up
        function showPopup(title, message) {
            document.getElementById('popupTitle').textContent = title;
            document.getElementById('popupMessage').textContent = message;
            document.getElementById('popup').style.display = 'block';
            document.getElementById('popupOverlay').style.display = 'block';

            // Jika tombol Durian diklik, aktifkan tombol Tugas
            if (title === 'Durian') {
                document.getElementById('tugasBtn').disabled = false;
            }

            // Jika tombol Tugas diklik, tampilkan tombol Mau/Tidak
            if (title === 'Tugas') {
                document.getElementById('mauTidakGroup').style.display = 'block';
            }
        }

        // Fungsi untuk menutup pop-up
        function closePopup() {
            document.getElementById('popup').style.display = 'none';
            document.getElementById('popupOverlay').style.display = 'none';
        }

        // Fungsi untuk menangani jawaban "Mau" atau "Tidak"
        function respond(choice) {
            const notification = document.getElementById('notification');
            if (choice === 'Mau') {
                notification.textContent = "Yeay! Kamu memilih MAU! 😊";
                notification.style.color = "#28a745";
            } else {
                notification.textContent = "Yah, kamu memilih TIDAK. 😢";
                notification.style.color = "#dc3545";
            }

            // Simpan jawaban ke localStorage
            localStorage.setItem('jawabanImel', choice);
        }

        // Fungsi untuk mengecek jawaban yang disimpan di localStorage
        function cekJawaban() {
            const jawaban = localStorage.getItem('jawabanImel');
            if (jawaban) {
                alert(`Jawaban Imel: ${jawaban}`);
            } else {
                alert("Imel belum memilih.");
            }
        }
    </script>
</body>
</html>
