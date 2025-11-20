<script setup>
import { onMounted, ref } from "vue";

const particles = ref([]);
const particleCount = 30;

onMounted(() => {
  // Generate random particles
  for (let i = 0; i < particleCount; i++) {
    particles.value.push({
      id: i,
      left: Math.random() * 100,
      top: Math.random() * 100,
      size: Math.random() * 4 + 2,
      duration: Math.random() * 20 + 15,
      delay: Math.random() * 5
    });
  }
});
</script>

<template>
  <div class="particles-container">
    <div
      v-for="particle in particles"
      :key="particle.id"
      class="particle"
      :style="{
        left: particle.left + '%',
        top: particle.top + '%',
        width: particle.size + 'px',
        height: particle.size + 'px',
        animationDuration: particle.duration + 's',
        animationDelay: particle.delay + 's'
      }"
    ></div>
  </div>
</template>

<style scoped>
.particles-container {
  position: fixed;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
  overflow: hidden;
  pointer-events: none;
  z-index: 1;
}

.particle {
  position: absolute;
  background: radial-gradient(circle, rgba(102, 126, 234, 0.8), rgba(118, 75, 162, 0.4));
  border-radius: 50%;
  animation: float infinite ease-in-out;
  opacity: 0;
}

@keyframes float {
  0%, 100% {
    transform: translate(0, 0) scale(1);
    opacity: 0;
  }
  10% {
    opacity: 0.6;
  }
  50% {
    transform: translate(50px, -100px) scale(1.5);
    opacity: 0.8;
  }
  90% {
    opacity: 0.3;
  }
}
</style>
