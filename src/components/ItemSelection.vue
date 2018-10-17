<template>
  <div  class="itemselection">
      <div class="jumbotron">
          <h2><span class="glyphicon glyphicon-list-alt"</span> Ferry List</h2>
          
        <h4>Select a item</h4>
        <select class="form-control" id="" v-on:change="itemChanged">
            <option v-bind:value="item.VesselID" v-for="item in items" :key="item.VesselID">{{item.VesselName}}</option>
        </select>
        <div v-if="item">
            <!-- <h6>{{item.description}}</h6> -->
            <a v-bind:href="item.VesselID" class="btn btn-primary" target="_blank">View vessel {{item.VesselName}}  information</a>
        </div>

    </div>
  </div>
</template>

<script>
export default {
  name: 'itemselection',
  data () {
      return{
            items: [],
            item:'',
      }
  },
  methods:{
      itemChanged: function(e){
          for (var i=0; i<this.items.length; i++) {
              if(this.items[i].VesselID== e.target.value){
                //   console.log(items[i]);
                  this.item = this.items[i];
                //   console.log(item);
              }
          }
          this.$emit('itemChanged', e.target.value);
        //   console.log(items);
      }
  },
  created: function(){
      var proxy = 'https://cors-anywhere.herokuapp.com/';
      var API_URL = 'http://www.wsdot.wa.gov/Ferries/API/Vessels/rest/vessellocations';
      var API_KEY = '?apiaccesscode=80e61cf4-541b-4651-8228-6376d80567f7'
      this.$http.get(proxy+API_URL+API_KEY)
      .then(response => {
          
          this.items = response.data;
          console.log(response.data);
      })
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
h6{
    padding: 1em 0 1em 0;
}
</style>