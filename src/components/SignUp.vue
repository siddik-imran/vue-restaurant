<template>
    <img class="logo" alt="Vue logo" src="../assets/logo.png">
    <h1>Sign Up</h1>

    <div class="register">
        <input type="text" v-model="name" placeholder="Enter Name">
        <input type="email" v-model="email" placeholder="Enter Email">
        <input type="password" v-model="password" placeholder="Enter Password">
        <button @click="signUp()">Sign Up</button>
        <p>
          if you are register?.click here  <router-link to="/login">Login</router-link>
        </p>
    </div>

</template>

<script>

import axios from 'axios'

export default{
    name: 'SignUp',
    data() {
        return {
            name: '',
            email: '',
            password: ''
        }
    },
    methods:{
        async signUp() {
           let result = await axios.post("http://localhost:3000/users", {
               name:this.name,
               email:this.email,
               password:this.password
           });
           console.log(result);
           if(result.status==201){
              localStorage.setItem("user-info",JSON.stringify(result.data))
              this.$router.push({name:'Home'})
           }
           
        }
    },
    mounted() {
        let user = localStorage.getItem('user-info');
        if(user){
            this.$router.push({name:'Home'})
        }
    }
};
</script>

<style>
.logo{
    width: 100px;
}
.register input{
    width: 300px;
    padding: 12px;
    display: block;
    margin-bottom: 30px;
    margin-left: auto;
    margin-right: auto;
    border: 1px solid skyblue;
}
.register button {
    padding: 12px 34px;
    font-size: 14px;
    background: teal;
    border: none;
    cursor: pointer;
    color: #fff;
}
</style>
