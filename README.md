<!DOCTYPE html>
<html lang="id">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Toko Online Digital</title>
    <style>
        /* CSS untuk styling */
        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
        }

        body {
            font-family: Arial, sans-serif;
            background: #f5f5f5;
            color: #333;
            padding: 20px;
        }

        header {
            background: #007bff;
            color: white;
            padding: 10px 0;
            text-align: center;
        }

        header h1 {
            margin: 0;
        }

        nav {
            display: flex;
            justify-content: center;
            gap: 20px;
            margin: 20px 0;
        }

        nav a {
            text-decoration: none;
            color: #007bff;
            font-weight: bold;
        }

        nav a:hover {
            text-decoration: underline;
        }

        .container {
            max-width: 1200px;
            margin: auto;
            display: grid;
            grid-template-columns: repeat(auto-fill, minmax(300px, 1fr));
            gap: 20px;
        }

        .product-card {
            background: white;
            padding: 15px;
            border-radius: 8px;
            box-shadow: 0 2px 10px rgba(0, 0, 0, 0.1);
        }

        .product-card img {
            width: 100%;
            border-radius: 8px;
        }

        .product-card h3 {
            margin: 10px 0;
        }

        .product-card p {
            font-size: 14px;
            color: #555;
        }

        .product-card .price {
            color: #e91e63;
            font-size: 18px;
            margin: 10px 0;
        }

        .btn {
            display: inline-block;
            padding: 10px 15px;
            background: #28a745;
            color: white;
            text-decoration: none;
            border-radius: 5px;
            text-align: center;
            cursor: pointer;
        }

        .btn:hover {
            background: #218838;
        }

        footer {
            text-align: center;
            margin-top: 30px;
            padding: 10px;
            background: #007bff;
            color: white;
        }

        /* Modal Formulir Pembelian */
        .modal {
            display: none;
            position: fixed;
            z-index: 1;
            left: 0;
            top: 0;
            width: 100%;
            height: 100%;
            background-color: rgba(0, 0, 0, 0.5);
        }

        .modal-content {
            background-color: #fff;
            margin: 10% auto;
            padding: 20px;
            border-radius: 8px;
            width: 50%;
        }

        .modal-content h2 {
            margin-bottom: 20px;
        }

        .form-group {
            margin-bottom: 15px;
        }

        .form-group label {
            display: block;
            margin-bottom: 5px;
        }

        .form-group input, .form-group textarea {
            width: 100%;
            padding: 8px;
            border: 1px solid #ccc;
            border-radius: 5px;
        }

        .close-btn {
            background: #dc3545;
        }

        .close-btn:hover {
            background: #c82333;
        }

        .confirmation {
            text-align: center;
            padding: 20px;
            background: #fff;
            border-radius: 8px;
            box-shadow: 0 2px 10px rgba(0, 0, 0, 0.1);
            display: none;
        }
    </style>
</head>
<body>

<header>
    <h1>Selamat Datang di Toko Online berbasis digital. dilarang berhutang</h1>
    <p>Temukan berbagai produk pilihan dengan harga terbaik!</p>
</header>

<nav>
    <a href="#">Beranda</a>
    <a href="#">Produk</a>
    <a href="#">Tentang Kami</a>
    <a href="#">Kontak</a>
</nav>

<div class="container">
    <div class="product-card">
        <img src="https://via.placeholder.com/300" alt="Produk 1">
        <h3>Produk 1</h3>
        <p>Deskripsi singkat tentang produk ini.</p>
        <p class="price">Rp 1000.000</p>
        <button class="btn" onclick="bukaForm('Produk 1', 'Rp 1000.000')">Beli Sekarang</button>
    </div>

    <div class="product-card">
        <img src="https://via.placeholder.com/300" alt="Produk 2">
        <h3>Produk 2</h3>
        <p>Deskripsi singkat tentang produk ini.</p>
        <p class="price">Rp 2000.000</p>
        <button class="btn" onclick="bukaForm('Produk 2', 'Rp 2000.000')">Beli Sekarang</button>
    </div>
</div>

<!-- Modal Formulir -->
<div id="formModal" class="modal">
    <div class="modal-content">
        <h2>Formulir Pembelian</h2>
        <form id="orderForm">
            <div class="form-group">
                <label>Produk</label>
                <input type="text" id="productName" readonly>
            </div>
            <div class="form-group">
                <label>Harga</label>
                <input type="text" id="productPrice" readonly>
            </div>
            <div class="form-group">
                <label>Nama Lengkap</label>
                <input type="text" id="customerName" required>
            </div>
            <div class="form-group">
                <label>Alamat Pengiriman</label>
                <textarea id="address" rows="3" required></textarea>
            </div>
            <div class="form-group">
                <label>No. Telepon</label>
                <input type="tel" id="phoneNumber" required>
            </div>
            <button type="button" class="btn" onclick="konfirmasiPesanan()">Konfirmasi Pesanan</button>
            <button type="button" class="btn close-btn" onclick="tutupForm()">Batal</button>
        </form>
    </div>
</div>

<!-- Konfirmasi Pesanan -->
<div id="confirmation" class="confirmation"></div>

<footer>
    <p>&copy; 2025 Toko Online. kami jamin keamanannya.</p>
</footer>

<script>
    function bukaForm(product, price) {
        document.getElementById('productName').value = product;
        document.getElementById('productPrice').value = price;
        document.getElementById('formModal').style.display = 'block';
    }

    function tutupForm() {
        document.getElementById('formModal').style.display = 'none';
    }

    function konfirmasiPesanan() {
        const nama = document.getElementById('customerName').value;
        const alamat = document.getElementById('address').value;
        const telepon = document.getElementById('phoneNumber').value;

        if (nama && alamat && telepon) {
            const pesan = `
                <h2>Pesanan Berhasil!</h2>
                <p>Terima kasih, <b>${nama}</b>!</p>
                <p>Pesanan Anda akan dikirim ke:</p>
                <p>${alamat}</p>
                <p>Nomor Telepon: ${telepon}</p>
            `;
            document.getElementById('confirmation').innerHTML = pesan;
            document.getElementById('confirmation').style.display = 'block';
            tutupForm();
        }
    }
</script>

</body>
</html>
