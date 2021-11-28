<template>
  <div id="app">

      <EditableTable v-model="items" :fields="fields" :key="componentKey"></EditableTable>
          <div>
    <b-button v-b-modal.modal-1>Generar asiento</b-button>

    <b-modal id="modal-1" title="BootstrapVue">
    <p class="my-4">Cuenta Debe/Haber</p>
        <b-form @submit="onSubmit" v-if="show">
      <b-form-group
        id="input-group-1"
        label="Cuenta Debe: "
        label-for="input-1"
      >
        <b-form-input
          id="input-1"
          v-model="form.ctaDebe"
          placeholder="Ingrese el nombre de la cuenta Debe"
          required
        ></b-form-input>
      </b-form-group>

      <b-form-group id="input-group-2" label="Cuenta Haber:" label-for="input-2">
        <b-form-input
          id="input-2"
          v-model="form.ctaHaber"
          placeholder="Ingrese el nombre de la cuenta del Haber"
          required
        ></b-form-input>
      </b-form-group>

<b-form-group id="input-group-2" label="Cantidad:" label-for="input-3">
        <b-form-input
          id="input-3"
          type="number"
          v-model="form.cantidad"
          placeholder="Ingrese la cantidad de las cuentas"
          required
        ></b-form-input>
      </b-form-group>

        <b-form-datepicker v-model="form.fecha"></b-form-datepicker>
      <b-button type="submit" variant="primary">Submit</b-button>
      
    </b-form>

    </b-modal>  
    </div>
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
let titleAdded=[];
//items=this.items
let Comp = {
 template: '<div></div>'
}
function tablas(items){
    let tabla='';
    
    for (var i = 0; i < items.length; i++) {
    let total=0;
    if(!(titleAdded.includes(items[i].descripcion))){
      
      tabla=tabla+'<table>'+'<tr>'+items[i].descripcion+'</tr>';
      titleAdded.push(items[i].descripcion);
      tabla=tabla+'<tr>'+' <tr><th>Debe</th><th>Haber</th></tr>'
    for (var j = 0; j < items.length; j++) {
      if((items[i].descripcion==items[j].descripcion)&&(items[j].tipo=='Debe')){
        tabla=tabla+'<tr>'+'<td>'+items[j].cantidad+'</td>'+'</tr>'
        total=total+items[j].cantidad;
      }
      if((items[i].descripcion==items[j].descripcion)&&(items[j].tipo=='Haber')){
        tabla=tabla+'<tr>'+'<td></td>'+'<td>'+items[j].cantidad+'</td>'+'</tr>'
        total=total-items[j].cantidad;
      }
      
    }
    }
    tabla=tabla+'<tr></tr>'
    if(total>0){
    tabla=tabla+'<td><b>'+total+'</b></td>'
    }
    if(total<0){
    tabla=tabla+'<td></td>'+'<td><b>'+Math.abs(total)+'</b></td>'
    }
    console.log(total)
    tabla=tabla+'</tr>'+'</table>'
    } //end item table Caja eg
    
    return tabla;
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
/*   for (var i = 0; i < this.items.length; i++) {
console.log(this.items[i].descripcion);
  } */
  Comp = {
 template: '<div>'+tablas(this.items)+'</div>'//'<div>Hello world '+this.items[0].descripcion+tablas(this.items)+'</div>' 
 }
this.comp2.push(Comp)
},
onSubmit(event) {
        event.preventDefault()
        alert(JSON.stringify(this.form))
        let debe={cantidad: this.form.cantidad, descripcion: this.form.ctaDebe, tipo: 'Debe', fecha: this.form.fecha}
        let haber={cantidad: this.form.cantidad, descripcion: this.form.ctaHaber, tipo: 'Haber', fecha: this.form.fecha}
        this.items.push(debe)
        this.items.push(haber) 
        this.componentKey += 1
      },
  },
  data() {
    return {
      componentKey: 0,
      form: {
          ctaDebe: '',
          ctaHaber: '',
          cantidad: 0,
          fecha: ''
        },
        show: true,
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
          { cantidad: 150, descripcion: 'Caja', tipo: 'Haber', fecha: '2021-05-20' },
          { cantidad: 100, descripcion: 'Bco Cta Cte', tipo: 'Haber', fecha: '2021-05-20' }
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