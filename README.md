<!DOCTYPE html>
<html lang="fr">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Quête d’amour — Pour Sarah</title>
  <!-- Google Fonts : Press Start 2P pour l'effet Pixel, Outfit pour l'élégance -->
  <link rel="preconnect" href="https://fonts.googleapis.com">
  <link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>
  <link href="https://fonts.googleapis.com/css2?family=Outfit:wght@300;400;600&family=Press+Start+2P&display=swap" rel="stylesheet">
  
  <style>
    /* RESET & BASE */
    * {
      margin: 0;
      padding: 0;
      box-sizing: border-box;
    }

    body {
      font-family: 'Outfit', sans-serif;
      background-color: #0b0914;
      color: #f3f0ff;
      min-height: 100vh;
      overflow-x: hidden;
      display: flex;
      justify-content: center;
      align-items: center;
    }

    /* CANVAS DE PARTICULES EN ARRIÈRE-PLAN */
    #particles-canvas {
      position: fixed;
      top: 0;
      left: 0;
      width: 100%;
      height: 100%;
      z-index: 0;
      pointer-events: none;
    }

    .app-container {
      position: relative;
      z-index: 1;
      width: 90%;
      max-width: 800px;
      text-align: center;
      padding: 2rem 0;
    }

    /* TYPOGRAPHIE & BADGES */
    .badge-pixel {
      font-family: 'Press Start 2P', cursive;
      font-size: 0.75rem;
      color: #a78bfa;
      background: rgba(167, 139, 250, 0.1);
      border: 1px solid rgba(167, 139, 250, 0.3);
      padding: 8px 16px;
      display: inline-block;
      border-radius: 4px;
      margin-bottom: 1.5rem;
      letter-spacing: 1px;
    }

    h1 {
      font-size: 3.5rem;
      font-weight: 600;
      background: linear-gradient(135deg, #ffffff 0%, #c4b5fd 100%);
      -webkit-background-clip: text;
      -webkit-text-fill-color: transparent;
      margin-bottom: 1rem;
    }

    .subtitle {
      font-size: 1.2rem;
      color: #a1a1aa;
      margin-bottom: 2rem;
    }

    h2 {
      font-size: 2rem;
      margin-bottom: 0.5rem;
    }

    .section-desc {
      color: #a1a1aa;
      margin-bottom: 2.5rem;
    }

    /* BOUTONS */
    .btn-primary {
      font-family: 'Outfit', sans-serif;
      font-size: 1.1rem;
      font-weight: 600;
      color: #0b0914;
      background: #a78bfa;
      border: none;
      padding: 14px 32px;
      border-radius: 12px;
      cursor: pointer;
      transition: all 0.3s ease;
      box-shadow: 0 0 20px rgba(167, 139, 250, 0.3);
    }

    .btn-primary:hover {
      background: #c4b5fd;
      transform: translateY(-2px);
      box-shadow: 0 0 30px rgba(167, 139, 250, 0.5);
    }

    /* GRILLE D'INVENTAIRE (STYLE SLOTS RETRO-CHIC) */
    .inventory-grid {
      display: grid;
      grid-template-columns: repeat(auto-fit, minmax(220px, 1fr));
      gap: 1.5rem;
      margin-top: 2rem;
    }

    .inventory-slot {
      background: rgba(23, 20, 38, 0.6);
      border: 1px solid rgba(167, 139, 250, 0.2);
      backdrop-filter: blur(12px);
      padding: 2rem 1.5rem;
      border-radius: 16px;
      cursor: pointer;
      transition: all 0.3s ease;
      display: flex;
      flex-direction: column;
      align-items: center;
    }

    .inventory-slot:hover {
      border-color: #a78bfa;
      transform: translateY(-5px);
      background: rgba(35, 30, 58, 0.8);
      box-shadow: 0 10px 25px rgba(0, 0, 0, 0.5);
    }

    .item-icon {
      font-size: 3rem;
      margin-bottom: 1rem;
    }

    .item-title {
      font-weight: 600;
      font-size: 1.1rem;
      margin-bottom: 0.3rem;
    }

    .item-status {
      font-size: 0.85rem;
      color: #a1a1aa;
    }

    /* MODALS (GLASSMORPHISM) */
    .modal-overlay {
      position: fixed;
      top: 0;
      left: 0;
      width: 100%;
      height: 100%;
      background: rgba(5, 4, 10, 0.75);
      backdrop-filter: blur(8px);
      z-index: 10;
      display: flex;
      justify-content: center;
      align-items: center;
      opacity: 1;
      transition: opacity 0.3s ease;
    }

    .modal-content {
      background: rgba(20, 16, 35, 0.85);
      border: 1px solid rgba(167, 139, 250, 0.3);
      padding: 2.5rem;
      border-radius: 20px;
      max-width: 500px;
      width: 90%;
      position: relative;
      text-align: center;
      box-shadow: 0 20px 50px rgba(0,0,0,0.6);
      transform: scale(1);
      transition: transform 0.3s ease;
    }

    .close-btn {
      position: absolute;
      top: 15px;
      right: 20px;
      background: none;
      border: none;
      color: #a1a1aa;
      font-size: 1.8rem;
      cursor: pointer;
    }

    .close-btn:hover {
      color: #ffffff;
    }

    .pixel-tag {
      font-family: 'Press Start 2P', cursive;
      font-size: 0.6rem;
      color: #34d399;
      margin-bottom: 1rem;
    }

    .poem-text {
      font-style: italic;
      line-height: 1.8;
      color: #e4e4e7;
      margin-top: 1rem;
    }

    /* QUIZ INTERACTIF KABYLE */
    .quiz-container {
      margin-top: 1.5rem;
      display: flex;
      flex-direction: column;
      gap: 0.75rem;
    }

    .highlight {
      color: #a78bfa;
    }

    .btn-option {
      background: rgba(255, 255, 255, 0.05);
      border: 1px solid rgba(255, 255, 255, 0.1);
      color: #ffffff;
      padding: 10px 16px;
      border-radius: 8px;
      cursor: pointer;
      transition: all 0.2s ease;
      font-family: 'Outfit', sans-serif;
    }

    .btn-option:hover {
      background: rgba(167, 139, 250, 0.2);
      border-color: #a78bfa;
    }

    .quiz-result {
      margin-top: 1.5rem;
      color: #34d399;
      font-weight: 600;
      animation: fadeIn 0.5s ease;
    }

    /* UTILITAIRES ANIMATION & MASQUAGE */
    .hidden {
      display: none !important;
      opacity: 0;
      pointer-events: none;
    }

    @keyframes fadeIn {
      from { opacity: 0; transform: translateY(10px); }
      to { opacity: 1; transform: translateY(0); }
    }
  </style>
</head>
<body>

  <!-- Canvas pour le fond de particules réactif -->
  <canvas id="particles-canvas"></canvas>

  <div class="app-container">
    
    <!-- Hero Section -->
    <header class="hero">
      <div class="badge-pixel">QUÊTE D’AMOUR</div>
      <h1>Pour Sarah</h1>
      <p class="subtitle">Une aventure pensée pour toi, morceau par morceau.</p>
      <button id="btn-start" class="btn-primary">Commencer l'aventure</button>
    </header>

    <!-- Zone principale : Inventaire des Souvenirs (cachée au départ) -->
    <main id="quest-section" class="hidden">
      
      <h2>L'Inventaire Enchanté</h2>
      <p class="section-desc">Clique sur un objet pour débloquer un souvenir ou un mystère.</p>

      <div class="inventory-grid">
        
        <!-- Slot 1 : Le Livre Enchanté -->
        <div class="inventory-slot" onclick="openModal('modal-book')">
          <div class="item-icon">📖</div>
          <div class="item-title">Livre Souvenir</div>
          <div class="item-status">Débloqué</div>
        </div>

        <!-- Slot 2 : Le Décodeur Kabyle -->
        <div class="inventory-slot" onclick="openModal('modal-kabyle')">
          <div class="item-icon">🗝️</div>
          <div class="item-title">Mots Doux</div>
          <div class="item-status">À décoder</div>
        </div>

        <!-- Slot 3 : Le Coffre Final -->
        <div class="inventory-slot" onclick="openModal('modal-declaration')">
          <div class="item-icon">💎</div>
          <div class="item-title">Message Ultime</div>
          <div class="item-status">Spécial</div>
        </div>

      </div>

    </main>

  </div>

  <!-- MODALS -->

  <!-- Modal 1 : Le Livre -->
  <div id="modal-book" class="modal-overlay hidden">
    <div class="modal-content glass">
      <button class="close-btn" onclick="closeModal('modal-book')">&times;</button>
      <div class="pixel-tag">POÉSIE</div>
      <h3>Récit d'un monde à deux</h3>
      <p class="poem-text">
        Comme une carte infinie qu'on explore sans fin,<br>
        Chaque moment passé avec toi a le goût d'une aventure.<br>
        Des blocs posés sous les étoiles jusqu'aux rires du quotidien,<br>
        Tu es mon point de repère absolu.
      </p>
    </div>
  </div>

  <!-- Modal 2 : Décodeur Kabyle -->
  <div id="modal-kabyle" class="modal-overlay hidden">
    <div class="modal-content glass">
      <button class="close-btn" onclick="closeModal('modal-kabyle')">&times;</button>
      <div class="pixel-tag">DÉCODEUR</div>
      <h3>Langage du Cœur</h3>
      <p>Trouve la bonne traduction pour débloquer le message secret :</p>

      <div class="quiz-container">
        <p class="quiz-question">Que veut dire <strong class="highlight">« Hemleghkem »</strong> ?</p>
        <button class="btn-option" onclick="checkAnswer(false, this)">Un sort de protection</button>
        <button class="btn-option" onclick="checkAnswer(true, this)">Je t'aime</button>
        <button class="btn-option" onclick="checkAnswer(false, this)">Une pomme dorée</button>
      </div>

      <div id="quiz-result" class="quiz-result hidden">
        ✨ <em>Ken hobbek atas atas...</em> Plus que les mots ne peuvent le dire !
      </div>
    </div>
  </div>

  <!-- Modal 3 : Déclaration -->
  <div id="modal-declaration" class="modal-overlay hidden">
    <div class="modal-content glass declaration-modal">
      <button class="close-btn" onclick="closeModal('modal-declaration')">&times;</button>
      <div class="pixel-tag">QUÊTE ACCOMPLIE</div>
      <h3>Ma Sarah ❤️</h3>
      <p>
        Merci d'être qui tu es, d'illuminer chaque journée et d'être ma partenaire préférée, sur Minecraft comme dans la vraie vie.
      </p>
      <button class="btn-primary" style="margin-top: 15px;" onclick="triggerFireworks()">Lancer la célébration 🎆</button>
    </div>
  </div>

  <script>
    // 1. ANIMATION DES PARTICULES (CANVAS JS)
    const canvas = document.getElementById('particles-canvas');
    const ctx = canvas.getContext('2d');

    let particlesArray = [];
    const numberOfParticles = 60;

    function resizeCanvas() {
      canvas.width = window.innerWidth;
      canvas.height = window.innerHeight;
    }
    resizeCanvas();
    window.addEventListener('resize', resizeCanvas);

    class Particle {
      constructor() {
        this.x = Math.random() * canvas.width;
        this.y = Math.random() * canvas.height;
        this.size = Math.random() * 3 + 1;
        this.speedX = (Math.random() - 0.5) * 0.5;
        this.speedY = (Math.random() - 0.5) * 0.5;
        this.color = `rgba(${167 + Math.random() * 50}, 139, 250, ${Math.random() * 0.5 + 0.2})`;
      }

      update() {
        this.x += this.speedX;
        this.y += this.speedY;

        if (this.x < 0 || this.x > canvas.width) this.speedX *= -1;
        if (this.y < 0 || this.y > canvas.height) this.speedY *= -1;
      }

      draw() {
        ctx.fillStyle = this.color;
        ctx.beginPath();
        ctx.arc(this.x, this.y, this.size, 0, Math.PI * 2);
        ctx.fill();
      }
    }

    function initParticles() {
      particlesArray = [];
      for (let i = 0; i < numberOfParticles; i++) {
        particlesArray.push(new Particle());
      }
    }

    function animateParticles() {
      ctx.clearRect(0, 0, canvas.width, canvas.height);
      particlesArray.forEach(p => {
        p.update();
        p.draw();
      });
      requestAnimationFrame(animateParticles);
    }

    initParticles();
    animateParticles();

    // 2. GESTION DE LA NAVIGATION ET DE LA TRANSITION
    document.getElementById('btn-start').addEventListener('click', () => {
      document.querySelector('.hero').classList.add('hidden');
      const questSection = document.getElementById('quest-section');
      questSection.classList.remove('hidden');
      questSection.style.animation = 'fadeIn 0.8s ease forwards';
    });

    // 3. GESTION DES MODALS
    function openModal(modalId) {
      const modal = document.getElementById(modalId);
      modal.classList.remove('hidden');
    }

    function closeModal(modalId) {
      const modal = document.getElementById(modalId);
      modal.classList.add('hidden');
    }

    // Fermer le modal si clic à l'extérieur
    window.addEventListener('click', (e) => {
      if (e.target.classList.contains('modal-overlay')) {
        e.target.classList.add('hidden');
      }
    });

    // 4. LOGIQUE DU DÉCODEUR KABYLE
    function checkAnswer(isCorrect, btn) {
      const resultDiv = document.getElementById('quiz-result');
      if (isCorrect) {
        btn.style.background = '#34d399';
        btn.style.borderColor = '#34d399';
        btn.style.color = '#0b0914';
        resultDiv.classList.remove('hidden');
      } else {
        btn.style.background = '#ef4444';
        btn.style.borderColor = '#ef4444';
        setTimeout(() => {
          btn.style.background = 'rgba(255, 255, 255, 0.05)';
          btn.style.borderColor = 'rgba(255, 255, 255, 0.1)';
        }, 1000);
      }
    }

    // 5. CÉLÉBRATION FINALE
    function triggerFireworks() {
      for (let i = 0; i < 40; i++) {
        particlesArray.push(new FastParticle());
      }
      alert("✨ Ken hobbek atas atas Sarah ! ✨");
    }

    class FastParticle extends Particle {
      constructor() {
        super();
        this.x = canvas.width / 2;
        this.y = canvas.height / 2;
        this.speedX = (Math.random() - 0.5) * 8;
        this.speedY = (Math.random() - 0.5) * 8;
        this.size = Math.random() * 5 + 2;
        this.color = '#34d399';
      }
    }
  </script>
</body>
</html>
