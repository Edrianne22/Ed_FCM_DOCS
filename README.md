<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Documentation</title>
    <link href="https://fonts.googleapis.com/css2?family=Roboto:wght@700&display=swap" rel="stylesheet">
    <style>
        body {
            font-family: 'Arial', sans-serif;
            margin: 0;
            height: 100vh;
            animation: backgroundAnimation 10s infinite alternate;
            display: flex;
            align-items: center;
            justify-content: center;
            position: relative;
            overflow: hidden;
        }

        @keyframes backgroundAnimation {
            0% { background-color: #66bb6a; }
            50% { background-color: #81c784; }
            100% { background-color: #a5d6a7; }
        }

        .container {
            background: rgba(255, 255, 255, 0.9);
            padding: 30px;
            border-radius: 10px;
            box-shadow: 0 4px 20px rgba(0, 0, 0, 0.2);
            width: 600px;
            position: relative;
            z-index: 1;
        }

        h1 {
            color: #388e3c;
            margin-bottom: 15px;
            font-size: 26px;
            font-family: 'Roboto', sans-serif;
            display: flex;
            align-items: center;
        }

        .logo {
            width: 50px;
            margin-right: 10px;
        }

        .input-group {
            display: flex;
            margin: 10px 0;
            align-items: center;
        }

        label {
            margin-right: 10px;
            font-weight: bold;
            color: #333;
            width: 120px;
            font-size: 16px;
        }

        input, textarea {
            padding: 10px;
            border: 2px solid #4caf50;
            border-radius: 5px;
            width: calc(100% - 130px);
            font-size: 14px;
            transition: border 0.3s ease;
        }

        input:focus, textarea:focus {
            border-color: #388e3c;
            outline: none;
        }

        button {
            background-color: #4caf50;
            color: white;
            border: none;
            padding: 10px 15px;
            border-radius: 5px;
            cursor: pointer;
            margin: 5px 0;
            font-size: 14px;
            transition: background-color 0.3s ease;
        }

        button:hover {
            background-color: #388e3c;
        }

        #output {
            white-space: pre-wrap;
            background: #fff;
            padding: 15px;
            border-radius: 5px;
            border: 1px solid #4caf50;
            margin-top: 15px;
            font-size: 14px;
            text-align: left;
            max-height: 200px;
            overflow-y: auto;
        }

        .button-group {
            display: flex;
            justify-content: space-between;
            margin-top: 15px;
        }

        footer {
            position: absolute;
            bottom: 10px;
            right: 10px;
            font-size: 12px;
            color: #333;
        }

        .flying-logos {
            position: absolute;
            top: 0;
            left: 0;
            width: 100%;
            height: 100%;
            overflow: hidden;
            z-index: 0;
        }

        .logo-icon {
            position: absolute;
            width: 40px;
            opacity: 0.7;
            animation: flyLogo 10s infinite linear;
        }

        @keyframes flyLogo {
            0% {
                transform: translateY(100vh) translateX(-50%);
            }
            100% {
                transform: translateY(-100px) translateX(50%);
            }
        }
    </style>
</head>
<body>

<div class="flying-logos">
    <!-- Generate 50 Flying Logos -->
    <script>
        for (let i = 0; i < 50; i++) {
            const logo = document.createElement('img');
            logo.src = "https://logowik.com/content/uploads/images/fcm-travel-solution5417.jpg"; // Logo URL
            logo.alt = "Logo";
            logo.className = "logo-icon";
            logo.style.left = `${Math.random() * 100}%`;
            logo.style.animationDuration = `${Math.random() * 5 + 5}s`;
            logo.style.animationDelay = `${Math.random() * 5}s`;
            document.querySelector('.flying-logos').appendChild(logo);
        }
    </script>
</div>

<div class="container">
    <h1>
        <img src="https://logowik.com/content/uploads/images/fcm-travel-solution5417.jpg" alt="Logo" class="logo">
        FCM Documentation
    </h1>

    <div class="input-group">
        <label for="agentName">Agent Name:</label>
        <input type="text" id="agentName" placeholder="Enter Name" required>
    </div>
    
    <div class="input-group">
        <label for="callTime">Call Time:</label>
        <input type="text" id="callTime" placeholder="Enter Time" required>
    </div>
    
    <div class="input-group">
        <label for="callDate">Call Date:</label>
        <input type="text" id="callDate" readonly>
    </div>
    
    <div class="input-group">
        <label for="entryText">Entry:</label>
        <textarea id="entryText" placeholder="Documentation..." required></textarea>
    </div>
    
    <div class="button-group">
        <button onclick="addEntry()">Add Entry</button>
        <button onclick="clearEntries()">Clear</button>
        <button onclick="copyOutput()">Copy</button>
    </div>

    <div id="output">
        5H-ECC DOCUMENTATION START******************************<br>
        §5H-** EMERGENCY CUSTOMER CARE ** <span id="callDetails"></span> **<br>
        <div id="entries"></div>
        §5H-ECC DOCUMENTATION END********************************
    </div>

    <footer>
        Developed by Edrianne James T. Salutin
    </footer>
</div>

<script>
    function updateCallDetails() {
        const agentName = document.getElementById('agentName').value || "ED";
        const callTime = document.getElementById('callTime').value || "149A-EST";
        const callDate = document.getElementById('callDate').value;
        document.getElementById('callDetails').innerText = `${agentName}/${callTime}/${callDate}`;
    }

    function addEntry() {
        updateCallDetails();
        const entryText = document.getElementById('entryText').value.trim();
        if (entryText) {
            const entriesDiv = document.getElementById('entries');
            const newEntry = document.createElement('div');
            newEntry.innerText = `§5H-${entryText}`;
            entriesDiv.appendChild(newEntry);
            document.getElementById('entryText').value = ''; // Clear the textarea
        }
    }

    function clearEntries() {
        document.getElementById('entries').innerHTML = '';
    }

    function copyOutput() {
        const output = document.getElementById('output').innerText;
        navigator.clipboard.writeText(output).then(() => {
            alert('Output copied to clipboard!');
        });
    }

    function setTodayDate() {
        const today = new Date();
        const monthNames = ["JAN", "FEB", "MAR", "APR", "MAY", "JUN", "JUL", "AUG", "SEP", "OCT", "NOV", "DEC"];
        const formattedDate = `${("0" + today.getDate()).slice(-2)}${monthNames[today.getMonth()]}`;
        document.getElementById('callDate').value = formattedDate;
    }

    setTodayDate();

    document.getElementById('entryText').addEventListener('keypress', function(event) {
        if (event.key === 'Enter') {
            event.preventDefault();
            addEntry();
        }
    });
</script>

</body>
</html>
