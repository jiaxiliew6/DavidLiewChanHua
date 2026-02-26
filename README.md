<!DOCTYPE html>
<html lang="zh-CN">
<head>
    <meta charset="UTF-8">
    <meta http-equiv="Content-Security-Policy" content="default-src 'self'; script-src 'self' 'unsafe-inline' https://cdn.tailwindcss.com; style-src 'self' 'unsafe-inline' https://fonts.googleapis.com; img-src 'self' data:; font-src 'self' https://fonts.gstatic.com;">
    <meta http-equiv="X-Content-Type-Options" content="nosniff">
    <meta http-equiv="X-Frame-Options" content="DENY">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>刘振华 David Liew Chan Hua<</title>
    <script src="https://cdn.tailwindcss.com"></script>
    <style>
        /* Typography */
        @font-face { font-family: 'Avenir'; src: local('Avenir'), sans-serif; }
        body { background-color: #F9F6EE; color: #333; font-family: 'Adobe Heiti Std', sans-serif; margin: 0; }
        
        .chinese-font { font-family: 'HYXingZhiTi', cursive; font-weight: normal; }
	.chinese-font-serif { font-family: 'YouYuan', serif; font-weight: normal; }
        .english-font { font-family: 'Avenir', sans-serif; font-weight: normal; }
        
        /* Theme Colors */
        .bg-primary { background-color: #26681f; }
        .text-white-custom { color: #F9F6EE; }

        /* Animation & Stop Motion */
        .fade-in { animation: fadeIn 1.8s ease-out forwards; }
        @keyframes fadeIn { from { opacity: 0; transform: translateY(30px); } to { opacity: 1; transform: translateY(0); } }
        .stop-motion-hover 
        {1.0s cubic-bezier(0.165, 0.84, 0.44, 1), box-shadow 1.0s ease;}
        .stop-motion-hover:hover { 
	    transform: translateY(-8px) scale(1.02); /* Lifts upward slightly */ 
	}
        
	.stop-motion-hover:hover img {
    	    box-shadow: 0 20px 40px rgba(0,0,0,0.15); /* Softens and deepens shadow */
	}

	@keyframes stopMotion {
            0% { transform: rotate(0.5deg) scale(1.01); }
            50% { transform: rotate(-0.5deg) scale(1.01); }
        }

	/* Container for swipe effect */
	#page-container {
    	    display: flex;
    	    transition: transform 0.6s cubic-bezier(0.23, 1, 0.32, 1); /* Fluid motion */
            width: 300%; /* 3 pages */
        }

	.page-content {
    	    width: 33.333%;
    	    flex-shrink: 0;
    	    opacity: 0;
    	    transition: opacity 0.4s steps(4); /* Stop-motion feel */
	}

	.page-content.active {
    	    opacity: 1;
	}

	main { overflow: hidden; } /* Prevent horizontal scrollbar */	

        /* Masonry Grid */
        .art-grid {         
    	    column-count: 1; /* Default for mobile */
            column-gap: 1.5rem;
            width: 90%;
            margin: 0 auto;
        }

        @media (min-width: 768px) {
            .art-grid { 
                column-count: 2; /* Tablets */
            }
        }

        @media (min-width: 1024px) {
            .art-grid { 
                column-count: 3; /* PC Screens */
                width: 95%;
                max-width: 1600px;
            }
        }
        
        .art-card { 
            display: inline-block; 
            width: 100%; 
            break-inside: avoid; 
	    transition: opacity 0.4s ease, transform 0.4s ease;
            margin-bottom: 3rem; 
            position: relative; 
            cursor: pointer;
            text-align: center;
	    /* Keep existing styles, just ensure display is managed correctly */
    	    transition: opacity 0.3s ease;
        }
	
	/* When hidden by filter */
	.art-card.hidden-art {
    	    display: none;
    	    opacity: 0;
    	    transform: scale(0.95);
	}

        /* Protection Shield */
        .art-card::after {
            content: "";
            position: absolute;
            top: 0; left: 0; width: 100%; height: 100%;
            z-index: 10;
	    pointer-events: none; /* Add this to let clicks pass through to the card */
        }

        /* Image Height Constraint for PC Screen */
        .art-card img { 
            width: auto; 
            max-width: 100%;
            max-height: 75vh; /* Fitting the PC screen (75% of view height) */
            margin: 0 auto;
            display: block;
            border-radius: 2px;
            box-shadow: 0 10px 20px rgba(0,0,0,0.08);
        }

	#toTopBtn { 
    	    width: 50px; 
    	    height: 50px; 
    	    display: flex; 
    	    align-items: center; 
    	    justify-content: center; 
    	    font-size: 24px;
    	    cursor: pointer;
	    opacity: 0; /* Make sure it starts at 0 */
    	    pointer-events: none; /* This ensures it doesn't block clicks when hidden */
	}

	#toTopBtn.show { 
            opacity: 1; 
            pointer-events: auto; 
	}

        /* Fullscreen Viewer */
        #viewer { display: none; position: fixed; inset: 0; background: rgba(0,0,0,0.98); z-index: 100; overflow: hidden; }
        #viewer img { max-height: 85vh; transition: transform 0.2s ease, margin 0.3s ease; /* Smooth glide back */cursor: grab; user-select: none; display: block; }
	/* 让容器高度根据当前激活的页面自动调节 */
	#page-container {
    	    align-items: flex-start; /* 确保子项不强制等高 */
    	    width: 300%; 
	}

	.page-content {
    	    height: 0;
    	    overflow: hidden;
    	    padding-bottom: 0;
    	    padding-top: 0;
    	    transition: opacity 0.4s steps(4);
	}

	/* 只有激活状态的 section 才占用空间和高度 */
	.page-content.active {
    	    height: auto;
    	    overflow: visible;
	}

	/* 针对移动端优化，确保内容不会溢出 */
	section {
    	    max-width: 100vw;
	}
    </style>
</head>
<body>

    <header class="bg-primary text-white-custom p-4 md:p-8 text-center fade-in">
    <div class="flex flex-col md:flex-row items-center justify-center gap-4 md:gap-12">
        <h1 class="chinese-font text-10xl md:text-7xl" style="font-weight: normal; line-height: 1.2; letter-spacing: 20px; md:letter-spacing: 10px;">刘振华</h1>
        
        <div class="w-24 h-px md:w-px md:h-24 bg-white/30"></div>

        <h1 class="english-font text-2xl md:text-5xl" style="font-weight: 100; letter-spacing: 4px; md:letter-spacing: 10px;">David Liew Chan Hua</h1>
    </div>

    <div style="margin-top: 60px"></div>

    <p class="chinese-font-serif text-lg md:text-3xl opacity-1.0;" style="letter-spacing: 14px; md:letter-spacing: 10px;">婆罗洲热带风情 • 乡土的笔墨情怀</p>
</header>

    <nav class="flex justify-center space-x-4 md:space-x-12 p-4 md:p-8 text-lg md:text-xl bg-#F9F6EE border-transparent top-0 z-50 english-font tracking-widest">
        <button onclick="showPage('artwork')" class="hover:text-green-800">
	    <span class="chinese-font-serif text-sm md:text-2xl">作品集</span>
            <span class="english-font text-[20px] md:text-x1">Artwork</span>
	</button>
        <button onclick="showPage('biodata')" class="hover:text-green-800">
	    <span class="chinese-font-serif text-sm md:text-2xl">画家简介</span>
            <span class="english-font text-[20px] md:text-x1">Biodata</span>
	</button>
        <button onclick="showPage('contact')" class="hover:text-green-800">
	    <span class="chinese-font-serif text-sm md:text-2xl">联系方式</span>
            <span class="english-font text-[20px] md:text-x1">Contact Me</span>
	</button>
    </nav>

    <main class="container mx-auto px-6 md:px-20 py-10">
        
        <div id="page-container"> <section id="artwork" class="page-content active">
            <div class="art-grid" id="mainGallery">
	    <div class="flex flex-wrap justify-center grid-cols-4 gap-4 mb-10 english-font">
    		<button onclick="filterArt('all')" class="px-4 py-2 bg-primary text-white rounded">全部 All</button>
		<div class="flex justify-center mb-8">
    		    <div class="relative w-full max-w-md">
        		<div class="absolute inset-y-0 left-0 pl-3 flex items-center pointer-events-none">
            		    <svg class="h-5 w-5 text-green-800" xmlns="http://www.w3.org/2000/svg" fill="none" viewBox="0 0 24 24" stroke="currentColor">
                		<path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M21 21l-6-6m2-5a7 7 0 11-14 0 7 7 0 0114 0z" />
            		    </svg>
        		</div>
        		<input type="text" id="artSearch" onkeyup="searchArt()" 
            		    placeholder="搜索作品名称或年份..." 
            		    class="w-full pl-10 pr-4 py-2 border-2 border-green-800 rounded-lg focus:outline-none focus:ring-2 focus:ring-green-500 bg-white/50"
        		>
    		    </div>
		</div>
    		<button onclick="filterArt('热带水果系列')" class="px-4 py-2 border border-green-800 hover:bg-green-100 rounded">热带水果系列</button>
    		<button onclick="filterArt('热带花鸟系列')" class="px-4 py-2 border border-green-800 hover:bg-green-100 rounded">热带花鸟系列</button>
		<button onclick="filterArt('南洋风景系列')" class="px-4 py-2 border border-green-800 hover:bg-green-100 rounded">南洋风景系列</button>
    		<button onclick="filterArt('红毛猩猩系列')" class="px-4 py-2 border border-green-800 hover:bg-green-100 rounded">红毛猩猩系列</button>
		<button onclick="filterArt('其他传统题材系列')" class="px-4 py-2 border border-green-800 hover:bg-green-100 rounded">其他传统题材系列</button>
	    </div>
		<div class="art-card stop-motion-hover" data-category="热带水果系列" onclick="openViewer(this)">
                    <img src="images/painting/作者 刘振华Liew Chan Hua 标题 丰收 尺寸 138 cm x 68 cm.jpg" alt="丰收" loading="lazy" class="">
                    <p class="mt-3 text-sm italic desc-text" contenteditable="false">丰收 | 138 cm x 68 cm | 2025</p>
                </div>
                <div class="art-card stop-motion-hover" data-category="热带花鸟系列" onclick="openViewer(this)">
                    <img src="images/painting/姓名 刘振华Liew Chan Hua 标题 花蝶共舞 媒介 水墨画 尺寸 139 cm x 68 cm.jpg" alt="花蝶共舞" loading="lazy" class="">
                    <p class="mt-3 text-sm italic desc-text" contenteditable="false">花蝶共舞 | 139 cm x 68 cm | 2025</p>
                </div>
                <div class="art-card stop-motion-hover" data-category="热带水果系列" onclick="openViewer(this)">
                    <img src="images/painting/作者 刘振华Liew Chan Hua 标题 果王果后 媒介 水墨画 尺寸 138 cm x 68 cm.jpg" alt="果王果后" loading="lazy" class="">
                    <p class="mt-3 text-sm italic desc-text" contenteditable="false">果王果后 | 138 cm x 68 cm | 2025</p>
                </div>
                <div class="art-card stop-motion-hover" data-category="热带水果系列" onclick="openViewer(this)">
                    <img src="images/painting/作者 刘振华 标题 满园旺来 尺寸 138 cm x 68 cm.jpg" alt="满园旺来" loading="lazy" class="">
                    <p class="mt-3 text-sm italic desc-text" contenteditable="false">满园旺来 | 138 cm x 68 cm | 2025</p>
                </div>
                <div class="art-card stop-motion-hover" data-category="热带花鸟系列" onclick="openViewer(this)">
                    <img src="images/painting/作者 刘振华Liew Chan Hua 标题 丰收时节 媒介 水墨画 尺寸 138 cm x 68 cm.jpg" alt="丰收时节" loading="lazy" class="">
                    <p class="mt-3 text-sm italic desc-text" contenteditable="false">丰收时节 | 138 cm x 68 cm | 2025</p>
                </div>
                <div class="art-card stop-motion-hover" data-category="红毛猩猩系列" onclick="openViewer(this)">
                    <img src="images/painting/姓名 刘振华Liew Chan Hua 标题 戏猿 媒介 水墨画 尺寸 139 cm x 68 cm.jpg" alt="戏猿" loading="lazy" class="">
                    <p class="mt-3 text-sm italic desc-text" contenteditable="false">戏猿 | 139 cm x 68 cm | 2025</p>
                </div>
                <div class="art-card stop-motion-hover" data-category="热带花鸟系列" onclick="openViewer(this)">
                    <img src="images/painting/姓名 刘振华Liew Chan Hua 标题 王花迎喜 媒介 水墨画 尺寸 139 cm x 68 cm.jpg" alt="王花迎喜" loading="lazy" class="">
                    <p class="mt-3 text-sm italic desc-text" contenteditable="false">王花迎喜 | 139 cm x 68 cm | 2025</p>
                </div>
                <div class="art-card stop-motion-hover" data-category="热带水果系列" onclick="openViewer(this)">
                    <img src="images/painting/姓名 刘振华Liew Chan Hua 标题 硕果累累 媒介 水墨画 尺寸 139 cm x 68 cm.jpg" alt="硕果累累" loading="lazy" class="">
                    <p class="mt-3 text-sm italic desc-text" contenteditable="false">硕果累累 | 139 cm x 68 cm | 2025</p>
                </div>
                <div class="art-card stop-motion-hover" data-category="南洋风景系列" onclick="openViewer(this)">
                    <img src="images/painting/作者 刘振华 Liew Chan Hua 标题 南洋风光 媒介 水墨画 尺寸 138 cm x 68 cm.jpg" alt="南洋风光" loading="lazy" class="">
                    <p class="mt-3 text-sm italic desc-text" contenteditable="false">南洋风光 | 138 cm x 68 cm | 2025</p>
                </div>
		<div class="art-card stop-motion-hover" data-category="红毛猩猩系列" onclick="openViewer(this)">
                    <img src="images/painting/戏耍 尺寸：138 cm x 69 cm 媒介：水墨画.jpeg" alt="戏耍" loading="lazy" class="">
                    <p class="mt-3 text-sm italic desc-text" contenteditable="false">戏耍 | 138 cm x 69 cm | 2024</p>
                </div>
		<div class="art-card stop-motion-hover" data-category="南洋风景系列" onclick="openViewer(this)">
                    <img src="images/painting/作者：刘振华 Liew Chan Hua 标题：特拉加艾也  尺寸：70 cm x 46 cm.jpeg" alt="特拉加艾也" loading="lazy" class="">
                    <p class="mt-3 text-sm italic desc-text" contenteditable="false">特拉加艾也 | 70 cm x 46 cm | 2023</p>
                </div>
		<div class="art-card stop-motion-hover" data-category="其他传统题材系列" onclick="openViewer(this)">
                    <img src="images/painting/作者：刘振华Liew Chan Hua 题目：柳下鳞影The Carps 尺寸：70 cm x 46 cm 年份： 2022 年作 Price RM 3000.00.jpeg" alt="柳下鳞影" loading="lazy" 			class="">
                    <p class="mt-3 text-sm italic desc-text" contenteditable="false">柳下鳞影 | 70 cm x 46 cm | 2022</p>
                </div>
		<div class="art-card stop-motion-hover" data-category="红毛猩猩系列" onclick="openViewer(this)">
                    <img src="images/painting/作者：刘振华题目：丰收  尺寸：138 cm x 69 cm.jpg.jpeg" alt="丰收" loading="lazy" class="">
                    <p class="mt-3 text-sm italic desc-text" contenteditable="false">丰收 | 136 cm x 69 cm | 2022</p>
                </div>
		<div class="art-card stop-motion-hover" data-category="热带水果系列" onclick="openViewer(this)">
                    <img src="images/painting/作者：刘振华题目：飘香时节                尺寸：138 cm x 69 cm.jpg.jpeg" alt="飘香时节" loading="lazy" class="">
                    <p class="mt-3 text-sm italic desc-text" contenteditable="false">飘香时节 | 138 cm x 69 cm | 2022</p>
                </div>
		<div class="art-card stop-motion-hover" data-category="其他传统题材系列" onclick="openViewer(this)">
                    <img src="images/painting/刘振华作品 ； 清泉鳞影 [ 70 cm x 68 cm ] 2022年作 Liew Chan Hua ; The Carps RM 5,000.00.jpg.jpeg" alt="清泉鳞影" loading="lazy" class="">
		    <p class="mt-3 text-sm italic desc-text" contenteditable="false">清泉鳞影 | 70 cm x 68 cm | 2022</p>
		</div>
		<div class="art-card stop-motion-hover" data-category="热带花鸟系列" onclick="openViewer(this)">
                    <img src="images/painting/刘振华作品 ； 忆童年 [ 70 cm x 45 cm ] 2019年作 Liew Chan Hua ; Childhood - RM 3,000.00.jpg.jpeg" alt="忆童年" loading="lazy" class="">
                    <p class="mt-3 text-sm italic desc-text" contenteditable="false">忆童年 | 70 cm x 45 cm | 2019</p>
                </div>
		<div class="art-card stop-motion-hover" data-category="其他传统题材系列" onclick="openViewer(this)">
                    <img src="images/painting/刘振华作品 ； 一啸震山河 [ 123 cm x 63 cm ]2009年作 Liew Chan Hua ； The Tiger - RM 8,000.00.jpg.jpeg" alt="一啸震山河" loading="lazy" class="">
		<p class="mt-3 text-sm italic desc-text" contenteditable="false">一啸震山河 | 123 cm x 65 cm | 2009</p>
		</div>
		<div class="art-card stop-motion-hover" data-category="其他传统题材系列" onclick="openViewer(this)">
                    <img src="images/painting/刘振华作品 ； 戏虾 [ 69 cm x 46 cm ] 2018年作 Liew Chan Hua ; The Prawns - Not For Sale.jpg.jpeg" alt="戏虾" loading="lazy" class="">
		    <p class="mt-3 text-sm italic desc-text" contenteditable="false">戏虾 | 69 cm x 46 cm | 2018</p>
		</div>
		<div class="art-card stop-motion-hover" data-category="其他传统题材系列" onclick="openViewer(this)">
                    <img src="images/painting/刘振华作品 ； 山珍图 [ 69 cm x 45 cm ] 2016年作 Liew Chan Hua ; The Healthy Foods - RM 3,000.00.jpg.jpeg" alt="山珍图" loading="lazy" class="">
		    <p class="mt-3 text-sm italic desc-text" contenteditable="false">山珍图 | 69 cm x 45 cm | 2016</p>
		</div>
		<div class="art-card stop-motion-hover" data-category="其他传统题材系列" onclick="openViewer(this)">
                    <img src="images/painting/刘振华作品 ； 飘香  [ 70 cm x 45 cm ] 2018年作 Liew Chan Hua ;  Scrumptious Food - Not For Sale.jpg.jpeg" alt="飘香" loading="lazy" class="">
		    <p class="mt-3 text-sm italic desc-text" contenteditable="false">飘香 | 70 cm x 45 cm | 2018</p>
		</div>
		<div class="art-card stop-motion-hover" data-category="其他传统题材系列" onclick="openViewer(this)">
                    <img src="images/painting/刘振华作品 ； 万里雄风 [ 137 cm x 70 cm ] 2014年作 Liew Chan Hua ; The Running Horses RM 10,000.00.jpg.jpeg" alt="万里雄风" loading="lazy"  			    class="">
		    <p class="mt-3 text-sm italic desc-text" contenteditable="false">万里雄风 | 137 cm x 70 cm | 2014</p>
		</div>
		<div class="art-card stop-motion-hover" data-category="南洋风景系列" onclick="openViewer(this)">
                    <img src="images/painting/刘振华作品 ； 姆鲁山国家公园石林云海图 [ 144 cm x 76 cm ] 2022 年作 Liew Chan Hua ; The Pinnacles of Mulu National Park - RM 16,000.00.jpg.jpeg" 		    alt="姆鲁山国家公园石林云海图" loading="lazy" class="">
                    <p class="mt-3 text-sm italic desc-text" contenteditable="false">姆鲁山国家公园石林云海图 | 144 cm x 76 cm | 2022</p>
		</div>
		<div class="art-card stop-motion-hover" data-category="热带花鸟系列" onclick="openViewer(this)">
                    <img src="images/painting/刘振华作品 ； 相依 [ 70 cm x 69 cm ] 2018年作Liew Chan Hua ;The Couple - RM 5,000.00.jpg.jpeg" alt="相依" loading="lazy" class="">
                    <p class="mt-3 text-sm italic desc-text" contenteditable="false">相依 | 70 cm x 69 cm | 2018</p>
                </div>
		<div class="art-card stop-motion-hover" data-category="热带花鸟系列" onclick="openViewer(this)">
                    <img src="images/painting/刘振华作品 ； 教子图 [ 69 cm x 68 cm ] 2019 年作 Liew Chan Hua ; Teaching - RM 5,000.00.jpg.jpeg" alt="教子图" loading="lazy" class="">
                    <p class="mt-3 text-sm italic desc-text" contenteditable="false">教子图 | 69 cm x 68 cm | 2019</p>
                </div>
		<div class="art-card stop-motion-hover" data-category="热带花鸟系列" onclick="openViewer(this)">
                    <img src="images/painting/刘振华作品 ； 田园相聚 [ 70 cm x 69 cm ] 2022年作Liew Chan Hua ; Gathering - RM 5,000.00.jpg.jpeg" alt="田园相聚" loading="lazy" class="">
                    <p class="mt-3 text-sm italic desc-text" contenteditable="false">田园相聚 | 70 cm x 69 cm | 2019</p>
                </div>
		<div class="art-card stop-motion-hover" data-category="其他传统题材系列" onclick="openViewer(this)">
                    <img src="images/painting/刘振华作品 ； 秋意 [ 70 cm x 45 cm ] 2019年作Liew Chan Hua ; The bottle gourds with the praying mantis - RM 3,000.00.jpg.jpeg" alt="秋意" 			    loading="lazy" class="">
		    <p class="mt-3 text-sm italic desc-text" contenteditable="false">秋意 | 70 cm x 45 cm | 2019</p>
		</div>
		<div class="art-card stop-motion-hover" data-category="其他传统题材系列" onclick="openViewer(this)">
                    <img src="images/painting/刘振华作品 ； 荷趣 [ 69 cm x 63 cm  2018 年作] Liew Chan Hua ; Lotus With Dragonflies - RM 5,000.00.jpg.jpeg" alt="荷趣" 			    		    loading="lazy" class="">
		    <p class="mt-3 text-sm italic desc-text" contenteditable="false">荷趣 | 69 cm x 63 cm | 2018</p>
		</div>
		<div class="art-card stop-motion-hover" data-category="热带水果系列" onclick="openViewer(this)">
                    <img src="images/painting/刘振华作品 ；南洋佳果 [ 137 cm x 35 cm ] 2018 年作 Liew Chan Hua ; The Nanyang Fruits - RM 5,000.00.jpg.jpeg" alt="南洋佳果" loading="lazy" 			    class="">
                    <p class="mt-3 text-sm italic desc-text" contenteditable="false">南洋佳果 | 137 cm x 35 cm | 2018</p>
                </div>
		<div class="art-card stop-motion-hover" data-category="红毛猩猩系列" onclick="openViewer(this)">
                    <img src="images/painting/刘振华作品：溪边的相约 [ 138 cm x 69 cm ]2019年作.jpg.jpeg" alt="溪边的相约" loading="lazy" class="">
                    <p class="mt-3 text-sm italic desc-text" contenteditable="false">溪边的相约 | 136 cm x 69 cm | 2019</p>
                </div>
		<div class="art-card stop-motion-hover" data-category="热带花鸟系列" onclick="openViewer(this)">
                    <img src="images/painting/刘振华作品： [ 138 cm x 69 cm ]2019年作.jpg.jpeg" alt="无标题" loading="lazy" class="">
                    <p class="mt-3 text-sm italic desc-text" contenteditable="false">无标题 | 138 cm x 69 cm | 2019</p>
                </div>
		<div class="art-card stop-motion-hover" data-category="热带花鸟系列" onclick="openViewer(this)">
                    <img src="images/painting/刘振华作品：觅食 [ 138 cm x 69 cm ] 2019年作.jpg.jpeg" alt="觅食" loading="lazy" class="">
                    <p class="mt-3 text-sm italic desc-text" contenteditable="false">觅食 | 138 cm x 69 cm | 2019</p>
                </div>
		<div class="art-card stop-motion-hover" data-category="热带花鸟系列" onclick="openViewer(this)">
                    <img src="images/painting/刘振华作品 [自得其乐：169 cm x 69 cm] 2019年作.jpg.jpeg" alt="自得其乐" loading="lazy" class="">
                    <p class="mt-3 text-sm italic desc-text" contenteditable="false">自得其乐 | 169 cm x 69 cm | 2019</p>
                </div>
		<div class="art-card stop-motion-hover" data-category="南洋风景系列" onclick="openViewer(this)">
                    <img src="images/painting/作者：刘振华 标题：林中奇景 尺寸：181 cm x 97 cm  媒介：水墨画.jpg.jpeg" alt="林中奇景" loading="lazy" class="">
                    <p class="mt-3 text-sm italic desc-text" contenteditable="false">林中奇景 | 181 cm x 97 cm | 2019</p>
                </div>
		<div class="art-card stop-motion-hover" data-category="热带花鸟系列" onclick="openViewer(this)">
                    <img src="images/painting/作者：刘振华Liew Chan Hua 标题：园中乐 尺寸：181 cm x 97 cm  媒介：水墨画.jpg.jpeg" alt="园中乐" loading="lazy" class="">
                    <p class="mt-3 text-sm italic desc-text" contenteditable="false">园中乐 | 181 cm x 97 cm | 2019</p>
                </div>
		<div class="art-card stop-motion-hover" data-category="红毛猩猩系列" onclick="openViewer(this)">
                    <img src="images/painting/刘振华作品  [ 归来：138 cm x 69 cm ]2019年作.jpg.jpeg" alt="归来" loading="lazy" class="">
                    <p class="mt-3 text-sm italic desc-text" contenteditable="false">归来 | 136 cm x 69 cm | 2019</p>
                </div>
		<div class="art-card stop-motion-hover" data-category="其他传统题材系列" onclick="openViewer(this)">
                    <img src="images/painting/刘振华作品 ： 秋艳 （ 139 cm x 69 cm ）2019年作jpg.jpg.jpeg" alt="秋艳" loading="lazy" class="">
		    <p class="mt-3 text-sm italic desc-text" contenteditable="false">秋艳 | 139 cm x 69 cm | 2019</p>
		</div>
		<div class="art-card stop-motion-hover" data-category="南洋风景系列" onclick="openViewer(this)">
                    <img src="images/painting/作者：刘振华Liew Chan Hua 题目：神山远景                 尺寸：247 cm x 123 cm.jpg.jpeg" alt="神山远景" loading="lazy" class="">
                    <p class="mt-3 text-sm italic desc-text" contenteditable="false">神山远景 | 247 cm x 123 cm | 2018</p>
                </div>
		<div class="art-card stop-motion-hover" data-category="热带水果系列" onclick="openViewer(this)">
                    <img src="images/painting/作者：刘振华Liew Chan Hua 标题：果档一景 尺寸：139 cm  x  69 cm  媒介：水墨画.jpg.jpeg" alt="果档一景" loading="lazy" class="">
                    <p class="mt-3 text-sm italic desc-text" contenteditable="false">果档一景 | 139 cm  x  69 cm | 2018</p>
                </div>
		<div class="art-card stop-motion-hover" data-category="热带水果系列" onclick="openViewer(this)">
                    <img src="images/painting/作者：刘振华Liew Chan Hua 标题：果王果后 尺寸：139 cm  x  69 cm 媒介：水墨画.jpg.jpeg" alt="果王果后" loading="lazy" class="">
                    <p class="mt-3 text-sm italic desc-text" contenteditable="false">果王果后 | 139 cm  x  69 cm | 2018</p>
                </div>
		<div class="art-card stop-motion-hover" data-category="热带水果系列" onclick="openViewer(this)">
                    <img src="images/painting/刘振华作品  [ 飘香：139 cm  x  69 cm ]2018年作.jpg.jpeg" alt="飘香" loading="lazy" class="">
                    <p class="mt-3 text-sm italic desc-text" contenteditable="false">飘香 | 139 cm  x  69 cm | 2018</p>
                </div>
		<div class="art-card stop-motion-hover" data-category="热带花鸟系列" onclick="openViewer(this)">
                    <img src="images/painting/刘振华作品 ：满园佳色 [ 181 cm x 97 cm 】2018年作.jpg.jpeg" alt="满园佳色" loading="lazy" class="">
                    <p class="mt-3 text-sm italic desc-text" contenteditable="false">满园佳色 | 181 cm x 97 cm | 2018</p>
                </div>
		<div class="art-card stop-motion-hover" data-category="热带水果系列" onclick="openViewer(this)">
                    <img src="images/painting/刘振华作品  [ 丰收：139 cm  x  69 cm ] 2018年作.jpg.jpeg" alt="丰收" loading="lazy" class="">
                    <p class="mt-3 text-sm italic desc-text" contenteditable="false">丰收 | 139 cm  x  69 cm | 2018</p>
                </div>
		<div class="art-card stop-motion-hover" data-category="热带水果系列" onclick="openViewer(this)">
                    <img src="images/painting/刘振华作品  [ 果后山竹：138 cm x 69 cm ]-2018年作.jpg.jpeg" alt="果后山竹" loading="lazy" class="">
                    <p class="mt-3 text-sm italic desc-text" contenteditable="false">果后山竹 | 138 cm  x  69 cm | 2018</p>
                </div>
		<div class="art-card stop-motion-hover" data-category="热带水果系列" onclick="openViewer(this)">
                    <img src="images/painting/刘振华作品  [ 南洋佳果-红毛丹：69 cm x 68 cm ]-2017年作.jpg.jpeg" alt="红毛丹" loading="lazy" class="">
                    <p class="mt-3 text-sm italic desc-text" contenteditable="false">红毛丹 | 69 cm x 68 cm | 2017</p>
                </div>
		<div class="art-card stop-motion-hover" data-category="热带水果系列" onclick="openViewer(this)">
                    <img src="images/painting/刘振华作品  [ 硕果累累：138 cm x 70 cm ]-2018年作.jpg.jpeg" alt="硕果累累" loading="lazy" class="">
                    <p class="mt-3 text-sm italic desc-text" contenteditable="false">硕果累累 | 138 cm x 70 cm | 2018</p>
                </div>
		<div class="art-card stop-motion-hover" data-category="其他传统题材系列" onclick="openViewer(this)">
                    <img src="images/painting/刘振华作品  [ 蝴绕花枝恋暖香：138 cm x 69 cm ]-2017年作.jpg.jpeg" alt="蝴绕花枝恋暖香" loading="lazy" class="">
		    <p class="mt-3 text-sm italic desc-text" contenteditable="false">蝴绕花枝恋暖香 | 138 cm x 69 cm | 2017</p>
		</div>
		<div class="art-card stop-motion-hover" data-category="热带花鸟系列" onclick="openViewer(this)">
                    <img src="images/painting/刘振华作品  [ 阴下香兰：138 cm x 69 cm ] 2017年作.jpg.jpeg" alt="阴下香兰" loading="lazy" class="">
                    <p class="mt-3 text-sm italic desc-text" contenteditable="false">阴下香兰 | 138 cm x 69 cm | 2017</p>
                </div>
		<div class="art-card stop-motion-hover" data-category="红毛猩猩系列" onclick="openViewer(this)">
                    <img src="images/painting/刘振华作品：戏乐 [ 138 cm x 69 cm ]-2017年作.jpg.jpeg" alt="戏乐" loading="lazy" class="">
                    <p class="mt-3 text-sm italic desc-text" contenteditable="false">戏乐 | 138 cm x 69 cm | 2017</p>
                </div>
		<div class="art-card stop-motion-hover" data-category="热带花鸟系列" onclick="openViewer(this)">
                    <img src="images/painting/刘振华作品  [ 乐园：181 cm x 97 cm ]-2017年作.jpg.jpeg" alt="乐园" loading="lazy" class="">
                    <p class="mt-3 text-sm italic desc-text" contenteditable="false">乐园 | 181 cm x 97 cm | 2017</p>
                </div>
		<div class="art-card stop-motion-hover" data-category="热带花鸟系列" onclick="openViewer(this)">
                    <img src="images/painting/刘振华作品  [ 乐土：181 cm x 97 cm ] 2017年.jpg.jpeg" alt="乐土" loading="lazy" class="">
                    <p class="mt-3 text-sm italic desc-text" contenteditable="false">乐园 | 181 cm x 97 cm | 2017</p>
                </div>
		<div class="art-card stop-motion-hover" data-category="红毛猩猩系列" onclick="openViewer(this)">
                    <img src="images/painting/刘振华作品  [ 温暖的家：181 cm x 97 cm ]-2016年作.jpg.jpeg" alt="温暖的家" loading="lazy" class="">
                    <p class="mt-3 text-sm italic desc-text" contenteditable="false">温暖的家 | 181 cm x 97 cm | 2016</p>
                </div>
		<div class="art-card stop-motion-hover" data-category="南洋风景系列" onclick="openViewer(this)">
                    <img src="images/painting/作者：刘振华Liew Chan Hua 标题：南洋风光 尺寸：181 cm x 97 cm 媒介：水墨画.jpg.jpeg" alt="南洋风光" loading="lazy" class="">
                    <p class="mt-3 text-sm italic desc-text" contenteditable="false">南洋风光 | 181 cm x 97 cm | 2016</p>
                </div>
		<div class="art-card stop-motion-hover" data-category="热带花鸟系列" onclick="openViewer(this)">
                    <img src="images/painting/刘振华作品  [ 巨花图：181 cm x 97 cm ] 2016年作.jpg.jpeg" alt="巨花图" loading="lazy" class="">
                    <p class="mt-3 text-sm italic desc-text" contenteditable="false">巨花图 | 181 cm x 97 cm | 2016</p>
                </div>
		<div class="art-card stop-motion-hover" data-category="热带花鸟系列" onclick="openViewer(this)">
                    <img src="images/painting/刘振华作品  [争艳：70 cm x70 cm ]-2016年作.jpg.jpeg" alt="争艳" loading="lazy" class="">
                    <p class="mt-3 text-sm italic desc-text" contenteditable="false">争艳 | 70 cm x70 cm | 2016</p>
                </div>
		<div class="art-card stop-motion-hover" data-category="热带花鸟系列" onclick="openViewer(this)">
                    <img src="images/painting/刘振华作品  [粉红胡姬： 69 cm x 46 cm ] 2016年作.jpg.jpeg" alt="粉红胡姬" loading="lazy" class="">
                    <p class="mt-3 text-sm italic desc-text" contenteditable="false">粉红胡姬 | 69 cm x 46 cm | 2016</p>
                </div>
		<div class="art-card stop-motion-hover" data-category="其他传统题材系列" onclick="openViewer(this)">
                    <img src="images/painting/刘振华作品  [ 畅游：139 cm x 70cm ] 2016年作.jpg.jpeg" alt="畅游" loading="lazy" class="">
		    <p class="mt-3 text-sm italic desc-text" contenteditable="false">畅游 | 139 cm x 70cm | 2016</p>
		</div>
		<div class="art-card stop-motion-hover" data-category="热带水果系列" onclick="openViewer(this)">
                    <img src="images/painting/作者：刘振华Liew Chan Hua 标题：南洋佳果 尺寸：136 cm x 68cm 媒介：水墨画.jpg.jpeg" alt="南洋佳果" loading="lazy" class="">
                    <p class="mt-3 text-sm italic desc-text" contenteditable="false">南洋佳果 | 136 cm x 68cm | 2016</p>
                </div>
		<div class="art-card stop-motion-hover" data-category="南洋风景系列" onclick="openViewer(this)">
                    <img src="images/painting/刘振华作品  [ 旭日映红林：139 cm x 70cm ]-2016年作.jpg.jpeg" alt="旭日映红林" loading="lazy" class="">
                    <p class="mt-3 text-sm italic desc-text" contenteditable="false">旭日映红林 | 139 cm x 70cm | 2016</p>
                </div>
		<div class="art-card stop-motion-hover" data-category="热带花鸟系列" onclick="openViewer(this)">
                    <img src="images/painting/刘振华作品  [ 晨颂：181 cm x 97 cm ]-2016年作.jpg.jpeg" alt="晨颂" loading="lazy" class="">
                    <p class="mt-3 text-sm italic desc-text" contenteditable="false">晨颂 | 181 cm x 97 cm | 2016</p>
                </div>
		<div class="art-card stop-motion-hover" data-category="热带花鸟系列" onclick="openViewer(this)">
                    <img src="images/painting/作者：刘振华Liew Chan Hua 标题：神山奇草 尺寸：139 cm x  69 cm 媒介：水墨画.jpg.jpeg" alt="神山奇草" loading="lazy" class="">
                    <p class="mt-3 text-sm italic desc-text" contenteditable="false">神山奇草 | 139 cm x  69 cm | 2016</p>
                </div>
		<div class="art-card stop-motion-hover" data-category="热带花鸟系列" onclick="openViewer(this)">
                    <img src="images/painting/作者：刘振华Liew Chan Hua 标题： 巨花图 尺寸：137 cm x 69 cm 媒介：水墨画.jpg.jpeg" alt="巨花图" loading="lazy" class="">
                    <p class="mt-3 text-sm italic desc-text" contenteditable="false">巨花图 | 137 cm x  69 cm | 2016</p>
                </div>
		<div class="art-card stop-motion-hover" data-category="其他传统题材系列" onclick="openViewer(this)">
                    <img src="images/painting/刘振华作品  [ 荷塘一景：137 cm x  69 cm ] 2015年作.jpg.jpeg" alt="荷塘一景" loading="lazy" class="">
		    <p class="mt-3 text-sm italic desc-text" contenteditable="false">荷塘一景 | 137 cm x  69 cm | 2015</p>
		</div>
		<div class="art-card stop-motion-hover" data-category="热带花鸟系列" onclick="openViewer(this)">
                    <img src="images/painting/刘振华作品  [ 墨兰图： 69 cm x 46 cm ] 2015年作 .jpg.jpeg" alt="墨兰图" loading="lazy" class="">
                    <p class="mt-3 text-sm italic desc-text" contenteditable="false">墨兰图 | 69 cm x 46 cm | 2015</p>
                </div>
		<div class="art-card stop-motion-hover" data-category="热带花鸟系列" onclick="openViewer(this)">
                    <img src="images/painting/刘振华作品 【 蝴蝶兰 ：69 cm x 45 cm 】-2015年作.jpg.jpeg" alt="蝴蝶兰" loading="lazy" class="">
                    <p class="mt-3 text-sm italic desc-text" contenteditable="false">蝴蝶兰 | 69 cm x 45 cm | 2015</p>
                </div>
		<div class="art-card stop-motion-hover" data-category="热带花鸟系列" onclick="openViewer(this)">
                    <img src="images/painting/刘振华作品  [ 白兰吐香： 69 cm x 46 cm ] 2015年作.jpg.jpeg" alt="白兰吐香" loading="lazy" class="">
                    <p class="mt-3 text-sm italic desc-text" contenteditable="false">白兰吐香 | 69 cm x 46 cm | 2015</p>
                </div>
		<div class="art-card stop-motion-hover" data-category="南洋风景系列" onclick="openViewer(this)">
                    <img src="images/painting/刘振华作品： 风下之乡沙巴田园一景（ 139 cm x 69 cm )-2016年作.jpg.jpeg" alt="风下之乡沙巴田园一景" loading="lazy" class="">
                    <p class="mt-3 text-sm italic desc-text" contenteditable="false">风下之乡沙巴田园一景 | 139 cm x 69cm | 2016</p>
                </div>
		<div class="art-card stop-motion-hover" data-category="热带花鸟系列" onclick="openViewer(this)">
                    <img src="images/painting/刘振华作品 【母爱：69 cm x 58 cm ] 2015年作.jpg.jpeg" alt="母爱" loading="lazy" class="">
                    <p class="mt-3 text-sm italic desc-text" contenteditable="false">母爱 | 69 cm x 58 cm | 2015</p>
                </div>
		<div class="art-card stop-motion-hover" data-category="其他传统题材系列" onclick="openViewer(this)">
                    <img src="images/painting/刘振华作品 【向阳图 ：127 cm x 69 cm 】-2014年作.jpg.jpeg" alt="向阳图" loading="lazy" class="">
		    <p class="mt-3 text-sm italic desc-text" contenteditable="false">向阳图 | 127 cm x 69 cm | 2014</p>
		</div>
		<div class="art-card stop-motion-hover" data-category="热带水果系列" onclick="openViewer(this)">
                    <img src="images/painting/刘振华作品：红绿相映（140 cm x 69 cm) 2015年作.jpg.jpeg" alt="红绿相映" loading="lazy" class="">
                    <p class="mt-3 text-sm italic desc-text" contenteditable="false">红绿相映 | 140 cm x 69 cm | 2015</p>
                </div>
		<div class="art-card stop-motion-hover" data-category="其他传统题材系列" onclick="openViewer(this)">
                    <img src="images/painting/刘振华作品：迎风（135 cm x 68 cm )-2014年作.jpg.jpeg" alt="迎风" loading="lazy" class="">
		    <p class="mt-3 text-sm italic desc-text" contenteditable="false">迎风 | 135 cm x 68 cm | 2014</p>
		</div>
		<div class="art-card stop-motion-hover" data-category="南洋风景系列" onclick="openViewer(this)">
                    <img src="images/painting/刘振华作品：南洋风光  (243 cm x 120 cm) 2014年作.jpg.jpeg" alt="南洋风光" loading="lazy" class="">
                    <p class="mt-3 text-sm italic desc-text" contenteditable="false">南洋风光 | 243 cm x 120 cm | 2014</p>
                </div>
		<div class="art-card stop-motion-hover" data-category="热带花鸟系列" onclick="openViewer(this)">
                    <img src="images/painting/刘振华作品：山中奇草【 139 cm x 69 cm 】2014年作.jpg.jpeg" alt="山中奇草" loading="lazy" class="">
                    <p class="mt-3 text-sm italic desc-text" contenteditable="false">山中奇草 | 139 cm x 69 cm | 2014</p>
                </div>
            </div>
        </section>

        <section id="biodata" class="page-content">
            <div class="flex flex-col md:flex-row gap-12 items-start">
                <div class="w-full md:w-1/3 text-center">
                    <img id="profilePic" src="images/profile/姓名 刘振华 Liew Chan Hua.jpg" class="w-full rounded shadow-xl mb-4">
                    <button id="changeProfileBtn" class="hidden text-blue-500 text-xs underline" onclick="alert('Upload functionality would trigger here.')">Edit Profile Image</button>
                </div>
                <div id="bioText" class="w-full md:w-2/3 leading-relaxed space-y-6 text-justify" style="font-size: 14px;" contenteditable="false">
                    <p>刘振华，祖籍广东广宁，1965年出生于马来西亚砂拉越诗巫。1992年毕业于马来西亚艺术学院主修水墨画。两次赴中国台湾进修儿童美术教学课程。现任马来西亚水墨画协会沙巴亚庇联委会名誉会长、中国湖南祁东开福文化艺术展览馆签约艺术家、为多个艺术团体会员，山竹园画室创办人兼美术导师。受邀培训沙巴华教幼稚园美术老师及从事美术教学30多年。曾举办过9次个人画展，参加过数十次国际联展于中国大陆、新加坡、日本、中国内蒙古、中国香港、韩国、马来西亚等地区及无数次国内联展。</p>
		    <p>刘振华曾在中国荣获多次艺术奖项，包括1998年首届世界华人书画展佳作奖、2015年孔子文明艺术全国书画名家展特别奖、北京国际美术大展（亚太区）金奖、99炎帝杯世界书画展入选奖及马来西亚国内奖项。其作品亦收藏于中国艺术研究院、中国孔子画院、中国文化信息协会、河南省开福文化展览馆、韩国文化艺术研究会、马来西亚沙巴州旅游、文化及环境部、沙巴州画廊、沙巴神学院及国内外收藏人士。作品及个人资料受邀与中国大陆近代和当代书画名家入编20多集重要经典专辑。同时获得国内外报章及电子媒体等广泛报导。</p>
                    <p>刘振华的作品富有浓烈的南洋风情和热带雨林气息，结合了传统水墨画和西洋画的基本元素。作品构图严谨、线条流畅、用色古艳清新。形神兼备、气韵生动且意境优雅。作品流露出对大自然的讴歌、礼赞兼美感。创作方向坚持己见，不仿前人。以大自然为师，画风清新、自成一格，有马来西亚乡土水墨画家之美誉。题材方面多取自于当地景物、花卉走兽和风土人情：如榴莲、红毛丹、椰树、木槿花、胡姬花、红树林、莱佛西亚花、猪茏草、犀鸟、婆罗洲人猿、农村景色等。</p>
                    <p>Artist Liew Chan Hua was born in Sarawak, Malaysia in 1965.  He is the Honorary President of Chinese Ink Painting Society Malaysia, Sabah Kota Kinabalu Branch. Member of several art’s Associations and the founder of Bamboo Art Studio. He has been engaged in teaching art for more than 30 years. Liew has been holding 9 solo art exhibitions and numerous international joint art exhibitions in the mainland China, Singapore, Japan, Korea, Hong Kong, Inner Mongolia Autonomous Region and Malaysia.</p>
		    <p>Liew has worn the Creative Award of the 1st World Chinese Calligraphy and Painting Exhibition in China, The Golden Prize Beijing International Painting Show, Special Award of Confucius Civilization Art Exhibition in China, the Selected Medal Award of the 99 Emperor Yan’s International Exhibition at Hunan, China and many local art awards.</p>
		    <p>Liew’s art works were collected by the China National Academy of Art, Confucius Institute of China, Chinese Cultural Information Association of China, Hunan Kaifu Culture Exhibition Hall, Korea Culture Art Research Institute, Sabah Art Gallery, Sabah Theological Seminary and the Ministry of Tourism, Culture and Environment of Sabah. His art works and personal profiles also invited to co-publish in more than 20 art albums together with many high ranking artists in China.</p>
                </div>
            </div>
        </section>

        <section id="contact" class="page-content">
            <div class="grid md:grid-cols-4 gap-10">
                <div class="p-10 border border-transparent bg-#F9F6EE rounded-lg text-center">
		    <img src="images/icons/Facebook.png" style="width: 100px; height: 100px; block; margin-left: auto; margin-right: auto; width: auto;">
                    <h3 style="font-family: 'Chubbo', sans-serif; font-weight: 400; color: #26681f">Facebook</h3>
      		    <p id="waVal" contenteditable="false">刘振华(David Liew Chan Hua)</p>
		    <a href="https://www.facebook.com/davidliewchanhua" target="_blank" style="display: inline-block; padding: 10px 20px; background-color: #26681f; color: white;     
                     text-decoration: none; border-radius: 5px; margin-top: 10px;">
                     Follow Me </a>
                </div>
		<div class="p-10 border border-transparent bg-#F9F6EE rounded-lg text-center">
		    <img src="images/icons/Whatsapp.png" style="width: 100px; height: 100px; block; margin-left: auto; margin-right: auto; width: auto;">
                    <h3 style="font-family: 'Chubbo', sans-serif; font-weight: 400; color: #26681f">WhatsApp</h3>
      		    <p id="waVal" contenteditable="false">+60 16-813 4773</p>
		    <a href="https://wa.me/60168134773" target="_blank" style="display: inline-block; padding: 10px 20px; background-color: #26681f; color: white;     
                     text-decoration: none; border-radius: 5px; margin-top: 10px;">
                     Send Message </a>
                </div>
		<div class="p-10 border border-transparent bg-#F9F6EE rounded-lg text-center">
		    <img src="images/icons/Email.png" style="width: 100px; height: 100px; block; margin-left: auto; margin-right: auto; width: auto;">
                    <h3 style="font-family: 'Chubbo', sans-serif; font-weight: 400; color: #26681f">Email</h3> 
                    <p id="emailVal" contenteditable="false">davidliew9@gmail.com</p>
                    <a href="mailto:davidliew9@gmail.com" style="display: inline-block; padding: 10px 20px; background-color: #26681f; color: white; text-decoration: none; border-radius: 		     5px; margin-top: 10px;">
                        Send Message </a>
                </div>
		<div class="p-10 border border-transparent bg-#F9F6EE-lg text-center">
		    <img src="images/icons/Wechat.png" style="width: 100px; height: 100px; block; margin-left: auto; margin-right: auto; width: auto;">
                    <h3 style="font-family: 'Chubbo', sans-serif; font-weight: 400; color: #26681f">WeChat</h3>
		    <p id="waVal" contenteditable="false">davidliewchanhua</p>
                    <img src="images/icons/QR Wechat.png" style="width: 150px; height: 150px; block; margin-left: auto; margin-top: 10px; margin-right: auto; width: auto;">
                </div>
            </div>
        </section>
    </main>

    <div id="viewer">
        <div class="absolute top-5 right-5 text-white text-3xl cursor-pointer z-[110]" onclick="closeViewer()">✕</div>
        
        <button class="absolute top-5 left-5 text-white bg-black/40 hover:bg-green-800 px-4 py-2 rounded border border-white/20 z-[110] text-sm md:text-base" onclick="resetZoom()">
    	    恢复原大小 Reset Zoom
	</button>
        
        <div class="flex items-center justify-center h-full w-full">
            <img id="viewerImg" src="" onmousedown="startDrag(event)">
        </div>
        
        <button class="absolute right-5 top-1/2 text-white text-6xl hover:text-green-400 z-[110]" onclick="changeImg(1)">›</button>
        
        <div id="viewerDesc" class="absolute bottom-10 left-0 right-0 text-center text-white-custom font-light bg-black/50 py-2"></div>
    </div>

    <script>
        let currentIdx = 0;
        const allImgs = [];
        const allDescs = [];

        // Initialize lists for sequence navigation
        document.querySelectorAll('.art-card').forEach(card => {
            allImgs.push(card.querySelector('img').src);
            allDescs.push(card.querySelector('.desc-text').innerText);
        });

        function showPage(id) {
            const container = document.getElementById('page-container');
            const pages = ['artwork', 'biodata', 'contact'];
            const index = pages.indexOf(id);

            // 1. Fluid Swipe
            container.style.transform = `translateX(-${(index * 100) / 3}%)`;

            // 2. Toggle active class for content visibility
            document.querySelectorAll('.page-content').forEach(p => {
                p.classList.remove('active');
            });

            const targetPage = document.getElementById(id);
            if (targetPage) targetPage.classList.add('active');

            // 3. Update Navigation Button Styles
            document.querySelectorAll('nav button').forEach(btn => {
                btn.classList.remove('text-green-800', 'border-b-2', 'border-green-800', 'font-bold');
                btn.classList.add('text-gray-500');
            });
    
            // 4. Highlight the active button
            const activeBtn = document.querySelector(`nav button[onclick="showPage('${id}')"]`);
            if (activeBtn) {
                activeBtn.classList.add('text-green-800', 'border-b-2', 'border-green-800', 'font-bold');
                activeBtn.classList.remove('text-gray-500');
            }

            // Scroll to top
            window.scrollTo({top: 0, behavior: 'smooth'});
        }

        function filterArt(category) {
            const cards = document.querySelectorAll('.art-card');
            const buttons = document.querySelectorAll('#artwork button');    

            // Update button styles (using window.event to safely get the clicked button)
            buttons.forEach(btn => {
                btn.classList.remove('bg-primary', 'text-white');
                btn.classList.add('border', 'border-green-800');
            });
            
            if (window.event && window.event.target) {
                window.event.target.classList.add('bg-primary', 'text-white');
            }

            cards.forEach(card => {
                if (category === 'all' || card.getAttribute('data-category') === category) {
                    card.style.display = 'inline-block';
                    setTimeout(() => card.style.opacity = '1', 10);
                } else {
                    card.style.opacity = '0';
                    card.style.display = 'none';
                }
            });
        }

        // Fullscreen Viewer Logic
        let scale = 1;
        function openViewer(card) {
            const img = card.querySelector('img');
            currentIdx = allImgs.indexOf(img.src);
            updateViewer();
            document.getElementById('viewer').style.display = 'block';
            scale = 1;
            document.getElementById('viewerImg').style.transform = `scale(1)`;
        }

        function updateViewer() {
            document.getElementById('viewerImg').src = allImgs[currentIdx];
            document.getElementById('viewerDesc').innerText = allDescs[currentIdx];
        }

        function changeImg(dir) {
            currentIdx = (currentIdx + dir + allImgs.length) % allImgs.length;
            updateViewer();
        }

        function closeViewer() { document.getElementById('viewer').style.display = 'none'; }

        // Mousewheel Zoom
        document.getElementById('viewer').onwheel = (e) => {
            e.preventDefault();
            scale += e.deltaY * -0.001;
            scale = Math.min(Math.max(0.5, scale), 4);
            document.getElementById('viewerImg').style.transform = `scale(${scale})`;
        };

        // Keyboard Support: Escape to close, Arrows to navigate
	document.addEventListener('keydown', (e) => {
    	    const viewer = document.getElementById('viewer');
    	    if (viewer.style.display === 'block') {
            	if (e.key === "Escape") closeViewer();
            	if (e.key === "ArrowRight") changeImg(1);
              	if (e.key === "ArrowLeft") changeImg(-1);
    	    }
	});

	// Pointer Events (Supports both Mouse and Touch)
	let isDragging = false;
	let startX, startY, scrollLeft, scrollTop;

	const vImg = document.getElementById('viewerImg');

	vImg.addEventListener('pointerdown', (e) => {
    	    isDragging = true;
            vImg.style.cursor = 'grabbing';
    	    startX = e.clientX;
    	    startY = e.clientY;
    	    // Store current margins to continue drag from previous position
    	    scrollLeft = parseInt(vImg.style.marginLeft) || 0;
    	    scrollTop = parseInt(vImg.style.marginTop) || 0;
    	    vImg.setPointerCapture(e.pointerId);
	});

	vImg.addEventListener('pointermove', (e) => {
    	    if (!isDragging) return;
    	    const dx = e.clientX - startX;
    	    const dy = e.clientY - startY;
    	    vImg.style.marginLeft = (scrollLeft + dx) + 'px';
    	    vImg.style.marginTop = (scrollTop + dy) + 'px';
	});

	vImg.addEventListener('pointerup', (e) => {
    	    isDragging = false;
    	    vImg.style.cursor = 'grab';
    	    vImg.releasePointerCapture(e.pointerId);
	});

        // 1. Disable Right-Click menu
        document.addEventListener('contextmenu', event => event.preventDefault());

        // 2. Disable dragging images (preventing users from dragging to desktop)
        document.addEventListener('dragstart', event => {
            if (event.target.tagName === 'IMG') {
            event.preventDefault();
            }
        });
	window.onscroll = function() {
            const btn = document.getElementById('toTopBtn');
            if (document.body.scrollTop > 300 || document.documentElement.scrollTop > 300) {
                btn.classList.add('show');
            } else {
                btn.classList.remove('show');
            }
        };

	// 3. Prevent keyboard shortcuts for Developer Tools (F12, Ctrl+Shift+I, etc.)
	document.onkeydown = function(e) {
    	    if (e.keyCode == 123) return false; // F12
    	    if (e.ctrlKey && e.shiftKey && (e.keyCode == 'I'.charCodeAt(0) || e.keyCode == 'J'.charCodeAt(0))) return false;
    	    if (e.ctrlKey && e.keyCode == 'U'.charCodeAt(0)) return false; // View Source
	};
	function searchArt() {
    	    const input = document.getElementById('artSearch').value.toLowerCase();
    	    const cards = document.querySelectorAll('.art-card');

    	    cards.forEach(card => {
        	// 获取图片描述中的文字内容
        	const desc = card.querySelector('.desc-text').innerText.toLowerCase();
        	// 获取图片的alt属性文字
        	const alt = card.querySelector('img').alt.toLowerCase();

        	if (desc.includes(input) || alt.includes(input)) {
            	    card.style.display = 'inline-block';
            	    card.style.opacity = '1';
        	} else {
            	    card.style.opacity = '0';
            	    card.style.display = 'none';
        	}
    	    });
	}
	// 1. 定义重置函数
	function resetZoom() {
    	    const vImg = document.getElementById('viewerImg');
    	    scale = 1; // 重置全局缩放倍数
    	    vImg.style.transform = `scale(1)`; // 恢复缩放
    	    vImg.style.marginLeft = '0px'; // 归位中心
    	    vImg.style.marginTop = '0px';  // 归位中心
	}

	// 2. 为查看器图片添加双击监听
	document.getElementById('viewerImg').addEventListener('dblclick', function() {
    	    resetZoom();
	});

	// 3. 修改原有的 changeImg 函数，确保切换下一张时自动重置缩放（可选，建议添加）
	const originalChangeImg = changeImg;
	changeImg = function(dir) {
    	    resetZoom();
    	    originalChangeImg(dir);
	};
    </script>
    <button id="toTopBtn" onclick="window.scrollTo({top: 0, behavior: 'smooth'})" class="fixed bottom-8 right-8 bg-primary text-white p-4 rounded-full shadow-2xl opacity-0 transition-opacity duration-300 z-[100] border border-white/20">↑</button>
</body>
</html>
