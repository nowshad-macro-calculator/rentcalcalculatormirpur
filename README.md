Mirpur rent and inheritance calculator 
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
            flex-direction: column;
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
    <script src="https://cdnjs.cloudflare.com/ajax/libs/jspdf/2.5.1/jspdf.umd.min.js"></script>
</head>
<body>

<div class="container">
    <h1>Mirpur House Rent Calculator</h1>
    <div class="house-layout" id="house-layout"></div>
    
    <div class="summary">
        <h3>Summary</h3>
        <label>Salary: <input type="number" id="salary" value="10000" onchange="updateSummary()"></label><br>
        <label>Misc Electricity Bill: <input type="number" id="electricity-bill" value="1000" onchange="updateSummary()"></label><br>
        <label>Water Bill: <input type="number" id="water-bill" value="8000" onchange="updateSummary()"></label><br>
        <label>Additional Income: <input type="number" id="additional-income" value="0" onchange="updateSummary()"></label><br>
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
    const personsDefault = {
        "East": [0, 5, 6, 7, 6, 3, 0],
        "West": [0, 2, 8, 7, 2, 4, 0]
    };

    function getCurrentMonth() {
        const date = new Date();
        return date.toLocaleString('default', { month: 'long' });
    }

    function renderHouse() {
        const layout = document.getElementById("house-layout");
        layout.innerHTML = "";
        for (let i = 6; i >= 0; i--) {
            layout.innerHTML += `
                <div class="floor-row">
                    <div class="unit">
                        <h4>East ${floors[i]} Floor</h4>
                        Rent: ${flats["East"][i]} Taka<br>
                        Persons: <input type="number" value="${personsDefault["East"][i]}" id="east-${i}-persons" onchange="updateSummary()">
                        <br>Rent Received: <select id="east-${i}-rent" onchange="updateSummary()">
                            <option value="no">No</option>
                            <option value="yes">Yes</option>
                        </select>
                    </div>
                    <div class="unit">
                        <h4>West ${floors[i]} Floor</h4>
                        Rent: ${flats["West"][i]} Taka<br>
                        Persons: <input type="number" value="${personsDefault["West"][i]}" id="west-${i}-persons" onchange="updateSummary()">
                        <br>Rent Received: <select id="west-${i}-rent" onchange="updateSummary()">
                            <option value="no">No</option>
                            <option value="yes">Yes</option>
                        </select>
                    </div>
                </div>`;
        }
    }

    function updateSummary() {
        let totalRentReceived = 0;
        let totalDue = 0;
        let totalUtility = 0;
        for (let i = 0; i <= 6; i++) {
            ["East", "West"].forEach(side => {
                let rentReceived = document.getElementById(`${side.toLowerCase()}-${i}-rent`).value === "yes" ? flats[side][i] : 0;
                let dueAmount = rentReceived === 0 ? flats[side][i] : 0;
                let utility = personsDefault[side][i] * 200;
                totalRentReceived += rentReceived;
                totalDue += dueAmount;
                totalUtility += utility;
            });
        }
        
        let salary = parseInt(document.getElementById("salary").value);
        let electricityBill = parseInt(document.getElementById("electricity-bill").value);
        let waterBill = parseInt(document.getElementById("water-bill").value);
        let additionalIncome = parseInt(document.getElementById("additional-income").value);
        let totalExpenses = salary + electricityBill + waterBill;
        let netIncome = totalRentReceived + additionalIncome - totalExpenses;
        let parvinShare = netIncome * 0.125;
        let nowshadShare = netIncome * 0.5833;
        let nowshinShare = netIncome * 0.2917;

        document.getElementById("summary-details").innerHTML = `
            <h4>${getCurrentMonth()} Summary</h4>
            <p>Total Rent Received: ${totalRentReceived + additionalIncome} Taka</p>
            <p>Additional Income: ${additionalIncome} Taka</p>
            <p>Total Due: ${totalDue} Taka</p>
            <p>Total Utility: ${totalUtility} Taka</p>
            <p>Total Expenses: ${totalExpenses} Taka</p>
            <p>Net Income: ${netIncome} Taka</p>
            <h4>Inheritance Distribution</h4>
            <p>Parvin: ${parvinShare.toFixed(2)} Taka</p>
            <p>Nowshad: ${nowshadShare.toFixed(2)} Taka</p>
            <p>Nowshin: ${nowshinShare.toFixed(2)} Taka</p>
        `;
    }

    window.onload = () => { renderHouse(); updateSummary(); };
</script>
</body>
</html>
