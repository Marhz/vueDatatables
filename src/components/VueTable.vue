<template>
  <div>
    <div class="search">
      <label for="search">Search :</label>
      <input type="text" id="search" @keyup="getSearch" v-model="search">
    </div>
    <table>
      <thead>
        <tr>
          <slot></slot>
          <th v-if="hasAction">{{ actionColumn.title }}</th>
        </tr>
      </thead>
      <tbody>
        <tr v-for="row in paginatedData">
          <td v-for="{ id } in columns">
            {{ row[id] }}
          </td>
          <vue-table-action-column
            v-if="hasAction"
            :actionColumn="actionColumn"
            :row="row"
          ></vue-table-action-column>
        </tr>
      </tbody>
    </table>
    <div v-if="emptyTable" class="vue-table__no-data">
      No data to display
    </div>
    <div v-if="pages > 1">
      <button @click="prevPage">prev</button>
      <button @click="nextPage">next</button>
      <pre>{{currentPage}} / {{ this.pages }}</pre>
    </div>
    <div>
      <label for="">Per page :</label>
      <select v-model="perPage">
        <option v-for="num in perPageOptions" :value="num">{{ num }}</option>
      </select>
    </div>
  </div>
</template>

<script>
  import VueTableActionColumn from './VueTableActionColumn.vue'
  export default {
    components: { VueTableActionColumn },
    props: {
      data: {
        type: Array
      },
      actionColumn: {
        type: Object,
        default() {
          return {
            actions: []
          }
        }
      },
      perPageOptions: {
        type: Array,
        default() {
          return [2,4,8]
        }
      }
    },
    data() {
      return {
        displayedData: this.data,
        columns: [],
        lastSortedBy: '',
        currentPage: 1,
        pages: 0,
        search: '',
        perPage: this.perPageOptions[0]
      }
    },
    watch: {
      //work around to update the displayedData object when an action is used
      data: function () {
        this.displayedData = this.data;
        this.getSearch();
      }
    },
    methods: {
      sortBy({id, sortType}) {
        if (this.lastSortedBy === id) {
          this.displayedData.reverse();
          return;
        }
        switch (sortType) {
          case 'number': {
            this.displayedData.sort((a, b) =>  a[id] - b[id])
            break;
          }
          case 'string': {
            this.displayedData.sort((a, b) => {
              if (a[id] < b[id])
                return -1
              if (a[id] > b[id])
                return 1
              return 0
            });
            break;
          }
        }
        this.lastSortedBy = id
      },
      nextPage() {
        if (this.currentPage == this.pages)
          this.currentPage = 1;
        else
          this.currentPage++;
      },
      prevPage() {
        if (this.currentPage == 1)
          this.currentPage = this.pages;
        else
          this.currentPage--;
      },
      getSearch() {
        if (this.search === "") {
          this.displayedData = this.data;
          return;
        }
        const columns = this.columns.filter(c => c.searchable);
        this.displayedData = this.data.filter((row, index) => {
          for (const column of columns) {
            if ((""+row[column.id]).includes(this.search)) {
              return true;
            }
          }
          return false;
        })
      },
      setColumns() {
        this.columns = this.$children
          .filter(c => c.id !== undefined) //filters vue-table-column elements, can probably be done cleaner
          .map(c => {
            return {id: c.id, searchable: c.search}
          });
      }
    },
    computed: {
      paginatedData() {
        this.pages = Math.ceil(this.displayedData.length / this.perPage);
        if (this.currentPage > this.pages && this.pages > 0)
          this.currentPage = this.pages;
        let page = this.perPage * this.currentPage;
        return this.displayedData.slice(page - this.perPage, page);
      },
      hasAction() {
        return this.actionColumn.actions.length > 0
      },
      emptyTable() {
        return this.displayedData.length === 0
      }
    },
    mounted() {
      this.setColumns();
    }
  }
</script>

<style>
  table {
    width: 100%;
  }
  td {
    text-align: center;
  }
  tr:nth-child(even), thead {
    background: #ececec
  }
  .search {
    margin-bottom: 15px;
    float: right;
  }
  .vue-table__no-data {
    display: flex;
    align-items: center;
    justify-content: center;
    width: 100%;
    height: 300px;
    background: #afafaf;
    font-size: 35px;
  }
</style>
