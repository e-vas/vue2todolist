<template>
  <li>
    <input type="checkbox" 
    v-on:click="$emit('checBoxTask', todos.id)"
    v-bind:checked="todos.complited"
    
    /> 
    <span>
      {{ todos.title }}
    </span>
    <button
    v-on:click="$emit('deleteTask', todos.id)"
    > &#x2716; 
    </button>
  </li>
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