<!DOCTYPE html>
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
                <div class="flex items-center space-x-6">
                    <a href="#home" class="py-4 px-2 text-gray-700 hover:text-gray-900">Home</a>
                    <a href="#apps" class="py-4 px-2 text-gray-700 hover:text-gray-900">Apps</a>
                    <a href="#faq" class="py-4 px-2 text-gray-700 hover:text-gray-900">FAQ</a>
                    <a href="#contact" class="py-4 px-2 text-gray-700 hover:text-gray-900">Contact</a>
                    <button onclick="showModal('privacy-modal')" class="py-4 px-2 text-gray-700 hover:text-gray-900">Privacy</button>
                    <button onclick="showModal('terms-modal')" class="py-4 px-2 text-gray-700 hover:text-gray-900">Terms</button>
                </div>
            </div>
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
                    <a href="#" class="text-blue-600 hover:underline">Learn More</a>
                </div>
            </div>
        </div>
    </section>

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
                    <a href="mailto:Matthoyt1@yahoo.com" class="inline-block bg-gray-800 text-white px-6 py-3 rounded-lg hover:bg-gray-700 transition-colors">Email Support</a>
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
                    <h3 class="text-xl font-semibold text-gray-800 mb-3">1. Information We Collect</h3>
                    <p>We collect information that you provide directly to us when using our applications:</p>
                    <ul class="list-disc pl-6 mt-2 space-y-2">
                        <li>User-provided content and analysis requests</li>
                        <li>Device information and usage statistics</li>
                        <li>Crash reports and performance data</li>
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
                    <p>If you have any questions about this privacy policy, please contact us at Matthoyt1@yahoo.com</p>
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
                    <p>By downloading, installing, or using our applications, you agree to be bound by these Terms of Service.</p>
                </section>
                <section>
                    <h3 class="text-xl font-semibold text-gray-800 mb-3">2. License to Use</h3>
                    <p>We grant you a limited, non-exclusive, non-transferable license to use our applications for personal, non-commercial purposes.</p>
                </section>
                <section>
                    <h3 class="text-xl font-semibold text-gray-800 mb-3">3. Contact Information</h3>
                    <p>If you have any questions about these Terms of Service, please contact us at Matthoyt1@yahoo.com</p>
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

