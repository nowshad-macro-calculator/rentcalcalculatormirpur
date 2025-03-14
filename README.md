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
            <div class="floor" id="east-ground">
                <span>Ground Floor</span> - 19000 Taka
                <label>Rent Received: <select id="east-ground-received" onchange="updateFlatData('east', 0)">
                    <option value="no">No</option>
                    <option value="yes">Yes</option>
                </select></label>
                <label>Persons: <input type="number" id="east-ground-persons" value="0" onchange="updateFlatData('east', 0)"></label>
                <span id="east-ground-utility">Utility: 0 Taka</span>
                <span id="east-ground-due">Due: 19000 Taka</span>
            </div>
            <div class="floor" id="east-1st">
                <span>1st Floor</span> - 15500 Taka
                <label>Rent Received: <select id="east-1st-received" onchange="updateFlatData('east', 1)">
                    <option value="no">No</option>
                    <option value="yes">Yes</option>
                </select></label>
                <label>Persons: <input type="number" id="east-1st-persons" value="5" onchange="updateFlatData('east', 1)"></label>
                <span id="east-1st-utility">Utility: 1000 Taka</span>
                <span id="east-1st-due">Due: 15500 Taka</span>
            </div>
            <div class="floor" id="east-2nd">
                <span>2nd Floor</span> - 15500 Taka
                <label>Rent Received: <select id="east-2nd-received" onchange="updateFlatData('east', 2)">
                    <option value="no">No</option>
                    <option value="yes">Yes</option>
                </select></label>
                <label>Persons: <input type="number" id="east-2nd-persons" value="6" onchange="updateFlatData('east', 2)"></label>
                <span id="east-2nd-utility">Utility: 1200 Taka</span>
                <span id="east-2nd-due">Due: 15500 Taka</span>
            </div>
            <div class="floor" id="east-3rd">
                <span>3rd Floor</span> - 14500 Taka
                <label>Rent Received: <select id="east-3rd-received" onchange="updateFlatData('east', 3)">
                    <option value="no">No</option>
                    <option value="yes">Yes</option>
                </select></label>
                <label>Persons: <input type="number" id="east-3rd-persons" value="7" onchange="updateFlatData('east', 3)"></label>
                <span id="east-3rd-utility">Utility: 1400 Taka</span>
                <span id="east-3rd-due">Due: 14500 Taka</span>
            </div>
            <div class="floor" id="east-4th">
                <span>4th Floor</span> - 14400 Taka
                <label>Rent Received: <select id="east-4th-received" onchange="updateFlatData('east', 4)">
                    <option value="no">No</option>
                    <option value="yes">Yes</option>
                </select></label>
                <label>Persons: <input type="number" id="east-4th-persons" value="6" onchange="updateFlatData('east', 4)"></label>
                <span id="east-4th-utility">Utility: 1200 Taka</span>
                <span id="east-4th-due">Due: 14400 Taka</span>
            </div>
            <div class="floor" id="east-5th">
                <span>5th Floor</span> - 14200 Taka
                <label>Rent Received: <select id="east-5th-received" onchange="updateFlatData('east', 5)">
                    <option value="no">No</option>
                    <option value="yes">Yes</option>
                </select></label>
                <label>Persons: <input type="number" id="east-5th-persons" value="3" onchange="updateFlatData('east', 5)"></label>
                <span id="east-5th-utility">Utility: 600 Taka</span>
                <span id="east-5th-due">Due: 14200 Taka</span>
            </div>
            <div class="floor" id="east-6th">
                <span>6th Floor</span> - 0 Taka (Not rented)
                <label>Rent Received: <select id="east-6th-received" onchange="updateFlatData('east', 6)">
                    <option value="no">No</option>
                    <option value="yes">Yes</option>
                </select></label>
                <label>Persons: <input type="number" id="east-6th-persons" value="0" onchange="updateFlatData('east', 6)"></label>
                <span id="east-6th-utility">Utility: 0 Taka</span>
                <span id="east-6th-due">Due: 0 Taka</span>
            </div>
        </div>

        <!-- West Side -->
        <div class="side">
            <h3>West Side</h3>
            <div class="floor" id="west-ground">
                <span>Ground Floor</span> - 20500 Taka
                <label>Rent Received: <select id="west-ground-received" onchange="updateFlatData('west', 0)">
                    <option value="no">No</option>
                    <option value="yes">Yes</option>
                </select></label>
                <label>Persons: <input type="number" id="west-ground-persons" value="0" onchange="updateFlatData('west', 0)"></label>
                <span id="west-ground-utility">Utility: 0 Taka</span>
                <span id="west-ground-due">Due: 20500 Taka</span>
            </div>
            <div class="floor" id="west-1st">
                <span>1st Floor</span> - 16000 Taka
                <label>Rent Received: <select id="west-1st-received" onchange="updateFlatData('west', 1)">
                    <option value="no">No</option>
                    <option value="yes">Yes</option>
                </select></label>
                <label>Persons: <input type="number" id="west-1st-persons" value="2" onchange="updateFlatData('west', 1)"></label>
                <span id="west-1st-utility">Utility: 400 Taka</span>
                <span id="west-1st-due">Due: 16000 Taka</span>
            </div>
            <div class="floor" id="west-2nd">
                <span>2nd Floor</span> - 15000 Taka
                <label>Rent Received: <select id="west-2nd-received" onchange="updateFlatData('west', 2)">
                    <option value="no">No</option>
                    <option value="yes">Yes</option>
                </select></label>
                <label>Persons: <input type="number" id="west-2nd-persons" value="8" onchange="updateFlatData('west', 2)"></label>
                <span id="west-2nd-utility">Utility: 1600 Taka</span>
                <span id="west-2nd-due">Due: 15000 Taka</span>
            </div>
            <div class="floor" id="west-3rd">
                <span>3rd Floor</span> - 14500 Taka
                <label>Rent Received: <select id="west-3rd-received" onchange="updateFlatData('west', 3)">
                    <option value="no">No</option>
                    <option value="yes">Yes</option>
                </select></label>
                <label>Persons: <input type="number" id="west-3rd-persons" value="7" onchange="updateFlatData('west', 3)"></label>
                <span id="west-3rd-utility">Utility: 1400 Taka</span>
                <span id="west-3rd-due">Due: 14500 Taka</span>
            </div>
            <div class="floor" id="west-4th">
                <span>4th Floor</span> - 14000 Taka
                <label>Rent Received: <select id="west-4th-received" onchange="updateFlatData('west', 4)">
                    <option value="no">No</option>
                    <option value="yes">Yes</option>
                </select></label>
                <label>Persons: <input type="number" id="west-4th-persons" value="2" onchange="updateFlatData('west', 4)"></label>
                <span id="west-4th-utility">Utility: 400 Taka</span>
                <span id="west-4th-due">Due: 14000 Taka</span>
            </div>
            <div class="floor" id="west-5th">
                <span>5th Floor</span> - 13700 Taka
                <label>Rent Received: <select id="west-5th-received" onchange="updateFlatData('west', 5)">
                    <option value="no">No</option>
                    <option value="yes">Yes</option>
                </select></label>
                <label>Persons: <input type="number" id="west-5th-persons" value="4" onchange="updateFlatData('west', 5)"></label>
                <span id="west-5th-utility">Utility: 800 Taka</span>
                <span id="west-5th-due">Due: 13700 Taka</span>
            </div>
            <div class="floor" id="west-6th">
                <span>6th Floor</span> - 6000 Taka
                <label>Rent Received: <select id="west-6th-received" onchange="updateFlatData('west', 6)">
                    <option value="no">No</option>
                    <option value="yes">Yes</option>
                </select></label>
                <label>Persons: <input type="number" id="west-6th-persons" value="0" onchange="updateFlatData('west', 6)"></label>
                <span id="west-6th-utility">Utility: 0 Taka</span>
                <span id="west-6th-due">Due: 6000 Taka</span>
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
                    <th>Utility</th>
                    <th>Received</th>
                    <th>Due</th>
                </tr>
            </thead>
            <tbody id="summary-tbody">
                <!-- Summary rows will be populated here -->
            </tbody>
        </table>

        <div class="input-field">
            <label for="salary-deduction">Salary Deduction (10000 Taka): </label>
            <input type="number" id="salary-deduction" value="10000">
        </div>

        <div class="input-field">
            <label for="water-bill">Water Bill: </label>
            <input type="number" id="water-bill" value="200">
        </div>

        <div class="input-field">
            <label for="electricity-bill">Electricity Bill: </label>
            <input type="number" id="electricity-bill" value="0">
        </div>

        <div class="record-section">
            <button class="button" onclick="calculateExpenses()">Calculate After Expenses</button>
            <button class="button" onclick="exportToPDF()">Export to PDF</button>
        </div>

        <h4>Total Rent Received: <span id="total-rent-received">0</span></h4>
        <h4>Total Utility & Service Charge: <span id="total-utility">0</span></h4>
        <h4>Total Due: <span id="total-due">0</span></h4>
        <h4>Total Expenses: <span id="total-expenses">0</span></h4>
        <h4>Total After Expenses: <span id="final-total">0</span></h4>
        
        <h4>Inheritance Distribution</h4>
        <p>Wife gets: <span id="wife-share">0</span></p>
        <p>Son gets: <span id="son-share">0</span></p>
        <p>Daughter gets: <span id="daughter-share">0</span></p>
    </div>
</div>

<script>
    const flatData = {
        east: [
            { rent: 19000, persons: 0, received: 'no', utility: 0, due: 19000 },
            { rent: 15500, persons: 5, received: 'no', utility: 1000, due: 15500 },
            { rent: 15500, persons: 6, received: 'no', utility: 1200, due: 15500 },
            { rent: 14500, persons: 7, received: 'no', utility: 1400, due: 14500 },
            { rent: 14400, persons: 6, received: 'no', utility: 1200, due: 14400 },
            { rent: 14200, persons: 3, received: 'no', utility: 600, due: 14200 },
            { rent: 0, persons: 0, received: 'no', utility: 0, due: 0 }
        ],
        west: [
            { rent: 20500, persons: 0, received: 'no', utility: 0, due: 20500 },
            { rent: 16000, persons: 2, received: 'no', utility: 400, due: 16000 },
            { rent: 15000, persons: 8, received: 'no', utility: 1600, due: 15000 },
            { rent: 14500, persons: 7, received: 'no', utility: 1400, due: 14500 },
            { rent: 14000, persons: 2, received: 'no', utility: 400, due: 14000 },
            { rent: 13700, persons: 4, received: 'no', utility: 800, due: 13700 },
            { rent: 6000, persons: 0, received: 'no', utility: 0, due: 6000 }
        ]
    };

    function updateFlatData(side, floorIndex) {
        const flat = flatData[side][floorIndex];
        flat.received = document.getElementById(`${side}-${floorIndex}-received`).value;
        flat.persons = parseInt(document.getElementById(`${side}-${floorIndex}-persons`).value || 0;
        flat.utility = flat.persons * 200;
        flat.due = flat.received === 'yes' ? 0 : flat.rent;

        document.getElementById(`${side}-${floorIndex}-utility`).innerText = `Utility: ${flat.utility} Taka`;
        document.getElementById(`${side}-${floorIndex}-due`).innerText = `Due: ${flat.due} Taka`;

        calculateSummary();
    }

    function calculateSummary() {
        let totalRentReceived = 0;
        let totalUtility = 0;
        let totalDue = 0;
        let summaryHtml = '';

        for (let side in flatData) {
            flatData[side].forEach((flat, index) => {
                totalRentReceived += flat.received === 'yes' ? flat.rent : 0;
                totalUtility += flat.utility;
                totalDue += flat.due;

                const flatName = `${side === 'east' ? 'East' : 'West'} ${index === 0 ? 'Ground Floor' : `${index}th Floor`}`;
                summaryHtml += `
                    <tr>
                        <td>${flatName}</td>
                        <td>${flat.rent}</td>
                        <td>${flat.utility}</td>
                        <td>${flat.received === 'yes' ? flat.rent : 0}</td>
                        <td>${flat.due}</td>
                    </tr>
                `;
            });
        }

        document.getElementById('summary-tbody').innerHTML = summaryHtml;
        document.getElementById('total-rent-received').innerText = totalRentReceived;
        document.getElementById('total-utility').innerText = totalUtility;
        document.getElementById('total-due').innerText = totalDue;
    }

    function calculateExpenses() {
        const salaryDeduction = parseInt(document.getElementById('salary-deduction').value || 0);
        const waterBill = parseInt(document.getElementById('water-bill').value || 0);
        const electricityBill = parseInt(document.getElementById('electricity-bill').value || 0);

        const totalExpenses = salaryDeduction + waterBill + electricityBill;
        const totalRentReceived = parseInt(document.getElementById('total-rent-received').innerText || 0);
        const totalAfterExpenses = totalRentReceived - totalExpenses;

        const wifeShare = totalAfterExpenses * 0.125;
        const sonShare = totalAfterExpenses * 0.5833;
        const daughterShare = totalAfterExpenses * 0.2917;

        document.getElementById('total-expenses').innerText = totalExpenses;
        document.getElementById('final-total').innerText = totalAfterExpenses;
        document.getElementById('wife-share').innerText = wifeShare.toFixed(2);
        document.getElementById('son-share').innerText = sonShare.toFixed(2);
        document.getElementById('daughter-share').innerText = daughterShare.toFixed(2);
    }

    function exportToPDF() {
        const { jsPDF } = window.jspdf;
        const doc = new jsPDF();

        doc.text("Mirpur House Rent Summary", 10, 10);
        const summaryTable = document.getElementById('summary-tbody');
        let summaryText = "Flat | Rent | Utility | Received | Due\n";

        for (let row of summaryTable.rows) {
            summaryText += `${row.cells[0].innerText} | ${row.cells[1].innerText} | ${row.cells[2].innerText} | ${row.cells[3].innerText} | ${row.cells[4].innerText}\n`;
        }

        doc.text(summaryText, 10, 20);
        doc.save('Mirpur_House_Rent_Summary.pdf');
    }

    // Initialize default values
    function initializeDefaults() {
        for (let side in flatData) {
            flatData[side].forEach((flat, index) => {
                document.getElementById(`${side}-${index}-persons`).value = flat.persons;
                document.getElementById(`${side}-${index}-utility`).innerText = `Utility: ${flat.utility} Taka`;
                document.getElementById(`${side}-${index}-due`).innerText = `Due: ${flat.due} Taka`;
            });
        }
        calculateSummary();
    }

    // Call initializeDefaults on page load
    window.onload = initializeDefaults;
</script>

</body>
</html>
