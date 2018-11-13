<template>
<div id="app">
  <div class="container">
    <div class="row pen-title">
      <div class="col">
        <h3 class="title">{{title}}</h3>
      </div>
      <div class="col col-auto align-self-center text-right">
        <div class="input-group">
          <div class="input-group-prepend">
            <label class="input-group-text" for="inputGroupSelect01"># of People</label>
          </div>
          <input class="form-control" type="text" v-model='quantity'>
          <div class="input-group-append">
            <button class="btn btn-primary" v-on:click="getPeople">Refresh List</button>
          </div>
        </div>
      </div>
    </div>
    <div class="row">
      <div v-for="person in people" :key="person" class="col-md-6 col-lg-4">
         <transition name="fade">
        <div class="person">
          <div class="person__header">
            <img v-bind:src="person.picture.large" v-bind:alt="person" class="rounded img-thumbnail">
            <div class="person__name">{{person.name.first}} {{person.name.last}}</div>
          </div>
          <div class="person__email">
            <a v-bind:href="'mailto:' + person.email">{{person.email}}</a>
          </div>
          <div class="person__address">
            <address>
              {{person.location.street}}
              {{person.location.city}}
              {{person.location.state}}
            </address>
          </div>
          <div class="person__map">
            <iframe width="100%" height="170" frameborder="0" scrolling="no" marginheight="0" marginwidth="0" v-bind:src="'https://maps.google.com/maps?q=' + person.location.coordinates.latitude +',' + person.location.coordinates.longitude + '&z=7&amp;output=embed'">
            </iframe>
          </div>
        </div>
           </transition>
      </div>

    </div>
  </div>
</div>


  
</template>
 
<script>



export default {
  
  name: 'app',
  data () {
    return {
    title: "Find Random Users",
    people: [],
    quantity: 0
   
    }
  },
  
      methods: {

    getPeople: function () { 
      this.people = [];
      axios.get('https://randomuser.me/api/?results=' + this.quantity)
      .then((rsp)=>{
        this.people = rsp.data.results;
      })
   }
  },
  created: function () {
    this.getPeople();
  } 
}



</script>

<style>
#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
}
body {
  background-image: url("https://images.pexels.com/photos/255379/pexels-photo-255379.jpeg?auto=compress&cs=tinysrgb&dpr=2&h=650&w=940");
}

.pen-title {
  margin: 36px 0;
  color: #fff;
  padding-bottom: 36px;
  border-bottom: 1px solid #999;
}
  
  .title{
    text-shadow: 2px 2px 2px rgba(0, 0, 0, 0.7);
  }

.person {
  background: radial-gradient(ellipse at center, #ffffff 0%, #e5e5e5 100%);
  border: 1px solid #666;
  border-radius: 4px;
  margin-bottom: 30px;
  text-align: center;
  box-shadow: 5px 5px 5px rgba(0, 0, 0, 0.2);
}

  header {
    font-size: 24px;
    text-transform: capitalize;
    margin: 15px 0 30px;
  }

  map {
    background: white;
    border: 2px solid #88b5de;
    border-radius: 5px;
    padding: 5px 5px 0;
    margin: 0 15px 15px;
  }


</style>
