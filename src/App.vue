<template>
  <div id="app">
      <EditableTable v-model="items" :fields="fields"></EditableTable>
  </div>
</template>

<script>
import EditableTable from './components/EditableTable.vue';

export default {
  descripcion: "App",
  components: {
    EditableTable
  },
  data() {
    return {
      fields: [
        { key: "selectRow", label: "" },
        { key: "descripcion", label: "descripcion", type: "text" },
        { key: "tipo", label: "tipo", type: "select", options: ['Debe', 'Haber'] },
        { key: "cantidad", label: "cantidad", type: "number" },
        { key: "fecha", label: "fecha", type: "date" },
        { key: "edit", label: "", type: "edit" }
      ],
       items: [
          { cantidad: 100, descripcion: 'Caja', tipo: 'Debe', fecha: '2021-05-20' },
          { cantidad: 150, descripcion: 'Deudores Varios', tipo: 'Debe', fecha: '2021-05-20' },
          { cantidad: 100, descripcion: 'Caja', tipo: 'Haber', fecha: '2021-05-20' },
          { cantidad: 150, descripcion: 'Bco Cta Cte', tipo: 'Haber', fecha: '2021-05-20' }
        ]
    };
  }
};
</script>

<style>
#app {
  margin: 20px;
}
</style>