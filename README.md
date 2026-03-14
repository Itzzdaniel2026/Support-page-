ㅤㅤㅤㅤㅤㅤㅤㅤㅤㅤㅤㅤㅤㅤㅤㅤㅤㅤㅤㅤㅤㅤㅤㅤㅤㅤㅤㅤㅤㅤㅤㅤㅤㅤㅤㅤㅤㅤㅤㅤㅤㅤ


<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Support Form</title>
    <style>
        body {
            font-family: Arial, sans-serif;
            background: #f4f4f4;
            padding: 20px;
        }
        .container {
            max-width: 500px;
            margin: auto;
            background: white;
            padding: 20px;
            border-radius: 8px;
            box-shadow: 0 0 10px rgba(0,0,0,0.1);
        }
        input, textarea, button {
            width: 100%;
            margin-top: 10px;
            padding: 10px;
            border-radius: 5px;
            border: 1px solid #ccc;
        }
        button {
            background: #5865F2;
            color: white;
            cursor: pointer;
            border: none;
        }
        button:hover {
            background: #4752C4;
        }
    </style>
</head>
<body>

<div class="container">
    <h2>Support Request</h2>

    <form id="supportForm">
        <label>Discord Username</label>
        <input type="text" id="username" required>

        <label>Discord ID</label>
        <input type="text" id="userid" required>

        <label>Subject</label>
        <input type="text" id="subject" required>

        <label>Describe the Issue</label>
        <textarea id="issue" rows="5" required></textarea>

        <button type="submit">Submit</button>
    </form>

    <p id="responseMessage" style="margin-top:15px;"></p>
</div>

<script>
document.getElementById("supportForm").addEventListener("submit", function(e) {
    e.preventDefault();

    const webhookURL = "https://discord.com/api/webhooks/1482373191879102464/tOX4JSyjMtX-hjmr6mmTgqE9tPwZL_2l9ubaJx7Wkd1Ba9KnqSTWLEHEcau3-DxXDnJU";

    const username = document.getElementById("username").value;
    const userid = document.getElementById("userid").value;
    const subject = document.getElementById("subject").value;
    const issue = document.getElementById("issue").value;

    const message = {
        content: "**New Support Request Submitted**",
        embeds: [
            {
                title: subject,
                color: 5814783,
                fields: [
                    { name: "Discord Username", value: username, inline: false },
                    { name: "Discord ID", value: userid, inline: false },
                    { name: "Issue Description", value: issue, inline: false }
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
    .then(response => {
        document.getElementById("responseMessage").innerText = "Your support request has been submitted.";
        document.getElementById("supportForm").reset();
    })
    .catch(error => {
        document.getElementById("responseMessage").innerText = "There was an error submitting your request.";
    });
});
</script>

</body>
</html>

