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
            color: #222;
        }

        /* Mobile App Frame Container */
        .app-screen {
            width: 100%;
            max-width: 414px;
            height: 736px;
            background-color: #f2f2f2;
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
            background: #f2f2f2;
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
            padding-bottom: 10px;
            margin-bottom: 15px;
        }

        .top-bar i {
            font-size: 1.2rem;
            cursor: pointer;
            color: #333;
        }

        .cart-badge {
            position: absolute;
            top: -8px;
            right: -10px;
            background: #222;
            color: white;
            border-radius: 50%;
            padding: 2px 6px;
            font-size: 0.7rem;
            font-weight: bold;
        }

        /* Common Design Elements */
        .img-header {
            width: 100%;
            height: 180px;
            object-fit: cover;
            border-radius: 12px;
            margin-bottom: 15px;
            background-color: #e2e2e2;
            display: flex;
            align-items: center;
            justify-content: center;
            color: #666;
            font-size: 3rem;
            border: 1.5px dashed #ccc;
        }

        .btn-primary {
            background-color: #444;
            color: white;
            border: none;
            padding: 14px;
            border-radius: 25px;
            font-weight: bold;
            width: 100%;
            cursor: pointer;
            text-align: center;
            margin-top: auto;
            font-size: 1rem;
            transition: 0.2s;
        }

        .btn-primary:hover {
            background-color: #222;
        }

        .form-input {
            width: 100%;
            padding: 12px;
            margin-bottom: 15px;
            border: 1.5px solid #222;
            border-radius: 12px;
            box-sizing: border-box;
            background: #fff;
            font-weight: bold;
            font-size: 1rem;
        }

        /* Menu List Styles */
        .menu-item-row {
            display: flex;
            justify-content: space-between;
            align-items: center;
            padding: 10px 0;
            border-bottom: 1px solid #ddd;
            background: #fff;
            padding: 10px;
            border-radius: 10px;
            margin-bottom: 8px;
        }

        .btn-add-menu {
            background: #222;
            color: white;
            border: none;
            padding: 6px 14px;
            border-radius: 6px;
            font-size: 0.8rem;
            cursor: pointer;
        }

        /* Cart Page Styles based on Design */
        .cart-card-container {
            background: #fff;
            border-radius: 15px;
            padding: 15px;
            display: flex;
            align-items: center;
            gap: 15px;
            margin-bottom: 20px;
            box-shadow: 0 2px 5px rgba(0,0,0,0.05);
        }

        .cart-item-box {
            background: #fff;
            border-radius: 12px;
            padding: 12px;
            display: flex;
            align-items: center;
            gap: 12px;
            margin-bottom: 12px;
            box-shadow: 0 1px 3px rgba(0,0,0,0.05);
        }

        .cart-item-box img {
            width: 60px;
            height: 60px;
            border-radius: 8px;
            object-fit: cover;
            background: #e2e2e2;
        }

        .qty-box {
            display: flex;
            align-items: center;
            border: 1.5px solid #ccc;
            border-radius: 6px;
            padding: 2px 8px;
            background: #f9f9f9;
            width: fit-content;
        }

        .qty-btn {
            background: none;
            border: none;
            font-size: 1rem;
            cursor: pointer;
            padding: 0 6px;
            font-weight: bold;
        }

        /* Order Status Page Styles based on Design */
        .success-card {
            background: #fff;
            border-radius: 15px;
            padding: 20px;
            text-align: center;
            box-shadow: 0 2px 8px rgba(0,0,0,0.05);
            margin-bottom: 30px;
        }

        .success-icon {
            width: 60px;
            height: 60px;
            background: #e8e8e8;
            border-radius: 50%;
            display: flex;
            align-items: center;
            justify-content: center;
            margin: 0 auto 15px auto;
            font-size: 1.5rem;
            color: #000;
        }

        .status-timeline {
            display: flex;
            flex-direction: column;
            gap: 25px;
            padding-left: 20px;
            position: relative;
        }

        .status-node {
            display: flex;
            align-items: center;
            gap: 20px;
            font-weight: bold;
            font-size: 1.1rem;
        }

        .status-circle {
            width: 32px;
            height: 32px;
            border-radius: 50%;
            background: #fff;
            border: 2px solid #222;
            display: flex;
            align-items: center;
            justify-content: center;
        }

        .status-circle.active {
            background: #000;
            color: #fff;
        }
    </style>
</head>
<body>

<div class="app-screen">

    <!-- PAGE 1: Welcome Screen (Based on Design 1)[cite: 6] -->
    <div id="page1" class="page active">
        <div class="top-bar">
            <i class="fa-solid fa-bars"></i>
            <div>
                <i class="fa-regular fa-bell"></i> &nbsp;
                <i class="fa-solid fa-share-nodes"></i> &nbsp;
                <i class="fa-solid fa-magnifying-glass"></i>
            </div>
        </div>
        
        <!-- Image placeholder atau gambar kedai -->
        <div class="img-header">
            <img src="bagushi.jpg.png" style="width:100%; height:100%; object-fit:cover; border-radius:12px;" onerror="this.style.display='none'">
            <i class="fa-regular fa-image" style="position: absolute;"></i>
        </div>

        <h1 class="title-large" style="font-size: 1.6rem; line-height: 1.2; margin-bottom: 10px;">BAGUSHI STEAMBOAT & GRILL CHANGLUN</h1>
        <p style="text-align: center; font-size: 1.8rem; font-weight: bold; margin-bottom: 30px;">Welcome!</p>
        
        <button class="btn-primary" onclick="goToPage(2)">Start Ordering</button>
    </div>

    <!-- PAGE 2: Sign In Form -->
    <div id="page2" class="page">
        <div class="top-bar">
            <i class="fa-solid fa-chevron-left" onclick="goToPage(1)"></i>
            <span class="header-title">Sign In</span>
            <i></i>
        </div>
        <h1 class="title-large" style="font-size: 1.3rem; margin-bottom: 20px;">Customer Sign In</h1>
        
        <input type="text" id="loginEmail" class="form-input" placeholder="Name / Email" required>
        
        <div class="password-container" style="position:relative; width:100%;">
            <input type="password" id="loginPassword" class="form-input" placeholder="Password" required style="padding-right: 40px; margin-bottom: 0;">
            <i class="fa-solid fa-eye toggle-password" id="togglePassword" onclick="togglePasswordVisibility()" style="position:absolute; right:15px; top:40%; transform:translateY(-50%); cursor:pointer; color:#777;"></i>
        </div>
        
        <button class="btn-primary" style="margin-top: 25px;" onclick="handleSignIn()">Continue</button>
        <div style="text-align: center; margin-top: 15px;">
            <small onclick="goToPage(9)" style="cursor: pointer; text-decoration: underline; color: #666;">(Staff / Kitchen Dashboard - Page 9)</small>
        </div>
    </div>

    <!-- PAGE 3: Confirm Table Number (Based on Design 2)[cite: 7] -->
    <div id="page3" class="page">
        <div class="top-bar">
            <i class="fa-solid fa-bars"></i>
            <div>
                <i class="fa-regular fa-bell"></i> &nbsp;
                <i class="fa-solid fa-share-nodes"></i> &nbsp;
                <i class="fa-solid fa-magnifying-glass"></i>
            </div>
        </div>
        
        <div class="img-header">
            <img src="bagushi.jpg.png" style="width:100%; height:100%; object-fit:cover; border-radius:12px;" onerror="this.style.display='none'">
            <i class="fa-regular fa-image" style="position: absolute;"></i>
        </div>

        <h2 class="title-large" style="margin-bottom: 5px;">Confirm Your Table</h2>
        <p class="subtitle" style="font-size: 0.85rem; margin-bottom: 20px;">Your table number has been detected from the QR code</p>
        
        <div style="background: #fff; border: 1.5px solid #222; border-radius: 15px; padding: 15px; text-align: center; margin-bottom: 15px;">
            <label style="font-size: 0.9rem; font-weight: bold; display: block; margin-bottom: 8px;">Table Number</label>
            <select id="selectMeja" class="form-input" style="text-align: center; margin-bottom: 0;">
                <option value="Table 05">05</option>
                <option value="Table 01">01</option>
                <option value="Table 02">02</option>
                <option value="Table 08">08</option>
                <option value="Table 12">12</option>
            </select>
        </div>
        
        <p style="text-align: center; font-size: 0.75rem; color: #666; margin-bottom: 20px;">Tap the arrow if the detected table number is incorrect</p>

        <button class="btn-primary" onclick="confirmTable()">Confirm</button>
    </div>

    <!-- PAGE 4: Menu Categories Selection -->
    <div id="page4" class="page">
        <div class="top-bar">
            <span style="font-size:0.8rem; color:#666;">Menu Categories</span>
            <i class="fa-solid fa-cart-shopping" onclick="goToPage(7)" style="font-size:1.3rem; position:relative;">
                <span class="cart-badge total-cart-count">0</span>
            </i>
        </div>
        <input type="text" id="searchMenuInput" class="form-input" placeholder="🔍 Search all 54 items..." oninput="filterMenu(this.value)">
        
        <div id="searchResults" style="display: none; margin-bottom: 15px;">
            <p style="font-weight: bold; margin-bottom: 8px; font-size: 0.9rem; color:#d9534f;">Search Results:</p>
            <div id="searchResultList" style="display: flex; flex-direction: column; gap: 8px;"></div>
            <hr style="margin: 15px 0; border: 0; border-top: 1px solid #ccc;">
        </div>

        <div id="defaultCategories" style="flex: 1; overflow-y: auto; padding-bottom: 10px;">
            <p style="font-weight: bold; margin-bottom: 8px;">Select Category:</p>
            <div style="display: grid; grid-template-columns: 1fr 1fr; gap: 10px;">
                <div class="form-input" style="text-align:center; cursor:pointer; margin-bottom:0; padding:15px;" onclick="filterByCategory('Sup / Dapur')">Sup / Dapur</div>
                <div class="form-input" style="text-align:center; cursor:pointer; margin-bottom:0; padding:15px;" onclick="filterByCategory('Sos Pencicah')">Sos Pencicah</div>
                <div class="form-input" style="text-align:center; cursor:pointer; margin-bottom:0; padding:15px;" onclick="filterByCategory('Daging')">Daging</div>
                <div class="form-input" style="text-align:center; cursor:pointer; margin-bottom:0; padding:15px;" onclick="filterByCategory('Ayam')">Ayam</div>
                <div class="form-input" style="text-align:center; cursor:pointer; margin-bottom:0; padding:15px;" onclick="filterByCategory('Seafood')">Seafood</div>
                <div class="form-input" style="text-align:center; cursor:pointer; margin-bottom:0; padding:15px;" onclick="filterByCategory('Bebola & Steamboat')">Bebola & Steamboat</div>
                <div class="form-input" style="text-align:center; cursor:pointer; margin-bottom:0; padding:15px;" onclick="filterByCategory('Mee')">Mee</div>
                <div class="form-input" style="text-align:center; cursor:pointer; margin-bottom:0; padding:15px;" onclick="filterByCategory('Sayur')">Sayur</div>
                <div class="form-input" style="text-align:center; cursor:pointer; margin-bottom:0; padding:15px;" onclick="filterByCategory('Side Dish')">Side Dish</div>
                <div class="form-input" style="text-align:center; cursor:pointer; margin-bottom:0; padding:15px;" onclick="filterByCategory('Minuman')">Minuman</div>
                <div class="form-input" style="text-align:center; cursor:pointer; margin-bottom:0; padding:15px;" onclick="filterByCategory('Alacarte Add On')">Alacarte Add On</div>
                <div class="form-input" style="text-align:center; cursor:pointer; margin-bottom:0; padding:15px;" onclick="filterByCategory('Set Menu')">Set Menu</div>
            </div>
        </div>
        <button class="btn-primary" style="margin-top: 10px;" onclick="filterByCategory('All')">View All Menu Items</button>
    </div>

    <!-- PAGE 5: Filtered Menu List -->
    <div id="page5" class="page">
        <div class="top-bar">
            <div style="display:flex; align-items:center; gap:8px;">
                <i class="fa-solid fa-chevron-left" onclick="goToPage(4)"></i>
                <span id="page5Title" class="header-title">Menu List</span>
            </div>
            <div>
                <i class="fa-solid fa-bag-shopping" onclick="goToPage(7)" style="font-size: 1.2rem; cursor: pointer; position:relative;">
                    <span class="cart-badge total-cart-count">0</span>
                </i>
            </div>
        </div>

        <div id="fullMenuListContainer" style="flex:1; overflow-y:auto; padding-bottom: 20px;"></div>

        <button class="btn-primary" onclick="goToPage(7)">Go to Cart (<span class="total-cart-count">0</span>)</button>
    </div>

    <!-- PAGE 6: Product Detail & Special Request -->
    <div id="page6" class="page">
        <div class="top-bar">
            <i class="fa-solid fa-chevron-left" onclick="goToPage(5)"></i>
            <div>
                <i class="fa-solid fa-bag-shopping" onclick="goToPage(7)" style="font-size: 1.2rem; cursor: pointer; position:relative;">
                    <span class="cart-badge total-cart-count">0</span>
                </i>
            </div>
        </div>

        <h2 id="detailName" style="margin-bottom: 10px;">Item Name</h2>
        <div style="position: relative; margin-bottom: 15px;">
            <img id="detailImg" src="https://via.placeholder.com/350x200?text=Bagushi+Menu" class="img-header" style="height: 180px;">
        </div>

        <p id="detailPrice" style="font-weight: bold; font-size: 1.1rem; margin-bottom: 5px;">Price: RM 0.00</p>
        <p id="detailCategory" style="color: #666; font-size: 0.9rem; margin-bottom: 15px;"></p>

        <label style="font-weight: bold; display: block; margin-top: 10px; margin-bottom: 5px;">Special Request:</label>
        <input type="text" id="specialRequest" class="form-input" placeholder="E.g., Less spicy / Extra soup">

        <button class="btn-primary" onclick="addCurrentDetailToCart()">Add to Cart</button>
    </div>

    <!-- PAGE 7: My Cart & Checkout (Based on Design 3)[cite: 8] -->
    <div id="page7" class="page">
        <div style="display: flex; align-items: center; gap: 10px; margin-bottom: 15px;">
            <i class="fa-solid fa-chevron-left" onclick="goToPage(5)"></i>
            <h2 style="font-size: 1.3rem;">My cart</h2>
        </div>

        <!-- Table Number Card -->
        <div class="cart-card-container">
            <div style="font-size: 2rem;"><i class="fa-solid fa-chair"></i></div>
            <div>
                <small style="color: #666; font-size: 0.8rem;">Table Number</small>
                <h3 id="cartTableDisplay" style="font-size: 1.1rem;">Table 5</h3>
            </div>
        </div>

        <p style="font-weight: bold; margin-bottom: 10px;">Your Order</p>

        <!-- Dynamic Cart Items Container -->
        <div id="cartList" style="flex: 1; overflow-y: auto; margin-bottom: 15px;"></div>

        <div style="background: #fff; padding: 15px; border-radius: 12px; margin-top: auto;">
            <div style="display: flex; justify-content: space-between; font-weight: bold; font-size: 1.1rem; margin-bottom: 15px;">
                <span>Total</span>
                <span>RM <span id="cartTotalPrice">0.00</span></span>
            </div>
            <button class="btn-primary" style="border-radius: 12px;" onclick="placeOrder()">Place Order</button>
        </div>
    </div>

    <!-- PAGE 8: Customer Order Status (Based on Design 4)[cite: 9] -->
    <div id="page8" class="page">
        <div class="top-bar" style="margin-bottom: 15px;">
            <i class="fa-solid fa-chevron-left" onclick="goToPage(7)"></i>
            <h2 class="header-title" style="font-size: 1.1rem;">Order Status</h2>
            <i></i>
        </div>

        <!-- Success Notification Card -->
        <div class="success-card">
            <div class="success-icon">
                <i class="fa-solid fa-check"></i>
            </div>
            <h3 style="font-size: 1.1rem; margin-bottom: 5px;">Order Successfully Placed!</h3>
            <p style="font-size: 0.85rem; color: #666;">Your order has been sent to the staff.</p>
        </div>

        <p style="font-weight: bold; margin-bottom: 20px; font-size: 1.1rem;">Order Progress</p>

        <div class="status-timeline">
            <div class="status-node">
                <div class="status-circle active"><i class="fa-solid fa-check" style="font-size: 0.9rem;"></i></div>
                <span>Order Receive</span>
            </div>
            <div class="status-node">
                <div class="status-circle"></div>
                <span style="color: #888;">Preparing</span>
            </div>
            <div class="status-node">
                <div class="status-circle"></div>
                <span style="color: #888;">Ready to Serve</span>
            </div>
        </div>

        <button class="btn-primary" style="margin-top: auto; border-radius: 12px;" onclick="goToPage(9)">Go to Staff Dashboard (Page 9)</button>
    </div>

    <!-- PAGE 9: Kitchen / Incoming Orders Dashboard -->
    <div id="page9" class="page">
        <div class="top-bar">
            <i class="fa-solid fa-chevron-left" onclick="goToPage(1)"></i>
            <h2 class="header-title">Incoming Orders</h2>
        </div>

        <div style="display: flex; gap: 5px; margin-bottom: 15px;">
            <button class="btn-primary" style="padding: 6px; font-size:0.75rem; border-radius:8px; margin-top:0;">All (3)</button>
            <button class="btn-primary" style="padding: 6px; font-size:0.75rem; border-radius:8px; margin-top:0; background:#888;">Preparing (2)</button>
            <button class="btn-primary" style="padding: 6px; font-size:0.75rem; border-radius:8px; margin-top:0; background:#888;">Ready (1)</button>
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
        <div class="top-bar">
            <i class="fa-solid fa-chevron-left" onclick="goToPage(9)"></i>
            <h2 class="header-title">Update Order Status</h2>
        </div>

        <div style="background: #fff; padding: 15px; border-radius: 12px; border: 1px solid #ccc; margin-bottom: 25px;">
            <h3 style="margin-bottom: 10px;">Table No 5</h3>
            <p style="color: #444; line-height: 1.5;">
                Sliced Beef x1<br>
                Chicken x2
            </p>
        </div>

        <label style="font-weight: bold; display: block; margin-bottom: 8px;">Status:</label>
        <select class="form-input" style="height: 45px;">
            <option value="Done">Done</option>
            <option value="In Progress">In Progress</option>
            <option value="Not Started">Not Started</option>
        </select>

        <button class="btn-primary" style="margin-top: 15px; border-radius:12px;" onclick="alert('Order status updated successfully!'); goToPage(9);">Update Status</button>
    </div>

</div>

<script>
    const menuItems = [
        { id: 1, category: 'Sup / Dapur', name: 'Sup tomyam refill', price: 3.00, img: 'https://via.placeholder.com/150?text=Tomypam+Soup' },
        { id: 2, category: 'Sup / Dapur', name: 'Sup jepun (Shoyu) refill', price: 3.00, img: 'https://via.placeholder.com/150?text=Shoyu+Soup' },
        { id: 3, category: 'Sup / Dapur', name: 'Sup mala (pedas) refill', price: 3.00, img: 'https://via.placeholder.com/150?text=Mala+Soup' },
        { id: 4, category: 'Sup / Dapur', name: 'BBQ pan', price: 5.00, img: 'https://via.placeholder.com/150?text=BBQ+Pan' },
        { id: 5, category: 'Sup / Dapur', name: 'Steamboat pan', price: 5.00, img: 'https://via.placeholder.com/150?text=Steamboat+Pan' },
        { id: 6, category: 'Sup / Dapur', name: 'Shabu Shabu hot pot', price: 5.00, img: 'https://via.placeholder.com/150?text=Hot+Pot' },

        { id: 7, category: 'Sos Pencicah', name: 'Sos Bagushi original', price: 1.00, img: 'https://via.placeholder.com/150?text=Original+Sos' },
        { id: 8, category: 'Sos Pencicah', name: 'Sos Bagushi spicy', price: 1.00, img: 'https://via.placeholder.com/150?text=Spicy+Sos' },
        { id: 9, category: 'Sos Pencicah', name: 'Sos seafood', price: 1.00, img: 'https://via.placeholder.com/150?text=Seafood+Sos' },
        { id: 10, category: 'Sos Pencicah', name: 'Sos yong tau fu (Sukiyaki)', price: 1.00, img: 'https://via.placeholder.com/150?text=Sukiyaki+Sos' },

        { id: 11, category: 'Daging', name: 'Daging ribeye', price: 6.00, img: 'https://via.placeholder.com/150?text=Ribeye' },
        { id: 12, category: 'Daging', name: 'Daging brisket', price: 6.00, img: 'https://via.placeholder.com/150?text=Brisket' },
        { id: 13, category: 'Daging', name: 'Daging Korea', price: 6.00, img: 'https://via.placeholder.com/150?text=Korea+Beef' },
        { id: 14, category: 'Daging', name: 'Daging perap', price: 6.00, img: 'https://via.placeholder.com/150?text=Marinated+Beef' },
        { id: 15, category: 'Daging', name: 'Daging black pepper', price: 6.00, img: 'https://via.placeholder.com/150?text=Black+Pepper+Beef' },

        { id: 16, category: 'Ayam', name: 'Ayam fresh', price: 5.00, img: 'https://via.placeholder.com/150?text=Fresh+Chicken' },
        { id: 17, category: 'Ayam', name: 'Ayam korea', price: 5.00, img: 'https://via.placeholder.com/150?text=Korea+Chicken' },
        { id: 18, category: 'Ayam', name: 'Ayam perap', price: 5.00, img: 'https://via.placeholder.com/150?text=Marinated+Chicken' },
        { id: 19, category: 'Ayam', name: 'Ayam black pepper', price: 5.00, img: 'https://via.placeholder.com/150?text=Black+Pepper+Chicken' },

        { id: 20, category: 'Seafood', name: 'Lala', price: 4.00, img: 'https://via.placeholder.com/150?text=Lala' },
        { id: 21, category: 'Seafood', name: 'Udang', price: 6.00, img: 'https://via.placeholder.com/150?text=Prawns' },
        { id: 22, category: 'Seafood', name: 'Sotong', price: 6.00, img: 'https://via.placeholder.com/150?text=Sotong' },

        { id: 23, category: 'Bebola & Steamboat', name: 'Telur ayam', price: 1.50, img: 'https://via.placeholder.com/150?text=Egg' },
        { id: 24, category: 'Bebola & Steamboat', name: 'Tohu telur', price: 3.00, img: 'https://via.placeholder.com/150?text=Tofu' },
        { id: 25, category: 'Bebola & Steamboat', name: 'Bebola daging', price: 4.00, img: 'https://via.placeholder.com/150?text=Beef+Ball' },
        { id: 26, category: 'Bebola & Steamboat', name: 'Bebola ikan', price: 4.00, img: 'https://via.placeholder.com/150?text=Fish+Ball' },
        { id: 27, category: 'Bebola & Steamboat', name: 'Crab stick', price: 4.00, img: 'https://via.placeholder.com/150?text=Crab+Stick' },
        { id: 28, category: 'Bebola & Steamboat', name: 'Bebola sotong', price: 4.00, img: 'https://via.placeholder.com/150?text=Squid+Ball' },
        { id: 29, category: 'Bebola & Steamboat', name: 'Tohu ikan', price: 4.00, img: 'https://via.placeholder.com/150?text=Fish+Tofu' },

        { id: 30, category: 'Mee', name: 'Nasi putih', price: 1.50, img: 'https://via.placeholder.com/150?text=White+Rice' },
        { id: 31, category: 'Mee', name: 'Sohun', price: 2.00, img: 'https://via.placeholder.com/150?text=Sohun' },
        { id: 32, category: 'Mee', name: 'Mee kuning', price: 2.00, img: 'https://via.placeholder.com/150?text=Yellow+Mee' },
        { id: 33, category: 'Mee', name: 'Meggi', price: 2.00, img: 'https://via.placeholder.com/150?text=Meggi' },

        { id: 34, category: 'Sayur', name: 'Kubis', price: 2.00, img: 'https://via.placeholder.com/150?text=Cabbage' },
        { id: 35, category: 'Sayur', name: 'Sawi', price: 2.00, img: 'https://via.placeholder.com/150?text=Sawi' },
        { id: 36, category: 'Sayur', name: 'Karot', price: 2.00, img: 'https://via.placeholder.com/150?text=Carrot' },
        { id: 37, category: 'Sayur', name: 'Inoki', price: 3.00, img: 'https://via.placeholder.com/150?text=Enoki' },
        { id: 38, category: 'Sayur', name: 'Chimeji', price: 3.00, img: 'https://via.placeholder.com/150?text=Shimeji' },

        { id: 39, category: 'Side Dish', name: 'Tepung tin siam', price: 3.00, img: 'https://via.placeholder.com/150?text=Side+Dish' },
        { id: 40, category: 'Side Dish', name: 'French fries', price: 5.00, img: 'https://via.placeholder.com/150?text=French+Fries' },
        { id: 41, category: 'Side Dish', name: 'Tembikai', price: 5.00, img: 'https://via.placeholder.com/150?text=Watermelon' },
        { id: 42, category: 'Side Dish', name: 'Kek pisang', price: 5.00, img: 'https://via.placeholder.com/150?text=Banana+Cake' },
        { id: 43, category: 'Side Dish', name: 'Nugget', price: 5.00, img: 'https://via.placeholder.com/150?text=Nuggets' },

        { id: 44, category: 'Minuman', name: 'Oren', price: 3.00, img: 'https://via.placeholder.com/150?text=Orange+Drink' },
        { id: 45, category: 'Minuman', name: 'Teh O ice', price: 3.00, img: 'https://via.placeholder.com/150?text=Teh+O+Ice' },
        { id: 46, category: 'Minuman', name: 'Sirap', price: 3.00, img: 'https://via.placeholder.com/150?text=Sirap' },

        { id: 47, category: 'Alacarte Add On', name: 'Set sayur + chedawan', price: 6.00, img: 'https://via.placeholder.com/150?text=Veg+Mushroom+Set' },
        { id: 48, category: 'Alacarte Add On', name: 'Set mee + telur', price: 6.00, img: 'https://via.placeholder.com/150?text=Mee+Egg+Set' },
        { id: 49, category: 'Alacarte Add On', name: 'Set bebola', price: 10.00, img: 'https://via.placeholder.com/150?text=Meatball+Set' },
        { id: 50, category: 'Alacarte Add On', name: 'Set sayur + bb + mee + telur', price: 10.00, img: 'https://via.placeholder.com/150?text=Combo+Set' },
        { id: 51, category: 'Alacarte Add On', name: 'Set seafood + ayam', price: 12.00, img: 'https://via.placeholder.com/150?text=Seafood+Chicken+Set' },

        { id: 52, category: 'Set Menu', name: 'Set Solo (1 Orang)', price: 25.00, img: 'https://via.placeholder.com/150?text=Set+Solo' },
        { id: 53, category: 'Set Menu', name: 'Set Couple (2 Orang)', price: 45.00, img: 'https://via.placeholder.com/150?text=Set+Couple' },
        { id: 54, category: 'Set Menu', name: 'Set Family (3-4 Orang)', price: 75.00, img: 'https://via.placeholder.com/150?text=Set+Family' }
    ];

    let cart = [];
    let currentDetailItem = null;
    let selectedTable = 'Table 5';

    function filterByCategory(categoryName) {
        const container = document.getElementById('fullMenuListContainer');
        const page5Title = document.getElementById('page5Title');
        container.innerHTML = '';

        let filteredItems = [];
        if (categoryName === 'All') {
            filteredItems = menuItems;
            page5Title.innerText = 'All Menu Items';
        } else {
            filteredItems = menuItems.filter(item => item.category === categoryName);
            page5Title.innerText = categoryName;
        }

        filteredItems.forEach(item => {
            container.innerHTML += `
                <div class="menu-item-row">
                    <div class="menu-item-info" onclick="openProductDetail('${item.name}', ${item.price}, '${item.img}', '${item.category}')" style="cursor:pointer; flex:1;">
                        <h4 style="font-size:0.9rem;">${item.id}. ${item.name}</h4>
                        <small style="color:#666;">RM ${item.price.toFixed(2)}</small>
                    </div>
                    <button class="btn-add-menu" onclick="addToCart('${item.name}', ${item.price}, '${item.img}')">+ Add</button>
                </div>
            `;
        });

        goToPage(5);
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
        selectedTable = table;
        document.getElementById('cartTableDisplay').innerText = table;
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
                <div class="menu-item-row" style="background:#fff; padding:8px 12px; border-radius:8px;">
                    <div onclick="openProductDetail('${item.name}', ${item.price}, '${item.img}', '${item.category}')" style="cursor:pointer; flex:1;">
                        <span style="font-size: 0.9rem; font-weight: bold;">${item.id}. ${item.name}</span><br>
                        <small style="color: #666;">RM ${item.price.toFixed(2)} (${item.category})</small>
                    </div>
                    <button class="btn-add-menu" onclick="addToCart('${item.name}', ${item.price}, '${item.img}')">+ Add</button>
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

    function openProductDetail(name, price, img, category) {
        currentDetailItem = { name: name, price: price, img: img };
        document.getElementById('detailName').innerText = name;
        document.getElementById('detailPrice').innerText = 'Price: RM ' + price.toFixed(2);
        document.getElementById('detailCategory').innerText = 'Category: ' + category;
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
            cartList.innerHTML = '<p style="text-align:center; color:#999; margin-top:30px;">Your cart is currently empty.</p>';
            document.getElementById('cartTotalPrice').innerText = '0.00';
            return;
        }

        let total = 0;

        cart.forEach((item, index) => {
            const itemTotal = item.price * item.qty;
            total += itemTotal;

            const itemHTML = `
                <div class="cart-item-box">
                    <img src="${item.img}" alt="${item.name}">
                    <div style="flex:1;">
                        <p style="font-weight: bold; font-size: 0.95rem; margin-bottom: 2px;">${item.name}</p>
                        <small style="color:#666; display:block; margin-bottom:5px;">RM ${itemTotal.toFixed(2)}</small>
                        <div class="qty-box">
                            <button class="qty-btn" onclick="changeQty(${index}, -1)">-</button>
                            <span style="padding: 0 8px; font-weight: bold; font-size: 0.9rem;">${item.qty}</span>
                            <button class="qty-btn" onclick="changeQty(${index}, 1)">+</button>
                        </div>
                    </div>
                    <i class="fa-regular fa-trash-can" style="color: #666; cursor: pointer; font-size: 1.1rem; padding: 10px;" onclick="removeItem(${index})"></i>
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

    function placeOrder() {
        if (cart.length === 0) {
            alert('Your cart is empty! Please add some items first.');
            return;
        }
        goToPage(8);
    }
</script>

</body>
</html>