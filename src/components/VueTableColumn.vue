<template>
  <th>
    <span @click="sortBy">{{ label }}</span><br>
    <span v-if="searchable" @click="toggleSearch">search: {{ search }}</span>
  </th>
</template>

<script>
  export default {
    props: {
      label: {
        type: String
      },
      id: {
        type: String
      },
      sortType: {
        type: String,
        default: 'string'
      },
      searchable: {
        default: true
      }
    },
    data() {
      return {
        search: this.searchable
      }
    },
    methods: {
      sortBy() {
        this.$parent.sortBy({id: this.id, sortType: this.sortType})
      },
      toggleSearch() {
        this.search = ! this.search;
        this.$parent.setColumns();
        this.$parent.getSearch();
      }
    }
  }
</script>
