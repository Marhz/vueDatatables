<template>
  <td>
    <span v-for="action in actionColumn.def" @click="action.callback(row)">
      <i :class="action.icon"></i><span v-text="action.text"></span>
    </span>
  </td>
</template>

<script>
  export default {
    props: ['actionColumn', 'row']
  }
</script>
