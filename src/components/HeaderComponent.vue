<script setup>
import { onMounted } from "vue";

const props = defineProps({
  isSignedIn: {
    type: Boolean,
    required: true
  }
});

const emit = defineEmits(["logout"]);

onMounted(() => {
  console.log("1.2 Header ready");
});

const handleLogout = () => {
  emit("logout");
};
</script>

<template>
  <header :class="{ 'signed-in': isSignedIn }">
    <div class="header-content">
      <div class="logo">LOGO</div>
      <button
        v-if="isSignedIn"
        @click="handleLogout"
        class="logout-btn"
      >
        Logout
      </button>
    </div>
  </header>
</template>

<style scoped>
header {
  background: var(--white);
  padding: 1.25rem 2.5rem;
  box-shadow: 0 2px 20px var(--shadow);
  backdrop-filter: blur(10px);
  transition: all 0.4s cubic-bezier(0.4, 0, 0.2, 1);
  position: relative;
  z-index: 100;
}

header.signed-in {
  background: linear-gradient(135deg, #667eea 0%, #764ba2 50%, #f093fb 100%);
  background-size: 200% 200%;
  animation: headerGradient 8s ease infinite;
  box-shadow: 0 4px 30px rgba(102, 126, 234, 0.3);
}

@keyframes headerGradient {
  0% {
    background-position: 0% 50%;
  }
  50% {
    background-position: 100% 50%;
  }
  100% {
    background-position: 0% 50%;
  }
}

.header-content {
  display: flex;
  justify-content: space-between;
  align-items: center;
  max-width: 1400px;
  margin: 0 auto;
}

.logo {
  font-size: 1.75rem;
  font-weight: 800;
  letter-spacing: -0.5px;
  color: var(--dark);
  text-transform: uppercase;
  position: relative;
  transition: all 0.3s ease;
}

.logo::after {
  content: '';
  position: absolute;
  bottom: -4px;
  left: 0;
  width: 0;
  height: 3px;
  background: var(--secondary-gradient);
  transition: width 0.3s ease;
}

.logo:hover::after {
  width: 100%;
}

header.signed-in .logo {
  color: var(--white);
  text-shadow: 0 2px 10px rgba(0, 0, 0, 0.2);
}

.logout-btn {
  padding: 0.75rem 1.75rem;
  background: var(--white);
  color: var(--dark);
  border: none;
  border-radius: 50px;
  cursor: pointer;
  font-size: 0.95rem;
  font-weight: 600;
  transition: all 0.3s cubic-bezier(0.4, 0, 0.2, 1);
  box-shadow: 0 4px 15px rgba(0, 0, 0, 0.1);
  text-transform: uppercase;
  letter-spacing: 0.5px;
}

.logout-btn:hover {
  transform: translateY(-2px);
  box-shadow: 0 6px 25px rgba(0, 0, 0, 0.15);
  background: var(--light);
}

.logout-btn:active {
  transform: translateY(0);
}
</style>
