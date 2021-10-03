<template>
    <Header></Header>
    <h2>Add Restuarent</h2>
    <form class="register">
        <input type="text" v-model="restaurant.name" placeholder="Name">
        <input type="text" v-model="restaurant.address" placeholder="Address">
        <input type="text" v-model="restaurant.contact" placeholder="01...">
        <button @click.prevent="addRestaurant()" >Save</button>
    </form>
</template>

<script>
import Header from './Header.vue'
import axios from 'axios'
export default {
   name: "Add",
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
       async addRestaurant(){
        //    console.log(this.restaurant.name)
           const result = await axios.post("http://localhost:3000/restaurants",{
               name:this.restaurant.name,
               address:this.restaurant.address,
               contact:this.restaurant.contact
           });
           if(result.status == 201){
               this.$router.push({name:'Home'});
           }
       }
   },
    mounted() {
        let user = localStorage.getItem('user-info');
        if(!user){
            this.$router.push({name:'SignUp'})
        }
    }
};
</script>

<style scoped>

</style>
