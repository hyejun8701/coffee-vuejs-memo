<template>
  <div id="app">
    <v-app style="backgroundColor:#f5f5f5;">
      <app-header />
      <memo-app @change="updateMemoCount" />
    </v-app>
  </div>
</template>

<script>
import AppHeader from './components/AppHeader'
import MemoApp from './components/MemoApp'

export default {
  name: 'app',
  components: {
    AppHeader,
    MemoApp
  },
  data () {
    return {
      memoCount: 0,
    }
  },
  methods: {
    updateMemoCount (count) {
      this.memoCount = count
    }
  }
}
</script>

<style>
@import "./styles/reset.css";

#app {
  width: 560px;
  margin: 0 auto;
}
</style>
