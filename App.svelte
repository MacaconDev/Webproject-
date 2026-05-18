<script>
  import { onMount } from 'svelte';
  import { fly, fade, scale } from 'svelte/transition';
  import { cubicOut } from 'svelte/easing';

  let visible = false;
  let mouseX = 0;
  let mouseY = 0;
  let isDesktop = true;

  // ข้อมูลส่วนตัวของคุณลีโอ
  const profile = {
    name: "PHANATHON SANGTA",
    thaiName: "นายปัณณธร แสงตา",
    nickname: "LEO // ลีโอ",
    class: "CLASS: M.5/2",
    status: "STATUS: ONLINE",
    avatar: "https://img2.pic.in.th/1000010238.webp", // รูปภาพของคุณลีโอ
    bio: "I LOVE CODE I LOVE PROGRAMMING.",
    facebook: "https://www.facebook.com/share/14dfVCWQFb8/",
    instagram: "https://www.instagram.com/phanathonsangta?igsh=Z2s4ano0cjRxbWtq"
  };

  onMount(() => {
    visible = true;
    isDesktop = window.innerWidth > 768;
    window.addEventListener('resize', () => {
      isDesktop = window.innerWidth > 768;
    });
  });

  function handleMouseMove(event) {
    if (!isDesktop) return;
    const { innerWidth, innerHeight } = window;
    mouseX = (innerWidth / 2 - event.pageX) / 45;
    mouseY = (innerHeight / 2 - event.pageY) / 45;
  }

  function handleMouseLeave() {
    mouseX = 0;
    mouseY = 0;
  }
</script>

<svelte:head>
  <!-- Bootstrap 5 -->
  <link href="https://cdn.jsdelivr.net/npm/bootstrap@5.3.0/dist/css/bootstrap.min.css" rel="stylesheet">
  <!-- FontAwesome Icons -->
  <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.4.0/css/all.min.css">
  <!-- Google Fonts: Orbitron (ไซเบอร์เหลี่ยม) และ Prompt (ไทยโมเดิร์น) -->
  <link href="https://fonts.googleapis.com/css2?family=Orbitron:wght@500;700;900&family=Prompt:wght@300;400;600&display=swap" rel="stylesheet">
</svelte:head>

<svelte:window on:mousemove={handleMouseMove} on:mouseleave={handleMouseLeave} />

<main class="cyber-container min-vh-100 d-flex align-items-center justify-content-center overflow-hidden position-relative p-3">
  
  <!-- BACKGROUND LAYER (ตารางกริดและแสงสะท้อน) -->
  <div class="cyber-bg-grid"></div>
  <div class="neon-glow glow-blue"></div>
  <div class="neon-glow glow-cyan"></div>

  {#if visible}
    <!-- 3D PARALLAX CONTAINER -->
    <div 
      class="container position-relative z-3"
      style="transform: perspective(1500px) rotateY({mouseX}deg) rotateX({mouseY}deg);"
    >
      <div class="row g-4 align-items-stretch justify-content-center">
        
        <!-- ================= ฝั่งซ้าย: กล่องรูปภาพทรงเหลี่ยมดิบๆ ================= -->
        <div class="col-lg-4 d-flex">
          <div class="cyber-card image-card w-100 text-center d-flex flex-column justify-content-center position-relative p-4" in:scale={{ duration: 800, easing: cubicOut, start: 0.95 }}>
            
            <!-- ดีเทลเหลี่ยมมุมกล่อง -->
            <div class="corner-line top-left"></div>
            <div class="corner-line bottom-right"></div>
            
            <div class="avatar-box mx-auto mb-4 position-relative">
              <!-- กรอบสี่เหลี่ยมซ้อนกันเป็นเลเยอร์ -->
              <div class="border-frame-rear"></div>
              <img src={profile.avatar} alt="Leo Profile" class="cyber-avatar shadow" in:fly={{ y: 30, duration: 600, delay: 300 }} />
            </div>

            <!-- ป้ายแถบสถานะทรงเหลี่ยม -->
            <div class="status-tag px-3 py-1 mx-auto mb-2" in:fade={{ delay: 600 }}>
              <span class="pulse-dot"></span>
              <span class="ms-2 small-tech">{profile.status}</span>
            </div>

            <div class="small-tech text-cyan mt-1" in:fade={{ delay: 700 }}>{profile.class}</div>
          </div>
        </div>

        <!-- ================= ฝั่งขวา: กล่องข้อความและปุ่มกดเหลี่ยมเพชร ================= -->
        <div class="col-lg-7 d-flex">
          <div class="cyber-card main-card w-100 p-4 p-md-5 d-flex flex-column justify-content-between" in:scale={{ duration: 800, delay: 200, easing: cubicOut, start: 0.95 }}>
            
            <!-- โค้ดลายน้ำจางๆ สไตล์เว็บดีไซเนอร์ -->
            <div class="watermark-text">LEO_052</div>

            <div>
              <!-- เมนูแถบบน -->
              <div class="d-flex justify-content-between align-items-center mb-4 card-header-line">
                <span class="text-cyan small-tech"><i class="fas fa-bolt me-2"></i> DATA_ACCESS: CONNECTED</span>
                <span class="text-muted small-tech">SYS_V.52</span>
              </div>

              <!-- ชื่อภาษาอังกฤษตัวหนาดุดัน -->
              <h1 class="display-4 fw-black text-white tech-font mb-1" in:fly={{ x: -20, duration: 600, delay: 400 }}>
                {profile.name}
              </h1>
              
              <!-- ชื่อภาษาไทยและชื่อเล่น -->
              <h3 class="text-white-50 th-name mb-4" in:fly={{ x: -20, duration: 600, delay: 500 }}>
                {profile.thaiName} <span class="text-cyan">({profile.nickname})</span>
              </h3>
              
              <p class="bio-text text-muted mb-5" in:fly={{ y: 15, duration: 600, delay: 600 }}>
                {profile.bio}
              </p>
            </div>

            <!-- ================= ปุ่มกดช่องทางติดต่อ (เหลี่ยมมุมตัด) ================= -->
            <div>
              <div class="small-tech text-muted mb-3">// USER_NETWORKS</div>
              <div class="row g-3">
                
                <!-- Facebook -->
                <div class="col-sm-6" in:fly={{ y: 15, delay: 700 }}>
                  <a href={profile.facebook} target="_blank" rel="noopener noreferrer" class="square-btn btn-facebook w-100">
                    <div class="btn-skew-layer"></div>
                    <i class="fab fa-facebook-f me-2"></i> FACEBOOK
                  </a>
                </div>

                <!-- Instagram -->
                <div class="col-sm-6" in:fly={{ y: 15, delay: 800 }}>
                  <a href={profile.instagram} target="_blank" rel="noopener noreferrer" class="square-btn btn-instagram w-100">
                    <div class="btn-skew-layer"></div>
                    <i class="fab fa-instagram me-2"></i> INSTAGRAM
                  </a>
                </div>

              </div>
            </div>

          </div>
        </div>

      </div>
    </div>
  {/if}

</main>

<style>
  /* 🎛️ Dark Cyber-Blue Theme Config */
  :root {
    --bg-dark: #030611;
    --card-dark: rgba(7, 12, 28, 0.75);
    --blue-primary: #0044ff;
    --cyan-accent: #00f0ff;
    --border-tech: rgba(0, 240, 255, 0.18);
  }

  :global(body) {
    background-color: var(--bg-dark);
    font-family: 'Prompt', sans-serif;
    margin: 0;
    overflow-x: hidden;
  }

  /* ฟอนต์แนวเหลี่ยมไซเบอร์ */
  .tech-font {
    font-family: 'Orbitron', sans-serif;
    font-weight: 900;
    letter-spacing: -1px;
  }

  .small-tech {
    font-family: 'Orbitron', sans-serif;
    font-size: 0.8rem;
    letter-spacing: 1.5px;
    font-weight: 700;
  }

  /* 🌌 BACKGROUND LAYERS */
  .cyber-container {
    background: radial-gradient(circle at 50% 50%, #081126 0%, var(--bg-dark) 100%);
  }

  .cyber-bg-grid {
    position: absolute;
    inset: 0;
    background-image: 
      linear-gradient(rgba(0, 240, 255, 0.015) 1px, transparent 1px),
      linear-gradient(90deg, rgba(0, 240, 255, 0.015) 1px, transparent 1px);
    background-size: 35px 35px;
    z-index: 1;
  }

  .neon-glow {
    position: absolute;
    border-radius: 50%;
    filter: blur(130px);
    opacity: 0.2;
    z-index: 2;
    pointer-events: none;
  }
  .glow-blue { width: 500px; height: 500px; background: var(--blue-primary); top: -10%; left: 15%; }
  .glow-cyan { width: 450px; height: 450px; background: var(--cyan-accent); bottom: -5%; right: 10%; }

  /* 🎴 CYBER HARD-EDGED CARDS (การ์ดเหลี่ยมหนาแบบไม่โค้งมน) */
  .cyber-card {
    background: var(--card-dark);
    backdrop-filter: blur(15px);
    -webkit-backdrop-filter: blur(15px);
    border: 1px solid var(--border-tech);
    /* เอาความโค้งมนออก (หรือเหลือแค่ 4px นิดเดียวพอให้คม) */
    border-radius: 4px; 
    box-shadow: 0 25px 50px rgba(0, 0, 0, 0.6);
    position: relative;
    transform-style: preserve-3d;
    transition: border-color 0.3s, box-shadow 0.3s;
  }

  .cyber-card:hover {
    border-color: rgba(0, 240, 255, 0.4);
    box-shadow: 0 25px 50px rgba(0, 240, 255, 0.08);
  }

  /* แถบตกแต่งมุมกล่องแบบเหลี่ยม */
  .corner-line {
    position: absolute;
    width: 15px;
    height: 15px;
    border: 2px solid var(--cyan-accent);
    pointer-events: none;
  }
  .corner-line.top-left { top: -1px; left: -1px; border-right: none; border-bottom: none; }
  .corner-line.bottom-right { bottom: -1px; right: -1px; border-left: none; border-top: none; }

  /* 📷 BOX LAYER AVATAR (รูปภาพสี่เหลี่ยมจัตุรัสแบบคมๆ) */
  .avatar-box {
    width: 200px;
    height: 200px;
    transform: translateZ(30px);
  }

  .cyber-avatar {
    width: 100%;
    height: 100%;
    object-fit: cover;
    border: 2px solid #ffffff;
    border-radius: 4px; /* ทรงเหลี่ยม */
    position: relative;
    z-index: 2;
  }

  /* เฟรมเหลี่ยมซ้อนข้างหลังรูป */
  .border-frame-rear {
    position: absolute;
    inset: 6px;
    border: 2px solid var(--cyan-accent);
    transform: rotate(4deg);
    z-index: 1;
    transition: transform 0.4s ease;
  }
  .image-card:hover .border-frame-rear {
    transform: rotate(0deg) scale(1.05);
  }

  /* ป้ายสถานะ */
  .status-tag {
    background: rgba(255, 255, 255, 0.04);
    border: 1px solid rgba(255, 255, 255, 0.1);
    display: inline-flex;
    align-items: center;
    border-radius: 2px;
  }
  .pulse-dot {
    width: 7px;
    height: 7px;
    background-color: #00ff66;
    border-radius: 50%;
    box-shadow: 0 0 8px #00ff66;
  }

  /* 📝 TEXT ELEMENTS */
  .text-cyan { color: var(--cyan-accent); }
  
  .card-header-line {
    border-bottom: 1px solid rgba(255, 255, 255, 0.08);
    padding-bottom: 15px;
  }

  .th-name {
    font-weight: 600;
    font-size: 1.5rem;
  }

  .bio-text {
    font-size: 1rem;
    line-height: 1.7;
    max-width: 600px;
  }

  .watermark-text {
    position: absolute;
    right: 20px;
    top: 25px;
    font-family: 'Orbitron', sans-serif;
    font-size: 4rem;
    font-weight: 900;
    color: rgba(255, 255, 255, 0.015);
    pointer-events: none;
    user-select: none;
  }

  /* 🔘 SQUARE BUTTONS (ปุ่มเหลี่ยมมุมตัดเฉียง สไตล์ Reawx) */
  .square-btn {
    position: relative;
    display: inline-flex;
    align-items: center;
    justify-content: center;
    padding: 15px 20px;
    font-family: 'Orbitron', sans-serif;
    font-size: 0.85rem;
    font-weight: 700;
    letter-spacing: 2px;
    color: #ffffff;
    text-decoration: none;
    background: rgba(255, 255, 255, 0.02);
    border: 1px solid rgba(255, 255, 255, 0.1);
    border-radius: 0px; /* สี่เหลี่ยมตัดมุมคม */
    overflow: hidden;
    transition: all 0.3s ease;
    transform: translateZ(20px);
  }

  /* เลเยอร์สีไฮไลท์วิ่งสไลด์ตอนเมาส์ชี้ */
  .btn-skew-layer {
    position: absolute;
    top: 0;
    left: -100%;
    width: 100%;
    height: 100%;
    z-index: -1;
    transition: all 0.4s cubic-bezier(0.25, 1, 0.5, 1);
  }

  .square-btn:hover {
    color: #000000;
    border-color: transparent;
    transform: translateY(-4px) translateZ(30px);
  }

  .square-btn:hover .btn-skew-layer {
    left: 0;
  }

  .btn-facebook .btn-skew-layer { background: #1877F2; }
  .btn-facebook:hover { box-shadow: 0 10px 20px rgba(24, 119, 242, 0.3); }

  .btn-instagram .btn-skew-layer { background: linear-gradient(45deg, #f9ce34, #ee2a7b, #6228d7); }
  .btn-instagram:hover { color: #ffffff; box-shadow: 0 10px 20px rgba(238, 42, 123, 0.3); }

  /* Responsive สำหรับจอมือถือ */
  @media (max-width: 991px) {
    .main-card {
      padding: 30px 20px !important;
    }
    .watermark-text {
      font-size: 2.5rem;
    }
  }
</style>
    
