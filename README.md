# MattHoyt1.github.io

<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Hygge Detector - Support</title>
    <link rel="stylesheet" href="styles.css">
</head>
<body>
    <header class="header">
        <div class="container">
            <h1>Hygge Detector Support</h1>
            <p>Welcome to the support page for Hygge Detector.</p>
        </div>
    </header>
</body>
  <body>
    <nav class="navbar">
        <div class="container">
            <a href="#faq">FAQ</a>
            <a href="#contact">Contact Us</a>
            <a href="#privacy-policy">Privacy Policy</a>
            <a href="#terms">Terms of Use</a>
        </div>
    </nav>
  </body>
    <main>
        <section id="faq" class="section">
            <div class="container">
                <h2>Frequently Asked Questions</h2>
                <details>
                    <summary>How do I use the Hygge Detector app?</summary>
                    <p>Simply take a photo or upload one, and the app will analyze the image for hygge factors!</p>
                </details>
                <details>
                    <summary>What should I do if the app crashes?</summary>
                    <p>Ensure your device is running iOS 15 or later and try reinstalling the app.</p>
                </details>
                <details>
                    <summary>How can I restore my purchases?</summary>
                    <p>Go to the app settings and select "Restore Purchases."</p>
                </details>
            </div>
        </section>
<body>
        <section id="contact" class="section">
            <div class="container">
                <h2>Contact Us</h2>
                <p>If you have any questions or need support, please reach out:</p>
                <form action="mailto:support@hyggeapp.com" method="POST" enctype="text/plain">
                    <label for="name">Name:</label>
                    <input type="text" id="name" name="name" required>
                    <label for="email">Email:</label>
                    <input type="email" id="email" name="email" required>
                    <label for="message">Message:</label>
                    <textarea id="message" name="message" required></textarea>
                    <button type="submit">Send</button>
                </form>
            </div>
        </section>
</body>
      <body>
        <section id="privacy-policy" class="section">
            <div class="container">
                <h2>Privacy Policy</h2>
                <p>Your privacy is important to us. The app collects minimal data to provide the best user experience. For detailed information, <a href="privacy-policy.html">read our full policy</a>.</p>
            </div>
        </section>
      </body>
      <body>
        <section id="terms" class="section">
            <div class="container">
                <h2>Terms of Use</h2>
                <p>By using Hygge Detector, you agree to our terms. For details, <a href="terms.html">read our full terms</a>.</p>
            </div>
        </section>
    </main>
      </body>
      <body>
    <footer class="footer">
        <div class="container">
            <p>© 2024 Henrik A. Gomídea. All rights reserved.</p>
            <p>No part of this site may be reproduced without permission.</p>
        </div>
    </footer>
</body>
</html>



body {
    font-family: 'Avenir Next', sans-serif;
    margin: 0;
    padding: 0;
    background: linear-gradient(to bottom, #F0E4C8, #DCC8B4);
    color: #604C3E;
    line-height: 1.6;
}

.header {
    text-align: center;
    padding: 2rem 1rem;
    background: linear-gradient(to bottom, #FAF3E0, #F0E4C8);
    box-shadow: 0 2px 10px rgba(0, 0, 0, 0.1);
}

.header h1 {
    margin: 0;
    font-size: 2.5rem;
    color: #805A40;
}

.header p {
    font-size: 1rem;
    color: #604C3E;
}

.navbar {
    background: #DCC8B4;
    padding: 0.5rem 0;
}

.navbar .container {
    display: flex;
    justify-content: center;
    gap: 1rem;
}

.navbar a {
    color: #604C3E;
    text-decoration: none;
    font-size: 1.2rem;
}

.navbar a:hover {
    text-decoration: underline;
}

.section {
    padding: 2rem 1rem;
}

.section h2 {
    text-align: center;
    font-size: 2rem;
    color: #805A40;
    margin-bottom: 1rem;
}

.section .container {
    max-width: 800px;
    margin: 0 auto;
}

details {
    margin-bottom: 1rem;
    background: #FFF7E6;
    padding: 1rem;
    border-radius: 8px;
    box-shadow: 0 2px 5px rgba(0, 0, 0, 0.1);
}

details summary {
    font-weight: bold;
    cursor: pointer;
}

details p {
    margin-top: 0.5rem;
}

form {
    display: flex;
    flex-direction: column;
    gap: 1rem;
}

form label {
    font-weight: bold;
}

form input, form textarea, form button {
    font-family: inherit;
    padding: 0.5rem;
    border: 1px solid #BDAA97;
    border-radius: 4px;
}

form button {
    background: #C89666;
    color: white;
    border: none;
    cursor: pointer;
    font-size: 1rem;
}

form button:hover {
    background: #A6794E;
}

.footer {
    text-align: center;
    padding: 1rem;
    background: #DCC8B4;
    font-size: 0.9rem;
    color: #604C3E;
    border-top: 1px solid #BDAA97;
}
