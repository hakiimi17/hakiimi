<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>HAKIMI INTERNATIONAL BUSINESS </title>
    <link href="https://maxcdn.bootstrapcdn.com/bootstrap/4.5.2/css/bootstrap.min.css" rel="stylesheet">
    <style>
        #receipt {
            border: 1px solid #ccc;
            padding: 20px;
            border-radius: 10px;
            background-color: #f9f9f9;
            margin-top: 20px;
        }
        #receipt h4 {
            text-align: center;
            margin-bottom: 20px;
        }
        #receiptItems p {
            border-bottom: 1px dotted #ccc;
            padding-bottom: 5px;
            margin-bottom: 5px;
        }
        .total-section {
            text-align: right;
            font-size: 1.2em;
            font-weight: bold;
        }
    </style>
</head>
<body>
    <div class="container mt-5">
        <div class="card">
            <div class="card-header text-center">
                <h3>Risiit</h3>
            </div>
            <div class="card-body">
                <form>
                    <div id="itemsContainer">
                        <div class="form-group item-row">
                            <label for="itemName1">Sheyga La Gatay 1</label>
                            <input type="text" class="form-control itemName" placeholder="Gali magaca sheyga">
                            <label for="itemPrice1">Qiimaha (Lacagta) 1</label>
                            <input type="number" class="form-control itemPrice" placeholder="Gali qiimaha sheyga">
                        </div>
                    </div>
                    <button type="button" class="btn btn-secondary mb-3" onclick="addItem()">Ku Dar Shey</button>
                    <div class="form-group">
                        <label for="purchaseDate">Xiliga Iibka</label>
                        <input type="date" class="form-control" id="purchaseDate">
                    </div>
                    <button type="button" class="btn btn-primary" onclick="generateReceipt()">Samee Risiit</button>
                </form>
                <div id="receipt" style="display:none;">
                    <h4>Faahfaahinta Risiitka</h4>
                    <p><strong>Magaca Goobta:</strong> HAKIMI INTERNATIONAL BUSINESS</p>
                    <div id="receiptItems"></div>
                    <p class="total-section"><strong>Wadarta Guud:</strong> <span id="totalPrice"></span></p>
                    <p><strong>Xiliga Iibka:</strong> <span id="receiptPurchaseDate"></span></p>
                </div>
            </div>
        </div>
    </div>

    <script>
        let itemCount = 1;

        function addItem() {
            itemCount++;
            const itemsContainer = document.getElementById('itemsContainer');
            const itemRow = document.createElement('div');
            itemRow.className = 'form-group item-row';
            itemRow.innerHTML = `
                <label for="itemName${itemCount}">Sheyga La Gatay ${itemCount}</label>
                <input type="text" class="form-control itemName" placeholder="Gali magaca sheyga">
                <label for="itemPrice${itemCount}">Qiimaha (Lacagta) ${itemCount}</label>
                <input type="number" class="form-control itemPrice" placeholder="Gali qiimaha sheyga">
            `;
            itemsContainer.appendChild(itemRow);
        }

        function generateReceipt() {
            const purchaseDate = document.getElementById('purchaseDate').value;
            const itemNames = document.querySelectorAll('.itemName');
            const itemPrices = document.querySelectorAll('.itemPrice');

            let receiptItemsHTML = '';
            let total = 0;

            itemNames.forEach((itemName, index) => {
                const price = parseFloat(itemPrices[index].value) || 0;
                total += price;

                receiptItemsHTML += `
                    <p><strong>Sheyga ${index + 1}:</strong> ${itemName.value} - <strong>Qiimaha:</strong> ${price.toFixed(2)} USD</p>
                `;
            });

            document.getElementById('receiptItems').innerHTML = receiptItemsHTML;
            document.getElementById('totalPrice').innerText = total.toFixed(2) + " USD";
            document.getElementById('receiptPurchaseDate').innerText = purchaseDate;

            document.getElementById('receipt').style.display = 'block';
        }
    </script>
</body>
</html>

