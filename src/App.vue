<template>
  <div id="app">
    <header>
      <div class="title">{{title}}</div>
    </header>

    <section class="main-content w-50 mx-auto">
      <main-navigation @changeList="changeContent"></main-navigation>
      <windows-list v-if="id === 'Windows'"></windows-list>
      <rooms-list v-if="id === 'Rooms'"></rooms-list>
    </section>
  </div>
</template>

<script>
import MainNavigation from './components/MainNavigation.vue';
import WindowsList from './components/WindowsList.vue';
import RoomsList from './components/RoomsList.vue';

export default {
  name: 'App',
  components: {
    MainNavigation,
    WindowsList,
    RoomsList
  },
  data: function() {
    return {
      title: 'My App Title',
      id: 'Windows'
    }
  },
  methods: {
    changeContent(value) {
      this.id = value;
    }
  }
}
</script>

<style lang="scss" scoped>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}

</style>
