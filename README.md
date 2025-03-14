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
            width: 50px;
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
        .user-role {
            text-align: right;
            margin-bottom: 10px;
            color: #007BFF;
        }
        .input-field {
            margin-top: 10px;
        }
        .input-field label {
            margin-right: 10px;
        }
    </style>
</head>
<body>

<div class="container">
    <h1>Mirpur House Rent Calculator</h1>
    <div class="user-role" id="user-role">User: Parvin</div>

    <!-- House Layout (East and West Sides) -->
    <div class="house-layout">
        <!-- East Side -->
        <div class="side">
            <h3>East Side</h3>
            <div class="floor" id="east-ground">
                Ground Floor - 19000 Taka
                <input type="checkbox" id="east-ground-checkbox">
                <input type="number" id="east-ground-persons" value="0" placeholder="No. of persons" onchange="updateFlatData('east', 0)">
                <span id="east-ground-utility">Utility Bill: 0 Taka</span>
            </div>
            <div class="floor" id="east-1st">
                1st Floor - 15500 Taka
                <input type="checkbox" id="east-1st-checkbox">
                <input type="number" id="east-1st-persons" value="5" placeholder="No. of persons" onchange="updateFlatData('east', 1)">
                <span id="east-1st-utility">Utility Bill: 1000 Taka</span>
            </div>
            <div class="floor" id="east-2nd">
                2nd Floor - 15500 Taka
                <input type="checkbox" id="east-2nd-checkbox">
                <input type="number" id="east-2nd-persons" value="6" placeholder="No. of persons" onchange="updateFlatData('east', 2)">
                <span id="east-2nd-utility">Utility Bill: 1200 Taka</span>
            </div>
            <div class="floor" id="east-3rd">
                3rd Floor - 14500 Taka
                <input type="checkbox" id="east-3rd-checkbox">
                <input type="number" id="east-3rd-persons" value="7" placeholder="No. of persons" onchange="updateFlatData('east', 3)">
                <span id="east-3rd-utility">Utility Bill: 1400 Taka</span>
            </div>
            <div class="floor" id="east-4th">
                4th Floor - 14400 Taka
                <input type="checkbox" id="east-4th-checkbox">
                <input type="number" id="east-4th-persons" value="6" placeholder="No. of persons" onchange="updateFlatData('east', 4)">
                <span id="east-4th-utility">Utility Bill: 1200 Taka</span>
            </div>
            <div class="floor" id="east-5th">
                5th Floor - 14200 Taka
                <input type="checkbox" id="east-5th-checkbox">
                <input type="number" id="east-5th-persons" value="3" placeholder="No. of persons" onchange="updateFlatData('east', 5)">
                <span id="east-5th-utility">Utility Bill: 600 Taka</span>
            </div>
            <div class="floor" id="east-6th">
                6th Floor - 0 Taka (Not rented)
                <input type="checkbox" id="east-6th-checkbox">
                <input type="number" id="east-6th-persons" value="0" placeholder="No. of persons" onchange="updateFlatData('east', 6)">
                <span id="east-6th-utility">Utility Bill: 0 Taka</span>
            </div>
        </div>

        <!-- West Side -->
        <div class="side">
            <h3>West Side</h3>
            <div class="floor" id="west-ground">
                Ground Floor - 0 Taka
                <input type="checkbox" id="west-ground-checkbox">
                <input type="number" id="west-ground-persons" value="0" placeholder="No. of persons" onchange="updateFlatData('west', 0)">
                <span id="west-ground-utility">Utility Bill: 0 Taka</span>
            </div>
            <div class="floor" id="west-1st">
                1st Floor - 16000 Taka
                <input type="checkbox" id="west-1st-checkbox">
                <input type="number" id="west-1st-persons" value="2" placeholder="No. of persons" onchange="updateFlatData('west', 1)">
                <span id="west-1st-utility">Utility Bill: 400 Taka</span>
            </div>
            <div class="floor" id="west-2nd">
                2nd Floor - 15000 Taka
                <input type="checkbox" id="west-2nd-checkbox">
                <input type="number" id="west-2nd-persons" value="8" placeholder="No. of persons" onchange="updateFlatData('west', 2)">
                <span id="west-2nd-utility">Utility Bill: 1600 Taka</span>
            </div>
            <div class="floor" id="west-3rd">
                3rd Floor - 14500 Taka
                <input type="checkbox" id="west-3rd-checkbox">
                <input type="number" id="west-3rd-persons" value="7" placeholder="No. of persons" onchange="updateFlatData('west', 3)">
                <span id="west-3rd-utility">Utility Bill: 1400 Taka</span>
            </div>
            <div class="floor" id="west-4th">
                4th Floor - 14000 Taka
                <input type="checkbox" id="west-4th-checkbox">
                <input type="number" id="west-4th-persons" value="2" placeholder="No. of persons" onchange="updateFlatData('west', 4)">
                <span id="west-4th-utility">Utility Bill: 400 Taka</span>
            </div>
            <div class="floor" id="west-5th">
                5th Floor - 13700 Taka
                <input type="checkbox" id="west-5th-checkbox">
                <input type="number" id="west-5th-persons" value="4" placeholder="No. of persons" onchange="updateFlatData('west', 5)">
                <span id="west-5th-utility">Utility Bill: 800 Taka</span>
            </div>
            <div class="floor" id="west-6th">
                6th Floor - 6000 Taka
                <input type="checkbox" id="west-6th-checkbox">
                <input type="number" id="west-6th-persons" value="0" placeholder="No. of persons" onchange="updateFlatData('west', 6)">
                <span id="west-6th-utility">Utility Bill: 0 Taka</span>
            </div>
        </div>
    </div>

    <!-- Calculate Button -->
    <div class="record-section">
        <button class="button" onclick="calculateRent()">Calculate</button>
    </div>

    <!-- Summary Section -->
    <div class="summary">
        <h3>Summary</h3>
        <table>
            <tr>
                <th>Flat</th>
                <th>Rent</th>
                <th>Utility Bill</th>
                <th>Received Rent</th>
                <th>Due Rent</th>
            </tr>
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

        <h4>Total After Deductions: <span id="final-total">0</span></h4>
        <h4>Amount Distribution</h4>
        <p>Mother gets: <span id="mother-share">0</span></p>
        <p>Brother gets: <span id="brother-share">0</span></p>
        <p>Sister gets: <span id="sister-share">0</span></p>
    </div>

    <!-- Export Button -->
    <div class="record-section">
        <button class="button" onclick="exportReport()">Export Report</button>
    </div>
</div>

<script>
    let flatData = {
        "east": [
            { rent: 19000, persons: 0, received: 0, utility: 0, due: 0 },
            { rent: 15500, persons: 5, received: 0, utility: 1000, due: 0 },
            { rent: 15500, persons: 6, received: 0, utility: 1200, due: 0 },
            { rent: 14500, persons: 7, received: 0, utility: 1400, due: 0 },
            { rent: 14400, persons: 6, received: 0, utility: 1200, due: 0 },
            { rent: 14200, persons: 3, received: 0, utility: 600, due: 0 },
            { rent: 0, persons: 0, received: 0, utility: 0, due: 0 }
        ],
        "west": [
            { rent: 0, persons: 0, received: 0, utility: 0, due: 0 },
            { rent: 16000, persons: 2, received: 0, utility: 400, due: 0 },
            { rent: 15000, persons: 8, received: 0, utility: 1600, due: 0 },
            { rent: 14500, persons: 7, received: 0, utility: 1400, due: 0 },
            { rent: 14000, persons: 2, received: 0, utility: 400, due: 0 },
            { rent: 13700, persons: 4, received: 0, utility: 800, due: 0 },
            { rent: 6000, persons: 0, received: 0, utility: 0, due: 0 }
        ]
    };

    function updateFlatData(side, floorIndex) {
        let persons = document.getElementById(`${side}-${floorIndex}-persons`).value;
        flatData[side][floorIndex].persons = persons;
        flatData[side][floorIndex].utility = persons * 200;
        document.getElementById(`${side}-${floorIndex}-utility`).innerText = `Utility Bill: ${flatData[side][floorIndex].utility} Taka`;
    }

    function calculateRent() {
        let rentReceived = confirm("Has the rent been received?");
        if (rentReceived) {
            for (let side in flatData) {
                for (let floorIndex in flatData[side]) {
                    flatData[side][floorIndex].received = flatData[side][floorIndex].rent;
                    flatData[side][floorIndex].due = flatData[side][floorIndex].rent - flatData[side][floorIndex].received;
                }
            }
            updateSummary();
        }
    }

    function updateSummary() {
        let totalRent = 0, totalUtility = 0, totalReceived = 0, totalDue = 0;
        let summaryHtml = '';
        
        for (let side in flatData) {
            summaryHtml += `<tr><td colspan="5">${side.charAt(0).toUpperCase() + side.slice(1)} Side</td></tr>`;
            flatData[side].forEach((flat, index) => {
                totalRent += flat.rent;
                totalUtility += flat.utility;
                totalReceived += flat.received;
                totalDue += flat.due;
                summaryHtml += `
                    <tr>
                        <td>Flat ${index + 1}</td>
                        <td>${flat.rent}</td>
                        <td>${flat.utility}</td>
                        <td>${flat.received}</td>
                        <td>${flat.due}</td>
                    </tr>
                `;
            });
        }

        document.getElementById("summary-tbody").innerHTML = summaryHtml;
        document.getElementById("final-total").innerText = totalReceived;
        let salaryDeduction = parseInt(document.getElementById("salary-deduction").value);
        let waterBill = parseInt(document.getElementById("water-bill").value);
        let electricityBill = parseInt(document.getElementById("electricity-bill").value);
        let totalAfterDeductions = totalReceived - salaryDeduction - waterBill - electricityBill;

        let motherShare = totalAfterDeductions / 8;
        let brotherShare = 2 * motherShare;
        let sisterShare = motherShare;

        document.getElementById("mother-share").innerText = motherShare;
        document.getElementById("brother-share").innerText = brotherShare;
        document.getElementById("sister-share").innerText = sisterShare;
    }

    function exportReport() {
        let reportType = prompt("Which format would you like? Type 'PDF' or 'Excel'");
        if (reportType === 'PDF') {
            alert("PDF export coming soon!");
        } else if (reportType === 'Excel') {
            alert("Excel export coming soon!");
        } else {
            alert("Invalid format choice!");
        }
    }
</script>

</body>
</html>
