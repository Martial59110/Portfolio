<script lang="ts">
  import { onMount } from 'svelte';
  import emailjs from '@emailjs/browser';
  
  let formSubmitted = $state(false);
  let formError = $state(false);
  let loading = $state(false);

  const socialLinks = [
    { 
      name: 'GitHub',
      icon: 'fab fa-github',
      url: 'https://github.com/Martial59110',
      color: '#EA4335'
    },
    { 
      name: 'LinkedIn',
      icon: 'fab fa-linkedin',
      url: 'https://www.linkedin.com/in/martialfloquet/',
      color: '#EA4335'
    },
    { 
      name: 'Email',
      icon: 'fas fa-envelope',
      url: 'mailto:floquet.martial@gmail.com',
      color: '#EA4335'
    }
  ];

  async function handleSubmit(event: SubmitEvent) {
    event.preventDefault();
    loading = true;
    
    const form = event.target as HTMLFormElement;
    const formData = new FormData(form);
    const templateParams = {
      from_name: formData.get('name'),
      from_email: formData.get('email'),
      message: `Message de : ${formData.get('name')}\nEmail : ${formData.get('email')}\n\nMessage :\n${formData.get('message')}`
    };

    try {
      await emailjs.send(
        'service_7fhllew',
        'template_2oo46sy',
        templateParams,
        'KivnHqgnpUCX8fCYw'
      );
      formSubmitted = true;
      form.reset();
    } catch (error) {
      formError = true;
      console.error('Erreur lors de l\'envoi:', error);
      const errorMessage = document.querySelector('.error-message p');
      if (errorMessage) {
        errorMessage.textContent = "Une erreur est survenue lors de l'envoi du message. Veuillez me contacter directement par email : floquet.martial@gmail.com";
      }
    } finally {
      loading = false;
    }
  }

  onMount(() => {
    emailjs.init('KivnHqgnpUCX8fCYw');
  });
</script>

<section id="contact" class="contact py-6 bg-dark">
  <div class="container">
    <div class="text-center mb-5">
      <h2 class="display-4 text-white mb-3">Me contacter</h2>
      <div class="separator"></div>
      <p class="lead text-white-50">N'hésitez pas à me contacter pour toute question.</p>
    </div>

    <div class="row justify-content-center">
      <div class="col-lg-8">
        <div class="contact-wrapper">
          <!-- Carte de contact -->
          <div class="contact-card">
            {#if formSubmitted}
              <div class="success-message">
                <i class="fas fa-check-circle"></i>
                <h3>Message envoyé !</h3>
                <p>Merci de m'avoir contacté. Je vous répondrai dans les plus brefs délais.</p>
              </div>
            {:else if formError}
              <div class="error-message">
                <i class="fas fa-exclamation-circle"></i>
                <h3>Une erreur est survenue</h3>
                <p>Veuillez réessayer plus tard ou me contacter directement par email.</p>
              </div>
            {:else}
              <form on:submit={handleSubmit} class="contact-form" autocomplete="off">
                <div class="form-floating mb-4">
                  <input 
                    type="text" 
                    class="form-control" 
                    id="name" 
                    name="name"
                    placeholder="Votre nom" 
                    autocomplete="off"
                    required
                  >
                  <label for="name">
                    <i class="fas fa-user me-2"></i>
                    Votre nom
                  </label>
                </div>

                <div class="form-floating mb-4">
                  <input 
                    type="email" 
                    class="form-control" 
                    id="email" 
                    name="email"
                    placeholder="Votre email" 
                    autocomplete="off"
                    required
                  >
                  <label for="email">
                    <i class="fas fa-envelope me-2"></i>
                    Votre email
                  </label>
                </div>

                <div class="form-floating mb-4">
                  <textarea 
                    class="form-control" 
                    id="message" 
                    name="message"
                    placeholder=" "
                    autocomplete="off"
                    style="height: 150px; min-height: 150px; resize: vertical;" 
                    required
                  ></textarea>
                  <label for="message">
                    <i class="fas fa-comment me-2"></i>
                    Votre message
                  </label>
                </div>

                <button type="submit" class="btn btn-gradient w-100" disabled={loading}>
                  {#if loading}
                    <div class="spinner-border spinner-border-sm me-2" role="status">
                      <span class="visually-hidden">Chargement...</span>
                    </div>
                    Envoi en cours...
                  {:else}
                    <span>Envoyer le message</span>
                    <div class="btn-gradient-hover"></div>
                  {/if}
                </button>
              </form>
            {/if}
          </div>

          <!-- Réseaux sociaux -->
          <div class="social-links-wrapper mt-5">
            <h3 class="text-center text-white mb-4">Me retrouver ailleurs</h3>
            <div class="social-links">
              {#each socialLinks as link}
                <a 
                  href={link.url} 
                  class="social-link" 
                  target="_blank" 
                  rel="noopener noreferrer"
                  style="--link-color: {link.color}"
                >
                  <i class="{link.icon}"></i>
                  <span>{link.name}</span>
                </a>
              {/each}
            </div>
          </div>
        </div>
      </div>
    </div>
  </div>
</section>

<style lang="postcss">
  .separator {
    width: 80px;
    height: 4px;
    background: linear-gradient(135deg, var(--primary), var(--secondary));
    margin: 1.5rem auto;
    border-radius: 2px;
  }

  .contact-wrapper {
    position: relative;
    z-index: 1;
  }

  .contact-card {
    background: rgba(255, 255, 255, 0.05);
    border-radius: 20px;
    padding: 2.5rem;
    border: 1px solid rgba(255, 255, 255, 0.1);
    box-shadow: 0 10px 30px rgba(0, 0, 0, 0.2);
    backdrop-filter: blur(10px);
    transition: transform 0.3s ease, box-shadow 0.3s ease;
  }

  .contact-card:hover {
    transform: translateY(-5px);
    box-shadow: 0 15px 40px rgba(0, 0, 0, 0.3);
  }

  .form-control {
    background: rgba(255, 255, 255, 0.05);
    border: 1px solid rgba(255, 255, 255, 0.1);
    color: white;
    transition: all 0.3s ease;
  }

  .form-control:focus {
    background: rgba(255, 255, 255, 0.08);
    border-color: var(--primary);
    box-shadow: 0 0 0 0.25rem rgba(74, 144, 226, 0.25);
    color: white;
  }

  .form-floating label {
    color: rgba(255, 255, 255, 0.7);
    display: flex;
    align-items: center;
  }

  .form-floating > .form-control:focus ~ label,
  .form-floating > .form-control:not(:placeholder-shown) ~ label {
    color: var(--primary);
    transform: scale(0.85) translateY(-1rem);
  }

  .success-message,
  .error-message {
    text-align: center;
    padding: 2rem;
    color: white;
  }

  .success-message i,
  .error-message i {
    font-size: 3rem;
    margin-bottom: 1rem;
  }

  .success-message i {
    color: #4CAF50;
  }

  .error-message i {
    color: #f44336;
  }

  .social-links {
    display: flex;
    justify-content: center;
    gap: 1.5rem;
    flex-wrap: wrap;
  }

  .social-link {
    display: flex;
    align-items: center;
    gap: 0.5rem;
    padding: 0.8rem 1.5rem;
    border-radius: 10px;
    background: rgba(255, 255, 255, 0.05);
    color: white;
    text-decoration: none;
    transition: all 0.3s ease;
    border: 1px solid rgba(255, 255, 255, 0.1);
  }

  .social-link:hover {
    background: rgba(255, 255, 255, 0.1);
    transform: translateY(-3px);
    color: var(--link-color);
    border-color: var(--link-color);
  }

  .social-link i {
    font-size: 1.2rem;
  }

  @keyframes gradient {
    0% { background-position: 0% 50%; }
    50% { background-position: 100% 50%; }
    100% { background-position: 0% 50%; }
  }

  .btn-gradient {
    position: relative;
    background: linear-gradient(135deg, var(--primary), var(--secondary));
    border: none;
    color: white;
    overflow: hidden;
    z-index: 1;
    transition: all 0.3s ease;
  }

  .btn-gradient:hover {
    transform: translateY(-2px);
    box-shadow: 0 5px 15px rgba(74, 144, 226, 0.3);
  }

  .btn-gradient:disabled {
    opacity: 0.7;
    cursor: not-allowed;
    transform: none;
  }

  .spinner-border {
    width: 1rem;
    height: 1rem;
    border-width: 0.15em;
  }

  .form-floating textarea.form-control {
    padding-top: 2.5rem;
    padding-bottom: 0.625rem;
  }

  .form-floating > textarea ~ label {
    padding: 1rem 0.75rem;
    height: auto;
    transform-origin: 0 0;
  }

  .form-floating > textarea:focus ~ label,
  .form-floating > textarea:not(:placeholder-shown) ~ label {
    opacity: 0.65;
    transform: scale(0.85) translateY(-0.5rem) translateX(0.15rem);
  }

  .form-floating textarea.form-control::placeholder {
    color: transparent;
  }

  .form-floating textarea.form-control:focus::placeholder {
    color: rgba(255, 255, 255, 0.5);
  }
</style> 