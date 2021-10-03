<template>
    <div class="nav">
        <router-link to="/">Home</router-link>
        <router-link to="/add">Add Restaurant</router-link>
        <a class="right"  @click="logout()">Logout</a>
    </div>
</template>

<script>
export default {
   name:'Header',
   methods:{
       logout(){
           localStorage.clear()
           this.$router.push({name:'Login'})
       }
   }
}
</script>

<style scoped>
.nav {
    background: #50BB7A;
    overflow: hidden; 
}
.nav a {
    padding:  14px;
    text-decoration: none;
    color: #fff;
    float: left;
    font-size: 18px;
}
.nav a:hover{
    background: #fff;
    color: #222;
}

.right {
    float: right !important;
}
</style>
