<template>
  <div id="app">

    <div id="header" class="default-border">
      <div id="logo">
        <img alt="Vue logo" src="./assets/logo.png">
      </div>
      <div>Customer Program</div>
    </div>
    <div id="content">
      <div id="users-left-panel" class="default-border">
        <div class="user-card default-border" v-for="user in users" v-bind:key="user.id"
             @click="getUserInfo(user.id)">
          <div id="user-name">{{user.name}}</div>
          <div></div>
          <div>Vorige afspraak: 2021-02-07</div> <!--          todo hier hoort datum laatste afspraak-->
        </div>

      </div>

      <div id="user-page" class="default-border">
        <div id="user-general">
          <div>Naam:</div>
          <div>Telefoonnummer:</div>
          <div>Doorverwezen via:</div>
        </div>
<!--        No user profile to show...-->
      </div>
    </div>

<!--    <img alt="Vue logo" src="./assets/logo.png">-->
<!--    <HelloWorld msg="Welcome to Your Vue.js App"/>-->
  </div>
</template>

<script>
// import HelloWorld from './components/HelloWorld.vue'

export default {
  name: 'App',
  data: function () {
    return {
      users: 'loading',
    };
  },
  components: {
    // HelloWorld
  },
  created() {
    this.getUsersFromApi();
  },
  methods: {
    getUsersFromApi() {
      //infos to test with a lot of cards:
      // fetch('https://jsonplaceholder.typicode.com/comments')
      fetch('https://jsonplaceholder.typicode.com/users')
          .then(response => response.json())
          .then(json => {
                console.log(json);
                this.users = json;
              }
          )
    },
    getUserInfo(userId) {
      console.log("clicked on User:" + userId)
    }
  }

}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  /*text-align: center;*/
  /*color: #2c3e50;*/

  display: flex;
  flex-direction: column;

  /*height: 100vh;*/
  /*position: absolute;*/
  /*top: 40px; !* Header Height *!*/
  /*bottom: 20px; !* Footer Height *!*/
  /*height: 100%;*/
}
#header {
  display: flex;
  justify-content: center;
  align-items: center;
  line-height: 80px;
  height: 80px;
  margin: 2px;

  background-color: lightgreen;

  font-size: 34px;
  font-weight: bold;
}
#header img {
  max-height:80px;
  display: block;
  margin: 0 auto;
}
#content {
  display: flex;
  align-items: stretch;
  margin: 2px;
  height: calc(100vh - 80px);
}
#users-left-panel {
  flex-grow: 2;
  max-width: 400px;
  margin-right: 2px;
  padding: 2px;
  background-color: #f1f1f1;

  overflow:hidden;
  overflow-y: scroll;
}
#user-page {
  flex-grow: 5;
  background-color: #f1f1f1;

  padding: 2px;
}
#user-name {
  font-weight: bold;
}
.default-border {
  border-style: solid;
  border-radius: 5px;
  border-width: 2px;
  border-color: gray;
}
.user-card {
  margin: 4px 5px 5px;
  padding: 5px;
  background-color: white;
  height: 50px;

  display: flex;
  flex-direction: column;

  box-shadow: 3px 3px 3px black;

  cursor: pointer;
}
.user-card:hover {
  background-color: lightgreen;
}
.user-card div{
  flex-grow: 1;
  align-self: flex-start
}


#user-general {
  display: grid;
  grid-template-rows: auto auto auto;
}
</style>
