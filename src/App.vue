<template>
  <div id="app">
      <EditableTable v-model="items" :fields="fields"></EditableTable>
      <!-- <b-button v-on:click="libroMayor">Generar libro Mayor</b-button> -->
        <b-button type="button" @click="libroMayor">Generar libro Mayor</b-button>
  <component
    v-for="(component, index) in comp2"
    :key="index"
    :is="component"
  />
  </div>
</template>

<script>
import EditableTable from './components/EditableTable.vue';
let items2=[{descripcion: 'asd'}]
//items=this.items
let Comp = {
 template: '<div>Hello world '+items2[0].descripcion+'</div>'
}
export default {
  descripcion: "App",
  components: {
    EditableTable, Comp
  },
/*   watch: {
    items2 = this.items
  }, */
  methods:{
    libroMayor(){
  for (var i = 0; i < this.items.length; i++) {
console.log(this.items[i].descripcion);
  }
  Comp = {
 template: '<div>Hello world '+this.items[0].descripcion+'</div>' }
this.comp2.push(Comp)
},
  },
  data() {
    return {
      comp2: [Comp],
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