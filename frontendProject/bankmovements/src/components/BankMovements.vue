<template>
  <div>
    <div class="row align-items-center py-3">
      <div class="col">
        <h4>Importar Movimientos Bancarios</h4>
      </div>
      <div class="col">
        <input id="excelFile" type="file" @change="uploadFile()" accept=".csv"/>
      </div>
    </div>
    
    <div class="">
      <h2>Listado de Movimientos Bancarios</h2>
      <table v-if="items.length > 0" class="table">
        <thead>
          <tr>
            <th>Fecha</th>
            <th>Descripción</th>
            <th>Moneda</th>
            <th>Monto</th>
            <th>Código único</th>
          </tr>
        </thead>
        <tbody>
          <tr v-for="(item, index) in items" :key="index">
            <td class="text-center" @click="editItem(item, index)">{{ item[0] }}</td>
            <td class="text-start" @click="editItem(item, index)">{{ item[1] }}</td>
            <td class="text-center" @click="editItem(item, index)">PEN</td>
            <td class="text-start" @click="editItem(item, index)">{{ convertToPEN(item) }}</td>
            <td class="text-center" @click="editItem(item, index)">{{ item[4] }}</td>
            
            <td>
              <button @click="deleteItem(index)" class="btn btn-danger">Eliminar</button>
            </td>
          </tr>
        </tbody>
      </table>
      <button @click="addItem" class="btn btn-success">
        Agregar Registro
      </button>
      <button v-if="items.length > 0" @click="downloadExcelFile()" class="btn btn-primary">
        Descargar Excel
      </button>
    </div>
  </div>
</template>

<script>
import Papa from "papaparse";
import exportXlsFile from "export-from-json";

export default {
  data() {
    return {
      items: [],
      tipoDeCambio: [
        {fecha: '28/05/2023', venta: 3.675, compra: 3.671},
        {fecha: '29/05/2023', venta: 3.678, compra: 3.674},
        {fecha: '30/05/2023', venta: 3.68, compra: 3.667},
      ]
    };
  },
  methods: {
    uploadFile() {
      const input = document.getElementById("excelFile");
      const file = input.files[0];
      
      if (file) {
        Papa.parse(file, {
          complete: (result) => {
            this.items = result.data;
          },
          header: false, // Adjust this if your CSV has headers
        });
      }
    },
    downloadExcelFile() {
      const data = this.items;
      const fileName = 'download';
      const exportType = exportXlsFile.types.xls;
      exportXlsFile({ data, fileName, exportType });
    },
    addItem() {
    this.items.push(['', '', '', '', '']); // Agregar un nuevo registro vacío
    },
    editItem(item, index) {
      const newDate = prompt('Editar fecha:', item[0]); // Solicitar nuevo valor
      if (newDate !== null) {
        this.items[index][0] = newDate;
      }
      const newValue = prompt('Editar descripción:', item[1]); // Solicitar nuevo valor
      if (newValue !== null) {
        this.items[index][1] = newValue;
      }
      const newMoney = prompt('Editar moneda:', item[2]); // Solicitar nuevo valor
      if (newMoney !== null) {
        this.items[index][2] = newMoney;
      }
      const newAmount = prompt('Editar monto:', item[3]); // Solicitar nuevo valor
      if (newAmount !== null) {
        this.items[index][3] = newAmount;
      }
      const newCode = prompt('Editar código único:', item[4]); // Solicitar nuevo valor
      if (newCode !== null) {
        this.items[index][4] = newCode;
      }
    },
    deleteItem(index) {
      if (confirm('¿Seguro que deseas eliminar este registro?')) {
        this.items.splice(index, 1);
      }
    },
    convertToPEN(item) {
      const currencyIndex = this.tipoDeCambio.findIndex(entry => entry.fecha === item[0]);
      console.log("Currency Index:", currencyIndex);
      if (currencyIndex !== -1 && item[2].toLowerCase() === 'usd') {
        const exchangeRate = this.tipoDeCambio[currencyIndex].compra;
        console.log("Exchange Rate:", exchangeRate);
        console.log("Original Amount:", item[3]);
        const convertedAmount = (parseFloat(item[3]) * exchangeRate).toFixed(2);
        console.log("Converted Amount:", convertedAmount);
        return convertedAmount;
      }
      return item[3];
    },
  },
};
</script>

<style scoped>
</style>
