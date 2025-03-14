function updateFlatData(side, floorIndex) {
    const flat = flatData[side][floorIndex];
    flat.received = document.getElementById(`${side}-${floorIndex}-received`).value;
    flat.persons = parseInt(document.getElementById(`${side}-${floorIndex}-persons`).value || 0);
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

            const flatName = `${side === 'east' ? 'East' : 'West'} ${index === 0 ? 'Ground Floor' : `${index + 1}th Floor`}`;
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
