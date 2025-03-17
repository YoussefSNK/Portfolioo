<script setup>
import { ref, onMounted } from 'vue'
import { gsap } from 'gsap'

// États du formulaire
const form = ref({
  name: '',
  email: '',
  subject: '',
  message: ''
})

const isSubmitting = ref(false)
const formSubmitted = ref(false)
const formError = ref(false)

// Validation simple
const errors = ref({
  name: '',
  email: '',
  subject: '',
  message: ''
})

const validateForm = () => {
  let isValid = true
  errors.value = {
    name: '',
    email: '',
    subject: '',
    message: ''
  }
  
  if (!form.value.name.trim()) {
    errors.value.name = 'Le nom est requis'
    isValid = false
  }
  
  if (!form.value.email.trim()) {
    errors.value.email = 'L\'email est requis'
    isValid = false
  } else if (!/^[^\s@]+@[^\s@]+\.[^\s@]+$/.test(form.value.email)) {
    errors.value.email = 'Veuillez entrer un email valide'
    isValid = false
  }
  
  if (!form.value.subject.trim()) {
    errors.value.subject = 'Le sujet est requis'
    isValid = false
  }
  
  if (!form.value.message.trim()) {
    errors.value.message = 'Le message est requis'
    isValid = false
  }
  
  return isValid
}

// Gestion de l'envoi du formulaire
const submitForm = () => {
  if (!validateForm()) return
  
  isSubmitting.value = true
  
  // Simuler l'envoi du formulaire
  setTimeout(() => {
    isSubmitting.value = false
    formSubmitted.value = true
    
    // Réinitialiser le formulaire
    form.value = {
      name: '',
      email: '',
      subject: '',
      message: ''
    }
    
    // Afficher le message de succès pendant 5 secondes
    setTimeout(() => {
      formSubmitted.value = false
    }, 5000)
  }, 1500)
}

onMounted(() => {
  // Animation du titre et du sous-titre
  gsap.from('.contact-title, .contact-subtitle', {
    opacity: 0,
    y: 30,
    duration: 0.8,
    stagger: 0.2
  })
  
  // Animation des sections
  gsap.from('.contact-form-container, .contact-info-container', {
    opacity: 0,
    y: 50,
    duration: 0.8,
    stagger: 0.3,
    delay: 0.3
  })
  
  // Animation des éléments de contact
  gsap.from('.contact-item', {
    opacity: 0,
    y: 20,
    duration: 0.5,
    stagger: 0.1,
    delay: 0.8
  })
})
</script>

<template>
  <div class="contact">
    <div class="container">
      <header class="contact-header">
        <h1 class="contact-title section-title">Contact</h1>
        <p class="contact-subtitle">Vous avez une question ou un projet en tête? N'hésitez pas à me contacter!</p>
      </header>
      
      <div class="contact-content">
        <div class="contact-form-container">
          <h2>Envoyez-moi un message</h2>
          
          <!-- Message de succès -->
          <div v-if="formSubmitted" class="form-success">
            <i class="fas fa-check-circle"></i>
            <h3>Message envoyé!</h3>
            <p>Merci pour votre message. Je vous répondrai dans les plus brefs délais.</p>
          </div>
          
          <!-- Message d'erreur global -->
          <div v-if="formError" class="form-error">
            <i class="fas fa-exclamation-circle"></i>
            <h3>Erreur</h3>
            <p>Une erreur s'est produite lors de l'envoi du message. Veuillez réessayer.</p>
          </div>
          
          <!-- Formulaire de contact -->
          <form @submit.prevent="submitForm" v-if="!formSubmitted">
            <div class="form-group">
              <label for="name">Nom</label>
              <div class="input-container">
                <i class="fas fa-user"></i>
                <input 
                  type="text" 
                  id="name" 
                  v-model="form.name" 
                  placeholder="Votre nom" 
                  :class="{ 'input-error': errors.name }"
                >
              </div>
              <p v-if="errors.name" class="error-message">{{ errors.name }}</p>
            </div>
            
            <div class="form-group">
              <label for="email">Email</label>
              <div class="input-container">
                <i class="fas fa-envelope"></i>
                <input 
                  type="email" 
                  id="email" 
                  v-model="form.email" 
                  placeholder="Votre email" 
                  :class="{ 'input-error': errors.email }"
                >
              </div>
              <p v-if="errors.email" class="error-message">{{ errors.email }}</p>
            </div>
            
            <div class="form-group">
              <label for="subject">Sujet</label>
              <div class="input-container">
                <i class="fas fa-bookmark"></i>
                <input 
                  type="text" 
                  id="subject" 
                  v-model="form.subject" 
                  placeholder="Sujet de votre message" 
                  :class="{ 'input-error': errors.subject }"
                >
              </div>
              <p v-if="errors.subject" class="error-message">{{ errors.subject }}</p>
            </div>
            
            <div class="form-group">
              <label for="message">Message</label>
              <div class="textarea-container">
                <textarea 
                  id="message" 
                  v-model="form.message" 
                  placeholder="Votre message" 
                  rows="6" 
                  :class="{ 'input-error': errors.message }"
                ></textarea>
              </div>
              <p v-if="errors.message" class="error-message">{{ errors.message }}</p>
            </div>
            
            <button type="submit" class="btn btn-primary" :disabled="isSubmitting">
              <div v-if="isSubmitting" class="spinner"></div>
              <span v-else>Envoyer</span>
            </button>
          </form>
        </div>
        
        <div class="contact-info-container">
          <h2>Mes coordonnées</h2>
          
          <div class="contact-items">
            <div class="contact-item">
              <div class="contact-icon">
                <i class="fas fa-map-marker-alt"></i>
              </div>
              <div class="contact-text">
                <h3>Localisation</h3>
                <p>Paris, France</p>
              </div>
            </div>
            
            <div class="contact-item">
              <div class="contact-icon">
                <i class="fas fa-envelope"></i>
              </div>
              <div class="contact-text">
                <h3>Email</h3>
                <p><a href="mailto:contact@johndoe.com">contact@johndoe.com</a></p>
              </div>
            </div>
            
            <div class="contact-item">
              <div class="contact-icon">
                <i class="fas fa-phone-alt"></i>
              </div>
              <div class="contact-text">
                <h3>Téléphone</h3>
                <p><a href="tel:+33123456789">+33 1 23 45 67 89</a></p>
              </div>
            </div>
          </div>
          
          <div class="social-links">
            <h3>Suivez-moi</h3>
            <div class="social-icons">
              <a href="https://github.com/" target="_blank" rel="noopener noreferrer" class="social-icon">
                <i class="fab fa-github"></i>
              </a>
              <a href="https://linkedin.com/" target="_blank" rel="noopener noreferrer" class="social-icon">
                <i class="fab fa-linkedin-in"></i>
              </a>
              <a href="https://twitter.com/" target="_blank" rel="noopener noreferrer" class="social-icon">
                <i class="fab fa-twitter"></i>
              </a>
              <a href="https://dribbble.com/" target="_blank" rel="noopener noreferrer" class="social-icon">
                <i class="fab fa-dribbble"></i>
              </a>
            </div>
          </div>
          
          <div class="availability">
            <h3>Disponibilité</h3>
            <div class="availability-status available">
              <span class="status-dot"></span>
              <span class="status-text">Disponible pour de nouveaux projets</span>
            </div>
          </div>
        </div>
      </div>
      
      <div class="map-container">
        <h2>Me trouver</h2>
        <div class="map-frame">
          <iframe src="https://www.google.com/maps/embed?pb=!1m18!1m12!1m3!1d83998.9472264258!2d2.277020137428867!3d48.85883773935406!2m3!1f0!2f0!3f0!3m2!1i1024!2i768!4f13.1!3m3!1m2!1s0x47e66e1f06e2b70f%3A0x40b82c3688c9460!2sParis%2C%20France!5e0!3m2!1sfr!2sfr!4v1685622597351!5m2!1sfr!2sfr" 
            width="100%" 
            height="450" 
            style="border:0;" 
            allowfullscreen="" 
            loading="lazy" 
            referrerpolicy="no-referrer-when-downgrade">
          </iframe>
        </div>
      </div>
    </div>
  </div>
</template>

<style lang="scss" scoped>
.contact {
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
  
  &-content {
    display: grid;
    grid-template-columns: 1fr 1fr;
    gap: var(--spacing-xl);
    margin-bottom: var(--spacing-xl);
    
    @media (max-width: 992px) {
      grid-template-columns: 1fr;
    }
  }
}

.contact-form-container,
.contact-info-container {
  background-color: var(--background-light);
  border-radius: var(--border-radius-lg);
  padding: var(--spacing-xl);
  box-shadow: var(--box-shadow-light);
  
  h2 {
    margin-bottom: var(--spacing-lg);
    font-size: 1.8rem;
    position: relative;
    padding-bottom: var(--spacing-sm);
    
    &::after {
      content: '';
      position: absolute;
      bottom: 0;
      left: 0;
      width: 50px;
      height: 3px;
      background-color: var(--primary-color);
      border-radius: var(--border-radius-sm);
    }
  }
}

.form-group {
  margin-bottom: var(--spacing-md);
  
  label {
    display: block;
    margin-bottom: var(--spacing-xs);
    font-weight: 500;
  }
}

.input-container,
.textarea-container {
  position: relative;
  
  i {
    position: absolute;
    top: 50%;
    left: var(--spacing-md);
    transform: translateY(-50%);
    color: var(--gray-medium);
  }
  
  input, textarea {
    width: 100%;
    padding: var(--spacing-md) var(--spacing-md) var(--spacing-md) calc(var(--spacing-md) * 2 + 1rem);
    border: 1px solid var(--gray-light);
    border-radius: var(--border-radius-md);
    font-family: var(--font-primary);
    transition: all var(--transition-medium);
    
    &:focus {
      outline: none;
      border-color: var(--primary-color);
      box-shadow: 0 0 0 3px rgba(58, 134, 255, 0.2);
    }
    
    &.input-error {
      border-color: var(--error-color);
      
      &:focus {
        box-shadow: 0 0 0 3px rgba(229, 56, 59, 0.2);
      }
    }
  }
}

.textarea-container {
  i {
    top: var(--spacing-md);
    transform: none;
  }
  
  textarea {
    resize: vertical;
  }
}

.error-message {
  color: var(--error-color);
  font-size: 0.875rem;
  margin-top: var(--spacing-xs);
  margin-bottom: 0;
}

.form-success,
.form-error {
  background-color: #f0f9f4;
  border-radius: var(--border-radius-md);
  padding: var(--spacing-lg);
  text-align: center;
  margin-bottom: var(--spacing-lg);
  
  i {
    font-size: 3rem;
    color: var(--success-color);
    margin-bottom: var(--spacing-md);
  }
  
  h3 {
    margin-bottom: var(--spacing-sm);
  }
  
  p {
    color: var(--gray-dark);
    margin-bottom: 0;
  }
}

.form-error {
  background-color: #fdf1f1;
  
  i {
    color: var(--error-color);
  }
}

.spinner {
  width: 20px;
  height: 20px;
  border: 2px solid rgba(255, 255, 255, 0.3);
  border-radius: 50%;
  border-top-color: white;
  animation: spin 0.8s linear infinite;
  margin: 0 auto;
}

@keyframes spin {
  0% { transform: rotate(0deg); }
  100% { transform: rotate(360deg); }
}

.contact-items {
  margin-bottom: var(--spacing-lg);
}

.contact-item {
  display: flex;
  margin-bottom: var(--spacing-md);
  
  &:last-child {
    margin-bottom: 0;
  }
}

.contact-icon {
  width: 50px;
  height: 50px;
  background: linear-gradient(135deg, var(--primary-color), var(--secondary-color));
  border-radius: 50%;
  display: flex;
  align-items: center;
  justify-content: center;
  margin-right: var(--spacing-md);
  
  i {
    font-size: 1.25rem;
    color: white;
  }
}

.contact-text {
  h3 {
    font-size: 1.1rem;
    margin: 0 0 var(--spacing-xs) 0;
  }
  
  p {
    color: var(--gray-dark);
    margin: 0;
    
    a {
      color: var(--primary-color);
      transition: color var(--transition-fast);
      
      &:hover {
        color: var(--accent-color);
      }
    }
  }
}

.social-links {
  margin-bottom: var(--spacing-lg);
  
  h3 {
    font-size: 1.1rem;
    margin-bottom: var(--spacing-md);
  }
}

.social-icons {
  display: flex;
  gap: var(--spacing-sm);
}

.social-icon {
  width: 40px;
  height: 40px;
  background-color: var(--gray-light);
  border-radius: 50%;
  display: flex;
  align-items: center;
  justify-content: center;
  color: var(--gray-dark);
  transition: all var(--transition-medium);
  
  &:hover {
    background-color: var(--primary-color);
    color: white;
    transform: translateY(-3px);
  }
}

.availability {
  h3 {
    font-size: 1.1rem;
    margin-bottom: var(--spacing-md);
  }
  
  &-status {
    display: flex;
    align-items: center;
    
    &.available .status-dot {
      background-color: var(--success-color);
    }
    
    &.busy .status-dot {
      background-color: var(--warning-color);
    }
    
    &.unavailable .status-dot {
      background-color: var(--error-color);
    }
  }
  
  .status-dot {
    width: 12px;
    height: 12px;
    border-radius: 50%;
    margin-right: var(--spacing-sm);
  }
  
  .status-text {
    color: var(--gray-dark);
  }
}

.map-container {
  margin-top: var(--spacing-xl);
  
  h2 {
    margin-bottom: var(--spacing-lg);
    font-size: 1.8rem;
    position: relative;
    padding-bottom: var(--spacing-sm);
    
    &::after {
      content: '';
      position: absolute;
      bottom: 0;
      left: 0;
      width: 50px;
      height: 3px;
      background-color: var(--primary-color);
      border-radius: var(--border-radius-sm);
    }
  }
}

.map-frame {
  border-radius: var(--border-radius-lg);
  overflow: hidden;
  box-shadow: var(--box-shadow-light);
  height: 450px;
  
  iframe {
    width: 100%;
    height: 100%;
    border: 0;
  }
}

@media (max-width: 768px) {
  .contact-form-container,
  .contact-info-container {
    padding: var(--spacing-lg);
  }
  
  .map-frame {
    height: 350px;
  }
}

@media (max-width: 480px) {
  .social-icons {
    justify-content: space-between;
  }
}
</style> 