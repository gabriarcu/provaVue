<template>
  <!-- <nav>
    <router-link to="/">Home</router-link> |
    <router-link to="/about">About</router-link>
  </nav> -->
  <router-view />
  <v-layout>
    <v-bottom-navigation>
      <v-btn value="home"  to="/">
        <v-icon>mdi-home</v-icon>

        <span>Home</span>
      </v-btn>

      <v-btn value="stat" to="/statistiche">
        <v-icon>mdi-finance</v-icon>

        <span>Statistiche</span>
      </v-btn>

      <!-- <v-btn value="nearby">
        <v-icon>mdi-map-marker</v-icon>

        <span>Nearby</span>
      </v-btn> -->
    </v-bottom-navigation>
  </v-layout>
</template>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  background-color: black
}

nav {
  padding: 30px;
}

nav a {
  font-weight: bold;
  color: #2c3e50;
}

nav a.router-link-exact-active {
  color: #42b983;
}
</style>
