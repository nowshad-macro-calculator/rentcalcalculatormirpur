Nowshad's Mirpur Rent Calculator 

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
                Ground Floor - 20500 Taka
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

    <!-- Summary Section -->
    <div class="summary">
        <h3>Summary</h3>
        <table>
            <thead>
                <tr>
                    <th>Flat</th>
                    <th>Rent</th>
                    <th>Utility Bill</th>
                    <th>Total Amount</th>
                    <th>Received Rent</th>
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
        </div>

        <h4>Total After Deductions: <span id="final-total">0</span></h4>
        <h4>Amount Distribution</h4>
        <p>Wife gets: <span id="wife-share">0</span></p>
        <p>Son gets: <span id="son-share">0</span></p>
        <p>Daughter gets: <span id="daughter-share">0</span></p>

        <!-- Total Rent and Utility Summary -->
        <div>
            <h4>Total Rent: <span id="total-rent">0</span></h4>
            <h4>Total Utility: <span id="total-utility">0</span></h4>
        </div>
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
            { rent: 20500, persons: 0, received: 0, utility: 0, due: 0 }, // Updated ground floor rent for West side
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

    function calculateExpenses() {
        let totalReceived = 0;
        let totalExpenses = parseInt(document.getElementById("salary-deduction").value) + parseInt(document.getElementById("water-bill").value) + parseInt(document.getElementById("electricity-bill").value);
        let summaryHtml = '';
        let totalRent = 0;
        let totalUtility = 0;

        for (let side in flatData) {
            for (let floorIndex in flatData[side]) {
                let flat = flatData[side][floorIndex];
                let totalAmount = flat.rent + flat.utility;
                flat.received = flat.rent;  // Assuming rent is received
                flat.due = flat.rent - flat.received;
                totalReceived += flat.received;
                totalRent += flat.rent;
                totalUtility += flat.utility;

                summaryHtml += `
                    <tr>
                        <td>Flat ${floorIndex + 1}</td>
                        <td>${flat.rent}</td>
                        <td>${flat.utility}</td>
                        <td>${totalAmount}</td>
                        <td>${flat.received}</td>
                        <td>${flat.due}</td>
                    </tr>
                `;
            }
        }

        document.getElementById("summary-tbody").innerHTML = summaryHtml;

        // After deductions
        let totalAfterDeductions = totalReceived - totalExpenses;

        // Distribution logic
        let wifeShare = totalAfterDeductions * 0.125;
        let sonShare = totalAfterDeductions * 0.5833;
        let daughterShare = totalAfterDeductions * 0.2917;

        document.getElementById("final-total").innerText = totalAfterDeductions;
        document.getElementById("wife-share").innerText = wifeShare.toFixed(2);
        document.getElementById("son-share").innerText = sonShare.toFixed(2);
        document.getElementById("daughter-share").innerText = daughterShare.toFixed(2);

        // Display total rent and utility
        document.getElementById("total-rent").innerText = totalRent;
        document.getElementById("total-utility").innerText = totalUtility;
    }
</script>

</body>
</html>
