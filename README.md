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
        .input-field {
            margin-top: 10px;
        }
        .input-field label {
            margin-right: 10px;
        }
        .language-toggle {
            margin: 20px 0;
            text-align: right;
        }
    </style>
    <!-- Include jsPDF library -->
    <script src="https://cdnjs.cloudflare.com/ajax/libs/jspdf/2.5.1/jspdf.umd.min.js"></script>
</head>
<body>

<div class="container">
    <!-- Language Toggle Button -->
    <div class="language-toggle">
        <button class="button" onclick="toggleLanguage()">Switch to Bangla</button>
    </div>

    <h1 id="page-title">Mirpur House Rent Calculator</h1>

    <!-- House Layout (East and West Sides) -->
    <div class="house-layout">
        <!-- East Side -->
        <div class="side">
            <h3 id="east-side-title">East Side</h3>
            <!-- Flat entries -->
            <div class="floor" id="east-ground">
                <span id="east-ground-name">East Side Ground Floor</span> - 19000 Taka
                <input type="checkbox" id="east-ground-checkbox" onchange="updateFlatData('east', 0)">
                <input type="number" id="east-ground-persons" value="0" placeholder="No. of persons" onchange="updateFlatData('east', 0)">
                <input type="number" id="east-ground-utility-service" value="0" placeholder="Utility & Service Charge" onchange="updateFlatData('east', 0)">
                <span id="east-ground-total">Grand Total: 19000 Taka</span>
                <span id="east-ground-due">Due: 19000 Taka</span>
            </div>
            <!-- Repeat for other East side floors (1st, 2nd, etc.) -->
        </div>

        <!-- West Side -->
        <div class="side">
            <h3 id="west-side-title">West Side</h3>
            <!-- Flat entries -->
            <div class="floor" id="west-ground">
                <span id="west-ground-name">West Side Ground Floor</span> - 20500 Taka
                <input type="checkbox" id="west-ground-checkbox" onchange="updateFlatData('west', 0)">
                <input type="number" id="west-ground-persons" value="0" placeholder="No. of persons" onchange="updateFlatData('west', 0)">
                <input type="number" id="west-ground-utility-service" value="0" placeholder="Utility & Service Charge" onchange="updateFlatData('west', 0)">
                <span id="west-ground-total">Grand Total: 20500 Taka</span>
                <span id="west-ground-due">Due: 20500 Taka</span>
            </div>
            <!-- Repeat for other West side floors (1st, 2nd, etc.) -->
        </div>
    </div>

    <!-- Summary Section -->
    <div class="summary">
        <h3 id="summary-title">Summary</h3>
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
            <label for="salary-deduction" id="salary-deduction-label">Salary Deduction (10000 Taka): </label>
            <input type="number" id="salary-deduction" value="10000" onchange="updateTotal()">
        </div>

        <div class="input-field">
            <label for="water-bill" id="water-bill-label">Water Bill: </label>
            <input type="number" id="water-bill" value="200" onchange="updateTotal()">
        </div>

        <div class="input-field">
            <label for="electricity-bill" id="electricity-bill-label">Electricity Bill: </label>
            <input type="number" id="electricity-bill" value="0" onchange="updateTotal()">
        </div>

        <div class="record-section">
            <button class="button" onclick="calculateExpenses()">Calculate After Expenses</button>
            <button class="button" onclick="exportToPDF()">Export to PDF</button>
        </div>

        <h4 id="total-rent-received-label">Total Rent Received: <span id="total-rent-received">0</span></h4>
        <h4 id="total-expenses-label">Total Expenses: <span id="total-expenses">0</span></h4>
        <h4 id="total-after-expenses-label">Total After Expenses: <span id="final-total">0</span></h4>
        
        <h4 id="inheritance-title">Inheritance Distribution</h4>
        <p id="wife-share-label">Wife gets: <span id="wife-share">0</span></p>
        <p id="son-share-label">Son gets: <span id="son-share">0</span></p>
        <p id="daughter-share-label">Daughter gets: <span id="daughter-share">0</span></p>

        <!-- Total Rent and Utility Summary -->
        <div>
            <h4 id="total-rent-label">Total Rent: <span id="total-rent">0</span></h4>
            <h4 id="total-utility-service-label">Total Utility & Service Charge: <span id="total-utility-service">0</span></h4>
            <h4 id="total-grand-total-label">Total Grand Total: <span id="total-grand-total">0</span></h4>
        </div>
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

    let language = 'en';  // Default language is English

    // Function to switch between English and Bangla
    function toggleLanguage() {
        if (language === 'en') {
            language = 'bn';
            document.getElementById('page-title').innerText = 'মিরপুর হাউস ভাড়া ক্যালকুলেটর';
            document.getElementById('east-side-title').innerText = 'পূর্ব দিক';
            document.getElementById('west-side-title').innerText = 'পশ্চিম দিক';
            document.getElementById('summary-title').innerText = 'সারাংশ';
            document.getElementById('salary-deduction-label').innerText = 'বেতন কর্তন (১০০০০ টাকা):';
            document.getElementById('water-bill-label').innerText = 'পানি বিল:';
            document.getElementById('electricity-bill-label').innerText = 'বিদ্যুৎ বিল:';
            document.getElementById('total-rent-received-label').innerText = 'মোট ভাড়া পাওয়া:';
            document.getElementById('total-expenses-label').innerText = 'মোট খরচ:';
            document.getElementById('total-after-expenses-label').innerText = 'খরচ পরবর্তী মোট:';
            document.getElementById('inheritance-title').innerText = 'ঐশ্বর্যের বিতরণ';
            document.getElementById('wife-share-label').innerText = 'মা পাবেন:';
            document.getElementById('son-share-label').innerText = 'ছেলে পাবেন:';
            document.getElementById('daughter-share-label').innerText = 'মেয়ে পাবেন:';
            document.getElementById('total-rent-label').innerText = 'মোট ভাড়া:';
            document.getElementById('total-utility-service-label').innerText = 'মোট ইউটিলিটি ও সেবার চার্জ:';
            document.getElementById('total-grand-total-label').innerText = 'মোট গ্র্যান্ড টোটাল:';
            document.querySelector('.language-toggle button').innerText = 'Switch to English';
        } else {
            language = 'en';
            document.getElementById('page-title').innerText = 'Mirpur House Rent Calculator';
            document.getElementById('east-side-title').innerText = 'East Side';
            document.getElementById('west-side-title').innerText = 'West Side';
            document.getElementById('summary-title').innerText = 'Summary';
            document.getElementById('salary-deduction-label').innerText = 'Salary Deduction (10000 Taka):';
            document.getElementById('water-bill-label').innerText = 'Water Bill:';
            document.getElementById('electricity-bill-label').innerText = 'Electricity Bill:';
            document.getElementById('total-rent-received-label').innerText = 'Total Rent Received:';
            document.getElementById('total-expenses-label').innerText = 'Total Expenses:';
            document.getElementById('total-after-expenses-label').innerText = 'Total After Expenses:';
            document.getElementById('inheritance-title').innerText = 'Inheritance Distribution';
            document.getElementById('wife-share-label').innerText = 'Wife gets:';
            document.getElementById('son-share-label').innerText = 'Son gets:';
            document.getElementById('daughter-share-label').innerText = 'Daughter gets:';
            document.getElementById('total-rent-label').innerText = 'Total Rent:';
            document.getElementById('total-utility-service-label').innerText = 'Total Utility & Service Charge:';
            document.getElementById('total-grand-total-label').innerText = 'Total Grand Total:';
            document.querySelector('.language-toggle button').innerText = 'Switch to Bangla';
        }
    }

    // Function to update flat data (rent received, utility, etc.)
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
    }

    // Function to calculate expenses and inheritance distribution
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
