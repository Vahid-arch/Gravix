<template>
  <section class="hero" :style="{ backgroundColor: bgColor }">
    <div class="container">
      <h1 id="hero-title" class="headline">
        <span class="line1">{{ line1 }}</span>
        <span class="line2">{{ line2 }}</span>
      </h1>

      <div class="actions">
        <a class="ghost" href="#services">Explore Services</a>
      </div>

      <!-- Scroll down arrow -->
      <div class="scroll-down" @click="scrollToDetails">
        <span></span>
        <span></span>
        <span></span>
      </div>
    </div>
  </section>
</template>

<script setup>
const props = defineProps({
  line1: { type: String, default: 'GRAVIX' },
  line2: { type: String, default: '.IN' },
  bgColor: { type: String, default: '#000000' }
})

const scrollToDetails = () => {
  const el = document.querySelector('.details')
  if (el) el.scrollIntoView({ behavior: 'smooth' })
}
</script>

<style scoped>
.hero {
  position: relative;
  min-height: 80vh; /* slightly less than 100vh to reduce gap */
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: center;
  text-align: center;
  color: #fff;
}

/* Headline */
.headline {
  font-weight: 900;
  font-size: clamp(48px, 10vw, 10rem);
  line-height: 0.85;
}
.headline .line1 { 
  display: block; opacity: 0; transform: translateY(50px);
  animation: slideUp 1s ease-out forwards;
}
.headline .line2 { 
  display: block; color: #ff0000; margin-top: 0.25em;
  opacity: 0; transform: translateY(50px);
  animation: slideUp 1s ease-out forwards; animation-delay: 0.3s;
}

/* Actions */
.actions { margin-top: 24px; }
.ghost {
  color: #d4d4d8; text-decoration: none; font-size: 0.95rem;
  border: 1px solid rgba(255,255,255,0.15);
  background: rgba(255,255,255,0.06); padding: 10px 16px;
  border-radius: 9999px; transition: all 0.2s ease;
}
.ghost:hover { background: rgba(255,255,255,0.12); color: #fff; }

/* Scroll down arrow */
.scroll-down {
  margin-top: 40px;
  display: flex;
  flex-direction: column;
  align-items: center;
  cursor: pointer;
}
.scroll-down span {
  display: block; width: 8px; height: 8px;
  border-bottom: 2px solid #fff; border-right: 2px solid #fff;
  transform: rotate(45deg); margin: 4px; animation: bounce 1.5s infinite;
}
.scroll-down span:nth-child(2) { animation-delay: 0.2s; }
.scroll-down span:nth-child(3) { animation-delay: 0.4s; }

@keyframes bounce {
  0%,20%,50%,80%,100% { transform: rotate(45deg) translateY(0); }
  40% { transform: rotate(45deg) translateY(8px); }
  60% { transform: rotate(45deg) translateY(4px); }
}

@keyframes slideUp {
  0% { opacity: 0; transform: translateY(50px); }
  100% { opacity: 1; transform: translateY(0); }
}

/* Reduce Hero height on mobile for seamless gap */
@media (max-width: 640px) {
  .hero {
    min-height: calc(70vh - 48px); /* account for mobile navbar height */
    padding-top: 48px;             /* push content below navbar */
  }
}
</style>
