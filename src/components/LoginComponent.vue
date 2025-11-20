<script setup>
import { ref, computed, watch } from "vue";

const props = defineProps({
  studentEmail: {
    type: String,
    required: true
  },
  studentId: {
    type: String,
    required: true
  }
});

const emit = defineEmits(["login"]);

const email = ref("");
const password = ref("");
const errorMessage = ref("");

// Computed property to check if inputs are valid
const isValid = computed(() => {
  return email.value === props.studentEmail && password.value === props.studentId;
});

// Watch isValid to log button state
watch(isValid, (newValue) => {
  if (!newValue && (email.value || password.value)) {
    console.log("2.3 Login button disabled state reflects validity");
  }
});

const handleSubmit = (event) => {
  event.preventDefault();

  if (isValid.value) {
    emit("login", {
      email: email.value,
      password: password.value
    });
    // Clear form after successful login (handled in parent)
  } else {
    errorMessage.value = "Invalid email or password. Please try again.";
    console.log("2.4 Login failed");
  }
};

// Watch for logout to reset form
const resetForm = () => {
  email.value = "";
  password.value = "";
  errorMessage.value = "";
  console.log("6.2 Login form reset");
};

// Expose reset method for parent
defineExpose({ resetForm });
</script>

<template>
  <div class="login-container">
    <div class="login-box">
      <h2>Sign In</h2>
      <form @submit.prevent="handleSubmit">
        <div class="form-group">
          <label for="email">Email</label>
          <input
            id="email"
            v-model="email"
            type="email"
            placeholder="Enter your email"
            required
          />
        </div>

        <div class="form-group">
          <label for="password">Student ID</label>
          <input
            id="password"
            v-model="password"
            type="password"
            placeholder="Enter your student ID"
            required
          />
        </div>

        <div v-if="errorMessage" class="error-message">
          {{ errorMessage }}
        </div>

        <button
          type="submit"
          class="login-btn"
          :disabled="!isValid"
        >
          Login
        </button>
      </form>
    </div>
  </div>
</template>

<style scoped>
.login-container {
  display: flex;
  justify-content: center;
  align-items: center;
  min-height: 500px;
  padding: 2rem;
}

.login-box {
  width: 100%;
  max-width: 450px;
  padding: 3rem 2.5rem;
  border: none;
  border-radius: 24px;
  background: var(--white);
  box-shadow: 0 20px 60px var(--shadow-lg), 0 0 0 1px rgba(102, 126, 234, 0.1);
  backdrop-filter: blur(10px);
  animation: slideUp 0.6s ease-out, glowPulse 3s ease-in-out infinite;
  position: relative;
  overflow: hidden;
}

.login-box::before {
  content: '';
  position: absolute;
  top: -50%;
  left: -50%;
  width: 200%;
  height: 200%;
  background: conic-gradient(
    from 0deg,
    transparent,
    rgba(102, 126, 234, 0.1),
    transparent 30%
  );
  animation: rotate 6s linear infinite;
}

.login-box::after {
  content: '';
  position: absolute;
  inset: 2px;
  background: var(--white);
  border-radius: 22px;
  z-index: 1;
}

.login-box > * {
  position: relative;
  z-index: 2;
}

@keyframes rotate {
  100% {
    transform: rotate(360deg);
  }
}

@keyframes glowPulse {
  0%, 100% {
    box-shadow: 0 20px 60px var(--shadow-lg), 0 0 0 1px rgba(102, 126, 234, 0.1);
  }
  50% {
    box-shadow: 0 20px 60px var(--shadow-lg), 0 0 30px rgba(102, 126, 234, 0.3), 0 0 0 1px rgba(102, 126, 234, 0.2);
  }
}

@keyframes slideUp {
  from {
    opacity: 0;
    transform: translateY(30px);
  }
  to {
    opacity: 1;
    transform: translateY(0);
  }
}

h2 {
  margin-top: 0;
  margin-bottom: 2rem;
  text-align: center;
  font-size: 2rem;
  font-weight: 700;
  background: var(--primary-gradient);
  -webkit-background-clip: text;
  -webkit-text-fill-color: transparent;
  background-clip: text;
}

.form-group {
  margin-bottom: 1.5rem;
  position: relative;
}

label {
  display: block;
  margin-bottom: 0.75rem;
  color: var(--dark);
  font-weight: 600;
  font-size: 0.9rem;
  text-transform: uppercase;
  letter-spacing: 0.5px;
}

input {
  width: 100%;
  padding: 1rem 1.25rem;
  border: 2px solid transparent;
  border-radius: 12px;
  font-size: 1rem;
  background: var(--light);
  box-sizing: border-box;
  transition: all 0.3s cubic-bezier(0.4, 0, 0.2, 1);
  font-family: inherit;
}

input:focus {
  outline: none;
  border-color: #667eea;
  background: var(--white);
  box-shadow: 0 0 0 4px rgba(102, 126, 234, 0.1);
  transform: translateY(-2px);
}

input::placeholder {
  color: #999;
}

.error-message {
  color: #f5576c;
  font-size: 0.875rem;
  margin-bottom: 1.5rem;
  padding: 0.875rem 1rem;
  background: linear-gradient(135deg, #fff5f5 0%, #ffe5e5 100%);
  border-radius: 12px;
  border-left: 4px solid #f5576c;
  animation: shake 0.5s ease-in-out;
}

@keyframes shake {
  0%, 100% { transform: translateX(0); }
  25% { transform: translateX(-10px); }
  75% { transform: translateX(10px); }
}

.login-btn {
  width: 100%;
  padding: 1rem 1.5rem;
  background: var(--primary-gradient);
  color: var(--white);
  border: none;
  border-radius: 12px;
  font-size: 1rem;
  font-weight: 700;
  cursor: pointer;
  transition: all 0.3s cubic-bezier(0.4, 0, 0.2, 1);
  box-shadow: 0 10px 30px rgba(102, 126, 234, 0.3);
  text-transform: uppercase;
  letter-spacing: 1px;
  position: relative;
  overflow: hidden;
}

.login-btn::before {
  content: '';
  position: absolute;
  top: 0;
  left: -100%;
  width: 100%;
  height: 100%;
  background: linear-gradient(90deg, transparent, rgba(255, 255, 255, 0.3), transparent);
  transition: left 0.5s;
}

.login-btn:hover:not(:disabled)::before {
  left: 100%;
}

.login-btn:hover:not(:disabled) {
  transform: translateY(-3px);
  box-shadow: 0 15px 40px rgba(102, 126, 234, 0.4);
}

.login-btn:active:not(:disabled) {
  transform: translateY(-1px);
}

.login-btn:disabled {
  background: linear-gradient(135deg, #e0e0e0 0%, #d0d0d0 100%);
  cursor: not-allowed;
  box-shadow: none;
  opacity: 0.6;
}
</style>
