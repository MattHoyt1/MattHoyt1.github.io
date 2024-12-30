<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Matthew Hoyt App Support</title>
    <link href="https://cdnjs.cloudflare.com/ajax/libs/tailwindcss/2.2.19/tailwind.min.css" rel="stylesheet">
    <style>
        .gradient-bg {
            background: linear-gradient(to bottom, #FAE2D2, #E6D2BE);
        }
        .warm-shadow {
            box-shadow: 0 4px 6px -1px rgba(120, 100, 80, 0.1), 0 2px 4px -1px rgba(120, 100, 80, 0.06);
        }
        .modal {
            display: none;
            position: fixed;
            top: 0;
            left: 0;
            width: 100%;
            height: 100%;
            background-color: rgba(0, 0, 0, 0.5);
            z-index: 1000;
        }
        .modal.active {
            display: block;
        }
        .modal-content {
            position: relative;
            background: white;
            margin: 2rem auto;
            padding: 2rem;
            width: 90%;
            max-width: 800px;
            max-height: 90vh;
            overflow-y: auto;
            border-radius: 0.5rem;
        }
        .close-button {
            position: absolute;
            top: 1rem;
            right: 1rem;
            font-size: 1.5rem;
            cursor: pointer;
        }
    </style>
</head>
<body class="gradient-bg min-h-screen">
    <!-- Navigation -->
    <nav class="bg-white bg-opacity-90 shadow-lg sticky top-0 z-50">
        <div class="max-w-6xl mx-auto px-4">
            <div class="flex justify-between">
                <div class="flex space-x-7">
                    <div class="flex items-center py-4">
                        <span class="font-bold text-2xl text-gray-700">Matthew Hoyt</span>
                    </div>
                </div>
                <div class="hidden md:flex items-center space-x-6">
                    <a href="#home" class="py-4 px-2 text-gray-700 hover:text-gray-900">Home</a>
                    <a href="#apps" class="py-4 px-2 text-gray-700 hover:text-gray-900">Apps</a>
                    <a href="#faq" class="py-4 px-2 text-gray-700 hover:text-gray-900">FAQ</a>
                    <a href="#contact" class="py-4 px-2 text-gray-700 hover:text-gray-900">Contact</a>
                    <button onclick="showModal('privacy-modal')" class="py-4 px-2 text-gray-700 hover:text-gray-900">Privacy</button>
                    <button onclick="showModal('terms-modal')" class="py-4 px-2 text-gray-700 hover:text-gray-900">Terms</button>
                </div>
            <div class="md:hidden flex items-center">
                    <button id="menu-btn" class="text-gray-700 focus:outline-none">
                        <svg xmlns="http://www.w3.org/2000/svg" class="h-6 w-6" fill="none" viewBox="0 0 24 24" stroke="currentColor">
                            <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M4 6h16M4 12h16m-7 6h7" />
                        </svg>
                    </button>
                </div>
            </div>
        </div>
        <div id="mobile-menu" class="hidden md:hidden">
    <a href="#home" class="block py-2 px-4 text-sm text-gray-700 hover:bg-gray-100">Home</a>
    <a href="#apps" class="block py-2 px-4 text-sm text-gray-700 hover:bg-gray-100">Apps</a>
    <a href="#faq" class="block py-2 px-4 text-sm text-gray-700 hover:bg-gray-100">FAQ</a>
    <a href="#contact" class="block py-2 px-4 text-sm text-gray-700 hover:bg-gray-100">Contact</a>
    <button onclick="showModal('privacy-modal')" class="block py-2 px-4 text-sm text-gray-700 hover:bg-gray-100">Privacy</button>
    <button onclick="showModal('terms-modal')" class="block py-2 px-4 text-sm text-gray-700 hover:bg-gray-100">Terms</button>
</div>
    </nav>
    <!-- Main Content Sections -->
    <!-- [Previous sections remain unchanged: Hero, Apps, FAQ, Contact] -->
    <section id="home" class="py-20">
        <div class="max-w-6xl mx-auto px-4">
            <div class="text-center">
                <h1 class="text-4xl font-bold text-gray-800 mb-4">App Support Center</h1>
                <p class="text-xl text-gray-600">Find help and information for all Matthew Hoyt apps</p>
            </div>
        </div>
    </section>
    <!-- Apps Section -->
   <section id="apps" class="py-20 bg-white bg-opacity-90">
    <div class="max-w-4xl mx-auto px-4">
        <h2 class="text-3xl font-bold text-gray-800 mb-8 text-center">Our Apps</h2>
        <div class="grid grid-cols-1 md:grid-cols-2 gap-8">
            <div class="warm-shadow rounded-lg p-6 bg-white">
                <h3 class="text-xl font-semibold text-gray-800 mb-2">Hygge Analysis</h3>
                <p class="text-gray-600 mb-4">Discover the coziness in your space with AI-powered analysis.</p>
                <button onclick="showModal('learn-more-modal')" class="text-blue-600 hover:underline">Learn More</button>
            </div>
        </div>
    </div>
</section>

<!-- Learn More Modal -->
<div id="learn-more-modal" class="modal">
    <div class="modal-content warm-shadow">
        <span class="close-button" onclick="hideModal('learn-more-modal')">&times;</span>
        <h2 class="text-3xl font-bold text-gray-800 mb-4">What is hygge?</h2>
        <p class="text-gray-600 leading-relaxed">
            Now, you might be wondering, "What is hygge?" Hygge is the Danish art of creating a space that feels warm, inviting, and, yes, perfectly cozy. And until today, understanding hygge was subjective, elusive—a feeling. But not anymore.
        </p>
        <p class="text-gray-600 leading-relaxed mt-4">
            With the Hygge Detector App, we're bringing the power of advanced AI, computer vision, and the art of design together to give you a tool that doesn’t just look at your room—it understands it.
        </p>
        <p class="text-gray-600 leading-relaxed mt-4">
            Take a photo or upload one. In just seconds, our app analyzes the lighting, the colors, the objects—the very soul of your space. It gives you a simple, elegant score: your Hygge Score. And then? It tells you exactly how to improve it. Need more warmth? Add a candle. Too much clutter? Simplify. Missing harmony? We'll guide you.
        </p>
        <p class="text-gray-600 leading-relaxed mt-4">
            This app doesn’t just show you the numbers—it makes you feel something. It inspires you to create a sanctuary for yourself, your loved ones, and your life.
        </p>
        <p class="text-gray-600 leading-relaxed mt-4">
            We believe technology should enhance your humanity. With the Hygge Detector App, we’re helping you enhance your home, your mood, and your connection to what matters most.
        </p>
        <p class="text-gray-600 leading-relaxed mt-4">
            This isn't just an app. It's hygge, in your pocket.
        </p>
    </div>
</div>
    <!-- FAQ Section -->
    <section id="faq" class="py-20">
        <div class="max-w-4xl mx-auto px-4">
            <h2 class="text-3xl font-bold text-gray-800 mb-8 text-center">Frequently Asked Questions</h2>
            <div class="space-y-6">
                <div class="warm-shadow rounded-lg p-6 bg-white">
                    <h3 class="text-xl font-semibold text-gray-800 mb-2">How do I get support for an app?</h3>
                    <p class="text-gray-600">Each app has its own dedicated support section. Select your app above to find specific help and guidance.</p>
                </div>
                <div class="warm-shadow rounded-lg p-6 bg-white">
                    <h3 class="text-xl font-semibold text-gray-800 mb-2">How do I report an issue?</h3>
                    <p class="text-gray-600">You can report issues through the contact form below or by emailing our support team directly.</p>
                </div>
                <div class="warm-shadow rounded-lg p-6 bg-white">
                    <h3 class="text-xl font-semibold text-gray-800 mb-2">Are my data and privacy protected?</h3>
                    <p class="text-gray-600">Yes, we take data protection seriously. See our <button onclick="showModal('privacy-modal')" class="text-blue-600 hover:underline">privacy policy</button> for detailed information about how we handle your data.</p>
                </div>
            </div>
        </div>
    </section>
    <!-- Contact Section -->
    <section id="contact" class="py-20 bg-white bg-opacity-90">
        <div class="max-w-4xl mx-auto px-4">
            <h2 class="text-3xl font-bold text-gray-800 mb-8 text-center">Contact Support</h2>
            <div class="warm-shadow rounded-lg p-8 bg-white">
                <div class="text-center">
                    <p class="text-gray-600 mb-4">Need help with one of our apps? We're here to assist you!</p>
                    <a href="mailto:Matthewhoytapps@gmail.com" class="inline-block bg-gray-800 text-white px-6 py-3 rounded-lg hover:bg-gray-700 transition-colors">Email Support</a>
                </div>
            </div>
        </div>
    </section>
    <!-- Privacy Policy Modal -->
    <div id="privacy-modal" class="modal">
        <div class="modal-content warm-shadow">
            <span class="close-button" onclick="hideModal('privacy-modal')">&times;</span>
            <h2 class="text-3xl font-bold text-gray-800 mb-6">Privacy Policy</h2>
            <div class="space-y-6 text-gray-600">
                <section>
                    <h3 class="text-xl font-semibold text-gray-800 mb-3">Information We Collect</h3>
                    <p>In-App Purchases:</p>
                    <ul class="list-disc pl-6 mt-2 space-y-2">
                        <li>All payments are processed securely through Apple’s in-app purchase system. We do not collect or store payment information. For details on Apple’s privacy practices, please visit Apple’s Privacy Policy.</li>
                        </ul>
                        <p>Usage Data:</p>
                    <ul class="list-disc pl-6 mt-2 space-y-2">
                        <li>We may collect anonymous data on app usage, such as how often features are used, to improve the app’s functionality.</li>
                        </ul>
                         <p>Images Submitted for Analysis:</p>
                    <ul class="list-disc pl-6 mt-2 space-y-2">
                        <li>Any images uploaded or taken with the app are processed locally on your device. We do not store or share these images.</li>
                        </ul>
                </section>
                <section>
                    <h3 class="text-xl font-semibold text-gray-800 mb-3">How We Use Your Data</h3>
                    <p>Unlocking Premium Features:</p>
                    <ul class="list-disc pl-6 mt-2 space-y-2">
                        <li>We use purchase confirmation data to enable premium features or subscriptions.</li>
                        </ul>
                        <p>Improving the App:</p>
                    <ul class="list-disc pl-6 mt-2 space-y-2">
                        <li> Anonymous usage data helps us refine the app and add new features.</li>
                        </ul>
                </section>
                 <section>
                    <h3 class="text-xl font-semibold text-gray-800 mb-3">Data Sharing</h3>
                    <ul class="list-disc pl-6 mt-2 space-y-2">
                        <li>We do not sell or share your personal information with third parties. Payment data is securely handled by Apple.</li>
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
                        <li>We may update this policy from time to time. Changes will be posted within the app and on our website.

If you have any questions, feel free to contact us at Matthewhoytapps@gmail.com.</li>
                        </ul>
                </section>
                <!-- [Rest of privacy policy sections] -->
                <section>
                    <h3 class="text-xl font-semibold text-gray-800 mb-3">2. How We Use Your Information</h3>
                    <p>We use the collected information to:</p>
                    <ul class="list-disc pl-6 mt-2 space-y-2">
                        <li>Provide and improve our services</li>
                        <li>Analyze app performance and fix issues</li>
                        <li>Communicate with you about updates and support</li>
                    </ul>
                </section>
                <section>
                    <h3 class="text-xl font-semibold text-gray-800 mb-3">7. Contact Us</h3>
                    <p>If you have any questions about this privacy policy, please contact us at Matthewhoytapps@gmail.com</p>
                </section>
            </div>
        </div>
    </div>
    <!-- Terms of Service Modal -->
    <div id="terms-modal" class="modal">
        <div class="modal-content warm-shadow">
            <span class="close-button" onclick="hideModal('terms-modal')">&times;</span>
            <h2 class="text-3xl font-bold text-gray-800 mb-6">Terms of Service</h2>
            <div class="space-y-6 text-gray-600">
                <section>
                    <h3 class="text-xl font-semibold text-gray-800 mb-3">1. Acceptance of Terms</h3>
                    <p>By downloading, installing, or using our applications, you agree to be bound by these Terms of Service. If you do not agree, please stop using our apps. </p>
                </section>
                <section>
                    <h3 class="text-xl font-semibold text-gray-800 mb-3">2. License to Use</h3>
                    <p>Personal Use Only:</p>
                     <ul class="list-disc pl-6 mt-2 space-y-2">
                        <li>We grant you a limited, non-exclusive, non-transferable license to use our applications for personal, non-commercial purposes.</li>
                        </ul>
                        <p>Age Requirement:</p>
                        <ul class="list-disc pl-6 mt-2 space-y-2">
                        <li>You must be at least 13 years old to use our apps. If you are under 18, you must have parental or gaurdian consent.</li>
                    </ul>
                </section>
                <section>
                <h3 class="text-xl font-semibold text-gray-800 mb-3">3. In-App Purchases</h3>
                <p>Our apps may offer optional in-app purchases, such as premium features or subscriptions</p>
                <ul class="list-disc pl-6 mt-2 space-y-2">
                <li>All purchases are processed securely through in-app purchases, such as premium features or subscriptions</li>
                <li>Purchased features are non-transferable and non-refundable unless required by applicable law.</li>
                </ul>
                </section>
                <section>
                    <h3 class="text-xl font-semibold text-gray-800 mb-3">2. Intellectual Property</h3>
                     <ul class="list-disc pl-6 mt-2 space-y-2">
                        <li>All content, logos, and materials in Hygge Detector are owned by us and protected by copyright laws. You may not copy, modify, distribute, or sell any part of the app.</li>
                    </ul>
                </section>
                <section>
                    <h3 class="text-xl font-semibold text-gray-800 mb-3">2. Disclaimer of Warranties</h3>
                     <ul class="list-disc pl-6 mt-2 space-y-2">
                        <li>Apps are provided "as is" without warranties of any kind, either express or implied.</li>
                        <li>We do not guarantee the accuracy, reliability, or suitability of the app’s results.</li>
                    </ul>
                </section>
                 <section>
                    <h3 class="text-xl font-semibold text-gray-800 mb-3">2. Limitation of Liability</h3>
                     <ul class="list-disc pl-6 mt-2 space-y-2">
                        <li>To the maximum extent permitted by law, we are not liable for any damages arising from your use of the app, including indirect, incidental, or consequential damages.</li>
                        </ul>
                </section>
                  <section>
                    <h3 class="text-xl font-semibold text-gray-800 mb-3">2. Termination</h3>
                     <ul class="list-disc pl-6 mt-2 space-y-2">
                        <li>We reserve the right to terminate or suspend your access to the app at any time, with or without notice, if you violate these Terms and Conditions.</li>
                        </ul>
                </section>
                <section>
                    <h3 class="text-xl font-semibold text-gray-800 mb-3">2. Governing Law</h3>
                     <ul class="list-disc pl-6 mt-2 space-y-2">
                        <li>These terms are governed by the laws of The United States of America. Any disputes will be resolved exclusively in the courts of The United States of America.</li>
                        </ul>
                </section>
                <section>
                    <h3 class="text-xl font-semibold text-gray-800 mb-3">2. Changes to Terms</h3>
                     <ul class="list-disc pl-6 mt-2 space-y-2">
                        <li>We may update these Terms and Conditions from time to time. Updates will be posted within the app and on our website.</li>
                        </ul>
                </section>
                <section>
                    <h3 class="text-xl font-semibold text-gray-800 mb-3">3. Contact Information</h3>
                    <p>If you have any questions about these Terms of Service, please contact us at Matthewhoytapps@gmail.com</p>
                </section>
            </div>
        </div>
    </div>
    <!-- Footer -->
    <footer class="bg-gray-800 text-white py-8">
        <div class="max-w-6xl mx-auto px-4">
            <div class="text-center">
                <p>&copy; 2024 Matthew Hoyt. All rights reserved.</p>
            </div>
        </div>
    </footer>
    <!-- JavaScript for Modal Functionality -->
    <script>
    document.getElementById('menu-btn').addEventListener('click', function () {
    const mobileMenu = document.getElementById('mobile-menu');
    mobileMenu.classList.toggle('hidden');
});
        function showModal(modalId) {
            document.getElementById(modalId).classList.add('active');
            document.body.style.overflow = 'hidden';
        }
        function hideModal(modalId) {
            document.getElementById(modalId).classList.remove('active');
            document.body.style.overflow = 'auto';
        }
        // Close modal when clicking outside
        window.onclick = function(event) {
            if (event.target.classList.contains('modal')) {
                event.target.classList.remove('active');
                document.body.style.overflow = 'auto';
            }
        }
        // Close modal on escape key
        document.addEventListener('keydown', function(event) {
            if (event.key === 'Escape') {
                document.querySelectorAll('.modal').forEach(modal => {
                    modal.classList.remove('active');
                });
                document.body.style.overflow = 'auto';
            }
        });
    </script>
</body>
</html>

