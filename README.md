<!DOCTYPE html>
<html lang="fr">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>La Quête d'Athanor — Pour Sarah</title>
  <link rel="stylesheet" href="style.css">
  <!-- Google Fonts : Press Start 2P pour l'effet Pixel, Outfit pour l'élégance -->
  <link rel="preconnect" href="https://fonts.googleapis.com">
  <link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>
  <link href="https://fonts.googleapis.com/css2?family=Outfit:wght@300;400;600&family=Press+Start+2P&display=swap" rel="stylesheet">
</head>
<body>

  <!-- Canvas pour le fond de particules réactif -->
  <canvas id="particles-canvas"></canvas>

  <div class="app-container">
    
    <!-- Hero Section -->
    <header class="hero">
      <div class="badge-pixel">QUÊTE D'ATHANOR</div>
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
          <div class="item-title">Livre d'Athanor</div>
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
        Comme une carte infini qu'on explore sans fin,<br>
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
      <button class="btn-primary" onclick="triggerFireworks()">Lancer la célébration 🎆</button>
    </div>
  </div>

  <script src="script.js"></script>
</body>
</html>
