---
layout: base
title: "Về Tôi"
permalink: /about/
---

<style>
/* ── ABOUT PAGE SPECIFIC ─────────────────────────── */
.about-hero {
  position: relative;
  background: var(--black);
  overflow: hidden;
  padding: 56px 48px 0;
}
.about-hero::before {
  content: '';
  position: absolute;
  inset: 0;
  background:
    repeating-linear-gradient(90deg, transparent, transparent 80px, rgba(255,255,255,.018) 80px, rgba(255,255,255,.018) 81px),
    linear-gradient(180deg, #071007 0%, #0a1a0a 100%);
}
.about-hero__stripe { position: absolute; left: 0; top: 0; bottom: 0; width: 6px; background: var(--red); }

.about-wrap {
  max-width: 1000px;
  margin: 0 auto;
  padding: 0 48px 80px;
}

/* ── PROFILE CARD ────────────────────────────────── */
.profile-card {
  position: relative;
  z-index: 2;
  background: var(--panel);
  border: 1px solid var(--border);
  border-top: 3px solid var(--red);
  padding: 32px;
  display: grid;
  grid-template-columns: auto 1fr;
  gap: 28px;
  align-items: start;
  margin-bottom: -1px;
  transform: translateY(0);
}
.profile-card__avatar {
  width: 140px; height: 140px;
  border-radius: 50%;
  border: 3px solid var(--red);
  object-fit: cover;
  background: var(--red);
  display: flex;
  align-items: center;
  justify-content: center;
  font-family: var(--display);
  font-size: 36px;
  color: #fff;
  flex-shrink: 0;
  overflow: hidden;
}
.profile-card__avatar img { width: 100%; height: 100%; object-fit: cover; border-radius: 50%; }

.profile-card__info {}
.profile-card__name {
  font-family: var(--display);
  font-size: 36px;
  letter-spacing: 2px;
  color: #fff;
  line-height: 1;
  margin-bottom: 4px;
}
.profile-card__role {
  font-family: var(--mono);
  font-size: 12px;
  color: var(--red);
  letter-spacing: 1px;
  margin-bottom: 12px;
}
.profile-card__bio {
  font-size: 14px;
  color: var(--muted);
  line-height: 1.65;
  max-width: 560px;
}
.profile-card__links {
  display: flex;
  gap: 10px;
  margin-top: 16px;
  flex-wrap: wrap;
}
.profile-link {
  display: inline-flex;
  align-items: center;
  gap: 6px;
  font-family: var(--cond);
  font-weight: 700;
  font-size: 12px;
  letter-spacing: 1.5px;
  text-transform: uppercase;
  padding: 6px 14px;
  border: 1px solid var(--border);
  border-radius: var(--radius);
  color: var(--muted);
  transition: all .2s;
}
.profile-link:hover { border-color: var(--red); color: #fff; background: rgba(218,41,28,.08); }
.profile-link--primary { border-color: var(--red); color: var(--red); }
.profile-link--primary:hover { background: var(--red); color: #fff; }

/* ── SECTIONS GRID ───────────────────────────────── */
.about-grid {
  display: grid;
  grid-template-columns: 1fr 1fr;
  gap: 1px;
  background: var(--border);
  border: 1px solid var(--border);
  margin-top: 32px;
}
.about-section {
  background: var(--panel);
  padding: 28px 28px 24px;
}
.about-section--full { grid-column: 1 / -1; }
.about-section__head {
  display: flex;
  align-items: center;
  gap: 10px;
  margin-bottom: 20px;
  padding-bottom: 12px;
  border-bottom: 2px solid var(--red);
}
.about-section__icon { font-size: 18px; }
.about-section__title {
  font-family: var(--display);
  font-size: 18px;
  letter-spacing: 2px;
  color: #fff;
}

/* ── TECH STACK ──────────────────────────────────── */
.tech-group { margin-bottom: 18px; }
.tech-group:last-child { margin-bottom: 0; }
.tech-group__label {
  font-family: var(--mono);
  font-size: 10px;
  letter-spacing: 2px;
  text-transform: uppercase;
  color: var(--muted);
  margin-bottom: 8px;
}
.tech-pills { display: flex; flex-wrap: wrap; gap: 7px; }
.tech-pill {
  font-family: var(--cond);
  font-weight: 700;
  font-size: 12px;
  letter-spacing: 1px;
  text-transform: uppercase;
  padding: 5px 13px;
  border-radius: var(--radius);
  border: 1px solid var(--border);
  color: var(--text);
  transition: all .18s;
  cursor: default;
}
.tech-pill:hover { border-color: var(--red); color: #fff; }
.tech-pill--hot { border-color: rgba(218,41,28,.4); color: #f87171; }

/* skill bars */
.skill-row { margin-bottom: 12px; }
.skill-row:last-child { margin-bottom: 0; }
.skill-row__top {
  display: flex;
  justify-content: space-between;
  align-items: center;
  margin-bottom: 5px;
}
.skill-row__name {
  font-family: var(--cond);
  font-weight: 700;
  font-size: 13px;
  letter-spacing: 1px;
  color: var(--text);
}
.skill-row__pct {
  font-family: var(--mono);
  font-size: 10px;
  color: var(--muted);
}
.skill-bar {
  height: 4px;
  background: var(--border);
  border-radius: 2px;
  overflow: hidden;
}
.skill-bar__fill {
  height: 100%;
  background: var(--red);
  border-radius: 2px;
  transform: scaleX(0);
  transform-origin: left;
  transition: transform .8s cubic-bezier(.16,1,.3,1);
}
.skill-bar__fill.in { transform: scaleX(1); }

/* ── FAN CORNER ──────────────────────────────────── */
.fan-cards { display: flex; flex-direction: column; gap: 12px; }
.fan-card {
  display: flex;
  gap: 16px;
  align-items: flex-start;
  padding: 14px 16px;
  background: var(--panel2);
  border: 1px solid var(--border);
  border-radius: var(--radius);
  transition: border-color .2s;
}
.fan-card__crest img {
  width: 80px;
  height: 110px;
  object-fit: cover;
  object-position: 50% 15%;
  border-radius: 4px;
  border: 2px solid var(--border);
}
.fan-card:hover { border-color: var(--red); }
.fan-card__crest { font-size: 32px; flex-shrink: 0; line-height: 1; }
.fan-card__body {}
.fan-card__name {
  font-family: var(--cond);
  font-weight: 700;
  font-size: 15px;
  letter-spacing: 1px;
  color: #fff;
  margin-bottom: 3px;
}
.fan-card__desc { font-size: 13px; color: var(--muted); line-height: 1.5; }
.fan-card__tag {
  display: inline-block;
  margin-top: 6px;
  font-family: var(--mono);
  font-size: 10px;
  letter-spacing: 1px;
  text-transform: uppercase;
  color: var(--red);
  border: 1px solid rgba(218,41,28,.3);
  padding: 1px 7px;
  border-radius: var(--radius);
}

/* ── CONTACT ─────────────────────────────────────── */
.contact-list { display: flex; flex-direction: column; gap: 10px; }
.contact-item {
  display: flex;
  align-items: center;
  gap: 14px;
  padding: 12px 16px;
  background: var(--panel2);
  border: 1px solid var(--border);
  border-radius: var(--radius);
  text-decoration: none;
  color: inherit;
  transition: border-color .2s, background .2s;
}
.contact-item:hover { border-color: var(--red); background: rgba(218,41,28,.05); }
.contact-item__icon { font-size: 20px; flex-shrink: 0; }
.contact-item__label {
  font-family: var(--cond);
  font-weight: 700;
  font-size: 13px;
  letter-spacing: 1px;
  text-transform: uppercase;
  color: var(--text);
}
.contact-item__value {
  font-family: var(--mono);
  font-size: 12px;
  color: var(--muted);
  margin-top: 1px;
}
.contact-item__arrow {
  margin-left: auto;
  color: var(--red);
  font-size: 16px;
  opacity: 0;
  transition: opacity .18s;
}
.contact-item:hover .contact-item__arrow { opacity: 1; }

/* responsive */
@media (max-width: 700px) {
  .about-hero, .about-wrap { padding-left: 20px; padding-right: 20px; }
  .about-grid { grid-template-columns: 1fr; }
  .about-section--full { grid-column: 1; }
  .profile-card { grid-template-columns: 1fr; }
  .profile-card__avatar { width: 72px; height: 72px; font-size: 28px; }
}
</style>

<!-- HERO -->
<div class="about-hero">
  <div class="about-hero__stripe"></div>
  <div style="position:relative;z-index:2;max-width:1000px;margin:0 auto;padding-bottom:32px;">
    <div style="font-family:var(--mono);font-size:11px;letter-spacing:2px;text-transform:uppercase;color:var(--red);margin-bottom:8px;">// about.me</div>
    <h1 style="font-family:var(--display);font-size:clamp(40px,6vw,72px);letter-spacing:2px;color:#fff;line-height:.9;">VỀ <span style="color:var(--gold);">TÔI</span></h1>
  </div>
</div>

<div class="about-wrap">

  <!-- PROFILE CARD -->
  <div class="profile-card reveal">
    <div class="profile-card__avatar" id="js-avatar">
      <img src="/assets/ThanhNPN_SE1409.jpg" alt="Ngọc Thành" style="width:100%;height:100%;object-fit:cover;object-position:62% 15%;border-radius:50%;" />
    </div>
    <div class="profile-card__info">
      <div class="profile-card__name">NGUYỄN PHÚC NGỌC THÀNH</div>
      <div class="profile-card__role">// software_engineer · Ho_chi_minh_city</div>
      <p class="profile-card__bio">
        Mình là một Software Engineer đang trên hành trình không ngừng học hỏi. Blog này là nơi mình ghi chép lại những kiến thức và kinh nghiệm tích luỹ được — từ Java, Spring Boot đến Docker. Mỗi bài viết là một pha bóng, mỗi bug fix là một bàn thắng.
      </p>
      <div class="profile-card__links">
        <a class="profile-link profile-link--primary" href="https://github.com/npngocthanh99" target="_blank" rel="noopener">
          ⌥ GitHub
        </a>
        <a class="profile-link" href="/">← Về trang chủ</a>
      </div>
    </div>
  </div>

  <!-- GRID -->
  <div class="about-grid">

    <!-- TECH STACK -->
    <div class="about-section reveal">
      <div class="about-section__head">
        <span class="about-section__icon">⚙️</span>
        <span class="about-section__title">TECH STACK</span>
      </div>
      <div class="tech-group">
        <div class="tech-group__label">Backend</div>
        <div class="tech-pills">
          <span class="tech-pill tech-pill--hot">Java</span>
          <span class="tech-pill tech-pill--hot">Spring Boot</span>
          <span class="tech-pill">Spring MVC</span>
          <span class="tech-pill">Spring Security</span>
          <span class="tech-pill">Spring Data JPA</span>
        </div>
      </div>
      <div class="tech-group">
        <div class="tech-group__label">Frontend</div>
        <div class="tech-pills">
          <span class="tech-pill tech-pill--hot">React</span>
          <span class="tech-pill">HTML/CSS</span>
          <span class="tech-pill">JavaScript</span>
        </div>
      </div>
      <div class="tech-group">
        <div class="tech-group__label">Database & Cache</div>
        <div class="tech-pills">
          <span class="tech-pill">MySQL</span>
          <span class="tech-pill tech-pill--hot">Redis</span>
          <span class="tech-pill">PostgreSQL</span>
        </div>
      </div>
      <div class="tech-group">
        <div class="tech-group__label">DevOps & Tools</div>
        <div class="tech-pills">
          <span class="tech-pill tech-pill--hot">Docker</span>
          <span class="tech-pill">Git</span>
          <span class="tech-pill">GitHub Actions</span>
          <span class="tech-pill">Linux</span>
        </div>
      </div>
    </div>

    <!-- SKILL LEVEL -->
    <div class="about-section reveal">
      <div class="about-section__head">
        <span class="about-section__icon">📊</span>
        <span class="about-section__title">KỸ NĂNG</span>
      </div>
      <div class="skill-row">
        <div class="skill-row__top"><span class="skill-row__name">Java / Spring Boot</span><span class="skill-row__pct">85%</span></div>
        <div class="skill-bar"><div class="skill-bar__fill" style="width:85%"></div></div>
      </div>
      <div class="skill-row">
        <div class="skill-row__top"><span class="skill-row__name">React</span><span class="skill-row__pct">70%</span></div>
        <div class="skill-bar"><div class="skill-bar__fill" style="width:70%"></div></div>
      </div>
      <div class="skill-row">
        <div class="skill-row__top"><span class="skill-row__name">Database & Redis</span><span class="skill-row__pct">75%</span></div>
        <div class="skill-bar"><div class="skill-bar__fill" style="width:75%"></div></div>
      </div>
      <div class="skill-row">
        <div class="skill-row__top"><span class="skill-row__name">Docker & DevOps</span><span class="skill-row__pct">65%</span></div>
        <div class="skill-bar"><div class="skill-bar__fill" style="width:65%"></div></div>
      </div>
      <div class="skill-row">
        <div class="skill-row__top"><span class="skill-row__name">Data Structures & Algorithms</span><span class="skill-row__pct">70%</span></div>
        <div class="skill-bar"><div class="skill-bar__fill" style="width:70%"></div></div>
      </div>
      <div class="skill-row">
        <div class="skill-row__top"><span class="skill-row__name">System Design</span><span class="skill-row__pct">55%</span></div>
        <div class="skill-bar"><div class="skill-bar__fill" style="width:55%"></div></div>
      </div>
    </div>

    <!-- FAN CORNER -->
    <div class="about-section reveal">
      <div class="about-section__head">
        <span class="about-section__icon">⚽</span>
        <span class="about-section__title">FAN CORNER</span>
      </div>
      <div class="fan-cards">
        <div class="fan-card">
          <div class="fan-card__crest">
            <img src="/assets/marco_reus.jpg" alt="Marco Reus" />
          </div>
          <div class="fan-card__body">
            <div class="fan-card__name">Marco Reus — #11</div>
            <div class="fan-card__desc">Huyền thoại Borussia Dortmund. Kỹ thuật điêu luyện, tinh thần chiến đấu bất khuất và sự trung thành hiếm có — đó là những giá trị mình học được cả trong bóng đá lẫn trong code.</div>
            <span class="fan-card__tag">Thần tượng số 1</span>
          </div>
        </div>
        <div class="fan-card">
          <div class="fan-card__crest">
            <img src="/assets/MU.jpg" alt="Manchester United"
              style="object-position:50% 40%;" />
          </div>
          <div class="fan-card__body">
            <div class="fan-card__name">Manchester United</div>
            <div class="fan-card__desc">The Red Devils — GGMU! Theo dõi từ nhỏ. Mỗi trận thắng là nguồn năng lượng để code tiếp, mỗi trận thua là bài học về resilience.</div>
            <span class="fan-card__tag">Glory Glory Man United</span>
          </div>
        </div>
        <div class="fan-card">
          <div class="fan-card__crest">
            <img src="/assets/DE.jpg" alt="Die Mannschaft"
              style="object-position:50% 30%;" />
          </div>
          <div class="fan-card__body">
            <div class="fan-card__name">Die Mannschaft</div>
            <div class="fan-card__desc">Đội tuyển Đức với triết lý bóng đá tổ chức, kỷ luật và teamwork — giống hệt một Spring application chạy production.</div>
            <span class="fan-card__tag">Đội tuyển Đức</span>
          </div>
        </div>
      </div>
    </div>

    <!-- CONTACT -->
    <div class="about-section reveal">
      <div class="about-section__head">
        <span class="about-section__icon">📬</span>
        <span class="about-section__title">LIÊN HỆ</span>
      </div>
      <div class="contact-list">
        <a class="contact-item" href="https://github.com/npngocthanh99" target="_blank" rel="noopener">
          <span class="contact-item__icon">🐙</span>
          <div>
            <div class="contact-item__label">GitHub</div>
            <div class="contact-item__value">github.com/npngocthanh99</div>
          </div>
          <span class="contact-item__arrow">↗</span>
        </a>
        <a class="contact-item" href="https://npngocthanh99.github.io" target="_blank" rel="noopener">
          <span class="contact-item__icon">🌐</span>
          <div>
            <div class="contact-item__label">Blog</div>
            <div class="contact-item__value">npngocthanh99.github.io</div>
          </div>
          <span class="contact-item__arrow">↗</span>
        </a>
      </div>

      <!-- quote -->
      <div style="margin-top:24px;padding:16px;background:var(--black);border-left:3px solid var(--red);">
        <div style="font-family:var(--cond);font-style:italic;font-size:15px;color:var(--muted);line-height:1.5;">
          "Code như Reus chơi bóng — kỹ thuật, tốc độ, và không bao giờ bỏ cuộc."
        </div>
        <div style="font-family:var(--mono);font-size:10px;color:var(--red);margin-top:8px;letter-spacing:1px;">— npngocthanh99</div>
      </div>
    </div>

  </div>
</div>

<script>
// Animate skill bars on scroll
const bars = document.querySelectorAll('.skill-bar__fill');
const barObserver = new IntersectionObserver(entries => {
  entries.forEach(e => { if (e.isIntersecting) { e.target.classList.add('in'); barObserver.unobserve(e.target); } });
}, { threshold: 0.3 });
bars.forEach(b => barObserver.observe(b));
</script>
