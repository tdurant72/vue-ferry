<template>
  <div class="itemlist">
    <div class="container">
        <!-- <h4>{{items.VesselName}}</h4> -->
        <ul class="media-list">
            <li class="media" v-for="item in items " :key="item.VesselID">
                <div class="align-content-center">
                    <a v-bind:href="item.VesselName" target="_blank">{{item.VesselName}}
                         <!-- <img class="media-object" v-bind:src="items.urlToImage">  -->
                    </a> 
                
                    <p>
                        <a v-bind:href="item.DepartingTerminalName" target="_blank">{{item.DepartingTerminalName}}</a>
                    </p>
                    <p >
                        <a v-bind:href="item.ArrivingTerminalName" target="_blank">{{item.ArrivingTerminalName}}</a>
                    </p>
                    <p>{{item.Latitude}}</p> 
                    <p>{{item.Longitude}}</p>
                </div>
            </li>
        </ul> 
    </div>
  </div>
</template>

<script>
export default {
  name: 'itemlist',
  props:['item'],
  data () {
    return {
      items:{},
      filteredID: ''
    }
  },
  methods:{
      updateSource: function(item){
          var proxy = 'https://cors-anywhere.herokuapp.com/';
          this.$http.get(proxy+'http://www.wsdot.wa.gov/Ferries/API/Vessels/rest/vessellocations/'+item+'?apiaccesscode=80e61cf4-541b-4651-8228-6376d80567f7')
        //   https://newsapi.org/v1/items?source=bbc-news&apiKey=8170f791ac1b49c8be33ed3e7a1346f3
          .then( response => {
            //   console.log(response.data);
              this.items = response.data;
              console.log(response.data);
          });
      },
      filterItems:function(item){
          this.filteredID = item.VesselID;
      },
      initialSource: function(){
          var proxy = 'https://cors-anywhere.herokuapp.com/';
          this.$http.get(proxy+'http://www.wsdot.wa.gov/Ferries/API/Vessels/rest/vessellocations?apiaccesscode=80e61cf4-541b-4651-8228-6376d80567f7')
          .then(response =>{
              this.items = response.data;
          });
      }
  },
  created: function(){
      this.initialSource(this.items);
  },
  watch:{
      item: function(val){
          this.filterItems(val);
      }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
    .media-object{
        width: 128px;
        padding: 10px;
    }
    .media{
        border-top: 1px solid lightgray;
        padding-top: 20px;
    }
    .media-list{
        padding: 0;
    }
    h4{
        font-size: 1.1em;
    }
</style>