<template>
  <div>
    <h2> The first Usuage of AXIOS </h2>
    <ag-grid-vue
      class="ag-theme-balham"
      style="width: 100%; height: 100vh"
      :columnDefs="columnDefs.value"
      :rowData="rowData.value"
    ></ag-grid-vue>
  </div>
</template>

<script>
import { AgGridVue } from 'ag-grid-vue3';
import { reactive, onMounted } from 'vue';

import 'ag-grid-community/dist/styles/ag-grid.css';
import 'ag-grid-community/dist/styles/ag-theme-balham.css';


export default {
  name: 'App',
  components: {
    AgGridVue
  },
  setup() {
    let columnDefs = reactive({
      value: [
      { field: 'athlete' },
      { field: 'age', filter: 'agNumberColumnFilter' },
      { field: 'country', filter: 'agTextColumnFilter'},
      { field: 'year' },
      { field: 'date' },
      { field: 'sport' },
      { field: 'gold' },
      { field: 'silver' },
      { field: 'bronze' },
      { field: 'total' }
      ]
    });
    let rowData = reactive({
      value: []
    });
    const defaultColDef = {
      def: { flex: 1, minWidth: 100, sortable: true, filter: true }
    };

    onMounted(() => {
      fetch("https://www.ag-grid.com/example-assets/olympic-winners.json")
        // .then(response => {
        //   rowData.value = response.data
        // })
        .then((result) => result.json())
        .then((remoteRowData) => (rowData.value = remoteRowData));
    });

    return {
      columnDefs,
      rowData,
      defaultColDef
    };
  }
}
</script>

<style>

</style>
