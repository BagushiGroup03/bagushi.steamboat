<!DOCTYPE html>
<html lang="en">
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
            position: relative;
        }

        .cart-badge {
            position: absolute;
            top: -8px;
            right: -10px;
            background: #d9534f;
            color: white;
            border-radius: 50%;
            padding: 2px 6px;
            font-size: 0.7rem;
            font-weight: bold;
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

        /* Password Wrapper for Hide/Show */
        .password-container {
            position: relative;
            width: 100%;
            margin-bottom: 15px;
        }

        .password-container input {
            width: 100%;
            padding: 12px;
            padding-right: 40px;
            border: 1px solid #ccc;
            border-radius: 8px;
            box-sizing: border-box;
            margin-bottom: 0;
        }

        .toggle-password {
            position: absolute;
            right: 12px;
            top: 50%;
            transform: translateY(-50%);
            cursor: pointer;
            color: #777;
        }

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
            display: flex;
            flex-direction: column;
            justify-content: space-between;
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

        .btn-add-quick {
            background: #222;
            color: white;
            border: none;
            padding: 5px 10px;
            border-radius: 5px;
            font-size: 0.8rem;
            margin-top: 8px;
            cursor: pointer;
        }

        /* Cart Page 7 Styles */
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
        <img src="bagushi.jpg.png" class="img-header" alt="Bagushi Steamboat & Grill Logo">
        <h1 class="title-large">BAGUSHI STEAMBOAT & GRILL CHANGLUN</h1>
        <p class="subtitle">Digital Ordering System & Fast Service</p>
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
        <p class="subtitle">Customer Sign In</p>
        
        <input type="text" id="loginEmail" class="form-input" placeholder="Name / Email" required>
        
        <div class="password-container">
            <input type="password" id="loginPassword" placeholder="Password" required>
            <i class="fa-solid fa-eye toggle-password" id="togglePassword" onclick="togglePasswordVisibility()"></i>
        </div>
        
        <button class="btn-primary" style="margin-top: 10px;" onclick="handleSignIn()">Sign In</button>
        <div style="text-align: center; margin-top: 15px;">
            <small onclick="goToPage(9)" style="cursor: pointer; text-decoration: underline; color: #666;">(Staff/Kitchen Access - Page 9)</small>
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
        <img src="bagushi.jpg.png" class="img-header" alt="Bagushi Steamboat & Grill">
        <h2 class="title-large">SELECT TABLE</h2>
        <p class="subtitle">Please confirm your table number to view the menu.</p>
        
        <select id="selectMeja" class="form-input" style="font-weight: bold;">
            <option value="">-- Select Table Number --</option>
            <option value="Table 01">Table 01</option>
            <option value="Table 02">Table 02</option>
            <option value="Table 05">Table 05</option>
            <option value="Table 08">Table 08</option>
            <option value="Table 12">Table 12</option>
        </select>
        
        <button class="btn-primary" onclick="confirmTable()">View Menu</button>
    </div>

    <!-- PAGE 4: Main Categories / Recommendations & Search Menu -->
    <div id="page4" class="page">
        <div class="top-bar">
            <span style="font-size:0.8rem; color:#666;">Menu Search</span>
            <i class="fa-solid fa-cart-shopping" onclick="goToPage(7)" style="font-size:1.3rem;">
                <span class="cart-badge total-cart-count">0</span>
            </i>
        </div>
        <input type="text" id="searchMenuInput" class="form-input" placeholder="🔍 Search menu (e.g., Beef, Chicken...)" oninput="filterMenu(this.value)">
        
        <div id="searchResults" style="display: none; margin-bottom: 15px;">
            <p style="font-weight: bold; margin-bottom: 8px; font-size: 0.9rem; color:#d9534f;">Search Results:</p>
            <div id="searchResultList" style="display: flex; flex-direction: column; gap: 8px;"></div>
            <hr style="margin: 15px 0; border: 0; border-top: 1px solid #eee;">
        </div>

        <div id="defaultCategories">
            <p style="font-weight: bold; margin-bottom: 10px;">Suggestions / Categories</p>
            <div class="category-card" onclick="goToPage(5)">
                <span>Best Sellers</span>
                <i class="fa-solid fa-chevron-right"></i>
            </div>
            <div class="category-card" onclick="goToPage(5)">
                <span>Steamboat & Grill Sets</span>
                <i class="fa-solid fa-chevron-right"></i>
            </div>
            <div class="category-card" onclick="goToPage(5)">
                <span>Meat & Seafood</span>
                <i class="fa-solid fa-chevron-right"></i>
            </div>
            <div class="category-card" onclick="goToPage(5)">
                <span>Drinks & Desserts</span>
                <i class="fa-solid fa-chevron-right"></i>
            </div>
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
                <i class="fa-solid fa-bag-shopping" onclick="goToPage(7)">
                    <span class="cart-badge total-cart-count">0</span>
                </i>
            </div>
        </div>

        <div class="grid-2x2" id="foodGridContainer"></div>

        <div style="text-align: center; margin-top: 10px;">
            <small style="color:#777;">Showing all items</small><br><br>
            <button class="btn-primary" onclick="goToPage(7)">Go to Cart (<span class="total-cart-count">0</span>)</button>
        </div>
    </div>

    <!-- PAGE 6: Product Detail & Special Request -->
    <div id="page6" class="page">
        <div class="top-bar">
            <i class="fa-solid fa-chevron-left" onclick="goToPage(5)"></i>
            <div>
                <i class="fa-solid fa-magnifying-glass"></i> &nbsp;
                <i class="fa-regular fa-user"></i> &nbsp;
                <i class="fa-solid fa-bag-shopping" onclick="goToPage(7)">
                    <span class="cart-badge total-cart-count">0</span>
                </i>
            </div>
        </div>

        <h2 id="detailName" style="margin-bottom: 10px;">Sliced Beef Premium</h2>
        <div style="position: relative;">
            <img id="detailImg" src="https://via.placeholder.com/350x200?text=Sliced+Beef+Premium" class="img-header" style="height: 200px;">
            <i class="fa-regular fa-heart heart-icon" style="font-size: 1.3rem;"></i>
        </div>

        <p id="detailPrice" style="font-weight: bold; font-size: 1.1rem; margin-bottom: 5px;">Price: RM 12.00</p>

        <label style="font-weight: bold; display: block; margin-top: 15px; margin-bottom: 5px;">Special Request:</label>
        <input type="text" id="specialRequest" class="form-input" placeholder="E.g., Less spicy / Extra soup">

        <button class="btn-primary" onclick="addCurrentDetailToCart()">Add to Cart</button>

        <hr style="margin: 20px 0; border: 0; border-top: 1px solid #eee;">
        <p style="font-weight: bold;">Customer Reviews</p>
        <div style="display: flex; gap: 10px; align-items: center; margin-top: 10px;">
            <img src="https://via.placeholder.com/50" style="border-radius: 5px;">
            <div>
                <small style="font-weight: bold;">Bagushi Popular Menu</small><br>
                <small>⭐⭐⭐⭐⭐ (5/5)</small>
            </div>
        </div>
    </div>

    <!-- PAGE 7: My Cart & Checkout -->
    <div id="page7" class="page">
        <div style="display: flex; align-items: center; gap: 10px; margin-bottom: 20px;">
            <i class="fa-solid fa-chevron-left" onclick="goToPage(5)"></i>
            <h2>My cart</h2>
        </div>

        <div id="cartList" style="flex: 1; overflow-y: auto;"></div>

        <div style="margin-top: auto; padding-top: 15px; border-top: 1px solid #eee;">
            <div style="display: flex; justify-content: space-between; font-weight: bold; font-size: 1.1rem; margin-bottom: 15px;">
                <span>Total</span>
                <span>RM <span id="cartTotalPrice">0.00</span></span>
            </div>
            <button class="btn-primary" onclick="checkout()">Checkout</button>
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
            <p style="font-size: 0.85rem; color: #666; margin-bottom: 15px;">Your order is being processed by the Bagushi kitchen.</p>
            <button class="btn-primary" onclick="goToPage(9)">Go to Staff Dashboard (Page 9)</button>
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

        <button class="btn-primary" style="margin-top: 15px;" onclick="alert('Order status updated successfully!'); goToPage(9);">Update Status</button>
    </div>

</div>

<script>
    const menuItems = [
        { name: 'Sliced Beef', price: 12.00, img: 'https://via.placeholder.com/150?text=Sliced+Beef' },
        { name: 'Chicken Slice', price: 10.00, img: 'https://via.placeholder.com/150?text=Marinated+Chicken' },
        { name: 'Fishball Combo', price: 8.00, img: 'https://via.placeholder.com/150?text=Fishball+Combo' },
        { name: 'Fresh Prawns', price: 15.00, img: 'https://via.placeholder.com/150?text=Prawns+Fresh' }
    ];

    let cart = [];
    let currentDetailItem = null;

    window.onload = function() {
        renderFoodGrid();
    };

    function renderFoodGrid() {
        const gridContainer = document.getElementById('foodGridContainer');
        gridContainer.innerHTML = '';
        menuItems.forEach(item => {
            gridContainer.innerHTML += `
                <div class="product-card">
                    <i class="fa-regular fa-heart heart-icon"></i>
                    <img src="${item.img}" alt="${item.name}" onclick="openProductDetail('${item.name}', ${item.price}, '${item.img}')">
                    <p style="font-weight: bold; margin-top: 5px;">${item.name}</p>
                    <small>RM ${item.price.toFixed(2)}</small>
                    <button class="btn-add-quick" onclick="addToCart('${item.name}', ${item.price}, '${item.img}')">+ Add</button>
                </div>
            `;
        });
    }

    function togglePasswordVisibility() {
        const passwordInput = document.getElementById('loginPassword');
        const toggleIcon = document.getElementById('togglePassword');
        
        if (passwordInput.type === 'password') {
            passwordInput.type = 'text';
            toggleIcon.classList.remove('fa-eye');
            toggleIcon.classList.add('fa-eye-slash');
        } else {
            passwordInput.type = 'password';
            toggleIcon.classList.remove('fa-eye-slash');
            toggleIcon.classList.add('fa-eye');
        }
    }

    function handleSignIn() {
        const emailInput = document.getElementById('loginEmail').value.trim();
        const passwordInput = document.getElementById('loginPassword').value.trim();

        if (emailInput === '' || passwordInput === '') {
            alert('Please fill in both Name/Email and Password before signing in!');
            return;
        }

        goToPage(3);
    }

    function goToPage(pageNumber) {
        const pages = document.querySelectorAll('.page');
        pages.forEach(page => page.classList.remove('active'));

        const targetPage = document.getElementById('page' + pageNumber);
        if (targetPage) {
            targetPage.classList.add('active');
        }

        if (pageNumber === 7) {
            renderCart();
        }
    }

    function confirmTable() {
        const table = document.getElementById('selectMeja').value;
        if (!table) {
            alert('Please select a table number first!');
            return;
        }
        goToPage(4);
    }

    function filterMenu(query) {
        const searchResultsBox = document.getElementById('searchResults');
        const searchResultList = document.getElementById('searchResultList');
        const defaultCategories = document.getElementById('defaultCategories');
        
        searchResultList.innerHTML = '';
        const keyword = query.toLowerCase().trim();

        if (keyword === '') {
            searchResultsBox.style.display = 'none';
            defaultCategories.style.display = 'block';
            return;
        }

        const filtered = menuItems.filter(item => item.name.toLowerCase().includes(keyword));

        searchResultsBox.style.display = 'block';
        defaultCategories.style.display = 'none';

        if (filtered.length === 0) {
            searchResultList.innerHTML = '<small style="color:#999;">No matching menu items found.</small>';
            return;
        }

        filtered.forEach(item => {
            searchResultList.innerHTML += `
                <div class="category-card" onclick="openProductDetail('${item.name}', ${item.price}, '${item.img}')" style="padding: 10px 15px; margin-bottom: 8px;">
                    <div style="display: flex; align-items: center; gap: 10px;">
                        <img src="${item.img}" style="width: 40px; height: 40px; border-radius: 6px; object-fit: cover;">
                        <div>
                            <span style="font-size: 0.9rem; font-weight: bold;">${item.name}</span><br>
                            <small style="color: #666;">RM ${item.price.toFixed(2)}</small>
                        </div>
                    </div>
                    <i class="fa-solid fa-chevron-right" style="font-size: 0.8rem;"></i>
                </div>
            `;
        });
    }

    function addToCart(name, price, img) {
        const existingItem = cart.find(item => item.name === name);
        if (existingItem) {
            existingItem.qty += 1;
        } else {
            cart.push({ name: name, price: price, img: img, qty: 1 });
        }
        updateCartBadge();
        alert(`${name} has been added to cart!`);
    }

    function openProductDetail(name, price, img) {
        currentDetailItem = { name: name, price: price, img: img };
        document.getElementById('detailName').innerText = name;
        document.getElementById('detailPrice').innerText = 'Price: RM ' + price.toFixed(2);
        document.getElementById('detailImg').src = img;
        document.getElementById('specialRequest').value = '';
        goToPage(6);
    }

    function addCurrentDetailToCart() {
        if (currentDetailItem) {
            addToCart(currentDetailItem.name, currentDetailItem.price, currentDetailItem.img);
            goToPage(7);
        }
    }

    function updateCartBadge() {
        const totalItems = cart.reduce((sum, item) => sum + item.qty, 0);
        document.querySelectorAll('.total-cart-count').forEach(el => {
            el.innerText = totalItems;
        });
    }

    function renderCart() {
        const cartList = document.getElementById('cartList');
        cartList.innerHTML = '';

        if (cart.length === 0) {
            cartList.innerHTML = '<p style="text-align:center; color:#999; margin-top:50px;">Your cart is currently empty.</p>';
            document.getElementById('cartTotalPrice').innerText = '0.00';
            return;
        }

        let total = 0;

        cart.forEach((item, index) => {
            const itemTotal = item.price * item.qty;
            total += itemTotal;

            const itemHTML = `
                <div class="cart-item">
                    <img src="${item.img}" alt="${item.name}">
                    <div style="flex:1;">
                        <p style="font-weight: bold; font-size: 0.9rem;">${item.name}</p>
                        <small style="color:#666;">RM ${item.price.toFixed(2)}</small>
                    </div>
                    <div class="qty-controls">
                        <button class="qty-btn" onclick="changeQty(${index}, -1)">-</button>
                        <span>${item.qty}</span>
                        <button class="qty-btn" onclick="changeQty(${index}, 1)">+</button>
                    </div>
                    <i class="fa-regular fa-trash-can" style="color: #999; cursor: pointer;" onclick="removeItem(${index})"></i>
                </div>
            `;
            cartList.innerHTML += itemHTML;
        });

        document.getElementById('cartTotalPrice').innerText = total.toFixed(2);
        updateCartBadge();
    }

    function changeQty(index, change) {
        cart[index].qty += change;
        if (cart[index].qty <= 0) {
            cart.splice(index, 1);
        }
        renderCart();
    }

    function removeItem(index) {
        cart.splice(index, 1);
        renderCart();
    }

    function checkout() {
        if (cart.length === 0) {
            alert('Your cart is empty! Please add some items first.');
            return;
        }
        goToPage(8);
    }
</script>

</body>
</html>