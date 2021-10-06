<template>
  <div id="app">
    <!-- <div id="nav">
      <router-link to="/">Home</router-link> |
      <router-link to="/about">About</router-link> |
      <router-link to="/SignUp">Sign Up</router-link>

    </div> -->
    <div>
  <b-navbar type="dark" variant="dark">
    <b-navbar-nav>
      <b-nav-item router-link to="/">Home</b-nav-item>
      <b-nav-item router-link to="/signup" v-show="!user">Log In</b-nav-item>
      <b-nav-item router-link to="/" @click="signoutButtonPressed" v-show="user">Log Out</b-nav-item>

      <!-- Navbar dropdowns -->
      <!-- <b-nav-item-dropdown text="Lang" right>
        <b-dropdown-item href="#">EN</b-dropdown-item>
        <b-dropdown-item href="#">ES</b-dropdown-item>
        <b-dropdown-item href="#">RU</b-dropdown-item>
        <b-dropdown-item href="#">FA</b-dropdown-item>
      </b-nav-item-dropdown> -->

      <b-nav-item-dropdown text="User" right>
        <b-dropdown-item router-link to="/account">Account</b-dropdown-item>
        <!-- <b-dropdown-item href="#">Settings</b-dropdown-item> -->
      </b-nav-item-dropdown>
    </b-navbar-nav>
  </b-navbar>
</div>
    <router-view/>
  </div>
</template>

<script>
import firebase from 'firebase/compat/app';
import 'firebase/compat/auth';

export default {
    data() {
        return {
            user: null
        };
    },
    created() {
        firebase.auth().onAuthStateChanged(user => {
            this.user = user;
        });
        console.log("Current User: ", this.user);
    },
    methods: {
        signoutButtonPressed(e) {
            e.stopPropagation();
            firebase.auth().signOut();
            this.$router.push({ name: "Login" });
        }
    }
};
</script>

<style>
#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
