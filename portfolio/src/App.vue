<script setup>
import { ref, onMounted, watch } from 'vue'
import { useRouter } from 'vue-router'
import { gsap } from 'gsap'

const router = useRouter()
const isMenuOpen = ref(false)
const currentRoute = ref('/')

onMounted(() => {
  // Mettre à jour la route active au chargement
  currentRoute.value = router.currentRoute.value.path
  
  // Animation d'entrée avec forceTransform pour éviter les problèmes de rendu
  const tl = gsap.timeline({ defaults: { ease: 'power2.out', force3D: true } })
  tl.from('.nav-logo', { opacity: 0, y: -20, duration: 0.6, clearProps: 'all' })
    .from('.nav-item', { 
      opacity: 0, 
      y: -20, 
      stagger: 0.1, 
      duration: 0.4,
      clearProps: 'all' // Assure que les propriétés d'animation sont nettoyées
    }, '-=0.2')
    .from('.router-container', { opacity: 0, duration: 0.8 }, '-=0.4')
})

// Mettre à jour la route active lorsque la route change
watch(() => router.currentRoute.value.path, (newPath) => {
  currentRoute.value = newPath
})

const toggleMenu = () => {
  isMenuOpen.value = !isMenuOpen.value
}

const setActiveRoute = (route) => {
  currentRoute.value = route
  if (window.innerWidth < 768) {
    isMenuOpen.value = false
  }
}
</script>

<template>
  <div class="app">
    <header class="header">
      <div class="container header-container">
        <div class="nav-logo">
          <router-link to="/" @click="setActiveRoute('/')">
            <span class="logo-text">Portfolio</span>
          </router-link>
        </div>
        
        <button class="menu-toggle" @click="toggleMenu" aria-label="Toggle navigation menu">
          <span class="menu-toggle-bar"></span>
          <span class="menu-toggle-bar"></span>
          <span class="menu-toggle-bar"></span>
        </button>
        
        <nav class="nav" :class="{ 'nav-open': isMenuOpen }">
          <ul class="nav-list">
            <li class="nav-item">
              <router-link to="/" class="nav-link" :class="{ 'active': currentRoute === '/' }" @click="setActiveRoute('/')">
                <i class="fas fa-home"></i> Accueil
              </router-link>
            </li>
            <li class="nav-item">
              <router-link to="/about" class="nav-link" :class="{ 'active': currentRoute === '/about' }" @click="setActiveRoute('/about')">
                <i class="fas fa-user"></i> À propos
              </router-link>
            </li>
            <li class="nav-item">
              <router-link to="/skills" class="nav-link" :class="{ 'active': currentRoute === '/skills' }" @click="setActiveRoute('/skills')">
                <i class="fas fa-code"></i> Compétences
              </router-link>
            </li>
            <li class="nav-item">
              <router-link to="/projects" class="nav-link" :class="{ 'active': currentRoute === '/projects' }" @click="setActiveRoute('/projects')">
                <i class="fas fa-laptop-code"></i> Projets
              </router-link>
            </li>
            <li class="nav-item">
              <router-link to="/contact" class="nav-link" :class="{ 'active': currentRoute === '/contact' }" @click="setActiveRoute('/contact')">
                <i class="fas fa-envelope"></i> Contact
              </router-link>
            </li>
          </ul>
        </nav>
      </div>
    </header>
    
    <main class="main router-container">
      <router-view v-slot="{ Component }">
        <transition name="fade" mode="out-in">
          <component :is="Component" />
        </transition>
      </router-view>
    </main>
    
    <footer class="footer">
      <div class="container footer-container">
        <div class="footer-content">
          <p class="footer-copyright">&copy; {{ new Date().getFullYear() }} Portfolio</p>
          <div class="footer-social">
            <a href="https://github.com/" target="_blank" rel="noopener noreferrer" class="social-link">
              <i class="fab fa-github"></i>
            </a>
            <a href="https://linkedin.com/" target="_blank" rel="noopener noreferrer" class="social-link">
              <i class="fab fa-linkedin"></i>
            </a>
            <a href="https://twitter.com/" target="_blank" rel="noopener noreferrer" class="social-link">
              <i class="fab fa-twitter"></i>
            </a>
          </div>
        </div>
      </div>
    </footer>
  </div>
</template>

<style lang="scss" scoped>
.app {
  display: flex;
  flex-direction: column;
  min-height: 100vh;
}

.header {
  background-color: var(--background-light);
  box-shadow: var(--box-shadow-light);
  position: sticky;
  top: 0;
  z-index: 100;
  transition: all var(--transition-medium);
  
  &-container {
    display: flex;
    justify-content: space-between;
    align-items: center;
    padding: 1rem var(--spacing-md);
    height: 70px; /* Hauteur fixe pour éviter les redimensionnements */
  }
}

.nav-logo {
  display: flex;
  align-items: center;
  z-index: 101; /* Assure que le logo reste au-dessus du menu mobile */
  
  a {
    display: flex;
    align-items: center;
    text-decoration: none;
  }
  
  .logo-text {
    font-size: 1.5rem;
    font-weight: 700;
    color: var(--primary-color);
    font-family: var(--font-secondary);
    letter-spacing: 1px;
    margin-left: var(--spacing-xs);
  }
}

.nav {
  &-list {
    display: flex;
    list-style: none;
    gap: var(--spacing-md);
    margin: 0;
    padding: 0;
  }
  
  &-item {
    margin: 0;
    padding: 0;
  }
  
  &-link {
    color: var(--text-dark);
    font-weight: 500;
    display: flex;
    align-items: center;
    gap: 0.4rem;
    padding: 0.5rem 0.75rem;
    border-radius: var(--border-radius-md);
    transition: all var(--transition-medium);
    text-decoration: none;
    
    i {
      font-size: 0.875rem;
    }
    
    &:hover, &.active {
      color: var(--primary-color);
      background-color: var(--gray-light);
    }
    
    &.active {
      font-weight: 600;
    }
  }
}

.menu-toggle {
  display: none;
  flex-direction: column;
  justify-content: space-between;
  width: 30px;
  height: 21px;
  background: transparent;
  border: none;
  cursor: pointer;
  padding: 0;
  z-index: 101; /* Assure que le bouton reste au-dessus du menu mobile */
  
  &-bar {
    height: 3px;
    width: 100%;
    background-color: var(--text-dark);
    border-radius: 1px;
    transition: all var(--transition-medium);
  }
}

.main {
  flex: 1;
}

.footer {
  background-color: var(--background-dark);
  color: var(--text-light);
  padding: var(--spacing-lg) 0;
  
  &-container {
    padding: 0 var(--spacing-md);
  }
  
  &-content {
    display: flex;
    justify-content: space-between;
    align-items: center;
  }
  
  &-copyright {
    margin-bottom: 0;
  }
  
  &-social {
    display: flex;
    gap: var(--spacing-md);
    
    .social-link {
      color: var(--text-light);
      font-size: 1.5rem;
      transition: color var(--transition-fast);
      
      &:hover {
        color: var(--primary-color);
      }
    }
  }
}

@media (max-width: 767px) {
  .header-container {
    padding: 1rem var(--spacing-sm);
  }
  
  .menu-toggle {
    display: flex;
    z-index: 100;
  }
  
  .nav {
    position: fixed;
    top: 0;
    right: -100%;
    width: 70%;
    height: 100vh;
    background-color: var(--background-light);
    padding: 5rem var(--spacing-lg) var(--spacing-lg);
    transition: right var(--transition-medium);
    box-shadow: var(--box-shadow-heavy);
    
    &-open {
      right: 0;
    }
    
    &-list {
      flex-direction: column;
      align-items: flex-start;
      gap: var(--spacing-lg);
    }
    
    &-link {
      font-size: 1.25rem;
      width: 100%;
    }
  }
  
  .nav-logo .logo-text {
    font-size: 1.25rem;
  }
  
  .footer {
    &-content {
      flex-direction: column;
      gap: var(--spacing-md);
      text-align: center;
    }
  }
}
</style>
