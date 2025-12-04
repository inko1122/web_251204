<!DOCTYPE html>
<html lang="ko">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>골든 크리스피 - 프리미엄 치킨</title>
    <link href="https://fonts.googleapis.com/css2?family=Noto+Sans+KR:wght@300;500;700;900&display=swap" rel="stylesheet">
    
    <style>
        /* [CSS 설정 시작] */
        
        /* 1. 기본 설정 및 변수 */
        :root {
            --primary-color: #FFA500; /* 황금빛 오렌지 */
            --secondary-color: #C8102E; /* 강렬한 레드 */
            --text-color: #333333;
            --bg-light: #f9f9f9;
            --white: #ffffff;
        }

        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
            font-family: 'Noto Sans KR', sans-serif;
        }

        body {
            color: var(--text-color);
            line-height: 1.6;
            background-color: var(--bg-light);
        }

        a {
            text-decoration: none;
            color: inherit;
        }

        ul {
            list-style: none;
        }

        /* 2. 헤더 스타일 */
        header {
            background-color: var(--white);
            box-shadow: 0 2px 5px rgba(0,0,0,0.1);
            position: fixed;
            width: 100%;
            top: 0;
            z-index: 1000;
        }

        .container {
            max-width: 1200px;
            margin: 0 auto;
            padding: 0 20px;
        }

        nav {
            display: flex;
            justify-content: space-between;
            align-items: center;
            height: 80px;
        }

        .logo {
            font-size: 24px;
            font-weight: 900;
            color: var(--secondary-color);
        }

        .nav-links {
            display: flex;
            gap: 30px;
        }

        .nav-links li a {
            font-weight: 700;
            transition: color 0.3s;
        }

        .nav-links li a:hover {
            color: var(--primary-color);
        }

        .btn-order {
            background-color: var(--secondary-color);
            color: var(--white);
            padding: 10px 25px;
            border-radius: 30px;
            font-weight: bold;
            transition: background 0.3s;
        }

        .btn-order:hover {
            background-color: #a00d24;
        }

        /* 3. 히어로 섹션 (메인 배너) */
        .hero {
            margin-top: 80px; /* 헤더 높이만큼 띄움 */
            height: 600px;
            background: linear-gradient(rgba(0,0,0,0.5), rgba(0,0,0,0.5)), url('https://images.unsplash.com/photo-1626082927389-6cd097cdc6ec?q=80&w=1470&auto=format&fit=crop'); /* 치킨 이미지 배경 */
            background-size: cover;
            background-position: center;
            display: flex;
            align-items: center;
            justify-content: center;
            text-align: center;
            color: var(--white);
        }

        .hero-content h1 {
            font-size: 3.5rem;
            margin-bottom: 20px;
            text-shadow: 2px 2px 4px rgba(0,0,0,0.5);
        }

        .hero-content p {
            font-size: 1.5rem;
            margin-bottom: 30px;
            font-weight: 300;
        }

        .btn-hero {
            background-color: var(--primary-color);
            color: var(--white);
            padding: 15px 40px;
            font-size: 1.2rem;
            border-radius: 5px;
            font-weight: bold;
            border: none;
            cursor: pointer;
            transition: transform 0.2s;
        }

        .btn-hero:hover {
            transform: scale(1.05);
            background-color: #ff8c00;
        }

        /* 4. 베스트 메뉴 섹션 */
        .menu-section {
            padding: 80px 0;
            background-color: var(--white);
        }

        .section-title {
            text-align: center;
            font-size: 2.5rem;
            margin-bottom: 50px;
            color: var(--secondary-color);
            font-weight: 800;
        }

        .menu-grid {
            display: grid;
            grid-template-columns: repeat(auto-fit, minmax(300px, 1fr));
            gap: 30px;
        }

        .menu-card {
            background: var(--white);
            border-radius: 15px;
            overflow: hidden;
            box-shadow: 0 5px 15px rgba(0,0,0,0.1);
            transition: transform 0.3s ease;
            cursor: pointer;
            border: 1px solid #eee;
        }

        .menu-card:hover {
            transform: translateY(-10px);
        }

        .menu-img {
            width: 100%;
            height: 250px;
            background-color: #ddd;
            object-fit: cover;
        }

        .menu-info {
            padding: 25px;
            text-align: center;
        }

        .menu-info h3 {
            font-size: 1.5rem;
            margin-bottom: 10px;
            color: #333;
        }

        .menu-info p {
            color: #666;
            margin-bottom: 15px;
        }

        .price {
            font-size: 1.2rem;
            font-weight: bold;
            color: var(--secondary-color);
        }

        /* 5. 브랜드 스토리 (홍보 배너 스타일) */
        .promo-section {
            padding: 100px 0;
            background-color: #FFF8E1; /* 연한 노란색 */
            text-align: center;
        }

        .promo-content {
            max-width: 800px;
            margin: 0 auto;
        }

        .promo-content h2 {
            font-size: 2.5rem;
            margin-bottom: 20px;
        }

        /* 6. 푸터 */
        footer {
            background-color: #222;
            color: #888;
            padding: 50px 0;
            text-align: center;
        }

        .footer-links {
            margin-bottom: 20px;
        }

        .footer-links a {
            margin: 0 10px;
            font-size: 0.9rem;
        }

        .copyright {
            font-size: 0.8rem;
        }

        /* 반응형 처리 */
        @media (max-width: 768px) {
            .hero-content h1 { font-size: 2.5rem; }
            .nav-links { display: none; } /* 모바일에서는 메뉴 숨김 (간소화) */
        }
    </style>
</head>
<body>

    <header>
        <div class="container">
            <nav>
                <div class="logo">GOLDEN CRISPY</div>
                <ul class="nav-links">
                    <li><a href="#">브랜드 스토리</a></li>
                    <li><a href="#">메뉴 소개</a></li>
                    <li><a href="#">매장 찾기</a></li>
                    <li><a href="#">이벤트</a></li>
                </ul>
                <a href="#" class="btn-order">온라인 주문</a>
            </nav>
        </div>
    </header>

    

[Image of delicious fried chicken banner]

    <section class="hero">
        <div class="hero-content">
            <h1>오늘 밤은, 황금빛 바삭함!</h1>
            <p>100% 엑스트라 버진 올리브오일로 튀겨낸 건강한 치킨</p>
            <button class="btn-hero">메뉴 보러가기</button>
        </div>
    </section>

    <section class="menu-section">
        <div class="container">
            <h2 class="section-title">BEST MENU</h2>
            <div class="menu-grid">
                <div class="menu-card">
                    <img src="https://images.unsplash.com/photo-1626645738196-c2a7c87a8f58?q=80&w=1470&auto=format&fit=crop" alt="황금 올리브 치킨" class="menu-img">
                    <div class="menu-info">
                        <h3>황금 크리스피</h3>
                        <p>바삭함의 절정! 육즙 가득한 대표 메뉴</p>
                        <span class="price">20,000원</span>
                    </div>
                </div>

                <div class="menu-card">
                    <img src="https://images.unsplash.com/photo-1569058242253-92a9c755a0ec?q=80&w=1470&auto=format&fit=crop" alt="양념 치킨" class="menu-img">
                    <div class="menu-info">
                        <h3>시크릿 양념</h3>
                        <p>매콤달콤한 비법 소스의 환상적인 조화</p>
                        <span class="price">21,500원</span>
                    </div>
                </div>

                <div class="menu-card">
                    <img src="https://images.unsplash.com/photo-1513639776629-7b611594e29b?q=80&w=1472&auto=format&fit=crop" alt="간장 치킨" class="menu-img">
                    <div class="menu-info">
                        <h3>소이 갈릭</h3>
                        <p>단짠단짠 간장 소스와 마늘의 풍미</p>
                        <span class="price">21,500원</span>
                    </div>
                </div>
            </div>
        </div>
    </section>

    <section class="promo-section">
        <div class="container promo-content">
            <h2>깨끗한 오일, 정직한 맛</h2>
            <p>우리는 타협하지 않습니다. 매일 교체하는 깨끗한 오일과<br>국내산 신선육만을 사용하여 최고의 맛을 선사합니다.</p>
        </div>
    </section>

    <footer>
        <div class="container">
            <div class="footer-links">
                <a href="#">이용약관</a>
                <a href="#">개인정보처리방침</a>
                <a href="#">가맹점 문의</a>
                <a href="#">고객센터</a>
            </div>
            <p class="copyright">&copy; 2024 Golden Crispy Chicken. All rights reserved.</p>
        </div>
    </footer>

</body>
</html>
