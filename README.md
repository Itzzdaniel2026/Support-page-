ㅤㅤㅤㅤㅤㅤㅤㅤㅤㅤㅤㅤㅤㅤㅤㅤㅤㅤㅤㅤㅤㅤㅤㅤㅤㅤㅤㅤㅤㅤㅤㅤㅤㅤㅤㅤㅤㅤㅤㅤㅤㅤ


<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Support Request</title>

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
            width: 430px;
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

        input, textarea {
            width: 100%;
            padding: 12px;
            margin-top: 6px;
            border-radius: 8px;
            border: 1px solid #ccc;
            font-size: 15px;
            transition: 0.2s;
        }

        input:focus, textarea:focus {
            border-color: #5865F2;
            box-shadow: 0 0 5px rgba(88,101,242,0.4);
            outline: none;
        }

        #verifyBtn {
            width: 100%;
            padding: 14px;
            margin-top: 20px;
            background: #ffb347;
            color: #222;
            border: none;
            border-radius: 8px;
            font-size: 16px;
            font-weight: 600;
            cursor: pointer;
            transition: 0.2s;
        }

        #verifyBtn.verified {
            background: #43b581;
            color: white;
        }

        button[type="submit"] {
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

        button[type="submit"]:disabled {
            background: #999;
            cursor: not-allowed;
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
    <h2>Submit a Support Ticket</h2>

    <form id="supportForm">
        <label>Discord Username</label>
        <input type="text" id="username" placeholder="e.g. CoolUser#1234" required>

        <label>Discord ID</label>
        <input type="text" id="userid" placeholder="e.g. 123456789012345678" required>

        <label>Subject</label>
        <input type="text" id="subject" placeholder="Short summary of your issue" required>

        <label>Describe the Issue</label>
        <textarea id="issue" rows="5" placeholder="Tell us what’s going on..." required></textarea>

        <button id="verifyBtn" type="button">Hold 2–4 Seconds to Verify Human</button>

        <button type="submit" id="submitBtn" disabled>Submit Ticket</button>
    </form>

    <p id="responseMessage"></p>
</div>

<script>
let holdTimer;
let holdTime = 0;
let verified = false;

const verifyBtn = document.getElementById("verifyBtn");
const submitBtn = document.getElementById("submitBtn");

verifyBtn.addEventListener("mousedown", () => {
    holdTime = 0;
    holdTimer = setInterval(() => {
        holdTime++;

        if (holdTime >= 2 && holdTime <= 4) {
            verified = true;
            verifyBtn.classList.add("verified");
            verifyBtn.textContent = "Verified ✓";
            submitBtn.disabled = false;
            clearInterval(holdTimer);
        }
    }, 1000);
});

verifyBtn.addEventListener("mouseup", () => {
    clearInterval(holdTimer);
});

document.getElementById("supportForm").addEventListener("submit", function(e) {
    e.preventDefault();

    if (!verified) {
        document.getElementById("responseMessage").innerText = "Please verify you are human first.";
        document.getElementById("responseMessage").style.color = "red";
        return;
    }

    const webhookURL = "https://discord.com/api/webhooks/1482377942053949591/hoYKlEzsOZu8yz5Yz8YntJ9QIfWb43eFGA6v9c4v0CLCFGrMH1Tug65CJBtwHJ1kozbi";

    const username = document.getElementById("username").value;
    const userid = document.getElementById("userid").value;
    const subject = document.getElementById("subject").value;
    const issue = document.getElementById("issue").value;

    const message = {
        content: "<@&1482333430334099476> **New Support Request Submitted**",
        allowed_mentions: { roles: ["1482333430334099476"] },
        embeds: [
            {
                title: subject,
                color: 5814783,
                fields: [
                    { name: "Discord Username", value: username },
                    { name: "Discord ID", value: userid },
                    { name: "Issue Description", value: issue }
                ],
                timestamp: new Date()
            }
        ]
    };

    fetch(webhookURL, {
        method: "POST",
        headers: { "Content-Type": "application/json" },
        body: JSON.stringify(message)
    })
    .then(() => {
        document.getElementById("responseMessage").innerText = "Your support request has been submitted!";
        document.getElementById("responseMessage").style.color = "green";
        document.getElementById("supportForm").reset();
        submitBtn.disabled = true;
        verifyBtn.classList.remove("verified");
        verifyBtn.textContent = "Hold 2–4 Seconds to Verify Human";
        verified = false;
    })
    .catch(() => {
        document.getElementById("responseMessage").innerText = "There was an error submitting your request.";
        document.getElementById("responseMessage").style.color = "red";
    });
});
</script>

</body>
</html>

