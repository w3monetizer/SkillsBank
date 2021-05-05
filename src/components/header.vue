<template>
  <header id="header">
    <div class="left">
      <router-link to="/"><img id="logo" src="../assets/icon_154-white.png"><span @click="
      $store.getters.isPaused ?
      $store.commit('togglePause',{value:false,src:'header'}):
      $store.commit('togglePause',{value:true,src:'header'})
      "
      title="Agile | AI">{{ $store.getters.isPaused ? 'Agile' : 'AI' }}</span></router-link>
    </div>
    <div class="center">
      <router-link to="/"><span title="Ideator > Automator > Monetizer" @click="$store.commit('nextView')">{{ $store.getters.view }}</span></router-link>
    </div>
    <nav class="right">
      <ul>
        <li v-if="!auth">
          <router-link to="/signup">sign up</router-link>
        </li>
        <li v-if="!auth">
          <router-link to="/signin">sign in</router-link>
        </li>
        <li v-if="auth">
          <router-link to="/dashboard">web</router-link>
        </li>
        <li v-if="auth">
          <button @click="onLogout" class="logout">logout</button>
        </li>
      </ul>
    </nav>
  </header>
</template>

<script>
export default {
  computed: {
    auth() {
      return this.$store.getters.isAuthenticated;
    },
    isPaused() {
      return this.$store.getters.isPaused;
    }
  },
  methods: {
    onLogout() {
      this.$store.dispatch("logout");
    }
  },
};
</script>

<style scoped>
#header {
  height: 56px;
  display: flex;
  flex-flow: row;
  justify-content: space-between ;
  align-items: center;
  background-color: #6aa84f;
  padding: 0 20px 1px 20px;
}

#logo {
  height: 56px;
  width: 56px;
  margin-bottom: 22px;
}

.left {
  width: 33%;
  font-size: 73px;
  font-weight: bold;
  color: white;
  cursor: pointer;
}

.left a {
  text-decoration: none;
  color: white;
}

.center {
  text-align: center;
  width: 33%;
  font-size: 73px;
  font-weight: bold;
  color: white;
  cursor: pointer;
  /* margin-left: 7rem; */
}

.center a {
  text-decoration: none;
  color: white;
}

.right {
  width: 33%;
  display: flex;
  flex-flow: row;
  justify-content: flex-end ;
}

nav {
  height: 100%;
}

ul {
  list-style: none;
  margin: 0;
  padding: 0;
  height: 100%;
  display: flex;
  flex-flow: row;
  align-items: center;
}

li {
  margin: 0 16px;
  cursor: pointer;
}

li a {
  text-decoration: none;
  color: white;
}

li a:hover,
li a:active,
li a.router-link-active {
  color: #333;
}

.logout {
  background-color: transparent;
  border: none;
  font: inherit;
  color: white;
  cursor: pointer;
}
</style>