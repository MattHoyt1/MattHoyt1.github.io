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
    </style>
</head>
<body class="gradient-bg min-h-screen">
    <!-- Navigation -->
    <nav class="bg-white bg-opacity-90 shadow-lg sticky top-0 z-50">
        <div class="max-w-6xl mx-auto px-4">
            <div class="flex justify-between">
                <div class="flex space-x-7">
                    <div class="flex items-center py-4">
                        <a href="index.html" class="font-bold text-2xl text-gray-700">Matthew Hoyt</a>
                    </div>
                </div>
                <div class="flex items-center space-x-6">
                    <a href="#home" class="py-4 px-2 text-gray-700 hover:text-gray-900">Home</a>
                    <a href="#apps" class="py-4 px-2 text-gray-700 hover:text-gray-900">Apps</a>
                    <a href="#faq" class="py-4 px-2 text-gray-700 hover:text-gray-900">FAQ</a>
                    <a href="#contact" class="py-4 px-2 text-gray-700 hover:text-gray-900">Contact</a>
                    <a href="privacy.html" class="py-4 px-2 text-gray-700 hover:text-gray-900">Privacy</a>
                    <a href="terms.html" class="py-4 px-2 text-gray-700 hover:text-gray-900">Terms</a>
                </div>
            </div>
        </div>
    </nav>

    <!-- Hero Section -->
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
                    <p class="text-gray-600">Yes, we take data protection seriously. See our <a href="privacy.html" class="text-blue-600 hover:underline">privacy policy</a> for detailed information about how we handle your data.</p>
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

    <!-- Privacy Policy -->
    <section id="privacy" class="py-20">
        <div class="max-w-4xl mx-auto px-4">
            <h2 class="text-3xl font-bold text-gray-800 mb-8 text-center">Privacy Policy</h2>
            <div class="warm-shadow rounded-lg p-8 bg-white">
                <div class="prose max-w-none">
                    <p class="text-gray-600">Your privacy is important to us. Our privacy policy outlines how we collect, use, and protect your data across all our applications.</p>
                    <p class="text-gray-600 mt-4">For the complete privacy policy, please see <a href="privacy.html" class="text-blue-600 hover:underline">our detailed privacy policy</a>.</p>
                </div>
            </div>
        </div>
    </section>

    <!-- Terms of Service -->
    <section id="terms" class="py-20 bg-white bg-opacity-90">
        <div class="max-w-4xl mx-auto px-4">
            <h2 class="text-3xl font-bold text-gray-800 mb-8 text-center">Terms of Service</h2>
            <div class="warm-shadow rounded-lg p-8 bg-white">
                <div class="prose max-w-none">
                    <p class="text-gray-600">By using our apps, you agree to these terms of service.</p>
                    <p class="text-gray-600 mt-4">For the complete terms of service, please see <a href="terms.html" class="text-blue-600 hover:underline">our detailed terms of service</a>.</p>
                </div>
            </div>
        </div>
    </section>

    <!-- Footer -->
    <footer class="bg-gray-800 text-white py-8">
        <div class="max-w-6xl mx-auto px-4">
            <div class="text-center">
                <p>&copy; 2024 Matthew Hoyt. All rights reserved.</p>
            </div>
        </div>
    </footer>
</body>
</html>


