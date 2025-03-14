Rent Calculator
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
                <input type="checkbox" class="rent-received" value="19000">
            </div>
            <div class="floor">
                <label>1st Floor: 15500 Taka</label>
                <input type="checkbox" class="rent-received" value="15500">
                <input type="number" value="5" class="persons" onchange="calculateUtility(this)">
                <span>Utility: <span class="utility">1000</span> Taka</span>
            </div>
            <div class="floor">
                <label>2nd Floor: 15500 Taka</label>
                <input type="checkbox" class="rent-received" value="15500">
                <input type="number" value="6" class="persons" onchange="calculateUtility(this)">
                <span>Utility: <span class="utility">1200</span> Taka</span>
            </div>
            <div class="floor">
                <label>3rd Floor: 14500 Taka</label>
                <input type="checkbox" class="rent-received" value="14500">
                <input type="number" value="7" class="persons" onchange="calculateUtility(this)">
                <span>Utility: <span class="utility">1400</span> Taka</span>
            </div>
            <div class="floor">
                <label>4th Floor: 14400 Taka</label>
                <input type="checkbox" class="rent-received" value="14400">
                <input type="number" value="6" class="persons" onchange="calculateUtility(this)">
                <span>Utility: <span class="utility">1200</span> Taka</span>
            </div>
            <div class="floor">
                <label>5th Floor: 14200 Taka</label>
                <input type="checkbox" class="rent-received" value="14200">
                <input type="number" value="3" class="persons" onchange="calculateUtility(this)">
                <span>Utility: <span class="utility">600</span> Taka</span>
            </div>
        </div>
        <div class="side" id="west-side">
            <h2>West Side</h2>
            <div class="floor">
                <label>Ground Floor: 20500 Taka</label>
                <input type="checkbox" class="rent-received" value="20500">
            </div>
            <div class="floor">
                <label>1st Floor: 16000 Taka</label>
                <input type="checkbox" class="rent-received" value="16000">
                <input type="number" value="2" class="persons" onchange="calculateUtility(this)">
                <span>Utility: <span class="utility">400</span> Taka</span>
            </div>
            <div class="floor">
                <label>2nd Floor: 15000 Taka</label>
                <input type="checkbox" class="rent-received" value="15000">
                <input type="number" value="8" class="persons" onchange="calculateUtility(this)">
                <span>Utility: <span class="utility">1600</span> Taka</span>
            </div>
            <div class="floor">
                <label>3rd Floor: 14500 Taka</label>
                <input type="checkbox" class="rent-received" value="14500">
                <input type="number" value="7" class="persons" onchange="calculateUtility(this)">
                <span>Utility: <span class="utility">1400</span> Taka</span>
            </div>
            <div class="floor">
                <label>4th Floor: 14000 Taka</label>
                <input type="checkbox" class="rent-received" value="14000">
                <input type="number" value="2" class="persons" onchange="calculateUtility(this)">
                <span>Utility: <span class="utility">400</span> Taka</span>
            </div>
            <div class="floor">
                <label>5th Floor: 13700 Taka</label>
                <input type="checkbox" class="rent-received" value="13700">
                <input type="number" value="4" class="persons" onchange="calculateUtility(this)">
                <span>Utility: <span class="utility">800</span> Taka</span>
            </div>
            <div class="floor">
                <label>6th Floor: 6000 Taka</label>
                <input type="checkbox" class="rent-received" value="6000">
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
        <button onclick="calculateTotal()">Calculate</button>
    </div>
    <script>
        function calculateUtility(element) {
            const persons = element.value;
            const utility = 200 * persons;
            element.nextElementSibling.children[0].innerText = utility;
        }

        function calculateTotal() {
            let totalRent = 0;
            let totalUtility = 0;
            const rentReceived = document.querySelectorAll('.rent-received:checked');
            rentReceived.forEach(rent => {
                totalRent += parseInt(rent.value);
            });
            const utilities = document.querySelectorAll('.utility');
            utilities.forEach(utility => {
                totalUtility += parseInt(utility.innerText);
            });
            const totalExpenses = 10000 + parseInt(document.getElementById('water-bill').value) + parseInt(document.getElementById('electricity-bill').value);
            const totalAfterExpenses = totalRent + totalUtility - totalExpenses;
            const wifeShare = totalAfterExpenses * 0.125;
            const sonShare = totalAfterExpenses * 0.5833;
            const daughterShare = totalAfterExpenses * 0.2917;

            document.getElementById('total-rent').innerText = totalRent;
            document.getElementById('total-utility').innerText = totalUtility;
            document.getElementById('total-expenses').innerText = totalExpenses;
            document.getElementById('total-after-expenses').innerText = totalAfterExpenses;
            document.getElementById('wife-share').innerText = wifeShare;
            document.getElementById('son-share').innerText = sonShare;
            document.getElementById('daughter-share').innerText = daughterShare;
        }
    </script>
</body>
</html>
