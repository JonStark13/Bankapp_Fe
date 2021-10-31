<template>
    <div v-if="loaded" class="information">
        <h1>Account Information</h1>
        <h2>Name: <span>{{name}}</span></h2>
        <h2>Balance: <span>{{balance}}</span></h2>
        <h2>Email: <span>{{email}}</span></h2>
    </div>
</template>

<script>
import jwt_decode from "jwt-decode";
import axios from 'axios';

export default {
    name: "Account",

    data: function(){
        return{
            name: "",
            email: "",
            balance: 0,
            loaded: false,
        }
    },

    methods: {
        getData: async function(){
            if (localStorage.getItem("token_access")===null||localStorage.getItem("token_refresh")===null){
                this.$emit('logOut');
                return;
            }

            await this.verifyToken();
            let token = localStorage.getItem("token_access");
            let userId = jwt_decode(token).user_id.toString();

            axios.get(`https://p65.herokuapp.com/user/${userId}/`, {headers: {'Authorization' :
                `Bearer ${token}`}})
                .then((result)=> {
                    this.name  = result.data.name;
                    this.email = result.data.email;
                    this.balance = result.data.balance;
                    this.loaded = true;
                    })
                .catch(()=>{
                    this.$emit('logOut');
                });
        }
    },

    created: async function(){
        this.getData();
    },

}
</script>
<style>
    .information{
        margin: 0;
        padding: 0%;
        width: 100%;
        height: 100%;

        display: flex;
        flex-direction: column;
        justify-content: center;
        align-items: center;
    }

    .information h1{
        font-size: 60px;
        color: #0F1316;
    }

    .information h2{
        font-size: 40px;
        color: rgba(6, 53, 37, 0.7);
    }

    .information span{
        color: brown;
        font-weight: bold;
    }
</style>
