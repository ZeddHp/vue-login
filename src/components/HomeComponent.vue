<script setup>
import { onMounted } from "vue";

onMounted(() => {
  console.log("5.1 Home rendered");
});
</script>

<template>
  <div class="home">
    <div class="welcome-card">
      <div class="icon-circle">
        <span class="home-icon">🏠</span>
      </div>
      <h1>HOME</h1>
      <p class="subtitle">Welcome to your dashboard</p>
      <div class="decorative-line"></div>
    </div>
  </div>
</template>

<style scoped>
.home {
  display: flex;
  justify-content: center;
  align-items: center;
  min-height: 500px;
  padding: 2rem;
  animation: fadeIn 0.8s ease-out;
}

@keyframes fadeIn {
  from {
    opacity: 0;
  }
  to {
    opacity: 1;
  }
}

.welcome-card {
  text-align: center;
  padding: 4rem 3rem;
  background: var(--white);
  border-radius: 24px;
  box-shadow: 0 20px 60px var(--shadow-lg);
  max-width: 600px;
  width: 100%;
  animation: scaleUp 0.6s cubic-bezier(0.4, 0, 0.2, 1);
  position: relative;
  overflow: hidden;
}

.welcome-card::before {
  content: '';
  position: absolute;
  top: 0;
  left: -100%;
  width: 100%;
  height: 100%;
  background: linear-gradient(90deg, transparent, rgba(255, 255, 255, 0.8), transparent);
  animation: shimmer 3s infinite;
}

@keyframes shimmer {
  0% {
    left: -100%;
  }
  100% {
    left: 100%;
  }
}

@keyframes scaleUp {
  from {
    opacity: 0;
    transform: scale(0.9);
  }
  to {
    opacity: 1;
    transform: scale(1);
  }
}

.icon-circle {
  width: 100px;
  height: 100px;
  margin: 0 auto 2rem;
  background: linear-gradient(135deg, #667eea, #764ba2, #f093fb, #4facfe);
  background-size: 300% 300%;
  animation: pulse 2s ease-in-out infinite, gradientRotate 6s ease infinite;
  border-radius: 50%;
  display: flex;
  align-items: center;
  justify-content: center;
  box-shadow: 0 10px 30px rgba(102, 126, 234, 0.3), 0 0 50px rgba(102, 126, 234, 0.2);
  position: relative;
}

.icon-circle::before {
  content: '';
  position: absolute;
  inset: -3px;
  border-radius: 50%;
  background: linear-gradient(45deg, #667eea, #764ba2, #f093fb, #4facfe);
  background-size: 300% 300%;
  animation: gradientRotate 6s ease infinite;
  opacity: 0.5;
  filter: blur(10px);
  z-index: -1;
}

@keyframes gradientRotate {
  0% {
    background-position: 0% 50%;
  }
  33% {
    background-position: 50% 100%;
  }
  66% {
    background-position: 100% 50%;
  }
  100% {
    background-position: 0% 50%;
  }
}

@keyframes pulse {
  0%, 100% {
    transform: scale(1);
  }
  50% {
    transform: scale(1.05);
  }
}

.home-icon {
  font-size: 3rem;
  filter: drop-shadow(0 2px 4px rgba(0, 0, 0, 0.2));
}

h1 {
  font-size: 4rem;
  font-weight: 900;
  margin: 0 0 1rem 0;
  background: var(--primary-gradient);
  -webkit-background-clip: text;
  -webkit-text-fill-color: transparent;
  background-clip: text;
  letter-spacing: -2px;
}

.subtitle {
  font-size: 1.25rem;
  color: #666;
  margin: 0 0 2rem 0;
  font-weight: 400;
}

.decorative-line {
  width: 80px;
  height: 4px;
  background: linear-gradient(90deg, #f093fb, #f5576c, #f093fb);
  background-size: 200% 100%;
  animation: lineShift 2s ease infinite;
  margin: 0 auto;
  border-radius: 2px;
  box-shadow: 0 0 10px rgba(245, 87, 108, 0.5);
  position: relative;
}

.decorative-line::before,
.decorative-line::after {
  content: '✨';
  position: absolute;
  top: 50%;
  transform: translateY(-50%);
  font-size: 0.8rem;
  animation: sparkle 2s ease infinite;
}

.decorative-line::before {
  left: -25px;
}

.decorative-line::after {
  right: -25px;
  animation-delay: 1s;
}

@keyframes lineShift {
  0%, 100% {
    background-position: 0% 0%;
  }
  50% {
    background-position: 100% 0%;
  }
}

@keyframes sparkle {
  0%, 100% {
    opacity: 0.3;
    transform: translateY(-50%) scale(0.8);
  }
  50% {
    opacity: 1;
    transform: translateY(-50%) scale(1.2);
  }
}
</style>
