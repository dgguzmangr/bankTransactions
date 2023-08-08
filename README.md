# bankTransactions

Administration of bank movements. Front end project developed with Vue3 for a CRUD that takes an Excel csv file as a database.

To install project dependencies: npm i.
To run the project, navigate to the 'bankmovements' folder and execute: npm run serve.

The requirement is as follows: A screen is needed that allows importing a CSV file of bank transactions (date, description, amount, unique transfer code). These transactions should be listed in a table displaying the amount in Peruvian Soles (PEN). If the transaction is in US Dollars (USD), the amount must be converted to Peruvian Soles (PEN) based on the exchange rate from SUNAT. Additionally, there should be an option to edit or delete any of these transactions.

Bank transactions: [{'date':'2023-05-28','description':'ITF','currency':'PEN','amount': -1.7, 'unique_code':'2010221'},{'date':'2023-05-28','description':'Refund for Invoice F01-00214','currency':'PEN','amount': -380, 'unique_code':'2010223'},{'date':'2023-05-29','description':'Interbank Commission','currency':'USD','amount': -5.3, 'unique_code':'2010225'},{'date':'2023-05-29','description':'Payment for RxH E01-00180','currency':'USD','amount': -1800, 'unique_code':'2010226'},{'date':'2023-05-30','description':'Microsoft Purchase','currency':'USD','amount': -9.9, 'unique_code':'2010227'},{'date':'2023-05-30','description':'Google Invoice Payment','currency':'USD','amount': -52.5, 'unique_code':'2010229'}]

SUNAT Exchange Rate: [{'date':'2023-05-28','sell':3.675,'buy':3.671},{'date':'2023-05-29','sell':3.678,'buy':3.674},{'date':'2023-05-30','sell':3.68,'buy':3.667}]


El requerimiento es el siguiente: Se necesita una pantalla que permite importar un archivo csv de movimientos bancarios (fecha, descripción, monto, código único de transferencia). Estos movimientos deben ser listados en una tabla donde se muestre el monto en soles (PEN). En caso el movimiento sea en dólares (USD), el monto debe ser convertido a soles (PEN) según el tipo de cambio de SUNAT. Además, se debe poder editar/eliminar alguno de ellos.

Movimientos bancarios: [{'fecha':'2023-05-28','descripcion':'ITF','moneda':'PEN', 'monto': -1.7, 'codigo_unico':'2010221'},{'fecha':'2023-05-28','descripcion':'Reembolso por Factura F01-00214','moneda':'PEN','monto': -380, 'codigo_unico':'2010223'},{'fecha':'2023-05-29','descripcion':'Comisión interbancaria','moneda':'USD','monto': -5.3, 'codigo_unico':'2010225'},{'fecha':'2023-05-29','descripcion':'Pago de RxH E01-00180','moneda':'USD','monto': -1800, 'codigo_unico':'2010226'},{'fecha':'2023-05-30','descripcion':'Consumo Microsoft','moneda':'USD','monto': -9.9, 'codigo_unico':'2010227'},{'fecha':'2023-05-30','descripcion':'Pago Invoice Google','moneda':'USD','monto': -52.5, 'codigo_unico':'2010229'}]


Tipo de Cambio Sunat: [{'fecha':'2023-05-28','venta':3.675,'compra':3.671},{'fecha':'2023-05-29','venta':3.678,'compra':3.674},{'fecha':'2023-05-30','venta':3.68,'compra':3.667}]