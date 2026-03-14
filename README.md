ㅤㅤㅤㅤㅤㅤㅤㅤㅤㅤㅤㅤㅤㅤㅤㅤㅤㅤㅤㅤㅤㅤㅤㅤㅤㅤㅤㅤㅤㅤㅤㅤㅤㅤㅤㅤㅤㅤㅤㅤㅤㅤ


<html lang="en">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>Discord Support Form</title>

<style>
body{
    font-family: Arial, sans-serif;
    background:#1e1e2f;
    color:white;
    display:flex;
    justify-content:center;
    align-items:center;
    height:100vh;
}

.container{
    background:#2a2a40;
    padding:25px;
    border-radius:10px;
    width:350px;
}

h2{
    text-align:center;
}

input, textarea{
    width:100%;
    padding:10px;
    margin-top:8px;
    margin-bottom:15px;
    border:none;
    border-radius:5px;
}

button{
    width:100%;
    padding:10px;
    background:#5865F2;
    border:none;
    color:white;
    font-size:16px;
    border-radius:5px;
    cursor:pointer;
}

button:hover{
    background:#4752c4;
}

.success{
    display:none;
    text-align:center;
    margin-top:10px;
    color:#4CAF50;
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
<input type="text" id="discordId" required>

<label>Subject</label>
<input type="text" id="subject" required>

<label>Describe the Issue</label>
<textarea id="issue" rows="4" required></textarea>

<button type="submit">Submit Ticket</button>

<div class="success" id="successMsg">Support request sent!</div>

</form>
</div>

<script>

document.getElementById("supportForm").addEventListener("submit", async function(e){
    e.preventDefault();

    const username = document.getElementById("username").value;
    const discordId = document.getElementById("discordId").value;
    const subject = document.getElementById("subject").value;
    const issue = document.getElementById("issue").value;

    const webhookURL = "YOUR_WEBHOOK_HERE";

    const payload = {
        embeds: [{
            title: "New Support Ticket",
            color: 5814783,
            fields: [
                { name: "Discord Username", value: username, inline: true },
                { name: "Discord ID", value: discordId, inline: true },
                { name: "Subject", value: subject, inline: false },
                { name: "Issue", value: issue, inline: false }
            ],
            timestamp: new Date()
        }]
    };

    await fetch(webhookURL, {
        method: "POST",
        headers: { "Content-Type": "application/json" },
        body: JSON.stringify(payload)
    });

    document.getElementById("successMsg").style.display = "block";
    document.getElementById("supportForm").reset();
});

</script>

</body>
</html>
