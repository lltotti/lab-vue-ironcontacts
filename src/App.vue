<script setup>
// This starter template is using Vue 3 <script setup> SFCs
// Check out https://v3.vuejs.org/api/sfc-script-setup.html#sfc-script-setup

 import contacts from "./contacts.json";
 import {ref,reactive} from "vue";

 const myContacts = Object.values(contacts);
 const fiveContacts = reactive(myContacts.slice(0,5));
 const restContacts = reactive(myContacts.slice(5,myContacts.length));
 
 function getRandom(){
   const endIndex=restContacts.length;
   if(endIndex>0){
     const index =Math.floor(Math.random() * (endIndex-1));
     fiveContacts.push(restContacts[index]);
     const x =restContacts.splice(index,1);
     console.log("Indice:"+index);
     console.log(x[0].name);
     
   }
 }

function sortPopularity(){
  fiveContacts.sort((a, b) => {
    if(Number(a.popularity.toFixed(2)) < Number(b.popularity.toFixed(2))) {
      return 1;
    }
  if(Number(a.popularity.toFixed(2)) > Number(b.popularity.toFixed(2))) {
      return -1;

    }
   
  })
}

function sortName(){
  fiveContacts.sort((a, b) => {
    return a.name.localeCompare(b.name);
  })
}

function deleteRow(nombre){
  const indexOf = fiveContacts.findIndex( (element) => element.name === nombre);
  console.log(nombre);
  console.log(indexOf);
  restContacts.push(fiveContacts[indexOf]);
  fiveContacts.splice(indexOf,1);

}


</script>

<template>
  <!-- <img alt="Vue logo" src="./assets/logo.png" /> -->
  <!-- <HelloWorld msg="Hello Vue 3 + Vite" /> -->
  <h1>IronContacts</h1>
  <!-- {{myContacts[0]}} -->
  <p>Contacts: {{fiveContacts.length}}</p> 
  <button @click="getRandom"> Add random contact</button>
  <button @click="sortName" style="margin:10px;"> Sort by name</button>
  <button @click="sortPopularity"> Sort by popularity</button>
  <table style="margin-left: auto;  margin-right: auto;">
    <tr>
      <th style="padding:10px;">Picture</th>
      <th style="padding:10px;">Name</th>
      <th style="padding:10px;">Popularity</th>
      <th style="padding:10px;">Won an Oscar</th>
      <th style="padding:10px;">Won an Emmy</th>
      <th style="padding:10px;">Actions</th>
    
    </tr>
    <tr v-for="cont in fiveContacts" :key="cont.name" :id="cont.name">
      <td style="padding:10px;"><img :src="cont.pictureUrl" style="width:60px;"></td>
      <td style="padding:10px;" >{{cont.name}}</td>
      <td style="padding:10px;">{{cont.popularity.toFixed(2)}}</td>
      <td style="padding:10px;">{{cont.wonOscar ? "🏆":" "}}</td>
      <td style="padding:10px;">{{cont.wonEmmy ?  "🏆":" "}}</td>
      <td style="padding:10px;"><button @click="deleteRow(cont.name)"> Delete</button></td>
    </tr>
  </table>
</template>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}


</style>
