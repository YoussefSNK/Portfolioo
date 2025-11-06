<script setup>
import { ref, onMounted } from 'vue'
import { gsap } from 'gsap'

const frontendSkills = ref([
  { name: 'HTML5', level: 95, icon: 'fab fa-html5', color: '#E34F26' },
  { name: 'CSS3', level: 90, icon: 'fab fa-css3-alt', color: '#1572B6' },
  { name: 'JavaScript', level: 92, icon: 'fab fa-js', color: '#F7DF1E' },
  { name: 'Vue.js', level: 88, icon: 'fab fa-vuejs', color: '#4FC08D' },
  { name: 'React', level: 80, icon: 'fab fa-react', color: '#61DAFB' },
  { name: 'SASS', level: 85, icon: 'fab fa-sass', color: '#CC6699' }
])

const backendSkills = ref([
  { name: 'Node.js', level: 85, icon: 'fab fa-node-js', color: '#339933' },
  { name: 'PHP', level: 78, icon: 'fab fa-php', color: '#777BB4' },
  { name: 'Python', level: 75, icon: 'fab fa-python', color: '#3776AB' },
  { name: 'MongoDB', level: 82, icon: 'fas fa-database', color: '#47A248' },
  { name: 'MySQL', level: 80, icon: 'fas fa-server', color: '#4479A1' },
  { name: 'GraphQL', level: 70, icon: 'fas fa-project-diagram', color: '#E535AB' }
])

const toolsSkills = ref([
  { name: 'Git', level: 90, icon: 'fab fa-git-alt', color: '#F05032' },
  { name: 'Docker', level: 75, icon: 'fab fa-docker', color: '#2496ED' },
  { name: 'VS Code', level: 95, icon: 'fas fa-code', color: '#007ACC' },
  { name: 'Webpack', level: 80, icon: 'fas fa-cube', color: '#8DD6F9' },
  { name: 'Figma', level: 85, icon: 'fab fa-figma', color: '#F24E1E' },
  { name: 'Adobe XD', level: 80, icon: 'fab fa-adobe', color: '#FF61F6' }
])

const otherSkills = ref([
  { name: 'UI/UX Design', icon: 'fas fa-pencil-ruler', description: 'Conception d\'interfaces utilisateur intuitives et esthétiques' },
  { name: 'Responsive Design', icon: 'fas fa-mobile-alt', description: 'Création de sites web adaptatifs pour tous les appareils' },
  { name: 'SEO', icon: 'fas fa-search', description: 'Optimisation pour les moteurs de recherche' },
  { name: 'Agile/Scrum', icon: 'fas fa-tasks', description: 'Méthodes de développement agiles et framework Scrum' },
  { name: 'Test unitaire', icon: 'fas fa-vial', description: 'Écriture de tests pour assurer la qualité du code' },
  { name: 'CI/CD', icon: 'fas fa-sync-alt', description: 'Intégration et déploiement continus' }
])

const languages = ref([
  { name: 'Français', level: 'Natif', flag: '🇫🇷' },
  { name: 'Anglais', level: 'Courant', flag: '🇬🇧' },
  { name: 'Espagnol', level: 'Intermédiaire', flag: '🇪🇸' },
  { name: 'Allemand', level: 'Notions', flag: '🇩🇪' }
])

onMounted(() => {
  // Animation du titre
  gsap.from('.skills-title, .skills-subtitle', {
    opacity: 0, 
    y: 30,
    duration: 0.8,
    stagger: 0.2
  })
  
  // Animation des barres de progression
  gsap.from('.skill-progress-bar', {
    scaleX: 0,
    duration: 1.5,
    stagger: 0.05,
    ease: 'power2.out',
    delay: 0.3
  })
  
  // Animation des cartes
  gsap.from('.skill-card', {
    opacity: 0,
    y: 20,
    duration: 0.6,
    stagger: 0.1,
    delay: 0.5
  })
})
</script>

<template>
  <div class="skills">
    <div class="container">
      <header class="skills-header">
        <h1 class="skills-title section-title">Mes compétences</h1>
        <p class="skills-subtitle">Un aperçu des technologies et outils que j'utilise pour créer des applications web modernes et performantes.</p>
      </header>
      
      <section class="skills-section">
        <h2 class="section-title">Technologies Front-end</h2>
        
        <div class="skills-grid">
          <div class="skill-item" v-for="(skill, index) in frontendSkills" :key="`frontend-${index}`">
            <div class="skill-header">
              <div class="skill-icon" :style="{ color: skill.color }">
                <i :class="skill.icon"></i>
              </div>
              <div class="skill-details">
                <h3 class="skill-name">{{ skill.name }}</h3>
                <span class="skill-level">{{ skill.level }}%</span>
              </div>
            </div>
            <div class="skill-progress">
              <div class="skill-progress-bar" :style="{ width: `${skill.level}%`, backgroundColor: skill.color }"></div>
            </div>
          </div>
        </div>
      </section>
      
      <section class="skills-section">
        <h2 class="section-title">Technologies Back-end</h2>
        
        <div class="skills-grid">
          <div class="skill-item" v-for="(skill, index) in backendSkills" :key="`backend-${index}`">
            <div class="skill-header">
              <div class="skill-icon" :style="{ color: skill.color }">
                <i :class="skill.icon"></i>
              </div>
              <div class="skill-details">
                <h3 class="skill-name">{{ skill.name }}</h3>
                <span class="skill-level">{{ skill.level }}%</span>
              </div>
            </div>
            <div class="skill-progress">
              <div class="skill-progress-bar" :style="{ width: `${skill.level}%`, backgroundColor: skill.color }"></div>
            </div>
          </div>
        </div>
      </section>
      
      <section class="skills-section">
        <h2 class="section-title">Outils & Environnements</h2>
        
        <div class="skills-grid">
          <div class="skill-item" v-for="(skill, index) in toolsSkills" :key="`tools-${index}`">
            <div class="skill-header">
              <div class="skill-icon" :style="{ color: skill.color }">
                <i :class="skill.icon"></i>
              </div>
              <div class="skill-details">
                <h3 class="skill-name">{{ skill.name }}</h3>
                <span class="skill-level">{{ skill.level }}%</span>
              </div>
            </div>
            <div class="skill-progress">
              <div class="skill-progress-bar" :style="{ width: `${skill.level}%`, backgroundColor: skill.color }"></div>
            </div>
          </div>
        </div>
      </section>
      
      <section class="skills-section">
        <h2 class="section-title">Compétences annexes</h2>
        
        <div class="other-skills-grid">
          <div class="skill-card" v-for="(skill, index) in otherSkills" :key="`other-${index}`">
            <div class="skill-card-icon">
              <i :class="skill.icon"></i>
            </div>
            <h3 class="skill-card-title">{{ skill.name }}</h3>
            <p class="skill-card-description">{{ skill.description }}</p>
          </div>
        </div>
      </section>
      
      <section class="skills-section languages-section">
        <h2 class="section-title">Langues</h2>
        
        <div class="languages-grid">
          <div class="language-item" v-for="(language, index) in languages" :key="`lang-${index}`">
            <div class="language-flag">{{ language.flag }}</div>
            <div class="language-details">
              <h3 class="language-name">{{ language.name }}</h3>
              <span class="language-level">{{ language.level }}</span>
            </div>
          </div>
        </div>
      </section>
      
      <section class="skills-section certifications-section">
        <h2 class="section-title">Certifications</h2>
        
        <div class="certifications-grid">
          <div class="certification-item">
            <div class="certification-logo">
              <i class="fab fa-vuejs"></i>
            </div>
            <div class="certification-content">
              <h3>Vue.js Advanced Developer</h3>
              <p class="certification-issuer">Vue Mastery, 2022</p>
            </div>
          </div>
          
          <div class="certification-item">
            <div class="certification-logo">
              <i class="fab fa-js"></i>
            </div>
            <div class="certification-content">
              <h3>JavaScript Algorithms & Data Structures</h3>
              <p class="certification-issuer">freeCodeCamp, 2021</p>
            </div>
          </div>
          
          <div class="certification-item">
            <div class="certification-logo">
              <i class="fab fa-aws"></i>
            </div>
            <div class="certification-content">
              <h3>AWS Certified Developer</h3>
              <p class="certification-issuer">Amazon Web Services, 2020</p>
            </div>
          </div>
        </div>
      </section>
      
      <section class="skills-cta">
        <div class="cta-container">
          <h2>Intéressé par mes compétences?</h2>
          <p>Consultez mes projets pour voir comment j'utilise ces technologies pour créer des applications web de qualité.</p>
          <router-link to="/projects" class="btn btn-primary">Voir mes projets</router-link>
        </div>
      </section>
    </div>
  </div>
</template>

<style lang="scss" scoped>
.skills {
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
}

.skills-grid {
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(300px, 1fr));
  gap: var(--spacing-lg);
  margin-top: var(--spacing-lg);
}

.skill-item {
  background-color: var(--background-light);
  border-radius: var(--border-radius-md);
  padding: var(--spacing-md);
  box-shadow: var(--box-shadow-light);
  transition: transform var(--transition-medium), box-shadow var(--transition-medium);
  
  &:hover {
    transform: translateY(-5px);
    box-shadow: var(--box-shadow-medium);
  }
}

.skill-header {
  display: flex;
  align-items: center;
  margin-bottom: var(--spacing-sm);
}

.skill-icon {
  font-size: 2rem;
  margin-right: var(--spacing-md);
  width: 40px;
  text-align: center;
}

.skill-details {
  flex: 1;
  display: flex;
  justify-content: space-between;
  align-items: center;
}

.skill-name {
  font-size: 1.1rem;
  margin: 0;
}

.skill-level {
  font-weight: 600;
  color: var(--gray-dark);
}

.skill-progress {
  height: 8px;
  background-color: var(--gray-light);
  border-radius: 4px;
  overflow: hidden;
}

.skill-progress-bar {
  height: 100%;
  border-radius: 4px;
  transform-origin: left;
}

.other-skills-grid {
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(250px, 1fr));
  gap: var(--spacing-lg);
  margin-top: var(--spacing-lg);
}

.skill-card {
  background-color: var(--background-light);
  border-radius: var(--border-radius-md);
  padding: var(--spacing-lg);
  box-shadow: var(--box-shadow-light);
  text-align: center;
  transition: transform var(--transition-medium), box-shadow var(--transition-medium);
  
  &:hover {
    transform: translateY(-5px);
    box-shadow: var(--box-shadow-medium);
    
    .skill-card-icon {
      transform: scale(1.1);
      
      i {
        color: var(--accent-color);
      }
    }
  }
  
  &-icon {
    font-size: 2.5rem;
    color: var(--primary-color);
    margin-bottom: var(--spacing-md);
    transition: transform var(--transition-medium);
    
    i {
      transition: color var(--transition-medium);
    }
  }
  
  &-title {
    margin-bottom: var(--spacing-sm);
    font-size: 1.2rem;
  }
  
  &-description {
    color: var(--gray-dark);
    line-height: 1.6;
    margin-bottom: 0;
  }
}

.languages-grid {
  display: flex;
  flex-wrap: wrap;
  gap: var(--spacing-lg);
  justify-content: center;
  margin-top: var(--spacing-lg);
}

.language-item {
  display: flex;
  align-items: center;
  background-color: var(--background-light);
  border-radius: var(--border-radius-md);
  padding: var(--spacing-md) var(--spacing-lg);
  min-width: 200px;
  box-shadow: var(--box-shadow-light);
  transition: transform var(--transition-medium), box-shadow var(--transition-medium);
  
  &:hover {
    transform: translateY(-5px);
    box-shadow: var(--box-shadow-medium);
  }
}

.language-flag {
  font-size: 2rem;
  margin-right: var(--spacing-md);
}

.language-details {
  flex: 1;
}

.language-name {
  margin: 0;
  font-size: 1.1rem;
}

.language-level {
  color: var(--gray-dark);
  font-size: 0.9rem;
}

.certifications-grid {
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(300px, 1fr));
  gap: var(--spacing-lg);
  margin-top: var(--spacing-lg);
}

.certification-item {
  display: flex;
  align-items: center;
  background-color: var(--background-light);
  border-radius: var(--border-radius-md);
  padding: var(--spacing-md);
  box-shadow: var(--box-shadow-light);
  transition: transform var(--transition-medium), box-shadow var(--transition-medium);
  
  &:hover {
    transform: translateY(-5px);
    box-shadow: var(--box-shadow-medium);
  }
}

.certification-logo {
  width: 50px;
  height: 50px;
  background: linear-gradient(135deg, var(--primary-color), var(--secondary-color));
  border-radius: 50%;
  display: flex;
  align-items: center;
  justify-content: center;
  margin-right: var(--spacing-md);
  
  i {
    font-size: 1.5rem;
    color: white;
  }
}

.certification-content {
  flex: 1;
  
  h3 {
    margin: 0 0 var(--spacing-xs) 0;
    font-size: 1.1rem;
  }
  
  .certification-issuer {
    color: var(--gray-dark);
    margin: 0;
    font-size: 0.9rem;
  }
}

.skills-cta {
  margin-top: var(--spacing-xl);
  
  .cta-container {
    background: linear-gradient(135deg, var(--primary-color), var(--secondary-color));
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
  }
}

@media (max-width: 992px) {
  .skills-grid,
  .other-skills-grid,
  .certifications-grid {
    grid-template-columns: repeat(2, 1fr);
  }
}

@media (max-width: 768px) {
  .skills-grid,
  .other-skills-grid,
  .certifications-grid {
    grid-template-columns: 1fr;
  }
  
  .languages-grid {
    flex-direction: column;
    align-items: stretch;
  }
  
  .skills-cta .cta-container {
    padding: var(--spacing-lg);
  }
}

@media (max-width: 480px) {
  .skill-header {
    flex-direction: column;
    align-items: flex-start;
  }
  
  .skill-icon {
    margin-right: 0;
    margin-bottom: var(--spacing-xs);
  }
  
  .certification-item {
    flex-direction: column;
    text-align: center;
  }
  
  .certification-logo {
    margin-right: 0;
    margin-bottom: var(--spacing-sm);
  }
}
</style> 