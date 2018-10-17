<template>
  <div class="container" id="app">
    <ItemSelection v-on:itemChanged="itemChanged"></ItemSelection>
    <Itemlist v-bind:item="item"></Itemlist>
  </div>
</template>

<script>
import ItemSelection from './components/ItemSelection'
import Itemlist from './components/Itemlist'

export default {
  name: 'app',
  components: {
    ItemSelection,
    Itemlist
  },
  data(){
    return {
      item:""
    }
  },
  methods:{
    itemChanged: function(item){
      this.item = item;
      console.log(item);
    }
  }
}
</script>

<style>
#app {
  padding-top: 20px;
}
</style>
