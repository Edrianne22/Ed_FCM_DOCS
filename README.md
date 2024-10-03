<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Documentation</title>
    <style>
        body {
            font-family: 'Arial', sans-serif;
            margin: 20px;
            background-color: #f5f5f5; /* Light background */
            color: #333; /* Dark text */
            transition: background-color 0.3s ease;
        }
        h1 {
            text-align: center;
            color: #4caf50; /* Apple green */
            margin-bottom: 20px;
            text-shadow: 2px 2px 4px rgba(0, 0, 0, 0.2);
        }
        .input-group {
            display: flex;
            align-items: center;
            margin: 10px 0;
        }
        label {
            margin-right: 10px;
            font-weight: bold;
            color: #333; /* Dark text for labels */
            width: 150px; /* Fixed width for labels */
        }
        input, textarea {
            width: calc(100% - 24px); /* Full width minus padding */
            padding: 12px;
            border: 2px solid #4caf50; /* Apple green border */
            border-radius: 5px;
            background-color: #ffffff; /* White background */
            color: #333; /* Dark text */
            transition: border 0.3s ease, background-color 0.3s ease;
        }
        /* Smaller width for specific inputs */
        #agentName, #callTime, #callDate {
            width: 120px; /* Adjusted width for 10 characters */
        }
        input:focus, textarea:focus {
            border-color: #388e3c; /* Darker green on focus */
            background-color: #f0f0f0; /* Light gray on focus */
            outline: none;
        }
        button {
            background-color: #4caf50; /* Apple green */
            color: white;
            border: none;
            padding: 12px 20px;
            border-radius: 5px;
            cursor: pointer;
            margin: 10px 5px;
            font-weight: bold;
            transition: background-color 0.3s ease, transform 0.2s ease;
            box-shadow: 0 2px 5px rgba(0, 0, 0, 0.2);
        }
        button:hover {
            background-color: #388e3c; /* Darker green on hover */
            transform: scale(1.05);
        }
        #output {
            white-space: pre-wrap;
            background-color: #ffffff; /* White background for output */
            color: #333; /* Dark text for output */
            padding: 15px;
            border: 1px solid #4caf50; /* Apple green border */
            margin-top: 20px;
            border-radius: 5px;
            box-shadow: 0 2px 5px rgba(0, 0, 0, 0.1);
            transition: background-color 0.3s ease;
        }
        #entries div {
            opacity: 0;
            animation: fadeIn 0.5s forwards;
            margin-top: 5px;
        }
        @keyframes fadeIn {
            to {
                opacity: 1;
            }
        }
    </style>
</head>
<body>

<h1>FCM Documentation</h1>

<div>
    <div class="input-group">
        <label for="agentName">Agent Name:</label>
        <input type="text" id="agentName" value="ED">
    </div>
    
    <div class="input-group">
        <label for="callTime">Call Time:</label>
        <input type="text" id="callTime" value="149A-EST">
    </div>
    
    <div class="input-group">
        <label for="callDate">Call Date:</label>
        <input type="text" id="callDate" value="02oct">
    </div>
    
    <div class="input-group">
        <label for="entryText">Documentation Entry:</label>
        <textarea id="entryText" placeholder="Enter your documentation here..."></textarea>
    </div>
    
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

<script>
    function updateCallDetails() {
        const agentName = document.getElementById('agentName').value;
        const callTime = document.getElementById('callTime').value;
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
            newEntry.style.opacity = '0';
            setTimeout(() => { newEntry.style.opacity = '1'; }, 0);
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

    // Add event listener for Enter key
    document.getElementById('entryText').addEventListener('keypress', function(event) {
        if (event.key === 'Enter') {
            event.preventDefault(); // Prevent new line in textarea
            addEntry();
        }
    });
</script>

</body>
</html>
