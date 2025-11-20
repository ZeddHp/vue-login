# Vue Login Application

A modern, visually stunning Vue 3 login application with animated gradients, particle effects, and smooth transitions.

## Features

- ✨ Modern UI with animated gradients and particle effects
- 🔐 Secure login flow with email and student ID validation
- 💾 LocalStorage state persistence (survives page reload)
- 🎨 Beautiful animations and hover effects
- 📱 Responsive design
- 🖼️ Interactive profile avatar with flip animation
- 🏠 Dashboard with Home and About Me sections

## Tech Stack

- **Vue 3** - Progressive JavaScript framework
- **Vite** - Next generation frontend tooling
- **Composition API** - Modern Vue component architecture
- **CSS Animations** - Smooth gradient transitions and effects

## Project Structure

```
vue-login/
├── src/
│   ├── components/
│   │   ├── AboutMeComponent.vue    # Profile information with flip avatar
│   │   ├── HeaderComponent.vue     # App header with logout
│   │   ├── HomeComponent.vue       # Dashboard home view
│   │   ├── LoginComponent.vue      # Login form
│   │   ├── ParticlesBackground.vue # Animated particles
│   │   └── SideNavComponent.vue    # Navigation sidebar
│   ├── App.vue                     # Root component
│   ├── main.js                     # App entry point
│   └── style.css                   # Global styles
├── public/
│   └── KL1F3957-Edit1.jpg         # Profile picture
├── package.json
├── vite.config.js
└── README.md
```

## Getting Started

### Prerequisites

- Node.js 20.19+ or 22.12+
- npm or yarn

### Installation

1. Clone the repository:
```bash
git clone https://github.com/ZeddHp/vue-login.git
cd vue-login
```

2. Install dependencies:
```bash
npm install
```

3. Start the development server:
```bash
npm run dev
```

4. Open your browser and navigate to `http://localhost:5173`

## Credentials

Use the following credentials to log in:

- **Email:** valtersbernhards.jargans@va.lv
- **Student ID:** IT22082

## Build for Production

```bash
npm run build
```

The built files will be in the `dist` directory.

## Preview Production Build

```bash
npm run preview
```

## Features Breakdown

### Login System
- Email and password validation
- Real-time button state (disabled until valid)
- Error messages with shake animation
- Rotating border glow effect

### Dashboard
- Animated gradient header
- Sidebar navigation with smooth transitions
- Particle background effects
- LocalStorage state persistence

### Profile Page
- Interactive avatar with flip animation on hover
- Profile information cards with hover effects
- Gradient animations throughout
- Responsive layout

## Design Highlights

- **Color Palette:** Purple, pink, and blue gradient combinations
- **Animations:** Smooth cubic-bezier transitions
- **Effects:** Particle system, rotating gradients, shimmer effects
- **Typography:** Modern sans-serif with gradient text effects

## Browser Support

- Chrome (latest)
- Firefox (latest)
- Safari (latest)
- Edge (latest)

## License

This project is created for educational purposes.

## Author

**Valters Bernhards Jargans**
- Student ID: IT22082
- Email: valtersbernhards.jargans@va.lv

---

🚀 Generated with [Claude Code](https://claude.com/claude-code)
