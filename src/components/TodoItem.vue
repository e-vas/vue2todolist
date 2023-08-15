<template>
  <v-list-item
  class="
  d-flex
  justify-space-between
  rounded-lg
  list-item
  "
  elevation="4"
  >
    <v-checkbox type="checkbox" v-on:click="$emit('checBoxTask', todos.id)" v-bind:checked="todos.complited"
      color=#69a563f0 />
    <v-list-item-title class="item-title  text-left d-flex flex-wrap" width="395px">
      {{ todos.title }}
    </v-list-item-title>
    <v-btn color=#c91a1a elevation="6" icon large v-on:click="$emit('deleteTask', todos.id)">
      &#x2716;

    </v-btn>
  </v-list-item>
</template>

<script>
export default {
  props:
    ['todos'],

  components: {


  },


}

</script>

<style scoped>
.done {
  text-decoration: line-through;
}
.item-title {
  white-space: normal;
}
.list-item {
  border-bottom: solid rgba(128, 128, 128, 0.486) 1px;
}
</style>