<template>
  <div class="container">
    <vue-table :data="data" :actionColumn="actionColumn" :perPageOptions="[1,2,5]">
      <vue-table-column label="id" id="id" sortType="number" :searchable="false"></vue-table-column>
      <vue-table-column label="Age" id="age" sortType="number"></vue-table-column>
      <vue-table-column label="Prenom" id="nom" sortType="string"></vue-table-column>
      <vue-table-column label="wtf" id="status" sortType="string"></vue-table-column>
      <vue-table-column label="Admin?" id="admin" sortType="number"></vue-table-column>
    </vue-table>
  </div>
</template>

<script>

import vueTable from './VueTable.vue'
import vueTableColumn from './VueTableColumn.vue'

export default {

  components: {
    vueTable,
    vueTableColumn
  },

  name: 'hello',
  data () {
    return {
      msg: 'Welcome to Your Vue.js App',
      actionColumn: {
        title: "Actions",
        actions: [{
          text: "Edit",
          icon: "fa fa-edit",
          callback: (row) => {
            alert("edit row with id: "+row.id)
          }
        },
        {
          text: 'delete',
          icon: 'fa fa-trash',
          callback: (row) => {
            this. data = this.data.filter(d => d.id !== row.id)
          }
        }]
      },
      data: []
    }
  },
  methods: {
  },
  created() {
      this.data = [
        {
          'id': 0,
          'nom': "test",
          'age': '65',
          'status': "dunncare",
          'admin': 0,
        },
        {
          'id': 1,
          'nom': "gogo",
          'age': '45',
          'status': "yolo",
          'admin': 1
        },
        {
          'id': 2,
          'nom': "lkpmlk",
          'age': '85',
          'status': "rkgegez",
          'admin': 0
        },
        {
          'id': 3,
          'nom': "test",
          'age': '15',
          'status': "dunncare",
          'admin': 0
        },
        {
          'id': 4,
          'nom': "gogo",
          'age': '45',
          'status': "yolo",
          'admin': 1
        },
        {
          'id': 5,
          'nom': "lkpmlk",
          'age': '85',
          'status': "rkgegez",
          'admin': 0
        },
        {
          'id': 6,
          'nom': "test",
          'age': '15',
          'status': "dunncare",
          'admin': 0
        },
        {
          'id': 7,
          'nom': "gogo",
          'age': '45',
          'status': "yolo",
          'admin': 1
        },
        {
          'id': 8,
          'nom': "lkpmlk",
          'age': '85',
          'status': "rkgegez",
          'admin': 0
        },
      ]
    }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
h1, h2 {
  font-weight: normal;
}

ul {
  list-style-type: none;
  padding: 0;
}

li {
  display: inline-block;
  margin: 0 10px;
}

a {
  color: #42b983;
}
.container {
  width: 70%;
  margin: auto;
}
</style>
