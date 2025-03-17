<script setup>
import { onMounted } from 'vue'
import { gsap } from 'gsap'

onMounted(() => {
  const tl = gsap.timeline()
  tl.from('.hero-title', { opacity: 0, y: 30, duration: 0.8 })
    .from('.hero-subtitle', { opacity: 0, y: 20, duration: 0.6 }, '-=0.4')
    .from('.hero-text', { opacity: 0, y: 20, duration: 0.6 }, '-=0.4')
    .from('.hero-cta', { opacity: 0, y: 20, duration: 0.6 }, '-=0.4')
    .from('.hero-image', { opacity: 0, scale: 0.9, duration: 0.8 }, '-=0.6')
    .from('.scroll-indicator', { opacity: 0, y: -10, duration: 0.4, repeat: 3, yoyo: true }, '-=0.2')
})
</script>

<template>
  <section class="hero">
    <div class="container">
      <div class="hero-content">
        <div class="hero-info">
          <h1 class="hero-title">Bienvenue sur mon <span class="accent">Portfolio</span></h1>
          <h2 class="hero-subtitle">Développeur Web Créatif</h2>
          <p class="hero-text">
            Je conçois et développe des expériences numériques élégantes et performantes, 
            en combinant des interfaces utilisateur modernes avec des technologies robustes.
          </p>
          <div class="hero-cta">
            <router-link to="/projects" class="btn btn-primary">Voir mes projets</router-link>
            <router-link to="/contact" class="btn btn-outline">Me contacter</router-link>
          </div>
        </div>
        <div class="hero-visual">
          <div class="hero-image">
            <div class="code-window">
              <div class="code-header">
                <div class="code-circles">
                  <span class="code-circle"></span>
                  <span class="code-circle"></span>
                  <span class="code-circle"></span>
                </div>
                <div class="code-title">youss.ef</div>
              </div>
              <div class="code-body">
                <pre class="code-content">
<span class="code-keyword">const</span> <span class="code-variable">developer</span> = {
  name: <span class="code-string">'MOIII'</span>,
  role: <span class="code-string">'Full Stack Developer'</span>,
  skills: [<span class="code-string">'Vue.js'</span>, <span class="code-string">'JavaScript'</span>, <span class="code-string">'Node.js'</span>],
  passion: <span class="code-string">'Creating elegant web solutions'</span>,
  
  <span class="code-function">code</span>() {
    <span class="code-keyword">return</span> <span class="code-string">'Clean & efficient'</span>;
  },
  
  <span class="code-function">design</span>() {
    <span class="code-keyword">return</span> <span class="code-string">'Modern & intuitive'</span>;
  }
};</pre>
              </div>
            </div>
          </div>
          <div class="floating-elements">
            <div class="floating-element html-tag">&lt;/&gt;</div>
            <div class="floating-element css-icon">{}</div>
            <div class="floating-element js-icon">JS</div>
            <div class="floating-element vue-icon">
              <svg xmlns="http://www.w3.org/2000/svg" viewBox="0 0 196.32 170.02">
                <path fill="#42b883" d="M120.83 0L98.16 39.26 75.49 0H0l98.16 170.02L196.32 0h-75.49z"/>
                <path fill="#35495e" d="M120.83 0L98.16 39.26 75.49 0H39.26l58.9 102.01L157.06 0h-36.23z"/>
              </svg>
            </div>
          </div>
        </div>
      </div>
      <div class="scroll-indicator">
        <span>Scroll</span>
        <i class="fas fa-chevron-down"></i>
      </div>
    </div>
  </section>
  
  <section class="home-services section">
    <div class="container">
      <h2 class="section-title">Ce que je fais</h2>
      
      <div class="services-grid">
        <div class="service-card">
          <div class="service-icon">
            <i class="fas fa-code"></i>
          </div>
          <h3 class="service-title">Développement Front-end</h3>
          <p class="service-description">
            Création d'interfaces utilisateur réactives et intuitives utilisant les dernières technologies web.
          </p>
        </div>
        
        <div class="service-card">
          <div class="service-icon">
            <i class="fas fa-server"></i>
          </div>
          <h3 class="service-title">Développement Back-end</h3>
          <p class="service-description">
            Construction d'APIs robustes et évolutives pour alimenter vos applications.
          </p>
        </div>
        
        <div class="service-card">
          <div class="service-icon">
            <i class="fas fa-mobile-alt"></i>
          </div>
          <h3 class="service-title">Design Responsive</h3>
          <p class="service-description">
            Sites web parfaitement adaptés à tous les appareils, de l'ordinateur au smartphone.
          </p>
        </div>
        
        <div class="service-card">
          <div class="service-icon">
            <i class="fas fa-paint-brush"></i>
          </div>
          <h3 class="service-title">UI/UX Design</h3>
          <p class="service-description">
            Conception d'expériences utilisateur agréables et esthétiquement plaisantes.
          </p>
        </div>
      </div>
    </div>
  </section>
  
  <section class="home-cta section">
    <div class="container">
      <div class="cta-content">
        <h2 class="cta-title">Intéressé par une collaboration?</h2>
        <p class="cta-text">Découvrez mon travail et discutons de votre prochain projet</p>
        <div class="cta-buttons">
          <router-link to="/contact" class="btn btn-primary">Contactez-moi</router-link>
          <router-link to="/projects" class="btn btn-outline">Voir mes projets</router-link>
        </div>
      </div>
    </div>
  </section>
</template>

<style lang="scss" scoped>
.hero {
  min-height: calc(100vh - 70px);
  display: flex;
  align-items: center;
  padding: var(--spacing-xl) 0;
  position: relative;
  overflow: hidden;
  
  &-content {
    display: grid;
    grid-template-columns: 1fr 1fr;
    gap: var(--spacing-xl);
    align-items: center;
  }
  
  &-info {
    z-index: 1;
  }
  
  &-title {
    font-size: 3.5rem;
    margin-bottom: var(--spacing-md);
    line-height: 1.1;
    
    .accent {
      color: var(--primary-color);
      position: relative;
      
      &::after {
        content: '';
        position: absolute;
        bottom: 0.1em;
        left: 0;
        width: 100%;
        height: 0.2em;
        background-color: var(--accent-color);
        opacity: 0.3;
        z-index: -1;
      }
    }
  }
  
  &-subtitle {
    font-size: 1.5rem;
    color: var(--gray-dark);
    margin-bottom: var(--spacing-md);
    font-weight: 400;
  }
  
  &-text {
    font-size: 1.125rem;
    color: var(--gray-dark);
    margin-bottom: var(--spacing-lg);
    max-width: 90%;
    line-height: 1.7;
  }
  
  &-cta {
    display: flex;
    gap: var(--spacing-md);
    margin-top: var(--spacing-lg);
  }
  
  &-visual {
    position: relative;
  }
  
  &-image {
    position: relative;
    z-index: 1;
  }
}

.code-window {
  background-color: var(--background-dark);
  border-radius: var(--border-radius-md);
  overflow: hidden;
  box-shadow: var(--box-shadow-heavy);
  transform: perspective(1000px) rotateY(-5deg) rotateX(5deg);
  transition: transform var(--transition-medium);
  
  &:hover {
    transform: perspective(1000px) rotateY(-2deg) rotateX(2deg);
  }
  
  .code-header {
    display: flex;
    padding: 0.75rem 1rem;
    background-color: rgba(255, 255, 255, 0.05);
    align-items: center;
  }
  
  .code-circles {
    display: flex;
    gap: 8px;
  }
  
  .code-circle {
    width: 12px;
    height: 12px;
    border-radius: 50%;
    
    &:nth-child(1) {
      background-color: #ff5f56;
    }
    
    &:nth-child(2) {
      background-color: #ffbd2e;
    }
    
    &:nth-child(3) {
      background-color: #27c93f;
    }
  }
  
  .code-title {
    color: var(--text-light);
    margin-left: 1rem;
    font-size: 0.875rem;
    opacity: 0.7;
  }
  
  .code-body {
    padding: 1.5rem;
  }
  
  .code-content {
    font-family: var(--font-code);
    color: var(--text-light);
    font-size: 0.9rem;
    white-space: pre;
    line-height: 1.6;
    margin: 0;
  }
  
  .code-keyword {
    color: #ff79c6;
  }
  
  .code-variable {
    color: #bd93f9;
  }
  
  .code-string {
    color: #f1fa8c;
  }
  
  .code-function {
    color: #50fa7b;
  }
}

.floating-elements {
  position: absolute;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
  z-index: 0;
  pointer-events: none;
}

.floating-element {
  position: absolute;
  display: flex;
  align-items: center;
  justify-content: center;
  
  &.html-tag {
    font-size: 1.5rem;
    color: #e34f26;
    top: 10%;
    left: -5%;
    font-weight: bold;
    opacity: 0.8;
    animation: float 6s ease-in-out infinite;
  }
  
  &.css-icon {
    font-size: 1.5rem;
    color: #264de4;
    bottom: 15%;
    left: -10%;
    font-weight: bold;
    opacity: 0.8;
    animation: float 7s ease-in-out infinite reverse;
  }
  
  &.js-icon {
    font-size: 1.4rem;
    color: #f7df1e;
    top: 80%;
    right: 5%;
    font-weight: bold;
    background-color: rgba(0, 0, 0, 0.8);
    padding: 0.3em;
    border-radius: 0.2em;
    opacity: 0.9;
    animation: float 5s ease-in-out 1s infinite;
  }
  
  &.vue-icon {
    width: 2rem;
    top: 5%;
    right: 10%;
    opacity: 0.9;
    animation: float 8s ease-in-out 2s infinite;
  }
}

@keyframes float {
  0% {
    transform: translateY(0);
  }
  50% {
    transform: translateY(-15px);
  }
  100% {
    transform: translateY(0);
  }
}

.scroll-indicator {
  position: absolute;
  bottom: 2rem;
  left: 50%;
  transform: translateX(-50%);
  display: flex;
  flex-direction: column;
  align-items: center;
  color: var(--gray-medium);
  font-size: 0.875rem;
  gap: 0.5rem;
  
  i {
    animation: bounce 2s infinite;
  }
}

@keyframes bounce {
  0%, 20%, 50%, 80%, 100% {
    transform: translateY(0);
  }
  40% {
    transform: translateY(-10px);
  }
  60% {
    transform: translateY(-5px);
  }
}

.home-services {
  background-color: var(--gray-light);
}

.services-grid {
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(250px, 1fr));
  gap: var(--spacing-lg);
  margin-top: var(--spacing-xl);
}

.service-card {
  background-color: var(--background-light);
  border-radius: var(--border-radius-md);
  padding: var(--spacing-lg);
  box-shadow: var(--box-shadow-light);
  transition: transform var(--transition-medium), box-shadow var(--transition-medium);
  
  &:hover {
    transform: translateY(-5px);
    box-shadow: var(--box-shadow-medium);
  }
  
  .service-icon {
    font-size: 2.5rem;
    color: var(--primary-color);
    margin-bottom: var(--spacing-md);
  }
  
  .service-title {
    margin-bottom: var(--spacing-sm);
    font-size: 1.25rem;
  }
  
  .service-description {
    color: var(--gray-dark);
    line-height: 1.6;
    margin-bottom: 0;
  }
}

.home-cta {
  background: linear-gradient(135deg, var(--primary-color), var(--secondary-color));
  color: var(--text-light);
  
  .cta-content {
    text-align: center;
    max-width: 700px;
    margin: 0 auto;
  }
  
  .cta-title {
    font-size: 2.5rem;
    margin-bottom: var(--spacing-md);
  }
  
  .cta-text {
    font-size: 1.25rem;
    margin-bottom: var(--spacing-lg);
    opacity: 0.9;
  }
  
  .cta-buttons {
    display: flex;
    gap: var(--spacing-md);
    justify-content: center;
    
    .btn-outline {
      border-color: var(--text-light);
      color: var(--text-light);
      
      &:hover {
        background-color: var(--text-light);
        color: var(--primary-color);
      }
    }
  }
}

@media (max-width: 992px) {
  .hero {
    &-content {
      grid-template-columns: 1fr;
      text-align: center;
    }
    
    &-text {
      max-width: 100%;
    }
    
    &-cta {
      justify-content: center;
    }
    
    &-visual {
      grid-row: 1;
      margin-bottom: var(--spacing-lg);
    }
  }
  
  .floating-element {
    &.html-tag {
      left: 5%;
    }
    
    &.css-icon {
      left: 75%;
    }
  }
}

@media (max-width: 768px) {
  .hero {
    padding: var(--spacing-lg) 0;
    
    &-title {
      font-size: 2.5rem;
    }
    
    &-subtitle {
      font-size: 1.25rem;
    }
  }
  
  .cta-buttons {
    flex-direction: column;
    align-items: center;
    gap: var(--spacing-sm);
    
    .btn {
      width: 100%;
      max-width: 300px;
    }
  }
}

@media (max-width: 480px) {
  .hero-title {
    font-size: 2rem;
  }
  
  .service-card {
    padding: var(--spacing-md);
  }
  
  .home-cta .cta-title {
    font-size: 1.75rem;
  }
}
</style> 