<template>
  <v-list-item
  class="
  d-flex
  flex-wrap
  justify-start
  mx-2
  text-left"
  >
    <v-checkbox type="checkbox" v-on:click="$emit('checBoxTask', todos.id)" v-bind:checked="todos.complited"
      color=#69a563f0 />
    <v-list-item-title>
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

<style>
.done {
  text-decoration: line-through;
}
</style>