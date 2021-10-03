<template>
    <Header></Header>
    <h2>Update Restaurant Info</h2>
    <form class="register">
        <input type="text" v-model="restaurant.name" placeholder="Name">
        <input type="text" v-model="restaurant.address" placeholder="Address">
        <input type="text" v-model="restaurant.contact" placeholder="Contact">
        <button @click.prevent="updateRestaurant()">Update</button>
    </form>
</template>

<script>
import Header from './Header.vue'
import axios from 'axios'
export default {
   name: "Update",
   components:{
       Header
   },
    data(){
       return{
           restaurant:{
               name:'',
               address:'',
               contact:''
           }
       }
   },
   methods:{
      async updateRestaurant(){
           const result = await axios.put("http://localhost:3000/restaurants/"+this.$route.params.id,{
               name:this.restaurant.name,
               address:this.restaurant.address,
               contact:this.restaurant.contact
           });
           if(result.status == 200){
               this.$router.push({name:'Home'});
           }
       }
   },
    async mounted() {
        let user = localStorage.getItem('user-info')
        if(!user){
            this.$router.push({name:'SignUp'})
        }
        let result = await axios.get('http://localhost:3000/restaurants/'+this.$route.params.id)
        this.restaurant = result.data
    }
};
</script>
