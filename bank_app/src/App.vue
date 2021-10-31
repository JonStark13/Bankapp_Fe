<template>
  <div id="app" class="app">
    <div class="header">
      <h1>Tokio II Bank</h1>
      <nav>
        <button v-if="is_auth" v-on:click="loadHome">Home</button>
        <button v-if="is_auth" v-on:click="loadAccount">Account</button>
        <button v-if="is_auth" v-on:click="logOut">Log Out</button>
        <button v-if="!is_auth" v-on:click="loadLogIn">Log In</button>
        <button v-if="!is_auth" v-on:click="loadSignUp">Sign In</button>
      </nav>
    </div>
  </div>

  <div class="main-component">
    <router-view
      v-on:completedLogIn="completedLogIn"
      v-on:completedSignUp="completedSignUp"
      v-on:logOut="logOut"
    >
    </router-view>
  </div>

  <div class="footer">
    <h2>NERV 2014</h2>
  </div>

</template>

<script>

export default {

  name: 'App',
  data: function(){
    return{
      is_auth: false
    }
  },
  components:{ 
  },
  methods:{
    verifyAuth: function(){
      this.is_auth = localStorage.getItem("isAuth")||false;

      if(this.is_auth==false)
        this.$router.push({name: "logIn"});
      else
        this.$$router.push({name: "home"});
    },

    loadLogIn: function(){
      this.$router.push({name: "logIn"})
    },

    loadSignUp: function(){
      this.$router.push({name: "signUp"})
    },

    completedLogIn: function(data) {
      localStorage.setItem("isAuth", true);
      localStorage.setItem("username", data.username);
      localStorage.setItem("token_access", data.token_access);
      localStorage.setItem("token_refresh", data.token_refresh);
      alert("Success");
      this.verifyAuth();
    },

    completedSignUp: function(data) {
      alert("SignUp completed");
      this.completedLogIn(data);
    },

    loadHome: function(){
      this.$router.push({name: "home"})
    },

    logOut: function(){
      localStorage.clear();
      alert("LogOut Success");
      this.verifyAuth();
    },

    loadAccount: function(){
      this.$router.push({name: "account"});
    },

  },
  created: function(){
    this.verifyAuth
  }

}
</script>

<style>
  body{
    margin: 0 0 0 0;
  }

  .header{
    margin: 0;
    padding: 0;
    width: 100%;
    height: 10vh;
    min-height: 10px;

    background-color: rgba(6, 53, 37, 0.7);
    color: #E5E7E9;
    display: flex;
    justify-content: space-between;
    align-items: center;
  }

  .header h1{
    width: 20%;
    text-align: center;
  }

  .header nav{
    height: 100%;
    width: 20%;

    display: flex;
    justify-content: space-around;
    align-items: center;

    font-size: 20px;
  }

  .header nav button{
    color: #E5E7E9;
    background-color: rgba(6, 53, 37, 0.7);
    border: 1px solid #E5E7E9;

    border-radius: 5px;
    padding: 10px 20px;
    font-size: 12px;
  }

  .header nav button:hover{
    color: rgba(6, 53, 37, 0.7);
    background-color: #E5E7E9;
    border: 1px solid #E5E7E9;
  }

  .main-component{
    height: 75vh;
    margin: 0%;
    padding: 0%;

    background-color: #FDFEFE;
  }

  .footer{
    margin: 0;
    padding: 0;
    width: 100%;
    height: 10vh;
    min-height: 100px;

    background-color: rgba(6, 53, 37, 0.7);
    color: #E5E7E9;
  }

  .footer h2{
    width: 100%;
    height: 100%;

    display: flex;
    justify-content: center;
    align-items: center;
  }
</style>
