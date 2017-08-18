<template>
  <td>
    <span v-for="action in actionColumn.actions" @click="action.callback(row)">
      <span>
        <i :class="action.icon"></i><span v-text="action.text"></span>
      </span>
    </span>
  </td>
</template>

<script>
  export default {
    props: ['actionColumn', 'row']
  }
</script>
