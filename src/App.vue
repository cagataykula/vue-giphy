<template>
  <div id="app">
    <div id="nav">
      <router-link to="/">Trends</router-link> |
      <router-link to="/search">Search</router-link>
    </div>
    <router-view/>
  </div>
</template>

<style>
#app {
  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: center;
  padding: 20px;
  flex-wrap: wrap;
}
</style>
