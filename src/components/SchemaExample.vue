<template>
  <div id="app">
    <article>
      <h3>Employee Information</h3>
      <EditTableRow v-model="items1" :fields="fields1"></EditTableRow>
    </article>
    <article>
      <h3>Employee Contract</h3>
      <EditTableRow v-model="items2" :fields="fields2"></EditTableRow>
    </article>
  </div>
</template>

<script>
import EditTableRow from './EditTableRow.vue';

export default {
  name: "SchemaExample",
  components: {
    EditTableRow
  },
  data() {
    return {
      fields1: [
        { key: "name", label: "Name", type: "text" },
        { key: "department", label: "Department", type: "select", options: ['Development', 'Marketing', 'HR', 'Accounting'] },
        { key: "age", label: "Age", type: "number" },
        { key: "dateOfBirth", label: "Date Of Birth", type: "date" },
        { key: "edit", label: "", type: "edit" }
      ],
       items1: [
          { age: 40, name: 'Dickerson', department: 'Development', dateOfBirth: '1984-05-20' },
          { age: 21, name: 'Larsen', department: 'Marketing', dateOfBirth: '1984-05-20' },
          { age: 89, name: 'Geneva', department: 'HR', dateOfBirth: '1984-05-20' },
          { age: 38, name: 'Jami', department: 'Accounting', dateOfBirth: '1984-05-20' }
        ],
        fields2: [
          { key: "id", label: "ID", type: "number" },
          { key: "name", label: "Name", type: "text" },
          { key: "contractEndDate", label: "Contract End Date", type: "date" },
          { key: "edit", label: "", type: "edit" }
      ],
       items2: [
          { id: 123, name: 'Dickerson', contractEndDate: '2022-05-20' },
          { id: 345, name: 'Larsen', contractEndDate: '2021-05-20' },
          { id: 456, name: 'Geneva', contractEndDate: '2023-05-20' },
          { id: 678, name: 'Jami', contractEndDate: '2024-05-20' }
        ]
    };
  }
};
</script>

<style>
#app {
  text-align: center;
  margin: 60px;
}
pre {
  text-align: left;
  color: #d63384;
}
</style>