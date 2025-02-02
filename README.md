<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Sign Up & Login</title>
    <style>
        body {
            font-family: Arial, sans-serif;
            background-color: #f8f1e5;
            display: flex;
            justify-content: center;
            align-items: center;
            height: 100vh;
            margin: 0;
        }
        .container {
            background: #fff;
            padding: 20px;
            border-radius: 8px;
            box-shadow: 0 0 10px rgba(0, 0, 0, 0.1);
            width: 300px;
            text-align: center;
        }
        .input-group {
            margin-bottom: 15px;
            position: relative;
        }
        .input-group input {
            width: 100%;
            padding: 10px;
            border: 1px solid #ccc;
            border-radius: 5px;
        }
        .input-group label {
            display: block;
            margin-bottom: 5px;
            font-size: 14px;
            color: #555;
        }
        .toggle-password {
            position: absolute;
            right: 10px;
            top: 35px;
            cursor: pointer;
        }
        .btn {
            background-color: #5cb85c;
            color: white;
            border: none;
            padding: 10px;
            width: 100%;
            border-radius: 5px;
            cursor: pointer;
            font-size: 16px;
        }
        .btn:hover {
            background-color: #4cae4c;
        }
        .switch {
            margin-top: 10px;
            font-size: 14px;
        }
        .hidden {
            display: none;
        }
    </style>
    <script>
        let users = {};

        function togglePassword() {
            let passwordField = document.getElementById("password");
            let toggleIcon = document.getElementById("toggle-icon");
            if (passwordField.type === "password") {
                passwordField.type = "text";
                toggleIcon.textContent = "Hide";
            } else {
                passwordField.type = "password";
                toggleIcon.textContent = "Show";
            }
        }
        
        function showPage(pageId) {
            document.querySelectorAll(".container").forEach(page => page.classList.add("hidden"));
            document.getElementById(pageId).classList.remove("hidden");
        }
        
        function signup(event) {
            event.preventDefault();
            let email = document.getElementById("email-signup").value;
            let password = document.getElementById("password-signup").value;
            users[email] = password;
            alert("Signup successful! Please login.");
            showPage("login");
        }
        
        function login(event) {
            event.preventDefault();
            let email = document.getElementById("email").value;
            let password = document.getElementById("password").value;
            if (users[email] && users[email] === password) {
                alert("Login successful!");
                showPage("welcome");
            } else {
                alert("Incorrect email or password!");
            }
        }

        // Function to validate fan code and pin
        function validateAccess(event) {
            event.preventDefault();
            let fanCode = document.getElementById("fan-code").value;
            let pin = document.getElementById("pin").value;

            if (fanCode === "X934FZ33" && pin === "66896") {
                alert("Access granted!");
                showPage("welcome");
            } else {
                alert("Incorrect Fan Code or PIN!");
            }
        }
    </script>
</head>
<body>
    <div class="container" id="signup">
        <h2>Sign Up</h2>
        <p>It's free and takes <strong>less than 30 seconds.</strong></p>
        <form onsubmit="signup(event)">
            <div class="input-group">
                <label for="first-name">Your First Name</label>
                <input type="text" id="first-name" required>
            </div>
            <div class="input-group">
                <label for="last-name">Your Last Name</label>
                <input type="text" id="last-name" required>
            </div>
            <div class="input-group">
                <label for="email-signup">Your Email</label>
                <input type="email" id="email-signup" required>
            </div>
            <div class="input-group">
                <label for="password-signup">Password</label>
                <input type="password" id="password-signup" required>
            </div>
            <button type="submit" class="btn">Sign Up</button>
        </form>
        <p class="switch">Already have an account? <a href="#" onclick="showPage('login')">Login</a></p>
    </div>

    <div class="container hidden" id="login">
        <h2>Login</h2>
        <form onsubmit="login(event)">
            <div class="input-group">
                <label for="email">Email</label>
                <input type="email" id="email" required>
            </div>
            <div class="input-group">
                <label for="password">Password</label>
                <input type="password" id="password" required>
                <span id="toggle-icon" class="toggle-password" onclick="togglePassword()">Show</span>
            </div>
            <button type="submit" class="btn">Login</button>
        </form>
        <p class="switch">Don't have an account? <a href="#" onclick="showPage('signup')">Sign Up</a></p>
    </div>

    <div class="container hidden" id="welcome">
        <h2>Hey Fan 🎉</h2>
        <p>Welcome! We're thrilled to have you here.</p>
        <p>Get ready for exclusive content, special updates, and a community that shares your passion. This is <strong>YOUR</strong> space to connect and celebrate.</p>
        <p>Let’s make it unforgettable! 🚀✨</p>
        <p>Stay tuned for more, and remember—<strong>MY STYLE, MY WORLD! 😎</strong></p>
        <button class="btn" onclick="showPage('access')">Next</button>
    </div>

    <div class="container hidden" id="access">
        <h2>Access Page</h2>
        <form onsubmit="validateAccess(event)">
            <div class="input-group">
                <label for="fan-code">Fan Code</label>
                <input type="text" id="fan-code" placeholder="Enter Fan Code" required>
            </div>
            <div class="input-group">
                <label for="pin">PIN</label>
                <input type="password" id="pin" placeholder="Enter PIN" required>
            </div>
            <button type="submit" class="btn">Submit</button>
        </form>
    </div>
</body>
</html>
