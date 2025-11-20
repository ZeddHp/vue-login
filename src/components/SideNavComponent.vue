<script setup>
import { onMounted } from "vue";

const props = defineProps({
  currentView: {
    type: String,
    required: true
  }
});

const emit = defineEmits(["navigate"]);

onMounted(() => {
  console.log("1.3 SideNav ready");
});

const handleNavigate = (view) => {
  emit("navigate", view);
};
</script>

<template>
  <nav class="sidenav">
    <div class="nav-header">
      <h3>Navigation</h3>
    </div>
    <ul>
      <li
        :class="{ active: currentView === 'Home' }"
        @click="handleNavigate('Home')"
      >
        <span class="icon">🏠</span>
        <span class="label">Home</span>
      </li>
      <li
        :class="{ active: currentView === 'AboutMe' }"
        @click="handleNavigate('AboutMe')"
      >
        <span class="icon">👤</span>
        <span class="label">About Me</span>
      </li>
    </ul>
  </nav>
</template>

<style scoped>
.sidenav {
  width: 260px;
  background: var(--white);
  border-right: none;
  padding: 2rem 0;
  box-shadow: 2px 0 20px var(--shadow);
  animation: slideRight 0.5s ease-out;
}

@keyframes slideRight {
  from {
    opacity: 0;
    transform: translateX(-20px);
  }
  to {
    opacity: 1;
    transform: translateX(0);
  }
}

.nav-header {
  padding: 0 1.5rem 1.5rem 1.5rem;
  border-bottom: 2px solid var(--light);
  margin-bottom: 1rem;
}

.nav-header h3 {
  font-size: 0.85rem;
  font-weight: 700;
  text-transform: uppercase;
  letter-spacing: 1.5px;
  color: #999;
  margin: 0;
}

ul {
  list-style: none;
  padding: 0;
  margin: 0;
}

li {
  padding: 1rem 1.5rem;
  margin: 0.5rem 1rem;
  cursor: pointer;
  transition: all 0.3s cubic-bezier(0.4, 0, 0.2, 1);
  border-radius: 12px;
  display: flex;
  align-items: center;
  gap: 1rem;
  position: relative;
  overflow: hidden;
}

li::before {
  content: '';
  position: absolute;
  left: 0;
  top: 0;
  height: 100%;
  width: 4px;
  background: var(--primary-gradient);
  transform: scaleY(0);
  transition: transform 0.3s ease;
}

li:hover {
  background: var(--light);
  transform: translateX(5px);
}

li.active {
  background: linear-gradient(135deg, #667eea 0%, #764ba2 50%, #f093fb 100%);
  background-size: 200% 200%;
  animation: navGradient 5s ease infinite;
  color: var(--white);
  font-weight: 600;
  box-shadow: 0 4px 15px rgba(102, 126, 234, 0.3), 0 0 20px rgba(102, 126, 234, 0.2);
  transform: translateX(5px);
}

@keyframes navGradient {
  0%, 100% {
    background-position: 0% 50%;
  }
  50% {
    background-position: 100% 50%;
  }
}

li.active::before {
  transform: scaleY(1);
}

.icon {
  font-size: 1.25rem;
  display: flex;
  align-items: center;
  justify-content: center;
  transition: transform 0.3s ease;
}

li:hover .icon,
li.active .icon {
  transform: scale(1.1);
}

.label {
  font-size: 1rem;
  font-weight: 500;
  letter-spacing: 0.3px;
}
</style>
