<!DOCTYPE html>
<html lang="ko">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>맘스터치 - 빠르게보다 올바르게</title>
    <link href="https://fonts.googleapis.com/css2?family=Noto+Sans+KR:wght@300;400;700;900&display=swap" rel="stylesheet">
    <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.4.0/css/all.min.css">

    <style>
        /* [CSS 변수 및 기본 설정] */
        :root {
            --primary: #FFC300;
            --secondary: #4A3B32;
            --accent: #E53935;
            --bg-color: #ffffff;
            --card-bg: #ffffff;
            --text-main: #333333;
            --text-sub: #666666;
            --border: #eeeeee;
            --shadow: rgba(0,0,0,0.1);
        }

        body.dark-mode {
            --bg-color: #1a1a1a;
            --card-bg: #2d2d2d;
            --text-main: #f1f1f1;
            --text-sub: #aaaaaa;
            --border: #444444;
            --shadow: rgba(0,0,0,0.5);
            --secondary: #FFC300; 
        }

        * { margin: 0; padding: 0; box-sizing: border-box; font-family: 'Noto Sans KR', sans-serif; transition: background-color 0.3s, color 0.3s; }
        body { background-color: var(--bg-color); color: var(--text-main); overflow-x: hidden; }
        a { text-decoration: none; color: inherit; }
        ul { list-style: none; }
        button { border: none; cursor: pointer; }

        /* [애니메이션] 스크롤 시 등장 효과 */
        .reveal {
            opacity: 0;
            transform: translateY(30px);
            transition: all 0.8s ease-out;
        }
        .reveal.active {
            opacity: 1;
            transform: translateY(0);
        }

        /* 1. 헤더 */
        header {
            position: fixed; top: 0; width: 100%;
            background-color: var(--card-bg);
            box-shadow: 0 2px 10px var(--shadow);
            z-index: 1000;
            height: 70px;
        }

        .header-inner {
            max-width: 1200px; margin: 0 auto; height: 100%;
            display: flex; justify-content: space-between; align-items: center; padding: 0 20px;
        }

        .logo { font-size: 1.8rem; font-weight: 900; color: var(--secondary); letter-spacing: -1px; }
        .logo span { color: var(--accent); }

        /* 데스크탑 메뉴 */
        .nav-menu { display: flex; gap: 20px; font-weight: 700; }
        .nav-menu li:hover { color: var(--primary); }

        .utils { display: flex; align-items: center; gap: 10px; }

        .btn-icon {
            background: var(--bg-color); border: 1px solid var(--text-sub);
            color: var(--text-main); padding: 6px 12px; border-radius: 20px; font-size: 0.8rem;
        }
        select.lang-select {
            padding: 6px; border-radius: 5px; background: var(--bg-color);
            color: var(--text-main); border: 1px solid var(--text-sub);
        }

        /* 햄버거 버튼 (모바일용) */
        .hamburger { display: none; font-size: 1.5rem; color: var(--text-main); background: none; }

        /* 2. 사이드바 (모바일 메뉴) */
        .sidebar {
            position: fixed; top: 0; right: -250px; width: 250px; height: 100%;
            background-color: var(--card-bg); box-shadow: -2px 0 5px var(--shadow);
            z-index: 1100; padding: 20px; transition: right 0.3s ease; display: flex; flex-direction: column; gap: 20px;
        }
        .sidebar.open { right: 0; }
        .sidebar-header { display: flex; justify-content: flex-end; }
        .close-sidebar { font-size: 1.5rem; background: none; color: var(--text-main); }
        .sidebar-menu li { padding: 15px 0; border-bottom: 1px solid var(--border); font-weight: bold; }

        /* 3. 히어로 섹션 */
        .hero {
            margin-top: 70px; height: 500px;
            background: linear-gradient(rgba(0,0,0,0.5), rgba(0,0,0,0.5)), url('https://images.unsplash.com/photo-1568901346375-23c9450c58cd?q=80&w=1599&auto=format&fit=crop');
            background-size: cover; background-position: center;
            display: flex; flex-direction: column; justify-content: center; align-items: center; text-align: center; color: white;
        }
        .hero h1 { font-size: 3rem; margin-bottom: 20px; text-shadow: 2px 2px 5px black; }
        .btn-cta {
            padding: 15px 40px; background-color: var(--primary); color: #000;
            font-size: 1.2rem; font-weight: bold; border-radius: 50px;
            box-shadow: 0 4px 15px rgba(255, 195, 0, 0.4);
        }
        .btn-cta:hover { transform: scale(1.05); background-color: #ffb300; }

        /* 4. 메뉴 리스트 */
        .container { max-width: 1200px; margin: 0 auto; padding: 80px 20px; }
        .section-title { text-align: center; margin-bottom: 50px; }
        .section-title h2 { font-size: 2.5rem; margin-bottom: 10px; }

        .menu-grid {
            display: grid; grid-template-columns: repeat(auto-fit, minmax(280px, 1fr));
            gap: 30px; justify-content: center;
        }

        .card {
            background-color: var(--card-bg); border-radius: 15px; overflow: hidden;
            box-shadow: 0 5px 15px var(--shadow); position: relative; cursor: pointer;
            transition: transform 0.3s;
        }
        .card:hover { transform: translateY(-10px); }
        .card img { width: 100%; height: 250px; object-fit: cover; }
        .badge {
            position: absolute; top: 15px; left: 15px; background-color: var(--accent);
            color: white; padding: 5px 10px; border-radius: 5px; font-weight: bold; font-size: 0.8rem;
        }
        .card-body { padding: 20px; text-align: center; }
        .card-body h3 { font-size: 1.4rem; margin-bottom: 5px; }
        .card-body p { color: var(--text-sub); font-size: 0.9rem; margin-bottom: 15px; height: 40px; }
        .price { font-size: 1.3rem; font-weight: 900; color: var(--text-main); }

        /* 5. 플로팅 장바구니 버튼 */
        .fab-cart {
            position: fixed; bottom: 30px; right: 30px;
            background-color: var(--accent); color: white;
            width: 70px; height: 70px; border-radius: 50%;
            display: flex; justify-content: center; align-items: center;
            font-size: 1.8rem; box-shadow: 0 4px 15px rgba(0,0,0,0.3);
            z-index: 900; cursor: pointer; transition: transform 0.2s;
        }
        .fab-cart:hover { transform: scale(1.1); }
        .cart-count {
            position: absolute; top: 0; right: 0;
            background-color: var(--primary); color: black;
            width: 25px; height: 25px; border-radius: 50%;
            font-size: 0.9rem; font-weight: bold;
            display: flex; justify-content: center; align-items: center;
            border: 2px solid white;
        }

        /* 6. 모달 공통 스타일 */
        .modal {
            display: none; position: fixed; z-index: 2000; left: 0; top: 0;
            width: 100%; height: 100%; background-color: rgba(0,0,0,0.6);
            justify-content: center; align-items: center;
        }
        .modal-content {
            background-color: var(--card-bg); padding: 30px; border-radius: 15px;
            text-align: center; max-width: 500px; width: 90%; position: relative;
            box-shadow: 0 10px 30px rgba(0,0,0,0.5);
            animation: slideUp 0.3s ease-out;
        }
        @keyframes slideUp { from {transform: translateY(50px); opacity: 0;} to {transform: translateY(0); opacity: 1;} }

        /* 상세 정보 모달 스타일 */
        .detail-img { width: 100%; height: 200px; object-fit: cover; border-radius: 10px; margin-bottom: 20px; }
        .nutrition-table {
            width: 100%; margin: 20px 0; border-collapse: collapse;
            font-size: 0.9rem; color: var(--text-main);
        }
        .nutrition-table th, .nutrition-table td {
            border: 1px solid var(--border); padding: 8px;
        }
        .nutrition-table th { background-color: var(--primary); color: #000; }
        
        .modal-btns { display: flex; gap: 10px; justify-content: center; margin-top: 20px; }
        .btn-modal { padding: 10px 20px; border-radius: 5px; font-weight: bold; flex: 1; }
        .btn-close { background-color: var(--border); color: var(--text-main); }
        .btn-add { background-color: var(--accent); color: white; }

        /* 장바구니 모달 스타일 */
        .cart-list { list-style: none; text-align: left; max-height: 300px; overflow-y: auto; margin: 20px 0; border-top: 1px solid var(--border); }
        .cart-item { display: flex; justify-content: space-between; padding: 10px 0; border-bottom: 1px solid var(--border); }
        .cart-total { font-size: 1.5rem; font-weight: 900; color: var(--accent); margin-top: 20px; text-align: right; }

        /* 반응형 */
        @media(max-width: 768px) {
            .nav-menu { display: none; }
            .hamburger { display: block; }
            .hero h1 { font-size: 2rem; }
            .fab-cart { width: 60px; height: 60px; bottom: 20px; right: 20px; font-size: 1.5rem; }
        }
    </style>
</head>
<body>

    <header>
        <div class="header-inner">
            <div class="logo">MOM'S <span>TOUCH</span></div>
            
            <ul class="nav-menu">
                <li><a href="#">브랜드 스토리</a></li>
                <li><a href="#">메뉴소개</a></li>
                <li><a href="#">매장찾기</a></li>
                <li><a href="#">고객센터</a></li>
            </ul>

            <div class="utils">
                <button class="btn-icon" onclick="toggleTheme()"><i class="fas fa-moon"></i></button>
                <select class="lang-select" onchange="changeLanguage(this.value)">
                    <option value="ko">KOR</option>
                    <option value="en">ENG</option>
                    <option value="jp">JPN</option>
                </select>
                <button class="hamburger" onclick="toggleSidebar()"><i class="fas fa-bars"></i></button>
            </div>
        </div>
    </header>

    <div class="sidebar" id="sidebar">
        <div class="sidebar-header">
            <button class="close-sidebar" onclick="toggleSidebar()"><i class="fas fa-times"></i></button>
        </div>
        <ul class="sidebar-menu">
            <li><a href="#">브랜드 스토리</a></li>
            <li><a href="#">메뉴소개</a></li>
            <li><a href="#">매장찾기</a></li>
            <li><a href="#">이벤트</a></li>
            <li><a href="#">고객센터</a></li>
        </ul>
    </div>

    <section class="hero reveal">
        <h1 data-i18n="heroTitle">압도적인 크기, 싸이버거</h1>
        <p data-i18n="heroSub">주문 즉시 조리하는 신선한 수제 버거의 기준</p>
        <button class="btn-cta" onclick="document.querySelector('.container').scrollIntoView({behavior:'smooth'})" data-i18n="orderBtn">주문하기</button>
    </section>

    <section class="container">
        <div class="section-title reveal">
            <h2 data-i18n="menuTitle">맘스터치 대표 메뉴</h2>
            <p data-i18n="menuSub">가성비 그 이상의 감동을 만나보세요</p>
        </div>

        <div class="menu-grid">
            <div class="card reveal" onclick="showDetail(1)">
                <div class="badge">BEST</div>
                <img src="https://images.unsplash.com/photo-1625813506062-0aeb1d7a094b?q=80&w=1500&auto=format&fit=crop" alt="싸이버거">
                <div class="card-body">
                    <h3 data-i18n="menu1_name">싸이버거</h3>
                    <p data-i18n="menu1_desc">매콤바삭한 통다리살 패티가 통째로!</p>
                    <div class="price">₩4,600</div>
                </div>
            </div>

            <div class="card reveal" onclick="showDetail(2)">
                <div class="badge">HOT</div>
                <img src="https://images.unsplash.com/photo-1630384060421-cb20d0e0649d?q=80&w=1450&auto=format&fit=crop" alt="케이준 감자">
                <div class="card-body">
                    <h3 data-i18n="menu3_name">케이준 양념감자</h3>
                    <p data-i18n="menu3_desc">한 번 맛보면 멈출 수 없는 감자튀김.</p>
                    <div class="price">₩2,000</div>
                </div>
            </div>

            <div class="card reveal" onclick="showDetail(3)">
                <div class="badge">NEW</div>
                <img src="https://images.unsplash.com/photo-1626645738196-c2a7c87a8f58?q=80&w=1470&auto=format&fit=crop" alt="치킨">
                <div class="card-body">
                    <h3 data-i18n="menu4_name">후라이드 치킨</h3>
                    <p data-i18n="menu4_desc">겉바속촉의 정석, 맘스터치 치킨.</p>
                    <div class="price">₩16,900</div>
                </div>
            </div>
        </div>
    </section>

    <div class="fab-cart" onclick="openCart()">
        <i class="fas fa-shopping-cart"></i>
        <div class="cart-count" id="cartCount">0</div>
    </div>

    <div id="detailModal" class="modal">
        <div class="modal-content">
            <img id="modalImg" src="" class="detail-img">
            <h2 id="modalTitle">메뉴 이름</h2>
            <p id="modalDesc" style="color:var(--text-sub); margin-bottom:10px;">설명</p>
            <h3 class="price" id="modalPrice">₩0</h3>
            
            <table class="nutrition-table">
                <tr><th>중량(g)</th><th>칼로리(kcal)</th><th>단백질(g)</th><th>나트륨(mg)</th></tr>
                <tr><td id="nutWeight">-</td><td id="nutKcal">-</td><td id="nutProtein">-</td><td id="nutNa">-</td></tr>
            </table>

            <div class="modal-btns">
                <button class="btn-modal btn-close" onclick="closeDetail()">취소</button>
                <button class="btn-modal btn-add" onclick="addToCartFromModal()">장바구니 담기</button>
            </div>
        </div>
    </div>

    <div id="cartModal" class="modal">
        <div class="modal-content">
            <h2><i class="fas fa-shopping-cart"></i> 장바구니</h2>
            <ul class="cart-list" id="cartList">
                <li style="padding:20px; text-align:center;">장바구니가 비었습니다.</li>
            </ul>
            <div class="cart-total" id="cartTotal">Total: ₩0</div>
            <div class="modal-btns">
                <button class="btn-modal btn-close" onclick="closeCart()">더 담기</button>
                <button class="btn-modal btn-add" onclick="alert('주문이 완료되었습니다!')">결제하기</button>
            </div>
        </div>
    </div>

    <footer>
        <p>&copy; 2025 MOM'S TOUCH Clone Project. <br>Designed for Practice.</p>
    </footer>

    <script>
        // --- 1. 데이터베이스 (상품 정보) ---
        const products = {
            1: { name: "싸이버거", price: 4600, img: "https://images.unsplash.com/photo-1625813506062-0aeb1d7a094b?q=80&w=1500&auto=format&fit=crop", desc: "매콤바삭한 통다리살 패티가 통째로 들어간 시그니처 버거", nutrition: {w: 230, kcal: 594, p: 28, na: 1025} },
            2: { name: "케이준 양념감자", price: 2000, img: "https://images.unsplash.com/photo-1630384060421-cb20d0e0649d?q=80&w=1450&auto=format&fit=crop", desc: "맘스터치만의 비법 양념으로 튀겨낸 바삭한 감자튀김", nutrition: {w: 100, kcal: 313, p: 4, na: 620} },
            3: { name: "후라이드 치킨", price: 16900, img: "https://images.unsplash.com/photo-1626645738196-c2a7c87a8f58?q=80&w=1470&auto=format&fit=crop", desc: "겉은 바삭하고 속은 촉촉한 클래식 치킨의 정석", nutrition: {w: 800, kcal: 2150, p: 140, na: 3200} }
        };

        let cart = []; // 장바구니 배열
        let currentProductId = null; // 현재 보고 있는 상품 ID

        // --- 2. 스크롤 애니메이션 (Intersection Observer) ---
        const observer = new IntersectionObserver((entries) => {
            entries.forEach(entry => {
                if (entry.isIntersecting) {
                    entry.target.classList.add('active');
                }
            });
        }, { threshold: 0.1 });

        document.querySelectorAll('.reveal').forEach(el => observer.observe(el));

        // --- 3. 상세 보기 모달 기능 ---
        function showDetail(id) {
            currentProductId = id;
            const p = products[id];
            
            document.getElementById('modalTitle').innerText = p.name;
            document.getElementById('modalDesc').innerText = p.desc;
            document.getElementById('modalPrice').innerText = `₩${p.price.toLocaleString()}`;
            document.getElementById('modalImg').src = p.img;
            
            // 영양정보 바인딩
            document.getElementById('nutWeight').innerText = p.nutrition.w;
            document.getElementById('nutKcal').innerText = p.nutrition.kcal;
            document.getElementById('nutProtein').innerText = p.nutrition.p;
            document.getElementById('nutNa').innerText = p.nutrition.na;

            document.getElementById('detailModal').style.display = 'flex';
        }

        function closeDetail() {
            document.getElementById('detailModal').style.display = 'none';
        }

        // --- 4. 장바구니 기능 ---
        function addToCartFromModal() {
            if (currentProductId) {
                cart.push(products[currentProductId]);
                updateCartUI();
                closeDetail();
                
                // 버튼에 애니메이션 효과
                const btn = document.querySelector('.fab-cart');
                btn.style.transform = "scale(1.3)";
                setTimeout(() => btn.style.transform = "scale(1)", 200);
            }
        }

        function updateCartUI() {
            document.getElementById('cartCount').innerText = cart.length;
        }

        function openCart() {
            const list = document.getElementById('cartList');
            const totalEl = document.getElementById('cartTotal');
            list.innerHTML = "";
            let total = 0;

            if (cart.length === 0) {
                list.innerHTML = "<li style='padding:20px; text-align:center;'>아직 담은 메뉴가 없습니다.</li>";
            } else {
                cart.forEach((item, index) => {
                    total += item.price;
                    list.innerHTML += `
                        <li class="cart-item">
                            <span>${item.name}</span>
                            <span style="font-weight:bold;">₩${item.price.toLocaleString()}</span>
                            <button onclick="removeFromCart(${index})" style="color:red; background:none; margin-left:10px;"><i class="fas fa-trash"></i></button>
                        </li>
                    `;
                });
            }
            totalEl.innerText = `Total: ₩${total.toLocaleString()}`;
            document.getElementById('cartModal').style.display = 'flex';
        }

        function removeFromCart(index) {
            cart.splice(index, 1);
            updateCartUI();
            openCart(); // UI 갱신을 위해 다시 호출
        }

        function closeCart() {
            document.getElementById('cartModal').style.display = 'none';
        }

        // --- 5. 모바일 사이드바 & 테마 ---
        function toggleSidebar() {
            document.getElementById('sidebar').classList.toggle('open');
        }

        function toggleTheme() {
            document.body.classList.toggle('dark-mode');
        }

        // --- 6. 다국어 (간단 구현) ---
        const translations = {
            ko: { heroTitle: "압도적인 크기, 싸이버거", orderBtn: "주문하기" },
            en: { heroTitle: "Overwhelming Size, Thigh Burger", orderBtn: "Order Now" },
            jp: { heroTitle: "圧倒的な大きさ、サイバーガー", orderBtn: "注文する" }
        };

        function changeLanguage(lang) {
            const t = translations[lang];
            if(!t) return;
            if(t.heroTitle) document.querySelector('[data-i18n="heroTitle"]').innerText = t.heroTitle;
            if(t.orderBtn) document.querySelector('[data-i18n="orderBtn"]').innerText = t.orderBtn;
            // (다른 텍스트도 필요 시 추가 가능)
        }

        // 모달 밖 클릭 시 닫기
        window.onclick = function(event) {
            if (event.target.classList.contains('modal')) {
                event.target.style.display = "none";
            }
        }
    </script>
</body>
</html>
