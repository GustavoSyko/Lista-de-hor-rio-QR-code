<template>
  <div>
    <h1>Horários</h1>

    <b-table 
      :items="tableData" 
      :fields="tableFields"
      >

    </b-table>


  </div>
</template>

<script>

import { BTable } from 'bootstrap-vue'

// verificar outro componente bootstrap para fazer as linhas ( group item talvez algo assims)


export default {
  name: 'HelloWorld',

  data() {
    return {
      tableData: [
        { id: 1, name: 'Alice', age: 25 },
        { id: 2, name: 'Bob', age: 30 },
        // Mais dados aqui...
      ],
      tableFields: [
        { key: 'name', label: 'Nome' },
        { key: 'age', label: 'Idade' },
        // Mais campos aqui...
      ],
    };
  },

  components: {
    BTable,

  },
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped></style>
