---
masthead_title: "La bohème by @haanss"
# title: "La bohème by @haanss"
layout: splash
author_profile: false
---

<!-- 1. 커스텀 스타일 (CSS) -->
<style>
  .portal-wrapper { font-family: 'Apple SD Gothic Neo', sans-serif; margin-top: 30px; }

  /* 카루셀 하단 정렬 완벽 고정 및 링크 속성 초기화 */
  .swiper { width: 100%; height: 450px; border-radius: 16px; margin-bottom: 40px; overflow: hidden; background: #111; position: relative; }
  .swiper-slide { padding: 0; color: white; background-size: cover; background-position: center; position: relative; display: block; text-decoration: none !important; cursor: pointer; }
  
  .featured-content { position: absolute; bottom: 60px; left: 50px; max-width: 60%; z-index: 2; text-align: left; }
  .featured-tag { font-size: 0.8rem; font-weight: bold; letter-spacing: 2px; color: #eee !important; margin-bottom: 10px; }
  
  /* 타이틀 2줄 고정 */
  .featured-title { 
    font-size: 2.2rem; 
    font-weight: bold; 
    line-height: 1.2; 
    height: 5.28rem;
    margin: 0; 
    color: #fff !important; 
    border: none !important; 
    display: -webkit-box; 
    -webkit-line-clamp: 2; 
    -webkit-box-orient: vertical; 
    overflow: hidden; 
    text-overflow: ellipsis; 
  }
  
  .featured-divider { width: 100%; height: 1px; background: rgba(255, 255, 255, 0.2); margin: 16px 0; }
  .featured-meta { font-size: 0.95rem; color: #fff !important; opacity: 0.8; }
  
  .slide-overlay { 
    position: absolute; top:0; left:0; width: 100%; height: 100%; 
    background: 
      linear-gradient(to top, rgba(0,0,0,0.95) 0%, rgba(0,0,0,0.1) 60%),
      linear-gradient(to right, rgba(0,0,0,0.3) 0%, rgba(0,0,0,0) 50%); 
    z-index: 1; 
  }

  /* 4열 큐레이션 그리드 */
  .curation-grid { display: grid; grid-template-columns: repeat(4, 1fr); gap: 24px; }
  .curation-card { display: flex; flex-direction: column; background: #fff; border-radius: 16px; overflow: hidden; text-decoration: none !important; color: inherit; transition: transform 0.2s ease-in-out; position: relative; border: 1px solid #f0f0f0; min-height: 450px; }
  .curation-card:hover { transform: translateY(-8px); box-shadow: 0 10px 20px rgba(0,0,0,0.08); }
  
  /* 이미지 래퍼를 1:1 정사각형 비율로 설정 */
  .card-img-wrap { width: 100%; aspect-ratio: 1 / 1; height: auto; overflow: hidden; background: #f8f8f8; display: flex; align-items: center; justify-content: center; position: relative; }
  .card-img { width: 100%; height: 100%; object-fit: cover; transition: opacity 0.5s ease-in-out; }
  
  .card-info { padding: 20px; display: flex; flex-direction: column; flex-grow: 1; position: relative; box-sizing: border-box; width: 100%; }
  .card-category { font-size: 0.85rem; font-weight: bold; color: #555; margin-bottom: 8px; letter-spacing: 1px; }
  
  /* 카드 내부 페이드(Fade) 효과용 */
  .fade-text { transition: opacity 0.5s ease-in-out; opacity: 1; }
  .fade-out { opacity: 0 !important; pointer-events: none; }

  .card-title { font-size: 1.05rem; font-weight: bold; margin: 0 0 10px 0; line-height: 1.4; font-family: sans-serif; color: #111; height: 2.8rem; display: -webkit-box; -webkit-line-clamp: 2; -webkit-box-orient: vertical; overflow: hidden; }
  .card-desc { font-size: 0.8rem; color: #888; margin-top: auto; display: flex; justify-content: space-between; align-items: center; }
  
  /* NEW 우측 상단 뱃지 */
  .badge { position: absolute; top: 15px; right: 15px; width: 45px; height: 45px; border-radius: 50%; display: flex; align-items: center; justify-content: center; font-size: 0.7rem; font-weight: bold; color: white; z-index: 3; box-shadow: 0 4px 6px rgba(0,0,0,0.1); transition: opacity 0.5s ease-in-out; }
  .badge-blue { background: #1a73e8; }
  .badge-gold { background: #c5a059; }
  .badge-pink { background: #d81b60; }
  .badge-black { background: #111; }

  /* 랜덤 순환 정보 상태 뱃지 (RECENT, EDITOR'S PICK, ARCHIVE) */
  .status-badge { font-size: 0.65rem; padding: 3px 6px; border-radius: 4px; background: rgba(0,0,0,0.06); color: #666; font-weight: bold; text-transform: uppercase; }

  /* 1. FILM 카드 스타일 (그라데이션 박스 높이를 늘려 제목 2줄 잘림 방지) */
  .card-film-style { border: none; min-height: 450px; }
  .card-film-style .card-img-wrap { position: absolute; top: 0; left: 0; width: 100%; height: 100%; z-index: 0; }
  .card-film-style .card-info { position: absolute; bottom: 0; left: 0; width: 100%; z-index: 2; background: linear-gradient(to top, rgba(0,0,0,0.95) 0%, rgba(0,0,0,0.6) 60%, rgba(0,0,0,0) 100%); padding: 100px 20px 20px 20px; box-sizing: border-box; height: 260px; }
  .card-film-style .card-category { color: #ddd; }
  .card-film-style .card-title { color: #fff; }
  .card-film-style .card-desc { color: #aaa; margin-top: 0; }
  .card-film-style .status-badge { background: rgba(255,255,255,0.2); color: #fff; }

  /* 2. MUSIC 카드 스타일 (배경 연회색, 이미지 80%) */
  .card-music-style .card-img-wrap { background: #f0f0f0; aspect-ratio: 1 / 1; }
  .card-music-style .card-img { width: 80%; height: 80%; border-radius: 4px; box-shadow: 0 8px 16px rgba(0,0,0,0.15); object-fit: cover; aspect-ratio: 1 / 1; }

  /* 3. BOOK 카드 스타일 */
  .card-book-style { border: none; background: #fdf6e9; min-height: 450px; }
  .card-book-style .card-img-wrap { position: absolute; top: 0; left: 0; width: 100%; height: 100%; z-index: 0; opacity: 0.2; background: #000; transition: opacity 0.3s ease-in-out; }
  .card-book-style:hover .card-img-wrap { opacity: 0.7; }
  .card-book-style .card-info { position: relative; z-index: 2; display: flex; flex-direction: column; text-align: center; height: 100%; box-sizing: border-box; padding: 20px; }
  .card-book-style .book-center-wrap { margin: auto 0; width: 100%; } 
  .card-book-style .card-category { margin-bottom: 15px; }
  .card-book-style .card-title { font-size: 1.2rem; margin: 0; height: auto; display: block; }
  .card-book-style .card-desc { margin-top: auto; width: 100%; justify-content: space-between; gap: 8px; } 

  @media (max-width: 1024px) { .curation-grid { grid-template-columns: repeat(2, 1fr); } }
  @media (max-width: 768px) { 
    .curation-grid { grid-template-columns: 1fr; } 
    .swiper { height: 350px; } 
    .featured-title { font-size: 1.8rem; height: 4.32rem; } 
    .featured-content { max-width: 100%; left: 30px; bottom: 40px; } 
  }
</style>

<link rel="stylesheet" href="https://cdn.jsdelivr.net/npm/swiper@10/swiper-bundle.min.css" />
<script src="https://cdn.jsdelivr.net/npm/swiper@10/swiper-bundle.min.js"></script>


<!-- 2. HTML 뼈대 -->
<div class="portal-wrapper">
  
  <!-- 상단 피처드 카루셀 -->
  <div class="swiper mySwiper">
    <div class="swiper-wrapper">
      {% for post in site.posts limit:3 %}
      {% assign bg_image = post.header.overlay_image | default: post.header.image | default: post.image %}
      {% if bg_image == nil or bg_image == empty %}
        {% assign bg_image = "https://images.unsplash.com/photo-1492691527719-9d1e07e534b4?auto=format&fit=crop&w=1600&q=80" %}
      {% endif %}
      
      <a href="{{ post.url | relative_url }}" class="swiper-slide" style="background-image: url('{{ bg_image | relative_url }}');">
        <div class="slide-overlay"></div>
        <div class="featured-content">
          <div class="featured-tag">{% if forloop.first %}LATEST ARTICLE{% else %}EDITOR'S PICK{% endif %}</div>
          <h2 class="featured-title">{{ post.title }}</h2>
          <div class="featured-divider"></div>
          <div class="featured-meta">{{ post.date | date: "%Y. %m. %d." }} • {{ post.categories | first | default: "Blog" }}</div>
        </div>
      </a>
      {% endfor %}
    </div>
    <div class="swiper-button-next" style="color: white;"></div>
    <div class="swiper-button-prev" style="color: white;"></div>
  </div>

  <div class="curation-grid">
    
    <!-- TECH 카드 -->
    {% assign tech_post = site.categories.Tech | first %}
    {% if tech_post %}
      {% assign tech_image = tech_post.header.overlay_image | default: tech_post.header.image | default: tech_post.image %}
      {% if tech_image == nil or tech_image == empty %}
        {% assign tech_image = "https://images.unsplash.com/photo-1517336714731-489689fd1ca8" %}
      {% endif %}
      
      <a href="{{ tech_post.url | relative_url }}" class="curation-card">
        <div class="badge badge-pink">NEW</div>
        <div class="card-img-wrap"><img src="{{ tech_image | relative_url }}" class="card-img"></div>
        <div class="card-info">
          <div class="card-category">TECH</div>
          <h3 class="card-title">{{ tech_post.title }}</h3>
          <div class="card-desc">
            <span>{{ tech_post.date | date: "%Y. %m. %d." }}</span>
            <span class="status-badge">RECENT</span>
          </div>
        </div>
      </a>
    {% else %}
      <a href="#" class="curation-card">
        <div class="badge badge-pink">NEW</div>
        <div class="card-img-wrap"><img src="https://images.unsplash.com/photo-1517336714731-489689fd1ca8" class="card-img"></div>
        <div class="card-info">
          <div class="card-category">TECH</div>
          <h3 class="card-title">첫 번째 TECH 글을 작성해 주세요</h3>
          <div class="card-desc">-</div>
        </div>
      </a>
    {% endif %}

    <!-- FILM 카드 -->
    <a href="#" class="curation-card card-film-style" id="card-film">
      <div class="badge badge-gold fade-text" id="top-badge-film">NEW</div>
      <div class="card-img-wrap"><img src="" class="card-img fade-text" id="img-film" style="display:none;"></div>
      <div class="card-info">
        <div class="card-category">FILM</div>
        <h3 class="card-title fade-text" id="title-film">데이터 불러오는 중...</h3>
        <div class="card-desc">
          <span class="fade-text" id="desc-film">Loading...</span>
          <span class="status-badge fade-text" id="badge-film">RECENT</span>
        </div>
      </div>
    </a>

    <!-- MUSIC 카드 -->
    <a href="#" class="curation-card card-music-style" id="card-music">
      <div class="badge badge-blue fade-text" id="top-badge-music">NEW</div>
      <div class="card-img-wrap"><img src="" class="card-img fade-text" id="img-music" style="display:none;"></div>
      <div class="card-info">
        <div class="card-category">MUSIC</div>
        <h3 class="card-title fade-text" id="title-music">데이터 불러오는 중...</h3>
        <div class="card-desc">
          <span class="fade-text" id="desc-music">Loading...</span>
          <span class="status-badge fade-text" id="badge-music">RECENT</span>
        </div>
      </div>
    </a>

    <!-- BOOK 카드 -->
    <a href="#" class="curation-card card-book-style" id="card-book">
      <div class="badge badge-black fade-text" id="top-badge-book">NEW</div>
      <div class="card-img-wrap"><img src="" class="card-img fade-text" id="img-book" style="display:none;"></div>
      <div class="card-info">
        
        <div class="book-center-wrap">
          <div class="card-category">BOOK</div>
          <h3 class="card-title fade-text" id="title-book">데이터 불러오는 중...</h3>
        </div>

        <div class="card-desc">
          <span class="fade-text" id="desc-book">Loading...</span>
          <span class="status-badge fade-text" id="badge-book">RECENT</span>
        </div>

      </div>
    </a>
    
  </div>
</div>

<!-- 3. 자바스크립트 -->
<script>
  var swiper = new Swiper(".mySwiper", {
    navigation: { nextEl: ".swiper-button-next", prevEl: ".swiper-button-prev" },
    loop: true,
    autoplay: { delay: 5000, disableOnInteraction: false }
  });

  // 카테고리별 글 데이터 및 타이머 저장소
  const rollingData = {
    film: { posts: [], currentIndex: 0, timeoutId: null },
    music: { posts: [], currentIndex: 0, timeoutId: null },
    book: { posts: [], currentIndex: 0, timeoutId: null }
  };

  function fetchJekyllFeed(url, type) {
    fetch(url)
      .then(response => {
        if (!response.ok) throw new Error('네트워크 응답 에러');
        return response.text();
      })
      .then(str => new window.DOMParser().parseFromString(str, "text/xml"))
      .then(data => {
        const entries = Array.from(data.querySelectorAll("entry"));
        
        if (entries.length > 0) {
          const extractedPosts = [];

          // 1. RECENT (가장 최신 글)
          extractedPosts.push({ ...parseEntry(entries[0], url), label: 'RECENT', isLatest: true });

          // 2. EDITOR'S PICK
          if (entries.length > 1) {
            const range10 = entries.slice(1, Math.min(10, entries.length));
            const randIdx = Math.floor(Math.random() * range10.length);
            extractedPosts.push({ ...parseEntry(range10[randIdx], url), label: "EDITOR'S PICK", isLatest: false });
          }

          // 3. ARCHIVE
          if (entries.length > 10) {
            const range30 = entries.slice(10, Math.min(30, entries.length));
            const randIdx = Math.floor(Math.random() * range30.length);
            extractedPosts.push({ ...parseEntry(range30[randIdx], url), label: 'ARCHIVE', isLatest: false });
          } else if (entries.length > 2 && extractedPosts.length < 3) {
            const usedIndexes = [0, entries.indexOf(entries.find(e => e.querySelector("title").textContent === extractedPosts[1]?.title))];
            const remains = entries.filter((_, idx) => !usedIndexes.includes(idx));
            if (remains.length > 0) {
              const randIdx = Math.floor(Math.random() * remains.length);
              extractedPosts.push({ ...parseEntry(remains[randIdx], url), label: 'ARCHIVE', isLatest: false });
            }
          }

          rollingData[type].posts = extractedPosts;
          updateCardDOM(type, extractedPosts[0]);
          
          if (extractedPosts.length > 1) {
            startCardRolling(type);
          }
        }
      })
      .catch(error => {
        console.error(type + ' 에러:', error);
      });
  }

  function parseEntry(entry, originUrl) {
    const title = entry.querySelector("title").textContent;
    const link = entry.querySelector("link").getAttribute("href");
    const published = entry.querySelector("published") || entry.querySelector("updated");
    const pubDate = new Date(published.textContent).toLocaleDateString();
    
    let imgUrl = null;
    const content = entry.querySelector("content");
    if (content) {
      const tempDiv = document.createElement('div');
      tempDiv.innerHTML = content.textContent;
      const img = tempDiv.querySelector('img');
      if (img) {
        imgUrl = img.getAttribute('src');
        if (imgUrl && !imgUrl.startsWith('http')) {
          const urlObj = new URL(originUrl);
          imgUrl = urlObj.origin + (imgUrl.startsWith('/') ? '' : '/') + imgUrl;
        }
      }
    }
    return { title, link, pubDate, imgUrl };
  }

  function updateCardDOM(type, postData) {
    const card = document.getElementById('card-' + type);
    const titleEl = document.getElementById('title-' + type);
    const descEl = document.getElementById('desc-' + type);
    const imgEl = document.getElementById('img-' + type);
    const badgeEl = document.getElementById('badge-' + type);
    const topBadgeEl = document.getElementById('top-badge-' + type);

    titleEl.classList.add('fade-out');
    descEl.classList.add('fade-out');
    badgeEl.classList.add('fade-out');
    if (imgEl) imgEl.classList.add('fade-out');
    if (topBadgeEl) topBadgeEl.classList.add('fade-out');

    setTimeout(() => {
      card.href = postData.link;
      titleEl.innerText = postData.title;
      descEl.innerText = postData.pubDate;
      badgeEl.innerText = postData.label;

      if (postData.imgUrl) {
        imgEl.src = postData.imgUrl;
        imgEl.style.display = 'block';
        imgEl.classList.remove('fade-out');
      } else if (imgEl) {
        imgEl.style.display = 'none';
      }

      if (topBadgeEl && postData.isLatest) {
        topBadgeEl.classList.remove('fade-out');
      }

      titleEl.classList.remove('fade-out');
      descEl.classList.remove('fade-out');
      badgeEl.classList.remove('fade-out');
    }, 500);
  }

  function scheduleNextRolling(type) {
    const randomDelay = Math.floor(Math.random() * 1901) + 4000;
    rollingData[type].timeoutId = setTimeout(() => {
      const data = rollingData[type];
      data.currentIndex = (data.currentIndex + 1) % data.posts.length;
      updateCardDOM(type, data.posts[data.currentIndex]);
      scheduleNextRolling(type);
    }, randomDelay);
  }

  function startCardRolling(type) {
    const card = document.getElementById('card-' + type);
    
    scheduleNextRolling(type);

    card.addEventListener('mouseenter', () => {
      clearTimeout(rollingData[type].timeoutId);
    });

    card.addEventListener('mouseleave', () => {
      scheduleNextRolling(type);
    });
  }

  fetchJekyllFeed('https://bom.la-bohe.me/feed.xml', 'film');
  fetchJekyllFeed('https://umm.la-bohe.me/feed.xml', 'music');
  fetchJekyllFeed('https://ssm.la-bohe.me/feed.xml', 'book');
</script>