<template>
  <section class="details">
    <div class="container">
      <h2 class="title">Why Choose Gravix?</h2>
      <p class="description">
        We craft innovative designs, execute data-driven marketing strategies, and build
        high-performing websites — all engineered for seamless user experiences.
        Our dedicated project managers ensure flawless delivery, while advanced AI solutions
        empower your business to reach its full potential — efficiently and affordably.
      </p>

      <div class="grid-wrapper">
        <div class="grid">
          <div class="card" v-for="(item, i) in features" :key="i">
            <h3>{{ item.title }}</h3>
            <p>{{ item.text }}</p>
          </div>
        </div>
      </div>

      <!-- Scroll down arrow to connection section -->
      <div class="scroll-down" @click="scrollToConnection">
        <span></span>
        <span></span>
        <span></span>
      </div>
    </div>
  </section>
</template>

<script setup>
const features = [
  { title: 'Creative Design', text: 'Modern, user-focused designs that captivate and convert.' },
  { title: 'Strategic Marketing', text: 'Data-driven campaigns to maximize your reach and ROI.' },
  { title: 'High-Performance Websites', text: 'Fast, responsive, and optimized for conversions.' },
  { title: 'AI-Powered Solutions', text: 'Cutting-edge automation to unlock new growth.' }
]

const scrollToConnection = () => {
  const el = document.querySelector('.connection-section')
  if (el) el.scrollIntoView({ behavior: 'smooth' })
}
</script>

<style scoped>
.details {
  background: #000;
  color: #fff;
  padding: 60px 16px;
}

.container {
  max-width: 1120px;
  margin: 0 auto;
  text-align: center;
}
.title {
  font-size: clamp(28px, 4vw, 40px);
  font-weight: 800;
  margin-bottom: 16px;
}

.description {
  max-width: 720px;
  margin: 0 auto 48px;
  font-size: 1.1rem;
  color: #d4d4d8;
  line-height: 1.6;
}
@media (max-width: 640px) {
  .description {
    display: none;
    margin-bottom: 24px; /* smaller gap for mobile */
  }
}

.grid-wrapper {
  overflow-x: auto;
  padding-bottom: 16px;
  -webkit-overflow-scrolling: touch;
}

.grid {
  display: grid;
  gap: 24px;
  grid-template-columns: repeat(auto-fit, minmax(240px, 1fr));
}

@media (max-width: 640px) {
  .grid {
    display: flex;
    flex-wrap: nowrap;
    gap: 16px; /* smaller gap on mobile like desktop */
  }
  .card {
    flex: 0 0 75%;
    scroll-snap-align: start;
  }
}

.card {
  background: rgba(255,255,255,0.05);
  border: 1px solid rgba(255,255,255,0.1);
  border-radius: 12px;
  padding: 24px;
  text-align: left;
  transition: background .3s ease;
}
.card:hover {
  background: rgba(255,255,255,0.08);
}
.card h3 {
  font-size: 1.2rem;
  margin-bottom: 8px;
}
.card p {
  font-size: 0.95rem;
  color: #a1a1aa;
}

.grid-wrapper::-webkit-scrollbar {
  display: none;
}
.grid-wrapper {
  scroll-snap-type: x mandatory;
  -webkit-overflow-scrolling: touch;
}

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
</style>
