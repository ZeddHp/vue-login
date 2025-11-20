<script setup>
import { ref, onMounted } from "vue";
import HeaderComponent from "./components/HeaderComponent.vue";
import SideNavComponent from "./components/SideNavComponent.vue";
import LoginComponent from "./components/LoginComponent.vue";
import HomeComponent from "./components/HomeComponent.vue";
import AboutMeComponent from "./components/AboutMeComponent.vue";
import ParticlesBackground from "./components/ParticlesBackground.vue";

// Student credentials - hardcoded
const STUDENT_EMAIL = "valtersbernhards.jargans@va.lv";
const STUDENT_ID = "IT22082";
const STUDENT_NAME = "Valters Bernhards Jargans";

// App state
const isSignedIn = ref(false);
const currentView = ref("Home");

// 7.2 State restored - Load persisted state on mount
onMounted(() => {
  const savedState = localStorage.getItem("loginState");
  if (savedState) {
    const state = JSON.parse(savedState);
    isSignedIn.value = state.isSignedIn;
    currentView.value = state.currentView;
    console.log("7.2 State restored");
  }
  console.log("1.1 Components initialized");
});

// Handle successful login
const handleLogin = (credentials) => {
  if (credentials.email === STUDENT_EMAIL && credentials.password === STUDENT_ID) {
    isSignedIn.value = true;
    currentView.value = "Home";

    // 7.1 State persisted - Save to localStorage
    localStorage.setItem("loginState", JSON.stringify({
      isSignedIn: true,
      currentView: "Home"
    }));
    console.log("7.1 State persisted");
    console.log("2.4 Login success");
    console.log("3.1 Header updated for signed-in state");
    console.log("3.2 SideNav rendered");
    console.log("3.3 Default view: Home");
  }
};

// Handle logout
const handleLogout = () => {
  isSignedIn.value = false;
  currentView.value = "Home";

  // Clear persisted state
  localStorage.removeItem("loginState");

  console.log("6.1 Logout");
};

// Handle navigation
const handleNavigate = (view) => {
  currentView.value = view;

  // Update persisted state
  localStorage.setItem("loginState", JSON.stringify({
    isSignedIn: isSignedIn.value,
    currentView: view
  }));

  if (view === "Home") {
    console.log("4.1 Navigate: Home");
  } else if (view === "AboutMe") {
    console.log("4.2 Navigate: AboutMe");
  }
};
</script>

<template>
  <div id="app">
    <ParticlesBackground />
    <div class="animated-bg"></div>

    <HeaderComponent :isSignedIn="isSignedIn" @logout="handleLogout" />

    <div class="main-container">
      <SideNavComponent v-if="isSignedIn" :currentView="currentView" @navigate="handleNavigate" />

      <div class="content">
        <LoginComponent v-if="!isSignedIn" :studentEmail="STUDENT_EMAIL" :studentId="STUDENT_ID" @login="handleLogin" />

        <HomeComponent v-if="isSignedIn && currentView === 'Home'" />

        <AboutMeComponent v-if="isSignedIn && currentView === 'AboutMe'" :name="STUDENT_NAME" :email="STUDENT_EMAIL"
          :studentId="STUDENT_ID" />
      </div>
    </div>
  </div>
</template>

<style>
#app {
  min-height: 100vh;
  display: flex;
  flex-direction: column;
  position: relative;
  overflow: hidden;
}

.animated-bg {
  position: fixed;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
  background: linear-gradient(135deg, #667eea, #764ba2, #f093fb, #4facfe);
  background-size: 400% 400%;
  animation: gradientShift 15s ease infinite;
  opacity: 0.15;
  z-index: 0;
}

@keyframes gradientShift {
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

.main-container {
  flex: 1;
  display: flex;
  position: relative;
  z-index: 2;
}

.content {
  flex: 1;
  overflow-y: auto;
  position: relative;
  z-index: 2;
}
</style>
