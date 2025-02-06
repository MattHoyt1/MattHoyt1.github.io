<html lang="en">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0"/>
  <title>Matthew Hoyt App Support</title>
  
  <!-- Tailwind CSS -->
  <script src="https://cdn.tailwindcss.com"></script>

  <style>
    /* ========= BACKGROUND & GENERAL LAYOUT ========= */
body {
  margin: 0;
  min-height: 100vh;
  /* Reversed gradient with purple at bottom, adjusted color stops for smoother transition */
  background: linear-gradient(
    to bottom,
   #fdf6e3 0%,    /* Light cream at top for brightness */
    #fbe9d7 40%,   /* Warm peachy-brown for smooth transition */
    #d4b59c 100%   /* Deeper, richer brown at bottom */
  );
  font-family: 'Helvetica Neue', 'Arial', sans-serif;
  position: relative;
  overflow-x: hidden;
}

    /* ========= FLOATING SPECKS CANVAS ========= */
  canvas {
    position: fixed;
    top: 0;
    left: 0;
    width: 100%;
    height: 100%;
    pointer-events: none;
    z-index: 0;
    opacity: 1;
    mix-blend-mode: screen;
  }
    
    /* ========= WARM SHADOW UTILITY ========= */
.warm-shadow {
  /* Multiple shadow layers for depth */
  box-shadow: 
    0 16px 24px -8px rgba(120, 100, 80, 0.2),
    0 8px 16px -6px rgba(120, 100, 80, 0.15),
    0 4px 8px -4px rgba(120, 100, 80, 0.1),
    0 0 0 1px rgba(120, 100, 80, 0.05);
  transition: all 0.4s cubic-bezier(0.175, 0.885, 0.32, 1.275);
  transform: translateY(0);
  /* Ensure proper stacking context without breaking clicks */
  position: relative;
  z-index: 1;
}

.warm-shadow:hover {
  transform: translateY(-8px);
  box-shadow: 
    0 24px 32px -12px rgba(120, 100, 80, 0.25),
    0 16px 24px -8px rgba(120, 100, 80, 0.15),
    0 8px 16px -6px rgba(120, 100, 80, 0.1),
    0 0 0 1px rgba(120, 100, 80, 0.05);
}

    /* Ensure email button is always visible */
section#contact a[href^="mailto"] {
  opacity: 1 !important;
  visibility: visible !important;
  display: inline-block !important;
  color: white !important;
}

/* Ensure the button's container is visible */
section#contact .text-center {
  opacity: 1;
  visibility: visible;
}

/* ========= CARD ENHANCEMENTS ========= */
.modal-content, 
.rounded-lg {
  background: rgba(255, 255, 255, 0.9);
  backdrop-filter: blur(16px);
  -webkit-backdrop-filter: blur(16px);
  border: 1px solid rgba(255, 255, 255, 0.5);
  position: relative;
  z-index: 1;
}

     /* ========= NAVIGATION ENHANCEMENT ========= */
  nav {
    background: rgba(255, 255, 255, 0.95);
    backdrop-filter: blur(12px);
    -webkit-backdrop-filter: blur(12px);
    box-shadow: 
      0 8px 16px -4px rgba(120, 100, 80, 0.1),
      0 4px 8px -4px rgba(120, 100, 80, 0.06);
    position: relative;
    z-index: 10;
  }
    
    /* ========= CARD HOVER EFFECTS ========= */
.rounded-lg::before {
  content: '';
  position: absolute;
  top: 0;
  left: 0;
  right: 0;
  height: 100%;
  background: linear-gradient(
    to bottom,
    rgba(255, 255, 255, 0.1) 0%,
    rgba(255, 255, 255, 0.2) 100%
  );
  opacity: 0;
  transition: opacity 0.3s ease;
  pointer-events: none;
  /* Change z-index to be behind the content */
  z-index: 0;
}

.rounded-lg:hover::before {
  opacity: 1;
}

/* Add new style to ensure content stays above the hover effect */
.rounded-lg > * {
  position: relative;
  z-index: 2;
}
    
    /* ========= MODAL STYLES ========= */
    .modal {
      z-index: 50;
      display: none;
      position: fixed;
      inset: 0; /* top:0, left:0, right:0, bottom:0 */
      background-color: rgba(0, 0, 0, 0.5);
      z-index: 50; /* Above normal content, below canvas is z-index:0 */
      align-items: center;
      justify-content: center;
    }
    .modal.active {
      display: flex; /* Show the modal */
    }
    .modal-content {
      z-index: 51;
      background: white;
      padding: 2rem;
      width: 90%;
      max-width: 800px;
      max-height: 90vh;
      overflow-y: auto;
      border-radius: 0.5rem;
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
<body>
  <!-- ============ FLOATING SPECKS BACKGROUND ============ -->
  <canvas id="specks"></canvas>

  <!-- ============ NAVIGATION ============ -->
  <nav class="bg-white bg-opacity-90 shadow-md sticky top-0 z-50">
    <div class="max-w-6xl mx-auto px-4 flex justify-between items-center py-4">
      <!-- Logo / Title -->
      <div class="text-2xl font-bold text-gray-700">
        Matthew Hoyt
      </div>
      <!-- Desktop Menu -->
      <div class="hidden md:flex space-x-6">
        <a href="#home" class="hover:text-gray-900 transition">Home</a>
        <a href="#apps" class="hover:text-gray-900 transition">Apps</a>
        <a href="#faq" class="hover:text-gray-900 transition">FAQ</a>
        <a href="#contact" class="hover:text-gray-900 transition">Contact</a>
        <button onclick="showModal('privacy-modal')" class="hover:text-gray-900 hover:underline transition">Privacy</button>
        <button onclick="showModal('terms-modal')" class="hover:text-gray-900 hover:underline transition">Terms</button>
      </div>
      <!-- Mobile Menu Button -->
      <button id="menu-btn" class="md:hidden text-gray-700 focus:outline-none">
        <svg xmlns="http://www.w3.org/2000/svg" class="h-7 w-7" fill="none" 
             viewBox="0 0 24 24" stroke="currentColor">
          <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" 
                d="M4 6h16M4 12h16m-7 6h7" />
        </svg>
      </button>
    </div>
    <!-- Mobile Menu (hidden by default) -->
    <div id="mobile-menu" class="hidden md:hidden bg-white bg-opacity-90">
      <a href="#home" class="block py-2 px-4 text-sm text-gray-700 hover:bg-gray-100">Home</a>
      <a href="#apps" class="block py-2 px-4 text-sm text-gray-700 hover:bg-gray-100">Apps</a>
      <a href="#faq" class="block py-2 px-4 text-sm text-gray-700 hover:bg-gray-100">FAQ</a>
      <a href="#contact" class="block py-2 px-4 text-sm text-gray-700 hover:bg-gray-100">Contact</a>
      <button onclick="showModal('privacy-modal')" 
              class="block w-full text-left py-2 px-4 text-sm text-gray-700 hover:bg-gray-100 hover:underline">
        Privacy
      </button>
      <button onclick="showModal('terms-modal')" 
              class="block w-full text-left py-2 px-4 text-sm text-gray-700 hover:bg-gray-100 hover:underline">
        Terms
      </button>
    </div>
  </nav>

  <!-- ============ HERO SECTION ============ -->
  <section id="home" class="py-20 text-center relative z-10">
    <div class="max-w-6xl mx-auto px-4">
      <h1 class="text-4xl font-bold text-gray-800 drop-shadow-sm mb-4">
        App Support Center
      </h1>
      <p class="text-xl text-gray-600">
        Find help and information for all Matthew Hoyt apps
      </p>
    </div>
  </section>

  <!-- ============ APPS SECTION ============ -->
  <section id="apps" class="py-20 bg-white bg-opacity-90 relative z-10">
    <div class="max-w-4xl mx-auto px-4">
      <h2 class="text-3xl font-bold text-gray-800 mb-8 text-center">Our Apps</h2>
      <div class="grid grid-cols-1 md:grid-cols-2 gap-8">
        <!-- Example App Card -->
        <div class="warm-shadow rounded-lg p-6 bg-white transition hover:shadow-xl">
          <h3 class="text-xl font-semibold text-gray-800 mb-2">Hygge Detector</h3>
          <p class="text-gray-600 mb-4">
            Discover the coziness in your space with AI-powered analysis.
          </p>
          <button onclick="showModal('learn-more-modal')" class="text-blue-600 hover:underline">
            Learn More
          </button>
        </div>
      </div>
    </div>
  </section>

  <!-- ============ LEARN MORE MODAL ============ -->
  <div id="learn-more-modal" class="modal">
    <div class="modal-content warm-shadow">
      <span class="close-button" onclick="hideModal('learn-more-modal')">&times;</span>
      <h2 class="text-3xl font-bold text-gray-800 mb-4">What is hygge?</h2>
      <p class="text-gray-600 leading-relaxed">
        Now, you might be wondering, "What is hygge?" Hygge is the Danish art of creating a space that feels 
        warm, inviting, and, yes, perfectly cozy. And until today, understanding hygge was subjective, elusive—a 
        feeling. But not anymore.
      </p>
      <p class="text-gray-600 leading-relaxed mt-4">
        With the Hygge Detector App, we're bringing the power of advanced AI, computer vision, and the art of 
        design together to give you a tool that doesn’t just look at your room—it understands it.
      </p>
      <p class="text-gray-600 leading-relaxed mt-4">
        Take a photo or upload one. In just seconds, our app analyzes the lighting, the colors, the objects—the 
        very soul of your space. It gives you a simple, elegant score: your Hygge Score. And then? It tells you 
        exactly how to improve it. Need more warmth? Add a candle. Too much clutter? Simplify. Missing harmony? 
        We'll guide you.
      </p>
      <p class="text-gray-600 leading-relaxed mt-4">
        This app doesn’t just show you the numbers—it makes you feel something. It inspires you to create a sanctuary 
        for yourself, your loved ones, and your life.
      </p>
      <p class="text-gray-600 leading-relaxed mt-4">
        We believe technology should enhance your humanity. With the Hygge Detector App, we’re helping you enhance your 
        home, your mood, and your connection to what matters most.
      </p>
      <p class="text-gray-600 leading-relaxed mt-4">
        This isn't just an app. It's hygge, in your pocket.
      </p>
    </div>
  </div>

  <!-- ============ FAQ SECTION ============ -->
  <section id="faq" class="py-20 relative z-10">
    <div class="max-w-4xl mx-auto px-4">
      <h2 class="text-3xl font-bold text-gray-800 mb-8 text-center">Frequently Asked Questions</h2>
      <div class="space-y-6">
        <!-- FAQ 1 -->
        <div class="warm-shadow rounded-lg p-6 bg-white">
          <h3 class="text-xl font-semibold text-gray-800 mb-2">How do I get support for an app?</h3>
          <p class="text-gray-600">
            Each app has its own dedicated support section. Select your app above to find specific help and guidance.
          </p>
        </div>
        <!-- FAQ 2 -->
        <div class="warm-shadow rounded-lg p-6 bg-white">
          <h3 class="text-xl font-semibold text-gray-800 mb-2">How do I report an issue?</h3>
          <p class="text-gray-600">
            You can report issues through the contact form below or by emailing our support team directly.
          </p>
        </div>
        <!-- FAQ 3 -->
        <div class="warm-shadow rounded-lg p-6 bg-white">
          <h3 class="text-xl font-semibold text-gray-800 mb-2">Are my data and privacy protected?</h3>
          <p class="text-gray-600">
            Yes, we take data protection seriously. See our 
            <button onclick="showModal('privacy-modal')" class="text-blue-600 hover:underline">privacy policy</button> 
            for detailed information about how we handle your data.
          </p>
        </div>
      </div>
    </div>
  </section>

  <!-- ============ CONTACT SECTION ============ -->
<section id="contact" class="py-20 bg-white bg-opacity-90 relative z-10">
  <div class="max-w-4xl mx-auto px-4">
    <h2 class="text-3xl font-bold text-gray-800 mb-8 text-center">Contact Support</h2>
    <div class="warm-shadow rounded-lg p-8 bg-white">
      <div class="text-center">
        <p class="text-gray-600 mb-4">Need help with one of our apps? We're here to assist you!</p>
        <a href="mailto:Matthewhoytapps@gmail.com" 
           class="text-white bg-gray-800 px-6 py-3 rounded-lg hover:bg-gray-700 inline-block opacity-100 visible">
          Email Support
        </a>
      </div>
    </div>
  </div>
</section>

  <!-- ============ PRIVACY POLICY MODAL ============ -->
  <div id="privacy-modal" class="modal">
    <div class="modal-content warm-shadow">
      <span class="close-button" onclick="hideModal('privacy-modal')">&times;</span>
      <h2 class="text-3xl font-bold text-gray-800 mb-6">Privacy Policy</h2>
      <div class="space-y-6 text-gray-600">
        <section>
          <h3 class="text-xl font-semibold text-gray-800 mb-3">Information We Collect</h3>
          <p>In-App Purchases:</p>
          <ul class="list-disc pl-6 mt-2 space-y-2">
            <li>
              All payments are processed securely through Apple’s in-app purchase system. 
              We do not collect or store payment information. 
              For details on Apple’s privacy practices, please visit Apple’s Privacy Policy.
            </li>
          </ul>
          <p class="mt-4">Usage Data:</p>
          <ul class="list-disc pl-6 mt-2 space-y-2">
            <li>
              We may collect anonymous data on app usage, such as how often features are used, 
              to improve the app’s functionality.
            </li>
          </ul>
          <p class="mt-4">Images Submitted for Analysis:</p>
          <ul class="list-disc pl-6 mt-2 space-y-2">
            <li>Any images uploaded or taken with the app are processed locally on your device. 
                We do not store or share these images.</li>
          </ul>
        </section>
        <section>
          <h3 class="text-xl font-semibold text-gray-800 mb-3">How We Use Your Data</h3>
          <p>Unlocking Premium Features:</p>
          <ul class="list-disc pl-6 mt-2 space-y-2">
            <li>We use purchase confirmation data to enable premium features or subscriptions.</li>
          </ul>
          <p class="mt-4">Improving the App:</p>
          <ul class="list-disc pl-6 mt-2 space-y-2">
            <li>Anonymous usage data helps us refine the app and add new features.</li>
          </ul>
        </section>
        <section>
          <h3 class="text-xl font-semibold text-gray-800 mb-3">Data Sharing</h3>
          <ul class="list-disc pl-6 mt-2 space-y-2">
            <li>
              We do not sell or share your personal information with third parties. 
              Payment data is securely handled by Apple.
            </li>
          </ul>
        </section>
        <section>
          <h3 class="text-xl font-semibold text-gray-800 mb-3">Your Rights</h3>
          <ul class="list-disc pl-6 mt-2 space-y-2">
            <li>You can manage or cancel subscriptions via your Apple account.</li>
            <li>If you have any concerns about your data, please contact us at Matthewhoytapps@gmail.com.</li>
          </ul>
        </section>
        <section>
          <h3 class="text-xl font-semibold text-gray-800 mb-3">Updates to This Policy</h3>
          <ul class="list-disc pl-6 mt-2 space-y-2">
            <li>
              We may update this policy from time to time. Changes will be posted within the app and on our website.
            </li>
          </ul>
        </section>
        <section>
          <h3 class="text-xl font-semibold text-gray-800 mb-3">How We Use Your Information</h3>
          <p>We use the collected information to:</p>
          <ul class="list-disc pl-6 mt-2 space-y-2">
            <li>Provide and improve our services</li>
            <li>Analyze app performance and fix issues</li>
            <li>Communicate with you about updates and support</li>
          </ul>
        </section>
        <section>
          <h3 class="text-xl font-semibold text-gray-800 mb-3">Contact Us</h3>
          <p>If you have any questions about this privacy policy, please contact us at <strong>Matthewhoytapps@gmail.com</strong></p>
        </section>
      </div>
    </div>
  </div>
  <!-- ============ TERMS OF SERVICE MODAL ============ -->
  <div id="terms-modal" class="modal">
    <div class="modal-content warm-shadow">
      <span class="close-button" onclick="hideModal('terms-modal')">&times;</span>
      <h2 class="text-3xl font-bold text-gray-800 mb-6">Terms of Service</h2>
      <div class="space-y-6 text-gray-600">
        <section>
          <h3 class="text-xl font-semibold text-gray-800 mb-3">Acceptance of Terms</h3>
          <p>
            By downloading, installing, or using our applications, you agree to be bound by these Terms of Service. 
            If you do not agree, please stop using our apps.
          </p>
        </section>
        <section>
          <h3 class="text-xl font-semibold text-gray-800 mb-3">License to Use</h3>
          <p>Personal Use Only:</p>
          <ul class="list-disc pl-6 mt-2 space-y-2">
            <li>
              We grant you a limited, non-exclusive, non-transferable license to use our applications for personal, 
              non-commercial purposes.
            </li>
          </ul>
          <p class="mt-4">Age Requirement:</p>
          <ul class="list-disc pl-6 mt-2 space-y-2">
            <li>
              You must be at least 13 years old to use our apps. If you are under 18, you must have parental or 
              guardian consent.
            </li>
          </ul>
        </section>
        <section>
          <h3 class="text-xl font-semibold text-gray-800 mb-3">In-App Purchases</h3>
          <p>Our apps may offer optional in-app purchases, such as premium features or subscriptions</p>
          <ul class="list-disc pl-6 mt-2 space-y-2">
            <li>All purchases are processed securely through in-app purchases.</li>
            <li>Purchased features are non-transferable and non-refundable unless required by applicable law.</li>
          </ul>
        </section>
        <section>
          <h3 class="text-xl font-semibold text-gray-800 mb-3">Intellectual Property</h3>
          <ul class="list-disc pl-6 mt-2 space-y-2">
            <li>
              All content, logos, and materials in Hygge Detector are owned by us and protected by copyright laws. 
              You may not copy, modify, distribute, or sell any part of the app.
            </li>
          </ul>
        </section>
        <section>
          <h3 class="text-xl font-semibold text-gray-800 mb-3">API Use</h3>
          <ul class="list-disc pl-6 mt-2 space-y-2">
            <li>
              Some of our apps use OpenAI’s API to generate content for analysis and recommendations. 
              All usage complies with OpenAI's terms of service and privacy policies.
            </li>
          </ul>
        </section>
        <section>
          <h3 class="text-xl font-semibold text-gray-800 mb-3">Disclaimer of Warranties</h3>
          <ul class="list-disc pl-6 mt-2 space-y-2">
            <li>Apps are provided "as is" without warranties of any kind, either express or implied.</li>
            <li>We do not guarantee the accuracy, reliability, or suitability of the app’s results.</li>
          </ul>
        </section>
        <section>
          <h3 class="text-xl font-semibold text-gray-800 mb-3">Limitation of Liability</h3>
          <ul class="list-disc pl-6 mt-2 space-y-2">
            <li>
              To the maximum extent permitted by law, we are not liable for any damages arising from your use of the app, 
              including indirect, incidental, or consequential damages.
            </li>
          </ul>
        </section>
        <section>
          <h3 class="text-xl font-semibold text-gray-800 mb-3">Termination</h3>
          <ul class="list-disc pl-6 mt-2 space-y-2">
            <li>
              We reserve the right to terminate or suspend your access to the app at any time, with or without notice, 
              if you violate these Terms and Conditions.
            </li>
          </ul>
        </section>
        <section>
          <h3 class="text-xl font-semibold text-gray-800 mb-3">Governing Law</h3>
          <ul class="list-disc pl-6 mt-2 space-y-2">
            <li>
              These terms are governed by the laws of The United States of America. Any disputes will be resolved exclusively 
              in the courts of The United States of America.
            </li>
          </ul>
        </section>
        <section>
          <h3 class="text-xl font-semibold text-gray-800 mb-3">Changes to Terms</h3>
          <ul class="list-disc pl-6 mt-2 space-y-2">
            <li>
              We may update these Terms and Conditions from time to time. Updates will be posted within the app and on our 
              website.
            </li>
          </ul>
        </section>
        <section>
          <h3 class="text-xl font-semibold text-gray-800 mb-3">Contact Information</h3>
          <p>
            If you have any questions about these Terms of Service, please contact us at 
            <strong>Matthewhoytapps@gmail.com</strong>
          </p>
        </section>
      </div>
    </div>
  </div>

  <!-- ============ FOOTER ============ -->
  <footer class="bg-gray-800 text-white py-8 text-center relative z-10">
    <p>&copy; 2024 Matthew Hoyt. All rights reserved.</p>
  </footer>

  <!-- ============ JAVASCRIPT ============ -->
  <script>

       const canvas = document.getElementById('specks');
const ctx = canvas.getContext('2d');

function resizeCanvas() {
  canvas.width = window.innerWidth;
  canvas.height = window.innerHeight;
}

resizeCanvas();

// Define paths that mimic the reference image pattern
// Each path is defined as a series of control points for Bezier curves
const paths = [
  // Diagonal paths with rounded corners
  {
    points: function(t) {
      const cellSize = 300; // Size of one pattern cell
      const cornerRadius = 50; // How rounded the corners are
      
      // Calculate base position in the grid
      const gridX = Math.floor(t * canvas.width / cellSize) * cellSize;
      const gridY = Math.floor(t * canvas.height / cellSize) * cellSize;
      
      // Position within current cell
      const localT = (t * canvas.width) % cellSize / cellSize;
      
      // Create diagonal path with rounded corners
      if (localT < 0.2) {
        // Round the corner
        const angle = localT * Math.PI / 0.4;
        return {
          x: gridX + cornerRadius * (1 - Math.cos(angle)),
          y: gridY + cornerRadius * (1 - Math.sin(angle))
        };
      } else if (localT < 0.8) {
        // Diagonal line
        const progress = (localT - 0.2) / 0.6;
        return {
          x: gridX + cornerRadius + progress * (cellSize - 2 * cornerRadius),
          y: gridY + cornerRadius + progress * (cellSize - 2 * cornerRadius)
        };
      } else {
        // Round the corner
        const angle = (localT - 0.8) * Math.PI / 0.4 + Math.PI/2;
        return {
          x: gridX + cellSize - cornerRadius + cornerRadius * Math.cos(angle),
          y: gridY + cellSize - cornerRadius + cornerRadius * Math.sin(angle)
        };
      }
    }
  },
  // Add more path variations here for the complete pattern
];

// Create specks that will follow the paths
const specks = [];
const numSpecks = 150; // Increased number for better coverage of paths

for (let i = 0; i < numSpecks; i++) {
  specks.push({
    pathIndex: Math.floor(Math.random() * paths.length),
    pathProgress: Math.random(), // Random starting position on path
    speed: Math.random() * 0.0002 + 0.0001, // Varied speeds for more organic movement
    radius: Math.random() * 2 + 1, // Slightly smaller for a more delicate look
    opacity: Math.random() * 0.3 + 0.2, // More subtle opacity
    pulse: Math.random() * Math.PI * 2,
    pulseSpeed: Math.random() * 0.02 + 0.01
  });
}

function drawSpecks() {
  ctx.clearRect(0, 0, canvas.width, canvas.height);

  specks.forEach(speck => {
    // Update position along path
    speck.pathProgress += speck.speed;
    if (speck.pathProgress > 1) {
      speck.pathProgress = 0;
      // Optionally switch to a different path
      speck.pathIndex = Math.floor(Math.random() * paths.length);
    }

    // Calculate position on path
    const position = paths[speck.pathIndex].points(speck.pathProgress);

    // Update pulse effect
    speck.pulse += speck.pulseSpeed;
    const pulseEffect = Math.sin(speck.pulse) * 0.15;
    const currentOpacity = speck.opacity + pulseEffect;

    // Draw speck with soft gradient
    const gradient = ctx.createRadialGradient(
      position.x, position.y, 0,
      position.x, position.y, speck.radius * 2
    );
    
    gradient.addColorStop(0, `rgba(255, 255, 255, ${currentOpacity})`);
    gradient.addColorStop(0.5, `rgba(255, 255, 255, ${currentOpacity * 0.5})`);
    gradient.addColorStop(1, 'rgba(255, 255, 255, 0)');
    
    ctx.beginPath();
    ctx.fillStyle = gradient;
    ctx.arc(position.x, position.y, speck.radius * 2, 0, Math.PI * 2);
    ctx.fill();
  });
  
  requestAnimationFrame(drawSpecks);
}

// Add the SVG pattern for the visible lines
const svgPattern = `
<svg width="100%" height="100%" style="position: fixed; top: 0; left: 0; z-index: 0; opacity: 0.1;">
  <defs>
    <pattern id="linePattern" x="0" y="0" width="300" height="300" patternUnits="userSpaceOnUse">
      <path d="M0,0 Q50,50 300,300" fill="none" stroke="currentColor" stroke-width="1"/>
      <path d="M300,0 Q250,50 0,300" fill="none" stroke="currentColor" stroke-width="1"/>
    </pattern>
  </defs>
  <rect width="100%" height="100%" fill="url(#linePattern)"/>
</svg>`;

document.body.insertAdjacentHTML('afterbegin', svgPattern);

// Start the animation
drawSpecks();

// Handle window resizing
window.addEventListener('resize', resizeCanvas);

    /* ========== MOBILE MENU TOGGLE ========== */
    const menuBtn = document.getElementById('menu-btn');
    const mobileMenu = document.getElementById('mobile-menu');

    menuBtn.addEventListener('click', () => {
      mobileMenu.classList.toggle('hidden');
    });

    /* ========== MODAL FUNCTIONS ========== */
    function showModal(modalId) {
      document.getElementById(modalId).classList.add('active');
      document.body.style.overflow = 'hidden'; /* Prevent scrolling behind the modal */
    }

    function hideModal(modalId) {
      document.getElementById(modalId).classList.remove('active');
      document.body.style.overflow = 'auto';
    }

    // Close modal if user clicks outside of modal content
    window.addEventListener('click', (e) => {
      if (e.target.classList.contains('modal')) {
        e.target.classList.remove('active');
        document.body.style.overflow = 'auto';
      }
    });

    // Close modal on Escape key
    document.addEventListener('keydown', (e) => {
      if (e.key === 'Escape') {
        document.querySelectorAll('.modal').forEach((modal) => {
          modal.classList.remove('active');
        });
        document.body.style.overflow = 'auto';
      }
    });
  </script>
</body>
</html>

