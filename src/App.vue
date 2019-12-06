<template>
  <div id="app">
    <ejs-grid :dataSource="data" :editSettings="editOptions" :toolbar="toolbarOptions">
      <e-columns>
        <e-column field='OrderID' headerText='Order ID' :isPrimaryKey='true'></e-column>
        <e-column field='CustomerID' headerText='Customer ID' editType="dropdownedit"></e-column>
        <e-column field='Freight' headerText='Freight' format="C2"></e-column>
        <e-column field='ShipCountry' headerText='Ship Country'></e-column>
        <e-column field='ShipPostalCode' headerText='Ship PostalCode' :editTemplate="editTemplate"></e-column>
      </e-columns>
    </ejs-grid>
  </div>
</template>

<script>
import Vue from "vue";
import { GridPlugin, Edit, Toolbar  } from '@syncfusion/ej2-vue-grids';
import { MaskedTextBoxPlugin } from '@syncfusion/ej2-vue-inputs'
Vue.use(GridPlugin);
Vue.use(MaskedTextBoxPlugin);
export default {
  name: 'app',
  data () {
    return {
       data: [
          { OrderID: 10248, CustomerID: 'VINET', Freight: 23.5, ShipCountry: "France", ShipPostalCode: "3012" },
          { OrderID: 10250, CustomerID: 'HANAR', Freight: 17.78, ShipCountry: "Germany", ShipPostalCode: "2089" },
          { OrderID: 10251, CustomerID: 'VICTE', Freight: 43.33, ShipCountry: "Brazil", ShipPostalCode: "1123" },
          { OrderID: 10252, CustomerID: 'SUPRD', Freight: 22.3, ShipCountry: "France", ShipPostalCode: "6577" },
          { OrderID: 10253, CustomerID: 'HANAR', Freight: 23.59, ShipCountry: "Belgium", ShipPostalCode: "4424" },
          { OrderID: 10254, CustomerID: 'CHOPS', Freight: 10.5, ShipCountry: "Brazil", ShipPostalCode: "8989" },
          { OrderID: 10255, CustomerID: 'RICSU', Freight: 12.33, ShipCountry: "Switzerland", ShipPostalCode: "1765" },
          { OrderID: 10256, CustomerID: 'WELLI', Freight: 21.2, ShipCountry: "Switzerland", ShipPostalCode: "5553" },
          { OrderID: 10249, CustomerID: 'TOMSP', Freight: 22.07, ShipCountry: "France", ShipPostalCode: "1209" },],
        editOptions: { allowAdding: true, allowEditing: true, allowDeleting: true, mode: "Dialog"},
        toolbarOptions: ["Add", "Edit", "Delete", "Update", "Cancel"],
    };
  },
  provide: {
    grid: [Edit, Toolbar]
  },
  methods: {
    editTemplate: function() {
      return {
        template: Vue.component("MaskEditTextBox", {
          template: `<ejs-maskedtextbox id="ShipPostalCode" v-model="data.ShipPostalCode" mask="00-00"  ></ejs-maskedtextbox>`,
          data() {
            return {
              data: {}
            };
          }
        })
      };
    }
	
  }
}
</script>

<style>
  @import url("https://cdn.syncfusion.com/ej2/material.css");
</style>