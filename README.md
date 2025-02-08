<!DOCTYPE html>
<html lang="es">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Panel de Balance</title>
    <link href="https://fonts.googleapis.com/css2?family=Roboto:wght@400;500&display=swap" rel="stylesheet">
    <style>
        body {
            font-family: 'Roboto', sans-serif;
            margin: 0;
            padding: 0;
            background-color: #f4f6f9;
            color: #333;
        }
        .container {
            max-width: 1200px;
            margin: 0 auto;
            padding: 20px;
        }
        header {
            background-color: #3498db;
            padding: 20px;
            color: white;
            text-align: center;
            border-radius: 8px;
        }
        .dashboard {
            background-color: #fff;
            padding: 30px;
            border-radius: 10px;
            box-shadow: 0 0 15px rgba(0, 0, 0, 0.1);
            margin-top: 20px;
        }
        .balance, .transaction-history, .support, .payment-info {
            margin-bottom: 30px;
        }
        .balance h2, .transaction-history h2, .support h2 {
            font-size: 24px;
            margin-bottom: 15px;
            color: #2c3e50;
        }
        .balance-info, .history-table, .support-btn, .payment-info {
            background-color: #ecf0f1;
            padding: 20px;
            border-radius: 8px;
        }
        .history-table table {
            width: 100%;
            border-collapse: collapse;
        }
        .history-table th, .history-table td {
            padding: 12px;
            text-align: left;
            border-bottom: 1px solid #ddd;
        }
        .btn {
            display: inline-block;
            background-color: #3498db;
            color: #fff;
            padding: 12px 20px;
            border-radius: 5px;
            text-decoration: none;
            font-size: 16px;
            text-align: center;
        }
        .btn:hover {
            background-color: #2980b9;
        }
        .popup {
            display: none;
            position: fixed;
            top: 0;
            left: 0;
            width: 100%;
            height: 100%;
            background-color: rgba(0, 0, 0, 0.5);
            justify-content: center;
            align-items: center;
        }
        .popup-content {
            background-color: white;
            padding: 40px;
            border-radius: 10px;
            text-align: center;
            width: 400px;
            box-shadow: 0 0 20px rgba(0, 0, 0, 0.2);
        }
        .popup input, .popup select {
            padding: 10px;
            margin: 10px;
            width: 80%;
            border-radius: 5px;
            border: 1px solid #ccc;
        }
        .popup button {
            padding: 12px 20px;
            background-color: #3498db;
            border: none;
            color: white;
            border-radius: 5px;
        }
        .popup button:hover {
            background-color: #2980b9;
        }
    </style>
</head>
<body>

<header>
    <h1>Bienvenido a tu Panel de Inversiones</h1>
</header>

<div class="container">
    <div class="dashboard">
        <div class="balance">
            <h2>Saldo Actual</h2>
            <div class="balance-info">
                <p>Saldo disponible: <strong id="balance">€5000</strong></p>
                <a href="#" class="btn">Ver Saldo</a>
            </div>
        </div>

        <div class="transaction-history">
            <h2>Historial de Transacciones</h2>
            <div class="history-table">
                <table>
                    <tr>
                        <th>Fecha</th>
                        <th>Descripción</th>
                        <th>Monto</th>
                    </tr>
                    <tr>
                        <td>08/02/2025</td>
                        <td>Depósito</td>
                        <td>€1000</td>
                    </tr>
                    <tr>
                        <td>07/02/2025</td>
                        <td>Retiro</td>
                        <td>€500</td>
                    </tr>
                    <tr>
                        <td>05/02/2025</td>
                        <td>Inversión Plan A</td>
                        <td>€2000</td>
                    </tr>
                </table>
            </div>
        </div>

        <div class="payment-info">
            <h2>Información de Pago</h2>
            <div class="payment-info">
                <label for="amount-paid">Monto Pagado:</label>
                <input type="number" id="amount-paid" placeholder="Monto pagado (€)" />
                <br><br>

                <button class="btn" onclick="updateBalance()">Actualizar Balance</button>
            </div>
        </div>

        <div class="support">
            <h2>Soporte</h2>
            <div class="support-btn">
                <a href="https://wa.me/2347040258315" class="btn">Contactar Soporte</a>
            </div>
        </div>
    </div>
</div>

<div class="popup" id="popup">
    <div class="popup-content">
        <h3>¿Cuánto pagaste y qué plan seleccionaste?</h3>
        <input type="number" placeholder="Monto pagado (€)" id="amount-paid-popup">
        <br>
        <label for="currency">Selecciona tu moneda:</label>
        <select id="currency">
            <option value="EUR">Euro (€)</option>
            <option value="MXN">Peso Mexicano (MXN)</option>
            <option value="ARS">Peso Argentino (ARS)</option>
            <option value="COP">Peso Colombiano (COP)</option>
            <option value="PEN">Nuevo Sol (PEN)</option>
        </select>
        <br><br>
        <label for="plan-select">Selecciona el Plan:</label>
        <select id="plan-select">
            <option value="Basic">Básico</option>
            <option value="Advanced">Avanzado</option>
            <option value="Elite">Élite</option>
        </select>
        <br><br>
        <button onclick="submitPayment()">Enviar</button>
    </div>
</div>

<script>
    // Show the pop-up on page load
    window.onload = function() {
        document.getElementById('popup').style.display = 'flex';
    };

    // Function to handle the payment form submission
    function submitPayment() {
        var amount = document.getElementById('amount-paid-popup').value;
        var plan = document.getElementById('plan-select').value;
        var currency = document.getElementById('currency').value;

        if (amount && plan && currency) {
            alert('Pago de ' + currency + ' ' + amount + ' para el plan: ' + plan + ' registrado correctamente.');
            document.getElementById('popup').style.display = 'none';
        } else {
            alert('Por favor, complete todos los campos.');
        }
    }

    // Function to update the balance based on the amount entered
    function updateBalance() {
        var amountPaid = document.getElementById('amount-paid').value;
        var currency = document.getElementById('currency').value;
        var currentBalance = 5000;  // Initial balance, can be dynamic based on user data
        var newBalance = parseFloat(currentBalance) + parseFloat(amountPaid);

        if (isNaN(newBalance)) {
            alert("Por favor, ingrese un monto válido.");
        } else {
            document.getElementById('balance').innerText = currency + " " + newBalance.toFixed(2);
            alert("¡Saldo actualizado exitosamente!");
        }
    }
</script>

</body>
</html><!DOCTYPE html>
<html lang="es">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Panel de Balance</title>
    <link href="https://fonts.googleapis.com/css2?family=Roboto:wght@400;500&display=swap" rel="stylesheet">
    <style>
        body {
            font-family: 'Roboto', sans-serif;
            margin: 0;
            padding: 0;
            background-color: #f4f6f9;
            color: #333;
        }
        .container {
            max-width: 1200px;
            margin: 0 auto;
            padding: 20px;
        }
        header {
            background-color: #3498db;
            padding: 20px;
            color: white;
            text-align: center;
            border-radius: 8px;
        }
        .dashboard {
            background-color: #fff;
            padding: 30px;
            border-radius: 10px;
            box-shadow: 0 0 15px rgba(0, 0, 0, 0.1);
            margin-top: 20px;
        }
        .balance, .transaction-history, .support, .payment-info {
            margin-bottom: 30px;
        }
        .balance h2, .transaction-history h2, .support h2 {
            font-size: 24px;
            margin-bottom: 15px;
            color: #2c3e50;
        }
        .balance-info, .history-table, .support-btn, .payment-info {
            background-color: #ecf0f1;
            padding: 20px;
            border-radius: 8px;
        }
        .history-table table {
            width: 100%;
            border-collapse: collapse;
        }
        .history-table th, .history-table td {
            padding: 12px;
            text-align: left;
            border-bottom: 1px solid #ddd;
        }
        .btn {
            display: inline-block;
            background-color: #3498db;
            color: #fff;
            padding: 12px 20px;
            border-radius: 5px;
            text-decoration: none;
            font-size: 16px;
            text-align: center;
        }
        .btn:hover {
            background-color: #2980b9;
        }
        .popup {
            display: none;
            position: fixed;
            top: 0;
            left: 0;
            width: 100%;
            height: 100%;
            background-color: rgba(0, 0, 0, 0.5);
            justify-content: center;
            align-items: center;
        }
        .popup-content {
            background-color: white;
            padding: 40px;
            border-radius: 10px;
            text-align: center;
            width: 400px;
            box-shadow: 0 0 20px rgba(0, 0, 0, 0.2);
        }
        .popup input, .popup select {
            padding: 10px;
            margin: 10px;
            width: 80%;
            border-radius: 5px;
            border: 1px solid #ccc;
        }
        .popup button {
            padding: 12px 20px;
            background-color: #3498db;
            border: none;
            color: white;
            border-radius: 5px;
        }
        .popup button:hover {
            background-color: #2980b9;
        }
    </style>
</head>
<body>

<header>
    <h1>Bienvenido a tu Panel de Inversiones</h1>
</header>

<div class="container">
    <div class="dashboard">
        <div class="balance">
            <h2>Saldo Actual</h2>
            <div class="balance-info">
                <p>Saldo disponible: <strong id="balance">€5000</strong></p>
                <a href="#" class="btn">Ver Saldo</a>
            </div>
        </div>

        <div class="transaction-history">
            <h2>Historial de Transacciones</h2>
            <div class="history-table">
                <table>
                    <tr>
                        <th>Fecha</th>
                        <th>Descripción</th>
                        <th>Monto</th>
                    </tr>
                    <tr>
                        <td>08/02/2025</td>
                        <td>Depósito</td>
                        <td>€1000</td>
                    </tr>
                    <tr>
                        <td>07/02/2025</td>
                        <td>Retiro</td>
                        <td>€500</td>
                    </tr>
                    <tr>
                        <td>05/02/2025</td>
                        <td>Inversión Plan A</td>
                        <td>€2000</td>
                    </tr>
                </table>
            </div>
        </div>

        <div class="payment-info">
            <h2>Información de Pago</h2>
            <div class="payment-info">
                <label for="amount-paid">Monto Pagado:</label>
                <input type="number" id="amount-paid" placeholder="Monto pagado (€)" />
                <br><br>

                <button class="btn" onclick="updateBalance()">Actualizar Balance</button>
            </div>
        </div>

        <div class="support">
            <h2>Soporte</h2>
            <div class="support-btn">
                <a href="https://wa.me/2347040258315" class="btn">Contactar Soporte</a>
            </div>
        </div>
    </div>
</div>

<div class="popup" id="popup">
    <div class="popup-content">
        <h3>¿Cuánto pagaste y qué plan seleccionaste?</h3>
        <input type="number" placeholder="Monto pagado (€)" id="amount-paid-popup">
        <br>
        <label for="currency">Selecciona tu moneda:</label>
        <select id="currency">
            <option value="EUR">Euro (€)</option>
            <option value="MXN">Peso Mexicano (MXN)</option>
            <option value="ARS">Peso Argentino (ARS)</option>
            <option value="COP">Peso Colombiano (COP)</option>
            <option value="PEN">Nuevo Sol (PEN)</option>
        </select>
        <br><br>
        <label for="plan-select">Selecciona el Plan:</label>
        <select id="plan-select">
            <option value="Basic">Básico</option>
            <option value="Advanced">Avanzado</option>
            <option value="Elite">Élite</option>
        </select>
        <br><br>
        <button onclick="submitPayment()">Enviar</button>
    </div>
</div>

<script>
    // Show the pop-up on page load
    window.onload = function() {
        document.getElementById('popup').style.display = 'flex';
    };

    // Function to handle the payment form submission
    function submitPayment() {
        var amount = document.getElementById('amount-paid-popup').value;
        var plan = document.getElementById('plan-select').value;
        var currency = document.getElementById('currency').value;

        if (amount && plan && currency) {
            alert('Pago de ' + currency + ' ' + amount + ' para el plan: ' + plan + ' registrado correctamente.');
            document.getElementById('popup').style.display = 'none';
        } else {
            alert('Por favor, complete todos los campos.');
        }
    }

    // Function to update the balance based on the amount entered
    function updateBalance() {
        var amountPaid = document.getElementById('amount-paid').value;
        var currency = document.getElementById('currency').value;
        var currentBalance = 5000;  // Initial balance, can be dynamic based on user data
        var newBalance = parseFloat(currentBalance) + parseFloat(amountPaid);

        if (isNaN(newBalance)) {
            alert("Por favor, ingrese un monto válido.");
        } else {
            document.getElementById('balance').innerText = currency + " " + newBalance.toFixed(2);
            alert("¡Saldo actualizado exitosamente!");
        }
    }
</script>

</body>
</html>
