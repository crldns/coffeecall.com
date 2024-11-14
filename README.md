<!DOCTYPE html>
<html lang="en">

<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Coffee Call - Order Your Coffee</title>
    <style>
        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
            font-family: Arial, sans-serif;
        }
        
        body {
            display: flex;
            justify-content: center;
            align-items: center;
            flex-direction: column;
            min-height: 100vh;
            background: #81653896;
            color: #41210a;
        }
        
        .navbar {
            width: 100%;
            background: #c1a259e8;
            padding: 10px;
            display: flex;
            justify-content: space-between;
            align-items: center;
            color: #0c0c0c;
            position: fixed;
            top: 0;
            left: 0;
            z-index: 100;
        }
        
        .navbar h2 {
            display: flex;
            align-items: center;
            margin-left: 20px;
        }
        
        .logo-image {
            width: 90px;
            /* Adjust the width as needed */
            height: auto;
            margin-right: 15px;
            /* Space between logo and text */
            vertical-align: middle;
        }
        
        .navbar ul {
            display: flex;
            list-style-type: none;
            margin-right: 20px;
        }
        
        .navbar ul li {
            margin-left: 20px;
        }
        
        .navbar ul li a {
            color: black;
            text-decoration: none;
            font-size: 2em;
            transition: color 0.3s;
        }
        
        .navbar ul li a:hover {
            color: #000000;
        }
        
        .order-container {
            width: 400px;
            text-align: center;
            background: #a46b1ca1;
            padding: 20px;
            border-radius: 10px;
            box-shadow: 0 4px 8px rgba(0, 0, 0, 0.2);
            margin-top: 70px;
        }
        
        .order-container h1 {
            color: #000000;
            margin-bottom: 20px;
        }
        
        .step {
            display: none;
        }
        
        .active-step {
            display: block;
        }
        
        .coffee-cup {
            width: 150px;
            height: 200px;
            margin: 20px auto;
            background: #D3B88C;
            border-radius: 0 0 50% 50%;
            border: 5px solid #4A2E1A;
        }
        
        .controls,
        .step-buttons,
        .nav-buttons {
            display: flex;
            justify-content: space-around;
            margin-top: 10px;
        }
        
        button {
            padding: 10px 20px;
            margin: 5px;
            border: none;
            border-radius: 5px;
            cursor: pointer;
            background: #4A2E1A;
            color: #ade89b;
            transition: background 0.3s;
        }
        
        button:hover {
            background: #7C5A44;
        }
        
        #message {
            margin-top: 20px;
            font-size: 1.2em;
        }
        
        .about-section {
            margin-top: 30px;
            padding: 20px;
            background: #fcfcfc;
            border-radius: 10px;
            box-shadow: 0 4px 8px rgba(0, 0, 0, 0.621);
            text-align: center;
            display: none;
        }
        
        .social-icons {
            display: flex;
            gap: 15px;
            justify-content: center;
            margin-top: 50px;
            margin-bottom: 50px;
        }
        
        .social-icons a img {
            width: 30px;
            height: 30px;
            transition: opacity 0.3s;
        }
        
        .social-icons a img:hover {
            opacity: 0.7;
        }
        
        .price {
            font-size: 1.1em;
            margin-top: 10px;
            color: #94735b;
        }
    </style>
</head>

<body>
    <!-- Navigation Bar -->
    <div class="navbar">
        <h2> <img src="D:\MY HTML\COFFEE.png" alt="Coffee Call Logo" class="logo-image"> Coffee Call </h2>
        <ul>
            <li><a href="javascript:void(0);" id="aboutUsLink">About Us</a></li>
        </ul>
    </div>
    <!-- About Us Section -->
    <div id="aboutUsSection" class="about-section">
        <h2>About Us</h2>
        <p>Our story began in <strong>2015</strong> with a passion for crafting the perfect cup of coffee. What started as a small shop has grown into a beloved community hub where coffee lovers gather. At Coffee Call, every order is made with love and dedication
            to bring you the best experience.</p>
    </div>
    <div class="order-container">
        <h1>Order Your Coffee</h1>
        <div class="coffee-cup" id="coffeeCup"></div>
        <!-- Step 1: Customer Name and Cup Size -->
        <div class="step active-step" id="step1"> <label for="customerName">Enter Your Name:</label> <input type="text" id="customerName" placeholder="Your Name" required><br><br> <label for="cupSize">Choose Cup Size:</label> <select id="cupSize"> <option value="">Select a size</option> <option value="Short">Short - ₱125.00</option> <option value="Tall">Tall - ₱150.00</option> <option value="Grande">Grande - ₱175.00</option> <option value="Venti">Venti - ₱200.00</option> </select>            </div>
        <!-- Step 2: Sugar Level -->
        <div class="step" id="step2"> <label for="sugarLevel">Choose Sugar Level:</label> <input type="range" id="sugarLevel" min="25" max="150" step="25" value="100">
            <p id="sugarLevelValue">Sugar Level: 100%</p>
        </div>
        <!-- Navigation Buttons for Steps -->
        <div class="step-buttons"> <button id="prevStep" disabled>Previous</button> <button id="nextStep">Next</button> </div>
        <p id="message"></p>
    </div>
    <!-- Social Media Section (at the bottom) -->
    <!-- Social Media Section (at the bottom) -->
    <div class="social-icons">
        <a href="https://www.facebook.com/profile.php?id=61568806676859&mibextid=LQQJ4d" target="_blank"> <img src="https://upload.wikimedia.org/wikipedia/commons/5/51/Facebook_f_logo_%282019%29.svg" alt="Facebook"> </a>
        <a href="https://www.instagram.com/coffe_ecall?igsh=MTRlOTUyeGE5dzQxMg%3D%3D&utm_source=qr" target="_blank"> <img src="https://upload.wikimedia.org/wikipedia/commons/9/95/Instagram_logo_2022.svg" alt="Instagram"> </a>
    </div>
    <script src="https://code.jquery.com/jquery-3.6.0.min.js"></script>
    <script>
        let currentStep = 1;
        const totalSteps = 6;
        $("#aboutUsLink").click(function() {
            $("#aboutUsSection").toggle();
        });
        $("#nextStep").click(function() {
            if (currentStep < totalSteps) {
                changeStep(1);
            } else {
                placeOrder();
            }
        });
        $("#prevStep").click(function() {
            if (currentStep > 1) {
                changeStep(-1);
            }
        });

        function changeStep(direction) {
            $("#step" + currentStep).removeClass("active-step");
            currentStep += direction;
            $("#step" + currentStep).addClass("active-step");
            $("#prevStep").prop("disabled", currentStep === 1);
            $("#nextStep").text(currentStep === totalSteps ? "Place Order" : "Next");
        }
        $("#sugarLevel").on("input", function() {
            $("#sugarLevelValue").text("Sugar Level: " + $(this).val() + "%");
        });
    </script>
</body>

</html>