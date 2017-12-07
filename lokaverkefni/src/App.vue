<template>
  <div id="app">
  <div class="field half first" id="spacebtw">
    <input class="input" id="inputval" type="text"> <a @click="pressbtn" class="button is-dark" id="btn1">Búa til</a>
  </div>
    <span id="titlecheck">Staða</span>
    <span id="titleid">Id</span>
    <span id="titlevrkf">Verkefni</span>
    <span id="titlecreated">Búið til</span>

    <div class="box is-active" v-for="task in tasks">
      <h1>
        <input @click="updateStatus(task.id)" :checked="task.completed"  id="checkbutton" type="checkbox">
        <span id="idtag">{{task.id}}</span>
        <label v-bind:class="{inputline:task.completed}" id="titletag">{{task.title}}</label>
        <span id="createdtag">{{task.created}}</span>
      </h1>
    </div>
  </div>
</template>

<script>
import axios from 'axios';
export default {
  name: 'app',
  data () {
    return {
      clicked:true,
      tasks:[],
    }
  },
  computed:{

  },
  methods:{
    updateStatus:function(id){
    axios.post('http://fjolbraut.org/api/tasks/' + id + '/status?api_token=vRy0Yz09n3bKlcqvag4tMCqXIuNTYd8X1AxmsKtnHNPp6Nk6x5pxPAyRo1E2')
    .then(function(response) {
      console.log(response);
      })
    .catch(function(error) {
        console.log(error);
      });
    },
    pressbtn:function(){
    var valinput = document.getElementById('inputval').value 
    axios.post('http://fjolbraut.org/api/tasks?api_token=vRy0Yz09n3bKlcqvag4tMCqXIuNTYd8X1AxmsKtnHNPp6Nk6x5pxPAyRo1E2',{
      title: valinput
    })
    .then(function(response) {
      console.log(response);
      })
    .catch(function(error) {
        console.log(error);
      });
    }
  },
  mounted(){
    var that = this;
    axios.get('http://fjolbraut.org/api/tasks?api_token=vRy0Yz09n3bKlcqvag4tMCqXIuNTYd8X1AxmsKtnHNPp6Nk6x5pxPAyRo1E2')
    .then(function(response) {
    that.tasks = response.data
    console.log(that.tasks)
    })
    .catch(function(error) {
      console.log(error);
    });
  }
}
</script>
<style>
body{
  padding-left:30%;
  padding-top: 20%;
}
#checkbutton{
  color:blue;
  cursor: pointer;
}
#idtag{
  padding-left: 24%;
}
#titletag{
  padding-left: 25%;
}
#createdtag{
  float: right
}
.box{
  width: 60%;
}
#titleid{
  padding-left: 13.5%;
}
#titlevrkf{
  padding-left:14.5%;
}
#titlecreated{
  padding-left:13%; 
}
.input{
  width:20%;
}
.input:focus{
  border-color: #ADD8E6;
}
#btn1{
  border-radius: 20px;
  width:10%;
  padding: 10px;
  text-overflow: ellipsis;
}
#btn1:hover{
  background-color:#ADD8E6;
}
#spacebtw{
  margin-bottom: 2%;
}
.inputline{
  text-decoration: line-through;
}
</style>
