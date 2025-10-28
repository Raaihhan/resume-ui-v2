<!-- src/pages/Hobbies/index.vue -->
<template>
  <div class="page">
   

    <main class="content">
      <header class="head">
        <h1 class="title"><span class="accent">HOBBIES</span></h1>
        <p class="subtitle">Beberapa kegiatan yang saya nikmati di waktu luang.</p>
      </header>

      <section class="hobby-grid">
        <article
          v-for="(h, i) in hobbies"
          :key="i"
          class="hobby-card"
        >
          <figure class="thumb" @click="preview(h.img, h.title)" title="Klik untuk perbesar">
            <img
              v-if="h.img"
              :src="h.img"
              :alt="h.title"
              @error="(e)=>{ e.target.style.display='none'; e.target.nextElementSibling.style.display='grid' }"
            />
            <div class="ph">
              <span class="emoji">{{ h.emoji }}</span>
            </div>
          </figure>

          <div class="info">
            <h3 class="name">{{ h.title }}</h3>
            <p class="desc">{{ h.desc }}</p>

            <ul class="tags" v-if="h.tags?.length">
              <li v-for="(t, ti) in h.tags" :key="ti">{{ t }}</li>
            </ul>
          </div>
        </article>
      </section>
    </main>

    <!-- Lightbox -->
    <div v-if="viewer.open" class="viewer" @click="closeViewer">
      <div class="viewer-inner" @click.stop>
        <button class="close" @click="closeViewer" aria-label="Close">×</button>
        <img :src="viewer.src" :alt="viewer.title" />
        <div class="cap">{{ viewer.title }}</div>
      </div>
    </div>
  </div>
</template>

<script setup>
import { ref, onMounted, onBeforeUnmount } from 'vue'
import Sidebar from '@/components/Sidebar.vue'
import travel from '@/assets/images/trvl.jpeg'

/**
 * Taruh file gambar di: public/assets/hobbies/
 * Contoh: /assets/hobbies/cycling.jpg
 */
const hobbies = [
  {
    title: 'Jalan Jalan & Traveling',
    img: travel,
    emoji: '👨‍💻',
    tags: ['Jalan', 'Pantai', 'Travel'],
    desc: 'Traveling untuk menghilangkan stress dan mencari inspirasi baru.'
  },
  {
    title: 'Reading Tech & Business',
    img: '/assets/hobbies/reading.jpg',
    emoji: '📚',
    tags: ['books', 'growth'],
    desc: 'Baca buku/artikel tentang sistem terdistribusi & praktik software craft.'
  },
  {
    title: 'Gym & Fitness',
    img: '/assets/hobbies/gym.jpg',
    emoji: '💪',
    tags: ['health', 'discipline'],
    desc: 'Latihan rutin untuk stamina & fokus yang lebih baik saat ngoding.'
  },
  {
    title: 'Cycling',
    img: '/assets/hobbies/cycling.jpg',
    emoji: '🚴‍♂️',
    tags: ['outdoor'],
    desc: 'Gowes santai di weeken; recharge otak sambil cari ide baru'
  },
  {
    title: 'Photography',
    img: '/assets/hobbies/photo.jpg',
    emoji: '📷',
    tags: ['creative'],
    desc: 'Eksplorasi komposisi & cahaya—melatih sense visual buat UI/UX.'
  },
  {
    title: 'Chess',
    img: '/assets/hobbies/chess.jpg',
    emoji: '♟️',
    tags: ['strategy'],
    desc: 'Melatih strategi & pengambilan keputusan—berguna juga saat desain sistem.'
  }
]

const viewer = ref({ open: false, src: '', title: '' })
function preview(src, title) { viewer.value = { open: true, src, title } }
function closeViewer() { viewer.value.open = false }

let escHandler
onMounted(() => {
  escHandler = (e) => { if (e.key === 'Escape') closeViewer() }
  window.addEventListener('keydown', escHandler)
})
onBeforeUnmount(() => {
  if (escHandler) window.removeEventListener('keydown', escHandler)
})
</script>

<style lang="scss" scoped>
@use "@/assets/styles/variables" as *;
@use "sass:color";

/* Layout umum */
.page { display:flex; min-height:100vh; background:$default-section-background; }
.content { flex:1; padding:64px clamp(20px, 5vw, 56px); max-width: 1200px; margin: 0 auto; }

/* Header */
.head { margin-bottom: 18px; }
.title { margin:0 0 6px; color:$text-default-color; font-size: clamp(28px, 4vw, 44px); }
.accent { color:$primary; }
.subtitle { color:$light-7; margin:0; }

/* Grid kartu */
.hobby-grid{
  margin-top: 18px;
  display: grid;
  grid-template-columns: repeat(auto-fill, minmax(260px, 1fr));
  gap: clamp(14px, 2vw, 22px);
}

/* Card */
.hobby-card{
  background: rgba(255,255,255,.6);
  border-radius: 14px;
  overflow: hidden;
  box-shadow: 0 10px 22px rgba(0,0,0,.06);
  transition: transform .18s ease, box-shadow .18s ease;

  &:hover{
    transform: translateY(-2px);
    box-shadow: 0 14px 28px rgba(0,0,0,.08);
  }
}

/* Thumbnail */
.thumb{
  position: relative;
  aspect-ratio: 16/9;
  overflow: hidden;
  cursor: zoom-in;
  background: color.scale($primary, $lightness: 70%);
}
.thumb img{
  width:100%; height:100%; object-fit:cover; display:block;
  transition: transform .3s ease;
}
.thumb:hover img{ transform: scale(1.04); }

/* Placeholder kalau gambar gagal load */
.ph{
  position:absolute; inset:0;
  display:none;                  /* akan di-show lewat @error handler */
  place-items:center;
  font-size: 42px;
  color: color.adjust($primary, $lightness: -5%);
  background: rgba(255,255,255,.55);
}

/* Info */
.info{ padding: 14px 14px 16px; }
.name{ margin:0 0 6px; font-size: 18px; color:$text-default-color; }
.desc{ margin:0 0 10px; color: shade($text-default-color, 18%); line-height: 1.55; }

/* Tags */
.tags{ display:flex; flex-wrap:wrap; gap:8px; margin:0; padding:0; list-style:none; }
.tags li{
  font-size: 12.5px;
  padding: 6px 10px;
  border-radius: 999px;
  background: color.adjust($primary, $lightness: 36%);
  color: $text-default-color;
  font-weight: 600;
}

/* Lightbox */
.viewer{
  position: fixed; inset:0;
  background: rgba(20,15,41,.78);
  display:grid; place-items:center;
  z-index: 9999;
}
.viewer-inner{
  position: relative;
  max-width: min(92vw, 1100px);
  max-height: 86vh;
  display:flex; flex-direction:column; align-items:center;
}
.viewer-inner img{
  max-width: 100%;
  max-height: 80vh;
  border-radius: 12px;
  box-shadow: 0 14px 28px rgba(0,0,0,.35);
}
.cap{
  margin-top: 10px; color:#fff; text-align:center; font-weight:600;
}
.close{
  position:absolute; top:-10px; right:-10px;
  width: 36px; height:36px; border-radius:50%;
  border:none; cursor:pointer;
  background:#fff; color:$text-default-color; font-size:20px; line-height:1;
  box-shadow: 0 6px 16px rgba(0,0,0,.25);
}
</style>
