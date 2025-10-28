<!-- src/pages/About/index.vue -->
<template>
  <div class="about">
    <!-- Background Lottie -->
    <DotLottieVue
        class="bg-lottie"
        autoplay
        loop
        aria-hidden="true"
        src="https://lottie.host/371dc2e7-ffd2-41e6-8136-5dde847b3e16/xUqwrYmiW5.lottie"
    />

    <div class="content">
      <section class="intro">
        <h1 class="title">
          WELCOME TO <span class="accent">MY RESUME!</span>
        </h1>

        <div class="meta">
          <span>📍 Jakarta - Indonesia</span>
          <span>·</span>
          <a href="mailto:raihanamin2212@gmail.com">raihanamin2212@gmail.com</a>
          <span>·</span>
          <a href="tel:+6281284697557">🇲🇨 (+62) 81284697557</a>
        </div>

        <p class="lead">
          Aku adalah seorang <strong>Backend Developer</strong> selama <strong>2 tahun</strong>,
          berfokus pada pengembangan layanan menggunakan <strong>Golang</strong> dan <strong>gRPC</strong>.
        </p>
        <p class="lead">
          Selama bekerja, aku membangun dan memelihara berbagai layanan backend yang efisien,
          mengoptimalkan kinerja sistem, serta memastikan komunikasi antar microservices berjalan
          lancar melalui protokol gRPC. Aku juga memiliki pengalaman dalam mengelola database,
          menerapkan autentikasi, dan merancang API yang aman dan scalable.
        </p>
        <p class="lead">
          Tujuanku adalah terus mengembangkan keahlian di bidang backend development, mempelajari
          teknologi baru, dan berkontribusi pada pengembangan sistem yang andal, cepat, dan mudah digunakan.
        </p>

        <SocialLinks :links="social" />
      </section>
    </div>
  </div>
</template>

<script setup>
import SocialLinks from '@/components/SocialLinks.vue'
import { DotLottieVue } from '@lottiefiles/dotlottie-vue'

const social = {
  instagram: 'https://instagram.com/username_kamu',
  facebook:  'https://facebook.com/username_kamu',
  linkedin:  'https://www.linkedin.com/in/username-kamu/',
  github:    'https://github.com/username_kamu',
}
</script>


<style lang="scss" scoped>
@use "@/assets/styles/variables" as *;

/* wrapper halaman */
.about{
  position: relative;
  min-height: 100vh;
  background: $default-section-background;
  overflow: hidden; /* supaya animasi tak bikin scroll horizontal */
}

/* Lottie background di kanan */
.bg-lottie{
  position: fixed;
  left: 50%;
  top: 8vh;                       /* geser vertical dari atas; ubah sesuai selera */
  transform: translateX(-50%);    /* center horizontal */
  width: clamp(900px, 90vw, 1700px); /* PERBESAR: min 900px, bisa hingga 1700px */
  height: auto;
  opacity: .22;                   /* transparansi; bisa 0.18–0.28 */
  pointer-events: none;           /* biar ga ganggu klik */
  z-index: 0;                     /* di belakang konten */
}

.content{
  position: relative;
  z-index: 1;                 /* di atas animasi */
  padding: fluid(32px, 80px) fluid(16px, 60px);
  max-width: min(1500px, 92vw);
  margin-top: clamp(250px, 12vh, 250px);
}

/* judul di tengah & besar */
.title{
  font-size: fluid(36px, 72px);
  line-height: 1.1;
  letter-spacing: .5px;
  margin: 0 0 fluid(12px, 18px);
  color: $text-default-color;
  text-align: center;
}
.accent{ color: $primary; }

/* meta dan paragraf */
.meta{
  display:flex; flex-wrap:wrap; gap:10px 14px; align-items:center;
  justify-content:center;              /* center juga */
  font-size: fluid(14px, 18px);
  color:$light-7; margin-bottom: fluid(16px, 28px);
  text-align:center;
}
.lead{
  color: shade($text-default-color, 15%);
  font-size: fluid(14px, 18px);
  line-height: 1.7;
  max-width: 3400px;
  margin: 0 auto fluid(10px, 16px);    /* center paragraf */
}
</style>


  
  