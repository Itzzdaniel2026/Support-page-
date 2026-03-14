ㅤㅤㅤㅤㅤㅤㅤㅤㅤㅤㅤㅤㅤㅤㅤㅤㅤㅤㅤㅤㅤㅤㅤㅤㅤㅤㅤㅤㅤㅤㅤㅤㅤㅤㅤㅤㅤㅤㅤㅤㅤㅤ

<html lang="en">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0" />
  <title>Support Page</title>
  <style>
    body {
      font-family: Arial, sans-serif;
      background: #1e1e2f;
      color: white;
      display: flex;
      justify-content: center;
      align-items: center;
      min-height: 100vh;
      margin: 0;
    }

    .container {
      background: #2a2a40;
      padding: 25px;
      border-radius: 12px;
      width: 100%;
      max-width: 420px;
      box-shadow: 0 8px 24px rgba(0,0,0,0.3);
    }

    h2 {
      text-align: center;
      margin-bottom: 20px;
    }

    label {
      display: block;
      margin-bottom: 6px;
      margin-top: 12px;
      font-weight: bold;
    }

    input,
    textarea {
      width: 100%;
      padding: 10px;
      border: none;
      border-radius: 6px;
      box-sizing: border-box;
      font-size: 14px;
    }

    textarea {
      resize: vertical;
    }

    button {
      width: 100%;
      padding: 12px;
      margin-top: 18px;
      background: #5865F2;
      border: none;
      color: white;
      font-size: 16px;
      border-radius: 6px;
      cursor: pointer;
    }

    button:hover {
      background: #4752c4;
    }

    .success,
    .error {
      display: none;
      text-align: center;
      margin-top: 15px;
      font-size: 14px;
    }

    .success {
      color: #57f287;
    }

    .error {
      color: #ed4245;
    }
  </style>
</head>
<body>
  <div class="container">
    <h2>Support Request</h2>

    <form id="supportForm">
      <label for="username">Discord Username</label>
      <input type="text" id="username" required />

      <label for="discordId">Discord ID</label>
      <input type="text" id="discordId" required />

      <label for="subject">Subject</label>
      <input type="text" id="subject" required />

      <label for="issue">Describe the Issue</label>
      <textarea id="issue" rows="5" required></textarea>

      <button type="submit">Submit Ticket</button>

      <div class="success" id="successMsg">Support request sent successfully.</div>
      <div class="error" id="errorMsg">Failed to send support request.</div>
    </form>
  </div>

  <script>
    document.getElementById("supportForm").addEventListener("submit", async function (e) {
      e.preventDefault();

      const username = document.getElementById("username").value.trim();
      const discordId = document.getElementById("discordId").value.trim();
      const subject = document.getElementById("subject").value.trim();
      const issue = document.getElementById("issue").value.trim();

      const webhookURL = "https://discord.com/api/webhooks/1482373191879102464/tOX4JSyjMtX-hjmr6mmTgE9tPwZL_2l9ubaJx7Wkd1Ba9KnqSTWLEHEcau3-DxXDnJU";

      const payload = {
        embeds: [
          {
            title: "New Support Ticket",
            color: 5763719,
            fields: [
              { name: "Discord Username", value: username || "Not provided", inline: true },
              { name: "Discord ID", value: discordId || "Not provided", inline: true },
              { name: "Subject", value: subject || "No subject", inline: false },
              { name: "Describe the Issue", value: issue || "No issue provided", inline: false }
            ],
            timestamp: new Date().toISOString()
          }
        ]
      };

      const successMsg = document.getElementById("successMsg");
      const errorMsg = document.getElementById("errorMsg");

      successMsg.style.display = "none";
      errorMsg.style.display = "none";

      try {
        const response = await fetch(webhookURL, {
          method: "POST",
          headers: {
            "Content-Type": "application/json"
          },
          body: JSON.stringify(payload)
        });

        if (response.ok) {
          successMsg.style.display = "block";
          document.getElementById("supportForm").reset();
        } else {
          errorMsg.style.display = "block";
        }
      } catch (error) {
        errorMsg.style.display = "block";
      }
    });
  </script>
</body>
</html>
