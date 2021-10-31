<template>
    <div class="greetings">
        <h1>¡Bienvenido <span>{{username}}</span>!</h1>
    </div>
</template>

<script>
export default {
    name: "Home",

    data: function(){
        return{
            username: localStorage.getItem('username')||"none"
        }
    }
}
</script>

<style>
    .greetings{
        margin: 0;
        padding: 0%;
        height: 100%;
        width: 100%;

        display: flex;
        justify-content: center;
        align-items: center;
    }

    .greetings h1{
        font-size: 50px;
        color: rgba(6, 53, 37, 0.7);
    }

    .greetings span{
        color: brown;
        font-weight: bold;
    }
    
</style>