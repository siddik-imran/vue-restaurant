<template>
    <Header></Header>
    <h2>Hello {{ name }}, Welcome Home</h2>
    <table border="1px">
        <tr>
            <td>Sl No.</td>
            <th>Name</th>
            <th>Address</th>
            <th>Contact</th>
            <th>Actions</th>
        </tr>
        <tr v-for="(item, i) in restaurants" :key="item.id">
            <td>{{ i+1 }}</td>
            <td>{{ item.name }}</td>
            <td>{{ item.address }}</td>
            <td>{{ item.contact }}</td>
            <td>
                <router-link :to="'/update/'+item.id">Edit | </router-link>
                <button @click.prevent="deleteRestaurant(item.id)">Delete</button>
            </td>
        </tr>
    </table>
</template>

<script>
import axios from 'axios'
import Header from './Header.vue'
export default {
   name: "Home",
   data(){
       return{
           name:'',
           restaurants:[],
       }
   },
   components:{
       Header
   },
    methods:{
      async deleteRestaurant(id){
        //   console.log('delete')
           let result = await axios.delete("http://localhost:3000/restaurants/"+id)
           if(result.status == 200){
               this.loadData()
           }
       },
       async loadData(){
            let user = localStorage.getItem('user-info');
            this.name = JSON.parse(user).name
            if(!user){
                this.$router.push({name:'SignUp'})
            }
            let result = await axios.get("http://localhost:3000/restaurants");
            this.restaurants = result.data
       }
   },
    async mounted() {
        this.loadData();
    }
};
</script>
<style scoped>
table{
    margin-top: 20px;
    margin-left: auto;
    margin-right: auto;
}
th{
     padding: 5px;
}
td{
    width: 200px;
    padding: 5px;
}
</style>