<template>
  <main>
    <Navbar
  :links="[
    { label: 'Services', href: '#services' },
    { label: 'Works',    href: '#works' },
    { label: 'Pricing',  href: '#pricing' },
    { label: 'Blogs',    href: '#blogs' }
  ]"
  :cta="{ label: `Let's Talk`, href: '#contact' }"
  logoSrc="/images/logo.png"
    />

    <Hero
      line1="GRAVIX"
      line2=".IN"
      bgColor="#000000"
    />
    <DetailsSection
      title="Why Choose Gravix?"
      description="We combine creativity, strategy, and technology to deliver exceptional results for your business. Our team is dedicated to pushing boundaries and driving growth through innovative solutions."
    />
    <ConnectionSection
      title="Connect with Us"
      description="Ready to elevate your business? Let's discuss how we can help you achieve your goals. Contact us today to get started."
    />
  </main>
</template>

<script setup>
import Navbar from '@/components/Navbar.vue'
import Hero from '@/components/Hero.vue'
import DetailsSection from './components/DetailsSection.vue';
import ConnectionSection from './components/ConnectionSection.vue';
</script>

<style>
html, body, #app { height: 100%; background: #000; margin: 0; font-family: 'Inter', sans-serif; }
</style>
