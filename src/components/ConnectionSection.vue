<template>
  <section class="connection-section">
    <div class="text-content">
      <h1 class="title">Take Your Brand to the Next Level With Us</h1>
      <p class="subtitle">Empowering growth through strategic social media marketing</p>
    </div>

    <div class="layout-container">
      <div class="rotating-circles">
        <svg class="connection-lines" xmlns="http://www.w3.org/2000/svg" viewBox="0 0 800 800">
          <circle cx="400" cy="400" r="250" class="connector" />
          <circle cx="400" cy="400" r="180" class="connector" />
          <circle cx="400" cy="400" r="110" class="connector" />
        </svg>
      </div>

      <div class="icon-circle">
        <div
          v-for="(icon, index) in icons"
          :key="index"
          class="icon-wrapper"
          :style="getIconPosition(index, icons.length)"
        >
          <a :href="icon.link" target="_blank">
            <img :src="icon.src" class="icon" />
          </a>
        </div>
      </div>
    </div>
  </section>
</template>

<script setup>
const icons = [
  { src: "/icons/facebook.svg", link: "#" },
  { src: "/icons/instagram.svg", link: "#" },
  { src: "/icons/pintrest.svg", link: "#" },
  { src: "/icons/tiktok.svg", link: "#" },
  { src: "/icons/youtube.svg", link: "#" },
  { src: "/icons/linkedin.svg", link: "#" },
  { src: "/icons/twitter.svg", link: "#" },
  { src: "/icons/messenger.svg", link: "#" },
];

const getIconPosition = (index, total) => {
  const angle = (index / total) * 2 * Math.PI;
  const radius = 250;
  const x = 400 + radius * Math.cos(angle) - 32;
  const y = 400 + radius * Math.sin(angle) - 32;
  return {
    position: 'absolute',
    left: `${x}px`,
    top: `${y}px`,
  };
};
</script>

<style scoped>
.connection-section {
  position: relative;
  background: #000;
  width: 100%;
  height: 100vh;
  overflow: hidden;
}

.text-content {
  position: absolute;
  top: 5%;
  width: 100%;
  text-align: center;
  color: white;
  z-index: 10;
  padding: 0 1rem;
}

.title {
  font-size: clamp(28px, 4vw, 40px);
  font-weight: 800;
  margin-bottom: 16px;
  line-height: 1.2;
  word-break: break-word;
}

.subtitle {
  font-size: 1rem;
  color: #ccc;
}

.layout-container {
  position: absolute;
  top: 50%;
  left: 50%;
  width: 800px;
  height: 800px;
  transform: translate(-50%, -50%);
  z-index: 5;
}

.rotating-circles {
  position: absolute;
  width: 100%;
  height: 100%;
  animation: rotateCircle 20s linear infinite;
  z-index: 1;
}

.connection-lines {
  width: 100%;
  height: 100%;
}

.connector {
  stroke: red;
  stroke-width: 1.5;
  fill: none;
  opacity: 0.5;
}

@keyframes rotateCircle {
  from { transform: rotate(0deg); }
  to { transform: rotate(360deg); }
}

.icon-circle {
  position: absolute;
  width: 100%;
  height: 100%;
  z-index: 5;
}

.icon-wrapper {
  width: 64px;
  height: 64px;
}

.icon {
  width: 100%;
  height: 100%;
  transition: transform 0.3s ease;
}

.icon:hover {
  transform: scale(1.2);
}

@media (max-width: 768px) {
  .layout-container {
    transform: translate(-50%, -50%) scale(0.6); /* slightly larger scale for mobile */
  }

  .icon-wrapper {
    width: 48px;
    height: 48px;
  }

  .subtitle {
    font-size: 0.9rem;
  }
}
</style>
