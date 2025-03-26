<script lang="ts">
  const software = [
    { name: 'Visual Studio Code', logo: 'https://cdn.jsdelivr.net/gh/devicons/devicon/icons/vscode/vscode-original.svg' },
    { name: 'Visual Studio', logo: 'https://cdn.jsdelivr.net/gh/devicons/devicon/icons/visualstudio/visualstudio-plain.svg' },
    { name: 'GitHub', logo: 'https://cdn.jsdelivr.net/gh/devicons/devicon/icons/github/github-original.svg' },
    { name: 'Blender', logo: 'https://cdn.jsdelivr.net/gh/devicons/devicon/icons/blender/blender-original.svg' },
    { name: 'Unity', logo: 'https://cdn.jsdelivr.net/gh/devicons/devicon/icons/unity/unity-original.svg' }
  ];

  const technicalSkills = {
    frontend: [
      { name: 'JavaScript', logo: 'https://cdn.jsdelivr.net/gh/devicons/devicon/icons/javascript/javascript-original.svg' },
      { name: 'React', logo: 'https://cdn.jsdelivr.net/gh/devicons/devicon/icons/react/react-original.svg' },
      { name: 'Svelte', logo: 'https://cdn.jsdelivr.net/gh/devicons/devicon/icons/svelte/svelte-original.svg' },
      { name: 'Flutter', logo: 'https://cdn.jsdelivr.net/gh/devicons/devicon/icons/flutter/flutter-original.svg' }
    ],
    backend: [
      { name: 'COBOL', logo: '/icons/cobol.svg' },
      { name: '.NET', logo: 'https://cdn.jsdelivr.net/gh/devicons/devicon/icons/dot-net/dot-net-original.svg' },
      { name: 'Python', logo: 'https://cdn.jsdelivr.net/gh/devicons/devicon/icons/python/python-original.svg' },
      { name: 'Node.js', logo: 'https://cdn.jsdelivr.net/gh/devicons/devicon/icons/nodejs/nodejs-original.svg' },
      { name: 'NestJS', logo: 'https://nestjs.com/img/logo-small.svg' }
    ]
  };

  const softSkills = [
    { name: 'Adaptabilité', icon: 'fa-sync-alt' },
    { name: 'Organisation', icon: 'fa-tasks' },
    { name: 'Esprit d\'équipe', icon: 'fa-users' },
    { name: 'Communication', icon: 'fa-comments' }
  ];
</script>

<section class="skills-section py-5">
  <div class="container">
    <h2 class="text-center mb-5">Compétences</h2>

    <!-- Logiciels -->
    <div class="section-container">
      <h3 class="section-title">TOOLS</h3>
      <div class="software-grid">
        {#each software as tool}
          <div class="software-card">
            <div class="software-card-inner">
              <img src={tool.logo} alt={tool.name} class="software-logo" />
              <h4>{tool.name}</h4>
            </div>
          </div>
        {/each}
      </div>
    </div>

    <!-- Compétences Techniques -->
    <div class="section-container">
      <h3 class="section-title">TECHNICAL SKILLS</h3>
      
      <h4 class="subsection-title">FRONT-END</h4>
      <div class="technical-grid">
        {#each technicalSkills.frontend as skill}
          <div class="skill-card">
            <div class="skill-card-inner">
              <img src={skill.logo} alt={skill.name} class="skill-logo" />
              <h4>{skill.name}</h4>
            </div>
          </div>
        {/each}
      </div>

      <h4 class="subsection-title">BACK-END</h4>
      <div class="technical-grid">
        {#each technicalSkills.backend as skill}
          <div class="skill-card">
            <div class="skill-card-inner">
              <img src={skill.logo} alt={skill.name} class="skill-logo" />
              <h4>{skill.name}</h4>
            </div>
          </div>
        {/each}
      </div>
    </div>

    <!-- Soft Skills -->
    <div class="section-container">
      <h3 class="section-title">SOFT SKILLS</h3>
      <div class="soft-skills-grid">
        {#each softSkills as skill}
          <div class="soft-skill-card">
            <i class="fas {skill.icon}"></i>
            <h4>{skill.name}</h4>
          </div>
        {/each}
      </div>
    </div>
  </div>
</section>

<style lang="postcss">
  .skills-section {
    background: var(--darker);
    color: white;
  }

  .section-container {
    margin-bottom: 4rem;
  }

  .section-title {
    text-align: center;
    margin-bottom: 2rem;
    font-size: 1.8rem;
    background: linear-gradient(135deg, var(--primary), var(--secondary));
    -webkit-background-clip: text;
    -webkit-text-fill-color: transparent;
  }

  .subsection-title {
    text-align: left;
    margin: 2rem 0 1rem;
    font-size: 1.3rem;
    color: var(--primary);
    padding-left: 1rem;
    border-left: 4px solid var(--primary);
  }

  /* Grilles */
  .software-grid,
  .technical-grid,
  .soft-skills-grid {
    display: grid;
    gap: 2rem;
    padding: 1rem;
  }

  .software-grid,
  .technical-grid {
    grid-template-columns: repeat(auto-fit, minmax(150px, 1fr));
  }

  .soft-skills-grid {
    grid-template-columns: repeat(auto-fit, minmax(180px, 1fr));
  }

  /* Cartes Logiciels et Techniques */
  .software-card,
  .skill-card {
    background: rgba(255, 255, 255, 0.05);
    border-radius: 15px;
    padding: 2rem;
    transition: all 0.3s ease;
    cursor: pointer;
  }

  .software-card:hover,
  .skill-card:hover {
    transform: translateY(-5px) scale(1.02);
    box-shadow: 0 5px 15px rgba(0, 0, 0, 0.3);
    background: rgba(255, 255, 255, 0.1);
  }

  .software-card-inner,
  .skill-card-inner {
    text-align: center;
  }

  .software-logo,
  .skill-logo {
    width: 60px;
    height: 60px;
    margin-bottom: 1rem;
    transition: transform 0.3s ease;
    filter: brightness(0.9);
  }

  .software-card:hover .software-logo,
  .skill-card:hover .skill-logo {
    transform: scale(1.1);
    filter: brightness(1);
  }

  h4 {
    font-size: 1rem;
    margin: 0;
    opacity: 0.9;
  }

  /* Cartes Soft Skills */
  .soft-skill-card {
    background: rgba(255, 255, 255, 0.05);
    border-radius: 15px;
    padding: 2rem;
    text-align: center;
    transition: all 0.3s ease;
  }

  .soft-skill-card:hover {
    transform: translateY(-5px) rotateY(10deg);
    box-shadow: 0 5px 15px rgba(0, 0, 0, 0.3);
    background: rgba(255, 255, 255, 0.1);
  }

  .soft-skill-card i {
    font-size: 2rem;
    margin-bottom: 1rem;
    background: linear-gradient(135deg, var(--primary), var(--secondary));
    -webkit-background-clip: text;
    -webkit-text-fill-color: transparent;
  }

  @media (max-width: 768px) {
    .software-grid,
    .technical-grid,
    .soft-skills-grid {
      grid-template-columns: repeat(2, 1fr);
    }
  }

  @media (max-width: 480px) {
    .software-grid,
    .technical-grid,
    .soft-skills-grid {
      grid-template-columns: 1fr;
    }
  }
</style> 