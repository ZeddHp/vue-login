<script setup>
import { onMounted } from "vue";

const props = defineProps({
  name: {
    type: String,
    required: true
  },
  email: {
    type: String,
    required: true
  },
  studentId: {
    type: String,
    required: true
  }
});

onMounted(() => {
  console.log("5.2 AboutMe rendered");
});
</script>

<template>
  <div class="about-me-container">
    <div class="about-me">
      <div class="profile-header">
        <div class="avatar-container">
          <div class="avatar">
            <span class="avatar-icon">👤</span>
            <img class="avatar-img" src="/KL1F3957-Edit1.jpg" alt="Profile Picture" />
          </div>
          <p class="hover-hint">Hover to reveal photo</p>
        </div>
        <h2>Profile Information</h2>
        <p class="subtitle">Your personal details</p>
      </div>

      <div class="info-grid">
        <div class="info-card">
          <div class="card-icon">📝</div>
          <div class="card-content">
            <span class="label">Name</span>
            <span class="value">{{ name }}</span>
          </div>
        </div>

        <div class="info-card">
          <div class="card-icon">📧</div>
          <div class="card-content">
            <span class="label">Student Email</span>
            <span class="value">{{ email }}</span>
          </div>
        </div>

        <div class="info-card">
          <div class="card-icon">🎓</div>
          <div class="card-content">
            <span class="label">Student ID</span>
            <span class="value">{{ studentId }}</span>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<style scoped>
.about-me-container {
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

.about-me {
  max-width: 800px;
  margin: 0 auto;
}

.profile-header {
  text-align: center;
  margin-bottom: 3rem;
  animation: slideDown 0.6s ease-out;
}

@keyframes slideDown {
  from {
    opacity: 0;
    transform: translateY(-20px);
  }
  to {
    opacity: 1;
    transform: translateY(0);
  }
}

.avatar-container {
  perspective: 1000px;
  width: 200px;
  height: 200px;
  margin: 0 auto 2rem;
  position: relative;
}

.avatar-container::before {
  content: '';
  position: absolute;
  inset: -8px;
  border-radius: 50%;
  background: linear-gradient(45deg, #667eea, #764ba2, #f093fb, #4facfe);
  background-size: 300% 300%;
  animation: avatarGradient 8s ease infinite;
  opacity: 0.4;
  filter: blur(20px);
  z-index: -1;
  transition: all 0.8s cubic-bezier(0.4, 0, 0.2, 1);
}

.avatar-container:hover::before {
  inset: -15px;
  opacity: 0.7;
  filter: blur(30px);
}

.avatar {
  width: 100%;
  height: 100%;
  position: relative;
  border-radius: 50%;
  display: flex;
  align-items: center;
  justify-content: center;
  background: linear-gradient(135deg, #667eea, #764ba2, #f093fb, #4facfe);
  background-size: 300% 300%;
  animation: pulse 2s ease-in-out infinite, avatarGradient 8s ease infinite;
  cursor: pointer;
  filter: drop-shadow(0 10px 30px rgba(102, 126, 234, 0.3));
  box-shadow: 0 10px 40px rgba(102, 126, 234, 0.3), 0 0 60px rgba(240, 147, 251, 0.3);
  transition: all 0.8s cubic-bezier(0.4, 0, 0.2, 1);
  overflow: hidden;
}

.avatar-container:hover .avatar {
  transform: scale(1.05);
  animation: none;
  filter: drop-shadow(0 15px 50px rgba(102, 126, 234, 0.5));
  background: var(--white);
}

.hover-hint {
  text-align: center;
  font-size: 0.85rem;
  color: #999;
  margin-top: 0.75rem;
  font-style: italic;
  opacity: 0.7;
  transition: opacity 0.3s ease;
}

.avatar-container:hover .hover-hint {
  opacity: 0;
}

@keyframes avatarGradient {
  0% {
    background-position: 0% 50%;
  }
  25% {
    background-position: 50% 100%;
  }
  50% {
    background-position: 100% 50%;
  }
  75% {
    background-position: 50% 0%;
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

.avatar-icon {
  font-size: 6rem;
  filter: drop-shadow(0 2px 4px rgba(0, 0, 0, 0.2));
  position: absolute;
  z-index: 2;
  opacity: 1;
  transition: all 0.8s cubic-bezier(0.4, 0, 0.2, 1);
  transform: rotateY(0deg) scale(1);
}

.avatar-container:hover .avatar-icon {
  opacity: 0;
  transform: rotateY(180deg) scale(0);
}

.avatar-img {
  position: absolute;
  width: 100%;
  height: 100%;
  object-fit: cover;
  border-radius: 50%;
  opacity: 0;
  transform: rotateY(-180deg) scale(0);
  transition: all 0.8s cubic-bezier(0.4, 0, 0.2, 1);
  z-index: 1;
}

.avatar-container:hover .avatar-img {
  opacity: 1;
  transform: rotateY(0deg) scale(1);
}

h2 {
  font-size: 2.5rem;
  font-weight: 800;
  margin: 0 0 0.5rem 0;
  background: var(--primary-gradient);
  -webkit-background-clip: text;
  -webkit-text-fill-color: transparent;
  background-clip: text;
}

.subtitle {
  font-size: 1.1rem;
  color: #666;
  margin: 0;
}

.info-grid {
  display: grid;
  grid-template-columns: 1fr;
  gap: 1.5rem;
}

.info-card {
  background: var(--white);
  padding: 2rem;
  border-radius: 20px;
  box-shadow: 0 10px 30px var(--shadow);
  display: flex;
  align-items: center;
  gap: 1.5rem;
  transition: all 0.3s cubic-bezier(0.4, 0, 0.2, 1);
  animation: slideUp 0.6s ease-out backwards;
}

.info-card:nth-child(1) {
  animation-delay: 0.1s;
}

.info-card:nth-child(2) {
  animation-delay: 0.2s;
}

.info-card:nth-child(3) {
  animation-delay: 0.3s;
}

@keyframes slideUp {
  from {
    opacity: 0;
    transform: translateY(20px);
  }
  to {
    opacity: 1;
    transform: translateY(0);
  }
}

.info-card:hover {
  transform: translateY(-5px);
  box-shadow: 0 15px 40px var(--shadow-lg);
}

.card-icon {
  width: 60px;
  height: 60px;
  background: linear-gradient(135deg, #4facfe 0%, #00f2fe 50%, #667eea 100%);
  background-size: 200% 200%;
  animation: iconGradient 4s ease infinite;
  border-radius: 16px;
  display: flex;
  align-items: center;
  justify-content: center;
  font-size: 1.75rem;
  flex-shrink: 0;
  box-shadow: 0 5px 15px rgba(79, 172, 254, 0.3);
  transition: all 0.3s ease;
}

@keyframes iconGradient {
  0%, 100% {
    background-position: 0% 50%;
  }
  50% {
    background-position: 100% 50%;
  }
}

.info-card:hover .card-icon {
  transform: scale(1.1) rotate(5deg);
  box-shadow: 0 8px 25px rgba(79, 172, 254, 0.5);
}

.card-content {
  flex: 1;
  display: flex;
  flex-direction: column;
  gap: 0.5rem;
}

.label {
  font-size: 0.85rem;
  font-weight: 700;
  text-transform: uppercase;
  letter-spacing: 1px;
  color: #999;
}

.value {
  font-size: 1.25rem;
  font-weight: 600;
  color: var(--dark);
  word-break: break-word;
}

@media (max-width: 768px) {
  .info-card {
    flex-direction: column;
    text-align: center;
  }

  .card-content {
    align-items: center;
  }
}
</style>
