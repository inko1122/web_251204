<!DOCTYPE html>
<html lang="ko">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>맘스터치 - 빠르게보다 올바르게</title>
    <link href="https://fonts.googleapis.com/css2?family=Noto+Sans+KR:wght@300;500;700;900&display=swap" rel="stylesheet">
    <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.0.0/css/all.min.css">

    <style>
        /* [CSS 설정] */
        :root {
            /* 라이트 모드 변수 */
            --primary: #FFC300; /* 맘스터치 옐로우 */
            --secondary: #4A3B32; /* 딥 브라운 */
            --accent: #E53935; /* 포인트 레드 */
            --bg-color: #ffffff;
            --card-bg: #ffffff;
            --text-main: #333333;
            --text-sub: #666666;
            --shadow: rgba(0,0,0,0.1);
        }

        /* 다크 모드 변수 재정의 */
        body.dark-mode {
            --bg-color: #1a1a1a;
            --card-bg: #2d2d2d;
            --text-main: #f1f1f1;
            --text-sub: #cccccc;
            --shadow: rgba(255,255,255,0.05);
            --secondary: #FFC300; /* 다크모드에서는 로고색 반전 효과 */
        }

        * { margin: 0; padding: 0; box-sizing: border-box; font-family: 'Noto Sans KR', sans-serif; transition: background-color 0.3s, color 0.3s; }
        
        body { background-color: var(--bg-color); color: var(--text-main); }
        a { text-decoration: none; color: inherit; }
        ul { list-style: none; }

        /* 1. 헤더 & 유틸리티 바 */
        header {
            position: fixed;
            top: 0; width: 100%;
            background-color: var(--card-bg);
            box-shadow: 0 2px 10px var(--shadow);
            z-index: 1000;
        }

        .header-inner {
            max-width: 1200px;
            margin: 0 auto;
            height: 70px;
            display: flex;
            justify-content: space-between;
            align-items: center;
            padding: 0 20px;
        }

        .logo {
            font-size: 1.8rem;
            font-weight: 900;
            color: var(--secondary); /* 맘스터치 로고 색상 */
            letter-spacing: -1px;
        }
        
        .logo span { color: var(--accent); } /* TOUCH 부분 포인트 */

        .utils {
            display: flex;
            align-items: center;
            gap: 15px;
        }

        /* 컨트롤 버튼 스타일 */
        .btn-icon {
            background: none;
            border: 1px solid var(--text-sub);
            color: var(--text-main);
            padding: 5px 10px;
            border-radius: 20px;
            cursor: pointer;
            font-size: 0.9rem;
        }
        
        .btn-official {
            background-color: var(--primary);
            color: #000;
            border: none;
            font-weight: bold;
        }

        select.lang-select {
            padding: 5px;
            border-radius: 5px;
            background: var(--card-bg);
            color: var(--text-main);
            border: 1px solid var(--text-sub);
        }

        /* 2. 히어로 섹션 */
        .hero {
            margin-top: 70px;
            height: 500px;
            background: linear-gradient(rgba(0,0,0,0.4), rgba(0,0,0,0.4)), url('https://images.unsplash.com/photo-1568901346375-23c9450c58cd?q=80&w=1599&auto=format&fit=crop');
            background-size: cover;
            background-position: center;
            display: flex;
            flex-direction: column;
            justify-content: center;
            align-items: center;
            text-align: center;
            color: white;
        }

        .hero h1 { font-size: 3.5rem; text-shadow: 2px 2px 5px rgba(0,0,0,0.7); margin-bottom: 20px; }
        .hero p { font-size: 1.5rem; margin-bottom: 30px; font-weight: 300; }
        
        .btn-cta {
            padding: 15px 40px;
            background-color: var(--primary);
            color: #333;
            font-size: 1.2rem;
            font-weight: bold;
            border-radius: 50px;
            border: none;
            cursor: pointer;
            box-shadow: 0 4px 15px rgba(255, 195, 0, 0.4);
        }
        .btn-cta:hover { transform: scale(1.05); }

        /* 3. 메뉴 그리드 */
        .container { max-width: 1200px; margin: 0 auto; padding: 60px 20px; }
        
        .section-title {
            text-align: center;
            margin-bottom: 50px;
        }
        .section-title h2 { font-size: 2.5rem; margin-bottom: 10px; }
        .section-title span { color: var(--primary); font-weight: bold; }

        .menu-grid {
            display: grid;
            grid-template-columns: repeat(auto-fit, minmax(280px, 1fr));
            gap: 30px;
        }

        .card {
            background-color: var(--card-bg);
            border-radius: 15px;
            overflow: hidden;
            box-shadow: 0 5px 15px var(--shadow);
            position: relative;
        }

        .card:hover { transform: translateY(-10px); }

        /* 베스트 뱃지 */
        .badge {
            position: absolute;
            top: 15px; left: 15px;
            background-color: var(--accent);
            color: white;
            padding: 5px 10px;
            border-radius: 5px;
            font-size: 0.8rem;
            font-weight: bold;
        }

        .card img {
            width: 100%;
            height: 200px;
            object-fit: cover;
            background-color: #eee;
        }

        .card-body { padding: 20px; text-align: center; }
        .card-body h3 { font-size: 1.4rem; margin-bottom: 10px; }
        .card-body p { color: var(--text-sub); font-size: 0.9rem; margin-bottom: 15px; min-height: 40px;}
        .price { font-size: 1.2rem; font-weight: 900; color: var(--text-main); }

        /* 4. 모달 (주문 팝업) */
        .modal {
            display: none; /* 기본 숨김 */
            position: fixed; z-index: 2000;
            left: 0; top: 0; width: 100%; height: 100%;
            background-color: rgba(0,0,0,0.6);
            justify-content: center; align-items: center;
        }
        .modal-content {
            background-color: var(--card-bg);
            padding: 40px;
            border-radius: 10px;
            text-align: center;
            max-width: 400px;
            width: 90%;
            box-shadow: 0 5px 20px rgba(0,0,0,0.3);
        }
        .close-btn {
            margin-top: 20px;
            padding: 10px 20px;
            background-color: var(--text-sub);
            color: white;
            border: none;
            cursor: pointer;
            border-radius: 5px;
        }

        /* 푸터 */
        footer {
            background-color: #1a1a1a;
            color: #888;
            padding: 40px;
            text-align: center;
            font-size: 0.8rem;
        }

        @media(max-width: 768px) {
            .hero h1 { font-size: 2.2rem; }
            .header-inner { padding: 0 10px; }
            .logo { font-size: 1.4rem; }
            .utils { gap: 8px; }
            .btn-icon { font-size: 0.7rem; padding: 4px 8px; }
        }
    </style>
</head>
<body>

    <header>
        <div class="header-inner">
            <div class="logo">MOM'S <span>TOUCH</span></div>
            <div class="utils">
                <button class="btn-icon" onclick="toggleTheme()">
                    <i class="fas fa-moon"></i> <span data-i18n="mode">다크모드</span>
                </button>
                
                <select class="lang-select" onchange="changeLanguage(this.value)">
                    <option value="ko">한국어</option>
                    <option value="en">English</option>
                    <option value="jp">日本語</option>
                </select>

                <a href="https://www.momstouch.co.kr/" target="_blank" class="btn-icon btn-official">
                    <i class="fas fa-external-link-alt"></i> Official
                </a>
            </div>
        </div>
    </header>

    <section class="hero">
        <h1 data-i18n="heroTitle">압도적인 크기, 싸이버거</h1>
        <p data-i18n="heroSub">주문 즉시 조리하는 신선한 수제 버거의 기준</p>
        <button class="btn-cta" onclick="openModal()" data-i18n="orderBtn">주문하기</button>
    </section>

    <section class="container">
        <div class="section-title">
            <h2 data-i18n="menuTitle">맘스터치 대표 메뉴</h2>
            <p data-i18n="menuSub">가성비 그 이상의 감동을 만나보세요</p>
        </div>

        <div class="menu-grid">
            <div class="card" onclick="openModal()">
                <div class="badge">No.1 BEST</div>
                <img src="https://images.unsplash.com/photo-1619250907584-6992d4f208df?q=80&w=1505&auto=format&fit=crop" alt="싸이버거">
                <div class="card-body">
                    <h3 data-i18n="menu1_name">싸이버거</h3>
                    <p data-i18n="menu1_desc">매콤바삭한 통다리살 패티가 통째로! 맘스터치 시그니처.</p>
                    <div class="price">₩4,600</div>
                </div>
            </div>

            <div class="card" onclick="openModal()">
                <img src="https://images.unsplash.com/photo-1594212699903-ec8a3eca50f5?q=80&w=1471&auto=format&fit=crop" alt="인크레더블 버거">
                <div class="card-body">
                    <h3 data-i18n="menu2_name">인크레더블 버거</h3>
                    <p data-i18n="menu2_desc">프리미엄 더블햄, 계란프라이, 통다리살의 환상적인 조합.</p>
                    <div class="price">₩5,700</div>
                </div>
            </div>

            <div class="card" onclick="openModal()">
                <div class="badge">HOT</div>
                <img src="https://images.unsplash.com/photo-1630384060421-cb20d0e0649d?q=80&w=1450&auto=format&fit=crop" alt="케이준 감자">
                <div class="card-body">
                    <h3 data-i18n="menu3_name">케이준 양념감자</h3>
                    <p data-i18n="menu3_desc">한 번 맛보면 멈출 수 없는 맘스터치만의 바삭한 감자튀김.</p>
                    <div class="price">₩2,000</div>
                </div>
            </div>

            <div class="card" onclick="openModal()">
                <img src="https://images.unsplash.com/photo-1626082927389-6cd097cdc6ec?q=80&w=1470&auto=format&fit=crop" alt="치킨">
                <div class="card-body">
                    <h3 data-i18n="menu4_name">후라이드 치킨</h3>
                    <p data-i18n="menu4_desc">겉바속촉의 정석. 클래식한 맘스터치 치킨.</p>
                    <div class="price">₩16,900</div>
                </div>
            </div>
        </div>
    </section>

    <div id="orderModal" class="modal">
        <div class="modal-content">
            <h2 data-i18n="modalTitle">주문 준비 중</h2>
            <br>
            <p data-i18n="modalDesc">현재 데모 페이지에서는 실제 결제가 불가능합니다.<br>공식 홈페이지를 이용해 주세요!</p>
            <button class="close-btn" onclick="closeModal()" data-i18n="closeBtn">닫기</button>
        </div>
    </div>

    <footer>
        <p>&copy; 2025 MOM'S TOUCH Clone Coding. All rights reserved.</p>
        <p>This is a fan-made example page.</p>
    </footer>

    <script>
        // 1. 언어 데이터셋 (Korean, English, Japanese)
        const translations = {
            ko: {
                mode: "다크모드",
                heroTitle: "압도적인 크기, 싸이버거",
                heroSub: "주문 즉시 조리하는 신선한 수제 버거의 기준",
                orderBtn: "주문하기",
                menuTitle: "맘스터치 대표 메뉴",
                menuSub: "가성비 그 이상의 감동을 만나보세요",
                menu1_name: "싸이버거",
                menu1_desc: "매콤바삭한 통다리살 패티가 통째로! 맘스터치 시그니처.",
                menu2_name: "인크레더블 버거",
                menu2_desc: "프리미엄 더블햄, 계란프라이, 통다리살의 환상적인 조합.",
                menu3_name: "케이준 양념감자",
                menu3_desc: "한 번 맛보면 멈출 수 없는 맘스터치만의 바삭한 감자튀김.",
                menu4_name: "후라이드 치킨",
                menu4_desc: "겉바속촉의 정석. 클래식한 맘스터치 치킨.",
                modalTitle: "주문 준비 중",
                modalDesc: "현재 데모 페이지에서는 실제 결제가 불가능합니다.<br>공식 홈페이지를 이용해 주세요!",
                closeBtn: "닫기"
            },
            en: {
                mode: "Dark Mode",
                heroTitle: "Overwhelming Size, Thigh Burger",
                heroSub: "Standard of fresh handmade burgers cooked to order.",
                orderBtn: "Order Now",
                menuTitle: "Signature Menu",
                menuSub: "Experience the value beyond price.",
                menu1_name: "Thigh Burger",
                menu1_desc: "Spicy & crispy whole chicken thigh patty! Signature menu.",
                menu2_name: "Incredible Burger",
                menu2_desc: "Fantastic combo of ham, fried egg, and chicken thigh.",
                menu3_name: "Cajun Fries",
                menu3_desc: "Crispy fries with special seasoning you can't stop eating.",
                menu4_name: "Fried Chicken",
                menu4_desc: "Classic crispy chicken. The standard of taste.",
                modalTitle: "Preparing Order",
                modalDesc: "Payment is not available on this demo page.<br>Please use the official website!",
                closeBtn: "Close"
            },
            jp: {
                mode: "ダークモード",
                heroTitle: "圧倒的な大きさ、サイバーガー",
                heroSub: "注文後すぐに調理する新鮮な手作りバーガーの基準。",
                orderBtn: "注文する",
                menuTitle: "代表メニュー",
                menuSub: "コスパ以上の感動に出会ってください。",
                menu1_name: "サイバーガー",
                menu1_desc: "辛くてサクサクの鶏もも肉パティが丸ごと！代表メニュー。",
                menu2_name: "インクレディブルバーガー",
                menu2_desc: "プレミアムハム、目玉焼き、鶏もも肉の幻想的な調和。",
                menu3_name: "ケイジャンポテト",
                menu3_desc: "一度食べたら止まらないマムズタッチだけの味付けポテト。",
                menu4_name: "フライドチキン",
                menu4_desc: "外はサクサク、中はジューシー。クラシックなチキン。",
                modalTitle: "注文準備中",
                modalDesc: "このデモページでは実際の決済はできません。<br>公式ホームページをご利用ください！",
                closeBtn: "閉じる"
            }
        };

        // 2. 다크모드 토글 기능
        function toggleTheme() {
            document.body.classList.toggle('dark-mode');
            const icon = document.querySelector('.btn-icon i');
            // 아이콘 변경 (달 <-> 해) 로직은 생략하거나 추가 가능
        }

        // 3. 언어 변경 기능
        function changeLanguage(lang) {
            const elements = document.querySelectorAll('[data-i18n]');
            elements.forEach(element => {
                const key = element.getAttribute('data-i18n');
                if (translations[lang][key]) {
                    element.innerHTML = translations[lang][key];
                }
            });
        }

        // 4. 모달 기능
        function openModal() {
            document.getElementById('orderModal').style.display = 'flex';
        }
        function closeModal() {
            document.getElementById('orderModal').style.display = 'none';
        }

        // 모달 바깥 클릭 시 닫기
        window.onclick = function(event) {
            const modal = document.getElementById('orderModal');
            if (event.target == modal) {
                modal.style.display = "none";
            }
        }
    </script>
</body>
</html>
