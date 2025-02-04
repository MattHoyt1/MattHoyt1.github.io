<html lang="en">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0"/>
  <title>Matthew Hoyt App Support</title>
  
  <!-- Tailwind CSS -->
  <script src="https://cdn.tailwindcss.com"></script>
  <!-- Google Fonts (Inter) -->
  <link rel="preconnect" href="https://fonts.googleapis.com">
  <link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>
  <link
    href="https://fonts.googleapis.com/css2?family=Inter:wght@400;600;700&display=swap"
    rel="stylesheet"
  />

  <style>
    /* ========= CUSTOM BASE STYLES ========= */
    html, body {
      margin: 0;
      padding: 0;
      font-family: 'Inter', sans-serif;
    }
    /* ===== BACKGROUND GRADIENT & CANVAS ===== */
    body {
      /* Subtle gradient background */
      background: linear-gradient(135deg, #f8e9dc 0%, #e4d6c6 100%);
      overflow-x: hidden;
      position: relative;
    }
    canvas {
      position: fixed;
      top: 0;
      left: 0;
      pointer-events: none;
      z-index: 0;
    }
    /* ===== MODAL STYLES ===== */
    .modal {
      display: none;
      position: fixed;
      inset: 0;
      background-color: rgba(0, 0, 0, 0.5);
      z-index: 50;
      align-items: center;
      justify-content: center;
    }
    .modal.active {
      display: flex;
    }
    .modal-content {
      background: #fff;
      width: 90%;
      max-width: 800px;
      max-height: 90vh;
      overflow-y: auto;
      border-radius: 0.75rem;
      padding: 2rem;
      position: relative;
      animation: fadeIn 0.3s ease-out;
    }
    .close-button {
      position: absolute;
      top: 1rem;
      right: 1rem;
      font-size: 1.5rem;
      cursor: pointer;
      color: gray;
    }
    .close-button:hover {
      color: black;
    }
    @keyframes fadeIn {
      from {
        opacity: 0;
        transform: translateY(-10px);
      }
      to {
        opacity: 1;
        transform: translateY(0);
      }
    }
  </style>
</head>
<body class="text-gray-700">

  <!-- Canvas for subtle floating specks -->
  <canvas id="specks"></canvas>

  <!-- NAVIGATION -->
  <nav class="sticky top-0 z-40 bg-white bg-opacity-90 backdrop-blur-sm shadow-sm">
    <div class="max-w-6xl mx-auto px-4 flex items-center justify-between py-4">
      <div class="text-xl font-bold">
        Matthew Hoyt
      </div>
      <div class="hidden md:flex space-x-6 font-medium">
        <a href="#home" class="hover:text-gray-900 transition">Home</a>
        <a href="#apps" class="hover:text-gray-900 transition">Apps</a>
        <a href="#faq" class="hover:text-gray-900 transition">FAQ</a>
        <a href="#contact" class="hover:text-gray-900 transition">Contact</a>
        <button onclick="showModal('privacy-modal')" class="hover:text-gray-900 transition">
          Privacy
        </button>
        <button onclick="showModal('terms-modal')" class="hover:text-gray-900 transition">
          Terms
        </button>
      </div>
      <!-- Mobile Menu Button -->
      <button id="menu-btn" class="md:hidden text-gray-700">
        <svg xmlns="http://www.w3.org/2000/svg" class="h-7 w-7" fill="none" 
             viewBox="0 0 24 24" stroke="currentColor">
          <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" 
                d="M4 6h16M4 12h16m-7 6h7" />
        </svg>
      </button>
    </div>
    <!-- Mobile Menu -->
    <div id="mobile-menu" class="hidden md:hidden bg-white bg-opacity-90 px-4">
      <a href="#home" class="block py-2 border-t border-gray-200 hover:bg-gray-100">Home</a>
      <a href="#apps" class="block py-2 border-t border-gray-200 hover:bg-gray-100">Apps</a>
      <a href="#faq" class="block py-2 border-t border-gray-200 hover:bg-gray-100">FAQ</a>
      <a href="#contact" class="block py-2 border-t border-gray-200 hover:bg-gray-100">Contact</a>
      <button onclick="showModal('privacy-modal')" 
              class="block w-full text-left py-2 border-t border-gray-200 hover:bg-gray-100">
        Privacy
      </button>
      <button onclick="showModal('terms-modal')" 
              class="block w-full text-left py-2 border-t border-gray-200 hover:bg-gray-100">
        Terms
      </button>
    </div>
  </nav>

  <!-- HERO -->
  <section id="home" class="relative z-10 pt-20 pb-16 text-center">
    <div class="max-w-3xl mx-auto px-4">
      <h1 class="text-4xl md:text-5xl font-bold text-gray-800 mb-4">
        App Support Center
      </h1>
      <p class="text-lg md:text-xl text-gray-600 mb-8">
        Find help and information for all Matthew Hoyt apps
      </p>
      <!-- Optional CTA Button -->
      <a href="#apps"
         class="inline-block bg-indigo-600 text-white font-medium rounded-lg px-6 py-3 
                hover:bg-indigo-700 transition">
        View Apps
      </a>
    </div>
  </section>

  <!-- APPS SECTION -->
  <section id="apps" class="relative z-10 py-16 bg-white bg-opacity-90">
    <div class="max-w-5xl mx-auto px-4">
      <h2 class="text-3xl font-bold text-center text-gray-800 mb-10">Our Apps</h2>
      <div class="grid grid-cols-1 md:grid-cols-2 gap-6">
        <!-- App Card -->
        <div class="bg-white rounded-lg shadow hover:shadow-md transition p-6 relative z-10">
          <h3 class="text-xl font-semibold text-gray-800 mb-2">Hygge Analysis</h3>
          <p class="text-gray-600 mb-4">
            Discover the coziness in your space with AI-powered analysis.
          </p>
          <button onclick="showModal('learn-more-modal')" class="text-indigo-600 hover:underline">
            Learn More
          </button>
        </div>
        <!-- Add more App Cards here if needed -->
      </div>
    </div>
  </section>

  <!-- LEARN MORE MODAL -->
  <div id="learn-more-modal" class="modal">
    <div class="modal-content">
      <span class="close-button" onclick="hideModal('learn-more-modal')">&times;</span>
      <h2 class="text-3xl font-bold text-gray-800 mb-4">What is Hygge?</h2>
      <p class="text-gray-600 leading-relaxed">
        [Your detailed content about Hygge goes here...]
      </p>
    </div>
  </div>

  <!-- FAQ SECTION -->
  <section id="faq" class="relative z-10 py-16">
    <div class="max-w-4xl mx-auto px-4">
      <h2 class="text-3xl font-bold text-center text-gray-800 mb-8">Frequently Asked Questions</h2>
      <div class="space-y-6">
        <!-- FAQ Item -->
        <div class="bg-white rounded-lg shadow p-6">
          <h3 class="text-xl font-semibold text-gray-800 mb-2">How do I get support for an app?</h3>
          <p class="text-gray-600">
            Each app has its own dedicated support section. Select your app above to find specific help and guidance.
          </p>
        </div>
        <!-- FAQ Item -->
        <div class="bg-white rounded-lg shadow p-6">
          <h3 class="text-xl font-semibold text-gray-800 mb-2">How do I report an issue?</h3>
          <p class="text-gray-600">
            You can report issues through the contact section or by emailing our support team directly.
          </p>
        </div>
        <!-- FAQ Item -->
        <div class="bg-white rounded-lg shadow p-6">
          <h3 class="text-xl font-semibold text-gray-800 mb-2">Are my data and privacy protected?</h3>
          <p class="text-gray-600">
            Yes, we take data protection seriously. See our 
            <button onclick="showModal('privacy-modal')" class="text-indigo-600 hover:underline">privacy policy</button>
            for details.
          </p>
        </div>
      </div>
    </div>
  </section>

  <!-- CONTACT SECTION -->
  <section id="contact" class="relative z-10 py-16 bg-white bg-opacity-90">
    <div class="max-w-4xl mx-auto px-4 text-center">
      <h2 class="text-3xl font-bold text-gray-800 mb-6">Contact Support</h2>
      <div class="bg-white rounded-lg shadow p-8">
        <p class="text-gray-600 mb-4">
          Need help with one of our apps? We're here to assist you!
        </p>
        <a href="mailto:Matthewhoytapps@gmail.com"
           class="inline-block bg-gray-800 text-white px-6 py-3 rounded-lg hover:bg-gray-700 transition">
          Email Support
        </a>
      </div>
    </div>
  </section>

  <!-- PRIVACY MODAL -->
  <div id="privacy-modal" class="modal">
    <div class="modal-content">
      <span class="close-button" onclick="hideModal('privacy-modal')">&times;</span>
      <h2 class="text-3xl font-bold text-gray-800 mb-6">Privacy Policy</h2>
      <div class="space-y-6 text-gray-600">
        <!-- Your detailed privacy policy content here -->
      </div>
    </div>
  </div>

  <!-- TERMS MODAL -->
  <div id="terms-modal" class="modal">
    <div class="modal-content">
      <span class="close-button" onclick="hideModal('terms-modal')">&times;</span>
      <h2 class="text-3xl font-bold text-gray-800 mb-6">Terms of Service</h2>
      <div class="space-y-6 text-gray-600">
        <!-- Your detailed terms content here -->
      </div>
    </div>
  </div>

  <!-- FOOTER -->
  <footer class="bg-gray-800 text-white py-8 text-center">
    <div class="max-w-5xl mx-auto px-4">
      <p>&copy; 2025 Matthew Hoyt. All rights reserved.</p>
    </div>
  </footer>

  <!-- JAVASCRIPT -->
  <script>
    /* ===== FLOATING SPECKS ===== */
    const canvas = document.getElementById('specks');
    const ctx = canvas.getContext('2d');

    function resizeCanvas() {
      canvas.width = window.innerWidth;
      canvas.height = window.innerHeight;
    }
    resizeCanvas();

    const specks = [];
    const numSpecks = 40; // Adjust for more/fewer specks

    for (let i = 0; i < numSpecks; i++) {
      specks.push({
        x: Math.random() * canvas.width,
        y: Math.random() * canvas.height,
        r: Math.random() * 1.3 + 0.3,
        sx: (Math.random() - 0.5) * 0.2,
        sy: (Math.random() - 0.5) * 0.2
      });
    }

    function animate() {
      ctx.clearRect(0, 0, canvas.width, canvas.height);
      ctx.fillStyle = 'rgba(255, 255, 255, 0.6)'; // Soft white
      specks.forEach(s => {
        ctx.beginPath();
        ctx.arc(s.x, s.y, s.r, 0, Math.PI * 2);
        ctx.fill();
        
        // Move
        s.x += s.sx;
        s.y += s.sy;

        // Wrap around screen edges
        if (s.x < 0) s.x = canvas.width;
        if (s.x > canvas.width) s.x = 0;
        if (s.y < 0) s.y = canvas.height;
        if (s.y > canvas.height) s.y = 0;
      });
      requestAnimationFrame(animate);
    }
    animate();

    window.addEventListener('resize', () => {
      resizeCanvas();
    });

    /* ===== MOBILE MENU TOGGLE ===== */
    const menuBtn = document.getElementById('menu-btn');
    const mobileMenu = document.getElementById('mobile-menu');
    menuBtn.addEventListener('click', () => {
      mobileMenu.classList.toggle('hidden');
    });

    /* ===== MODAL HANDLERS ===== */
    function showModal(id) {
      document.getElementById(id).classList.add('active');
      document.body.style.overflow = 'hidden'; 
    }
    function hideModal(id) {
      document.getElementById(id).classList.remove('active');
      document.body.style.overflow = 'auto'; 
    }

    // Close modal if user clicks outside content
    window.addEventListener('click', (e) => {
      if (e.target.classList.contains('modal')) {
        e.target.classList.remove('active');
        document.body.style.overflow = 'auto';
      }
    });

    // Close on Escape key
    document.addEventListener('keydown', (e) => {
      if (e.key === 'Escape') {
        document.querySelectorAll('.modal').forEach(modal => {
          modal.classList.remove('active');
        });
        document.body.style.overflow = 'auto';
      }
    });
  </script>
</body>
</html>
