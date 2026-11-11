<!DOCTYPE html>
<html lang="ms">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Bagushi Steamboat & Grill Changlun</title>
    <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.4.0/css/all.min.css">
    <style>
        * {
            box-sizing: border-box;
            font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
            margin: 0;
            padding: 0;
        }

        body {
            background-color: #f0f2f5;
            display: flex;
            justify-content: center;
            align-items: center;
            min-height: 100vh;
            color: #333;
        }

        /* Mobile App Frame Container */
        .app-screen {
            width: 100%;
            max-width: 414px;
            height: 736px;
            background-color: #fff;
            border-radius: 20px;
            box-shadow: 0 10px 25px rgba(0,0,0,0.15);
            overflow: hidden;
            position: relative;
            display: flex;
            flex-direction: column;
        }

        /* View Pages Controller */
        .page {
            display: none;
            flex-direction: column;
            width: 100%;
            height: 100%;
            padding: 20px;
            overflow-y: auto;
            position: absolute;
            top: 0;
            left: 0;
            background: #fff;
            box-sizing: border-box;
        }

        .page.active {
            display: flex;
        }

        /* Header Components */
        .top-bar {
            display: flex;
            justify-content: space-between;
            align-items: center;
            padding-bottom: 15px;
            margin-bottom: 15px;
            border-bottom: 1px solid #eee;
        }

        .top-bar i {
            font-size: 1.2rem;
            cursor: pointer;
            color: #555;
        }

        .header-title {
            font-weight: bold;
            font-size: 1.1rem;
        }

        /* Common Elements */
        .img-header {
            width: 100%;
            height: 180px;
            object-fit: cover;
            border-radius: 12px;
            margin-bottom: 20px;
            background-color: #e0e0e0;
        }

        .title-large {
            font-size: 1.4rem;
            font-weight: 800;
            text-align: center;
            text-transform: uppercase;
            margin-bottom: 10px;
            color: #222;
        }

        .subtitle {
            text-align: center;
            color: #666;
            margin-bottom: 25px;
            font-size: 0.95rem;
        }

        .btn-primary {
            background-color: #222;
            color: white;
            border: none;
            padding: 14px;
            border-radius: 10px;
            font-weight: bold;
            width: 100%;
            cursor: pointer;
            text-align: center;
            margin-top: auto;
            font-size: 1rem;
            transition: 0.2s;
        }

        .btn-primary:hover {
            background-color: #444;
        }

        .form-input {
            width: 100%;
            padding: 12px;
            margin-bottom: 15px;
            border: 1px solid #ccc;
            border-radius: 8px;
            box-sizing: border-box;
        }

        /* Page Specific UI Customizations */
        
        /* Page 4 & 5 Grid Styles */
        .category-card {
            display: flex;
            align-items: center;
            justify-content: space-between;
            border: 1.5px solid #222;
            border-radius: 12px;
            padding: 15px;
            margin-bottom: 12px;
            cursor: pointer;
            font-weight: bold;
        }

        .grid-2x2 {
            display: grid;
            grid-template-columns: 1fr 1fr;
            gap: 15px;
            margin-bottom: 15px;
        }

        .product-card {
            border: 1px solid #eee;
            border-radius: 10px;
            padding: 10px;
            background: #fafafa;
            position: relative;
            cursor: pointer;
        }

        .product-card img {
            width: 100%;
            height: 100px;
            object-fit: cover;
            border-radius: 8px;
            background: #e0e0e0;
        }

        .heart-icon {
            position: absolute;
            top: 15px;
            right: 15px;
            color: #888;
        }

        /* Cart Page 7 */
        .cart-item {
            display: flex;
            align-items: center;
            gap: 12px;
            margin-bottom: 15px;
            border-bottom: 1px solid #eee;
            padding-bottom: 12px;
        }

        .cart-item img {
            width: 60px;
            height: 60px;
            border-radius: 8px;
            object-fit: cover;
        }

        .qty-controls {
            display: flex;
            align-items: center;
            gap: 8px;
            border: 1px solid #ccc;
            border-radius: 6px;
            padding: 2px 8px;
        }

        .qty-btn {
            background: none;
            border: none;
            font-size: 1.1rem;
            cursor: pointer;
            padding: 0 4px;
        }

        /* Status Page 8 */
        .status-timeline {
            display: flex;
            flex-direction: column;
            gap: 30px;
            margin: 40px 20px;
            position: relative;
        }

        .status-node {
            display: flex;
            align-items: center;
            gap: 15px;
            font-weight: bold;
            font-size: 1.1rem;
        }

        .circle {
            width: 24px;
            height: 24px;
            border-radius: 50%;
            border: 2px solid #222;
            background: #fff;
        }

        .circle.filled {
            background: #222;
        }

        /* Admin Orders Table (Page 9) */
        table {
            width: 100%;
            border-collapse: collapse;
            font-size: 0.85rem;
            margin-top: 10px;
        }

        th, td {
            border: 1px solid #ddd;
            padding: 8px;
            text-align: center;
        }

        th {
            background-color: #f2f2f2;
        }

        .badge {
            padding: 3px 6px;
            border-radius: 4px;
            font-size: 0.75rem;
        }
        .badge-done { background: #d4edda; color: #155724; }
        .badge-progress { background: #fff3cd; color: #856404; }
        .badge-pending { background: #f8d7da; color: #721c24; }
    </style>
</head>
<body>

<div class="app-screen">

    <!-- PAGE 1: Welcome Screen -->
    <div id="page1" class="page active">
        <div class="top-bar">
            <i class="fa-solid fa-bars"></i>
            <div>
                <i class="fa-regular fa-bell"></i> &nbsp;
                <i class="fa-solid fa-share-nodes"></i> &nbsp;
                <i class="fa-solid fa-magnifying-glass"></i>
            </div>
        </div>
        <!-- Gambar Utama Kedai Bagushi Steamboat & Grill -->
        <img src="https://lh3.googleusercontent.com/d/10Tz-aT0t0e13P3y0vN-7Y79t5A3U1O9=" class="img-header" alt="Bagushi Steamboat & Grill Logo/Plang" onerror="this.src='https://via.placeholder.com/400x200?text=Bagushi+Steamboat+%26+Grill'">
        <h1 class="title-large">BAGUSHI STEAMBOAT & GRILL CHANGLUN</h1>
        <p class="subtitle">Sistem Pesanan Digital & Layanan Pantas</p>
        <button class="btn-primary" onclick="goToPage(2)">Next</button>
    </div>

    <!-- PAGE 2: Login / Register Form -->
    <div id="page2" class="page">
        <div class="top-bar">
            <i class="fa-solid fa-bars"></i>
            <div>
                <i class="fa-regular fa-bell"></i> &nbsp;
                <i class="fa-solid fa-share-nodes"></i> &nbsp;
                <i class="fa-solid fa-magnifying-glass"></i>
            </div>
        </div>
        <h1 class="title-large">BAGUSHI STEAMBOAT & GRILL CHANGLUN</h1>
        <p class="subtitle">Log Masuk Pelanggan</p>
        
        <input type="text" class="form-input" placeholder="Nama / Emel">
        <input type="password" class="form-input" placeholder="Kata Laluan">
        
        <button class="btn-primary" style="margin-top: 10px;" onclick="goToPage(3)">Sign In</button>
        <div style="text-align: center; margin-top: 15px;">
            <small onclick="goToPage(9)" style="cursor: pointer; text-decoration: underline; color: #666;">(Akses Pekerja/Dapur - Page 9)</small>
        </div>
    </div>

    <!-- PAGE 3: Confirm Table Number -->
    <div id="page3" class="page">
        <div class="top-bar">
            <i class="fa-solid fa-bars"></i>
            <div>
                <i class="fa-regular fa-bell"></i> &nbsp;
                <i class="fa-solid fa-share-nodes"></i> &nbsp;
                <i class="fa-solid fa-magnifying-glass"></i>
            </div>
        </div>
        <img src="https://lh3.googleusercontent.com/d/10Tz-aT0t0e13P3y0vN-7Y79t5A3U1O9=" class="img-header" alt="Bagushi Steamboat" onerror="this.src='https://via.placeholder.com/400x200?text=Bagushi+Steamboat'">
        <h2 class="title-large">PILIH MEJA</h2>
        <p class="subtitle">Please confirm your table number to view the menu.</p>
        
        <select id="selectMeja" class="form-input" style="font-weight: bold;">
            <option value="">-- Pilih Nombor Meja --</option>
            <option value="Meja 01">Meja 01</option>
            <option value="Meja 02">Meja 02</option>
            <option value="Meja 05">Meja 05</option>
            <option value="Meja 08">Meja 08</option>
            <option value="Meja 12">Meja 12</option>
        </select>
        
        <button class="btn-primary" onclick="confirmTable()">View Menu</button>
    </div>

    <!-- PAGE 4: Main Categories / Recommendations -->
    <div id="page4" class="page">
        <div class="top-bar">
            <span style="font-size:0.8rem; color:#666;">Recent</span>
            <i class="fa-solid fa-cart-shopping" onclick="goToPage(7)" style="font-size:1.3rem;"></i>
        </div>
        <input type="text" class="form-input" placeholder="🔍 Search menu...">
        
        <p style="font-weight: bold; margin-bottom: 10px;">Suggestions</p>
        <div class="category-card" onclick="goToPage(5)">
            <span>Best Sellers</span>
            <i class="fa-solid fa-chevron-right"></i>
        </div>
        <div class="category-card" onclick="goToPage(5)">
            <span>Set Steamboat & Grill</span>
            <i class="fa-solid fa-chevron-right"></i>
        </div>
        <div class="category-card" onclick="goToPage(5)">
            <span>Daging & Seafood</span>
            <i class="fa-solid fa-chevron-right"></i>
        </div>
        <div class="category-card" onclick="goToPage(5)">
            <span>Minuman & Pencuci Mulut</span>
            <i class="fa-solid fa-chevron-right"></i>
        </div>
    </div>

    <!-- PAGE 5: Food Categories Grid -->
    <div id="page5" class="page">
        <div class="top-bar">
            <div style="display:flex; align-items:center; gap:8px;">
                <i class="fa-solid fa-chevron-left" onclick="goToPage(4)"></i>
                <span class="header-title">Food Categories</span>
            </div>
            <div>
                <i class="fa-solid fa-magnifying-glass"></i> &nbsp;
                <i class="fa-regular fa-user"></i> &nbsp;
                <i class="fa-solid fa-bag-shopping" onclick="goToPage(7)"></i>
            </div>
        </div>

        <div class="grid-2x2">
            <div class="product-card" onclick="goToPage(6)">
                <i class="fa-regular fa-heart heart-icon"></i>
                <img src="https://via.placeholder.com/150?text=Sliced+Beef" alt="Sliced Beef">
                <p style="font-weight: bold; margin-top: 5px;">Sliced Beef</p>
                <small>RM 12.00</small>
            </div>
            <div class="product-card" onclick="goToPage(6)">
                <i class="fa-regular fa-heart heart-icon"></i>
                <img src="https://via.placeholder.com/150?text=Marinated+Chicken" alt="Chicken">
                <p style="font-weight: bold; margin-top: 5px;">Chicken Slice</p>
                <small>RM 10.00</small>
            </div>
            <div class="product-card" onclick="goToPage(6)">
                <i class="fa-regular fa-heart heart-icon"></i>
                <img src="https://via.placeholder.com/150?text=Fishball+Combo" alt="Fishball">
                <p style="font-weight: bold; margin-top: 5px;">Fishball Combo</p>
                <small>RM 8.00</small>
            </div>
            <div class="product-card" onclick="goToPage(6)">
                <i class="fa-regular fa-heart heart-icon"></i>
                <img src="https://via.placeholder.com/150?text=Prawns+Fresh" alt="Prawns">
                <p style="font-weight: bold; margin-top: 5px;">Fresh Prawns</p>
                <small>RM 15.00</small>
            </div>
        </div>

        <div style="text-align: center; margin-top: 10px;">
            <small style="color:#777;">Showing 4 out of 10</small><br><br>
            <button class="btn-primary" style="width: auto; padding: 8px 25px;" onclick="goToPage(7)">Go to Cart</button>
        </div>
    </div>

    <!-- PAGE 6: Product Detail & Special Request -->
    <div id="page6" class="page">
        <div class="top-bar">
            <i class="fa-solid fa-bars"></i>
            <div>
                <i class="fa-solid fa-magnifying-glass"></i> &nbsp;
                <i class="fa-regular fa-user"></i> &nbsp;
                <i class="fa-solid fa-bag-shopping" onclick="goToPage(7)"></i>
            </div>
        </div>

        <h2 style="margin-bottom: 10px;">Sliced Beef Premium</h2>
        <div style="position: relative;">
            <img src="https://via.placeholder.com/350x200?text=Sliced+Beef+Premium" class="img-header" style="height: 200px;">
            <i class="fa-regular fa-heart heart-icon" style="font-size: 1.3rem;"></i>
        </div>

        <p style="font-weight: bold; font-size: 1.1rem; margin-bottom: 5px;">Price: RM 12.00</p>
        <p style="margin-bottom: 15px;">Quantity: 1 Set</p>

        <label style="font-weight: bold; display: block; margin-bottom: 5px;">Special Request:</label>
        <input type="text" class="form-input" placeholder="Cth: Kurangkan pedas / Ekstra kuah">

        <button class="btn-primary" onclick="addToCart()">Add to Cart</button>

        <hr style="margin: 20px 0; border: 0; border-top: 1px solid #eee;">
        <p style="font-weight: bold;">Feature Title</p>
        <div style="display: flex; gap: 10px; align-items: center; margin-top: 10px;">
            <img src="https://via.placeholder.com/50" style="border-radius: 5px;">
            <div>
                <small style="font-weight: bold;">Ulasan Pelanggan</small><br>
                <small>⭐⭐⭐⭐⭐ (5/5)</small>
            </div>
        </div>
    </div>

    <!-- PAGE 7: My Cart & Checkout -->
    <div id="page7" class="page">
        <h2 style="margin-bottom: 20px;">My cart</h2>

        <div class="cart-item">
            <img src="https://via.placeholder.com/60?text=Beef">
            <div style="flex:1;">
                <p style="font-weight: bold; font-size: 0.9rem;">Sliced Beef</p>
                <small style="color:#666;">RM 12.00</small>
            </div>
            <div class="qty-controls">
                <button class="qty-btn">-</button>
                <span>1</span>
                <button class="qty-btn">+</button>
            </div>
            <i class="fa-regular fa-trash-can" style="color: #999; cursor: pointer;"></i>
        </div>

        <div class="cart-item">
            <img src="https://via.placeholder.com/60?text=Chicken">
            <div style="flex:1;">
                <p style="font-weight: bold; font-size: 0.9rem;">Chicken Slice</p>
                <small style="color:#666;">RM 20.00 (x2)</small>
            </div>
            <div class="qty-controls">
                <button class="qty-btn">-</button>
                <span>2</span>
                <button class="qty-btn">+</button>
            </div>
            <i class="fa-regular fa-trash-can" style="color: #999; cursor: pointer;"></i>
        </div>

        <div style="margin-top: auto; padding-top: 15px; border-top: 1px solid #eee;">
            <div style="display: flex; justify-content: space-between; font-weight: bold; font-size: 1.1rem; margin-bottom: 15px;">
                <span>Total</span>
                <span>RM 32.00</span>
            </div>
            <button class="btn-primary" onclick="goToPage(8)">Checkout</button>
        </div>
    </div>

    <!-- PAGE 8: Customer Order Status -->
    <div id="page8" class="page">
        <div style="display: flex; align-items: center; gap: 10px; margin-bottom: 20px;">
            <i class="fa-solid fa-chevron-left" onclick="goToPage(7)"></i>
            <h2 class="header-title" style="font-size: 1.2rem;">Order Status</h2>
        </div>

        <div class="status-timeline">
            <div class="status-node">
                <div class="circle filled"></div>
                <span>Order Received</span>
            </div>
            <div class="status-node">
                <div class="circle"></div>
                <span style="color: #888;">Preparing</span>
            </div>
            <div class="status-node">
                <div class="circle"></div>
                <span style="color: #888;">Ready to Serve</span>
            </div>
        </div>

        <div style="text-align: center; margin-top: auto;">
            <p style="font-size: 0.85rem; color: #666; margin-bottom: 15px;">Pesanan anda sedang diproses oleh dapur Bagushi.</p>
            <button class="btn-primary" onclick="goToPage(9)">Ke Halaman Pentadbir (Page 9)</button>
        </div>
    </div>

    <!-- PAGE 9: Kitchen / Incoming Orders Dashboard -->
    <div id="page9" class="page">
        <div style="display: flex; align-items: center; gap: 10px; margin-bottom: 15px;">
            <i class="fa-solid fa-chevron-left" onclick="goToPage(1)"></i>
            <h2 class="header-title">Incoming Orders</h2>
        </div>

        <div style="display: flex; gap: 5px; margin-bottom: 15px;">
            <button class="btn-primary" style="padding: 6px; font-size:0.75rem;">All (3)</button>
            <button class="btn-primary" style="padding: 6px; font-size:0.75rem; background:#888;">Preparing (2)</button>
            <button class="btn-primary" style="padding: 6px; font-size:0.75rem; background:#888;">Ready (1)</button>
        </div>

        <table>
            <thead>
                <tr>
                    <th>Table No.</th>
                    <th>Items</th>
                    <th>Time</th>
                    <th>Status</th>
                    <th>Action</th>
                </tr>
            </thead>
            <tbody>
                <tr>
                    <td>05</td>
                    <td>Sliced Beef x1<br>Chicken x2</td>
                    <td>1:00 PM</td>
                    <td><span class="badge badge-done">Done</span></td>
                    <td><button style="padding:2px 6px;" onclick="goToPage(10)">View</button></td>
                </tr>
                <tr>
                    <td>12</td>
                    <td>Fishball x5<br>Crabsticks x2</td>
                    <td>1:03 PM</td>
                    <td><span class="badge badge-progress">In prog...</span></td>
                    <td><button style="padding:2px 6px;" onclick="goToPage(10)">View</button></td>
                </tr>
                <tr>
                    <td>08</td>
                    <td>Squid x1<br>Prawns x1</td>
                    <td>1:06 PM</td>
                    <td><span class="badge badge-pending">Not sta...</span></td>
                    <td><button style="padding:2px 6px;" onclick="goToPage(10)">View</button></td>
                </tr>
            </tbody>
        </table>
    </div>

    <!-- PAGE 10: Kitchen / Update Order Status -->
    <div id="page10" class="page">
        <div style="display: flex; align-items: center; gap: 10px; margin-bottom: 20px;">
            <i class="fa-solid fa-chevron-left" onclick="goToPage(9)"></i>
            <h2 class="header-title">Update Order Status</h2>
        </div>

        <div style="background: #f9f9f9; padding: 15px; border-radius: 8px; border: 1px solid #ccc; margin-bottom: 25px;">
            <h3 style="margin-bottom: 10px;">Table No 5</h3>
            <p style="color: #444; line-height: 1.5;">
                Sliced Beef x1<br>
                Chicken x2
            </p>
        </div>

        <label style="font-weight: bold; display: block; margin-bottom: 8px;">Status:</label>
        <select class="form-input" style="font-weight: bold; height: 45px;">
            <option value="Done">Done</option>
            <option value="In Progress">In Progress</option>
            <option value="Not Started">Not Started</option>
        </select>

        <button class="btn-primary" style="margin-top: 15px;" onclick="alert('Status pesanan telah dikemas kini!'); goToPage(9);">Update Status</button>
    </div>

</div>

<script>
    // Navigation function to switch between pages
    function goToPage(pageNumber) {
        // Hide all pages
        const pages = document.querySelectorAll('.page');
        pages.forEach(page => page.classList.remove('active'));

        // Show target page
        const targetPage = document.getElementById('page' + pageNumber);
        if (targetPage) {
            targetPage.classList.add('active');
        }
    }

    function confirmTable() {
        const table = document.getElementById('selectMeja').value;
        if (!table) {
            alert('Sila pilih nombor meja terlebih dahulu!');
            return;
        }
        goToPage(4);
    }

    function addToCart() {
        alert('Item telah ditambah ke dalam troli!');
        goToPage(7);
    }
</script>

</body>
</html>