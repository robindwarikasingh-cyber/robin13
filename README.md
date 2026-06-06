[index.html](https://github.com/user-attachments/files/28667171/index.html)
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Registration Page</title>
    <style>
        * {
            box-sizing: border-box;
            font-family: Arial, Helvetica, sans-serif;
        }

        body {
            margin: 0;
            min-height: 100vh;
            background: linear-gradient(135deg, #0a2342, #1d4e89, #2a9d8f);
            display: flex;
            justify-content: center;
            align-items: center;
            padding: 20px;
        }

        .container {
            width: 100%;
            max-width: 460px;
            background-color: #ffffff;
            border-radius: 16px;
            box-shadow: 0 10px 30px rgba(0, 0, 0, 0.25);
            overflow: hidden;
        }

        .header {
            background-color: #0a2342;
            color: white;
            text-align: center;
            padding: 25px 20px;
        }

        .header h1 {
            margin: 0;
            font-size: 26px;
        }

        .header p {
            margin: 8px 0 0;
            font-size: 14px;
            color: #d9f3ee;
        }

        .security-note {
            background-color: #eef8f6;
            color: #0a2342;
            padding: 12px 18px;
            font-size: 14px;
            border-left: 5px solid #2a9d8f;
            margin: 18px;
            border-radius: 8px;
        }

        form {
            padding: 0 22px 24px;
        }

        label {
            display: block;
            margin-top: 15px;
            font-weight: bold;
            color: #0a2342;
            font-size: 14px;
        }

        input {
            width: 100%;
            padding: 12px;
            margin-top: 6px;
            border: 1px solid #cccccc;
            border-radius: 8px;
            font-size: 15px;
        }

        input:focus {
            outline: none;
            border-color: #2a9d8f;
            box-shadow: 0 0 5px rgba(42, 157, 143, 0.4);
        }

        input::placeholder {
            color: #666666;
            font-size: 13px;
        }

        .field-hint {
            font-size: 12px;
            color: #555555;
            margin-top: 5px;
        }

        button {
            width: 100%;
            margin-top: 22px;
            padding: 13px;
            background-color: #2a9d8f;
            border: none;
            color: white;
            font-size: 16px;
            font-weight: bold;
            border-radius: 8px;
            cursor: pointer;
        }

        button:hover {
            background-color: #23867b;
        }

        #messageBox {
            margin-top: 18px;
            padding: 14px;
            border-radius: 8px;
            font-size: 14px;
            display: none;
            line-height: 1.5;
        }

        .error {
            background-color: #ffe9e9;
            color: #8a1f1f;
            border: 1px solid #e6a1a1;
        }

        .success {
            background-color: #e8f7ee;
            color: #1f6f3c;
            border: 1px solid #8fd19e;
        }

        .footer {
            text-align: center;
            padding: 15px;
            background-color: #f4f6f8;
            font-size: 12px;
            color: #555555;
        }
    </style>
</head>
<body>
    <div class="container">
        <div class="header">
            <h1>Registration Page</h1>
            <p>Robin Secure Banking Portal</p>
            <p>Secure | Simple | Convenient</p>
        </div>

        <div class="security-note">
            Create your secure online banking profile. The field hints explain the validation rules before registration can continue.
        </div>

        <form id="registrationForm" onsubmit="return validateForm()">
            <label for="username">Username</label>
            <input type="text" id="username" name="username" placeholder="At least 5 characters, no spaces">

            <label for="password">Password</label>
            <input type="password" id="password" name="password" placeholder="8+ chars: upper, lower, number & special character">

            <label for="confirmPassword">Confirm password</label>
            <input type="password" id="confirmPassword" name="confirmPassword" placeholder="Must match the password entered above">

            <label for="email">Email id</label>
            <input type="text" id="email" name="email" placeholder="Enter a valid email, e.g. name@example.com">

            <label for="dob">Date of Birth</label>
            <input type="date" id="dob" name="dob" title="Select your date of birth. You must be at least 18 years old.">
            <div class="field-hint">Must not be a future date. User must be at least 18 years old.</div>

            <button type="submit">Submit Registration</button>

            <div id="messageBox"></div>
        </form>

        <div class="footer">
            This registration page was created by Robin Dwarikasingh as a personal JavaScript form validation project inspired by secure online banking.
        </div>
    </div>

    <script>
        function validateForm() {
            let username = document.getElementById("username").value.trim();
            let password = document.getElementById("password").value;
            let confirmPassword = document.getElementById("confirmPassword").value;
            let email = document.getElementById("email").value.trim();
            let dob = document.getElementById("dob").value;
            let messageBox = document.getElementById("messageBox");
            let messages = [];

            // Validation 1: Check that all fields are filled in
            if (username === "" || password === "" || confirmPassword === "" || email === "" || dob === "") {
                messages.push("All fields are required.");
            }

            // Validation 2: Username should be at least 5 characters and should not contain spaces
            if (username.length > 0 && username.length < 5) {
                messages.push("Username must be at least 5 characters long.");
            }

            if (username.includes(" ")) {
                messages.push("Username must not contain spaces.");
            }

            // Validation 3: Password strength check
            let passwordPattern = /^(?=.*[a-z])(?=.*[A-Z])(?=.*\d)(?=.*[!@#$%^&*]).{8,}$/;
            if (password.length > 0 && !passwordPattern.test(password)) {
                messages.push("Password must be at least 8 characters and include uppercase, lowercase, number, and special character.");
            }

            // Validation 4: Password and confirm password must match
            if (password !== confirmPassword) {
                messages.push("Password and Confirm password must match.");
            }

            // Validation 5: Email must be in a valid format
            let emailPattern = /^[^\s@]+@[^\s@]+\.[^\s@]+$/;
            if (email.length > 0 && !emailPattern.test(email)) {
                messages.push("Please enter a valid email address.");
            }

            // Validation 6: User must be at least 18 years old and date cannot be in the future
            if (dob !== "") {
                let birthDate = new Date(dob);
                let today = new Date();
                let age = today.getFullYear() - birthDate.getFullYear();
                let monthDifference = today.getMonth() - birthDate.getMonth();

                if (monthDifference < 0 || (monthDifference === 0 && today.getDate() < birthDate.getDate())) {
                    age--;
                }

                if (birthDate > today) {
                    messages.push("Date of Birth cannot be a future date.");
                } else if (age < 18) {
                    messages.push("User must be at least 18 years old to register for online banking.");
                }
            }

            if (messages.length > 0) {
                messageBox.style.display = "block";
                messageBox.className = "error";
                messageBox.innerHTML = "<strong>Please correct the following:</strong><br>" + messages.join("<br>");
                return false;
            } else {
                messageBox.style.display = "block";
                messageBox.className = "success";
                messageBox.innerHTML = "Registration details accepted. Your secure online banking profile can now be created.";
                return false;
            }
        }
    </script>
</body>
</html>
