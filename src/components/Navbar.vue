<template>
  <!-- ===== Desktop (unchanged) ===== -->
  <header class="navbar">
    <nav class="navbar-container">
      <!-- Logo -->
      <a class="brand" href="/" aria-label="Homepage">
        <slot name="logo">
          <img :src="logoSrc" alt="Gravix Logo" class="brand-logo" />
        </slot>
      </a>

      <!-- Links -->
      <ul class="nav-links">
        <li v-for="(link, index) in links" :key="index">
          <a :href="link.href" class="nav-link">{{ link.label }}</a>
        </li>
      </ul>

      <!-- CTA -->
      <a v-if="cta" :href="cta.href" class="cta-btn">
        {{ cta.label }}
      </a>
    </nav>
  </header>

  <!-- ===== Mobile pill (NEW — only shows ≤ 768px) ===== -->
  <nav class="mobile-nav" aria-label="Mobile">
    <div class="pill">
      <!-- Left: brand/logo -->
      <a class="pill-brand" href="/" aria-label="Homepage">
        <img v-if="logoSrc" :src="logoSrc" alt="Gravix Logo" class="pill-logo" />
        <span v-else class="pill-text">GRAVIX</span>
      </a>

      <!-- Center: chevron toggle -->
      <button
        class="pill-toggle"
        :aria-expanded="mobileOpen ? 'true' : 'false'"
        aria-controls="m-panel"
        @click="mobileOpen = !mobileOpen"
      >
        <svg class="chevron" viewBox="0 0 24 24" width="18" height="18" fill="none" stroke="currentColor" stroke-width="2">
          <path d="M6 9l6 6 6-6" />
        </svg>
      </button>

      <!-- Right: round gradient CTA -->
      <a
        v-if="cta"
        :href="cta.href"
        class="pill-cta"
        aria-label="Contact"
      >
        <!-- phone icon by default -->
        <svg viewBox="0 0 24 24" width="16" height="16" fill="none" stroke="white" stroke-width="2" stroke-linecap="round" stroke-linejoin="round">
          <path d="M22 16.92v3a2 2 0 0 1-2.18 2 19.8 19.8 0 0 1-8.63-3.07 19.5 19.5 0 0 1-6-6 19.8 19.8 0 0 1-3.07-8.67A2 2 0 0 1 4.11 2h3a2 2 0 0 1 2 1.72c.12.89.32 1.76.6 2.6a2 2 0 0 1-.45 2.11L8 9a16 16 0 0 0 7 7l.57-1.25a2 2 0 0 1 2.11-.45c.84.28 1.71.48 2.6.6A2 2 0 0 1 22 16.92z"/>
        </svg>
      </a>
    </div>

    <!-- Dropdown -->
    <transition name="fade">
      <div
        v-if="mobileOpen"
        class="m-panel"
        id="m-panel"
        @click.self="mobileOpen = false"
      >
        <ul class="m-list">
          <li v-for="(link, i) in links" :key="i">
            <a :href="link.href" class="m-item" @click="mobileOpen = false">
              {{ link.label }}
            </a>
          </li>
        </ul>
      </div>
    </transition>
  </nav>
</template>

<script setup>
import { ref } from 'vue'

defineProps({
  links: { type: Array, default: () => [] },
  cta: { type: Object, default: null },
  logoSrc: { type: String, default: '' }
})

const mobileOpen = ref(false)
</script>

<style scoped>
/* ===========================
   DESKTOP (your original)
   =========================== */

/* Navbar wrapper fixed height */
.navbar {
  background: rgba(0, 0, 0, 0.9);
  backdrop-filter: blur(8px);
  height: 90px; /* Fixed navbar height */
  display: flex;
  align-items: center;
  padding: 0 2.5rem;
  position: fixed;
  top: 0;
  width: 100%;
  z-index: 50;
}

/* Container for flex layout */
.navbar-container {
  display: flex;
  align-items: center;
  justify-content: space-between;
  width: 100%;
  max-width: 1440px;
  margin: 0 auto;
}

/* Logo bigger without affecting navbar height */
.brand-logo {
  height: 120px;       /* bigger than navbar height */
  max-width: 250px;    /* responsive max width */
  object-fit: contain;
  transform: translateY(-10px); /* center vertically overflow */
}

/* Links */
.nav-links {
  display: flex;
  gap: 2rem;
  list-style: none;
}

.nav-link {
  color: #fff;
  text-decoration: none;
  font-size: 1.1rem;
  font-weight: 500;
  transition: color 0.3s ease;
}
.nav-link:hover { color: #e50914; }

/* CTA button */
.cta-btn {
  background: #e50914;
  color: #fff;
  padding: 0.7rem 1.5rem;
  border-radius: 999px;
  font-size: 1rem;
  font-weight: 600;
  transition: background 0.3s ease;
}
.cta-btn:hover { background: #b20710; }

/* Keep your desktop behavior unchanged on large screens */
@media (min-width: 769px) {
  .mobile-nav { display: none; }
}

/* ===========================
   MOBILE-ONLY PILL NAV
   =========================== */

.mobile-nav {
  display: none;
  position: sticky;
  top: 0; /* FIXED: remove gap at top */
  z-index: 60;
  padding-inline: 12px;
}


/* pill container */
.pill {
  display: grid;
  grid-template-columns: 1fr auto 1fr; /* brand | chevron | cta */
  align-items: center;

  width: min(92vw, 360px);
  height: 48px;
  margin: 0 auto;
  padding: 0 8px;

  background: rgba(24,24,27,0.82);
  -webkit-backdrop-filter: blur(8px);
  backdrop-filter: blur(8px);
  border: 1px solid rgba(255,255,255,0.12);
  border-radius: 9999px;
  box-shadow: 0 8px 40px -12px rgba(0,0,0,.6);
}

/* left brand */
.pill-brand {
  display: inline-flex;
  align-items: center;
  gap: 8px;
  text-decoration: none;
  padding-left: 8px;
}
.pill-logo { height: 22px; object-fit: contain; }
.pill-text { color: #fff; font-weight: 900; letter-spacing: .06em; }

/* middle chevron */
.pill-toggle {
  display: inline-grid;
  place-items: center;
  width: 36px; height: 36px;
  border: 0; border-radius: 999px;
  background: transparent;
  color: #c9c9d1;
}
.pill-toggle:active { transform: scale(0.98); }
.chevron { opacity: .9; }

/* right round CTA */
.pill-cta {
  justify-self: end;
  display: inline-grid;
  place-items: center;
  width: 34px; height: 34px;
  border-radius: 9999px;
  background: radial-gradient(90% 90% at 30% 20%, #7c3aed, #a21caf);
  box-shadow: 0 8px 18px -8px rgba(124,58,237,.9);
}

/* dropdown panel */
.m-panel {
  margin: 8px auto 0;
  width: min(92vw, 360px);
  background: rgba(24,24,27,0.92);
  -webkit-backdrop-filter: blur(8px);
  backdrop-filter: blur(8px);
  border: 1px solid rgba(255,255,255,0.12);
  border-radius: 16px;
  box-shadow: 0 8px 40px -12px rgba(0,0,0,.6);
  overflow: hidden;
}

.m-list {
  list-style: none;
  margin: 0; padding: 6px;
  display: grid;
}
.m-item {
  display: block;
  padding: 12px 10px;
  color: #d4d4d8;
  text-decoration: none;
  border-radius: 10px;
}
.m-item:hover { background: rgba(255,255,255,.06); color: #fff; }

/* fade transition */
.fade-enter-active, .fade-leave-active { transition: opacity .15s ease; }
.fade-enter-from, .fade-leave-to { opacity: 0; }

/* show mobile pill, hide your desktop navbar on small screens */
@media (max-width: 768px) {
  .navbar { display: none; }     /* HIDE your original bar */
  .mobile-nav { display: block; }/* SHOW pill */
}
</style>
