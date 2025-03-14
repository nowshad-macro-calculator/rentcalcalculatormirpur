<!DOCTYPE html>
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
            border: 1px solid #ccc;
            padding: 10px;
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
            <span>Total Payable: 19000 Taka</span>
        </div>
        <div class="floor">
            <label>1st Floor: 15500 Taka</label>
            <input type="number" value="5" min="0"> persons
            <select>
                <option value="no">Rent Received: No</option>
                <option value="yes">Rent Received: Yes</option>
            </select>
            <span>Total Payable: 15500 + 1000 Taka</span>
        </div>
        <div class="floor">
            <label>2nd Floor: 15500 Taka</label>
            <input type="number" value="6" min="0"> persons
            <select>
                <option value="no">Rent Received: No</option>
                <option value="yes">Rent Received: Yes</option>
            </select>
            <span>Total Payable: 15500 + 1200 Taka</span>
        </div>
        <div class="floor">
            <label>3rd Floor: 14500 Taka</label>
            <input type="number" value="7" min="0"> persons
            <select>
                <option value="no">Rent Received: No</option>
                <option value="yes">Rent Received: Yes</option>
            </select>
            <span>Total Payable: 14500 + 1400 Taka</span>
        </div>
        <div class="floor">
            <label>4th Floor: 14400 Taka</label>
            <input type="number" value="6" min="0"> persons
            <select>
                <option value="no">Rent Received: No</option>
                <option value="yes">Rent Received: Yes</option>
            </select>
            <span>Total Payable: 14400 + 1200 Taka</span>
        </div>
        <div class="floor">
            <label>5th Floor: 14200 Taka</label>
            <input type="number" value="3" min="0"> persons
            <select>
                <option value="no">Rent Received: No</option>
                <option value="yes">Rent Received: Yes</option>
            </select>
            <span>Total Payable: 14200 + 600 Taka</span>
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
            <span>Total Payable: 20500 Taka</span>
        </div>
        <div class="floor">
            <label>1st Floor: 16000 Taka</label>
            <input type="number" value="2" min="0"> persons
            <select>
                <option value="no">Rent Received: No</option>
                <option value="yes">Rent Received: Yes</option>
            </select>
            <span>Total Payable: 16000 + 400 Taka</span>
        </div>
        <div class="floor">
            <label>2nd Floor: 15000 Taka</label>
            <input type="number" value="8" min="0"> persons
            <select>
                <option value="no">Rent Received: No</option>
                <option value="yes">Rent Received: Yes</option>
            </select>
            <span>Total Payable: 15000 + 1600 Taka</span>
        </div>
        <div class="floor">
            <label>3rd Floor: 14500 Taka</label>
            <input type="number" value="7" min="0"> persons
            <select>
                <option value="no">Rent Received: No</option>
                <option value="yes">Rent Received: Yes</option>
            </select>
            <span>Total Payable: 14500 + 1400 Taka</span>
        </div>
        <div class="floor">
            <label>4th Floor: 14000 Taka</label>
            <input type="number" value="2" min="0"> persons
            <select>
                <option value="no">Rent Received: No</option>
                <option value="yes">Rent Received: Yes</option>
            </select>
            <span>Total Payable: 14000 + 400 Taka</span>
        </div>
        <div class="floor">
            <label>5th Floor: 13700 Taka</label>
            <input type="number" value="4" min="0"> persons
            <select>
                <option value="no">Rent Received: No</option>
                <option value="yes">Rent Received: Yes</option>
            </select>
            <span>Total Payable: 13700 + 800 Taka</span>
        </div>
        <div class="floor">
            <label>6th Floor: 6000 Taka</label>
            <select>
                <option value="no">Rent Received: No</option>
                <option value="yes">Rent Received: Yes</option>
            </select>
            <span>Total Payable: 6000 Taka</span>
        </div>
    </div>
</div>

<div class="summary">
    <h3>Summary</h3>
    <label>Total Rent Received: <span id="total-rent">0</span> Taka</label><br>
    <label>Total Utility & Service Charge: <span id="total-utility">0</span> Taka</label><br>
    <label>Total Expenses: <span id="total-expenses">0</span> Taka</label><br>
    <label>Total After Expenses: <span id="total-after-expenses">0</span> Taka</label><br>
    <label>Inheritance Distribution:</label><br>
    <label>Wife: <span id="wife-share">0</span> Taka</label><br>
    <label>Son: <span id="son-share">0</span> Taka</label><br>
    <label>Daughter: <span id="daughter-share">0</span> Taka</label><br>
</div>

<div>
    <h3>Expenses</h3>
    <label>Staff Salary: <input type="number" value="10000" id="staff-salary"></label><br>
    <label>Water Bill: <input type="number" value="8000" id="water-bill"></label><br>
    <label>Common Electricity Bill: <input type="number" value="1000" id="electricity-bill"></label><br>
    <button id="calculate-button">Calculate Now</button>
    <button id="summary-button">Generate Summary</button>
</div>

<script>
    document.getElementById('calculate-button').addEventListener('click', function() {
        // Calculation logic goes here
    });

    document.getElementById('summary-button').addEventListener('click', function() {
        // Summary generation logic goes here
    });
</script>

</body>
</html>
