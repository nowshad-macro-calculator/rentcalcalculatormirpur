Mirpur rent calculator
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Mirpur House Rent Calculator</title>
    <style>
        body {
            font-family: Arial, sans-serif;
            margin: 20px;
        }
        .container {
            display: flex;
            justify-content: space-between;
        }
        .side {
            width: 45%;
        }
        .floor {
            margin: 10px 0;
        }
        .summary {
            margin-top: 20px;
            border-top: 1px solid #000;
            padding-top: 10px;
        }
    </style>
</head>
<body>

<h1>Mirpur House Rent Calculator</h1>

<div class="container">
    <div class="side" id="east-side">
        <h2>East Side</h2>
        <div class="floor">
            <label>Ground Floor: 19000 Taka</label>
            <select>
                <option value="no">Rent Received: No</option>
                <option value="yes">Rent Received: Yes</option>
            </select>
            <p>Total Payable: 19000 Taka</p>
        </div>
        <div class="floor">
            <label>1st Floor: 15500 Taka</label>
            <input type="number" value="5" min="0"> Persons
            <select>
                <option value="no">Rent Received: No</option>
                <option value="yes">Rent Received: Yes</option>
            </select>
            <p>Total Payable: 15500 + 1000 = 16500 Taka</p>
        </div>
        <div class="floor">
            <label>2nd Floor: 15500 Taka</label>
            <input type="number" value="6" min="0"> Persons
            <select>
                <option value="no">Rent Received: No</option>
                <option value="yes">Rent Received: Yes</option>
            </select>
            <p>Total Payable: 15500 + 1200 = 16700 Taka</p>
        </div>
        <div class="floor">
            <label>3rd Floor: 14500 Taka</label>
            <input type="number" value="7" min="0"> Persons
            <select>
                <option value="no">Rent Received: No</option>
                <option value="yes">Rent Received: Yes</option>
            </select>
            <p>Total Payable: 14500 + 1400 = 15900 Taka</p>
        </div>
        <div class="floor">
            <label>4th Floor: 14400 Taka</label>
            <input type="number" value="6" min="0"> Persons
            <select>
                <option value="no">Rent Received: No</option>
                <option value="yes">Rent Received: Yes</option>
            </select>
            <p>Total Payable: 14400 + 1200 = 15600 Taka</p>
        </div>
        <div class="floor">
            <label>5th Floor: 14200 Taka</label>
            <input type="number" value="3" min="0"> Persons
            <select>
                <option value="no">Rent Received: No</option>
                <option value="yes">Rent Received: Yes</option>
            </select>
            <p>Total Payable: 14200 + 600 = 14800 Taka</p>
        </div>
    </div>

    <div class="side" id="west-side">
        <h2>West Side</h2>
        <div class="floor">
            <label>Ground Floor: 20500 Taka</label>
            <select>
                <option value="no">Rent Received: No</option>
                <option value="yes">Rent Received: Yes</option>
            </select>
            <p>Total Payable: 20500 Taka</p>
        </div>
        <div class="floor">
            <label>1st Floor: 16000 Taka</label>
            <input type="number" value="2" min="0"> Persons
            <select>
                <option value="no">Rent Received: No</option>
                <option value="yes">Rent Received: Yes</option>
            </select>
            <p>Total Payable: 16000 + 400 = 16400 Taka</p>
        </div>
        <div class="floor">
            <label>2nd Floor: 15000 Taka</label>
            <input type="number" value="8" min="0"> Persons
            <select>
                <option value="no">Rent Received: No</option>
                <option value="yes">Rent Received: Yes</option>
            </select>
            <p>Total Payable: 15000 + 1600 = 16600 Taka</p>
        </div>
        <div class="floor">
            <label>3rd Floor: 14500 Taka</label>
            <input type="number" value="7" min="0"> Persons
            <select>
                <option value="no">Rent Received: No</option>
                <option value="yes">Rent Received: Yes</option>
            </select>
            <p>Total Payable: 14500 + 1400 = 15900 Taka</p>
        </div>
        <div class="floor">
            <label>4th Floor: 14000 Taka</label>
            <input type="number" value="2" min="0"> Persons
            <select>
                <option value="no">Rent Received: No</option>
                <option value="yes">Rent Received: Yes</option>
            </select>
            <p>Total Payable: 14000 + 400 = 14400 Taka</p>
        </div>
        <div class="floor">
            <label>5th Floor: 13700 Taka</label>
            <input type="number" value="4" min="0"> Persons
            <select>
                <option value="no">Rent Received: No</option>
                <option value="yes">Rent Received: Yes</option>
            </select>
            <p>Total Payable: 13700 + 800 = 14500 Taka</p>
        </div>
        <div class="floor">
            <label>6th Floor: 6000 Taka</label>
            <select>
                <option value="no">Rent Received: No</option>
                <option value="yes">Rent Received: Yes</option>
            </select>
            <p>Total Payable: 6000 Taka</p>
        </div>
    </div>
</div>

<div class="summary">
    <h2>Summary</h2>
    <p>Total Rent Received: <span id="total-rent">0</span> Taka</p>
    <p>Total Utility & Service Charge: <span id="total-utility">0</span> Taka</p>
    <p>Total Expenses: <span id="total-expenses">0</span> Taka</p>
    <p>Total After Expenses: <span id="total-after-expenses">0</span> Taka</p>
    <p>Inheritance Distribution:</p>
    <ul>
        <li>Wife: <span id="wife-share">0</span> Taka</li>
        <li>Son: <span id="son-share">0</span> Taka</li>
        <li>Daughter: <span id="daughter-share">0</span> Taka</li>
    </ul>
    <button onclick="generateReport()">Generate Report</button>
</div>

<script>
    function generateReport() {
        // Logic to generate PDF report
    }
</script>

</body>
</html>
