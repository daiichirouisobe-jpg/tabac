// ====== 設定 ======
const CALENDAR_ID = "73332b7acc518822df0bf29e7b5bd19e4ef6dfa7475806a550ab533ba239749d@group.calendar.google.com";
const API_KEY = "AIzaSyDJi2hS06OAfLSnT2li1b-L5bfF3kePWno";

let currentYear = new Date().getFullYear();
let currentMonth = new Date().getMonth();

// ====== Google カレンダーから予定を取得 ======
async function fetchEvents(year, month) {
  const timeMin = new Date(year, month, 1).toISOString();
  const timeMax = new Date(year, month + 1, 0, 23, 59, 59).toISOString();

  const url =
    `https://www.googleapis.com/calendar/v3/calendars/${encodeURIComponent(CALENDAR_ID)}/events` +
    `?key=${API_KEY}&timeMin=${timeMin}&timeMax=${timeMax}&singleEvents=true&orderBy=startTime`;

  try {
    const res = await fetch(url);
    const data = await res.json();

    if (!data.items) return [];

    return data.items.map(event => {
      const start = event.start.date || event.start.dateTime;
      return {
        title: event.summary || "予定",
        date: start
      };
    });

  } catch (e) {
    console.error("Googleカレンダー取得エラー:", e);
    return [];
  }
}

// ====== カレンダー描画 ======
async function renderCalendar(year, month) {
  const calendar = document.getElementById("custom-calendar");
  const now = new Date();

  const firstDay = new Date(year, month, 1).getDay();
  const lastDate = new Date(year, month + 1, 0).getDate();

  // Googleカレンダーの予定を取得
  const events = await fetchEvents(year, month);

  let html = `
    <div class="calendar-header">
      <button onclick="changeMonth(-1)">←</button>
      <span>${year}年 ${month + 1}月</span>
      <button onclick="changeMonth(1)">→</button>
    </div>
    <div class="calendar-grid">
      <div>日</div><div>月</div><div>火</div><div>水</div><div>木</div><div>金</div><div>土</div>
  `;

  // 空白セル
  for (let i = 0; i < firstDay; i++) {
    html += `<div class="calendar-cell"></div>`;
  }

  // 日付セル
  for (let day = 1; day <= lastDate; day++) {
    const dateStr = `${year}-${String(month + 1).padStart(2, "0")}-${String(day).padStart(2, "0")}`;

    const isToday =
      day === now.getDate() &&
      month === now.getMonth() &&
      year === now.getFullYear();

    // 該当日のイベントを抽出
    const todaysEvents = events.filter(e => e.date.startsWith(dateStr));

    html += `
      <div class="calendar-cell ${isToday ? "today" : ""}">
        ${day}
        ${todaysEvents
          .map(ev => `<div class="event">${ev.title}</div>`)
          .join("")}
      </div>
    `;
  }

  html += `</div>`;
  calendar.innerHTML = html;
}

// ====== 月送り ======
function changeMonth(offset) {
  currentMonth += offset;
  if (currentMonth < 0) {
    currentMonth = 11;
    currentYear--;
  } else if (currentMonth > 11) {
    currentMonth = 0;
    currentYear++;
  }
  renderCalendar(currentYear, currentMonth);
}

// ====== 初期表示 ======
document.addEventListener("DOMContentLoaded", function () {
  // カレンダー初期表示
  renderCalendar(currentYear, currentMonth);

  // ===== スライダー =====
  let currentSlide = 0;
  const slides = document.querySelectorAll(".hero-slider .slide");

  if (slides.length === 0) return; // 念のため

  function showSlide(index) {
    slides.forEach((slide, i) => {
      slide.classList.remove("active", "prev");
      if (i === index) {
        slide.classList.add("active");
      } else if (i === (index - 1 + slides.length) % slides.length) {
        slide.classList.add("prev");
      }
    });
  }

  function nextSlide() {
    currentSlide = (currentSlide + 1) % slides.length;
    showSlide(currentSlide);
  }

  // 初期表示
  showSlide(0);

  // ===== ギャラリー =====
  const gallerySlides = document.querySelectorAll('.gallery-slide');
  let galleryCurrent = 0;

  function showGallerySlide(index) {
    gallerySlides.forEach((slide, i) => {
      slide.classList.remove('active', 'prev');
      if (i === index) {
        slide.classList.add('active');
      } else if (i === (index - 1 + gallerySlides.length) % gallerySlides.length) {
        slide.classList.add('prev');
      }
    });
  }

  document.getElementById('nextBtn').addEventListener('click', () => {
    galleryCurrent = (galleryCurrent + 1) % gallerySlides.length;
    showGallerySlide(galleryCurrent);
  });

  document.getElementById('prevBtn').addEventListener('click', () => {
    galleryCurrent = (galleryCurrent - 1 + gallerySlides.length) % gallerySlides.length;
    showGallerySlide(galleryCurrent);
  });

  showGallerySlide(galleryCurrent);

  // 5〜10秒ごとに切り替え
  setInterval(nextSlide, 7000);
});

// ===== ページトップボタン =====
const backToTop = document.getElementById("backToTop");

window.addEventListener("scroll", () => {
  if (window.scrollY > 50) {
    backToTop.style.display = "block";
  } else {
    backToTop.style.display = "none";
  }
});

backToTop.addEventListener("click", () => {
  window.scrollTo({
    top: 0,
    behavior: "smooth"
  });
});


