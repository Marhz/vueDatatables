<template>
  <div class="container">
    <vue-table :data="data" :actionColumn="actionColumn" :perPageOptions="[3,6,9]">
      <vue-table-column label="id" id="id" sortType="number" :searchable="false"></vue-table-column>
      <vue-table-column label="Age" id="age" sortType="number"></vue-table-column>
      <vue-table-column label="Name" id="name" sortType="string"></vue-table-column>
      <vue-table-column label="Activity" id="status" sortType="string"></vue-table-column>
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
      data: [],
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
      }
    }
  },
  methods: {
  },
  created() {
      this.data = [
        {
          'id': 0,
          'name': "Micheal Jackson",
          'age': '65',
          'status': "Dead",
          'admin': 0,
        },
        {
          'id': 1,
          'name': "Palpatine",
          'age': '100',
          'status': "Emperor",
          'admin': 1
        },
        {
          'id': 2,
          'name': "Teemo",
          'age': '85',
          'status': "Cancer",
          'admin': 0
        },
        {
          'id': 3,
          'name': "John doe",
          'age': '15',
          'status': "Unknown",
          'admin': 0
        },
        {
          'id': 4,
          'name': "Usain Bolt",
          'age': '45',
          'status': "Running",
          'admin': 1
        },
        {
          'id': 5,
          'name': "Cancer",
          'age': '85',
          'status': "Teemo",
          'admin': 0
        },
        {
          'id': 6,
          'name': "Alan Rickman",
          'age': '15',
          'status': "Dead",
          'admin': 0
        },
        {
          'id': 7,
          'name': "Napoleon",
          'age': '45',
          'status': "Emperor",
          'admin': 1
        },
        {
          'id': 8,
          'name': "Daenerys Targs",
          'age': '85',
          'status': "Queen",
          'admin': 0
        },
        {
          'id': 9,
          'name': "Elizabeth II",
          'age': '85',
          'status': "Queen",
          'admin': 0
        },
        {
          'id': 10,
          'name': "Me",
          'age': '1337',
          'status': "Trash",
          'admin': 0
        },
        {
          'id': 11,
          'name': "Darth Vader",
          'age': '69',
          'status': "Emperorslayer",
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
