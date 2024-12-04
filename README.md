<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Login Page</title>
    <style>
        @import url('https://fonts.googleapis.com/css2?family=Permanent+Marker&display=swap'); /* Font Graffiti */

        body {
            margin: 0;
            padding: 0;
            font-family: 'Permanent Marker', cursive;
            background-image: url('https://images.unsplash.com/photo-1579547621706-1a9c79d5d5c4'); /* Background URL */
            background-size: cover;
            background-position: center;
            display: flex;
            justify-content: center;
            align-items: center;
            height: 100vh;
            color: white;
        }
        .login-container {
            background-color: rgba(0, 0, 0, 0.7);
            padding: 20px;
            border-radius: 20px;
            box-shadow: 0px 4px 6px rgba(0, 0, 0, 0.5);
            text-align: center;
            width: 400px;
            max-width: 90%;
        }
        .login-container h1 {
            margin-bottom: 20px;
            font-size: 24px;
        }
        .login-container input {
            width: 80%;
            padding: 10px;
            margin: 10px 0;
            border: none;
            border-radius: 20px;
            outline: none;
            text-align: center;
        }
        .login-container input::placeholder {
            color: #aaa;
        }
        .login-container button {
            padding: 10px 20px;
            background-color: #ff5722;
            color: white;
            border: none;
            border-radius: 20px;
            cursor: pointer;
            font-size: 16px;
        }
        .login-container button:hover {
            background-color: #e64a19;
        }
        .login-container .captcha {
            margin: 15px 0;
        }
        .captcha-images {
            display: flex;
            justify-content: space-around;
            margin: 10px 0;
        }
        .captcha-images img {
            width: 70px;
            height: 70px;
            cursor: pointer;
            border: 3px solid transparent;
            border-radius: 10px;
        }
        .captcha-images img.selected {
            border-color: lime;
        }
        .success-message {
            font-size: 16px;
            color: lime;
            margin-top: 10px;
            display: none;
        }
        .error-message {
            font-size: 14px;
            color: yellow;
            display: none;
        }
    </style>
</head>
<body>
    <div class="login-container">
        <h1>Login</h1>
        <form id="loginForm">
            <input type="text" id="username" placeholder="Username" required>
            <input type="password" id="password" placeholder="Password" required>
            
            <div class="captcha">
                <p id="captcha-question"></p>
                <div class="captcha-images" id="captcha-images">
                    <!-- Gambar akan dimuat secara dinamis -->
                </div>
                <input type="hidden" id="captcha-answer">
            </div>

            <button type="submit">Login</button>
        </form>
        <p id="success-message" class="success-message">Selamat bekerja, password anda benar, gunakan dengan bijak ya titid</p>
        <p id="error-message" class="error-message">Ngapain kont*l? Ini website-nya Isa Dwi Pariyanto ganteng dan tidak boleh di-bobol!</p>
    </div>

    <script>
        const loginForm = document.getElementById('loginForm');
        const errorMessage = document.getElementById('error-message');
        const successMessage = document.getElementById('success-message');
        const captchaQuestion = document.getElementById('captcha-question');
        const captchaImages = document.getElementById('captcha-images');
        const captchaAnswer = document.getElementById('captcha-answer');

        // Username dan password yang benar
        const correctUsername = "isadwi";
        const correctPassword = "123";

        // Data captcha
        const captchaData = [
            { question: "Pilih gambar anjing", correct: "dog", images: [
                { src: "https://via.placeholder.com/70?text=Dog", value: "dog" },
                { src: "https://via.placeholder.com/70?text=Cat", value: "cat" },
                { src: "https://via.placeholder.com/70?text=Car", value: "car" }
            ]},
            { question: "Pilih gambar mobil", correct: "car", images: [
                { src: "https://via.placeholder.com/70?text=Dog", value: "dog" },
                { src: "https://via.placeholder.com/70?text=Cat", value: "cat" },
                { src: "https://via.placeholder.com/70?text=Car", value: "car" }
            ]},
            { question: "Pilih gambar kucing", correct: "cat", images: [
                { src: "https://via.placeholder.com/70?text=Dog", value: "dog" },
                { src: "https://via.placeholder.com/70?text=Cat", value: "cat" },
                { src: "https://via.placeholder.com/70?text=Car", value: "car" }
            ]}
        ];

        // Pilih captcha secara acak
        const currentCaptcha = captchaData[Math.floor(Math.random() * captchaData.length)];
        captchaQuestion.textContent = currentCaptcha.question;

        // Tampilkan gambar captcha
        currentCaptcha.images.forEach(image => {
            const img = document.createElement("img");
            img.src = image.src;
            img.dataset.value = image.value;
            img.addEventListener("click", function () {
                document.querySelectorAll(".captcha-images img").forEach(i => i.classList.remove("selected"));
                img.classList.add("selected");
                captchaAnswer.value = image.value;
            });
            captchaImages.appendChild(img);
        });

        loginForm.addEventListener('submit', function(event) {
            event.preventDefault();

            const username = document.getElementById('username').value;
            const password = document.getElementById('password').value;
            const selectedAnswer = captchaAnswer.value;

            if (username === correctUsername && password === correctPassword && selectedAnswer === currentCaptcha.correct) {
                // Tampilkan pesan sukses
                errorMessage.style.display = 'none';
                successMessage.style.display = 'block';

                // Redirect ke WhatsApp setelah 2 detik
                setTimeout(() => {
                    window.location.href = "https://wa.me/62895622581800";
                }, 2000);
            } else {
                // Tampilkan pesan error khusus
                successMessage.style.display = 'none';
                errorMessage.style.display = 'block';
            }
        });
    </script>
</body>
</html>
