<script setup>
import { ref, onMounted, computed } from 'vue'
import { gsap } from 'gsap'

// Liste des projets
const projects = ref([
  {
    id: 1,
    title: 'E-commerce moderne',
    description: 'Une plateforme e-commerce complète avec panier, paiement et système d\'administration.',
    image: 'https://images.unsplash.com/photo-1661956602944-249bcd04b63f?ixlib=rb-4.0.3&ixid=MnwxMjA3fDF8MHxwaG90by1wYWdlfHx8fGVufDB8fHx8&auto=format&fit=crop&w=1170&q=80',
    tags: ['Vue.js', 'Node.js', 'MongoDB', 'Stripe'],
    category: 'web',
    link: '#',
    github: 'https://github.com/',
  },
  {
    id: 2,
    title: 'Application de gestion de tâches',
    description: 'Une application drag-and-drop pour la gestion de projets et tâches au style Trello.',
    image: 'https://images.unsplash.com/photo-1484480974693-6ca0a78fb36b?ixlib=rb-4.0.3&ixid=MnwxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHx8&auto=format&fit=crop&w=1172&q=80',
    tags: ['Vue.js', 'Vuex', 'Firebase', 'SCSS'],
    category: 'web',
    link: '#',
    github: 'https://github.com/',
  },
  {
    id: 3,
    title: 'Dashboard analytique',
    description: 'Un tableau de bord interactif pour la visualisation de données avec graphiques et statistiques en temps réel.',
    image: 'https://images.unsplash.com/photo-1551288049-bebda4e38f71?ixlib=rb-4.0.3&ixid=MnwxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHx8&auto=format&fit=crop&w=1170&q=80',
    tags: ['Vue.js', 'D3.js', 'Express', 'PostgreSQL'],
    category: 'web',
    link: '#',
    github: 'https://github.com/',
  },
  {
    id: 4,
    title: 'Site vitrine pour restaurant',
    description: 'Un site élégant avec réservation en ligne, menu dynamique et section blog.',
    image: 'https://images.unsplash.com/photo-1517248135467-4c7edcad34c4?ixlib=rb-4.0.3&ixid=MnwxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHx8&auto=format&fit=crop&w=1170&q=80',
    tags: ['Vue.js', 'GSAP', 'Netlify', 'Contentful'],
    category: 'web',
    link: '#',
    github: 'https://github.com/',
  },
  {
    id: 5,
    title: 'Application météo',
    description: 'Une application élégante de prévisions météo avec géolocalisation et animations.',
    image: 'https://images.unsplash.com/photo-1504608524841-42fe6f032b4b?ixlib=rb-4.0.3&ixid=MnwxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHx8&auto=format&fit=crop&w=765&q=80',
    tags: ['Vue.js', 'OpenWeatherAPI', 'PWA', 'Vite'],
    category: 'mobile',
    link: '#',
    github: 'https://github.com/',
  },
  {
    id: 6,
    title: 'Portfolio de photographe',
    description: 'Un portfolio visuellement impressionnant avec galerie d\'images et effets de transition.',
    image: 'https://images.unsplash.com/photo-1554080353-a576cf803bda?ixlib=rb-4.0.3&ixid=MnwxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHx8&auto=format&fit=crop&w=1074&q=80',
    tags: ['Vue.js', 'GSAP', 'Sanity.io', 'Netlify'],
    category: 'web',
    link: '#',
    github: 'https://github.com/',
  },
])

// Catégories pour le filtrage
const categories = [
  { id: 'all', name: 'Tous' },
  { id: 'web', name: 'Web' },
  { id: 'mobile', name: 'Mobile' },
  { id: 'design', name: 'Design' }
]

// État actif du filtre
const activeFilter = ref('all')

// Filtrer les projets selon la catégorie sélectionnée
const filteredProjects = computed(() => {
  if (activeFilter.value === 'all') {
    return projects.value
  }
  return projects.value.filter(project => project.category === activeFilter.value)
})

// Vue détaillée d'un projet
const selectedProject = ref(null)
const showProjectDetails = ref(false)

// Ouvrir la vue détaillée d'un projet
const openProjectDetails = (project) => {
  selectedProject.value = project
  showProjectDetails.value = true
  document.body.style.overflow = 'hidden' // Empêche le défilement du body
}

// Fermer la vue détaillée
const closeProjectDetails = () => {
  showProjectDetails.value = false
  document.body.style.overflow = 'auto' // Restaure le défilement
}

// Changer le filtre actif
const setFilter = (categoryId) => {
  activeFilter.value = categoryId
  
  // Animation des projets filtrés sans affecter la visibilité des filtres
  gsap.fromTo('.project-card', 
    { opacity: 0, y: 20 },
    { 
      opacity: 1, 
      y: 0, 
      duration: 0.5, 
      stagger: 0.1, 
      ease: 'power2.out', 
      clearProps: 'all' // Important : nettoie les propriétés après l'animation
    }
  )
}

onMounted(() => {
  // Animation du titre et sous-titre
  gsap.from('.projects-title, .projects-subtitle', {
    opacity: 0,
    y: 30,
    duration: 0.8,
    stagger: 0.2,
    clearProps: 'all' // Nettoie les propriétés après l'animation
  })
  
  // Animation des filtres - avec clearProps pour éviter les problèmes de visibilité
  gsap.from('.filter-item', {
    opacity: 0,
    y: 20,
    duration: 0.5,
    stagger: 0.1,
    delay: 0.3,
    clearProps: 'all' // Très important : s'assure que les éléments restent visibles après l'animation
  })
  
  // Animation des cartes de projet
  gsap.from('.project-card', {
    opacity: 0,
    y: 50,
    duration: 0.6,
    stagger: 0.1,
    delay: 0.5,
    clearProps: 'all' // Nettoie les propriétés après l'animation
  })
})
</script>

<template>
  <div class="projects">
    <div class="container">
      <header class="projects-header">
        <h1 class="projects-title section-title">Mes projets</h1>
        <p class="projects-subtitle">Découvrez une sélection de mes travaux récents en développement web et mobile.</p>
      </header>
      
      <div class="projects-filter">
        <ul class="filter-list">
          <li 
            v-for="category in categories" 
            :key="category.id" 
            class="filter-item"
            :class="{ active: activeFilter === category.id }"
            @click="setFilter(category.id)"
          >
            {{ category.name }}
          </li>
        </ul>
      </div>
      
      <div class="projects-grid">
        <div 
          v-for="project in filteredProjects" 
          :key="project.id" 
          class="project-card"
          @click="openProjectDetails(project)"
        >
          <div class="project-image">
            <img :src="project.image" :alt="project.title">
          </div>
          <div class="project-overlay">
            <h3 class="project-title">{{ project.title }}</h3>
            <div class="project-tags">
              <span v-for="(tag, index) in project.tags" :key="index" class="project-tag">{{ tag }}</span>
            </div>
            <div class="project-actions">
              <button class="project-btn">Voir détails</button>
            </div>
          </div>
        </div>
      </div>
      
      <!-- Si aucun projet ne correspond au filtre -->
      <div v-if="filteredProjects.length === 0" class="no-projects">
        <i class="fas fa-folder-open"></i>
        <p>Aucun projet trouvé dans cette catégorie.</p>
      </div>
      
      <!-- CTA -->
      <section class="projects-cta">
        <div class="cta-container">
          <h2>Vous avez un projet en tête?</h2>
          <p>N'hésitez pas à me contacter pour discuter de vos idées et voir comment je peux vous aider à les concrétiser.</p>
          <router-link to="/contact" class="btn btn-primary">Me contacter</router-link>
        </div>
      </section>
    </div>
    
    <!-- Vue détaillée d'un projet -->
    <div class="project-details-overlay" v-if="showProjectDetails" @click="closeProjectDetails">
      <div class="project-details-container" @click.stop>
        <button class="close-btn" @click="closeProjectDetails">
          <i class="fas fa-times"></i>
        </button>
        
        <div class="project-details-content" v-if="selectedProject">
          <div class="project-details-image">
            <img :src="selectedProject.image" :alt="selectedProject.title">
          </div>
          
          <div class="project-details-info">
            <h2>{{ selectedProject.title }}</h2>
            
            <div class="project-details-tags">
              <span v-for="(tag, index) in selectedProject.tags" :key="index" class="project-tag">{{ tag }}</span>
            </div>
            
            <p class="project-details-description">{{ selectedProject.description }}</p>
            
            <div class="project-features">
              <h3>Caractéristiques principales</h3>
              <ul>
                <li><i class="fas fa-check"></i> Interface utilisateur intuitive et réactive</li>
                <li><i class="fas fa-check"></i> Architecture robuste et évolutive</li>
                <li><i class="fas fa-check"></i> Performance optimisée pour une expérience fluide</li>
                <li><i class="fas fa-check"></i> Design entièrement responsive sur tous les appareils</li>
              </ul>
            </div>
            
            <div class="project-details-links">
              <a :href="selectedProject.link" target="_blank" rel="noopener noreferrer" class="btn btn-primary">
                <i class="fas fa-external-link-alt"></i> Voir le site
              </a>
              <a :href="selectedProject.github" target="_blank" rel="noopener noreferrer" class="btn btn-outline">
                <i class="fab fa-github"></i> Code source
              </a>
            </div>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<style lang="scss" scoped>
.projects {
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
}

.projects-filter {
  margin-bottom: var(--spacing-xl);
  
  .filter-list {
    display: flex;
    justify-content: center;
    list-style: none;
    gap: var(--spacing-md);
    flex-wrap: wrap;
    margin: 0;
    padding: 0;
  }
  
  .filter-item {
    padding: 0.5rem 1.25rem;
    border-radius: var(--border-radius-md);
    background-color: var(--gray-light);
    cursor: pointer;
    transition: all var(--transition-medium);
    font-weight: 500;
    opacity: 1 !important; /* Assure que les filtres restent toujours visibles */
    
    &:hover {
      background-color: var(--primary-color);
      color: var(--text-light);
    }
    
    &.active {
      background-color: var(--primary-color);
      color: var(--text-light);
    }
  }
}

.projects-grid {
  display: grid;
  grid-template-columns: repeat(auto-fill, minmax(350px, 1fr));
  gap: var(--spacing-lg);
  margin-bottom: var(--spacing-xl);
}

.project-card {
  position: relative;
  border-radius: var(--border-radius-md);
  overflow: hidden;
  box-shadow: var(--box-shadow-light);
  cursor: pointer;
  height: 280px;
  
  &:hover .project-overlay {
    opacity: 1;
  }
  
  &:hover .project-image img {
    transform: scale(1.05);
  }
}

.project-image {
  height: 100%;
  width: 100%;
  
  img {
    width: 100%;
    height: 100%;
    object-fit: cover;
    transition: transform var(--transition-medium);
  }
}

.project-overlay {
  position: absolute;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
  background: linear-gradient(to bottom, rgba(0, 0, 0, 0.2), rgba(0, 0, 0, 0.8));
  display: flex;
  flex-direction: column;
  justify-content: flex-end;
  padding: var(--spacing-lg);
  opacity: 0;
  transition: opacity var(--transition-medium);
  color: var(--text-light);
}

.project-title {
  font-size: 1.5rem;
  margin-bottom: var(--spacing-sm);
}

.project-tags {
  display: flex;
  flex-wrap: wrap;
  gap: 0.5rem;
  margin-bottom: var(--spacing-md);
}

.project-tag {
  background-color: rgba(255, 255, 255, 0.2);
  padding: 0.25rem 0.75rem;
  border-radius: var(--border-radius-sm);
  font-size: 0.8rem;
  backdrop-filter: blur(4px);
}

.project-actions {
  display: flex;
  gap: var(--spacing-sm);
}

.project-btn {
  background-color: var(--primary-color);
  color: var(--text-light);
  border: none;
  padding: 0.5rem 1rem;
  border-radius: var(--border-radius-md);
  cursor: pointer;
  font-weight: 500;
  transition: all var(--transition-medium);
  
  &:hover {
    background-color: var(--secondary-color);
    transform: translateY(-2px);
  }
}

.no-projects {
  text-align: center;
  padding: var(--spacing-xl) 0;
  color: var(--gray-dark);
  
  i {
    font-size: 3rem;
    margin-bottom: var(--spacing-md);
  }
  
  p {
    font-size: 1.2rem;
  }
}

.projects-cta {
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

.project-details-overlay {
  position: fixed;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
  background-color: rgba(0, 0, 0, 0.8);
  z-index: 1000;
  display: flex;
  align-items: center;
  justify-content: center;
  padding: var(--spacing-md);
}

.project-details-container {
  background-color: var(--background-light);
  border-radius: var(--border-radius-lg);
  max-width: 1000px;
  width: 100%;
  max-height: 90vh;
  overflow-y: auto;
  position: relative;
  box-shadow: var(--box-shadow-heavy);
}

.close-btn {
  position: absolute;
  top: 1rem;
  right: 1rem;
  background-color: rgba(0, 0, 0, 0.5);
  color: white;
  border: none;
  width: 40px;
  height: 40px;
  border-radius: 50%;
  display: flex;
  align-items: center;
  justify-content: center;
  cursor: pointer;
  z-index: 10;
  font-size: 1.2rem;
  transition: all var(--transition-fast);
  
  &:hover {
    background-color: var(--accent-color);
  }
}

.project-details-content {
  display: grid;
  grid-template-columns: 1fr 1fr;
  
  @media (max-width: 768px) {
    grid-template-columns: 1fr;
  }
}

.project-details-image {
  img {
    width: 100%;
    height: 100%;
    object-fit: cover;
    border-top-left-radius: var(--border-radius-lg);
    border-bottom-left-radius: var(--border-radius-lg);
    
    @media (max-width: 768px) {
      border-radius: 0;
      border-top-left-radius: var(--border-radius-lg);
      border-top-right-radius: var(--border-radius-lg);
      max-height: 300px;
    }
  }
}

.project-details-info {
  padding: var(--spacing-xl);
  
  h2 {
    margin-bottom: var(--spacing-sm);
    font-size: 2rem;
  }
  
  .project-details-tags {
    display: flex;
    flex-wrap: wrap;
    gap: 0.5rem;
    margin-bottom: var(--spacing-md);
    
    .project-tag {
      background-color: var(--gray-light);
      color: var(--gray-dark);
    }
  }
  
  .project-details-description {
    margin-bottom: var(--spacing-lg);
    line-height: 1.8;
  }
}

.project-features {
  margin-bottom: var(--spacing-lg);
  
  h3 {
    margin-bottom: var(--spacing-sm);
    font-size: 1.25rem;
  }
  
  ul {
    list-style: none;
    
    li {
      margin-bottom: var(--spacing-sm);
      display: flex;
      align-items: center;
      
      i {
        color: var(--success-color);
        margin-right: var(--spacing-sm);
      }
    }
  }
}

.project-details-links {
  display: flex;
  gap: var(--spacing-md);
  
  .btn {
    display: flex;
    align-items: center;
    gap: 0.5rem;
    
    i {
      font-size: 0.9rem;
    }
  }
  
  @media (max-width: 480px) {
    flex-direction: column;
  }
}

@media (max-width: 992px) {
  .projects-grid {
    grid-template-columns: repeat(auto-fill, minmax(300px, 1fr));
  }
}

@media (max-width: 768px) {
  .projects-grid {
    grid-template-columns: repeat(auto-fill, minmax(250px, 1fr));
  }
  
  .project-card {
    height: 250px;
  }
}

@media (max-width: 480px) {
  .projects-grid {
    grid-template-columns: 1fr;
  }
  
  .project-card {
    height: 220px;
  }
  
  .project-overlay {
    opacity: 1;
    background: linear-gradient(to bottom, rgba(0, 0, 0, 0.1), rgba(0, 0, 0, 0.7));
  }
}
</style> 