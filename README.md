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
            justify-content: space-between;
            flex-wrap: wrap;
        }
        .side {
            width: 48%;
        }
        .floor {
            padding: 10px;
            margin: 5px;
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
        <div id="summary-details"></div>
        <button class="button" onclick="generatePDF()">Export to PDF</button>
    </div>
</div>

<script>
    const flats = [
        { side: "East", floor: "Ground", rent: 19000, persons: 0 },
        { side: "East", floor: "1st", rent: 15500, persons: 5 },
        { side: "East", floor: "2nd", rent: 15500, persons: 6 },
        { side: "East", floor: "3rd", rent: 14500, persons: 7 },
        { side: "East", floor: "4th", rent: 14400, persons: 6 },
        { side: "East", floor: "5th", rent: 14200, persons: 3 },
        { side: "West", floor: "Ground", rent: 20500, persons: 0 },
        { side: "West", floor: "1st", rent: 16000, persons: 2 },
        { side: "West", floor: "2nd", rent: 15000, persons: 8 },
        { side: "West", floor: "3rd", rent: 14500, persons: 7 },
        { side: "West", floor: "4th", rent: 14000, persons: 2 },
        { side: "West", floor: "5th", rent: 13700, persons: 4 },
        { side: "West", floor: "6th", rent: 6000, persons: 0 }
    ];

    function renderHouse() {
        const layout = document.getElementById("house-layout");
        layout.innerHTML = "";
        flats.forEach((flat, index) => {
            layout.innerHTML += `
                <div class="floor">
                    <h4>${flat.side} ${flat.floor} Floor</h4>
                    Rent: ${flat.rent} Taka<br>
                    Persons: <input type="number" value="${flat.persons}" id="persons-${index}" onchange="updateSummary()">
                    <br>Rent Received: <select id="rent-${index}" onchange="updateSummary()">
                        <option value="no">No</option>
                        <option value="yes">Yes</option>
                    </select>
                </div>`;
        });
    }

    function updateSummary() {
        let totalRent = 0, totalUtility = 0, receivedRent = 0;
        flats.forEach((flat, index) => {
            flat.persons = parseInt(document.getElementById(`persons-${index}`).value || 0);
            let rentReceived = document.getElementById(`rent-${index}`).value === "yes";
            let utility = flat.persons * 200;
            totalRent += flat.rent;
            totalUtility += utility;
            if (rentReceived) receivedRent += flat.rent;
        });
        
        let salary = parseInt(document.getElementById("salary").value);
        let electricityBill = parseInt(document.getElementById("electricity-bill").value);
        let waterBill = parseInt(document.getElementById("water-bill").value);
        let totalExpenses = salary + electricityBill + waterBill;
        let netIncome = receivedRent - totalExpenses;
        let wifeShare = netIncome * 0.125;
        let sonShare = netIncome * 0.5833;
        let daughterShare = netIncome * 0.2917;

        document.getElementById("summary-details").innerHTML = `
            <p>Total Rent: ${totalRent} Taka</p>
            <p>Total Utility: ${totalUtility} Taka</p>
            <p>Rent Received: ${receivedRent} Taka</p>
            <p>Total Due: ${totalRent - receivedRent} Taka</p>
            <p>Total Expenses: ${totalExpenses} Taka</p>
            <p>Net Income: ${netIncome} Taka</p>
            <h4>Inheritance Distribution:</h4>
            <p>Wife: ${wifeShare.toFixed(2)} Taka</p>
            <p>Son: ${sonShare.toFixed(2)} Taka</p>
            <p>Daughter: ${daughterShare.toFixed(2)} Taka</p>
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
