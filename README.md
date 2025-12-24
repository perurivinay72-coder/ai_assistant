<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Interview Question Generator</title>

    <style>
        body {
            font-family: Arial, sans-serif;
            background: #f4f6f8;
            padding: 40px;
        }

        .container {
            max-width: 600px;
            margin: auto;
            background: white;
            padding: 30px;
            border-radius: 8px;
        }

        h2 {
            text-align: center;
        }

        input {
            width: 100%;
            padding: 10px;
            margin-top: 10px;
            font-size: 16px;
        }

        button {
            width: 100%;
            padding: 12px;
            margin-top: 15px;
            background: #007bff;
            color: white;
            border: none;
            font-size: 16px;
            cursor: pointer;
        }

        button:hover {
            background: #0056b3;
        }

        .output {
            margin-top: 20px;
            white-space: pre-line;
        }
    </style>
</head>

<body>

<div class="container">
    <h2>Interview Question Generator</h2>

    <input type="text" id="role" placeholder="Enter Job Role (e.g., Java Developer)">
    <button onclick="generateQuestions()">Generate Questions</button>

    <div class="output" id="result"></div>
</div>

<script>
function generateQuestions() {
    const role = document.getElementById("role").value;
    const result = document.getElementById("result");

    if (!role) {
        result.innerText = "Please enter a job role.";
        return;
    }

    result.innerText = "Generating questions...";

    fetch("https://vinay-peruri-48.app.n8n.cloud/webhook/interview-questions", {
        method: "POST",
        headers: {
            "Content-Type": "application/json"
        },
        body: JSON.stringify({ role: role })
    })
    .then(response => response.json())
    .then(data => {
        result.innerText = data.output;
    })
    .catch(error => {
        result.innerText = "Error connecting to server.";
    });
}
</script>

</body>
</html>
