<!DOCTYPE html>
<html lang="vi">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Công ty TNHH VLXD SONG THỊNH - Hệ Thống Phân Phối Toàn Quốc</title>
    <!-- Google Fonts & FontAwesome -->
    <link href="https://fonts.googleapis.com/css2?family=Inter:wght@300;400;500;600;700&display=swap" rel="stylesheet">
    <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.4.0/css/all.min.css">
    
    <style>
        /* BẢNG MÀU UI/UX ĐẶC TRƯNG MONSUB (DARK THEME CHỦ ĐẠO - HỖ TRỢ LIGHT THEME) */
        :root {
            --bg-main: #0b0f19;
            --bg-card: #131a26;
            --border-color: #1e293b;
            --text-primary: #f1f5f9;
            --text-secondary: #94a3b8;
            --accent: #38bdf8; /* Xanh Neon MonSub */
            --accent-glow: rgba(56, 189, 248, 0.15);
            --price-color: #f43f5e;
        }

        [data-theme="light"] {
            --bg-main: #f8fafc;
            --bg-card: #ffffff;
            --border-color: #cbd5e1;
            --text-primary: #0f172a;
            --text-secondary: #64748b;
            --accent: #0284c7;
            --accent-glow: rgba(2, 132, 199, 0.1);
            --price-color: #e11d48;
        }

        * { margin: 0; padding: 0; box-sizing: border-box; font-family: 'Inter', sans-serif; scroll-behavior: smooth; }
        body { background-color: var(--bg-main); color: var(--text-primary); transition: background 0.2s, color 0.2s; padding-top: 70px; }
        a { color: inherit; text-decoration: none; }
        .container { max-width: 1200px; margin: 0 auto; padding: 0 20px; }

        /* 1. THANH ĐIỀU HƯỚNG (NAVBAR) THÔNG MINH */
        header { position: fixed; top: 0; left: 0; width: 100%; background: rgba(11, 15, 25, 0.85); backdrop-filter: blur(12px); border-bottom: 1px solid var(--border-color); z-index: 1000; }
        [data-theme="light"] header { background: rgba(248, 250, 252, 0.85); }
        .nav-container { display: flex; justify-content: space-between; align-items: center; height: 70px; gap: 20px; }
        .logo { font-weight: 700; font-size: 20px; letter-spacing: -0.5px; text-transform: uppercase; }
        .logo span { color: var(--accent); }
        
        /* Thanh Tìm Kiếm Đầy Đủ Chức Năng (Autocomplete) */
        .search-box-container { position: relative; flex: 1; max-width: 500px; }
        .search-box { width: 100%; background: var(--bg-main); border: 1px solid var(--border-color); border-radius: 8px; padding: 10px 40px 10px 15px; color: var(--text-primary); font-size: 14px; outline: none; }
        .search-box-container i { position: absolute; right: 15px; top: 50%; transform: translateY(-50%); color: var(--text-secondary); }
        .autocomplete-suggestions { position: absolute; top: 105%; left: 0; width: 100%; background: var(--bg-card); border: 1px solid var(--border-color); border-radius: 8px; display: none; z-index: 999; box-shadow: 0 10px 25px rgba(0,0,0,0.3); }
        .suggestion-item { padding: 12px 15px; font-size: 13px; cursor: pointer; border-bottom: 1px solid var(--border-color); }
        .suggestion-item:hover { background: var(--accent-glow); color: var(--accent); }

        .nav-right { display: flex; align-items: center; gap: 20px; }
        .menu-links { display: flex; list-style: none; gap: 20px; font-size: 14px; font-weight: 500; }
        .menu-links a:hover { color: var(--accent); }
        .cart-icon { position: relative; cursor: pointer; font-size: 18px; }
        .cart-badge { position: absolute; top: -8px; right: -10px; background: var(--price-color); color: white; font-size: 10px; padding: 2px 6px; border-radius: 10px; font-weight: bold; }

        /* BANNER KHUYẾN MÃI / FLASH SALE */
        .flash-sale-bar { background: linear-gradient(90deg, #b91c1c, var(--price-color)); color: white; padding: 10px 0; text-align: center; font-size: 13px; font-weight: 600; }

        /* BỘ LỌC SẢN PHẨM PHÂN CẤP (FILTER) */
        .catalog-section { display: grid; grid-template-columns: 280px 1fr; gap: 30px; margin-top: 30px; }
        .sidebar-filter { background: var(--bg-card); border: 1px solid var(--border-color); border-radius: 12px; padding: 20px; height: fit-content; }
        .filter-group { margin-bottom: 20px; }
        .filter-group h3 { font-size: 14px; text-transform: uppercase; margin-bottom: 10px; color: var(--text-secondary); letter-spacing: 0.5px; }
        .filter-group select, .filter-group input { width: 100%; background: var(--bg-main); border: 1px solid var(--border-color); color: var(--text-primary); padding: 8px; border-radius: 6px; outline: none; font-size: 13px; }

        /* LƯỚI SẢN PHẨM CHUẨN MONSUB */
        .products-grid { display: grid; grid-template-columns: repeat(auto-fill, minmax(240px, 1fr)); gap: 20px; }
        .product-card { background: var(--bg-card); border: 1px solid var(--border-color); border-radius: 12px; overflow: hidden; position: relative; transition: all 0.2s; }
        .product-card:hover { border-color: var(--accent); box-shadow: 0 0 15px var(--accent-glow); transform: translateY(-2px); }
        .img-wrapper { position: relative; width: 100%; height: 220px; overflow: hidden; background: #fff; }
        .product-img { width: 100%; height: 100%; object-fit: cover; transition: transform 0.3s; }
        .product-card:hover .product-img { transform: scale(1.08); }
        .product-tag { position: absolute; top: 10px; left: 10px; background: var(--price-color); color: white; font-size: 11px; font-weight: 600; padding: 3px 8px; border-radius: 4px; }
        .product-info { padding: 15px; }
        .product-brand { font-size: 11px; color: var(--text-secondary); text-transform: uppercase; margin-bottom: 5px; }
        .product-title { font-size: 15px; font-weight: 600; margin-bottom: 8px; white-space: nowrap; overflow: hidden; text-overflow: ellipsis; }
        .price-box { display: flex; align-items: center; gap: 10px; margin-bottom: 12px; }
        .curr-price { color: var(--price-color); font-weight: 700; font-size: 16px; }
        .old-price { color: var(--text-secondary); text-decoration: line-through; font-size: 13px; }
        .btn-add-cart { width: 100%; background: transparent; border: 1px solid var(--accent); color: var(--accent); padding: 10px; border-radius: 8px; font-weight: 600; font-size: 13px; cursor: pointer; transition: 0.2s; }
        .btn-add-cart:hover { background: var(--accent); color: #0b0f19; }

        /* 2. CHI TIẾT SẢN PHẨM POPUP (MODAL PRODUCT PAGE) */
        .modal { position: fixed; top: 0; left: 0; width: 100%; height: 100%; background: rgba(0,0,0,0.8); display: none; justify-content: center; align-items: center; z-index: 2000; padding: 20px; }
        .modal-content { background: var(--bg-card); border: 1px solid var(--border-color); width: 100%; max-width: 900px; border-radius: 16px; display: grid; grid-template-columns: 1fr 1fr; overflow: hidden; position: relative; animation: fadeIn 0.3s; }
        .modal-close { position: absolute; top: 15px; right: 20px; font-size: 24px; cursor: pointer; color: var(--text-secondary); z-index: 10; }
        .modal-left { padding: 20px; display: flex; flex-direction: column; justify-content: center; background: #fff; position: relative; }
        .zoom-container { overflow: hidden; cursor: zoom-in; width: 100%; height: 350px; }
        .zoom-container img { width: 100%; height: 100%; object-fit: contain; transition: transform 0.1s; }
        .modal-right { padding: 30px; display: flex; flex-direction: column; justify-content: space-between; overflow-y: auto; max-height: 550px; }
        
        /* 3. GIỎ HÀNG & QUY TRÌNH THANH TOÁN (CHECKOUT MODAL) */
        .checkout-container { display: none; position: fixed; top: 0; right: 0; width: 450px; height: 100%; background: var(--bg-card); border-left: 1px solid var(--border-color); z-index: 2000; padding: 30px; box-shadow: -10px 0 30px rgba(0,0,0,0.5); overflow-y: auto; }
        .checkout-header { display: flex; justify-content: space-between; align-items: center; margin-bottom: 20px; padding-bottom: 10px; border-bottom: 1px solid var(--border-color); }
        .form-group { margin-bottom: 15px; }
        .form-group label { display: block; font-size: 12px; color: var(--text-secondary); margin-bottom: 5px; }
        .form-group input, .form-group select { width: 100%; background: var(--bg-main); border: 1px solid var(--border-color); color: var(--text-primary); padding: 10px; border-radius: 6px; outline: none; }
        .payment-methods { display: grid; grid-template-columns: 1fr 1fr; gap: 10px; margin-top: 10px; }
        .pay-method-card { border: 1px solid var(--border-color); padding: 12px; text-align: center; border-radius: 8px; cursor: pointer; font-size: 13px; }
        .pay-method-card.active { border-color: var(--accent); background: var(--accent-glow); color: var(--accent); }
        .qr-box { display: none; text-align: center; margin-top: 15px; padding: 15px; background: #fff; border-radius: 8px; }

        /* 4. ĐÁNH GIÁ (REVIEWS) */
        .reviews-section { margin-top: 20px; border-top: 1px solid var(--border-color); padding-top: 15px; }
        .review-item { font-size: 13px; background: rgba(255,255,255,0.02); padding: 10px; border-radius: 6px; margin-bottom: 8px; }
        .review-user { font-weight: 600; color: var(--accent); display: flex; justify-content: space-between; }
        
        /* COUPON SYSTEM */
        .coupon-box { display: flex; gap: 10px; margin: 15px 0; }
        .btn-apply { background: var(--accent); color: #0b0f19; border: none; padding: 0 15px; border-radius: 6px; font-weight: 600; cursor: pointer; }

        /* LIVE CHAT BOX TRỰC TUYẾN TẠO UY TÍN */
        .live-chat-widgets { position: fixed; bottom: 25px; right: 25px; display: flex; flex-direction: column; gap: 12px; z-index: 999; }
        .chat-icon-btn { width: 50px; height: 50px; border-radius: 50%; display: flex; align-items: center; justify-content: center; color: white; font-size: 22px; box-shadow: 0 4px 12px rgba(0,0,0,0.3); transition: transform 0.2s; }
        .chat-icon-btn:hover { transform: scale(1.1); }
        .btn-zalo { background: #0068ff; }
        .btn-hotline { background: #10b981; }

        /* FOOTER & CHÍNH SÁCH CHUẨN ĐỘ TIN CẬY */
        footer { background: var(--bg-card); border-top: 1px solid var(--border-color); margin-top: 60px; padding: 40px 0 20px 0; font-size: 13px; color: var(--text-secondary); }
        .footer-grid { display: grid; grid-template-columns: 2fr repeat(2, 1fr); gap: 4px; margin-bottom: 30px; }
        .footer-col h4 { color: var(--text-primary); margin-bottom: 15px; font-size: 14px; text-transform: uppercase; }
        .footer-col ul { list-style: none; }
        .footer-col li { margin-bottom: 10px; }
        .footer-col li a:hover { color: var(--accent); }
        .footer-bottom { text-align: center; padding-top: 20px; border-top: 1px solid var(--border-color); font-size: 12px; }

        @keyframes fadeIn { from { opacity: 0; transform: scale(0.95); } to { opacity: 1; transform: scale(1); } }

        /* RESPONSIVE CHUẨN ĐIỆN THOẠI (>70% TRUY CẬP) */
        @media (max-width: 900px) {
            .catalog-section { grid-template-columns: 1fr; }
            .modal-content { grid-template-columns: 1fr; max-height: 90vh; overflow-y: auto; }
            .modal-left { height: 260px; }
            .checkout-container { width: 100%; }
            .menu-links { display: none; }
            .footer-grid { grid-template-columns: 1fr; gap: 20px; }
        }
    </style>
</head>
<body>

    <!-- THANH ĐIỀU HƯỚNG TỐI GIẢN THÔNG MINH -->
    <header>
        <div class="container nav-container">
            <a href="#" class="logo">SONG THỊNH <span>VLXD</span></a>
            
            <!-- Ô Tìm Kiếm Thực Tế Tự Động Gợi Ý -->
            <div class="search-box-container">
                <input type="text" class="search-box" id="mainSearch" placeholder="Tìm kiếm nhanh sắt, thép, xi măng, cát đá..." oninput="handleSearch(this.value)">
                <i class="fas fa-search"></i>
                <div class="autocomplete-suggestions" id="suggestionBox"></div>
            </div>

            <div class="nav-right">
                <ul class="menu-links">
                    <li><a href="#">Trang Chủ</a></li>
                    <li><a href="#cua-hang">Sản Phẩm</a></li>
                    <li><a href="#chinh-sach">Chính Sách</a></li>
                </ul>
                <div class="cart-icon" onclick="toggleCheckout(true)">
                    <i class="fas fa-shopping-bag"></i>
                    <span class="cart-badge" id="cartCount">0</span>
                </div>
                <button onclick="toggleTheme()" style="background:none; border:none; color:var(--text-primary); cursor:pointer;"><i class="fas fa-adjust"></i></button>
            </div>
        </div>
    </header>

    <!-- FLASH SALE KÍCH CẦU MARKETING -->
    <div class="flash-sale-bar">
        🔥 FLASH SALE HÔM NAY: Nhập mã <span style="text-decoration: underline; color: #fde047;">ST2026</span> giảm ngay 5% tổng giá trị đơn hàng xây dựng!
    </div>

    <!-- KHU VỰC CỬA HÀNG CHUYÊN NGHIỆP -->
    <main class="container catalog-section" id="cua-hang">
        
        <!-- BỘ LỌC SIDEBAR (FILTER) -->
        <aside class="sidebar-filter">
            <div class="filter-group">
                <h3>Bộ lọc Vật Liệu</h3>
                <select id="filterCategory" onchange="filterProducts()">
                    <option value="all">Tất cả danh mục</option>
                    <option value="thep">Sắt Thép Hệ Thống</option>
                    <option value="ximang">Xi Măng Đóng Bao</option>
                    <option value="catda">Cát Đá Thô</option>
                </select>
            </div>
            <div class="filter-group">
                <h3>Thương Hiệu uy tín</h3>
                <select id="filterBrand" onchange="filterProducts()">
                    <option value="all">Tất cả thương hiệu</option>
                    <option value="Hòa Phát">Hòa Phát</option>
                    <option value="Hà Tiên">Hà Tiên</option>
                    <option value="Việt Nhật">Việt Nhật</option>
                </select>
            </div>
            <div class="filter-group">
                <h3>Khoảng Giá (VNĐ)</h3>
                <select id="filterPrice" onchange="filterProducts()">
                    <option value="all">Mọi mức giá</option>
                    <option value="under-150">Dưới 150.000đ</option>
                    <option value="over-150">Trên 150.000đ</option>
                </select>
            </div>
        </aside>

        <!-- LƯỚI HIỂN THỊ SẢN PHẨM -->
        <section class="products-grid" id="productGridContainer">
            <!-- Dữ liệu được render động bằng JavaScript ở phía dưới để tối ưu SEO và tốc độ -->
        </section>
    </main>

    <!-- 2. TRANG CHI TIẾT SẢN PHẨM PHÓNG TO (PRODUCT DETAILED PAGE MODAL) -->
    <div class="modal" id="productModal">
        <div class="modal-content">
            <span class="modal-close" onclick="closeProductModal()">&times;</span>
            <div class="modal-left">
                <div class="zoom-container" id="zoomArea" onmousemove="zoomImage(event)" onmouseleave="resetZoom()">
                    <img id="modalImg" src="" alt="Sản phẩm">
                </div>
            </div>
            <div class="modal-right">
                <div>
                    <span id="modalBrand" style="font-size:11px; text-transform:uppercase; color:var(--text-secondary);">Thương hiệu</span>
                    <h2 id="modalTitle" style="font-size: 22px; margin: 5px 0 15px 0;">Tên sản phẩm</h2>
                    <div class="price-box">
                        <span class="curr-price" id="modalPrice" style="font-size:24px;">0đ</span>
                    </div>
                    <p id="modalDesc" style="font-size: 14px; color: var(--text-secondary); line-height: 1.6; margin-bottom: 20px;">Mô tả chi tiết</p>
                </div>
                
                <!-- Khu vực hiển thị minh bạch đánh giá thực tế khách hàng -->
                <div class="reviews-section">
                    <h4 style="font-size:13px; margin-bottom:10px;"><i class="fas fa-star" style="color:#eab308"></i> ĐÁNH GIÁ THỰC TẾ (SÀN LỌC)</h4>
                    <div id="modalReviews"></div>
                </div>

                <button class="btn-add-cart" id="modalActionBtn" style="background:var(--accent); color:#0b0f19; font-size:15px; padding:12px; margin-top:20px;">THÊM VÀO GIỎ HÀNG THẦU</button>
            </div>
        </div>
    </div>

    <!-- 3. QUY TRÌNH THANH TOÁN ĐƠN GIẢN RÚT GỌN (CHECKOUT SIDEBAR) -->
    <div class="checkout-container" id="checkoutSidebar">
        <div class="checkout-header">
            <h3>ĐƠN HÀNG CỦA BẠN</h3>
            <span style="cursor:pointer; font-size:20px;" onclick="toggleCheckout(false)">&times;</span>
        </div>
        
        <div id="cartItemsList" style="margin-bottom: 20px;">
            <!-- Danh sách vật liệu đã chọn mua -->
        </div>

        <div class="coupon-box">
            <input type="text" id="couponInput" placeholder="Nhập mã ưu đãi (ST2026)">
            <button class="btn-apply" onclick="applyCoupon()">Áp Dụng</button>
        </div>

        <div style="font-size:16px; font-weight:700; margin-bottom:20px; display:flex; justify-content:space-between;">
            <span>TỔNG KHỐI LƯỢNG TIỀN:</span>
            <span id="cartTotalPrice" style="color:var(--price-color);">0đ</span>
        </div>

        <!-- MUA HÀNG KHÔNG CẦN ĐĂNG KÝ KÝ TÀI KHOẢN -->
        <h4 style="font-size:13px; margin-bottom:15px; text-transform:uppercase; color:var(--text-secondary)">Thông tin giao hàng nhanh</h4>
        <div class="form-group">
            <label>Tên nhà thầu / Khách hàng *</label>
            <input type="text" id="customerName" placeholder="Ví dụ: Nguyễn Văn A">
        </div>
        <div class="form-group">
            <label>Số điện thoại nhận vật tư *</label>
            <input type="tel" id="customerPhone" placeholder="Ví dụ: 0912345678">
        </div>
        <div class="form-group">
            <label>Địa chỉ nhận hàng (Công trình) *</label>
            <input type="text" id="customerAddress" placeholder="Số nhà, Tên đường, Quận/Huyện">
        </div>

        <!-- PHƯƠNG THỨC THANH TOÁN LINH HOẠT -->
        <label style="font-size:12px; color:var(--text-secondary)">Phương thức thanh toán</label>
        <div class="payment-methods">
            <div class="pay-method-card active" id="payCOD" onclick="setPayment('COD')"><i class="fas fa-truck"></i> Tiền mặt khi nhận hàng (COD)</div>
            <div class="pay-method-card" id="payBank" onclick="setPayment('BANK')"><i class="fas fa-qrcode"></i> Chuyển khoản QR ngân hàng</div>
        </div>

        <div class="qr-box" id="qrBoxArea">
            <p style="color:#0f172a; font-size:12px; font-weight:600; margin-bottom:10px;">Quét mã QR để chuyển khoản nhanh tổng đài</p>
            <img src="https://api.qrserver.com/v1/create-qr-code/?size=150x150&data=ST-VLXD-SONGTHINH" alt="Mã QR thanh toán">
        </div>

        <button class="btn-add-cart" style="background:var(--price-color); color:white; border:none; font-size:15px; font-weight:700; padding:14px; margin-top:20px;" onclick="submitOrder()">XÁC NHẬN ĐẶT HÀNG NGAY</button>
    </div>

    <!-- TÍN HIỆU UY TÍN CHĂM SÓC KHÁCH HÀNG (LIVE CHAT & PHONE) -->
    <div class="live-chat-widgets">
        <a href="https://zalo.me/0123456789" target="_blank" class="chat-icon-btn btn-zalo" title="Tư vấn kỹ thuật qua Zalo"><i class="fab fa-talking-tech"></i>Zalo</a>
        <a href="tel:0123456789" class="chat-icon-btn btn-hotline" title="Hotline điều phối xe tải bãi"><i class="fas fa-phone-alt"></i></a>
    </div>

    <!-- FOOTER CHÍNH SÁCH BẢO MẬT MINH BẠCH -->
    <footer id="chinh-sach">
        <div class="container footer-grid">
            <div class="footer-col">
                <h4>CÔNG TY TNHH VLXD SONG THỊNH</h4>
                <p style="line-height: 1.6; margin-bottom: 10px;">Tổng đại lý cung cấp các giải pháp vật liệu xây dựng thô và hoàn thiện chất lượng cao hàng đầu khu vực.</p>
                <p><i class="fas fa-map-marker-alt"></i> Văn phòng & Tổng Kho: TP. Hồ Chí Minh, Việt Nam</p>
                <p><i class="fas fa-envelope"></i> Email: kinhdoanh@songthinhvlxd.com</p>
                <p><i class="fas fa-shield-alt"></i> Website bảo mật mã hóa SSL Chứng chỉ xanh cao cấp.</p>
            </div>
            <div class="footer-col">
                <h4>CHÍNH SÁCH DOANH NGHIỆP</h4>
                <ul>
                    <li><a href="#">Chính sách vận chuyển xe tải ben</a></li>
                    <li><a href="#">Quy trình đổi trả vật tư lỗi bãi</a></li>
                    <li><a href="#">Chính sách bảo mật dữ liệu thầu</a></li>
                    <li><a href="#">Điều khoản công nợ dài hạn</a></li>
                </ul>
            </div>
            <div class="footer-col">
                <h4>ĐƠN VỊ VẬN CHUYỂN LIÊN KẾT</h4>
                <p style="margin-bottom: 8px;"><i class="fas fa-check-circle" style="color:var(--accent)"></i> Đội xe tự hành Song Thịnh (Giao nhanh 2h)</p>
                <p><i class="fas fa-check-circle" style="color:var(--accent)"></i> Liên kết hạ tầng toàn quốc: GHTK, Viettel Post.</p>
            </div>
        </div>
        <div class="footer-bottom">
            &copy; 2026 CÔNG TY TNHH VLXD SONG THỊNH. Tất cả quyền được bảo lưu. Thiết kế tinh tế tối giản theo cấu trúc lõi MonSub.
        </div>
    </footer>

    <!-- LOGIC VẬN HÀNH TOÀN BỘ WEBSITE (CORE ENGINE JS) -->
    <script>
        // NƠI LƯU TRỮ CƠ SỞ DỮ LIỆU SẢN PHẨM CHUẨN SEO
        const PRODUCTS_DB = [
            { id: 1, category: 'thep', brand: 'Hòa Phát', title: 'Thép Cuộn Phi 6 Hòa Phát mác CB300', price: 145000, oldPrice: 170000, img: 'https://images.unsplash.com/photo-1589939705384-5185137a7f0f?auto=format&fit=crop&q=80&w=400', desc: 'Thép cuộn chính hãng Hòa Phát, siêu bền dẻo, chuyên dụng cho đổ bê tông móng, sàn chung cư cao tầng. Đầy đủ CO/CQ từ nhà máy.', reviews: [{user:'Anh Hải (Thầu xây dựng)', text:'Thép dẻo, kéo uốn rất tốt, giao hàng đủ khối lượng cân bãi.'}, {user:'Minh Tuấn', text:'Giao hàng nhanh đúng hẹn đêm khuya.'}] },
            { id: 2, category: 'ximang', brand: 'Hà Tiên', title: 'Xi Măng Hà Tiên Đa Dụng PCB40', price: 89000, oldPrice: 99000, img: 'https://images.unsplash.com/photo-1517646287270-a5a9ca602e5c?auto=format&fit=crop&q=80&w=400', desc: 'Xi măng mác cao PCB40 chuyên dụng tô trát tường mịn, độ kết dính cực cao, hạn chế tối đa rạn nứt bề mặt công trình xây dựng dân dụng.', reviews: [{user:'Thầu Thạch', text:'Trát tường rất mịn màng, đông kết chuẩn thời gian.'}] },
            { id: 3, category: 'thep', brand: 'Việt Nhật', title: 'Thép Thanh Vằn Phi 12 Việt Nhật', price: 195000, oldPrice: 220000, img: 'https://images.unsplash.com/photo-1504307651254-35680f356dfd?auto=format&fit=crop&q=80&w=400', desc: 'Thép cốt bê tông thanh vằn Việt Nhật chịu tải cực cao, tiêu chuẩn công nghệ kỹ thuật Nhật Bản nghiêm ngặt.', reviews: [] },
            { id: 4, category: 'catda', brand: 'Khác', title: 'Cát Xây Tô Sàng Lọc Hạt Mịn', price: 130000, oldPrice: 150000, img: 'https://images.unsplash.com/photo-1600585154340-be6161a56a0c?auto=format&fit=crop&q=80&w=400', desc: 'Cát khai thác tự nhiên tại lòng sông lớn, đã qua hệ thống sàng lọc loại bỏ hoàn toàn tạp chất, bùn đất hữu cơ sạch 100%.', reviews: [{user:'Chú Năm Biên Hòa', text:'Cát sạch, trộn vữa xây rất dôi.'}] }
        ];

        let GIO_HANG = [];
        let UU_DAI_GIAM_GIA = 1; // Hệ số nhân tính tiền khi dùng coupon
        let PHUONG_THUC_TT = 'COD';

        // KHỞI TẠO TẢI SẢN PHẨM REALTIME SIÊU TỐC
        window.addEventListener('DOMContentLoaded', () => {
            renderProducts(PRODUCTS_DB);
        });

        function renderProducts(dataList) {
            const container = document.getElementById('productGridContainer');
            container.innerHTML = '';
            if(dataList.length === 0) {
                container.innerHTML = `<p style="grid-column:1/-1; text-align:center; color:var(--text-secondary);">Không tìm thấy vật liệu phù hợp với bộ lọc lọc.</p>`;
                return;
            }
            dataList.forEach(p => {
                container.innerHTML += `
                    <div class="product-card">
                        <span class="product-tag">Bán Chạy</span>
                        <div class="img-wrapper" onclick="openProductModal(${p.id})">
                            <img src="${p.img}" class="product-img" alt="${p.title}">
                        </div>
                        <div class="product-info">
                            <div class="product-brand">${p.brand}</div>
                            <h3 class="product-title" onclick="openProductModal(${p.id})">${p.title}</h3>
                            <div class="price-box">
                                <span class="curr-price">${p.price.toLocaleString()}đ</span>
                                <span class="old-price">${p.oldPrice.toLocaleString()}đ</span>
                            </div>
                            <button class="btn-add-cart" onclick="addToCart(${p.id})"><i class="fas fa-cart-plus"></i> Chọn Vật Tư</button>
                        </div>
                    </div>
                `;
            });
        }

        /* 1. LOGIC THANH TÌM KIẾM AUTOCOMPLETE MẠNH MẼ */
        function handleSearch(keyword) {
            const box = document.getElementById('suggestionBox');
            if (!keyword.trim()) { box.style.display = 'none'; return; }
            
            const matches = PRODUCTS_DB.filter(p => p.title.toLowerCase().includes(keyword.toLowerCase()));
            if(matches.length === 0) { box.style.display = 'none'; return; }

            box.innerHTML = '';
            matches.slice(0, 5).forEach(m => {
                const item = document.createElement('div');
                item.className = 'suggestion-item';
                item.innerText = m.title;
                item.onclick = () => {
                    document.getElementById('mainSearch').value = m.title;
                    box.style.display = 'none';
                    openProductModal(m.id);
                };
                box.appendChild(item);
            });
            box.style.display = 'block';
        }

        /* 1B. LOGIC BỘ LỌC PHÂN LOẠI DANH MỤC TRỰC QUAN */
        function filterProducts() {
            const cat = document.getElementById('filterCategory').value;
            const brand = document.getElementById('filterBrand').value;
            const priceRange = document.getElementById('filterPrice').value;

            let filtered = PRODUCTS_DB;

            if (cat !== 'all') filtered = filtered.filter(p => p.category === cat);
            if (brand !== 'all') filtered = filtered.filter(p => p.brand === brand);
            if (priceRange !== 'all') {
                if (priceRange === 'under-150') filtered = filtered.filter(p => p.price < 150000);
                if (priceRange === 'over-150') filtered = filtered.filter(p => p.price >= 150000);
            }
            renderProducts(filtered);
        }

        /* 2. CHỨC NĂNG ZOOM TRANG CHI TIẾT SẢN PHẨM */
        function openProductModal(id) {
            const p = PRODUCTS_DB.find(x => x.id === id);
            document.getElementById('modalImg').src = p.img;
            document.getElementById('modalBrand').innerText = p.brand;
            document.getElementById('modalTitle').innerText = p.title;
            document.getElementById('modalPrice').innerText = p.price.toLocaleString() + 'đ';
            document.getElementById('modalDesc').innerText = p.desc;
            
            // Render Review
            const reviewArea = document.getElementById('modalReviews');
            reviewArea.innerHTML = p.reviews.length === 0 ? '<p style="color:var(--text-secondary)">Chưa có đánh giá nào cho đợt hàng này.</p>' : '';
            p.reviews.forEach(r => {
                reviewArea.innerHTML += `<div class="review-item"><div class="review-user">${r.user} <span>⭐⭐⭐⭐⭐</span></div><div>${r.text}</div></div>`;
            });

            document.getElementById('modalActionBtn').onclick = () => { addToCart(p.id); closeProductModal(); };
            document.getElementById('productModal').style.display = 'flex';
        }

        function closeProductModal() { document.getElementById('productModal').style.display = 'none'; }
        
        function zoomImage(e) {
            const img = document.querySelector('#zoomArea img');
            const box = document.getElementById('zoomArea');
            const x = e.clientX - box.offsetLeft;
            const y = e.clientY - box.offsetTop;
            img.style.transformOrigin = `${x}px ${y}px`;
            img.style.transform = 'scale(1.8)';
        }
        function resetZoom() { document.querySelector('#zoomArea img').style.transform = 'scale(1)'; }

        /* 3. QUY TRÌNH QUẢN LÝ GIỎ HÀNG & CHECKOUT KHÔNG CẦN ĐĂNG KÝ */
        function addToCart(id) {
            const item = PRODUCTS_DB.find(p => p.id === id);
            GIO_HANG.push(item);
            updateCartUI();
        }

        function updateCartUI() {
            document.getElementById('cartCount').innerText = GIO_HANG.length;
            const container = document.getElementById('cartItemsList');
            container.innerHTML = '';
            
            let total = 0;
            GIO_HANG.forEach((p, idx) => {
                total += p.price;
                container.innerHTML += `
                    <div style="display:flex; justify-content:space-between; align-items:center; background:var(--bg-main); padding:10px; border-radius:6px; margin-bottom:8px; font-size:13px;">
                        <span style="white-space:nowrap; overflow:hidden; text-overflow:ellipsis; max-width:240px;">${p.title}</span>
                        <span style="font-weight:600; color:var(--price-color);">${p.price.toLocaleString()}đ</span>
                        <i class="fas fa-trash-alt" style="cursor:pointer; color:var(--text-secondary)" onclick="removeFromCart(${idx})"></i>
                    </div>
                `;
            });
            
            document.getElementById('cartTotalPrice').innerText = (total * UU_DAI_GIAM_GIA).toLocaleString() + 'đ';
        }

        function removeFromCart(index) {
            GIO_HANG.splice(index, 1);
            updateCartUI();
        }

        function toggleCheckout(open) {
            document.getElementById('checkoutSidebar').style.display = open ? 'block' : 'none';
        }

        function applyCoupon() {
            const code = document.getElementById('couponInput').value.trim();
            if(code === 'ST2026') {
                UU_DAI_GIAM_GIA = 0.95; // Giảm 5% tổng hóa đơn
                alert("Áp dụng mã giảm giá 5% thành công!");
                updateCartUI();
            } else {
                alert("Mã giảm giá không hợp lệ hoặc đã hết hạn.");
            }
        }

        function setPayment(method) {
            PHUONG_THUC_TT = method;
            document.getElementById('payCOD').className = 'pay-method-card' + (method === 'COD' ? ' active' : '');
            document.getElementById('payBank').className = 'pay-method-card' + (method === 'BANK' ? ' active' : '');
            document.getElementById('qrBoxArea').style.display = method === 'BANK' ? 'block' : 'none';
        }

        function submitOrder() {
            const name = document.getElementById('customerName').value.trim();
            const phone = document.getElementById('customerPhone').value.trim();
            const addr = document.getElementById('customerAddress').value.trim();

            if(GIO_HANG.length === 0) { alert("Giỏ hàng của bạn đang trống!"); return; }
            if(!name || !phone || !addr) { alert("Vui lòng điền đầy đủ các thông tin có dấu * để bộ phận xe bãi Song Thịnh chạy đơn!"); return; }

            alert(`🎉 ĐẶT HÀNG THÀNH CÔNG!\nChào hệ thống thầu ${name}, đơn hàng đang được điều phối nhân viên liên hệ xác nhận lộ trình qua số di động ${phone} trong vòng 5-15 phút. Cảm ơn đã tin tưởng Song Thịnh!`);
            GIO_HANG = [];
            updateCartUI();
            toggleCheckout(false);
        }

        // LOGIC CHUYỂN ĐỔI GIAO DIỆN (THEME)
        function toggleTheme() {
            const body = document.body;
            if (body.getAttribute('data-theme') === 'light') {
                body.removeAttribute('data-theme');
            } else {
                body.setAttribute('data-theme', 'light');
            }
        }
    </script>
</body>
</html>
