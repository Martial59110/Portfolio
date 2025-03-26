<script lang="ts">
  let { name, title, description } = $props<{
    name: string;
    title: string;
    description: string;
  }>();

  let gameStarted = $state(false);
  let gameFrame: HTMLIFrameElement;
  let isLoading = $state(false);

  function startGame() {
    isLoading = true;
    gameStarted = true;
    // Donner plus de temps pour que l'iframe se charge
    setTimeout(() => {
      if (gameFrame) {
        gameFrame.contentWindow?.postMessage({ type: 'start-game' }, '*');
      }
      isLoading = false;
    }, 500);
  }
</script>

<section class="hero min-vh-100 d-flex align-items-center position-relative overflow-hidden">
  <div class="position-absolute w-100 h-100 top-0 start-0" id="particles">
    <div class="glowing-dots"></div>
  </div>
  <div class="container position-relative">
    <div class="row align-items-center" id="about">
      <div class="col-lg-7">
        <div class="glitch-wrapper">
          <h1 class="display-3 fw-bold text-white glitch" data-text={name}>{name}</h1>
        </div>
        <p class="lead text-white-50 mb-2 typing-text">{title}</p>
        <p class="cyber-text text-gradient mb-4">Passionné par la programmation en tout genre et les jeux vidéo !</p>
        <div class="d-flex gap-3">
          <a href="#contact" class="btn btn-gradient btn-lg">
            <span>Me contacter</span>
            <div class="btn-gradient-hover"></div>
          </a>
          <a href="#projects" class="btn btn-outline-light btn-lg border-gradient">
            Voir mes projets
          </a>
        </div>
      </div>
      <div class="col-lg-5 d-none d-lg-block">
        <div class="game-container">
          <div class="game-frame">
            <div id="construct-game" class="game-canvas">
              {#if !gameStarted}
                <div class="game-placeholder">
                  <div class="game-loading">Chargement du jeu...</div>
                </div>
              {:else if isLoading}
                <div class="game-placeholder">
                  <div class="game-loading">Démarrage du jeu...</div>
                </div>
              {:else}
                <iframe 
                  bind:this={gameFrame}
                  src="game/index.html" 
                  width="100%" 
                  height="100%" 
                  frameborder="0" 
                  title="Mini-jeu"
                ></iframe>
              {/if}
            </div>
          </div>
        </div>
        <div class="game-controls mt-3">
          {#if !gameStarted}
            <button class="btn btn-primary btn-lg w-100 game-start-btn" onclick={startGame}>
              <i class="fas fa-play me-2"></i>Démarrer le jeu
            </button>
          {:else}
            <div class="game-control-hint">
              <i class="fas fa-gamepad"></i>
              <span>Utilisez le clavier et la souris pour jouer</span>
            </div>
          {/if}
        </div>
      </div>
    </div>
  </div>
</section>

<style>
  .game-container {
    background: rgba(255, 255, 255, 0.03);
    border-radius: 20px;
    padding: 20px;
    border: 1px solid rgba(255, 255, 255, 0.1);
    box-shadow: 0 0 30px rgba(74, 144, 226, 0.1);
    backdrop-filter: blur(10px);
    transition: transform 0.3s ease, box-shadow 0.3s ease;
  }

  .game-container:hover {
    transform: translateY(-5px);
    box-shadow: 0 0 40px rgba(74, 144, 226, 0.2);
    border-color: var(--primary);
  }

  .game-frame {
    aspect-ratio: 4/3;
    width: 100%;
    background: rgba(0, 0, 0, 0.3);
    border-radius: 10px;
    overflow: hidden;
    position: relative;
  }

  .game-canvas {
    width: 100%;
    height: 100%;
    display: flex;
    align-items: center;
    justify-content: center;
  }

  .game-placeholder {
    color: rgba(255, 255, 255, 0.7);
    text-align: center;
    font-size: 0.9rem;
    padding: 20px;
  }

  .game-loading {
    display: inline-block;
    position: relative;
  }

  .game-loading:after {
    content: '...';
    position: absolute;
    animation: loading-dots 1.5s infinite;
  }

  .game-controls {
    text-align: center;
  }

  .game-start-btn {
    background: linear-gradient(135deg, var(--primary), var(--secondary));
    border: none;
    padding: 12px 24px;
    font-weight: 500;
    transition: all 0.3s ease;
  }

  .game-start-btn:hover {
    transform: translateY(-2px);
    box-shadow: 0 5px 15px rgba(74, 144, 226, 0.3);
  }

  .game-start-btn i {
    font-size: 1.1em;
  }

  .game-control-hint {
    color: rgba(255, 255, 255, 0.7);
    font-size: 0.9rem;
    display: flex;
    align-items: center;
    justify-content: center;
    gap: 10px;
  }

  .game-control-hint i {
    color: var(--primary);
  }

  @keyframes loading-dots {
    0% { content: '.'; }
    33% { content: '..'; }
    66% { content: '...'; }
  }
</style> 