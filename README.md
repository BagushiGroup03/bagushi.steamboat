<!DOCTYPE html>
<html lang="ms">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Sistem Pesanan - Bagushi Steamboat & Grill</title>
    <style>
        body {
            font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
            background-color: #f8f9fa;
            margin: 0;
            padding: 20px;
            color: #333;
        }
        .container {
            max-width: 600px;
            margin: 0 auto;
            background: white;
            padding: 25px;
            border-radius: 12px;
            box-shadow: 0 4px 15px rgba(0,0,0,0.08);
        }
        h1 {
            text-align: center;
            color: #d9534f;
            margin-bottom: 5px;
        }
        p.subtitle {
            text-align: center;
            color: #666;
            margin-top: 0;
            margin-bottom: 25px;
        }
        .menu-item {
            display: flex;
            justify-content: space-between;
            align-items: center;
            padding: 15px 0;
            border-bottom: 1px solid #eee;
        }
        .menu-info h3 {
            margin: 0 0 5px 0;
            font-size: 1.1rem;
        }
        .menu-info span {
            color: #e67e22;
            font-weight: bold;
        }
        .counter-box {
            display: flex;
            align-items: center;
            gap: 10px;
        }
        button.btn-qty {
            background-color: #ddd;
            border: none;
            width: 30px;
            height: 30px;
            font-weight: bold;
            border-radius: 5px;
            cursor: pointer;
        }
        button.btn-qty:hover {
            background-color: #ccc;
        }
        .order-summary {
            margin-top: 25px;
            padding: 15px;
            background-color: #f1f8ff;
            border-radius: 8px;
        }
        .form-group {
            margin-bottom: 15px;
        }
        .form-group label {
            display: block;
            margin-bottom: 5px;
            font-weight: bold;
        }
        .form-group input {
            width: 100%;
            padding: 10px;
            box-sizing: border-box;
            border: 1px solid #ccc;
            border-radius: 5px;
        }
        .btn-submit {
            width: 100%;
            background-color: #27ae60;
            color: white;
            border: none;
            padding: 12px;
            font-size: 1rem;
            font-weight: bold;
            border-radius: 5px;
            cursor: pointer;
            margin-top: 10px;
        }
        .btn-submit:hover {
            background-color: #219653;
        }
    </style>
</head>
<body>

<div class="container">
    <h1>Bagushi Steamboat & Grill</h1>
    <p class="subtitle">Sistem Pesanan Meja Digital</p>

    <div class="form-group">
        <label for="namaPemesan">Nama Pelanggan:</label>
        <input type="text" id="namaPemesan" placeholder="Masukkan nama anda">
    </div>
    <div class="form-group">
        <label for="nomborMeja">Nombor Meja:</label>
        <input type="text" id="nomborMeja" placeholder="Cth: Meja 5">
    </div>

    <hr style="border: 0; border-top: 1px solid #eee; margin: 20px 0;">

    <h2>Menu Pilihan</h2>
    
    <!-- Item 1 -->
    <div class="menu-item">
        <div class="menu-info">
            <h3>Set Steamboat Regular</h3>
            <span>RM 25.00</span>
        </div>
        <div class="counter-box">
            <button class="btn-qty" onclick="ubahKuantiti('item1', -1)">-</button>
            <span id="qty-item1">0</span>
            <button class="btn-qty" onclick="ubahKuantiti('item1', 1)">+</button>
        </div>
    </div>

    <!-- Item 2 -->
    <div class="menu-item">
        <div class="menu-info">
            <h3>Set Grill Special</h3>
            <span>RM 32.00</span>
        </div>
        <div class="counter-box">
            <button class="btn-qty" onclick="ubahKuantiti('item2', -1)">-</button>
            <span id="qty-item2">0</span>
            <button class="btn-qty" onclick="ubahKuantiti('item2', 1)">+</button>
        </div>
    </div>

    <!-- Item 3 -->
    <div class="menu-item">
        <div class="menu-info">
            <h3>Ais Blended Coklat</h3>
            <span>RM 5.50</span>
        </div>
        <div class="counter-box">
            <button class="btn-qty" onclick="ubahKuantiti('item3', -1)">-</button>
            <span id="qty-item3">0</span>
            <button class="btn-qty" onclick="ubahKuantiti('item3', 1)">+</button>
        </div>
    </div>

    <!-- Ringkasan Pesanan -->
    <div class="order-summary">
        <h3>Jumlah Keseluruhan: RM <span id="totalHarga">0.00</span></h3>
        <button class="btn-submit" onclick="hantarPesanan()">Hantar Pesanan ke Dapur</button>
    </div>
</div>

<script>
    // Harga menu
    const hargaMenu = {
        item1: 25.00,
        item2: 32.00,
        item3: 5.50
    };

    // Kuantiti semasa
    let kuantiti = {
        item1: 0,
        item2: 0,
        item3: 0
    };

    function ubahKuantiti(idItem, nilai) {
        kuantiti[idItem] += nilai;
        if (kuantiti[idItem] < 0) {
            kuantiti[idItem] = 0;
        }
        
        // Papar kuantiti baru
        document.getElementById('qty-' + idItem).innerText = kuantiti[idItem];
        
        // Kira semula jumlah harga
        kiraTotal();
    }

    function kiraTotal() {
        let total = (kuantiti.item1 * hargaMenu.item1) + 
                    (kuantiti.item2 * hargaMenu.item2) + 
                    (kuantiti.item3 * hargaMenu.item3);
        
        document.getElementById('totalHarga').innerText = total.toFixed(2);
    }

    function hantarPesanan() {
        let nama = document.getElementById('namaPemesan').value;
        let meja = document.getElementById('nomborMeja').value;
        let total = document.getElementById('totalHarga').innerText;

        if (!nama || !meja) {
            alert('Sila masukkan Nama dan Nombor Meja terlebih dahulu!');
            return;
        }

        if (total == "0.00") {
            alert('Sila pilih sekurang-kurangnya satu menu!');
            return;
        }

        alert(`Terima kasih, ${nama} (${meja})! Pesanan anda bernilai RM${total} telah berjaya dihantar ke dapur.`);
    }
</script>

</body>
</html>