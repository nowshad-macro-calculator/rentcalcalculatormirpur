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
            margin-bottom: 30px;
        }
        .side {
            width: 45%;
        }
        .floor {
            padding: 10px;
            margin: 5px;
            background-color: #e8e8e8;
            text-align: center;
            border-radius: 5px;
            cursor: pointer;
        }
        .floor input {
            width: 80px;
        }
        .summary {
            margin-top: 30px;
            background-color: #f2f2f2;
            padding: 20px;
            border-radius: 5px;
        }
        .record-section {
            margin-top: 20px;
            text-align: center;
        }
        .button {
            padding: 10px 20px;
            background-color: #FF5733;
            color: white;
            border: none;
            cursor: pointer;
            border-radius: 5px;
        }
        .button:hover {
            background-color: #FF2D00;
        }
        table {
            width: 100%;
            border-collapse: collapse;
            margin-top: 20px;
        }
        table, th, td {
            border: 1px solid #ddd;
        }
        th, td {
            padding: 10px;
            text-align: center;
        }
        .input-field {
            margin-top: 10px;
        }
        .input-field label {
            margin-right: 10px;
        }
    </style>
    <!-- Include jsPDF library -->
    <script src="https://cdnjs.cloudflare.com/ajax/libs/jspdf/2.5.1/jspdf.umd.min.js"></script>
</head>
<body>

<div class="container">
    <h1>Mirpur House Rent Calculator</h1>

    <!-- House Layout (East and West Sides) -->
    <div class="house-layout">
        <!-- East Side -->
        <div class="side">
            <h3>East Side</h3>
            <!-- Flats from Ground to 6th Floor -->
            <div class="floor" id="east-ground">
                <span>East Side Ground Floor</span> - 19000 Taka
                <input type="checkbox" id="east-ground-checkbox" onchange="updateFlatData('east', 0)">
                <input type="number" id="east-ground-persons" value="0" placeholder="No. of persons" onchange="updateFlatData('east', 0)">
                <input type="number" id="east-ground-utility-service" value="0" placeholder="Utility & Service Charge" onchange="updateFlatData('east', 0)">
                <span id="east-ground-total">Grand Total: 19000 Taka</span>
                <span id="east-ground-due">Due: 19000 Taka</span>
            </div>
            <!-- Repeat similar blocks for other floors -->
            <div class="floor" id="east-1st">
                <span>East Side 1st Floor</span> - 15500 Taka
                <input type="checkbox" id="east-1st-checkbox" onchange="updateFlatData('east', 1)">
                <input type="number" id="east-1st-persons" value="5" placeholder="No. of persons" onchange="updateFlatData('east', 1)">
                <input type="number" id="east-1st-utility-service" value="0" placeholder="Utility & Service Charge" onchange="updateFlatData('east', 1)">
                <span id="east-1st-total">Grand Total: 16500 Taka</span>
                <span id="east-1st-due">Due: 15500 Taka</span>
            </div>
            <!-- Add additional floors similarly -->
        </div>

        <!-- West Side -->
        <div class="side">
            <h3>West Side</h3>
            <!-- Flats from Ground to 6th Floor -->
            <div class="floor" id="west-ground">
                <span>West Side Ground Floor</span> - 20500 Taka
                <input type="checkbox" id="west-ground-checkbox" onchange="updateFlatData('west', 0)">
                <input type="number" id="west-ground-persons" value="0" placeholder="No. of persons" onchange="updateFlatData('west', 0)">
                <input type="number" id="west-ground-utility-service" value="0" placeholder="Utility & Service Charge" onchange="updateFlatData('west', 0)">
                <span id="west-ground-total">Grand Total: 20500 Taka</span>
                <span id="west-ground-due">Due: 20500 Taka</span>
            </div>
            <!-- Repeat similar blocks for other floors -->
            <div class="floor" id="west-1st">
                <span>West Side 1st Floor</span> - 16000 Taka
                <input type="checkbox" id="west-1st-checkbox" onchange="updateFlatData('west', 1)">
                <input type="number" id="west-1st-persons" value="2" placeholder="No. of persons" onchange="updateFlatData('west', 1)">
                <input type="number" id="west-1st-utility-service" value="0" placeholder="Utility & Service Charge" onchange="updateFlatData('west', 1)">
                <span id="west-1st-total">Grand Total: 16400 Taka</span>
                <span id="west-1st-due">Due: 16000 Taka</span>
            </div>
            <!-- Add additional floors similarly -->
        </div>
    </div>

    <!-- Summary Section -->
    <div class="summary">
        <h3>Summary</h3>
        <table>
            <thead>
                <tr>
                    <th>Flat</th>
                    <th>Rent</th>
                    <th>Utility & Service Charge</th>
                    <th>Grand Total</th>
                    <th>Due Rent</th>
                </tr>
            </thead>
            <tbody id="summary-tbody">
                <!-- Summary rows will be populated here -->
            </tbody>
        </table>

        <div class="input-field">
            <label for="salary-deduction">Salary Deduction (10000 Taka): </label>
            <input type="number" id="salary-deduction" value="10000" onchange="updateTotal()">
        </div>

        <div class="input-field">
            <label for="water-bill">Water Bill: </label>
            <input type="number" id="water-bill" value="200" onchange="updateTotal()">
        </div>

        <div class="input-field">
            <label for="electricity-bill">Electricity Bill: </label>
            <input type="number" id="electricity-bill" value="0" onchange="updateTotal()">
        </div>

        <div class="record-section">
            <button class="button" onclick="calculateExpenses()">Calculate After Expenses</button>
            <button class="button" onclick="exportToPDF()">Export to PDF</button>
        </div>

        <h4>Total Rent Received: <span id="total-rent-received">0</span></h4>
        <h4>Total Expenses: <span id="total-expenses">0</span></h4>
        <h4>Total After Expenses: <span id="final-total">0</span></h4>

        <h4>Inheritance Distribution</h4>
        <p>Wife: <span id="wife-share">0</span></p>
        <p>Son: <span id="son-share">0</span></p>
        <p>Daughter: <span id="daughter-share">0</span></p>

        <h4>Total Rent: <span id="total-rent">0</span></h4>
        <h4>Total Utility & Service Charge: <span id="total-utility-service">0</span></h4>
        <h4>Total Grand Total: <span id="total-grand-total">0</span></h4>
    </div>
</div>

<script>
    let flatData = {
        "east": [
            { rent: 19000, persons: 0, received: 0, utilityService: 0, grandTotal: 19000, due: 19000 },
            { rent: 15500, persons: 5, received: 0, utilityService: 1000, grandTotal: 16500, due: 15500 },
            { rent: 15500, persons: 6, received: 0, utilityService: 1200, grandTotal: 16700, due: 15500 },
            { rent: 14500, persons: 7, received: 0, utilityService: 1400, grandTotal: 15900, due: 14500 },
            { rent: 14400, persons: 6, received: 0, utilityService: 1200, grandTotal: 15600, due: 14400 },
            { rent: 14200, persons: 3, received: 0, utilityService: 600, grandTotal: 14800, due: 14200 },
            { rent: 0, persons: 0, received: 0, utilityService: 0, grandTotal: 0, due: 0 }
        ],
        "west": [
            { rent: 20500, persons: 0, received: 0, utilityService: 0, grandTotal: 20500, due: 20500 },
            { rent: 16000, persons: 2, received: 0, utilityService: 400, grandTotal: 16400, due: 16000 },
            { rent: 15000, persons: 8, received: 0, utilityService: 1600, grandTotal: 16600, due: 15000 },
            { rent: 14500, persons: 7, received: 0, utilityService: 1400, grandTotal: 15900, due: 14500 },
            { rent: 14000, persons: 2, received: 0, utilityService: 400, grandTotal: 14400, due: 14000 },
            { rent: 13700, persons: 4, received: 0, utilityService: 800, grandTotal: 14500, due: 13700 },
            { rent: 6000, persons: 0, received: 0, utilityService: 0, grandTotal: 6000, due: 6000 }
        ]
    };

    function updateFlatData(side, floorIndex) {
        let persons = document.getElementById(`${side}-${floorIndex}-persons`).value;
        let utilityServiceCharge = document.getElementById(`${side}-${floorIndex}-utility-service`).value;
        let checkbox = document.getElementById(`${side}-${floorIndex}-checkbox`);

        flatData[side][floorIndex].persons = persons;
        flatData[side][floorIndex].utilityService = persons * 200 + parseInt(utilityServiceCharge);

        if (checkbox.checked) {
            flatData[side][floorIndex].received = flatData[side][floorIndex].rent;
            flatData[side][floorIndex].due = 0;
        } else {
            flatData[side][floorIndex].received = 0;
            flatData[side][floorIndex].due = flatData[side][floorIndex].rent;
        }

        flatData[side][floorIndex].grandTotal = flatData[side][floorIndex].rent + flatData[side][floorIndex].utilityService;

        document.getElementById(`${side}-${floorIndex}-total`).innerText = `Grand Total: ${flatData[side][floorIndex].grandTotal} Taka`;
        document.getElementById(`${side}-${floorIndex}-due`).innerText = `Due: ${flatData[side][floorIndex].due} Taka`;

        calculateTotalRentReceived();
    }

    function calculateTotalRentReceived() {
        let totalRentReceived = 0;
        for (let side in flatData) {
            for (let floorIndex in flatData[side]) {
                totalRentReceived += flatData[side][floorIndex].received;
            }
        }
        document.getElementById("total-rent-received").innerText = totalRentReceived;
    }

    function calculateExpenses() {
        let totalReceived = 0;
        let totalExpenses = parseInt(document.getElementById("salary-deduction").value) + parseInt(document.getElementById("water-bill").value) + parseInt(document.getElementById("electricity-bill").value);
        let summaryHtml = '';
        let totalRent = 0;
        let totalUtilityService = 0;
        let totalGrandTotal = 0;

        for (let side in flatData) {
            for (let floorIndex in flatData[side]) {
                let flat = flatData[side][floorIndex];
                totalReceived += flat.received;
                totalRent += flat.rent;
                totalUtilityService += flat.utilityService;
                totalGrandTotal += flat.grandTotal;

                summaryHtml += `
                    <tr>
                        <td>${side.charAt(0).toUpperCase() + side.slice(1)} ${parseInt(floorIndex)+1} Floor</td>
                        <td>${flat.rent}</td>
                        <td>${flat.utilityService}</td>
                        <td>${flat.grandTotal}</td>
                    </tr>
                `;
            }
        }

        document.getElementById("summary-tbody").innerHTML = summaryHtml;

        let totalAfterDeductions = totalReceived - totalExpenses;

        let wifeShare = totalAfterDeductions * 0.125;
        let sonShare = totalAfterDeductions * 0.5833;
        let daughterShare = totalAfterDeductions * 0.2917;

        document.getElementById("final-total").innerText = totalAfterDeductions;
        document.getElementById("wife-share").innerText = wifeShare.toFixed(2);
        document.getElementById("son-share").innerText = sonShare.toFixed(2);
        document.getElementById("daughter-share").innerText = daughterShare.toFixed(2);

        document.getElementById("total-rent-received").innerText = totalReceived;
        document.getElementById("total-expenses").innerText = totalExpenses;
        document.getElementById("total-rent").innerText = totalRent;
        document.getElementById("total-utility-service").innerText = totalUtilityService;
        document.getElementById("total-grand-total").innerText = totalGrandTotal;
    }

    function exportToPDF() {
        const { jsPDF } = window.jspdf;
        const doc = new jsPDF();

        doc.text("Mirpur House Rent Calculator Summary", 10, 10);

        const summaryTable = document.getElementById("summary-tbody");
        let summaryText = "Flat | Rent | Utility & Service Charge | Grand Total\n";
        
        for (let row of summaryTable.rows) {
            summaryText += `${row.cells[0].innerText} | ${row.cells[1].innerText} | ${row.cells[2].innerText} | ${row.cells[3].innerText}\n`;
        }

        doc.text(summaryText, 10, 20);
        doc.save("Mirpur_House_Rent_Summary.pdf");
    }
</script>

</body>
</html>
