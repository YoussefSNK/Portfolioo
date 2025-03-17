<script setup>
import { onMounted } from 'vue'
import { gsap } from 'gsap'
import { ScrollTrigger } from 'gsap/ScrollTrigger'

gsap.registerPlugin(ScrollTrigger)

onMounted(() => {
  // Animation du titre et de l'introduction
  gsap.from('.about-title, .about-subtitle', {
    opacity: 0,
    y: 30,
    duration: 0.8,
    stagger: 0.2
  })
  
  // Animation des sections avec ScrollTrigger
  gsap.utils.toArray('.about-section').forEach((section, i) => {
    gsap.from(section, {
      scrollTrigger: {
        trigger: section,
        start: 'top bottom-=100',
        toggleActions: 'play none none none'
      },
      opacity: 0,
      y: 50,
      duration: 0.8,
      delay: i * 0.1
    })
  })
  
  // Animation de la timeline
  gsap.from('.timeline-item', {
    scrollTrigger: {
      trigger: '.timeline',
      start: 'top bottom-=50',
      toggleActions: 'play none none none'
    },
    opacity: 0,
    y: 30,
    stagger: 0.2,
    duration: 0.6
  })
})
</script>

<template>
  <div class="about">
    <div class="container">
      <header class="about-header">
        <h1 class="about-title section-title">À propos de moi</h1>
        <p class="about-subtitle">Découvrez mon parcours, mes compétences et ma passion pour le développement web.</p>
      </header>
      
      <section class="about-section about-intro">
        <div class="about-grid">
          <div class="about-image-container">
            <div class="about-image">
              <img src="https://images.unsplash.com/photo-1507003211169-0a1dd7228f2d?ixlib=rb-4.0.3&ixid=MnwxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHx8&auto=format&fit=crop&w=387&q=80" alt="Développeur" />
            </div>
          </div>
          
          <div class="about-content">
            <h2>Bonjour, je suis <span class="highlight">John Doe</span></h2>
            <p class="about-lead">
              Développeur web passionné avec plus de 5 ans d'expérience dans la création de solutions web modernes et performantes.
            </p>
            
            <p>
              Mon objectif est de concevoir des expériences utilisateur exceptionnelles qui allient esthétique et fonctionnalité. 
              Je suis spécialisé dans le développement frontend avec Vue.js et possède également de solides compétences en backend.
            </p>
            
            <p>
              Passionné par les technologies web modernes, j'aime relever de nouveaux défis et apprendre constamment 
              pour rester à la pointe des dernières avancées technologiques.
            </p>
            
            <div class="about-stats">
              <div class="stat-item">
                <div class="stat-number">5+</div>
                <div class="stat-label">Années d'expérience</div>
              </div>
              
              <div class="stat-item">
                <div class="stat-number">30+</div>
                <div class="stat-label">Projets réalisés</div>
              </div>
              
              <div class="stat-item">
                <div class="stat-number">15+</div>
                <div class="stat-label">Clients satisfaits</div>
              </div>
            </div>
          </div>
        </div>
      </section>
      
      <section class="about-section">
        <h2 class="section-title">Mon parcours</h2>
        
        <div class="timeline">
          <div class="timeline-item">
            <div class="timeline-dot"></div>
            <div class="timeline-date">2023 - Présent</div>
            <div class="timeline-content">
              <h3>Développeur Frontend Senior</h3>
              <p class="timeline-place">TechInnovate, Paris</p>
              <p>
                Développement d'applications web complexes utilisant Vue.js et d'autres technologies modernes.
                Lead technique sur plusieurs projets majeurs et mentorat des développeurs juniors.
              </p>
            </div>
          </div>
          
          <div class="timeline-item">
            <div class="timeline-dot"></div>
            <div class="timeline-date">2020 - 2023</div>
            <div class="timeline-content">
              <h3>Développeur Fullstack</h3>
              <p class="timeline-place">WebSolutions, Lyon</p>
              <p>
                Conception et développement d'applications web pour des clients variés.
                Utilisation de Vue.js, Node.js et diverses bases de données pour créer des solutions complètes.
              </p>
            </div>
          </div>
          
          <div class="timeline-item">
            <div class="timeline-dot"></div>
            <div class="timeline-date">2018 - 2020</div>
            <div class="timeline-content">
              <h3>Développeur Web Junior</h3>
              <p class="timeline-place">DigitalCraft, Bordeaux</p>
              <p>
                Début de carrière dans le développement web avec un focus sur le frontend.
                Participation à divers projets d'équipe et apprentissage des bonnes pratiques du développement web.
              </p>
            </div>
          </div>
          
          <div class="timeline-item">
            <div class="timeline-dot"></div>
            <div class="timeline-date">2016 - 2018</div>
            <div class="timeline-content">
              <h3>Master en Développement Web</h3>
              <p class="timeline-place">Université de Technologie, Paris</p>
              <p>
                Formation approfondie en développement web, algorithmique et conception d'interfaces.
                Projets pratiques et stage de fin d'études dans une startup technologique.
              </p>
            </div>
          </div>
        </div>
      </section>
      
      <section class="about-section">
        <h2 class="section-title">Mes valeurs</h2>
        
        <div class="values-grid">
          <div class="value-card">
            <div class="value-icon">
              <i class="fas fa-lightbulb"></i>
            </div>
            <h3>Innovation</h3>
            <p>
              Je m'efforce toujours de trouver des solutions créatives et novatrices aux problèmes techniques et de design.
            </p>
          </div>
          
          <div class="value-card">
            <div class="value-icon">
              <i class="fas fa-shield-alt"></i>
            </div>
            <h3>Qualité</h3>
            <p>
              Je m'engage à produire un code propre, bien documenté et des interfaces utilisateur soignées.
            </p>
          </div>
          
          <div class="value-card">
            <div class="value-icon">
              <i class="fas fa-hands-helping"></i>
            </div>
            <h3>Collaboration</h3>
            <p>
              Je crois en la puissance du travail d'équipe et de la communication pour atteindre l'excellence.
            </p>
          </div>
          
          <div class="value-card">
            <div class="value-icon">
              <i class="fas fa-book"></i>
            </div>
            <h3>Apprentissage continu</h3>
            <p>
              Je reste constamment à l'affût des nouvelles technologies et des meilleures pratiques.
            </p>
          </div>
        </div>
      </section>
      
      <section class="about-section about-interests">
        <h2 class="section-title">Centres d'intérêt</h2>
        
        <div class="interests-container">
          <div class="interest-item">
            <div class="interest-icon">
              <i class="fas fa-mountain"></i>
            </div>
            <h3>Randonnée</h3>
          </div>
          
          <div class="interest-item">
            <div class="interest-icon">
              <i class="fas fa-camera"></i>
            </div>
            <h3>Photographie</h3>
          </div>
          
          <div class="interest-item">
            <div class="interest-icon">
              <i class="fas fa-chess"></i>
            </div>
            <h3>Échecs</h3>
          </div>
          
          <div class="interest-item">
            <div class="interest-icon">
              <i class="fas fa-book-open"></i>
            </div>
            <h3>Lecture</h3>
          </div>
          
          <div class="interest-item">
            <div class="interest-icon">
              <i class="fas fa-plane"></i>
            </div>
            <h3>Voyages</h3>
          </div>
        </div>
      </section>
      
      <section class="about-section about-cta">
        <div class="cta-container">
          <h2>Envie de travailler ensemble?</h2>
          <p>Consultez mon portfolio de projets ou contactez-moi directement pour discuter de votre projet.</p>
          <div class="cta-buttons">
            <router-link to="/projects" class="btn btn-primary">Voir mes projets</router-link>
            <router-link to="/contact" class="btn btn-outline">Me contacter</router-link>
          </div>
        </div>
      </section>
    </div>
  </div>
</template>

<style lang="scss" scoped>
.about {
  padding-top: var(--spacing-xl);
  padding-bottom: var(--spacing-xl);
  
  &-header {
    text-align: center;
    margin-bottom: var(--spacing-xl);
  }
  
  &-subtitle {
    font-size: 1.25rem;
    color: var(--gray-dark);
    max-width: 800px;
    margin: 0 auto;
  }
  
  &-section {
    margin-bottom: var(--spacing-xl);
  }
  
  &-grid {
    display: grid;
    grid-template-columns: 1fr 2fr;
    gap: var(--spacing-xl);
    align-items: center;
  }
  
  &-image-container {
    position: relative;
  }
  
  &-image {
    position: relative;
    border-radius: var(--border-radius-lg);
    overflow: hidden;
    box-shadow: var(--box-shadow-medium);
    
    &::before {
      content: '';
      position: absolute;
      top: -30px;
      left: -30px;
      width: 60px;
      height: 60px;
      border-top: 5px solid var(--primary-color);
      border-left: 5px solid var(--primary-color);
      z-index: -1;
    }
    
    &::after {
      content: '';
      position: absolute;
      bottom: -30px;
      right: -30px;
      width: 60px;
      height: 60px;
      border-bottom: 5px solid var(--accent-color);
      border-right: 5px solid var(--accent-color);
      z-index: -1;
    }
    
    img {
      display: block;
      width: 100%;
      height: 100%;
      object-fit: cover;
      transition: transform var(--transition-medium);
      
      &:hover {
        transform: scale(1.05);
      }
    }
  }
  
  &-content {
    h2 {
      margin-bottom: var(--spacing-md);
      
      .highlight {
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
    
    .about-lead {
      font-size: 1.25rem;
      font-weight: 500;
      margin-bottom: var(--spacing-md);
      color: var(--gray-dark);
    }
    
    p {
      margin-bottom: var(--spacing-md);
      line-height: 1.8;
    }
  }
  
  &-stats {
    display: flex;
    gap: var(--spacing-lg);
    margin-top: var(--spacing-lg);
  }
}

.stat-item {
  text-align: center;
  
  .stat-number {
    font-size: 2.5rem;
    font-weight: 700;
    color: var(--primary-color);
    margin-bottom: var(--spacing-xs);
    font-family: var(--font-secondary);
  }
  
  .stat-label {
    font-size: 0.9rem;
    color: var(--gray-dark);
  }
}

.timeline {
  position: relative;
  margin: var(--spacing-xl) 0;
  padding-left: 2rem;
  
  &::before {
    content: '';
    position: absolute;
    top: 0;
    bottom: 0;
    left: 7px;
    width: 2px;
    background-color: var(--gray-medium);
  }
  
  &-item {
    position: relative;
    margin-bottom: var(--spacing-lg);
    
    &:last-child {
      margin-bottom: 0;
    }
  }
  
  &-dot {
    position: absolute;
    top: 5px;
    left: -2rem;
    width: 16px;
    height: 16px;
    border-radius: 50%;
    background-color: var(--primary-color);
    border: 3px solid white;
    box-shadow: var(--box-shadow-light);
    z-index: 1;
  }
  
  &-date {
    font-weight: 600;
    color: var(--primary-color);
    margin-bottom: var(--spacing-xs);
  }
  
  &-content {
    background-color: var(--background-light);
    border-radius: var(--border-radius-md);
    padding: var(--spacing-md);
    box-shadow: var(--box-shadow-light);
    
    h3 {
      margin-bottom: var(--spacing-xs);
    }
    
    .timeline-place {
      color: var(--gray-dark);
      font-style: italic;
      margin-bottom: var(--spacing-sm);
    }
    
    p:last-child {
      margin-bottom: 0;
    }
  }
}

.values-grid {
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(240px, 1fr));
  gap: var(--spacing-lg);
  margin-top: var(--spacing-lg);
}

.value-card {
  background-color: var(--background-light);
  border-radius: var(--border-radius-md);
  padding: var(--spacing-lg);
  box-shadow: var(--box-shadow-light);
  text-align: center;
  transition: transform var(--transition-medium), box-shadow var(--transition-medium);
  
  &:hover {
    transform: translateY(-5px);
    box-shadow: var(--box-shadow-medium);
  }
  
  .value-icon {
    font-size: 2.5rem;
    color: var(--primary-color);
    margin-bottom: var(--spacing-md);
    
    i {
      background: linear-gradient(45deg, var(--primary-color), var(--secondary-color));
      -webkit-background-clip: text;
      -webkit-text-fill-color: transparent;
    }
  }
  
  h3 {
    margin-bottom: var(--spacing-sm);
  }
  
  p {
    color: var(--gray-dark);
    line-height: 1.6;
    margin-bottom: 0;
  }
}

.interests-container {
  display: flex;
  flex-wrap: wrap;
  gap: var(--spacing-lg);
  justify-content: center;
  margin-top: var(--spacing-lg);
}

.interest-item {
  display: flex;
  flex-direction: column;
  align-items: center;
  text-align: center;
  width: 140px;
  
  .interest-icon {
    width: 80px;
    height: 80px;
    border-radius: 50%;
    background-color: var(--gray-light);
    display: flex;
    align-items: center;
    justify-content: center;
    margin-bottom: var(--spacing-sm);
    transition: all var(--transition-medium);
    
    i {
      font-size: 1.75rem;
      color: var(--primary-color);
      transition: all var(--transition-medium);
    }
  }
  
  &:hover .interest-icon {
    background-color: var(--primary-color);
    transform: translateY(-5px);
    
    i {
      color: white;
    }
  }
  
  h3 {
    font-size: 1rem;
    font-weight: 500;
  }
}

.about-cta {
  margin-top: var(--spacing-xl);
  
  .cta-container {
    background: linear-gradient(45deg, var(--primary-color), var(--secondary-color));
    color: var(--text-light);
    border-radius: var(--border-radius-lg);
    padding: var(--spacing-xl);
    text-align: center;
    
    h2 {
      margin-bottom: var(--spacing-md);
    }
    
    p {
      margin-bottom: var(--spacing-lg);
      max-width: 600px;
      margin-left: auto;
      margin-right: auto;
    }
    
    .cta-buttons {
      display: flex;
      gap: var(--spacing-md);
      justify-content: center;
      
      .btn-outline {
        color: var(--text-light);
        border-color: var(--text-light);
        
        &:hover {
          background-color: var(--text-light);
          color: var(--primary-color);
        }
      }
    }
  }
}

@media (max-width: 992px) {
  .about-grid {
    grid-template-columns: 1fr;
  }
  
  .about-image-container {
    max-width: 400px;
    margin: 0 auto var(--spacing-lg);
  }
  
  .about-stats {
    justify-content: space-around;
  }
}

@media (max-width: 768px) {
  .timeline {
    padding-left: 1.5rem;
    
    &::before {
      left: 5px;
    }
    
    &-dot {
      width: 12px;
      height: 12px;
      left: -1.5rem;
    }
  }
  
  .about-cta .cta-container {
    padding: var(--spacing-lg);
  }
  
  .cta-buttons {
    flex-direction: column;
    align-items: center;
    
    .btn {
      width: 100%;
      max-width: 300px;
    }
  }
}

@media (max-width: 480px) {
  .about-stats {
    flex-direction: column;
    gap: var(--spacing-md);
  }
  
  .interests-container {
    gap: var(--spacing-md);
  }
  
  .interest-item {
    width: 120px;
  }
}
</style> 