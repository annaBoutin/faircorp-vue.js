<template>
  <ul class="nav nav-tabs">
    <li class="nav-item">
      <a class="nav-link" aria-current="page" href="#" @click="changeWindow">Windows</a>
    </li>
    <li class="nav-item">
        <a class="nav-link" href="#" tabindex="-1" aria-disabled="true" @click="changeRoom">Rooms</a>
    </li>
  </ul>
</template>


<script>
export default {
  name: 'MainNavigation',
  data: function() {
    return {
      test: 'Test 1'
    }
  },
  methods: {
    changeRoom() {
      this.$emit('changeList','Rooms');
    },
    changeWindow() {
      this.$emit('changeList','Windows');
    }
  }
}
</script>
