<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Mirpur House Rent Calculator</title>
    <style>
        body {
            font-family: Arial, sans-serif;
            margin: 0;
            padding: 0;
            background-color: #f5f5f5;
        }
        .container {
            max-width: 1200px;
            margin: 20px auto;
            padding: 20px;
            background-color: white;
            border-radius: 10px;
            box-shadow: 0px 4px 6px rgba(0, 0, 0, 0.1);
        }
        h1 {
            text-align: center;
            color: #007BFF;
        }
        .house-layout {
            display: flex;
            flex-direction: column-reverse;
            align-items: center;
        }
        .floor-row {
            display: flex;
            width: 80%;
            justify-content: space-between;
            margin-bottom: 5px;
        }
        .unit {
            width: 48%;
            padding: 10px;
            background-color: #e8e8e8;
            text-align: center;
            border-radius: 5px;
        }
        .summary {
            margin-top: 30px;
            background-color: #f2f2f2;
            padding: 20px;
            border-radius: 5px;
        }
        .button {
            padding: 10px 20px;
            background-color: #FF5733;
            color: white;
            border: none;
            cursor: pointer;
            border-radius: 5px;
        }
    </style>
</head>
<body>

<div class="container">
    <h1>Mirpur House Rent Calculator</h1>
    <div class="house-layout" id="house-layout"></div>
    
    <div class="summary">
        <h3>Summary</h3>
        <div id="summary-details"></div>
        <button class="button" onclick="generatePDF()">Export to PDF</button>
    </div>
</div>

<script>
    const floors = ["Ground", "1st", "2nd", "3rd", "4th", "5th", "6th"];
    const flats = {
        "East": [19000, 15500, 15500, 14500, 14400, 14200, 0],
        "West": [20500, 16000, 15000, 14500, 14000, 13700, 6000]
    };

    function renderHouse() {
        const layout = document.getElementById("house-layout");
        layout.innerHTML = "";
        for (let i = 6; i >= 0; i--) {
            layout.innerHTML += `
                <div class="floor-row">
                    <div class="unit">
                        <h4>East ${floors[i]} Floor</h4>
                        Rent: ${flats["East"][i]} Taka<br>
                        Persons: <input type="number" value="0" id="east-${i}-persons" onchange="updateSummary()">
                        <br>Rent Received: <select id="east-${i}-rent" onchange="updateSummary()">
                            <option value="no">No</option>
                            <option value="yes">Yes</option>
                        </select>
                    </div>
                    <div class="unit">
                        <h4>West ${floors[i]} Floor</h4>
                        Rent: ${flats["West"][i]} Taka<br>
                        Persons: <input type="number" value="0" id="west-${i}-persons" onchange="updateSummary()">
                        <br>Rent Received: <select id="west-${i}-rent" onchange="updateSummary()">
                            <option value="no">No</option>
                            <option value="yes">Yes</option>
                        </select>
                    </div>
                </div>`;
        }
    }

    function updateSummary() {
        let totalRent = 0, totalUtility = 0, receivedRent = 0, totalDue = 0;
        for (let i = 0; i <= 6; i++) {
            ["East", "West"].forEach(side => {
                let rent = flats[side][i];
                let persons = parseInt(document.getElementById(`${side.toLowerCase()}-${i}-persons`).value || 0);
                let rentReceived = document.getElementById(`${side.toLowerCase()}-${i}-rent`).value === "yes";
                let utility = persons * 200;
                
                totalRent += rent;
                totalUtility += utility;
                if (rentReceived) receivedRent += rent;
                else totalDue += rent;
            });
        }

        document.getElementById("summary-details").innerHTML = `
            <p>Total Rent: ${totalRent} Taka</p>
            <p>Total Utility: ${totalUtility} Taka</p>
            <p>Rent Received: ${receivedRent} Taka</p>
            <p>Total Due: ${totalDue} Taka</p>
        `;
    }

    function generatePDF() {
        const { jsPDF } = window.jspdf;
        const doc = new jsPDF();
        doc.text("Mirpur House Rent Summary", 10, 10);
        doc.text(document.getElementById("summary-details").innerText, 10, 20);
        doc.save("Mirpur_House_Rent_Summary.pdf");
    }

    window.onload = () => { renderHouse(); updateSummary(); };
</script>
</body>
</html>
