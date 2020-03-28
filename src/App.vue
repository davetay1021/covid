<template>
  <div id="app">
    <div>
      <b-navbar toggleable="lg" type="dark" variant="info">
         <b-navbar-brand href="#">Covid Stats</b-navbar-brand>

         <b-navbar-toggle target="nav-collapse"></b-navbar-toggle>

         <b-collapse id="nav-collapse" is-nav>
             <b-navbar-nav>
         </b-navbar-nav>

         <!-- Right aligned nav items -->
         <b-navbar-nav class="ml-auto">
            <b-nav-item-dropdown text="Countries" right>
                <b-dropdown-item v-on:click="load('USA')">USA</b-dropdown-item>
                <b-dropdown-item v-on:click="load('Italy')">Italy</b-dropdown-item>
                <b-dropdown-item v-on:click="load('China')">China</b-dropdown-item>
                <b-dropdown-item v-on:click="load('UK')">UK</b-dropdown-item>
                <b-dropdown-item v-on:click="load('Canada')">Canada</b-dropdown-item>
                <b-dropdown-item v-on:click="load('Mexico')">Mexico</b-dropdown-item>
                <b-dropdown-item v-on:click="load('Russia')">Russia</b-dropdown-item>
                <b-dropdown-item v-on:click="load('Spain')">Spain</b-dropdown-item>
                <b-dropdown-item v-on:click="load('Brazil')">Brazil</b-dropdown-item>
            </b-nav-item-dropdown>
         </b-navbar-nav>
         </b-collapse>
         </b-navbar>
     </div>
    <router-view ref="childViews" />
  </div>
</template>

<script>

export default {
    methods: {
        load(code) {
            this.$refs.childViews.loadCountry(code)
        }
    }
}

</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
}

#nav {
  padding: 30px;
}

#nav a {
  font-weight: bold;
  color: #2c3e50;
}

#nav a.router-link-exact-active {
  color: #42b983;
}
</style>
