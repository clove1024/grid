<template>
  <div>
    <h2> The first Usuage of AXIOS </h2>
    <ag-grid-vue
      class="ag-theme-balham"
      style="height: 500px"
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
import axios from 'axios'

export default {
  name: 'App',
  components: {
    AgGridVue
  },
  setup() {
    let columnDefs = reactive({
      value: [
      { field: 'athlete' },
      { field: 'age' },
      { field: 'country' },
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
      sortable: true,
      filter: true
    };

    onMounted(() => {
      axios.get("https://www.ag-grid.com/example-assets/olympic-winners.json")
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
