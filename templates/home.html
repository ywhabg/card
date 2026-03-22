<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Credit Card SMS Tracker</title>
    <script src="https://cdn.jsdelivr.net/npm/chart.js"></script>
    <style>
        body {
            font-family: Arial, sans-serif;
            max-width: 1200px;
            margin: 0 auto;
            padding: 24px;
            background: #f7f7f9;
            color: #222;
        }
        .card {
            background: white;
            border-radius: 12px;
            padding: 20px;
            margin-bottom: 20px;
            box-shadow: 0 2px 10px rgba(0,0,0,0.06);
        }
        h1, h2 { margin-top: 0; }
        textarea {
            width: 100%;
            min-height: 140px;
            padding: 12px;
            border: 1px solid #ccc;
            border-radius: 8px;
            font-size: 14px;
            box-sizing: border-box;
        }
        button, select {
            padding: 10px 16px;
            margin-right: 10px;
            margin-top: 12px;
            border-radius: 8px;
            font-size: 14px;
        }
        button {
            border: none;
            cursor: pointer;
            background: #2563eb;
            color: white;
        }
        button.secondary { background: #475569; }
        button.danger { background: #dc2626; }
        button.small {
            padding: 6px 10px;
            font-size: 12px;
            margin-top: 0;
            margin-right: 0;
        }
        select {
            border: 1px solid #ccc;
            background: white;
            color: #222;
        }
        pre {
            background: #111827;
            color: #f9fafb;
            padding: 14px;
            border-radius: 8px;
            overflow-x: auto;
            white-space: pre-wrap;
            word-wrap: break-word;
        }
        .grid {
            display: grid;
            grid-template-columns: repeat(auto-fit, minmax(230px, 1fr));
            gap: 16px;
        }
        .stat {
            background: #eff6ff;
            border-radius: 10px;
            padding: 14px;
        }
        table {
            width: 100%;
            border-collapse: collapse;
            margin-top: 12px;
            background: white;
        }
        th, td {
            border-bottom: 1px solid #e5e7eb;
            text-align: left;
            padding: 10px 8px;
            font-size: 14px;
            vertical-align: top;
        }
        th { background: #f3f4f6; }
        .muted { color: #6b7280; font-size: 13px; }
        .success { color: #166534; }
        .error { color: #b91c1c; }
        .toolbar {
            display: flex;
            flex-wrap: wrap;
            align-items: center;
            gap: 10px;
            margin-bottom: 10px;
        }
        canvas {
            margin-top: 12px;
            max-height: 380px;
        }
    </style>
</head>
<body>
    <div class="card">
        <h1>Credit Card SMS Tracker</h1>
        <div class="muted">Paste an SMS, parse it, save it, filter by card, and delete entries.</div>
    </div>

    <div class="card">
        <h2>Enter SMS</h2>
        <textarea id="smsInput" placeholder="Example: UOB: Spent USD 12.50 at AMAZON on 21/03/26 card ending with 1234"></textarea>
        <div>
            <button onclick="parseSms()">Parse SMS</button>
            <button onclick="submitSms()">Submit Transaction</button>
            <button class="secondary" onclick="loadDashboard()">Refresh Dashboard</button>
            <button class="danger" onclick="resetAll()">Reset All</button>
        </div>
        <p id="status" class="muted"></p>
    </div>

    <div class="card">
        <h2>Parse / Submit Result</h2>
        <pre id="resultBox">No result yet.</pre>
    </div>

    <div class="card">
        <h2>Stats</h2>
        <div class="grid" id="statsGrid"></div>
    </div>

    <div class="card">
        <h2>Spending Trend</h2>
        <div class="muted">Daily spending in SGD for the selected card or all cards.</div>
        <canvas id="spendingChart" height="110"></canvas>
    </div>

    <div class="card">
        <h2>Monthly Totals</h2>
        <pre id="monthlyTotals">Loading...</pre>
    </div>

    <div class="card">
        <h2>Transactions</h2>

        <div class="toolbar">
            <label for="cardFilter"><strong>Show card:</strong></label>
            <select id="cardFilter" onchange="loadDashboard()">
                <option value="">All Cards</option>
            </select>
            <button class="secondary" onclick="loadDashboard()">Apply Filter</button>
        </div>

        <div id="transactionsWrap">Loading...</div>
    </div>

    <script>
        let spendingChartInstance = null;

        async function apiGet(url) {
            const res = await fetch(url);
            return await res.json();
        }

        async function apiPost(url, payload) {
            const res = await fetch(url, {
                method: "POST",
                headers: { "Content-Type": "application/json" },
                body: JSON.stringify(payload)
            });
            const data = await res.json();
            return { ok: res.ok, data };
        }

        async function apiDelete(url) {
            const res = await fetch(url, { method: "DELETE" });
            const data = await res.json();
            return { ok: res.ok, data };
        }

        function setStatus(message, isError = false) {
            const el = document.getElementById("status");
            el.textContent = message;
            el.className = isError ? "error" : "success";
        }

        async function parseSms() {
            const sms = document.getElementById("smsInput").value.trim();
            if (!sms) {
                setStatus("Please enter SMS content first.", true);
                return;
            }

            setStatus("Parsing...");
            const result = await apiPost("/api/parse", { sms_content: sms });
            document.getElementById("resultBox").textContent = JSON.stringify(result.data, null, 2);
            setStatus(result.ok ? "Parse completed." : "Parse failed.", !result.ok);
        }

        async function submitSms() {
            const sms = document.getElementById("smsInput").value.trim();
            if (!sms) {
                setStatus("Please enter SMS content first.", true);
                return;
            }

            setStatus("Submitting transaction...");
            const result = await apiPost("/api/submit", { sms_content: sms });
            document.getElementById("resultBox").textContent = JSON.stringify(result.data, null, 2);

            if (result.ok) {
                setStatus("Transaction saved successfully.");
                document.getElementById("smsInput").value = "";
                await loadDashboard();
            } else {
                setStatus("Submit failed.", true);
            }
        }

        async function resetAll() {
            const confirmed = confirm("This will clear all transactions. Continue?");
            if (!confirmed) return;

            setStatus("Resetting...");
            const result = await apiPost("/api/reset", { confirm: "yes" });
            document.getElementById("resultBox").textContent = JSON.stringify(result.data, null, 2);

            if (result.ok) {
                setStatus("All transactions cleared.");
                await loadDashboard();
            } else {
                setStatus("Reset failed.", true);
            }
        }

        async function deleteTransaction(rowId) {
            const confirmed = confirm(`Delete transaction ${rowId}?`);
            if (!confirmed) return;

            setStatus("Deleting transaction...");
            const result = await apiDelete(`/api/transactions/${rowId}`);
            document.getElementById("resultBox").textContent = JSON.stringify(result.data, null, 2);

            if (result.ok) {
                setStatus("Transaction deleted successfully.");
                await loadDashboard();
            } else {
                setStatus("Delete failed.", true);
            }
        }

        async function loadStats() {
            const data = await apiGet("/api/stats");
            const stats = data.stats || {};
            const grid = document.getElementById("statsGrid");

            const items = [
                ["Total Transactions", stats.total_transactions ?? 0],
                ["Total Amount SGD", stats.total_amount_sgd ?? 0],
                ["Unique Cards", stats.unique_cards ?? 0],
                ["Current Month Transactions", stats.current_month_transactions ?? 0],
                ["Current Month Amount SGD", stats.current_month_amount_sgd ?? 0]
            ];

            grid.innerHTML = items.map(([label, value]) => `
                <div class="stat">
                    <div class="muted">${label}</div>
                    <div style="font-size:24px;font-weight:bold;margin-top:6px;">${value}</div>
                </div>
            `).join("");
        }

        async function loadMonthlyTotals() {
            const data = await apiGet("/api/totals/monthly/by-card");
            document.getElementById("monthlyTotals").textContent = JSON.stringify(data, null, 2);
        }

        async function loadCardsFilter() {
            const data = await apiGet("/api/cards");
            const select = document.getElementById("cardFilter");
            const currentValue = select.value;

            select.innerHTML = `<option value="">All Cards</option>`;

            if (data.cards && data.cards.length > 0) {
                data.cards.forEach(card => {
                    const option = document.createElement("option");
                    option.value = card.card_last_4;
                    option.textContent = `${card.card_label} (${card.transaction_count})`;
                    select.appendChild(option);
                });
            }

            if ([...select.options].some(opt => opt.value === currentValue)) {
                select.value = currentValue;
            }
        }

        function normalizeDateForDisplay(dateStr) {
            if (!dateStr) return "";
            const parts = String(dateStr).split("/");
            if (parts.length !== 3) return String(dateStr);
            const [dd, mm, yy] = parts;
            const fullYear = yy.length === 2 ? `20${yy}` : yy;
            return `${fullYear}-${mm}-${dd}`;
        }

        function buildChartFromTransactions(transactions) {
            const dailyTotals = {};

            transactions.forEach(tx => {
                const dateKey = normalizeDateForDisplay(tx.Date);
                const amountSGD = parseFloat(tx.Amount_SGD || 0);

                if (!dateKey || isNaN(amountSGD)) return;

                if (!dailyTotals[dateKey]) {
                    dailyTotals[dateKey] = 0;
                }
                dailyTotals[dateKey] += amountSGD;
            });

            const labels = Object.keys(dailyTotals).sort();
            const values = labels.map(label => Number(dailyTotals[label].toFixed(2)));

            const ctx = document.getElementById("spendingChart").getContext("2d");

            if (spendingChartInstance) {
                spendingChartInstance.destroy();
            }

            spendingChartInstance = new Chart(ctx, {
                type: "bar",
                data: {
                    labels: labels,
                    datasets: [{
                        label: "Daily Spending (SGD)",
                        data: values,
                        borderWidth: 1
                    }]
                },
                options: {
                    responsive: true,
                    plugins: {
                        legend: {
                            display: true
                        }
                    },
                    scales: {
                        y: {
                            beginAtZero: true,
                            ticks: {
                                callback: function(value) {
                                    return value.toFixed ? value.toFixed(2) : value;
                                }
                            }
                        }
                    }
                }
            });
        }

        async function loadTransactions() {
            const selectedCard = document.getElementById("cardFilter").value;
            const url = selectedCard
                ? `/api/transactions/${selectedCard}`
                : "/api/transactions";

            const data = await apiGet(url);
            const wrap = document.getElementById("transactionsWrap");

            if (!data.transactions || data.transactions.length === 0) {
                wrap.innerHTML = "<p class='muted'>No transactions found.</p>";

                if (spendingChartInstance) {
                    spendingChartInstance.destroy();
                    spendingChartInstance = null;
                }
                return;
            }

            let totalAmountSGD = 0;

            const rows = data.transactions.slice().reverse().map(tx => {
                const amountSGD = parseFloat(tx.Amount_SGD || 0);
                totalAmountSGD += isNaN(amountSGD) ? 0 : amountSGD;

                return `
                    <tr>
                        <td>${tx.Row_ID ?? ""}</td>
                        <td>${tx.Date ?? ""}</td>
                        <td>${tx.Card_Label ?? ""}</td>
                        <td>${tx.Currency ?? ""}</td>
                        <td>${tx.Amount ?? ""}</td>
                        <td>${tx.Amount_SGD ?? ""}</td>
                        <td>${tx.Description ?? ""}</td>
                        <td>
                            <button class="danger small" onclick="deleteTransaction('${tx.Row_ID}')">Delete</button>
                        </td>
                    </tr>
                `;
            }).join("");

            const footer = `
                <tfoot>
                    <tr style="font-weight:bold;background:#f9fafb;">
                        <td colspan="5">Grand Total</td>
                        <td>${totalAmountSGD.toFixed(2)}</td>
                        <td colspan="2"></td>
                    </tr>
                </tfoot>
            `;

            wrap.innerHTML = `
                <table>
                    <thead>
                        <tr>
                            <th>Row ID</th>
                            <th>Date</th>
                            <th>Card</th>
                            <th>Currency</th>
                            <th>Amount</th>
                            <th>Amount SGD</th>
                            <th>Description</th>
                            <th>Action</th>
                        </tr>
                    </thead>
                    <tbody>${rows}</tbody>
                    ${footer}
                </table>
            `;

            buildChartFromTransactions(data.transactions);
        }

        async function loadDashboard() {
            await loadStats();
            await loadMonthlyTotals();
            await loadCardsFilter();
            await loadTransactions();
        }

        loadDashboard();
    </script>
</body>
</html>
