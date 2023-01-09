<template>
<div>
  <div v-for="(item,index) in viewdata" :key="'item-' + index" class="home">
    <p>name: {{item.name}}</p>
    <br />
    <p>phone: {{item.price}}</p>
     <br />
    <p>details: {{item.details}}</p>
    <button @click="updatebutton(item)">Update</button>
    <button @click="deletebutton(item)">Delete</button>
  </div>

 
</div>
</template>

<script>
import axios from 'axios'


export default {
 data() {
  return {
    viewdata: ""
  }
 },
 methods:{
  async getdata(){
   let payload = await axios.get("http://localhost:4000/api/products")
   this.viewdata = payload.data;
   console.log(this.viewdata)
  },
  async updatebutton(item){
    this.$router.push({ name: "about",params:{id:item._id}});

  },
  async deletebutton(item){
    await axios.delete("http://localhost:4000/api/products/"+item._id)

    await this.getdata()
  }
 },
 mounted(){
  this.getdata()
 }
}
</script>
