<template>
  <li >
    <input type="checkbox" 
    
    v-on:click="$emit('checBoxTask', item.id)"
    v-bind:checked="item.complited"
    /> 
    <span>{{ item.title }}</span>
    <button
    
    v-on:click="$emit('deleteTask', item.id)"
    > &#x2716; </button>
  </li>
</template>

<script>
export default {
  props: 
  ['todos'], 
  
  components: {
    

  }
}

</script>