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
    const columnDefs = reactive({
      value: [
      { field: 'userId' },
      { field: 'id' },
      { field: 'title' },
      { field: 'body' }
      ]
    });
    const rowData = reactive({
      value: [
      { userId: '', id: '', title: '', body: '' }
    ]});
    onMounted(() => {
      axios.get("https://jsonplaceholder.typicode.com/posts")
        .then(response => {
          rowData.value = response.data
        })
        .then((result) => result.json())
        .then((remoteRowData) => (rowData.value = remoteRowData));
    });

    return {
      columnDefs,
      rowData
    };
  }
}
</script>

<style>

</style>
