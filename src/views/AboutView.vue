<template>
  <div class="about">
   <input type="text" v-model="singlevalue.name" />
   <input type="text" v-model="singlevalue.price" />
   <input type="text" v-model="singlevalue.details" />
  <button type="submit" @click="phoneadd">Submit</button>
  </div>
</template>

<script>
import axios from 'axios'

export default {
 data() {
  return {
   
    singlevalue:{
       name: "",
    price: "",
    details: "",
    }
  }
 },
 methods:{

  async phoneadd(){
    let payload = {
      name:this.singlevalue.name,
      price:this.singlevalue.price,
      details:this.singlevalue.details
    }
    if(this.$route.params.id) {
      await axios.put("http://localhost:4000/api/products/"+this.$route.params.id, payload)
    }
    else{
    try {
     await axios.post("http://localhost:4000/api/products/createproducts", payload)
     alert('success')
    } catch (error) {
      console.log(error)
    }
    }
  },
  async getsingle(){
    try {
     let singledata = await axios.get("http://localhost:4000/api/products/prodkey?productid="+this.$route.params.id )
     this.singlevalue = singledata.data.data;

    } catch (error) {
      console.log(error)
    }
  }
 },

 computed:{
  currentRoute(){
    return this.$route;
  }
 },
 async mounted(){
  if(this.$route.params.id){
    await this.getsingle()
  }
 }
 
}
</script>
